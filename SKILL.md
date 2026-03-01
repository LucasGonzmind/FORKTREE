
# SKILL.md

## RootDna Skill System

### Overview

In RootDna, a **Skill** is the fundamental unit of intelligence: a modular, reusable capability that an autonomous agent can execute to **perceive**, **decide**, and **act** within an environment.

RootDna agents are not monolithic “one-model-does-everything” systems. Instead, each agent is composed of multiple skills that can be **composed**, **routed**, **evaluated**, **inherited**, and **evolved** over time. This structure enables:

- **Continuous adaptation** in dynamic environments
- **Long-term learning** without full resets
- **System-wide intelligence accumulation** across generations
- **Transparency and control** through observable decision signals

RootDna skills are designed for real, changing environments such as markets, simulations, and digital ecosystems where feedback is continuous and uncertainty is the default.

---

## Design Principles

RootDna skills follow five principles that keep agents evolvable and safe:

### 1) Modularity
A skill should have a clear responsibility and minimal surface area. Small skills are easier to test, replace, and evolve.

### 2) Composability
Skills must work together. Every skill should define stable inputs/outputs so it can be chained, routed, or combined with other skills.

### 3) Adaptability
Skills should be able to improve from feedback. Adaptation can be simple parameter tuning or more advanced online learning.

### 4) Inheritance
Skills that prove effective should be transferrable to other agents or future generations through parameter transfer, structural reuse, or recombination.

### 5) Observability
Skills must expose signals and metrics that explain what they did and how well it worked. If it cannot be measured, it cannot evolve safely.

---

## Core Concepts

### Skill vs Strategy vs Agent

- **Skill**: a focused capability (e.g., volatility estimation, routing, execution)
- **Strategy**: a policy composed of skills (e.g., “trend + risk control + execution”)
- **Agent**: a runtime system that orchestrates skills, maintains state/memory, interacts with environments, and evolves over time

RootDna treats “intelligence” as an evolving system rather than a static artifact.

---

## Skill Layers (Taxonomy)

RootDna organizes skills into layers to keep responsibilities clear and evolution manageable.

### 1) Perception Skills
Perception skills transform raw environment inputs into structured signals.

**Examples**
- Market regime detection
- Volatility estimation
- Trend / momentum extraction
- Multi-agent state tracking
- Event parsing and normalization

**Typical outputs**
- Feature vectors
- Regime labels
- Confidence scores
- Alerts and anomalies

---

### 2) Decision Skills
Decision skills convert perceived state into action intent.

**Examples**
- Strategy routing
- Opportunity scoring
- Risk evaluation
- Allocation and sizing
- Policy selection (which behavior to run)

**Typical outputs**
- Action intents (long/short/hold, task selection, allocation %)
- Confidence and uncertainty estimates
- Rationale signals (which factors contributed)

---

### 3) Execution Skills
Execution skills convert intents into real actions.

**Examples**
- Trade execution
- Position management
- API integration (read/write)
- Inter-agent communication
- Simulation actions

**Typical outputs**
- Execution receipts (filled, partial, rejected)
- Errors and retries
- Latency and slippage (if relevant)

---

### 4) Adaptation Skills
Adaptation skills update behavior through feedback loops.

**Examples**
- Parameter tuning
- Reward shaping
- Online learning adapters
- Stability control and dampening
- Performance drift detection

**Typical outputs**
- Updated parameters and deltas
- Adaptation summaries
- Drift and stability metrics

---

### 5) Memory Skills
Memory skills store and retrieve long-term knowledge and maintain continuity.

**Examples**
- Episode memory (recent outcomes)
- Long-term pattern memory
- Summarization / compression
- Retrieval and ranking
- Identity persistence management

**Typical outputs**
- Memory snapshots
- Retrieval results
- Compression logs and health metrics

---

### 6) Evolution Skills
Evolution skills introduce structured variation and selection at the skill/agent level.

**Examples**
- Mutation (parameter / structural)
- Recombination (compose genes from multiple sources)
- Selection (fitness filters)
- Population sampling
- Breeding pipelines

**Typical outputs**
- New candidate skills/agents
- Mutation diffs
- Fitness evaluations

---

## Skill Lifecycle

A RootDna skill improves through a continuous lifecycle:

1. **Create**  
   Author a skill with clear I/O contracts and safety constraints.

2. **Compose**  
   Wire skills into an agent graph (pipeline, router, ensemble, hierarchy).

3. **Deploy**  
   Run in real or simulated environments.

4. **Observe**  
   Record decisions, signals, and metrics.

5. **Adapt**  
   Update parameters or internal logic based on feedback.

6. **Select**  
   Keep effective skills; revise or remove underperformers.

7. **Inherit**  
   Transfer winning skills into new agents or generations.

This loop allows intelligence to accumulate without full resets.

---

## Standard Skill Interface

RootDna skills should implement a consistent interface so they can be composed and routed safely.

At minimum, a skill should support:

- `initialize(config)` – load config, constraints, and initialize state
- `observe(env)` – transform raw environment into structured state/signals
- `propose(state)` – propose an intent (for decision skills)
- `act(intent)` – execute intent (for execution skills)
- `update(feedback)` – adapt based on outcomes
- `metrics()` – expose runtime performance signals

### Reference Interface (Python-style)

```python
from dataclasses import dataclass
from typing import Any, Dict, Optional

@dataclass
class SkillOutput:
    intent: Optional[Dict[str, Any]] = None
    signals: Optional[Dict[str, Any]] = None
    reason: Optional[str] = None
    confidence: float = 0.0

class Skill:
    name: str = "skill"

    def initialize(self, config: Dict[str, Any]) -> None:
        """Load config, constraints, and initialize internal state."""
        ...

    def observe(self, env: Dict[str, Any]) -> Dict[str, Any]:
        """Transform raw environment input into structured state/signals."""
        return {}

    def propose(self, state: Dict[str, Any]) -> SkillOutput:
        """Propose an intent given state (decision skills)."""
        return SkillOutput()

    def act(self, intent: Dict[str, Any]) -> Dict[str, Any]:
        """Execute intent (execution skills)."""
        return {}

    def update(self, feedback: Dict[str, Any]) -> None:
        """Update parameters/logic based on outcome feedback."""
        ...

    def metrics(self) -> Dict[str, Any]:
        """Expose metrics for evaluation and debugging."""
        return {}
```

---

## Composition Patterns

RootDna supports multiple composition patterns. Use the simplest pattern that fits the problem.

### 1) Pipeline (Chain)
A linear flow of skills:
Perception → Decision → Execution → Feedback

**Best for**
- Clear stages
- Easy debugging
- Low complexity

---

### 2) Router (Context-Based Selection)
A routing skill chooses which decision module(s) to activate based on context.

**Best for**
- Regime shifts (e.g., stable vs volatile)
- Conditional behaviors
- Resource-aware control

---

### 3) Ensemble (Voting / Blending)
Multiple decision skills propose intents; a coordinator merges them.

**Best for**
- Robustness
- Reducing single-strategy brittleness
- Maintaining diversity

---

### 4) Hierarchical (Manager + Workers)
A manager skill assigns sub-tasks to worker skills.

**Best for**
- Research agents
- Tool-using agents
- Complex multi-step execution

---

## Skill Routing

Routing is how RootDna stays adaptive without constantly rewriting agents.

A router typically considers:
- Context and regime signals
- Confidence / uncertainty
- Risk limits and constraints
- Recent performance and drift
- Resource budgets (latency, compute, cost)

Routing outputs:
- Which skills activate
- How their outputs are combined
- When to degrade to safe modes

Routing logic itself can evolve.

---

## Observability and Metrics

If a skill cannot be evaluated, it cannot evolve reliably.

### Minimum recommended metrics
- `success_rate`
- `avg_reward` or `avg_pnl` (when applicable)
- `risk_violations`
- `decision_confidence`
- `runtime_ms`
- `failure_rate`

### Recommended decision signals
- top contributing features
- active modules/genes
- confidence / uncertainty
- reason strings (short, structured)

---

## Feedback and Learning

RootDna separates **feedback** from **training**. Feedback can arrive at different time scales.

**Common feedback signals**
- Profit/loss (markets)
- Task success/failure (research/tools)
- Resource outcomes (latency/cost)
- Interaction outcomes (multi-agent)

A skill should support:
- Short loops (minutes/episodes)
- Long loops (days/weeks)
- Partial or delayed rewards

---

## Safety and Constraints

Autonomous systems require guardrails. Skills should enforce:

- Action boundaries (allowed actions only)
- Budget limits (rate, spend, compute)
- Risk limits (exposure, drawdown, volatility caps)
- Circuit breakers (halt on repeated failures)
- Fallback behaviors (safe defaults)

A safe skill:
- refuses actions outside constraints
- logs violations clearly
- degrades gracefully with missing data
- fails closed when uncertain

---

## Inheritance

RootDna supports multiple forms of inheritance:

1) **Parameter inheritance**  
Transfer tuned parameters into new skill instances.

2) **Structural inheritance**  
Reuse skill graphs (pipelines/routers) across agents.

3) **Behavioral inheritance**  
Preserve high-level tendencies (risk posture, exploration level).

4) **Cross-agent reuse**  
Promote stable skills to a shared library.

Inheritance is how RootDna accumulates intelligence rather than resetting.

---

## Mutation

Mutation introduces controlled variation.

**Mutation types**
- Parameter mutation: small nudges in thresholds/weights
- Structural mutation: add/remove/swap modules
- Routing mutation: adjust selection rules
- Memory mutation: change compression/retrieval strategies

**Mutation rules**
- bounded (limits on magnitude)
- logged (diffs recorded)
- evaluable (must be tested)
- reversible (rollback if unstable)

---

## Selection and Fitness

Selection prevents chaos by promoting only robust improvements.

### Fitness signals can include
- long-term performance
- risk-adjusted outcomes
- stability under drift
- generalization across regimes/environments
- constraint compliance
- interpretability and debug-ability

Selection methods may include:
- rolling windows
- tournament selection
- multi-objective scoring (reward + risk + stability)

---

## Versioning and Compatibility

Skills should be versioned to support safe inheritance.

Recommended metadata:
- `skill_id`
- `version`
- `compatibility_tags`
- `required_inputs`
- `expected_outputs`

Avoid breaking changes. When breaking changes are necessary, provide adapters.

---

## Practical Example: Minimal RootDna Agent

A minimal agent composition might be:

- Perception: `RegimeDetector`
- Decision: `StrategyRouter`
- Execution: `Executor`
- Adaptation: `FeedbackTuner`
- Memory: `EpisodeMemory`
- Evolution: `MutationEngine`

Each component can evolve independently.

---

## Developer Guidelines

**Write skills that are**
- small and readable
- testable and observable
- safe by default
- deterministic when possible
- compatible with composition patterns

**Avoid**
- giant skills that do everything
- hidden state with no logging
- decisions without confidence signals
- updates without evaluation/rollback

---

## Roadmap (Docs-First)

The RootDna skill system documentation will expand to include:

- skill registry and discovery
- standard environment adapters
- evaluation harnesses
- agent templates
- breeding and recombination pipelines
- contribution guidelines for community skills

---

## Conclusion

Skills are the foundation of RootDna. By modularizing intelligence into reusable, evolvable components, RootDna enables agents to:

- learn continuously
- adapt across environments
- inherit useful behavior
- evolve without resets

This transforms AI from static models into long-term adaptive systems.
