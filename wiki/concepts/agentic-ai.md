---
title: Agentic AI
type: concept
axis: both
tags: [agentic-ai, llm, automation, multi-agent, orchestration]
related: [[llm-evals]], [[agent-observability]], [[ai-tool-selection-rubric]], [[llm-as-judge]], [[karpathy-llm-wiki-pattern]], [[prompts-to-production-agentic-playbook]]
created: 2026-04-10
updated: 2026-04-11
---

# Agentic AI

## Definition
A system built on gen AI foundation models that can act in the real world and execute multistep processes autonomously. AI agents can automate complex tasks — often using natural language processing — that would normally require human effort.

## ความหมาย
ระบบที่สร้างบน foundation model ของ gen AI ซึ่งสามารถกระทำการในโลกจริงและดำเนินกระบวนการหลายขั้นตอนได้อย่างอัตโนมัติ AI agent สามารถทำงานที่ซับซ้อนซึ่งปกติต้องการความพยายามของมนุษย์ — มักใช้ natural language processing เป็นพื้นฐาน

---

## Why It Matters
Agentic AI is the current frontier of AI deployment in enterprise. Unlike single-turn LLM interactions, agents can plan, use tools, call APIs, and operate across multiple steps to complete a goal. This creates new testing challenges: behavior is harder to predict, errors can compound across steps, and failures may be silent.

## ความสำคัญ
Agentic AI คือแนวหน้าของการ deploy AI ในองค์กรในยุคปัจจุบัน ต่างจากการโต้ตอบกับ LLM แบบ single-turn ทั่วไป agent สามารถวางแผน ใช้เครื่องมือ เรียก API และทำงานข้ามหลายขั้นตอนเพื่อบรรลุเป้าหมาย สิ่งนี้สร้างความท้าทายด้านการทดสอบใหม่: พฤติกรรมคาดเดาได้ยาก ข้อผิดพลาดสะสมข้ามขั้นตอน และความล้มเหลวอาจเกิดขึ้นแบบเงียบๆ

---

## How It Works
A typical agentic system includes:
- A **foundation model (LLM)** — the reasoning core
- **Tools** the agent can call (web search, code execution, database queries, APIs)
- An **orchestration framework** managing agent state, tool calls, and multi-agent coordination (e.g. LangGraph, AutoGen, CrewAI)
- A **memory layer** (context window, retrieval systems, or external state)
- **Human-in-the-loop** checkpoints for oversight and edge cases

In multi-agent systems, agents act as both orchestrators (delegating subtasks) and integrators (assembling outputs from other agents and tools).

### Google's 3-Component Model (Agents Companion, 2025)
Google's [[google-agents-companion]] formalizes agent architecture into three mandatory elements:
- **Model** — the LM as central decision-making unit; general-purpose to multimodal or fine-tuned depending on task
- **Tools** — bridge between internal capabilities and the external world; three types: Extensions (API-to-agent bridge), Functions (self-contained code modules), Data Stores (dynamic, up-to-date information sources)
- **Orchestration Layer** — cyclical process governing how the agent assimilates information, reasons, and acts. Responsible for memory, state, reasoning, and planning. Reasoning frameworks (ReAct, CoT, ToT) operate here.

### กรอบ 3-องค์ประกอบของ Google
Google กำหนด agent architecture เป็น 3 ส่วนบังคับ: **Model** (LM เป็นศูนย์กลางการตัดสินใจ), **Tools** (เชื่อมต่อความสามารถภายในกับโลกภายนอก: Extensions, Functions, Data Stores), **Orchestration Layer** (กระบวนการวนซ้ำจัดการ memory, state, reasoning และ planning)

## กลไกการทำงาน
ระบบ agentic ทั่วไปประกอบด้วย:
- **Foundation model (LLM)** — แกนหลักของการใช้เหตุผล
- **เครื่องมือ (Tools)** — สิ่งที่ agent เรียกใช้ได้ (web search, รันโค้ด, query database, API)
- **Orchestration framework** — จัดการ state, tool call, และการประสานงานระหว่าง agent (เช่น LangGraph, AutoGen, CrewAI)
- **Memory layer** — context window, ระบบ retrieval, หรือ external state
- **Human-in-the-loop** — จุดตรวจสอบสำหรับการดูแลและ edge case

ในระบบ multi-agent, agent ทำหน้าที่ทั้งเป็น orchestrator (มอบหมายงานย่อย) และ integrator (รวบรวม output จาก agent อื่น)

---

## Variants and Orchestration Patterns

### Single Agent
One LLM with tools executing a defined task. Simplest form; use when the task is bounded and clear.

### ReAct Agent (Reason → Act → Observe)
Iterative loop: the agent reasons about what to do, acts (tool call), observes the result, and repeats until a breaking condition is met (explicit completion, confidence threshold reached, or error requiring human intervention). Methodology insight: GPT-3.5 with ReAct looping achieves **95.1% accuracy** on coding benchmarks vs. GPT-4 zero-shot at 67% — methodology beats model size. Best for iterative investigation workflows (e.g., a DB debugging agent that queries, analyzes, and examines indexes until finding root cause).

### Supervisor Agent Pattern
A central supervisor agent assigns subtasks to specialized worker agents, decides which to invoke next, and determines when the workflow is complete. Good for multi-domain workflows requiring centralized planning. Anthropic's Multi-Agent Research System uses this pattern.

### Hierarchical Agent Pattern
When supervisor-to-worker ratios become unwieldy, introduce tiers: worker agents → team supervisors → master supervisor. Evidence: 3-tier hierarchical architectures show 32% absolute improvement in task success rates (Liu et al.) and 95.3% accuracy on complex benchmarks (AgentOrchestra). Example: e-commerce fulfillment with regional supervisors managing warehouse agents.

### Human-in-the-Loop Pattern
Decision points requiring human oversight are embedded in the workflow. AI handles analysis; human provides the decision or review. Example: loan approval workflows.

### Multi-agent pipeline
Specialized agents coordinated by an orchestrator.

### Agentic workflow
A full business process redesigned around agents, where agents handle variable-input steps and simpler rule-based automation handles the deterministic remainder.

## Autonomy Level Framework

Four levels of human involvement (from [[prompts-to-production-agentic-playbook]]):

| Level | Description |
|-------|-------------|
| Human-in-the-Loop | Direct human intervention at workflow decision points |
| Human-on-the-Loop | Human maintains meaningful real-time control |
| Human-above-the-Loop | Strategic governance only |
| Human-behind-the-Loop | Post-operational analysis only |

Choosing the right autonomy level is an architectural decision — not just a product preference. It determines the testing strategy, the observability requirements, and the acceptable failure modes.

## ประเภทและ Pattern Orchestration

### Single Agent
LLM หนึ่งตัวพร้อมเครื่องมือสำหรับงานที่กำหนดไว้ ใช้เมื่องานมีขอบเขตชัดเจน

### ReAct Agent
Loop ซ้ำ: ใช้เหตุผล → กระทำ (tool call) → สังเกต → ทำซ้ำจนเจอ breaking condition ข้อมูลเชิงลึก: GPT-3.5 + ReAct looping ทำได้ **95.1%** เทียบกับ GPT-4 zero-shot ที่ 67% — methodology สำคัญกว่าขนาด model

### Supervisor Pattern
Supervisor กลางมอบหมายงานให้ worker agent เฉพาะทาง ดีสำหรับ workflow หลายโดเมนที่ต้องการการวางแผนจากศูนย์กลาง

### Hierarchical Pattern
เพิ่มลำดับชั้นเมื่อ ratio supervisor ต่อ worker ไม่มีประสิทธิภาพ สถาปัตยกรรม 3 ชั้นแสดงการปรับปรุง 32% ใน task success rate

### Human-in-the-Loop Pattern
ฝัง decision point ที่ต้องการมนุษย์ใน workflow ตัวอย่าง: workflow อนุมัติสินเชื่อ

---

## Enterprise Agent Types (2025)

Two types of enterprise agents are emerging (from [[google-agents-companion]]):

1. **"Assistants"** — Agents that interact with users, take a task, execute it, and return results. Conversational agents (Gems, GPTs) belong here. Can be general-purpose or domain-specialized. May be synchronous (fast, single session) or long-running (deep research agents).

2. **"Automation Agents"** — Agents that run in the background, listen for events, monitor changes in systems or data, and make smart decisions autonomously. Action may include acting on backend systems, validating observations, fixing problems, or notifying employees. These are the backbone of future enterprise automation — replacing hard-coded logic with intelligent decision-making.

Knowledge workers are evolving from "use an agent for a task" to "manage a fleet of agents" — assigning tasks, monitoring progress, and steering when agents need help.

## ประเภท Agent ในองค์กร

1. **"Assistants"** — Agent ที่โต้ตอบกับผู้ใช้ รับงาน ดำเนินการ และส่งคืนผล อาจเป็น synchronous หรือ long-running
2. **"Automation Agents"** — Agent ที่ทำงานเบื้องหลัง ฟัง event ตรวจสอบการเปลี่ยนแปลง และตัดสินใจอัตโนมัติ นี่คือกระดูกสันหลังของ automation ในอนาคต

---

## Current State
Active and fast-moving (late 2025). Early enterprise deployments show mixed results — some strong wins, but also "retrenching" where failed agents are replaced with humans. Tooling is maturing (LangGraph, AutoGen, CrewAI), but best practices for eval, observability, and human-agent collaboration are still being established.

## สถานะปัจจุบัน
กำลังพัฒนาอย่างรวดเร็ว (ปลายปี 2568) การ deploy ในองค์กรระยะแรกให้ผลลัพธ์หลากหลาย — บางส่วนประสบความสำเร็จ แต่ก็มีการ "ถอยหลัง" โดยเอาคนกลับมาแทน agent ที่ล้มเหลว เครื่องมือกำลังเติบโต แต่ best practice ยังอยู่ระหว่างการสร้าง

---

## Connection to AI for Testing
Wave 3 of AI adoption in software testing (2030+, per [[ais-impact-on-software-testing-qa-evolution]]) describes "autonomous end-to-end testing" where AI strategists define quality standards while agents execute the full testing lifecycle. This is agentic AI applied to the testing domain — the same architecture, orchestration challenges, and observability requirements apply.

## ความเชื่อมโยงกับ AI for Testing
คลื่นที่ 3 ของการนำ AI มาใช้ในการทดสอบซอฟต์แวร์ (2573+ ตาม [[ais-impact-on-software-testing-qa-evolution]]) อธิบาย "การทดสอบ end-to-end อัตโนมัติ" ที่ AI strategist กำหนดมาตรฐานคุณภาพขณะที่ agent ดำเนินวงจรการทดสอบทั้งหมด นี่คือ agentic AI ที่ถูกนำมาใช้ในโดเมนการทดสอบ — สถาปัตยกรรม ความท้าทาย orchestration และข้อกำหนด observability เดียวกันล้วนใช้ได้

---

## Testing Implications
Agentic systems introduce testing problems absent from traditional software:
- **Non-determinism** — the same input can produce different outputs
- **Compounding errors** — a mistake in step 2 corrupts all downstream steps
- **Silent failures** — the agent may appear to complete a task while having hallucinated a critical step
- **Scope of verification** — intermediate steps matter as much as the final output

See [[llm-evals]] for evaluation approaches and [[agent-observability]] for production monitoring.

## นัยสำคัญต่อการทดสอบ
ระบบ agentic สร้างปัญหาการทดสอบที่ไม่มีในซอฟต์แวร์ทั่วไป:
- **ความไม่แน่นอน** — input เดียวกันให้ output ที่ต่างกันได้
- **ข้อผิดพลาดสะสม** — ความผิดพลาดในขั้นที่ 2 ทำให้ขั้นตอนต่อๆ ไปผิดพลาดทั้งหมด
- **ความล้มเหลวแบบเงียบ** — agent อาจดูเหมือนทำงานเสร็จแต่จริงๆ hallucinate ขั้นตอนสำคัญ
- **ขอบเขตการตรวจสอบ** — ขั้นตอนตรงกลางสำคัญพอๆ กับ output สุดท้าย

ดู [[llm-evals]] และ [[agent-observability]]

---

## Open Questions
- How do you formally specify "correct" agent behavior for open-ended tasks?
- At what scale do eval suites become unmanageable to maintain?
- How do you test multi-agent systems where individual agent behavior is acceptable but emergent system behavior is not?

## คำถามที่ยังไม่มีคำตอบ
- จะกำหนดอย่างเป็นทางการได้อย่างไรว่าพฤติกรรม agent ที่ "ถูกต้อง" สำหรับงานปลายเปิดคืออะไร?
- เมื่อ scale ขึ้น eval suite จะจัดการไม่ได้ที่จุดไหน?
- จะทดสอบระบบ multi-agent ที่ agent แต่ละตัวทำงานได้ถูกต้องแต่พฤติกรรมของระบบโดยรวมไม่ถูกต้องได้อย่างไร?

---

## Non-Enterprise Example: LLM Wiki
The ingest → update → lint loop in [[karpathy-llm-wiki-pattern]] is a clean real-world example of a human-directed agentic workflow: the LLM takes a multi-step task, uses file tools, produces persistent artifacts, and operates at variable autonomy levels (collaborative to fully autonomous). The lint operation specifically resembles [[llm-evals]] applied to the LLM's own prior outputs.

## ตัวอย่างที่ไม่ใช่ Enterprise: LLM Wiki
วงจร ingest → update → lint ใน [[karpathy-llm-wiki-pattern]] คือตัวอย่างที่ชัดเจนในโลกจริงของ agentic workflow ที่มนุษย์กำกับทิศทาง: LLM รับงานหลายขั้นตอน ใช้เครื่องมือไฟล์ สร้างสิ่งประดิษฐ์ที่ยั่งยืน และทำงานในระดับ autonomy ที่ปรับได้ การดำเนินการ lint โดยเฉพาะคล้ายกับ [[llm-evals]] ที่ใช้กับ output ของ LLM เอง

---

## Agentic SDLC (ASDLC)

Traditional SDLC requires adaptation for agentic systems. The **Agentic Software Development Life Cycle** adds:
- Explicit specification of **prohibited behaviors** alongside desired behaviors
- Behavioral quality assurance methodologies (not input/output determinism)
- Versioning discipline across five artifact categories: prompts, tool manifests, policy configurations, memory schemas, and evaluation datasets
- Human oversight integration at appropriate autonomy levels
- Tracing as a first-class engineering concern from day one (not bolted on later)

Reference standard: ISO/IEC 5338:2023 ("AI system life cycle processes") — the first comprehensive framework emphasizing risk management throughout development and autonomous system behavior verification.

## Agentic SDLC (ASDLC)
SDLC แบบดั้งเดิมต้องปรับสำหรับระบบ agentic โดยเพิ่ม: การระบุพฤติกรรมต้องห้ามอย่างชัดเจน, การประกันคุณภาพเชิงพฤติกรรม, วินัยการ version artifact 5 ประเภท, การผสาน human oversight, และ tracing เป็น concern ด้านวิศวกรรมหลักตั้งแต่วันแรก

---

## Related / หน้าที่เกี่ยวข้อง
[[llm-evals]] · [[agent-observability]] · [[agentops]] · [[multi-agent-systems]] · [[agentic-rag]] · [[ai-tool-selection-rubric]] · [[llm-as-judge]] · [[ai-test-generation]] · [[self-healing-tests]] · [[karpathy-llm-wiki-pattern]]
[[one-year-of-agentic-ai-six-lessons]] (source / แหล่งที่มา)
[[ais-impact-on-software-testing-qa-evolution]] (source / แหล่งที่มา — Wave 3 connection)
[[prompts-to-production-agentic-playbook]] (source / แหล่งที่มา — ASDLC, capability matrix, orchestration patterns)
[[google-agents-companion]] (source / แหล่งที่มา — 3-component model, enterprise agent types, contractor model)
