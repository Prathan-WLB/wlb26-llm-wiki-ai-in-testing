---
title: LLM-as-Judge
type: concept
axis: testing-for-ai
tags: [evals, llm-as-judge, evaluation, testing-for-ai, bias]
related: [[llm-evals]], [[hallucination]], [[agentic-ai]]
created: 2026-04-10
updated: 2026-04-10
---

# LLM-as-Judge

## Definition
Using a large language model to evaluate the outputs of another LLM or agent. The judge LLM scores outputs against gold standards, rubrics, or human preferences — replacing or augmenting human reviewers.

## ความหมาย
การใช้ LLM ขนาดใหญ่ประเมิน output ของ LLM อีกตัว (หรือ agent) โดย LLM ที่ทำหน้าที่ judge จะให้คะแนน output เทียบกับ gold standard, rubric, หรือ human preference — ทดแทนหรือเสริมผู้ประเมินที่เป็นมนุษย์

---

## Why It Matters
Human evaluation is the gold standard for LLM quality but doesn't scale. LLM-as-judge enables evaluation at scale for subjective qualities — clarity, helpfulness, reasoning soundness — that deterministic metrics like F1 cannot capture.

## ความสำคัญ
การประเมินโดยมนุษย์คือมาตรฐานทองแต่ไม่สามารถ scale ได้ LLM-as-judge ทำให้ประเมินในปริมาณมากได้สำหรับคุณสมบัติเชิงอัตวิสัย — ความชัดเจน ความเป็นประโยชน์ ความสมเหตุสมผล — ที่ metric แบบ deterministic ไม่สามารถวัดได้

---

## How It Works
1. Define a rubric or evaluation criteria (e.g. "Is the answer factually correct?", "Is the reasoning sound?")
2. Prompt the judge LLM with the input, the agent's output, optionally a reference answer, and the rubric
3. The judge returns a score, rating, or pass/fail with reasoning
4. Aggregate across many examples to compute eval metrics

Common patterns:
- **Single-answer grading** — rate one output against a rubric
- **Pairwise comparison** — compare two outputs and pick the better one (used in RLHF)
- **Reference-based** — compare against a gold standard answer

## กลไกการทำงาน
1. กำหนด rubric หรือเกณฑ์การประเมิน (เช่น "คำตอบถูกต้องตามข้อเท็จจริงหรือไม่?")
2. ส่ง prompt ให้ judge LLM พร้อม input, output ของ agent, คำตอบอ้างอิง (ถ้ามี), และ rubric
3. judge ส่งคืนคะแนนหรือ pass/fail พร้อมเหตุผล
4. รวบรวมผลลัพธ์จากตัวอย่างจำนวนมากเพื่อคำนวณ metric

รูปแบบที่พบบ่อย:
- **Single-answer grading** — ให้คะแนน output หนึ่งชิ้นเทียบกับ rubric
- **Pairwise comparison** — เปรียบเทียบ output สอง output และเลือกที่ดีกว่า (ใช้ใน RLHF)
- **Reference-based** — เปรียบเทียบกับคำตอบ gold standard

---

## Known Biases and Limitations
- **Self-preference bias** — a model tends to rate outputs similar to its own style higher
- **Verbosity bias** — longer, more detailed answers are often rated higher even if less correct
- **Position bias** — in pairwise comparisons, the first or second option may be systematically preferred
- **Sycophancy** — if the judge is the same model being evaluated, it may be overconfident in its own outputs
- **Prompt sensitivity** — judge scores can shift significantly with minor prompt changes

These biases mean LLM-as-judge should be validated against human ratings before being trusted as a primary eval signal.

## Bias และข้อจำกัดที่รู้จัก
- **Self-preference bias** — model มักให้คะแนน output ที่มีรูปแบบคล้ายตัวเองสูงกว่า
- **Verbosity bias** — คำตอบที่ยาวและละเอียดมักได้คะแนนสูงกว่าแม้จะไม่ถูกต้องกว่า
- **Position bias** — ในการเปรียบเทียบแบบ pairwise ตัวเลือกแรกหรือที่สองอาจถูกเลือกอย่างเป็นระบบ
- **Sycophancy** — ถ้า judge เป็น model เดียวกับที่ถูกประเมิน อาจมั่นใจใน output ของตัวเองมากเกินไป
- **Prompt sensitivity** — คะแนนอาจเปลี่ยนมีนัยสำคัญเมื่อ prompt เปลี่ยนเล็กน้อย

---

## Current State
Widely adopted (2025). Used by OpenAI, Anthropic, Google for RLHF and model assessment. Frameworks: DeepEval, Ragas. Research into reducing position and verbosity bias is active.

## สถานะปัจจุบัน
ถูกนำไปใช้อย่างแพร่หลาย (ปี 2568) ใช้โดย OpenAI, Anthropic, Google สำหรับ RLHF และการประเมิน model งานวิจัยเพื่อลด position bias และ verbosity bias ยังดำเนินอยู่

---

## Open Questions / คำถามที่ยังไม่มีคำตอบ
- Can LLM judges reliably detect hallucinations in domains where they themselves might hallucinate? / LLM judge สามารถตรวจจับ hallucination ในโดเมนที่ตัวเองก็อาจ hallucinate ได้หรือไม่?
- How do you validate a judge's own reliability at scale? / จะตรวจสอบความน่าเชื่อถือของ judge เองในปริมาณมากได้อย่างไร?

---

## Related / หน้าที่เกี่ยวข้อง
[[llm-evals]] · [[hallucination]] · [[agentic-ai]]
[[one-year-of-agentic-ai-six-lessons]] (source / แหล่งที่มา)
