---
title: "Agents Companion (Google, Feb 2025) — Summary"
type: paper
axis: both
tags: [agentops, agent-evaluation, trajectory-evaluation, multi-agent, agentic-rag, contractor-model, enterprise-ai, google]
related: [[agentic-ai]], [[agentops]], [[multi-agent-systems]], [[agentic-rag]], [[llm-evals]], [[agent-observability]], [[llm-as-judge]]
created: 2026-04-12
updated: 2026-04-12
---

# Agents Companion (Google, Feb 2025) — Summary

**Source**: Gulli, Nigam, Wiesinger, et al. Google. February 2025.
**Full paper page**: [[google-agents-companion]]
**Scope**: "102" guide — for developers already familiar with agent basics. Covers operationalization, evaluation, multi-agent patterns, Agentic RAG, and enterprise deployment.

---

## The One-Line Thesis

Getting a gen AI agent from proof-of-concept to production is hard. The answer is **AgentOps** (disciplined operations) + **automated evaluation** (trajectory + final response) + **multi-agent design patterns**.

---

## Five Key Ideas

### 1. AgentOps: Your Agent Needs Its Own DevOps

AgentOps is not a metaphor — it's a specific discipline that inherits from DevOps → MLOps → FMOps → GenAIOps and adds agent-specific concerns:

- **Tool management** (internal functions and external APIs)
- **Agent brain prompt** (goal, profile, instructions — needs versioning like code)
- **Memory** (short-term session + long-term learned patterns)
- **Task decomposition** (breaking goals into delegatable subtasks)

The metrics hierarchy: business north star → goal completion rate → critical task success rates → telemetry → human feedback → traces. Traces are for debugging, not continuous measurement.

See [[agentops]] for the full ops hierarchy and A/B experiment design guidance.

### 2. Trajectory Evaluation: Evaluate the Path, Not Just the Answer

An agent's output can look correct while the reasoning path was wrong. Trajectory evaluation addresses this by comparing the agent's sequence of actions (tool calls, retrievals, API invocations) against a reference trajectory.

Six ground-truth-based metrics (from most to least strict):

| Metric | What it catches |
|--------|----------------|
| Exact match | Any deviation from the reference path |
| In-order match | Out-of-order core steps |
| Any-order match | Missing required steps (order ignored) |
| Precision | Unnecessary / spurious steps |
| Recall | Missing required steps |
| Single-tool use | Whether a specific tool was ever used |

**Limitation**: all six require a reference trajectory. Creating reference trajectories is expensive — requires domain experts. Research into autoraters for trajectories ("Agent-as-a-Judge") is active.

See [[llm-evals]] for the full trajectory metric table and comparison with LLM-as-Judge.

### 3. Multi-Agent Design Patterns: Five Production-Tested Architectures

The paper catalogs patterns from a real automotive AI deployment:

| Pattern | Description | Best for |
|---------|-------------|----------|
| **Hierarchical** | Central orchestrator routes to specialists | High-volume, clear domain boundaries |
| **Diamond** | Hierarchical + Rephraser moderates all outputs | User-facing, tone/safety consistency |
| **Peer-to-Peer** | Agents self-redirect when misrouted | Resilience to orchestrator misclassification |
| **Collaborative/Response Mixer** | Multiple agents answer; mixer picks best parts | Multi-domain queries, safety-critical questions |
| **Adaptive Loop** | Agent iteratively reformulates until criteria met | Search tasks where exact matches are rare |

See [[multi-agent-systems]] for full descriptions and the multi-agent evaluation section.

### 4. Agentic RAG: Agents as Active Retrievers

Traditional RAG (single static query) fails on ambiguous, multi-step, and multi-perspective queries — exactly the queries common in enterprise settings. Agentic RAG replaces the single lookup with an active retrieval agent that:

1. Generates multiple query refinements
2. Selects source types dynamically (graph DB, vector DB, web)
3. Evaluates retrieved content with a validation agent before generating

**Practical finding**: improve search quality *before* adding agentic retrieval. An agentic wrapper on poor search just burns more compute on bad results. Fix chunking, metadata, embedding tuning, and re-ranking first.

See [[agentic-rag]].

### 5. The Contractor Model: Formalize Agent Tasks as Contracts

This is the most novel contribution. The paper proposes treating agents not as tools but as **contractors** — service providers with formal task specifications:

- **Required fields**: task description, deliverables, expected cost, expected duration, reporting mechanism
- **Agents can**: negotiate ambiguous specs, flag scope gaps, generate subcontracts for delegated work
- **Lifecycle**: Contract Assessment → Execution → Resolution → (optional) Revision

**Why it matters**: the primary failure mode when moving from prototype to production is underspecification. The contractor model forces you to specify what "done" looks like, what it should cost, and how you'll know if something went wrong — before the agent starts.

---

## What This Changes in the Wiki

- **Open question from [[agentic-ai]]**: "How do you formally specify 'correct' agent behavior?" — the contractor model is Google's answer.
- **[[llm-evals]]**: trajectory evaluation (6 metrics) was missing. Now the wiki has concrete metric definitions.
- **[[agent-observability]]**: success metrics hierarchy (traces = diagnostic, not continuous) is a useful refinement.
- **[[multi-agent-systems]]**: the 5 architectural patterns are grounded in a real production deployment, not theory.

---

## Limitations to Keep in Mind

- No empirical comparisons between evaluation approaches
- Contractor model is proposed/theoretical — no production validation numbers
- Heavy Vertex AI angle throughout — recommendations assume Google stack
- Multi-agent evaluation section acknowledges the problem but doesn't solve scalability of trajectory eval for large systems

---

## Related
[[agentops]] · [[multi-agent-systems]] · [[agentic-rag]] · [[llm-evals]] · [[agentic-ai]] · [[agent-observability]] · [[llm-as-judge]]
