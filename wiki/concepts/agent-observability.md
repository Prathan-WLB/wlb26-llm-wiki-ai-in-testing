---
title: Agent Observability
type: concept
axis: testing-for-ai
tags: [observability, monitoring, agentic-ai, testing-for-ai, production]
related: [[agentic-ai]], [[llm-evals]], [[hallucination]], [[prompts-to-production-agentic-playbook]]
created: 2026-04-10
updated: 2026-04-11
---

# Agent Observability

## Definition
The ability to inspect, trace, and understand the internal behavior of AI agents at runtime — not just their final outputs. Analogous to distributed systems observability (logs, traces, metrics) but applied to AI agent workflows.

## ความหมาย
ความสามารถในการตรวจสอบ ติดตาม และทำความเข้าใจพฤติกรรมภายในของ AI agent ขณะทำงานจริง — ไม่ใช่แค่ output สุดท้าย เทียบได้กับ observability ของระบบ distributed (log, trace, metric) แต่ถูกนำมาใช้กับ AI agent workflow

---

## Why It Matters
When agents fail, outcome-only monitoring makes root cause analysis nearly impossible. A wrong final output could stem from a retrieval failure, a prompt injection, a misclassified input, or an error in step 7 of a 12-step workflow. Without step-level visibility, debugging is guesswork.

At scale (hundreds of agents), this compounds. The McKinsey example: an alternative dispute resolution provider saw a sudden accuracy drop and traced it to lower-quality upstream data from a specific user segment — only possible because they had built observability into every step.

## ความสำคัญ
เมื่อ agent ล้มเหลว การดูแค่ผลลัพธ์สุดท้ายทำให้หา root cause แทบไม่ได้ output ที่ผิดพลาดอาจเกิดจาก retrieval ล้มเหลว, prompt injection, input ที่จัดประเภทผิด, หรือข้อผิดพลาดในขั้นที่ 7 ของ workflow 12 ขั้น ถ้าไม่มีการมองเห็นระดับ step การ debug ก็เป็นแค่การเดา

---

## Key Components
- **Trace logging** — record every tool call, retrieval query, intermediate output, and decision branch with timestamps
- **Step-level metrics** — evaluate each workflow step independently, not just the final result
- **Input/output capture** — store actual inputs and outputs at each step for replay and debugging
- **Alerting** — detect anomalies (accuracy drops, latency spikes, escalation rate increases) in real time
- **Replay** — ability to re-run a specific trace to reproduce and debug a failure

## องค์ประกอบหลัก
- **Trace logging** — บันทึก tool call ทุกครั้ง, retrieval query, intermediate output, และ decision branch พร้อม timestamp
- **Step-level metrics** — ประเมินแต่ละขั้นตอนใน workflow แยกกัน ไม่ใช่แค่ผลลัพธ์สุดท้าย
- **Input/output capture** — เก็บ input และ output จริงในแต่ละขั้นตอนสำหรับ replay และ debug
- **Alerting** — ตรวจจับความผิดปกติแบบ real-time
- **Replay** — สามารถรัน trace เฉพาะซ้ำอีกครั้งเพื่อ reproduce และ debug

---

## How It Differs from Traditional Monitoring
Traditional monitoring asks: did the function return? Did it throw? How long did it take?

Agent observability additionally asks: was the reasoning sound? Did retrieval surface the right documents? Did the agent hallucinate in an intermediate step that then propagated downstream? This requires semantic monitoring embedded in the observability pipeline — not just offline eval suites.

## ความแตกต่างจาก Traditional Monitoring
Traditional monitoring ตรวจสอบ: function return ค่าหรือไม่? มี error throw หรือไม่? ใช้เวลานานเท่าไหร่?

Agent observability ยังต้องตรวจสอบเพิ่มเติม: การใช้เหตุผลสมเหตุสมผลหรือไม่? Retrieval ดึงเอกสารที่ถูกต้องมาหรือไม่? Agent hallucinate ในขั้นตอนตรงกลางหรือไม่? สิ่งเหล่านี้ต้องการการติดตามเชิงความหมาย ไม่ใช่แค่การติดตามเชิงปฏิบัติ

---

## Tooling (2025)
- **LangSmith** (LangChain) — tracing and debugging for LangGraph/LangChain agents
- **Arize AI, Weights & Biases** — production ML monitoring with LLM-specific features
- **Helicone, Braintrust** — LLM observability focused on cost, latency, and quality
- Open-source: Phoenix (Arize), OpenTelemetry integrations

## เครื่องมือ (ปี 2568)
- **LangSmith** — tracing และ debugging สำหรับ LangGraph/LangChain agent
- **Arize AI, Weights & Biases** — production ML monitoring พร้อม feature สำหรับ LLM
- **Helicone, Braintrust** — LLM observability ด้านต้นทุน latency และคุณภาพ
- Open-source: Phoenix (Arize), OpenTelemetry integrations

---

## Current State
Rapidly maturing. Most production agentic deployments include some trace logging. Full semantic monitoring (embedding evals in the production trace) is less common — more expensive and harder to set up.

## สถานะปัจจุบัน
กำลังเติบโตอย่างรวดเร็ว การ deploy agentic ใน production ส่วนใหญ่มี trace logging บ้างแล้ว การติดตามเชิงความหมายเต็มรูปแบบยังไม่เป็นที่แพร่หลาย — มีต้นทุนสูงกว่าและตั้งค่ายากกว่า

---

## Tracing as Planning Requirement

[[prompts-to-production-agentic-playbook]] elevates tracing to a mandatory planning question (Question 7 in the Iterative Assessment Framework), not an afterthought. The reasoning: agents show **63% coefficient of variation in execution paths for identical inputs**. Without a baseline trace captured early, you have nothing to regression-test against when behavior drifts.

Planning checklist for tracing:
- Choose framework: LangSmith or OpenTelemetry
- Instrument from day one — retrofitting is expensive
- Define retention policy
- Capture a behavioral baseline before any production changes
- Use traces for **behavioral regression testing** (did the agent's execution paths change after a prompt update?)

LangSmith visualizations also serve a secondary purpose: they surface that LLM calls introduce significant latency, reinforcing the Capability Matrix principle — don't make deterministic components agentic.

## Tracing ในฐานะข้อกำหนดการวางแผน
บทความ Goswami ยก tracing เป็นคำถามวางแผนบังคับ (ข้อ 7 ใน Iterative Assessment Framework) ไม่ใช่สิ่งที่เพิ่มภายหลัง เพราะ agent แสดง **ความแปรปรวน 63% ใน execution path** สำหรับ input เดียวกัน โดยไม่มี baseline trace คุณไม่มีอะไรทดสอบ regression เมื่อพฤติกรรมเบี่ยงเบน

---

## Open Questions / คำถามที่ยังไม่มีคำตอบ
- How do you set meaningful anomaly detection thresholds for non-deterministic agents? / จะตั้งเกณฑ์การตรวจจับความผิดปกติที่มีความหมายสำหรับ agent ที่ไม่แน่นอนได้อย่างไร?
- What's the right granularity — logging every token is too expensive, logging only final outputs is too coarse? / ระดับของรายละเอียดที่เหมาะสมคืออะไร?
- How do you maintain observability as agentic systems become more autonomous? / จะรักษา observability ไว้ได้อย่างไรเมื่อระบบ agentic มีอัตโนมัติมากขึ้น?

---

## Related / หน้าที่เกี่ยวข้อง
[[agentic-ai]] · [[llm-evals]] · [[hallucination]]
[[one-year-of-agentic-ai-six-lessons]] (source / แหล่งที่มา — lesson 4)
[[prompts-to-production-agentic-playbook]] (source / แหล่งที่มา — tracing as planning requirement, 63% path variation stat)
