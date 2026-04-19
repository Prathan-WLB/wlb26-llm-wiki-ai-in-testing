---
title: LLM Evals
type: concept
axis: testing-for-ai
tags: [evals, evaluation, benchmarking, testing-for-ai, llm, metrics]
related: [[agentic-ai]], [[llm-as-judge]], [[agent-observability]], [[hallucination]], [[prompts-to-production-agentic-playbook]], [[rlhf]], [[automation-bias]], [[explainability]], [[interactive-machine-learning]]
created: 2026-04-10
updated: 2026-04-19
---

# LLM Evals

## Definition
Evaluations ("evals") are structured tests used to assess the performance of LLMs and AI agents. They are the primary mechanism for testing AI systems — the equivalent of unit tests and integration tests for traditional software, adapted for probabilistic, open-ended outputs.

## ความหมาย
การประเมินผล (Evals) คือการทดสอบที่มีโครงสร้างเพื่อวัดประสิทธิภาพของ LLM และ AI agent เป็นกลไกหลักในการทดสอบระบบ AI — เทียบได้กับ unit test และ integration test ในซอฟต์แวร์ทั่วไป แต่ปรับมาสำหรับ output ที่เป็นความน่าจะเป็นและมีความหลากหลาย

---

## Why It Matters
LLM outputs are non-deterministic and hard to specify in advance. Unlike traditional software where correctness is binary, LLM correctness exists on a spectrum and depends on context. Evals bridge this gap: they operationalize "good enough" into measurable metrics, enabling systematic improvement and regression detection.

The McKinsey framing is apt: developing effective agents requires "harnessing individual expertise to create evaluations and codifying best practices with sufficient granularity." Evals are both the training manual and the performance test.

## ความสำคัญ
Output ของ LLM ไม่แน่นอนและมักระบุล่วงหน้าได้ยาก ต่างจากซอฟต์แวร์ทั่วไปที่ความถูกต้องเป็น binary ความถูกต้องของ LLM มีระดับและขึ้นอยู่กับบริบท Evals เชื่อม gap นี้: ทำให้ "ดีพอ" กลายเป็น metric ที่วัดได้ เปิดให้ปรับปรุงอย่างเป็นระบบและตรวจจับ regression ได้

---

## Eval Taxonomy (8 Types)

### 1. Task Success Rate (end-to-end)
Percentage of workflows completed correctly without escalation or human intervention. The most direct measure of real-world utility. Use as the primary metric for agentic workflows.

### 2. F1 Score / Precision and Recall
Balances false positives and false negatives. Best for classification, extraction, and decision tasks with a clear binary ground truth. Not suited to open-ended generative tasks.

### 3. Retrieval Accuracy
Percentage of correct documents, facts, or evidence retrieved relative to a ground truth set. Critical for RAG workflows. Measures the retrieval step independently from generation.

### 4. Semantic Similarity
Embedding-based cosine similarity between generated output and a reference output. Captures meaning alignment beyond exact string matching.

### 5. LLM-as-Judge
Using an LLM to evaluate outputs against gold standards or human preferences. Scales well for subjective judgments. Has known biases — see [[llm-as-judge]].

### 6. Bias Detection (via confusion matrices)
Measures systematic differences in outcomes across user groups. Required for high-stakes or regulated applications.

### 7. Hallucination Rate
Frequency of factually incorrect or unsupported claims. Critical for any workflow where the agent presents facts or makes recommendations. See [[hallucination]].

### 8. Calibration Error (confidence vs. accuracy)
Whether the agent's confidence scores align with actual correctness. Important for risk-sensitive workflows.

## อนุกรมวิธานของ Eval (8 ประเภท)

### 1. Task Success Rate (end-to-end)
อัตราส่วน workflow ที่เสร็จสมบูรณ์อย่างถูกต้องโดยไม่ต้องมี human intervention วัด utility จริงได้ตรงที่สุด ใช้เป็น metric หลักสำหรับ agentic workflow

### 2. F1 Score / Precision และ Recall
สมดุลระหว่าง false positive และ false negative เหมาะสำหรับงาน classification และ extraction ที่มี ground truth ชัดเจน

### 3. Retrieval Accuracy
อัตราส่วนเอกสารหรือข้อเท็จจริงที่ดึงมาถูกต้องเทียบกับ ground truth สำคัญมากสำหรับ RAG workflow

### 4. Semantic Similarity
ค่า cosine similarity แบบ embedding จับความหมายที่สอดคล้องกันเกินกว่าการ match คำตรงๆ

### 5. LLM-as-Judge
ใช้ LLM ประเมิน output เทียบกับ gold standard หรือ human preference scale ได้ดีสำหรับการตัดสินเชิงอัตวิสัย ดู [[llm-as-judge]]

### 6. Bias Detection (ผ่าน confusion matrix)
วัดความแตกต่างอย่างเป็นระบบในผลลัพธ์ระหว่างกลุ่มผู้ใช้ จำเป็นสำหรับแอปพลิเคชันที่มีความเสี่ยงสูง

### 7. Hallucination Rate
ความถี่ของ claim ที่ผิดจากข้อเท็จจริงหรือไม่มีหลักฐาน ดู [[hallucination]]

### 8. Calibration Error (ความมั่นใจ vs. ความแม่นยำ)
วัดว่า confidence score ของ agent สอดคล้องกับความถูกต้องจริงหรือไม่

---

## How Evals Are Built
1. **Identify what separates top performers** — what does great look like for this specific task?
2. **Codify as labeled examples** — write desired (and undesired) outputs for given inputs; can number in the thousands
3. **Run the agent against the eval set** — compute metrics
4. **Refine and rerun** — identify logic gaps, adjust prompts, retest

The "launch and leave" anti-pattern is a common failure mode. Evals must run continuously, especially as the underlying model or retrieval data changes.

## วิธีสร้าง Eval
1. **ระบุว่าอะไรทำให้ผู้ทำงานได้ดีต่างจากคนทั่วไป** — สำหรับงานนั้นๆ ผลลัพธ์ที่ยอดเยี่ยมหน้าตาเป็นอย่างไร?
2. **Codify เป็นตัวอย่างที่มี label** — อาจมีหลายพันตัวอย่างสำหรับ agent ที่ซับซ้อน
3. **รัน agent กับ eval set** — คำนวณ metric
4. **ปรับแต่งและรันใหม่** — ระบุช่องว่างทางตรรกะ ปรับ prompt ทดสอบซ้ำ

anti-pattern "launch แล้วทิ้ง" เป็นสาเหตุความล้มเหลวที่พบบ่อย

---

## Practical Challenges
- **Ground truth is expensive to create** — labeling thousands of examples requires domain experts
- **Distribution shift** — a passing eval suite can become stale as real-world inputs drift
- **Eval gaming** — optimizing for eval metrics can diverge from optimizing for real user value
- **Multi-step agents** — intermediate steps matter as much as the final output

## ความท้าทายในทางปฏิบัติ
- **Ground truth สร้างได้แพง** — การ label ตัวอย่างหลายพันรายการต้องใช้ผู้เชี่ยวชาญ
- **Distribution shift** — eval suite อาจล้าสมัยเมื่อ input จากโลกจริงเปลี่ยนไป
- **Eval gaming** — การ optimize metric อาจแยกออกจากคุณค่าจริงสำหรับผู้ใช้
- **Agent หลายขั้นตอน** — ขั้นตอนตรงกลางสำคัญพอๆ กับ output สุดท้าย

---

## Methodology Beats Model Size

[[prompts-to-production-agentic-playbook]] provides a striking benchmark: GPT-3.5 zero-shot achieves **48% accuracy** on coding benchmarks; GPT-4 zero-shot achieves **67%**. But GPT-3.5 with agentic iterative looping (ReAct) achieves **95.1%**. The eval and orchestration methodology contributes more to outcome quality than model selection alone. This reframes investment decisions: before upgrading to a larger model, ask whether the agentic methodology is optimized.

## Eval Datasets as Versioned Artifacts

Goswami's ASDLC framework treats **evaluation datasets** as a fifth versioned artifact category alongside prompts, tool manifests, policy configurations, and memory schemas. The reasoning: agents show 63% coefficient of variation in execution paths. Without versioned eval datasets, you cannot perform behavioral regression testing — you have no baseline to compare against after a prompt update or model swap.

Practical implication: eval datasets need the same Git-based discipline as production code. Changes to the eval set itself must be logged and justified, or you lose the ability to detect behavioral drift.

## Behavioral QA for Nondeterministic Systems

Agentic QA requires behavioral approaches, not input/output determinism checking. Key capabilities a behavioral QA approach must cover:
- **Execution path consistency** — does the agent follow expected reasoning paths across many runs?
- **Failure mode coverage** — does the eval set include known edge cases and escalation triggers?
- **Behavioral regression** — after any change (prompt, model, tool), do execution paths remain within expected bounds?
- **Success criteria beyond latency/accuracy** — behavioral consistency, escalation rate, silent failure detection

## วิธีการเชิงพฤติกรรมสำคัญกว่าขนาด Model
GPT-3.5 + ReAct looping ทำได้ 95.1% เทียบกับ GPT-4 zero-shot ที่ 67% — methodology เชิงพฤติกรรมและ orchestration มีผลกระทบมากกว่าการเลือก model เพียงอย่างเดียว

## Trajectory Evaluation — Agent-Specific Metrics

Agent evaluation requires going beyond the final output: **you must evaluate the path the agent took to get there**. An agent that hallucinated a step in the middle but got lucky with the final answer is not reliable — trajectory evaluation catches this.

An agent's trajectory is the sequence of actions taken (tool calls, retrieval queries, API invocations) before producing its response. The following 6 ground-truth-based metrics evaluate trajectory quality (from [[google-agents-companion]]):

| Metric | What it measures | Rigidity |
|--------|-----------------|----------|
| **Exact match** | Agent trajectory perfectly mirrors the reference trajectory | Highest — no deviation allowed |
| **In-order match** | Core steps occur in correct order; extra steps allowed | High — sequence preserved |
| **Any-order match** | All required steps present; order irrelevant | Medium — steps matter, not sequence |
| **Precision** | What fraction of predicted steps are relevant/correct per reference? | Penalizes unnecessary steps |
| **Recall** | What fraction of reference steps appear in the predicted trajectory? | Penalizes missing required steps |
| **Single-tool use** | Did the agent use a specific tool at all during execution? | Lowest — binary check |

**When to use which**: Exact match for workflows where the procedure is as important as the result (compliance, safety). In-order match for tasks with logical dependencies. Any-order match for exploratory tasks. Precision/recall together for balanced assessment. Single-tool use for checking that a specific capability was exercised.

**Key limitation**: all ground-truth-based trajectory evaluation requires a reference trajectory. Creating reference trajectories is expensive (requires domain experts to specify the ideal path). Research into autoraters for trajectory evaluation ("Agent-as-a-Judge") is active but not yet standard.

## อนุกรมวิธาน Trajectory Evaluation

การประเมิน agent ต้องก้าวเกิน output สุดท้าย: **ต้องประเมินเส้นทางที่ agent ใช้เพื่อไปถึงที่นั่นด้วย** metric 6 ตัวที่ใช้ ground truth:

| Metric | วัดอะไร |
|--------|--------|
| **Exact match** | trajectory ตรงกับ reference ทุกประการ |
| **In-order match** | ขั้นตอนหลักถูกลำดับ; ขั้นตอนพิเศษได้รับอนุญาต |
| **Any-order match** | ขั้นตอนที่จำเป็นครบ; ลำดับไม่สำคัญ |
| **Precision** | fraction ของขั้นตอนที่ทำนายที่ถูกต้องตาม reference |
| **Recall** | fraction ของขั้นตอน reference ที่ปรากฏใน prediction |
| **Single-tool use** | agent ใช้ tool เฉพาะหรือไม่ (binary) |

---

## Evaluation Method Comparison

From [[google-agents-companion]] (Table 1):

| Method | Strengths | Weaknesses |
|--------|-----------|------------|
| **Human Evaluation** | Captures nuanced behavior; considers human factors like creativity and common sense | Subjective; time-consuming; expensive; difficult to scale |
| **LLM-as-Judge (Autorater)** | Scalable; efficient; consistent | May overlook intermediate steps; limited by LLM capabilities and biases |
| **Automated Metrics** | Objective; scalable; efficient | May not capture full capabilities; susceptible to gaming |

**Recommendation**: use all three in combination. Automated metrics and trajectory evaluation for continuous monitoring; LLM-as-judge for final response quality at scale; human evaluation to calibrate whether your autoraters are aligned with human judgment. Don't outsource domain knowledge to automated evaluation alone.

## การเปรียบเทียบวิธีประเมิน

| วิธีการ | จุดแข็ง | จุดอ่อน |
|--------|---------|--------|
| **Human Evaluation** | จับพฤติกรรมที่ละเอียดอ่อน; พิจารณา human factors | อัตวิสัย; ใช้เวลา; แพง; scale ยาก |
| **LLM-as-Judge** | Scale ได้; มีประสิทธิภาพ; สม่ำเสมอ | อาจพลาด intermediate step; จำกัดโดย LLM |
| **Automated Metrics** | Objective; scale ได้; มีประสิทธิภาพ | อาจไม่ครอบคลุมความสามารถเต็มที่; gameable |

---

## Current State
Active tooling and research area (2025–2026). Frameworks: DeepEval, Ragas, PromptFoo. The field is formalizing fast but lacks consensus on standards, especially for agentic multi-step workflows. The ASDLC framing from [[prompts-to-production-agentic-playbook]] is one signal that the field is moving toward formalizing behavioral QA as a discipline distinct from traditional eval metrics.

## สถานะปัจจุบัน
เครื่องมือและงานวิจัยกำลังพัฒนาอย่างรวดเร็ว (ปี 2568–2569) Framework: DeepEval, Ragas, PromptFoo ยังขาดมาตรฐานที่ตกลงกัน โดยเฉพาะสำหรับ agentic workflow หลายขั้นตอน กรอบ ASDLC เป็นสัญญาณว่าสาขากำลังเคลื่อนไปสู่การทำให้ behavioral QA เป็นสาขาวิชาที่เป็นทางการ

---

## Open Questions / คำถามที่ยังไม่มีคำตอบ
- How many labeled examples are enough for a reliable eval suite? / ต้องการตัวอย่างที่มี label กี่รายการถึงจะเชื่อถือได้?
- How do you eval agents in domains where no ground truth exists? / จะ eval agent ในโดเมนที่ไม่มี ground truth ได้อย่างไร?
- Can evals detect emergent failure modes not anticipated at design time? / Eval สามารถตรวจจับโหมดความล้มเหลวแบบ emergent ที่ไม่ได้คาดไว้ได้หรือไม่?

---

## Related / หน้าที่เกี่ยวข้อง
[[llm-as-judge]] · [[agent-observability]] · [[agentic-ai]] · [[hallucination]] · [[rlhf]] · [[automation-bias]] · [[explainability]] · [[interactive-machine-learning]]
[[one-year-of-agentic-ai-six-lessons]] (source / แหล่งที่มา)
[[prompts-to-production-agentic-playbook]] (source / แหล่งที่มา — behavioral QA, eval dataset versioning, 95.1% methodology benchmark)
[[google-agents-companion]] (source / แหล่งที่มา — trajectory evaluation 6 metrics, autorater concept, evaluation method comparison table)
