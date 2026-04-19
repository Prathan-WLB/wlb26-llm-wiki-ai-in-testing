---
title: Hallucination
type: concept
axis: testing-for-ai
tags: [hallucination, evals, reliability, testing-for-ai, llm]
related: [[llm-evals]], [[llm-as-judge]], [[agent-observability]], [[automation-bias]], [[explainability]]
created: 2026-04-10
updated: 2026-04-19
---

# Hallucination

> **Stub** — core definition is complete; detection tooling, faithfulness scoring frameworks (RAGAS), and the irreducibility debate need expansion. See open questions below.

## Definition
When an LLM generates factually incorrect or unsupported claims — stated with apparent confidence. The model "hallucinates" content that doesn't exist in its training data or retrieved context.

## ความหมาย
เมื่อ LLM สร้าง claim ที่ผิดจากข้อเท็จจริงหรือไม่มีหลักฐานรองรับ — โดยแสดงออกมาอย่างมั่นใจ model "hallucinate" เนื้อหาที่ไม่มีอยู่ใน training data หรือ context ที่ดึงมา

---

## Why It Matters
Hallucination is one of the primary reliability failures in LLM-based systems. In agentic workflows, hallucinated intermediate steps propagate downstream and corrupt final outputs. In high-stakes domains (legal, medical, financial), a single hallucination can invalidate an entire analysis.

## ความสำคัญ
Hallucination เป็นหนึ่งในความล้มเหลวด้านความน่าเชื่อถือหลักของระบบ LLM ใน agentic workflow ขั้นตอนตรงกลางที่ hallucinate จะแพร่กระจายและทำให้ output สุดท้ายผิดพลาด ในโดเมนที่มีความเสี่ยงสูง (กฎหมาย การแพทย์ การเงิน) hallucination เพียงครั้งเดียวสามารถทำให้การวิเคราะห์ทั้งหมดไม่น่าเชื่อถือ

---

## Variants
- **Closed-domain hallucination** — the model contradicts information in the provided context (the retrieved document says X, the model says not-X)
- **Open-domain hallucination** — the model invents facts not grounded in any source
- **Partial hallucination** — the model gets most of an answer right but fabricates a specific detail (a number, a citation, a name)

## ประเภท
- **Closed-domain hallucination** — model ขัดแย้งกับข้อมูลใน context ที่ให้มา
- **Open-domain hallucination** — model สร้างข้อเท็จจริงที่ไม่ได้มาจากแหล่งใด
- **Partial hallucination** — model ตอบถูกส่วนใหญ่แต่ประดิษฐ์รายละเอียดเฉพาะ (ตัวเลข การอ้างอิง ชื่อ)

---

## How It's Measured
The **hallucination rate** eval metric tracks frequency of incorrect or unsupported claims. Measurement approaches:
- Fact-checking against a known ground truth set
- [[llm-as-judge]] prompted to identify unsupported claims
- RAG-specific: checking whether output claims are grounded in retrieved documents (faithfulness score)

## วิธีวัด
**Hallucination rate** วัดความถี่ของ claim ที่ผิดหรือไม่มีหลักฐาน วิธีการวัด:
- ตรวจสอบข้อเท็จจริงเทียบกับ ground truth set ที่รู้จัก
- [[llm-as-judge]] ที่ prompt ให้ระบุ claim ที่ไม่มีหลักฐานรองรับ
- เฉพาะ RAG: ตรวจสอบว่า claim ใน output มีพื้นฐานจากเอกสารที่ดึงมาหรือไม่ (faithfulness score)

---

## Current State
Active research area. RAG reduces hallucination by grounding the model in retrieved documents but doesn't eliminate it — models can still misread or ignore retrieved content. Newer model generations (2024–2025) show improvement but the problem persists, especially in complex multi-step reasoning.

## สถานะปัจจุบัน
เป็นพื้นที่วิจัยที่ยังคงดำเนินอยู่ RAG ลด hallucination โดยยึด model ไว้กับเอกสารที่ดึงมา แต่ไม่ได้กำจัดทั้งหมด model รุ่นใหม่ (2567–2568) แสดงการปรับปรุง แต่ปัญหายังคงอยู่ โดยเฉพาะสำหรับการใช้เหตุผลหลายขั้นตอน

---

## Open Questions / คำถามที่ยังไม่มีคำตอบ
- Is hallucination a fundamental property of transformer-based LLMs, or an engineering problem that will be solved? / Hallucination เป็นคุณสมบัติพื้นฐานของ LLM หรือปัญหาทางวิศวกรรมที่แก้ได้?
- How do you detect hallucinations in domains where no ground truth is easily accessible? / จะตรวจจับ hallucination ในโดเมนที่ไม่มี ground truth ที่เข้าถึงได้ง่ายได้อย่างไร?
- How does hallucination rate change as agents chain multiple LLM calls? / Hallucination rate เปลี่ยนอย่างไรเมื่อ agent เชื่อม LLM call หลายครั้ง?

## Related / หน้าที่เกี่ยวข้อง
[[llm-evals]] · [[llm-as-judge]] · [[agent-observability]] · [[automation-bias]] · [[explainability]]
