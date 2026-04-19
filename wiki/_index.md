---
title: Software Testing & AI — Wiki Index / ดัชนี Wiki
updated: 2026-04-19
page_count: 32
source_count: 12
---

# Software Testing & AI — Index / ดัชนี

> **How to use / วิธีใช้**: Read this index first when answering a query. Update on every ingest: add pages with a one-line summary, revise Key Themes when the overall picture shifts.
> อ่านไฟล์นี้ก่อนเมื่อต้องตอบคำถาม อัปเดตทุกครั้งที่ ingest: เพิ่มหน้าใหม่พร้อมสรุปหนึ่งบรรทัด แก้ไข Key Themes เมื่อภาพรวมเปลี่ยน

Two intersecting axes / สองแกนที่ตัดกัน:
- **AI for Testing** — applying AI/ML to make software testing smarter and more autonomous / ใช้ AI/ML เพื่อทำให้การทดสอบฉลาดและอัตโนมัติมากขึ้น
- **Testing for AI** — evaluating, validating, and ensuring quality in AI/ML systems / ประเมิน ตรวจสอบ และรับประกันคุณภาพในระบบ AI/ML

---

## Key Themes / ประเด็นสำคัญ

1. **The Oracle Problem** — defining "correct behavior" is the hard part in both axes / การนิยาม "พฤติกรรมที่ถูกต้อง" คือส่วนที่ยากที่สุดในทั้งสองแกน
2. **LLM Test Generation** — most active area on the AI for Testing side; oracle problem resurfaces here / พื้นที่ที่ active ที่สุดในแกน AI for Testing; oracle problem กลับมาที่นี่ด้วย
3. **Evals as a Discipline** — LLM evaluation becoming its own engineering field / LLM evaluation กำลังกลายเป็นสาขาวิศวกรรมของตัวเอง
4. **Agents Change the Testing Problem** — Wave 3 autonomous testing is agentic AI applied to QA / คลื่น 3 ของการทดสอบอัตโนมัติคือ agentic AI ที่ใช้กับ QA
5. **Tool Selection Matters** — the AI tool choice upstream determines testing complexity downstream / การเลือก AI tool กำหนดความซับซ้อนของการทดสอบ downstream
7. **Explainability Enables Oversight** — human oversight without explainability becomes rubber-stamping; the two are complementary safeguards, not substitutes (MIT Sloan, 77% expert panel) / oversight ที่ไม่มี explainability กลายเป็นการประทับตรา; ทั้งสองเป็น safeguard ที่เสริมกัน
6. **QA Roles Are Restructuring** — from test executors to quality orchestrators; 20–40% salary premium for AI-fluent testers / บทบาท QA กำลังปรับโครงสร้าง; premium 20–40% สำหรับผู้ทดสอบที่ใช้ AI ได้

---

## Concepts / แนวคิด

| Page | Summary / สรุป | Axis |
|------|----------------|------|
| [[agentic-ai]] | LLM-based systems acting autonomously across multistep workflows; Wave 3 testing is this applied to QA / ระบบ LLM ที่ทำงานอัตโนมัติ; คลื่น 3 ของการทดสอบคือสิ่งนี้ที่ใช้กับ QA | testing-for-ai |
| [[llm-evals]] | Structured tests for LLM/agent quality; taxonomy of 8 eval types / การทดสอบที่มีโครงสร้างสำหรับคุณภาพ LLM/agent; อนุกรมวิธาน eval 8 ประเภท | testing-for-ai |
| [[llm-as-judge]] | Using an LLM to evaluate another LLM's outputs; scales well but has known biases / ใช้ LLM ประเมิน output ของ LLM อีกตัว; มี bias ที่รู้จักกัน | testing-for-ai |
| [[agent-observability]] | Step-level tracing and monitoring of agent workflows in production / การติดตามระดับ step ของ agent workflow ใน production | testing-for-ai |
| [[hallucination]] | When LLMs generate factually incorrect or unsupported claims / เมื่อ LLM สร้าง claim ที่ผิดหรือไม่มีหลักฐาน | testing-for-ai |
| [[ai-test-generation]] | Using LLMs to automatically create test cases from code, specs, or behavior; oracle problem resurfaces / ใช้ LLM สร้าง test case อัตโนมัติ; oracle problem กลับมา | ai-for-testing |
| [[self-healing-tests]] | Tests that automatically repair broken selectors when UI changes; reduces maintenance toil / test ที่ซ่อมแซมตัวเองเมื่อ UI เปลี่ยน; ลดงาน maintenance | ai-for-testing |
| [[agentops]] | Disciplined operationalization of agents in production; extends DevOps/MLOps with tool management, agent brain prompts, memory, task decomposition / การนำ agent ไปใช้งาน production อย่างมีวินัย | both |
| [[multi-agent-systems]] | Architectures where multiple specialized agents collaborate; 4 system types, 5 architectural patterns, agent role taxonomy / สถาปัตยกรรมที่ agent เฉพาะทางหลายตัวร่วมกัน | both |
| [[agentic-rag]] | Agents that actively orchestrate retrieval — iterative query refinement, multi-source selection, validation before generation / agent ที่ประสานงาน retrieval อย่างแข็งขัน | both |
| [[risk-based-testing]] | AI converts subjective risk judgment into data-driven scoring using defect history, complexity, and change frequency; drives test prioritization / AI เปลี่ยนการตัดสินใจเรื่องความเสี่ยงเป็นคะแนนที่วัดได้ | ai-for-testing |
| [[pairwise-testing]] | Combinatorial technique covering all parameter pairs; AI adds extraction from requirements, risk weighting, and auto-regeneration / เทคนิค combinatorial ครอบคลุมทุกคู่พารามิเตอร์ | ai-for-testing |
| [[automation-bias]] | Tendency to over-rely on AI outputs without critical evaluation; legally mandated risk under EU AI Act Art. 14(4)(b); must be designed against / แนวโน้มพึ่งพา AI output มากเกินไป | both |
| [[rlhf]] | Reinforcement Learning from Human Feedback — reward model trained on human pairwise preferences guides LLM alignment; foundation of GPT-4, Claude, Gemini / เทคนิคการ align LLM ด้วย human preference | testing-for-ai |
| [[interactive-machine-learning]] | Human inside the feedback loop during operation — not just at dataset creation; IML reduces algorithm perfection pressure; Wekinator, interactive source separation as canonical examples / มนุษย์อยู่ใน feedback loop ระหว่างการทำงาน | both |
| [[explainability]] | The capacity to produce human-understandable accounts of AI reasoning; complementary to (not substitutable for) human oversight; explainability theater is the symmetrical failure to opacity / ความสามารถในการอธิบายเหตุผลของ AI ให้มนุษย์เข้าใจ | both |

## Tools / เครื่องมือ

| Page | Summary / สรุป | Axis |
|------|----------------|------|
| *(none yet / ยังไม่มี)* | | |

## Papers & Articles / บทความและงานวิจัย

| Page | Summary / สรุป | Year / ปี |
|------|----------------|-----------|
| [[one-year-of-agentic-ai-six-lessons]] | McKinsey: 6 lessons from 50+ agentic AI deployments; best source on evals taxonomy / 6 บทเรียนจาก 50+ โปรเจกต์; แหล่งที่ดีสุดสำหรับอนุกรมวิธาน eval | 2025 |
| [[google-agents-companion]] | Google: AgentOps hierarchy, 6 trajectory eval metrics, 5 multi-agent patterns, Agentic RAG, contractor model; most concrete production guide available / คู่มือการนำ agent ไปใช้งาน production ที่เป็นรูปธรรมที่สุด | 2025 |

## Summaries / สรุปบทความ

| Page | Summary / สรุป | Axis |
|------|----------------|------|
| [[ais-impact-on-software-testing-qa-evolution]] | AI restructures QA roles across 3 waves; testers evolve from executors to orchestrators; 20–40% salary premium for AI skills / AI ปรับโครงสร้างบทบาท QA ใน 3 คลื่น | ai-for-testing |
| [[ai-testing-autonomy-decision-guide]] | WLB (Apr 2026): decision flowchart + 19-task matrix mapping testing tasks to HITL/HOTL/HAbL/HBtL; override rate KPI; governance requirements; WLB stack transition roadmap / กรอบการตัดสินใจระดับ autonomy สำหรับ AI testing พร้อม decision matrix 19 งาน | ai-for-testing |
| [[karpathy-llm-wiki-pattern]] | Karpathy's pattern for LLM-maintained persistent wikis; alternative to RAG; ingest/query/lint operations are agentic workflows / รูปแบบ wiki ที่ LLM ดูแลรักษา; ทางเลือกแทน RAG | both |
| [[prompts-to-production-agentic-playbook]] | Goswami (InfoQ 2026): ASDLC, capability matrix for det. vs. agentic decomposition, 7 orchestration patterns, 5-artifact versioning; methodology beats model size (GPT-3.5 iterative 95.1% > GPT-4 zero-shot 67%) / playbook การพัฒนา agentic จาก prototype สู่ production | both |
| [[google-agents-companion]] | Google (Feb 2025): AgentOps + trajectory eval + multi-agent patterns + contractor model; the "102" production guide for agent builders / คู่มือ "102" สำหรับ agent builder ที่เน้น production | both |
| [[ai-in-software-testing-wlb-2026]] | WLB internal report (Apr 2026): As-Is→To-Be map for 4 areas (Strategy, Plan, Case Design, E2E); 80% time reduction benchmark; phased adoption roadmap; 61% org adoption stat / รายงาน WLB ครอบคลุม 4 พื้นที่หลัก | ai-for-testing |
| [[eu-ai-act-article-14-human-oversight]] | EU AI Act Art. 14: 5 mandatory oversight capabilities for high-risk AI; automation bias as legal risk; dual provider/deployer obligation; effective 2 Aug 2026 / ข้อกำหนดกำกับดูแลมนุษย์สำหรับ AI ความเสี่ยงสูง | both |
| [[ibm-human-in-the-loop]] | IBM Think: HITL/HOTL/HOOTL taxonomy; 3 mechanisms (annotation, active learning, RLHF); when to use; annotator subjectivity as fundamental constraint / อนุกรมวิธาน HITL และกลไกสำคัญ | both |
| [[stanford-hai-humans-in-the-loop-design]] | Wang (Stanford HAI): BRB critique (3 shortcomings of full automation), jargon slider/Wekinator/source separation examples, 4 design principles, selective inclusion reframe, tacit knowledge root of oracle problem / ปรัชญาการออกแบบ HITL และหลักการ 4 ข้อ | both |
| [[mit-sloan-ai-explainability-rubber-stamping]] | MIT Sloan + BCG: 77% expert panel finds explainability and oversight are complementary not competing; rubber-stamping mechanism (opacity → passive acceptance → illusion of control); explainability theater; 4 strategic recommendations / explainability และ oversight เป็น safeguard ที่เสริมกัน | both |
| [[entropy-hitl-systematic-review-2026]] | Lazaros et al. (Entropy 2026): 50-page PRISMA systematic review of 134 studies; 3D taxonomy (loop placement × granularity × temporal); 5 loop configurations; trust calibration model (over/well/under-trust); 7 method families with failure modes; 5-dimension HITL eval framework; adversarial manipulation as HITL security risk / systematic review ของ HITL AI ที่ครอบคลุมที่สุด | both |

## People / บุคคล

| Page | Summary / สรุป |
|------|----------------|
| *(none yet / ยังไม่มี)* | |

## Companies / บริษัท

| Page | Summary / สรุป | Axis |
|------|----------------|------|
| *(none yet / ยังไม่มี)* | | |

## Synthesis / บทสังเคราะห์

| Page | Summary / สรุป |
|------|----------------|
| [[ai-tool-selection-rubric]] | When to use agents vs. gen AI vs. rule-based; with testing implications / เมื่อไหร่ควรใช้ agent vs. gen AI vs. rule-based; พร้อมนัยสำคัญด้านการทดสอบ |
| [[contractor-model-and-oracle-problem]] | Google's contractor model as the field's clearest answer to Key Theme #1; where it succeeds and where the oracle problem remains open / contractor model ในฐานะคำตอบที่ชัดเจนที่สุดสำหรับ oracle problem | both |
| [[human-role-in-ai-agents]] | The human's role in AI agent systems across a spectrum: participant → supervisor → governor → auditor; determined by risk, maturity, and compliance / บทบาทของมนุษย์ใน AI agent ตาม autonomy level | both |

---

## Domain Overview / ภาพรวมของโดเมน

This is an active intersection of software engineering and AI research. LLMs are beginning to generate, repair, and prioritize tests — automating work QA engineers do manually. At the same time, the rise of LLMs as production systems has created new testing problems: how do you reliably evaluate a system whose outputs are probabilistic and hard to specify? The two axes share foundational challenges: the oracle problem, the coverage problem, and the specification problem appear in both.

นี่คือจุดตัดที่กำลังพัฒนาระหว่างวิศวกรรมซอฟต์แวร์และการวิจัย AI LLM กำลังเริ่มสร้าง ซ่อมแซม และจัดลำดับ test ในขณะเดียวกัน การเพิ่มขึ้นของ LLM เป็นระบบ production ได้สร้างปัญหาการทดสอบประเภทใหม่: จะประเมินระบบที่มี output แบบ probabilistic ได้อย่างไร? ทั้งสองแกนมีความท้าทายพื้นฐานร่วมกัน: oracle problem, coverage problem, และ specification problem ปรากฏในทั้งสองด้าน
