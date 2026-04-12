---
title: "Agents Companion (Google, 2025)"
type: paper
axis: both
tags: [agentic-ai, agentops, agent-evaluation, multi-agent, agentic-rag, trajectory-evaluation, enterprise-ai, google]
related: [[agentic-ai]], [[llm-evals]], [[agent-observability]], [[agentops]], [[multi-agent-systems]], [[agentic-rag]], [[llm-as-judge]]
created: 2026-04-12
updated: 2026-04-12
---

# Agents Companion (Google, 2025)

## Citation
Gulli, A., Nigam, L., Wiesinger, J., Vuskovic, V., Sigler, I., Nardini, I., Stroppa, N., Kartakis, S., Saribekyan, N., Nawalgaria, A., & Bount, A. (February 2025). *Agents Companion*. Google. (Editor: Nawalgaria, A.)

This is a "102" companion to Google's original Agents whitepaper — intended for developers already familiar with agent basics, covering advanced evaluation methodologies, multi-agent systems, Agentic RAG, and enterprise deployment.

---

## Core Claim
Getting a gen AI agent from proof-of-concept to production is hard — quality and reliability are the chief obstacles. The paper argues that **AgentOps** (a disciplined operational framework) + **automated evaluation** (trajectory + final response) + **multi-agent design patterns** constitute the practical path from prototype to production.

---

## Key Contributions

- **AgentOps taxonomy**: places agent operationalization within the MLOps → GenAIOps → AgentOps hierarchy, with specific components beyond standard DevOps/MLOps (tool management, agent brain prompt, memory, task decomposition)
- **Trajectory evaluation**: formalizes 6 automated evaluation metrics for the *steps an agent takes*, not just its final answer (exact match, in-order match, any-order match, precision, recall, single-tool use)
- **Multi-agent design patterns**: catalogs 4 system types (Sequential, Hierarchical, Collaborative, Competitive) and 5 architectural patterns (Hierarchical, Diamond, Peer-to-Peer, Collaborative, Response Mixer, Adaptive Loop)
- **Agentic RAG**: defines autonomous retrieval agents that actively refine queries, select sources, and cross-validate retrieved content — solving problems that static RAG fails on (ambiguous, multi-step, multi-perspective queries)
- **Agents-to-Contractors model**: proposes formalizing agent tasks as "contracts" with deliverables, expected cost/duration, and feedback mechanisms — addresses underspecification as the primary prototype-to-production failure mode
- **Automotive AI case study**: detailed real-world multi-agent deployment illustrating trade-offs between on-device (fast, offline) and cloud (capable, online) agents

---

## Method
Practitioner-authored technical whitepaper synthesizing Google's internal deployments, Vertex AI product experience, and academic references. Not an empirical study — no A/B data. References external benchmarks (BFCL, τ-bench, PlanBench, AgentBench, DABStep) and third-party frameworks (LangSmith, LangGraph).

---

## Results / Key Findings

**Agent architecture**: Three mandatory components — Model (LM as decision-making unit), Tools (extensions, functions, data stores), Orchestration layer (memory, state, reasoning — ReAct, CoT, ToT applicable here).

**Agent Success Metrics hierarchy**:
1. Business metrics (revenue, engagement) — north star, outside agent scope itself
2. Goal completion rate — primary agent-level KPI
3. Critical task success rates — per-subtask
4. Application telemetry (latency, errors)
5. Human feedback (thumbs up/down, QA review)
6. Detailed traces — for debugging, not continuous metric collection

**Trajectory evaluation — 6 metrics** (ground-truth based):
| Metric | What it measures |
|--------|-----------------|
| Exact match | Full trajectory matches reference exactly |
| In-order match | Core steps in correct order; extra steps allowed |
| Any-order match | All required steps present; order irrelevant |
| Precision | What fraction of predicted steps are in the reference? |
| Recall | What fraction of reference steps appear in prediction? |
| Single-tool use | Did the agent use a specific tool at all? |

**Evaluation method trade-offs** (Table 1 from paper):
| Method | Strengths | Weaknesses |
|--------|-----------|------------|
| Human evaluation | Nuanced, considers human factors | Expensive, slow, hard to scale |
| LLM-as-Judge | Scalable, efficient, consistent | May miss intermediate steps; limited by LLM |
| Automated metrics | Objective, scalable | May not capture full capabilities; gameable |

**Multi-agent system types**: Sequential (pipeline), Hierarchical (manager → workers), Collaborative (shared goal, information sharing), Competitive (agents optimize individually, may compete).

**Agent role taxonomy**: Planner (decompose objectives), Retriever (fetch external data), Execution (compute/generate/API calls), Evaluator (validate outputs for coherence).

**Agentic RAG advantages over static RAG**: Context-aware query expansion (multiple refinement passes), multi-step reasoning (sequential retrieval building structured responses), adaptive source selection, validation agents cross-checking for hallucinations.

**Contractor model** (novel): tasks defined as formal contracts with fields: Task/Project description (required), Deliverables & Specifications (required), Scope (optional), Expected Cost (required), Expected Duration (required), Input Sources (optional), Reporting and Feedback (required). Contractors can negotiate, flag ambiguities, generate subcontracts. Lifecycle: Contract Assessment → Contract Execution → Task Resolution → (optional) Contract Revision.

**Automotive AI case study** — patterns in production:
- *Hierarchical*: Orchestrator routes to specialized agents
- *Diamond*: Hierarchical + Rephraser agent post-processes responses for tone/context
- *Peer-to-Peer*: Agents detect misrouting and hand off directly; more resilient to orchestrator errors
- *Collaborative/Response Mixer*: Multiple agents answer simultaneously; mixer selects best parts
- *Adaptive Loop*: Agent iteratively reformulates failed queries until criteria met

**Google Co-Scientist** case study: multi-agent scientific research system using "generate, debate, evolve" loop. Components: Generation Agent, Reflection Agent, Ranking Agent (tournament), Evolution Agent, Proximity Check Agent, Meta-review Agent. Applied to liver fibrosis research — identified new drug candidates.

---

## Limitations

- No empirical performance data comparing the evaluation frameworks to each other
- Contractor model is proposed/theoretical — no production validation data
- Heavy vendor angle: Vertex AI Agent Builder, Agentspace, Vertex AI Eval Service, Gemini models are repeatedly positioned as the solution stack
- Multi-agent evaluation section acknowledges the problem space more than it solves it — scalability of trajectory eval for large multi-agent systems is left as future work
- Automotive case study is illustrative, not benchmarked

---

## My Take

This paper is the most concrete operationalization guide for production agents I've seen. The **trajectory evaluation taxonomy** (6 metrics) is immediately applicable and fills a gap in [[llm-evals]] — we had "evaluate trajectory" as a concept but lacked specific metrics. The **contractors model** is genuinely novel: it reframes the agent-as-tool mental model toward agent-as-service-provider, which matters for high-stakes enterprise deployments where scope ambiguity is the failure mode.

The **AgentOps hierarchy** (DevOps → MLOps → FMOps → GenAIOps → AgentOps) provides a useful anchor for understanding where agent concerns diverge from traditional software ops. This extends [[agent-observability]] significantly — observability is necessary but not sufficient; you also need goal completion rate, task decomposition management, and tool registry.

The paper reinforces the wiki's Key Theme #4 (Agents Change the Testing Problem) with concrete evidence. It also directly addresses the open question from [[agentic-ai]]: "How do you formally specify 'correct' agent behavior?" — the contractor model is Google's answer.

One tension: the paper says LLM-as-Judge "may overlook intermediate steps" but also recommends autoraters (= LLM-as-Judge) for final response evaluation. The recommendation is to pair autoraters with trajectory evaluation, not use either alone.

> **Extends [[agentic-ai]]**: 3-component architecture definition, enterprise agent types (Assistants vs Automation), new orchestration patterns (Diamond, Peer-to-Peer, Adaptive Loop, Response Mixer)
> **Extends [[llm-evals]]**: trajectory evaluation (6 metrics), autorater concept, evaluation method comparison table
> **Extends [[agent-observability]]**: agent success metrics hierarchy, goal completion rate as north star, trace-for-debugging vs. trace-as-metric distinction

---

## Related
[[agentops]] · [[multi-agent-systems]] · [[agentic-rag]] · [[agentic-ai]] · [[llm-evals]] · [[agent-observability]] · [[llm-as-judge]]
