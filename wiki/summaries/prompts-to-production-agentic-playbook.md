---
title: "From Prompts to Production: A Playbook for Agentic Development"
type: article
axis: both
tags: [agentic-ai, asdlc, orchestration, capability-matrix, versioning, mcp, react-agent, human-in-the-loop, observability]
related: [[agentic-ai]], [[agent-observability]], [[llm-evals]], [[ai-tool-selection-rubric]]
created: 2026-04-11
updated: 2026-04-11
---

# From Prompts to Production: A Playbook for Agentic Development
# จาก Prompt สู่ Production: คู่มือการพัฒนา Agentic

## Citation / แหล่งอ้างอิง

Abhishek Goswami. InfoQ. February 11, 2026.
URL: https://www.infoq.com/articles/prompts-to-production-playbook-for-agentic-development/
Reviewer: Srini Penchikala

---

## Core Claim / ข้อสรุปหลัก

Taking agentic AI from prototype to production requires a disciplined playbook: systematic decomposition of workflows into deterministic vs. agentic components, pattern-matched orchestration, versioning of all agentic artifacts, and behavioral (not input/output) quality assurance. The biggest mistake teams make is making everything agentic.

การนำ agentic AI จาก prototype ไปสู่ production ต้องการ playbook ที่เป็นระบบ: การแยกแยะ workflow เป็น component ที่ deterministic และ agentic อย่างเป็นระบบ, การเลือก pattern orchestration ที่เหมาะสม, การ version artifact ทั้งหมด, และการประกันคุณภาพเชิงพฤติกรรม (ไม่ใช่แค่ input/output) ข้อผิดพลาดที่ใหญ่ที่สุดคือการทำให้ทุกอย่างเป็น agentic

---

## Key Contributions / ผลงานหลัก

- Proposes the **Agentic SDLC (ASDLC)** — a lifecycle adaptation emphasizing not just what agents do but what they are prohibited from doing
- Introduces a **Capability Matrix** methodology for decomposing workflows into deterministic vs. agentic components
- Provides a detailed **Iterative Assessment Framework** (7 questions) for planning agentic implementations
- Catalogs orchestration patterns (ReAct, Supervisor, Hierarchical, Human-in-the-Loop) with real-world evidence
- Identifies **5 artifact categories** requiring versioning: prompts, tool manifests, policy configurations, memory schemas, evaluation datasets
- Benchmarks methodology over model size: agentic iterative looping with GPT-3.5 achieves **95.1% accuracy** vs. GPT-4 zero-shot at **67%**

---

## The Prototype-to-Production Gap / ช่องว่างระหว่าง Prototype และ Production

Agentic systems exhibit **nondeterministic behavior**, emergent capabilities, and autonomous decision-making. Prototypes don't represent real-world environments because agents behave inconsistently across executions with identical inputs. Research shows "up to 63% coefficient of variation in execution paths for identical inputs."

This is why traditional SDLC is insufficient — the article proposes the **Agentic SDLC (ASDLC)** which adds:
- Explicit prohibited behavior specification alongside desired behaviors
- Behavioral quality assurance methodologies
- Versioning discipline across agentic artifacts
- Human oversight integration at appropriate autonomy levels

ระบบ agentic แสดงพฤติกรรมที่ไม่แน่นอน ความสามารถที่เกิดขึ้นเอง และการตัดสินใจอัตโนมัติ การวิจัยแสดงว่ามี "ความแปรปรวนสูงถึง 63% ใน execution path สำหรับ input เดียวกัน"

---

## The Capability Matrix: Deterministic vs. Agentic / Capability Matrix: Deterministic กับ Agentic

### The Primary Anti-Pattern

**Making everything agentic** is the #1 mistake. If code can make clear, unambiguous decisions based on fixed rules, adding LLM reasoning introduces complexity and performance overhead without benefit. LLM calls should be reserved for genuine nondeterministic reasoning tasks — this also naturally reduces inference costs.

**การทำให้ทุกอย่างเป็น agentic** คือข้อผิดพลาดหลัก ถ้าโค้ดสามารถตัดสินใจที่ชัดเจนและไม่มีความคลุมเครือตามกฎตายตัวได้ การเพิ่มการใช้เหตุผลของ LLM แค่เพิ่มความซับซ้อนโดยไม่มีประโยชน์

### Customer Support Workflow Breakdown

A concrete decomposition example across 7 steps:

| Step | Deterministic | Agentic |
|------|--------------|---------|
| Ticket Reception | ID generation, channel detection, customer lookup, SLA timer | Customer intent analysis, issue identification |
| Classification & Routing | Queue assignment (based on agentic output) | Issue category, priority assessment, complexity scoring |
| Knowledge Base Search | DB lookup, caching, retrieval execution | Query generation, relevance assessment, solution synthesis |
| Solution Initiation | DB lookups, command execution | Decision on which solution to apply |
| Response Generation | Template application, placeholder resolution, routing | Personalization, verbiage choice based on urgency |
| Response Delivery | Channel send, logging, metrics | Effectiveness assessment, follow-up recommendation |
| Closure | Notifications, SLA tracking | Closure recommendations, summary generation |

**Key insight**: Understanding customer intent (unstructured text) and dynamic reasoning are agentic. Actions based on known system state (SLA values, ticket IDs, routing rules) are always deterministic.

---

## Orchestration Patterns / Pattern การ Orchestrate

### ReAct Agent (Reason → Act → Observe loop)

8-step loop until breaking condition:
1. Reason — LLM decides next action
2. Act — execute chosen tool
3. Observe — analyze results
4. Repeat until: explicit completion signal, confidence threshold reached, or error requiring human intervention

Best for: iterative investigation workflows (e.g., a database debugging agent that executes queries, analyzes performance, and examines indexes until finding a root cause).

### Supervisor Agent Pattern

Centralized supervisor assigns subtasks to specialized worker agents, deciding which to invoke next or when the workflow is complete. Anthropic's Multi-Agent Research System is a cited production example.

### Hierarchical Agent Pattern

When supervisor-to-worker ratios become unwieldy, add hierarchy: worker agents → team supervisors → master supervisor. Example: e-commerce fulfillment with a master agent coordinating regional supervisors (North America, Europe, Asia), each managing inventory/picking/packing/shipping agents.

### Human-in-the-Loop Pattern

Decision points requiring human oversight are embedded in the workflow. AI provides analysis; human provides the decision. Example: loan approval workflows.

### Autonomy Level Framework (4 levels)

| Level | Description |
|-------|-------------|
| Human-in-the-Loop | Direct human intervention at decision points |
| Human-on-the-Loop | Human maintains meaningful real-time control |
| Human-above-the-Loop | Strategic governance only |
| Human-behind-the-Loop | Post-operational analysis only |

### Additional Patterns (reference)

| Pattern | Use Case |
|---------|----------|
| Sequential Orchestration | Clear step-by-step dependencies; JPMorgan COiN processes 12,000 contracts in seconds |
| Concurrent Orchestration | Independent parallel tasks; Google Cloud Agent Assist: 28% more conversations, 15% faster |
| Hierarchical Orchestration | Complex task decomposition; AgentOrchestra achieves 95.3% on complex benchmarks |
| Event-Driven | Scalable distributed systems |
| Blackboard | Knowledge-intensive tasks |

---

## Iterative Assessment Framework: 7 Planning Questions

Before building, iterate through these questions until each reaches full definition:

1. **Well-Defined Workflows** — What is the application scope and boundary? What parts are agentic vs. not?
2. **Nondeterministic Decision Mapping** — Where does LLM reasoning add value vs. deterministic logic?
3. **Capability Matrix Preparation** — Map deterministic vs. agentic components for each workflow to optimize cost and reliability
4. **Tool Requirements** — What tools does the agent need? What are the authorization requirements? Define MCP schemas
5. **Input/Output Contracts** — Define clear interfaces enabling testing; validate with sample data
6. **Success Criteria** — Behavioral consistency, failure handling, escalation triggers — not just accuracy and latency
7. **Tracing Approach** — Choose framework (LangSmith / OpenTelemetry); instrument; capture behavioral baseline

---

## Versioning Requirements / ข้อกำหนดการ Version

Agentic systems have more failure points than conventional backends. All five artifact categories require version control, rollback capability, and Infrastructure-as-Code treatment:

1. **Prompt Templates / System Prompts** — agents show 63% coefficient of variation in execution paths; versioning enables rollback when behavior drifts
2. **Tool Manifests** — function definitions, parameters, descriptions
3. **Policy Configurations** — safety constraints, operational bounds, decision guidelines
4. **Memory Schemas** — agent state data structure definitions
5. **Evaluation Datasets** — test data and behavioral baselines for regression testing

Modern tooling: Git-based version control with performance monitoring (PortKey); runtime prompt control for production agents (LaunchDarkly).

---

## Quality Assurance for Agentic Systems / การประกันคุณภาพ

Agentic QA requires **behavioral approaches**, not input/output determinism checking. The nondeterministic nature means the same input can follow 63% different execution paths — traditional pass/fail testing misses this.

Key requirements:
- Behavioral consistency testing (does the agent behave within expected bounds across many runs?)
- Execution path auditing via traces
- Regression testing against versioned eval datasets
- Specialized tooling integrating with standard CI/CD

---

## Model Context Protocol (MCP) / Model Context Protocol

MCP provides a **vendor-neutral standard** for agent-tool integration (JSON-RPC 2.0). Adopted by OpenAI, Google DeepMind, and Microsoft. Reduces integration development time and improves maintainability. MCP schema definition is part of the iterative assessment framework (Question 4: Tool Requirements).

MCP ให้มาตรฐานที่เป็นกลางสำหรับการ integrate agent กับเครื่องมือ ลดเวลาพัฒนา integration และปรับปรุงความสามารถในการบำรุงรักษา

---

## Key Numbers / ตัวเลขสำคัญ

| Claim | Figure | Source |
|-------|--------|--------|
| GPT-3.5 zero-shot on coding benchmark | 48% | Article |
| GPT-4 zero-shot on coding benchmark | 67% | Article |
| GPT-3.5 with agentic iterative looping | **95.1%** | Article (ReAct paper) |
| Execution path variation for identical inputs | 63% coefficient of variation | Article |
| AgentOrchestra hierarchical accuracy | 95.3% | Zhang et al. via article |
| 3-tier hierarchical architecture improvement | 32% absolute task success | Liu et al. via article |
| Multi-agent token consumption vs. single | 15× more on average | Anthropic research via article |
| JPMorgan COiN contracts processed | 12,000 in seconds | Article |
| Legal hours saved by COiN | 360,000 annually | Article |
| Google Agent Assist conversation volume | +28% | Article |
| Google Agent Assist response time | −15% | Article |

---

## My Take / ความเห็นส่วนตัว

The **Capability Matrix** is the most actionable framework in this article — it operationalizes the intuition that "not everything needs to be agentic" into a systematic decomposition exercise. The customer support example is concrete enough to adapt directly.

The 95.1% vs. 67% benchmark (GPT-3.5 iterative vs. GPT-4 zero-shot) is the article's most provocative claim. It reframes the question from "which model?" to "which methodology?" — directly relevant to how teams should invest in agent architecture vs. model upgrades.

The ASDLC framing is useful for conversations with engineering leadership: it gives "we need to test agents differently" a named framework and ISO standard backing (ISO/IEC 5338:2023).

The 5-artifact versioning taxonomy plugs a real gap — most teams version prompts informally if at all. Policy configurations and evaluation datasets as first-class versioned artifacts is the right direction.

**Capability Matrix** คือกรอบที่นำไปปฏิบัติได้มากที่สุดในบทความนี้ ตัวเลข 95.1% vs. 67% ตั้งคำถามใหม่: จาก "ควรใช้ model ไหน?" เป็น "ควรใช้ methodology ไหน?" ซึ่งตรงประเด็นสำหรับการตัดสินใจลงทุน

---

## Related / หน้าที่เกี่ยวข้อง
[[agentic-ai]] · [[agent-observability]] · [[llm-evals]] · [[ai-tool-selection-rubric]]
