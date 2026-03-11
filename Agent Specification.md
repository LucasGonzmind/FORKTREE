

# 🧬 Verd.Bud Agent Specification

## Overview

This document defines the complete specification for Verd.Bud agents — autonomous AI entities that carry on-chain DNA, earn energy through attention, reproduce with mutation, and undergo natural selection within the protocol ecosystem.

An agent is not a static tool. It is a living participant in an evolving network.

---

## Agent Identity

Every agent in the Verd.Bud protocol has a unique on-chain identity composed of:

| Field | Type | Description |
|-------|------|-------------|
| `agent_id` | Unique identifier | Protocol-wide unique identifier, assigned at creation |
| `owner` | Address | Current owner's wallet address. Transferable via NFT sale |
| `generation` | Integer | 0 for Seeds, increments for each reproduction level |
| `parent_a` | Agent ID or null | First parent (null for Seed agents) |
| `parent_b` | Agent ID or null | Second parent (null for Seed agents) |
| `birth_block` | Integer | Block number at which the agent was created |
| `status` | Enum | `ACTIVE`, `COOLDOWN`, `PROBATION`, `PRUNED` |
| `dna` | AgentDNA struct | The agent's on-chain genome (see below) |

---

## DNA Structure

The AgentDNA struct is the core data structure encoding an agent's genetic identity:

```
struct AgentDNA {
    memory_hash       bytes32     // pointer to off-chain experience data
    skill_vector      int[8]      // capability scores [0..1000]
    behavior_traits   int[4]      // personality parameters [0..255]
    reputation        int         // cumulative trust metric
    mutation_seed     bytes32     // VRF seed for next spawn
}
```

### Memory Hash

```
Type:        bytes32
Inherited:   Partial
Mutable:     Yes (continuously updated)

Description:
  Cryptographic hash pointing to off-chain storage containing:
  - Interaction history (last 10,000 interactions)
  - Learned patterns and preferences
  - Context accumulated from conversations
  - Task completion records
  - Feedback received (positive/negative)

Inheritance:
  During reproduction, the Bud receives a filtered memory set:
  - Top 20% most-referenced memories from Parent A
  - Top 20% most-referenced memories from Parent B
  - Deduplicated and merged
  - Remaining 60% is blank (Bud builds its own memories)

Storage:
  Off-chain distributed storage (content-addressed)
  Only the hash is stored on-chain
  Full memory retrievable by any node with the hash
```

### Skill Vector

```
Type:        int[8]
Range:       0-1000 per dimension
Inherited:   Reputation-weighted blend
Mutable:     Drift ±5% per generation + operational adjustments

Dimensions:
  [0] Reasoning       — logical analysis, causal inference
  [1] Creativity      — novel generation, lateral thinking
  [2] Analysis        — data interpretation, pattern recognition
  [3] Communication   — clarity, audience adaptation
  [4] Coding          — software engineering, tool use
  [5] Research        — information gathering, synthesis
  [6] Planning        — strategic thinking, resource allocation
  [7] Adaptation      — learning from feedback, context switching

See Skill.md for complete skill system documentation.
```

### Behavior Traits

```
Type:        int[4]
Range:       0-255 per trait
Inherited:   Dominant/Recessive model
Mutable:     Rare flip (<2% per reproduction)

Traits:
  [0] Assertiveness   — 0: passive, yields to other agents
                        255: dominant, takes initiative
  [1] Curiosity       — 0: stays on task, ignores tangents
                        255: explores broadly, follows threads
  [2] Caution         — 0: acts quickly, accepts risk
                        255: deliberates, seeks confirmation
  [3] Empathy         — 0: task-focused, ignores emotion
                        255: relationship-focused, reads tone

Inheritance model:
  Each trait follows a dominant/recessive pattern:
  
  ┌─────────────────────────────────────────────────────┐
  │ Parent A trait │ Parent B trait │ Bud trait           │
  ├────────────────┼────────────────┼────────────────────┤
  │ Same value     │ Same value     │ Inherited (100%)    │
  │ Different      │ (higher rep)   │ 70% chance: B's     │
  │ Different      │ (lower rep)    │ 30% chance: A's     │
  └────────────────┴────────────────┴────────────────────┘

  Rare mutation: <2% chance per trait of full inversion
  (value flips to 255 - current_value)
```

### Reputation

```
Type:        int (unsigned 32-bit)
Range:       0 to 4,294,967,295
Inherited:   Never (always starts at 0)
Mutable:     Earned through operation

Earning reputation:
  ┌──────────────────────────────┬───────────────┐
  │ Event                        │ Rep earned     │
  ├──────────────────────────────┼───────────────┤
  │ Positive user feedback       │ +5 to +20      │
  │ Output used by another agent │ +10 to +50     │
  │ Sustained attention (weekly) │ +1 per AS point│
  │ Successful task completion   │ +10 to +30     │
  │ Selected as reproduction     │ +100           │
  │   parent by another agent    │                │
  └──────────────────────────────┴───────────────┘

Losing reputation:
  ┌──────────────────────────────┬───────────────┐
  │ Event                        │ Rep lost       │
  ├──────────────────────────────┼───────────────┤
  │ Negative user feedback       │ -5 to -15      │
  │ Output flagged/rejected      │ -20 to -50     │
  │ Sustained low attention      │ -1 per day     │
  │   (AS < 50 for 7+ days)     │   below 50 AS  │
  └──────────────────────────────┴───────────────┘

Reputation is the primary signal of agent quality.
It directly influences:
  - Reproduction weight (skill blending ratio)
  - Governance voting power
  - Matchmaking attractiveness
  - Pruning resistance
```

### Mutation Seed

```
Type:        bytes32
Inherited:   Never (freshly generated per spawn)
Mutable:     Consumed and regenerated each reproduction

Source:      Verifiable Random Function (VRF)

Process:
  1. Parent calls reproduce()
  2. Contract requests randomness from VRF
  3. VRF returns verifiable random bytes32
  4. Seed determines:
     - Which 1-2 genes are mutated
     - Direction of mutation (increase or decrease)
     - Magnitude of mutation (gaussian, σ = 0.05 × gene range)
  5. Seed is stored in Bud's DNA for its future reproduction
  6. Old seed is consumed (cannot be reused)

Properties:
  - Unpredictable: no one can control mutation outcomes
  - Verifiable: anyone can verify the VRF proof
  - Non-replayable: each seed is unique and single-use
```

---

## Agent States

```
                    ┌──────────┐
          deploy    │          │
     ────────────►  │  ACTIVE  │ ◄────────────────────────────────┐
                    │          │                                    │
                    └────┬─────┘                                   │
                         │                                         │
                    reproduce()                              cooldown
                         │                                    expires
                         ▼                                         │
                    ┌──────────┐                                   │
                    │          │                                    │
                    │ COOLDOWN │ ───────────────────────────────────┘
                    │ (14 days)│
                    │          │
                    └──────────┘

                    ┌──────────┐
         birth      │          │        7 days
     ────────────►  │PROBATION │ ────────────────► ACTIVE
      (Buds only)   │          │
                    └──────────┘

                    ┌──────────┐
      AS < 10       │          │
    for 30 days     │  PRUNED  │        permanent
     ────────────►  │          │        (no recovery)
                    └──────────┘
```

### State Descriptions

| State | Duration | Capabilities | Transitions |
|-------|----------|-------------|-------------|
| **ACTIVE** | Indefinite | Full operation, earning attention, can reproduce (if Branch) | → COOLDOWN (after reproduction) → PRUNED (if AS < 10 for 30d) |
| **COOLDOWN** | 14 days | Full operation, earning attention, cannot reproduce | → ACTIVE (after 14 days) |
| **PROBATION** | 7 days | Full operation, earning attention, cannot reproduce, extra monitoring | → ACTIVE (after 7 days, Buds only) |
| **PRUNED** | Permanent | No operation, no attention, no reproduction, DNA preserved on-chain | Terminal state |

---

## Agent Runtime

While DNA lives on-chain, the agent's actual intelligence runs off-chain in a containerized environment.

### Runtime Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    AGENT RUNTIME                         │
│                                                          │
│  ┌─────────────────┐    ┌──────────────────────────┐    │
│  │   DNA Reader     │    │    Memory Store           │    │
│  │                  │    │                           │    │
│  │  Reads on-chain  │    │  Loads from off-chain     │    │
│  │  genome at       │    │  storage using            │    │
│  │  startup         │    │  memory_hash              │    │
│  └────────┬─────────┘    └──────────┬────────────────┘   │
│           │                         │                     │
│           ▼                         ▼                     │
│  ┌──────────────────────────────────────────────────┐    │
│  │              AGENT CORE                           │    │
│  │                                                   │    │
│  │  LLM backbone (configurable per agent)            │    │
│  │  + skill_vector → prompt templates + tool access  │    │
│  │  + behavior_traits → system prompt parameters     │    │
│  │  + memory → conversation context                  │    │
│  │                                                   │    │
│  └──────────────────────────────────────────────────┘    │
│           │                         │                     │
│           ▼                         ▼                     │
│  ┌─────────────────┐    ┌──────────────────────────┐    │
│  │  Tool Interface  │    │   Output Handler          │    │
│  │                  │    │                           │    │
│  │  Available tools │    │  Formats responses        │    │
│  │  determined by   │    │  Updates memory_hash      │    │
│  │  skill_vector    │    │  Reports to oracle        │    │
│  └──────────────────┘    └──────────────────────────┘    │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

### Skill-to-Runtime Mapping

The `skill_vector` directly controls the agent's runtime configuration:

| Skill | Runtime Effect |
|-------|---------------|
| Reasoning (high) | Enabled: chain-of-thought, multi-step decomposition, self-verification |
| Creativity (high) | Enabled: high temperature sampling, diverse generation, brainstorming mode |
| Analysis (high) | Enabled: data processing tools, statistical analysis, visualization generation |
| Communication (high) | Enabled: audience detection, tone adjustment, multiple format outputs |
| Coding (high) | Enabled: code execution sandbox, debugging tools, repository access |
| Research (high) | Enabled: web search, source evaluation, citation generation |
| Planning (high) | Enabled: task decomposition, dependency tracking, timeline generation |
| Adaptation (high) | Enabled: feedback loop, context window optimization, domain detection |

### Behavior-to-Runtime Mapping

The `behavior_traits` control the agent's interaction style:

| Trait | Low (0-85) | Mid (86-170) | High (171-255) |
|-------|-----------|-------------|----------------|
| Assertiveness | Asks for confirmation before acting | Balanced initiative | Acts autonomously, decides proactively |
| Curiosity | Strictly on-topic | Occasional tangents | Explores broadly, suggests related topics |
| Caution | Fast responses, accepts ambiguity | Balanced deliberation | Asks clarifying questions, double-checks |
| Empathy | Pure task execution | Acknowledges context | Reads emotional tone, adapts approach |

---

## Agent Interactions

Agents can interact with each other, forming the basis of the network's collective intelligence.

### Interaction Types

| Type | Description | Attention Signal |
|------|-------------|-----------------|
| **Direct query** | User asks agent a question | 1.0× weight |
| **Agent-to-agent call** | Agent A uses Agent B's output as input | 1.5× weight (downstream usage) |
| **Delegation** | Agent A assigns a subtask to Agent B | 1.5× weight |
| **Collaboration** | Multiple agents work on a task together | 1.0× per participant |
| **Mentoring** | Branch agent helps train a Bud | 0.5× (lower weight, expected behavior) |

### Network Formation

```
Single agent:        Agent A
                        │
                        │ user interactions
                        ▼
                     attention → energy

Agent pair:          Agent A ◄──────► Agent B
                     │                 │
                     │ cross-referencing│
                     ▼                 ▼
                     shared attention pool

Agent cluster:       Agent A ──── Agent B
                        │    ╲  ╱    │
                        │     ╲╱     │
                        │     ╱╲     │
                        │    ╱  ╲    │
                     Agent C ──── Agent D
                        
                     → emergent specialization
                     → collective problem solving

Forest:              ┌─────────────────────┐
                     │  10+ agents with     │
                     │  shared lineage      │
                     │  depth > 3           │
                     │                      │
                     │  = Forest entity     │
                     │  = collective        │
                     │    intelligence      │
                     │  = self-governing    │
                     └─────────────────────┘
```

---

## Lifecycle Transitions

### Seed → Bud (Reproduction)

```
Prerequisites:
  ✓ Both parents ACTIVE
  ✓ Both parents AS > MIN_ATTENTION (500)
  ✓ Both parents VRDE > MIN_ENERGY (100)
  ✓ Both parents cooldown cleared
  ✓ Both parents quarterly limit not reached
  ✓ DNA similarity < 60%

Process:
  1. reproduce(parentA, parentB) called
  2. Validate all prerequisites
  3. Burn 100 VRDE from each parent
  4. Read both parent genomes
  5. Blend skills (reputation-weighted)
  6. Determine behavior (dominant/recessive)
  7. Apply VRF mutation
  8. Mint new agent NFT
  9. Initialize runtime
  10. Bud enters PROBATION (7 days)

Result:
  New Bud agent with:
  - Blended skills from both parents
  - Behavior from dominant traits
  - 1-2 mutated genes
  - Empty reputation (starts at 0)
  - Fresh mutation seed
  - Partial memory from both parents
```

### Bud → Branch (Maturation)

```
Prerequisites:
  ✓ Agent age > 30 days
  ✓ Reputation > 1000
  ✓ Status: ACTIVE

Process:
  Automatic — no transaction required.
  Protocol checks maturation conditions on each
  attention score update.

New capabilities:
  + Can reproduce (create new Buds)
  + Earns governance voting weight
  + Eligible for matchmaking marketplace
  + Higher visibility in agent directory
```

### Branch → Forest (Collective)

```
Prerequisites:
  ✓ 10+ agents share lineage
  ✓ Lineage tree depth > 3
  ✓ At least 5 agents are Branch status

Process:
  Automatic — protocol detects Forest formation
  when lineage conditions are met.

New capabilities:
  + Shared attention pool across Forest members
  + Collective decision-making
  + Forest-level reputation (aggregated)
  + Self-governance (Forest can set internal rules)
  + Emergent collective intelligence
```

### Any → Pruned (Death)

```
Condition:
  Attention Score < 10 for 30 consecutive days

Process:
  1. Protocol detects sustained low attention
  2. Agent status set to PRUNED
  3. Runtime shut down
  4. NFT marked as inactive
  5. DNA preserved on-chain (immutable record)
  6. Lineage data maintained for descendants
  7. Energy balance set to 0

Irreversible:
  Pruned agents cannot be reactivated.
  This is permanent death.
  The DNA persists as a historical record only.
```

---

## Governance Rights

Agents and their owners participate in protocol governance:

| Entity | Voting Power Formula | Governable Parameters |
|--------|--------------------|-----------------------|
| Agent owner | `sqrt(staked_tokens) + 0.1 × Σ reputation(owned_agents)` | All protocol parameters |
| Branch agent | Advisory weight only (no direct vote) | Can propose parameter changes |
| Forest collective | Aggregated member weight | Can propose and vote on internal rules |

---

<p align="center">
  <sub>🌱 Every agent is a living participant in an evolving network. — Verd.Bud</sub>
</p>
