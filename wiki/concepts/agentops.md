---
title: AgentOps
type: concept
axis: both
tags: [agentops, operationalization, devops, mlops, agent-evaluation, observability, metrics]
related: [[agentic-ai]], [[agent-observability]], [[llm-evals]], [[multi-agent-systems]], [[google-agents-companion]]
created: 2026-04-12
updated: 2026-04-12
---

# AgentOps

## Definition
AgentOps (Agent and Operations) is a subcategory of GenAIOps focused on the efficient operationalization of AI agents in production. It extends DevOps and MLOps practices with agent-specific concerns: tool management, agent brain prompt engineering, memory systems, and task decomposition.

## ความหมาย
AgentOps คือ subcategory ของ GenAIOps ที่เน้นการนำ AI agent ไปใช้งานใน production อย่างมีประสิทธิภาพ ขยายต่อจาก DevOps และ MLOps โดยเพิ่มความกังวลเฉพาะ agent: การจัดการ tool, การ engineer agent brain prompt, ระบบ memory, และการแยกย่อยงาน

---

## Why It Matters
Getting from proof-of-concept to production is the hardest part of agent development. Quality and reliability are the most cited blockers. AgentOps provides the framework to bridge this gap — it is to agents what DevOps was to software deployments: a discipline that makes reliable, measurable production operation the default rather than the exception.

The classic failure mode: a team builds an impressive demo, deploys it, sees mysterious quality drops, and can't diagnose why because no metrics or traces were instrumented from the start.

## ความสำคัญ
การก้าวจาก proof-of-concept สู่ production คือส่วนที่ยากที่สุดของการพัฒนา agent คุณภาพและความน่าเชื่อถือคืออุปสรรคหลักที่ถูกอ้างถึง AgentOps ให้กรอบการทำงานเพื่อข้ามช่องว่างนี้

---

## The Ops Hierarchy

```
DevOps
  └── MLOps          (adds: non-deterministic ML model concerns)
        └── FMOps    (adds: pre-trained foundation model concerns)
              └── GenAIOps  (adds: prompt engineering, application development)
                    ├── PromptOps   (prompt storage, lineage, evaluation scores)
                    ├── RAGOps      (retrieval pipeline, chunking, re-ranking)
                    └── AgentOps   (← here)
```

Each layer inherits from the one above. DevOps and MLOps best practices are still required — security, authentication, throttling, CI/CD, version control, and metrics-driven development all apply. AgentOps adds on top, it doesn't replace.

## ลำดับชั้นของ Ops

DevOps เป็นรากฐาน MLOps สร้างต่อโดยเพิ่มความกังวลเรื่อง ML model ที่ไม่แน่นอน FMOps เพิ่มการจัดการ foundation model GenAIOps เพิ่มการพัฒนา prompt และแอปพลิเคชัน AgentOps อยู่ภายใต้ GenAIOps พร้อมกับ PromptOps และ RAGOps

---

## How It Works — Agent Success Metrics

The key insight: **you cannot improve what you don't measure**. AgentOps defines a hierarchy of metrics to instrument before writing agent logic.

### North Star: Business Metrics
Revenue, user engagement, cost reduction. These are outside the agent's direct control but must be the ultimate reference point. Without a clear north star, you can optimize trajectory scores while losing business value.

### Primary: Goal Completion Rate
Most agents are designed to accomplish goals. **Goal completion rate** — what fraction of attempted goals does the agent complete successfully — is the single most important agent-level metric. Decompose each goal into critical subtasks and instrument each independently.

### Telemetry: Latency, Errors, Throughput
Standard application metrics. More important for agents than for deterministic software because agents can appear to complete a task while having produced incorrect output — latency and error rates alone don't tell you about quality.

### Qualitative: Human Feedback
A simple thumbs up/down or rubric review from end users, QA testers, or domain experts provides signal that automated metrics miss. Human feedback can also calibrate whether your autoraters (LLM-as-judge) are aligned with human judgment.

### Diagnostic: Traces
Traces capture every internal step: tool calls, retrieval queries, intermediate outputs, and decision branches. **Traces are not ongoing metrics** — measuring every internal step continuously is usually impractical. Instead, use traces to debug specific failures identified by the metrics above.

## วิธีการทำงาน — Agent Success Metrics

ข้อมูลเชิงลึกหลัก: **ไม่สามารถปรับปรุงสิ่งที่ไม่ได้วัด** AgentOps กำหนดลำดับชั้น metric ที่ต้อง instrument ก่อนเขียน logic ของ agent

### ดาวนำทาง: Business Metrics
รายได้, การมีส่วนร่วมของผู้ใช้, การลดต้นทุน สิ่งเหล่านี้อยู่นอกการควบคุมโดยตรงของ agent แต่ต้องเป็นจุดอ้างอิงสูงสุด

### หลัก: Goal Completion Rate
**อัตราการบรรลุเป้าหมาย** — เป็น metric ระดับ agent ที่สำคัญที่สุดตัวเดียว แยกย่อยแต่ละเป้าหมายเป็น subtask สำคัญและ instrument แต่ละ subtask แยกกัน

### Telemetry: Latency, Errors, Throughput
Metric แอปพลิเคชันมาตรฐาน สำคัญมากกว่าสำหรับ agent เพราะ agent อาจดูเหมือนทำงานเสร็จแต่จริงๆ ให้ output ที่ผิด

### เชิงคุณภาพ: Human Feedback
ข้อมูล feedback จากมนุษย์ให้สัญญาณที่ metric อัตโนมัติพลาด และยังช่วย calibrate autorater ด้วย

### วินิจฉัย: Traces
Trace บันทึกทุก step ภายใน ไม่ใช่ metric ต่อเนื่อง ใช้เพื่อ debug ความล้มเหลวเฉพาะที่ metric ระบุ

---

## AgentOps-Specific Components

Beyond standard DevOps/MLOps tooling, AgentOps adds:

- **Tool management** — internal tools (functions, APIs the agent can call) and external tools (APIs, data stores). Tool use inherits standard API management concerns (auth, throttling, rate limits, versioning).
- **Agent brain prompt** — the goal, profile, and instructions that define agent identity and behavior. Requires its own versioning and A/B testing discipline.
- **Orchestration** — memory, state, reasoning framework (ReAct, CoT, ToT). How the agent cycles through perceive → reason → act loops.
- **Memory** — short-term (session context, working memory) and long-term (learned patterns, user profiles, example stores). Reflection: which short-term items should persist to long-term?
- **Task decomposition** — how complex goals are broken into subtasks. In multi-agent systems, how tasks are delegated to specialized agents.

## องค์ประกอบเฉพาะของ AgentOps

นอกจากเครื่องมือ DevOps/MLOps มาตรฐาน AgentOps เพิ่ม: การจัดการ Tool, Agent Brain Prompt, Orchestration, Memory (ระยะสั้นและยาว), และ Task Decomposition

---

## A/B Experimentation for Agents

The AgentOps mental model for continuous improvement: run A/B experiments where treatment gets the new agent and control gets the old. Before launching any agent change, define which metrics you're optimizing and what threshold constitutes success. The business north star, goal completion rate, and critical task success rates must all be understood, instrumented, and analyzable before any A/B result is meaningful.

---

## Current State
Emerging discipline (2025). Terminology is still being standardized — "AgentOps," "LLMOps," "GenAIOps" are used inconsistently across the industry. The core insight (inherit DevOps/MLOps, layer agent-specific concerns on top) is gaining consensus. Tooling is maturing: Vertex AI Eval Service, LangSmith, and OpenTelemetry-based tracing are common components.

## สถานะปัจจุบัน
สาขาที่กำลังเกิดขึ้น (ปี 2568) คำศัพท์ยังไม่ได้มาตรฐาน แต่แนวคิดหลัก (สืบทอด DevOps/MLOps แล้วเพิ่มความกังวลเฉพาะ agent) กำลังได้รับการยอมรับ

---

## EU AI Act Compliance Implications

**Article 14** of the EU AI Act (effective 2 August 2026) adds legal weight to several AgentOps components for any agent system classified as high-risk:

| AgentOps Component | Article 14 Requirement |
|-------------------|----------------------|
| **Emergency stop mechanism** | Art. 14(4)(e): overseer must be able to interrupt the system via a "stop" button or equivalent |
| **Override capability** | Art. 14(4)(d): overseer must be able to disregard, override, or reverse system output at any time |
| **Monitoring infrastructure** | Art. 14(4)(a): overseer must be able to duly monitor operation — observability is legally required |
| **Output interpretability** | Art. 14(4)(c): output must be correctly interpretable by the overseer |
| **Automation bias countermeasures** | Art. 14(4)(b): system must keep overseer aware of over-reliance risk |

The **dual provider/deployer structure** of Art. 14(3) maps directly onto AgentOps deployment:
- **Provider responsibility**: build oversight features in before placing on market (stop button, override mechanism, monitoring hooks)
- **Deployer responsibility**: implement operational oversight measures — cannot rely entirely on provider-built features

> **Extends [[eu-ai-act-article-14-human-oversight]]**: AgentOps is the operational framework through which Article 14 compliance is implemented.

---

## Open Questions
- Where exactly does AgentOps end and application observability begin? At what granularity should traces be collected in production?
- How do you run A/B experiments on agents when execution paths are non-deterministic and small sample sizes may not reach statistical significance?
- How does AgentOps change for multi-agent systems where no single "goal completion" can be attributed to one agent?

---

## Related
[[agentic-ai]] · [[agent-observability]] · [[llm-evals]] · [[multi-agent-systems]] · [[automation-bias]]
[[google-agents-companion]] (source)
[[eu-ai-act-article-14-human-oversight]] (source — Art. 14 compliance requirements map to AgentOps components)
