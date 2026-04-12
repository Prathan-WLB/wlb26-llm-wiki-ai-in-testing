---
title: Multi-Agent Systems
type: concept
axis: both
tags: [multi-agent, agentic-ai, orchestration, design-patterns, evaluation]
related: [[agentic-ai]], [[agentops]], [[llm-evals]], [[agent-observability]], [[agentic-rag]], [[google-agents-companion]]
created: 2026-04-12
updated: 2026-04-12
---

# Multi-Agent Systems

## Definition
A multi-agent system is an architecture where multiple specialized AI agents collaborate to achieve complex objectives that no single agent could handle alone. Each agent is an independent entity — potentially using a different LLM — with its own unique role, context, and tools. Agents communicate and coordinate to achieve a common goal.

The analogy: a team of experts rather than one generalist. The Navigation Agent finds locations; the Media Agent knows music; the Car Manual Agent answers vehicle questions. Together they create an experience no single agent could.

## ความหมาย
ระบบ multi-agent คือสถาปัตยกรรมที่ AI agent เฉพาะทางหลายตัวร่วมกันบรรลุเป้าหมายที่ซับซ้อนซึ่ง agent ตัวเดียวไม่สามารถจัดการได้ เปรียบเหมือนทีมผู้เชี่ยวชาญแทนที่จะเป็น generalist คนเดียว

---

## Why It Matters
Single-agent systems hit practical limits: context windows fill up, a single LLM can't be expert at everything, and large tasks can't parallelize. Multi-agent systems break through these limits — and introduce a new class of engineering and evaluation challenges.

Advantages over single-agent:
- **Enhanced accuracy** — agents cross-check each other's work
- **Parallelism** — agents work simultaneously on different subtasks
- **Specialization** — each agent optimized for its narrow domain
- **Scalability** — add more agents to expand capability
- **Fault tolerance** — if one agent fails, others can compensate
- **Reduced hallucinations** — multiple-perspective cross-validation

## ความสำคัญ
ระบบ single-agent มีข้อจำกัดในทางปฏิบัติ: context window เต็ม, LLM ตัวเดียวเชี่ยวชาญทุกอย่างไม่ได้, งานขนาดใหญ่ทำแบบขนานไม่ได้ ระบบ multi-agent แก้ปัญหาเหล่านี้ แต่นำมาซึ่งความท้าทายด้านวิศวกรรมและการประเมินใหม่

---

## System Types

| Type | Description | Example |
|------|-------------|---------|
| **Sequential** | Agents work in pipeline; each completes before passing to next | Assembly line: each stage processes before handing off |
| **Hierarchical** | Manager agent coordinates; worker agents execute | Leader makes strategic decisions; followers execute tasks |
| **Collaborative** | Agents share information and resources toward a common goal | Research team where each member contributes expertise |
| **Competitive** | Agents optimize individually; may compete for resources | LLMs acting as players in a game, coordinating while competing |

## ประเภทของระบบ

| ประเภท | คำอธิบาย |
|--------|----------|
| **Sequential** | Agent ทำงานตามลำดับ แต่ละตัวส่งต่อผลลัพธ์ให้ถัดไป |
| **Hierarchical** | Manager agent ประสานงาน; worker agent ดำเนินการ |
| **Collaborative** | Agent แบ่งปันข้อมูลและทรัพยากรเพื่อเป้าหมายร่วม |
| **Competitive** | Agent optimize แต่ละตัวเอง อาจแข่งขันกันเพื่อทรัพยากร |

---

## Agent Role Taxonomy

Agents within a multi-agent system can be categorized by function:

- **Planner agents** — break high-level objectives into structured subtasks
- **Retriever agents** — dynamically fetch relevant data from external sources (see [[agentic-rag]])
- **Execution agents** — perform computations, generate responses, interact with APIs
- **Evaluator agents** — monitor and validate responses for coherence and alignment

## อนุกรมวิธานบทบาทของ Agent

- **Planner agent** — แยกย่อยเป้าหมายระดับสูงเป็น subtask ที่มีโครงสร้าง
- **Retriever agent** — ดึงข้อมูลจากแหล่งภายนอกแบบ dynamic (ดู [[agentic-rag]])
- **Execution agent** — ดำเนินการคำนวณ สร้าง response โต้ตอบกับ API
- **Evaluator agent** — ติดตามและตรวจสอบ response ว่าสอดคล้องกันและบรรลุเป้าหมาย

---

## Architectural Patterns

### Hierarchical Pattern
A central Orchestrator Agent classifies queries and routes them to appropriate specialized agents. The orchestrator maintains conversation context across turns, manages fallback when specialists can't respond, and resolves ambiguous intent.

```
         Orchestrator
    ┌────┬────┬────┬────┐
  Nav  Media  Msg  Manual  ...
```

**Best for**: clear domain boundaries, high request volume, when orchestrator classification accuracy is high.

### Diamond Pattern
A variation of Hierarchical where all agent responses pass through a central Rephraser/Moderator agent before reaching the user. The Rephraser adapts tone, information density, and style to user context (e.g., simpler language while driving, more formal in professional settings).

```
         Orchestrator
    ┌────┬────┬────┬────┐
  Nav  Media  Msg  Manual
    └────┴────┴────┴────┘
              ↓
          Rephraser
              ↓
            User
```

**Best for**: user-facing systems where response style/safety consistency matters.

### Peer-to-Peer Pattern
Agents can hand off queries to one another when they detect misrouting. Creates resilience — the central orchestrator doesn't need perfect classification accuracy. Specialized agents have better boundary awareness of their own domain than a general orchestrator.

```
  Media Search ↔ Navigation ↔ Car Manual ↔ Knowledge ↔ Message
  (any agent can redirect to any other)
```

**Advantages over pure hierarchical**: resilience to misclassification; domain experts know their own boundaries; reduces orchestrator complexity.

### Collaborative / Response Mixer Pattern
Multiple agents address different aspects of the same query simultaneously. A Response Mixer Agent evaluates answers based on accuracy and relevance, removes incorrect information, and combines the best parts from each specialist response. Uses confidence scores to weight responses.

**Best for**: queries that span multiple domains; safety-critical questions where missing any perspective would be harmful.

### Adaptive Loop Pattern
An agent iteratively reformulates failed queries until results meet desired criteria. Instead of returning "no results," the agent automatically broadens or reformulates the search across multiple passes.

Example: "Find a vegan Italian restaurant" → fails → "Italian restaurants with vegetarian options" → still fails → "Italian restaurants" filtered for plant-based → final fallback.

**Best for**: search and retrieval tasks where exact matches are rare and the user needs best-available rather than empty results.

## รูปแบบสถาปัตยกรรม

รูปแบบหลัก 5 แบบ:
- **Hierarchical**: Orchestrator กลางกำหนดเส้นทาง
- **Diamond**: Hierarchical + Rephraser agent กรองก่อนส่งถึงผู้ใช้
- **Peer-to-Peer**: Agent ส่งต่อให้กันเมื่อตรวจพบการกำหนดเส้นทางผิด
- **Collaborative/Response Mixer**: Agent หลายตัวตอบพร้อมกัน; Mixer รวมคำตอบที่ดีที่สุด
- **Adaptive Loop**: Agent ปรับปรุง query ซ้ำๆ จนกว่าจะได้ผลลัพธ์ที่ดีพอ

---

## Important Components

Beyond the LLM and tools, multi-agent systems require:

- **Interaction Wrapper** — interface managing input/output modalities (text, voice, structured data)
- **Memory Management** — short-term (session, cache), long-term (user profiles, learned patterns), and reflection (deciding what moves from short to long-term)
- **Cognitive Functionality** — Chain-of-Thought, ReAct, Tree-of-Thoughts for complex reasoning; user intent refinement (ask a clarifying question when uncertain)
- **Tool Integration** — dynamic tool registries enabling discovery, registration, and "Tool RAG" (selecting the right tool from a large set)
- **Flow / Routing** — governs agent-to-agent connections; delegation, handoff, or using an agent as a tool
- **Agent Communication** — structured protocols for inter-agent messages; important for consensus on complex problems
- **Remote Agent Communication** — asynchronous tasks that outlast a user session; durable task state, notification mechanisms
- **Agent & Tool Registry (mesh)** — critical as the number of agents/tools grows; stores ontology, capabilities, requirements, and performance metrics; agents select from the registry to make plans

---

## Challenges

Multi-agent systems multiply single-agent problems and add new ones:

| Challenge | Description |
|-----------|-------------|
| **Task Communication** | Most frameworks communicate via messages, not structured async tasks — fragile for complex workflows |
| **Task Allocation** | Efficiently dividing complex tasks among agents; feedback loops often must be hand-coded |
| **Coordinating Reasoning** | Getting agents to debate and reason together requires sophisticated mechanisms |
| **Managing Context** | Tracking all information, tasks, and conversations across agents can overwhelm context limits |
| **Time and Cost** | Multi-agent interactions are computationally expensive; higher latency and runtime cost |
| **Complexity** | Like microservices, the system as a whole becomes more complex than the sum of its parts |

## ความท้าทาย

| ความท้าทาย | คำอธิบาย |
|-----------|----------|
| **Task Communication** | Framework ส่วนใหญ่สื่อสารด้วย message ไม่ใช่ async task ที่มีโครงสร้าง |
| **Task Allocation** | แบ่งงานที่ซับซ้อนระหว่าง agent อย่างมีประสิทธิภาพ; feedback loop มักต้องโค้ดเอง |
| **Coordinating Reasoning** | การให้ agent debate กันต้องการกลไกที่ซับซ้อน |
| **Managing Context** | ติดตาม context ทั้งหมดระหว่าง agent อาจเกิน context limit |
| **Time and Cost** | ต้นทุนการคำนวณสูง; latency เพิ่มขึ้น |
| **Complexity** | ระบบโดยรวมซับซ้อนกว่าผลรวมของส่วนประกอบ |

---

## Multi-Agent Evaluation

Multi-agent evaluation is a direct extension of single-agent evaluation. The same metrics apply: business north star, goal completion rate, telemetry, human feedback, and traces. Key additional questions:

- **Cooperation and Coordination**: how well do agents work together to achieve common goals?
- **Planning and Task Assignment**: did the right plan emerge? Did child agents deviate or get lost?
- **Agent Utilization**: did the system select the right agent as a tool, delegate the background task correctly, transfer the user appropriately?
- **Scalability**: does quality improve (or at least hold) as more agents are added? Does latency scale reasonably?

Because multi-agent systems have more steps, trajectory evaluation at the *system* level means a trajectory that spans multiple agents. Each agent can also be evaluated in isolation. Both views are needed.

## การประเมิน Multi-Agent

การประเมิน multi-agent เป็นการขยายตรงจากการประเมิน single-agent metric เดิมยังใช้ได้ แต่เพิ่มคำถามเรื่อง: การร่วมมือและประสานงาน, การวางแผนและมอบหมายงาน, การใช้ agent อย่างมีประสิทธิภาพ, และ scalability

---

## Current State
Active and rapidly maturing (2025). Production deployments exist (automotive, enterprise search, scientific research). Tooling: LangGraph (multi-agent orchestration), AutoGen (Microsoft), CrewAI. Key unsolved problem: standardized inter-agent communication protocols. Most frameworks still use ad-hoc message passing. The "contractor" model ([[google-agents-companion]]) is a proposed evolution toward formal task specification.

## สถานะปัจจุบัน
กำลังพัฒนาอย่างรวดเร็ว (ปี 2568) มีการ deploy ใน production แล้ว ปัญหาที่ยังไม่แก้ไข: โปรโตคอลการสื่อสารระหว่าง agent ที่เป็นมาตรฐาน

---

## Open Questions
- How do you formally specify and test emergent behavior in multi-agent systems — behaviors that arise from agent interaction but were not programmed into any single agent?
- At what scale does a centralized orchestrator become a bottleneck? How do you decide when to switch to peer-to-peer routing?
- How do you attribute quality improvements or failures to specific agents in a collaborative system?

---

## Related
[[agentic-ai]] · [[agentops]] · [[llm-evals]] · [[agent-observability]] · [[agentic-rag]]
[[google-agents-companion]] (source — automotive case study, contractor model, evaluation section)
[[prompts-to-production-agentic-playbook]] (source — Supervisor, Hierarchical patterns)
[[one-year-of-agentic-ai-six-lessons]] (source — multi-agent deployment lessons)
