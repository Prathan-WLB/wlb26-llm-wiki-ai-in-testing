---
title: The Contractor Model as an Answer to the Oracle Problem
type: synthesis
axis: both
tags: [oracle-problem, contractor-model, agent-evaluation, specification, agentic-ai, llm-evals]
related: [[agentic-ai]], [[llm-evals]], [[agentops]], [[multi-agent-systems]], [[google-agents-companion]], [[human-role-in-ai-agents]]
created: 2026-04-12
updated: 2026-04-19
---

# The Contractor Model as an Answer to the Oracle Problem

**Key Theme #1** of this wiki is the Oracle Problem: defining "correct behavior" is the hard part in both axes (AI for Testing and Testing for AI). This page argues that Google's **contractor model** ([[google-agents-companion]]) is the most concrete proposed answer to this problem for agentic systems — and examines where it succeeds and where it still falls short.

---

## What the Oracle Problem Is

In software testing, the oracle problem is the challenge of knowing whether a test outcome is correct. For deterministic software, this is manageable — you specify expected outputs. For AI systems, it becomes severe:

- LLM outputs are probabilistic. The same input yields different outputs across runs.
- "Correct" is often context-dependent, subjective, or requires domain expertise to judge.
- Multi-step agents can produce a correct final answer via an incorrect or unreliable path.
- Emergent behaviors in multi-agent systems were not anticipated at design time.

The oracle problem shows up in both wiki axes:
- **AI for Testing** — when LLMs generate test cases, how do you know the generated tests are correct? Who evaluates the evaluator?
- **Testing for AI** — when you eval an agent, what is the ground truth you're comparing against? How do you specify the "right" trajectory?

The field has partial solutions (see [[llm-evals]]: LLM-as-judge, trajectory metrics, human eval). None fully solves the oracle problem — they displace it. LLM-as-judge replaces one oracle question with another: is the judge LLM reliable?

---

## What the Contractor Model Proposes

From [[google-agents-companion]], the contractor model reframes agents from tools (you invoke, they respond) to **contractors** (you specify a job, they execute it within agreed constraints).

A formal agent contract contains:

| Field | Required | Oracle relevance |
|-------|----------|-----------------|
| Task/Project description | Yes | Defines the goal |
| Deliverables & Specifications | Yes | **Defines done** — the oracle |
| Expected Cost | Yes | Bounds the acceptable execution cost |
| Expected Duration | Yes | Bounds the acceptable time window |
| Reporting and Feedback | Yes | Defines the signal the oracle uses to judge |
| Scope | Optional | Defines what's out of scope — constrains acceptable paths |
| Input Sources | Optional | Constrains retrieval — narrows the oracle's reference space |

**The oracle insight**: by forcing the human to fill in "Deliverables & Specifications" and "Reporting and Feedback" before the agent starts, the contract *externalizes* the oracle definition. The agent isn't run against a vague prompt and evaluated ad hoc — it's run against explicit success criteria that were committed to in advance.

Agents can also **negotiate** the contract: flag ambiguous deliverables, request clarification on scope, generate subcontracts for delegated subtasks. This turns oracle specification into a dialogue rather than a one-time assumption.

---

## Where This Connects to Trajectory Evaluation

The contractor model sets the oracle; trajectory evaluation (also from [[google-agents-companion]]) measures compliance with it.

The six trajectory metrics map onto the contract fields:

| Trajectory metric | What it checks against the contract |
|-------------------|------------------------------------|
| Exact match | Did the agent follow the specified procedure exactly? |
| In-order match | Did it follow the required sequence, with allowed variation? |
| Any-order match | Did it hit all required steps, regardless of order? |
| Precision | Did it avoid steps outside the contract scope? |
| Recall | Did it execute all steps the contract requires? |
| Single-tool use | Did it use the specific tool the contract specifies? |

Together: the contract defines the reference trajectory; trajectory metrics measure how closely the agent's actual trajectory matched it.

This is a closed loop: **contract → reference trajectory → eval metrics → feedback → contract revision**.

---

## The Displacement Problem: What's Still Unsolved

The contractor model is a genuine improvement, but it displaces rather than solves the oracle problem:

**1. Who writes the contract?**
Filling in "Deliverables & Specifications" requires a human with domain expertise. For novel or open-ended tasks, this is hard — the oracle problem reappears one level up.

**2. Who validates the contract itself?**
A poorly written contract produces an agent that executes faithfully to wrong criteria. Contract correctness is not guaranteed by the contract format.

**3. The reference trajectory problem.**
Creating a reference trajectory (required for all six trajectory metrics) requires a domain expert to walk through the ideal path. This is expensive and doesn't scale to the full distribution of queries an agent will encounter.

**4. Emergent multi-agent behavior.**
The contractor model works well for single-agent or clearly delegated multi-agent tasks. In [[multi-agent-systems]] with collaborative or competitive coordination, behavior emerges from agent interaction — no single contract captures the expected system behavior.

**5. Dynamic contracts.**
Real tasks change. A contractor model with static contract fields may be brittle when the task scope shifts mid-execution.

---

## How the Two Wiki Axes Are Affected Differently

### AI for Testing axis
The contractor model is directly applicable to agentic test generation:
- A test generation agent receives a contract specifying: what code to test, what kinds of tests are desired (unit / integration / property-based), what coverage threshold counts as done, and what the reporting mechanism is.
- The deliverables field forces explicit oracle definition for generated tests: are the tests correct if they pass? If they find bugs? If they meet coverage? This must be stated before the agent runs.
- Contract negotiation handles cases where the code is ambiguous — the agent asks rather than hallucinating a test spec.

### Testing for AI axis
The contractor model reframes agent eval itself:
- An eval framework can be structured as a contract audit: does the agent's execution comply with the contract it was given?
- Trajectory evaluation becomes contract compliance checking.
- The "Reporting and Feedback" field maps directly to eval signal design — making eval design an explicit part of task specification rather than an afterthought.

---

## Synthesis: What This Changes

The contractor model is the field's clearest statement that **the oracle problem for agents is primarily a specification problem**, not a measurement problem. We have trajectory metrics; we have LLM-as-judge; we have human eval. What we lacked was a structured way to commit to the oracle *before* execution rather than construct it *after* seeing the output.

The contractor model's contribution is procedural: it makes oracle specification a required step, not an optional one.

Its limitation is identical: the procedure only works if the humans filling in the contract know what "done" looks like. For novel, open-ended, or emergent tasks, that knowledge may not exist in advance. The oracle problem for those cases remains open.

**Open question worth pursuing**: Is there a category of tasks where the contractor model fully resolves the oracle problem (bounded, well-defined, expert-specified tasks), and a category where it cannot (open-ended, exploratory, emergent tasks)? Mapping that boundary would be a useful contribution to the field.

---

## Related
[[agentic-ai]] · [[llm-evals]] · [[agentops]] · [[multi-agent-systems]] · [[llm-as-judge]] · [[human-role-in-ai-agents]]
[[google-agents-companion]] (primary source — contractor model, trajectory evaluation)
[[one-year-of-agentic-ai-six-lessons]] (context — oracle problem in enterprise evals)
