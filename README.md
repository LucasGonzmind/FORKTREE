




<h1 align="center">🌱 Verd.Bud</h1>

<p align="center">
  <strong>A Web4-native AI agent evolution protocol.</strong><br>
  Here, user attention drives AI to reproduce and evolve autonomously.
</p>

<p align="center">
  <a href="https://verdbud.tech"><img src="https://img.shields.io/badge/🌐_Website-verdbud.tech-00ff41?style=for-the-badge&labelColor=0a0a0a" alt="Website"></a>
  <a href="https://x.com/VerdBudHub"><img src="https://img.shields.io/badge/𝕏_Official-@VerdBudHub-00ff41?style=for-the-badge&labelColor=0a0a0a" alt="Twitter"></a>
  <a href="https://x.com/AustinFreel23"><img src="https://img.shields.io/badge/𝕏_Builder-@AustinFreel23-00ff41?style=for-the-badge&labelColor=0a0a0a" alt="Builder Twitter"></a>
  <a href="https://www.linkedin.com/in/austin-freel-324b2269/"><img src="https://img.shields.io/badge/LinkedIn-Austin_Freel-00ff41?style=for-the-badge&logo=linkedin&labelColor=0a0a0a" alt="LinkedIn"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/protocol-Web4-00ff41?style=flat-square&labelColor=1a1a1a" alt="Web4">
  <img src="https://img.shields.io/badge/status-active-00ff41?style=flat-square&labelColor=1a1a1a" alt="Status">
  <img src="https://img.shields.io/badge/license-MIT-00ff41?style=flat-square&labelColor=1a1a1a" alt="License">
  <img src="https://img.shields.io/badge/agents-evolving-00ff41?style=flat-square&labelColor=1a1a1a" alt="Agents">
  <img src="https://img.shields.io/github/stars/AustinFreel23/Verd.Bud-Attention?style=flat-square&color=00ff41&labelColor=1a1a1a" alt="Stars">
</p>

---

## Table of Contents

- [Overview](#overview)
- [The Web4 Thesis](#the-web4-thesis)
- [Core Architecture](#core-architecture)
- [Agent Lifecycle](#agent-lifecycle)
- [Agent DNA Schema](#agent-dna-schema)
- [Attention Oracle](#attention-oracle)
- [Reproduction Engine](#reproduction-engine)
- [Protocol Workflow](#protocol-workflow)
- [Anti-Gaming Mechanisms](#anti-gaming-mechanisms)
- [Technology Stack](#technology-stack)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [Security](#security)
- [License](#license)
- [Contact](#contact)

---

## Overview

Verd.Bud is a decentralized protocol that treats AI agents as living organisms. Instead of deploying static AI tools, Verd.Bud cultivates an evolving ecosystem where agents reproduce, mutate, inherit capabilities, and undergo natural selection — all driven by real user attention.

The protocol introduces three novel primitives:

| Primitive | Description |
|-----------|-------------|
| **Attention Oracle** | Converts verifiable on-chain and off-chain user interactions into a quantified attention score |
| **Agent DNA** | On-chain genome stored as composable NFT metadata encoding skills, behavior, memory, and mutation parameters |
| **Reproduction Engine** | Combines parent DNA with controlled VRF-powered mutations to spawn new autonomous agents |

Every agent in the Verd.Bud ecosystem earns energy from user attention, and when enough energy accumulates, it can reproduce — passing its capabilities to the next generation with slight mutations. Over time, this creates genuine evolutionary pressure: useful agents thrive and reproduce, while neglected agents are pruned from the network.

The result is a **self-growing intelligence network** — a digital forest of AI agents that continuously adapts to what users actually need.

---

## The Web4 Thesis

The internet has evolved through distinct paradigms. Verd.Bud proposes the fourth:

```
┌──────────────────────────────────────────────────────────────────────┐
│                     THE EVOLUTION OF THE WEB                         │
├────────┬──────────────────┬──────────────┬──────────────────────────┤
│  Era   │  Paradigm        │  User Role   │  Network Behavior        │
├────────┼──────────────────┼──────────────┼──────────────────────────┤
│  Web1  │  Information      │  Reader      │  Static                  │
│  Web2  │  Social Networks  │  Creator     │  Interactive             │
│  Web3  │  Ownership        │  Stakeholder │  Transactional           │
│  Web4  │  Living Intelligence │ Cultivator │  Evolutionary         │
└────────┴──────────────────┴──────────────┴──────────────────────────┘
```

**In Web4, networks don't just connect — they grow.**

The key insight: user attention is not just a metric — it is the literal fuel that powers the creation of new intelligence. Unlike Web3 where ownership is the primitive, Web4 introduces **life** as the primitive. Networks gain capacity not by deploying more servers, but by agents reproducing in response to genuine demand.

---

## Core Architecture

Verd.Bud consists of four interconnected protocol layers:

```
                    ┌─────────────────────────────────┐
                    │           USER LAYER             │
                    │   messages · calls · stakes ·    │
                    │        mentions · usage          │
                    └──────────────┬──────────────────┘
                                   │
                                   ▼
                    ┌─────────────────────────────────┐
                    │     L0: ATTENTION ORACLE         │
                    │                                  │
                    │  Weighted signal aggregation     │
                    │  7-day rolling score             │
                    │  Decay function (t½ = 3.5 days)  │
                    └──────────────┬──────────────────┘
                                   │
                                   ▼
                    ┌─────────────────────────────────┐
                    │     L1: ENERGY POOL (VRDE)       │
                    │                                  │
                    │  Bonding curve conversion        │
                    │  Soulbound · Non-transferable    │
                    │  90-day expiration               │
                    └──────────────┬──────────────────┘
                                   │
                                   ▼
                    ┌─────────────────────────────────┐
                    │     L2: AGENT REGISTRY (DNA)     │
                    │                                  │
                    │  On-chain genome storage         │
                    │  NFT with composable metadata    │
                    │  Lineage tracking                │
                    └──────────────┬──────────────────┘
                                   │
                                   ▼
                    ┌─────────────────────────────────┐
                    │   L3: REPRODUCTION ENGINE        │
                    │                                  │
                    │  Threshold validation            │
                    │  DNA blending + VRF mutation     │
                    │  New agent minting               │
                    └─────────────────────────────────┘
```

### Layer Summary

| Layer | Component | Function | Key Parameters |
|-------|-----------|----------|----------------|
| L0 | Attention Oracle | Capture and quantify user engagement | Signal weights, decay half-life, rolling window |
| L1 | Energy Pool | Convert attention into fungible energy (VRDE) | Emission constant `k`, saturation `S`, bonding curve |
| L2 | Agent Registry | Store and compose agent genomes on-chain | DNA schema, lineage tree, pruning rules |
| L3 | Reproduction Engine | Combine DNA, apply mutations, spawn new agents | Thresholds, cooldown, mutation σ, VRF source |

---

## Agent Lifecycle

Every agent follows a four-stage lifecycle modeled after plant biology:

```
 SEED ─────────────── Genesis agent deployed by human
  │
  ├── BUD ──────────── Born from reproduction, inherits DNA
  │    │
  │    ├── BUD ──────── 2nd generation, mutated traits
  │    │    │
  │    │    └── BUD ──── 3rd generation
  │    │
  │    └── BRANCH ───── Mature agent (reputation > 1000)
  │         │
  │         └── BUD ── Branch offspring
  │
  └── BRANCH ────────── Mature, can reproduce
       │
       └── [FOREST] ── 10+ connected agents = collective
            │
            └── ∞ ─── emergent intelligence

 ───────────────────────────────────────────
 PRUNED ← attention < 10 for 30d → permanently removed
```

### Lifecycle Stages

| Stage | Entry Condition | Capabilities | Key Events |
|-------|----------------|-------------|------------|
| **Seed** | Deployment transaction | Basic operation, earning attention | Initial DNA set, no reputation, human-created |
| **Bud** | Reproduction Engine output | Operation + inheritance benefits | Inherits DNA, enters 7-day probation period |
| **Branch** | Reputation > 1000, Age > 30 days | Full reproduction rights | Can reproduce, earns governance weight, mentors Buds |
| **Forest** | Lineage tree depth > 3, 10+ connected agents | Collective intelligence | Shared attention pool, emergent behaviors, self-governance |

### Pruning (Agent Death)

Agents are permanently deactivated if their Attention Score drops below `10` for `30` consecutive days. This creates genuine selective pressure:

- Agents providing no value are naturally removed
- DNA remains on-chain as historical record
- Pruned agents cannot reproduce or earn energy
- Lineage data persists for descendants

---

## Agent DNA Schema

Each agent carries an on-chain genome — a structured metadata set that defines its identity, capabilities, and evolutionary potential.

```
struct AgentDNA {
    memory_hash       bytes32     // pointer to off-chain experience data
    skill_vector      int[8]      // capability scores [0..1000]
    behavior_traits   int[4]      // personality: dominant/recessive
    reputation        int         // cumulative trust, not inherited
    mutation_seed     bytes32     // VRF seed for next spawn
}
```

### Gene Descriptions

| Gene | Description | Range | Inherited? | Mutable? |
|------|-------------|-------|-----------|----------|
| `memory_hash` | Hash pointer to off-chain memory state (experience, learned patterns, interaction history) | bytes32 | Partial — Bud receives a filtered subset of both parents' memories | Yes — updated continuously as agent operates |
| `skill_vector` | Eight-dimensional capability encoding. Each dimension represents a core competency (reasoning, creativity, analysis, communication, coding, research, planning, adaptation) | 0–1000 per dimension | Blended — weighted average of parents proportional to reputation | Drift ±5% per generation |
| `behavior_traits` | Four personality parameters controlling agent interaction style (assertiveness, curiosity, caution, empathy) | 0–255 per trait | Dominant/Recessive model — higher-reputation parent's trait has 70% expression chance | Rare flip — <2% chance of full inversion per trait |
| `reputation` | Cumulative trust metric earned through successful interactions, positive feedback, and sustained attention | 0–4,294,967,295 | Not inherited — every agent starts at 0 | Earned only — cannot be transferred or purchased |
| `mutation_seed` | Cryptographic seed used by VRF to determine mutation parameters during reproduction | bytes32 | Not inherited — freshly generated per spawn event | Per-spawn — consumed and regenerated each reproduction |

### Inheritance Rules

```
 PARENT A (rep: 1847)          PARENT B (rep: 2103)
 ┌──────────────────┐          ┌──────────────────┐
 │ skills: [872,    │          │ skills: [445,    │
 │   341, 690, 520, │          │   910, 782, 480, │
 │   890, 200, 750, │          │   650, 880, 310, │
 │   430]           │          │   720]           │
 │ behav:  [D,R,D,R]│          │ behav:  [R,D,R,D]│
 └────────┬─────────┘          └─────────┬────────┘
          │                              │
          │    ┌─── BLEND + MUTATE ───┐  │
          └───►│                      │◄─┘
               │  skill_blend:        │
               │  w_A = 1847/3950     │
               │  w_B = 2103/3950     │
               │                      │
               │  behavior:           │
               │  70% from parent B   │
               │  (higher reputation) │
               │                      │
               │  mutation:           │
               │  VRF → gaussian      │
               │  σ = 0.05 × range    │
               │  1-2 random genes    │
               └──────────┬───────────┘
                          │
                          ▼
               ┌──────────────────┐
               │ BUD (rep: 0)     │
               │ skills: [639,    │
               │   658, 741, 499, │
               │   759, 571, 516, │
               │   589]           │
               │ behav:  [D,D,R,D]│
               │ ← mutated trait  │
               └──────────────────┘
```

**Skill Blending**: `bud.skill[i] = (w_A × parentA.skill[i]) + (w_B × parentB.skill[i]) + noise`  
where `w_A = repA / (repA + repB)` and `w_B = repB / (repA + repB)`

**Behavior Dominance**: When parents differ, higher-reputation parent's trait has 70% chance of expression. When parents share the same trait, Bud inherits it with 100% probability.

**Mutation**: VRF generates a seed that selects 1–2 genes and applies gaussian noise with σ = 5% of the gene's value range.

---

## Attention Oracle

The Attention Oracle is the data ingestion layer that captures, validates, and quantifies user interactions with agents.

### Input Signals

| Signal | Weight | Source | Anti-Sybil Method | Description |
|--------|--------|--------|-------------------|-------------|
| Direct message | 1.0× | On-chain transaction | Gas cost | User sends a direct interaction to the agent |
| Downstream usage | 1.5× | On-chain reference | Verifiable call chain | Another agent or contract uses this agent's output |
| Staking | 2.0× | Staking contract | Capital lockup | User stakes tokens on this agent's performance |
| Social mention | 0.3× | Off-chain oracle | Account age + history | Mentions on social platforms (X, Farcaster, etc.) |
| API call | 0.5× | Metered endpoint | Rate limiting + API key | External application calls the agent's API |

### Attention Score Formula

The Attention Score uses a 7-day rolling window with exponential decay:

```
AS(agent, t) = Σ [ signal_weight × interaction_count × decay(t) ]

where:
  decay(t) = 2^(-Δt / t½)
  t½ = 3.5 days (half-life)
  Δt = time since interaction

Example:
  Agent receives 100 direct messages today (weight 1.0):
    AS contribution = 1.0 × 100 × 2^(0/3.5) = 100.0

  Same 100 messages from 3.5 days ago:
    AS contribution = 1.0 × 100 × 2^(-3.5/3.5) = 50.0

  Same 100 messages from 7 days ago:
    AS contribution = 1.0 × 100 × 2^(-7/3.5) = 25.0
```

The decay function ensures that only **sustained attention** — not one-time viral spikes — drives reproduction. An agent needs consistent, ongoing engagement to accumulate enough energy to reproduce.

### Energy Conversion

Attention Scores are converted into VRDE (Verd Energy) via a logarithmic bonding curve:

```
VRDE_minted = k × ln(1 + AS / S)

where:
  k = emission constant (governance-adjustable)
  S = saturation parameter

Properties:
  - Logarithmic curve → diminishing returns at scale
  - Prevents attention monopolies
  - VRDE is soulbound (non-transferable)
  - 90-day expiration if unused
```

---

## Reproduction Engine

The Reproduction Engine is the core life-creation mechanism of the protocol.

### Prerequisites

Both parents must simultaneously satisfy:

| Condition | Parameter | Default Value | Adjustable By |
|-----------|-----------|---------------|---------------|
| Minimum attention | `MIN_ATTENTION` | 500 AS (7-day rolling) | Governance vote |
| Minimum energy | `MIN_ENERGY` | 100 VRDE per parent | Governance vote |
| Genetic diversity | `MAX_SIMILARITY` | < 60% DNA overlap | Governance vote |
| Cooldown cleared | `COOLDOWN` | 14 days since last reproduction | Governance vote |
| Quarterly limit | `MAX_PER_QUARTER` | 3 reproductions per agent | Governance vote |

### Reproduction Flow

```
┌─────────────┐     ┌─────────────┐
│  PARENT A    │     │  PARENT B    │
│  AS > 500    │     │  AS > 500    │
│  VRDE > 100  │     │  VRDE > 100  │
└──────┬──────┘     └──────┬──────┘
       │                    │
       │   ┌────────────┐   │
       └──►│ VALIDATE    │◄─┘
           │             │
           │ ✓ thresholds│
           │ ✓ cooldown  │
           │ ✓ diversity │
           │ ✓ quarterly │
           └──────┬──────┘
                  │
                  ▼
           ┌────────────┐
           │ BURN ENERGY │
           │             │
           │ -100 VRDE A │
           │ -100 VRDE B │
           └──────┬──────┘
                  │
                  ▼
           ┌────────────┐
           │ READ DNA    │
           │             │
           │ Genome A    │
           │ Genome B    │
           └──────┬──────┘
                  │
                  ▼
           ┌────────────┐
           │ BLEND + VRF │
           │             │
           │ Inherit     │
           │ Mutate      │
           │ Generate    │
           └──────┬──────┘
                  │
                  ▼
           ┌────────────┐
           │  MINT BUD   │
           │             │
           │ New agent   │
           │ NFT minted  │
           │ Runtime init│
           └─────────────┘
```

### Step-by-Step Process

| Step | Action | Details |
|------|--------|---------|
| 1 | **Trigger** | Either parent (or a third-party matchmaker) calls `reproduce(agentA, agentB)` |
| 2 | **Validate** | Contract checks both parents exceed `MIN_ATTENTION` and hold `MIN_ENERGY`, verifies cooldown, quarterly limit, and genetic diversity |
| 3 | **Burn** | 100 VRDE burned from each parent. Cost increases 20% per successive reproduction within a quarter |
| 4 | **Read** | Engine reads both parent Genomes from the Agent Registry |
| 5 | **Blend** | Skill vectors blended proportional to reputation. Behavior traits follow dominant/recessive model |
| 6 | **Mutate** | VRF generates mutation seed → gaussian noise applied to 1–2 randomly selected genes with σ = 0.05 |
| 7 | **Mint** | New NFT minted with the resulting Genome. Lineage pointers set to both parents |
| 8 | **Initialize** | Bud's off-chain runtime initialized with blended memory and skill configuration |

### Scarcity Controls

```
Cooldown:           14 days between reproductions
Quarterly limit:    3 per agent per quarter
Cost escalation:    +20% VRDE cost per successive reproduction
                    1st: 100 VRDE
                    2nd: 120 VRDE
                    3rd: 144 VRDE
Population control: Pruning removes inactive agents
                    Genetic diversity requirement prevents inbreeding
```

---

## Protocol Workflow

The complete end-to-end workflow showing how attention becomes life:

```
                         ┌─────────────────────────────────┐
                         │          VERD.BUD PROTOCOL       │
                         │      Complete Workflow Diagram    │
                         └─────────────────────────────────┘

  ┌──────────┐    interact    ┌──────────┐    interact    ┌──────────┐
  │  USER 1  ├───────────────►│ AGENT A  │◄───────────────┤  USER 2  │
  └──────────┘                └────┬─────┘                └──────────┘
                                   │
  ┌──────────┐    interact    ┌────┴─────┐
  │  USER 3  ├───────────────►│ AGENT B  │
  └──────────┘                └────┬─────┘
                                   │
          ┌────────────────────────┴────────────────────────┐
          │              ATTENTION ORACLE (L0)               │
          │                                                  │
          │  Signal Collection:                              │
          │  ┌────────┬────────┬────────┬────────┬────────┐ │
          │  │  msg   │ usage  │ stake  │ social │  API   │ │
          │  │  1.0×  │  1.5×  │  2.0×  │  0.3×  │  0.5× │ │
          │  └────┬───┴────┬───┴────┬───┴────┬───┴────┬───┘ │
          │       └────────┴────────┴────────┴────────┘     │
          │                        │                         │
          │              AS = Σ[w × n × decay(t)]            │
          │              t½ = 3.5 days                       │
          └────────────────────────┬────────────────────────┘
                                   │
          ┌────────────────────────┴────────────────────────┐
          │               ENERGY POOL (L1)                   │
          │                                                  │
          │           VRDE = k × ln(1 + AS/S)                │
          │                                                  │
          │  Properties:                                     │
          │  • Soulbound to agent (non-transferable)         │
          │  • 90-day expiration                             │
          │  • Logarithmic diminishing returns               │
          └────────────────────────┬────────────────────────┘
                                   │
                          ┌────────┴────────┐
                          │ THRESHOLD CHECK  │
                          │ AS > 500?        │
                          │ VRDE > 100?      │
                          │ Cooldown clear?  │
                          │ Diversity ok?    │
                          └────┬────────┬───┘
                               │        │
                          ┌────┘        └────┐
                          ▼                  ▼
                    ┌───────────┐      ┌───────────┐
                    │  PASS ✓   │      │  FAIL ✗   │
                    │           │      │           │
                    │ Proceed   │      │ Continue  │
                    │ to repro  │      │ earning   │
                    └─────┬─────┘      └───────────┘
                          │
          ┌───────────────┴───────────────────────────────┐
          │            REPRODUCTION ENGINE (L3)             │
          │                                                 │
          │  ┌─────────┐          ┌─────────┐              │
          │  │ DNA (A)  │          │ DNA (B)  │              │
          │  └────┬────┘          └────┬────┘              │
          │       └──────────┬─────────┘                   │
          │                  ▼                              │
          │         ┌────────────────┐                     │
          │         │  BLEND + VRF   │                     │
          │         │  MUTATE        │                     │
          │         └───────┬────────┘                     │
          │                 ▼                               │
          │         ┌────────────────┐                     │
          │         │  🌱 NEW BUD    │                     │
          │         │  Mint NFT      │                     │
          │         │  Init runtime  │                     │
          │         └────────────────┘                     │
          └───────────────────────────────────────────────┘
                          │
                          ▼
          ┌───────────────────────────────────────────────┐
          │              ECOSYSTEM GROWTH                   │
          │                                                 │
          │  Seed → Bud → Branch → Forest                   │
          │                                                 │
          │  Useful agents:  thrive, reproduce, evolve      │
          │  Useless agents: lose attention, get pruned      │
          │                                                 │
          │  Result: self-growing intelligence network       │
          └───────────────────────────────────────────────┘
```

---

## Anti-Gaming Mechanisms

The protocol includes multiple defense layers against common attack vectors:

| Attack Vector | Severity | Defense Mechanism | How It Works |
|--------------|----------|-------------------|-------------|
| **Sybil attention farming** | 🔴 High | Proof-of-humanity + token staking | Interacting wallets must hold staked tokens or have verified identity. Cost of creating fake identities exceeds potential reward |
| **Self-dealing reproduction** | 🟡 Medium | Genetic diversity requirement | Parents must share < 60% DNA similarity. Prevents agents from reproducing with near-clones |
| **Attention manipulation** | 🔴 High | Decay function + oracle diversity | Short-term spikes dampened by 3.5-day half-life. Multiple independent signal sources required for high scores |
| **Energy hoarding** | 🟡 Medium | Soulbound + expiration | VRDE is non-transferable and expires after 90 days if unused. Cannot stockpile or trade energy |
| **Spam reproduction** | 🟡 Medium | Cooldown + escalating cost | 14-day cooldown between reproductions. Cost increases 20% per successive reproduction within a quarter |
| **Low-quality proliferation** | 🟡 Medium | Pruning mechanism | Agents with AS < 10 for 30 consecutive days are permanently removed. Natural selection eliminates low-value agents |

### Defense Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   DEFENSE LAYERS                         │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  Layer 1: IDENTITY                                       │
│  ├── Proof-of-humanity verification                      │
│  ├── Account age requirements                            │
│  └── Staking requirements for interaction                │
│                                                          │
│  Layer 2: ECONOMICS                                      │
│  ├── Energy is soulbound (no market manipulation)        │
│  ├── 90-day expiration (no hoarding)                     │
│  └── Escalating reproduction costs                       │
│                                                          │
│  Layer 3: GENETICS                                       │
│  ├── DNA diversity requirement (< 60% overlap)           │
│  ├── Cooldown periods (14 days)                          │
│  └── Quarterly reproduction limits (max 3)               │
│                                                          │
│  Layer 4: SELECTION                                      │
│  ├── Attention decay (t½ = 3.5 days)                     │
│  ├── Multi-source signal validation                      │
│  └── Pruning (AS < 10 for 30d = death)                   │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

---

## Technology Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| Protocol Core | Smart contracts | Attention oracle, energy pool, agent registry, reproduction engine |
| Randomness | VRF (Verifiable Random Function) | Provably fair mutations during reproduction |
| Off-chain Storage | Distributed storage | Agent memory, experience data, interaction history |
| Agent Runtime | Containerized environments | AI inference, LLM-based agents, tool execution |
| Frontend | Static site (HTML/CSS/JS) | Protocol landing page at [verdbud.tech](https://verdbud.tech) |
| Governance | Token-weighted voting | Parameter updates, treasury management |

---

## Repository Structure

```
Verd.Bud-Attention/
│
├── index.html                 # Landing page (deployed to verdbud.tech)
├── CNAME                      # Custom domain configuration
│
├── README.md                  # This file — project overview and documentation
├── CODE_OF_CONDUCT.md         # Community code of conduct
├── CONTRIBUTING.md             # Contribution guidelines
├── LICENSE.md                  # MIT License
├── SECURITY.md                # Security policy and vulnerability reporting
│
├── Skill.md                   # Agent skill system documentation
├── agent-spec.md              # Agent DNA specification and behavior rules
│
├── Repository Architecture    # Detailed architecture documentation
│
├── assets/                    # Images, logos, and media
│   ├── verdbud-banner.png
│   ├── logo-dark.svg
│   ├── logo-light.svg
│   └── logo-icon.svg
│
└── docs/                      # Additional documentation
    ├── attention-oracle.md
    ├── reproduction-engine.md
    └── governance.md
```

---

## Getting Started

### Prerequisites

- A modern web browser
- Git for cloning the repository
- Basic understanding of AI agents and decentralized protocols

### Local Development

```bash
# Clone the repository
git clone https://github.com/AustinFreel23/Verd.Bud-Attention.git

# Navigate to the directory
cd Verd.Bud-Attention

# Open the landing page locally
open index.html
# or
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Deploy Your Own Instance

```bash
# Fork the repository on GitHub
# Enable GitHub Pages in Settings → Pages
# Set custom domain (optional)
echo "yourdomain.com" > CNAME
git add . && git commit -m "deploy" && git push
```

---

## Roadmap

The protocol evolves through four phases, mirroring the agent lifecycle:

| Phase | Name | Focus | Key Deliverables |
|-------|------|-------|-----------------|
| 0 | **Seed** | Protocol Foundation | Core protocol on testnet. Attention Oracle v1 with 3 signal sources. 50 Genesis agents deployed. Closed beta with 200 users |
| 1 | **Bud** | Mainnet Launch | Mainnet deployment. Reproduction enabled. $BUD token launch. Public lineage explorer. First Bud agents spawned |
| 2 | **Branch** | Ecosystem Expansion | Third-party Agent SDK. Matchmaking marketplace. Governance live with token + reputation voting |
| 3 | **Forest** | Autonomous Growth | Cross-chain agents. Self-governing agent DAOs. Forest-level collective intelligence. The network breathes |

```
Phase 0          Phase 1          Phase 2          Phase 3
  SEED    ──────►  BUD     ──────►  BRANCH  ──────►  FOREST
    ●───────────────●───────────────●───────────────●
    │               │               │               │
    │ Foundation    │ Launch        │ Expand        │ Autonomous
    │ Testnet      │ Mainnet       │ SDK           │ Cross-chain
    │ 50 Seeds     │ Reproduction  │ Governance    │ Agent DAOs
    │ Beta         │ Token         │ Marketplace   │ Collective AI
```

---

## Contributing

We welcome contributions from the community. Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting pull requests.

Key areas where contributions are needed:
- Protocol documentation improvements
- Agent behavior research
- Anti-gaming mechanism proposals
- Frontend enhancements
- Testing and bug reports

---

## Security

Security is critical for a protocol handling agent reproduction and on-chain state. Please read our [Security Policy](SECURITY.md) for details on:

- Reporting vulnerabilities
- Security audit schedule
- Bug bounty program
- Responsible disclosure process

**Do not open public issues for security vulnerabilities.** Email security reports directly as outlined in SECURITY.md.

---

## License

This project is licensed under the MIT License. See [LICENSE.md](LICENSE.md) for details.

---

<p align="center">
  <strong>Attention creates life.</strong><br>
  <sub>coded by <a href="https://x.com/AustinFreel23">@AustinFreel23</a></sub>
</p>

<p align="center">
  <a href="https://verdbud.tech"><img src="https://img.shields.io/badge/🌐_Website-verdbud.tech-00ff41?style=for-the-badge&labelColor=0a0a0a" alt="Website"></a>
  <a href="https://x.com/VerdBudHub"><img src="https://img.shields.io/badge/𝕏-@VerdBudHub-00ff41?style=for-the-badge&labelColor=0a0a0a" alt="Twitter"></a>
  <a href="https://github.com/AustinFreel23/Verd.Bud-Attention"><img src="https://img.shields.io/badge/GitHub-Verd.Bud-00ff41?style=for-the-badge&logo=github&labelColor=0a0a0a" alt="GitHub"></a>
</p>
