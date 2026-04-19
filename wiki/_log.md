# บันทึกการดำเนินงาน

เพิ่มเฉพาะ (append-only) ล่าสุดอยู่บน แต่ละรายการขึ้นต้นด้วย `## [YYYY-MM-DD] ประเภท | ชื่อ` เพื่อให้ grep ได้

```bash
# 5 รายการล่าสุด:
grep "^## \[" wiki/_log.md | head -5
# รายการ ingest ทั้งหมด:
grep "^## \[.*\] ingest" wiki/_log.md
```

---

## [2026-04-13] ingest | AI in Software Testing — Autonomy Level Decision Guide (WLB, April 2026)

**แหล่งที่มา**: We Love Bug Co., Ltd. (WLB). Internal Enterprise Deployment Reference. April 2026.
**ไฟล์**: `sources/reports/ai-testing-autonomy-decision-guide.md`

**สร้างใหม่**:
- `wiki/summaries/ai-testing-autonomy-decision-guide.md` — full summary: decision flowchart, 19-task × risk matrix, override rate KPI, governance requirements per level, AI type × level mapping, WLB As-Is→To-Be, maturity progression model, 3 rules from conclusion

**อัปเดต**:
- `wiki/concepts/agentic-ai.md` — added override rate health metric (10–30% HITL), governance infrastructure note, link to new summary
- `wiki/concepts/risk-based-testing.md` — added Risk Score → autonomy level formula (L×I maps to HITL/HOTL/HAbL/HBtL), connection section
- `wiki/synthesis/human-role-in-ai-agents.md` — added testing-specific 3 rules from conclusion, override rate metric, link to new summary
- `wiki/_index.md` — added summary page entry; page_count 21→22, source_count 6→7

**ประเด็นสำคัญ**:
- The 75%–16% stat (QA leaders vs. orgs with production AI) is the core framing: the gap is governance, not tooling
- Override rate (10–30%) is a new concrete calibration KPI not previously in the wiki
- Risk Score → autonomy level formula directly extends [[risk-based-testing]] beyond prioritization into governance

---

## [2026-04-13] query | What is the role of the human in the AI Agent?

**สร้างใหม่**:
- `wiki/synthesis/human-role-in-ai-agents.md` — autonomy level framework (4 levels), evolving role from user to fleet manager, human as decision authority at high-stakes points; spectrum: participant → supervisor → governor → auditor

**อ้างอิงหลัก**: [[agentic-ai]], [[multi-agent-systems]]

---
## [2026-04-19] ingest | Human-in-the-Loop AI: A Systematic Review — Entropy 2026

**แหล่งที่มา**: Lazaros, K.; Vrahatis, A.G.; Kotsiantis, S. *Entropy* 2026, 28, 377
**DOI**: https://doi.org/10.3390/e28040377
**ไฟล์**: `sources/papers/entropy-28-00377-v2.pdf` (50 หน้า, open access)
**Method**: PRISMA-aligned systematic review; 134 studies in structured synthesis

**สร้างใหม่**:
- `wiki/summaries/entropy-hitl-systematic-review-2026.md` — full summary: 3D taxonomy, 5 loop configurations (In/On/Over/Under/Along), 7 method families with failure modes, trust calibration model (over/well/under-trust), 5-dimension HITL eval framework, adversarial manipulation risk, "human-with-the-loop" vision, connections table

**อัปเดต**:
- `wiki/concepts/automation-bias.md` — เพิ่ม "Trust Calibration: Over-Trust, Well-Calibrated, Under-Trust" section: tri-zone model with calibration interventions; skill degradation as over-trust consequence; "Scapegoat-in-the-loop" risk: human held responsible for AI decisions without meaningful oversight capacity
- `wiki/concepts/interactive-machine-learning.md` — เพิ่ม "IML-Specific Failure Modes" section: non-stationary guidance, oscillatory updates, local patches degrading global performance, confirmation bias, cognitive overload; all from Table 1 of the review
- `wiki/concepts/rlhf.md` — เพิ่ม 3 failure modes: collapse to safe but uninformative outputs (distinct from reward hacking), norm/preference drift, inconsistent rater judgments; updated Related
- `wiki/concepts/agentic-ai.md` — เพิ่ม "Entropy Review: Five Loop Configurations" section: adds Under-the-Loop (AI advisory, human executor) and Along-the-Loop (collaborative peer) — two patterns not in existing 4-level framework; 3D taxonomy insight: loop placement alone insufficient
- `wiki/_index.md` — เพิ่ม entropy-hitl-systematic-review-2026 ใน Summaries; page_count: 30, source_count: 11

**น่าสนใจ**: สามประเด็นที่ไม่เคยมีใน wiki ก่อน: (1) **Under-the-Loop** — AI advisory + human executor เป็น pattern ที่พบบ่อยมากในระบบ decision support แต่ไม่มีชื่อที่ชัดเจนในแหล่งอื่น; (2) **Adversarial manipulation** ของ human components ใน HITL — threat model ต้องรวม human vulnerabilities ไม่ใช่แค่ technical vulnerabilities; (3) **5-dimension HITL eval framework** และ vector reporting principle: รายงานผลเป็น vector ต่อ dimension ไม่ใช่ aggregate score — ป้องกันการ suppress failure modes ที่ dimension หนึ่งดีขึ้นขณะอีก dimension แย่ลง ความสำเร็จ HITL ขึ้นอยู่กับ workflow integration มากกว่า model accuracy — confirmed across all 6 domains

---

## [2026-04-19] ingest | AI Explainability: How to Avoid Rubber-Stamping Recommendations — MIT Sloan

**แหล่งที่มา**: MIT Sloan Management Review, June 12, 2025
**URL**: https://sloanreview.mit.edu/article/ai-explainability-how-to-avoid-rubber-stamping-recommendations/
**Authors**: Elizabeth M. Renieris, David Kiron, Steven Mills, Anne Kleppe (research partner: BCG)
**Method**: 30-person international expert panel + global executive survey (n=1,221)

**สร้างใหม่**:
- `wiki/summaries/mit-sloan-ai-explainability-rubber-stamping.md` — full summary: central finding (77% panel), complementarity framework, rubber-stamping mechanism, explainability theater, 4 strategic recommendations, organizational survey data, regulatory context
- `wiki/concepts/explainability.md` — new concept: definition, types (global/local, intrinsic/post-hoc, by audience), explainability theater problem, context-dependent explainability framework, connection to oversight/automation-bias/llm-as-judge/EU AI Act

**อัปเดต**:
- `wiki/concepts/automation-bias.md` — เพิ่ม "Explainability as the Upstream Enabler" section: opacity → passive acceptance → rubber-stamping mechanism; explainability theater as symmetrical failure; MIT Sloan 77% finding; updated Related links
- `wiki/concepts/llm-as-judge.md` — เพิ่ม "Explainability of Judge Outputs" section: judge scores without reasoning create rubber-stamping risk; EU Art. 14(4)(c) implication for judge deployments; updated Related links
- `wiki/summaries/eu-ai-act-article-14-human-oversight.md` — เพิ่มย่อหน้า MIT Sloan empirical support ใต้ Art. 14(4)(c) interpretability standard; updated Related links
- `wiki/_index.md` — เพิ่ม explainability ใน Concepts; mit-sloan summary ใน Summaries; Key Theme #7; page_count: 29, source_count: 10

**น่าสนใจ**: การค้นพบที่ชัดเจนที่สุดคือ **77% panel disagreement** กับ proposition ว่า oversight ลด explainability needs — นี่เป็น empirical evidence ที่แข็งแกร่งว่าทั้งสองเป็น complementary safeguards Concept "explainability theater" เป็น insight ใหม่ที่สำคัญ: performative explanations อาจ *อันตรายกว่า* opacity เพราะลบ skepticism ของ overseer ไป โดยไม่ให้ insight จริง Connection กับ [[llm-as-judge]] ชัดเจน: judge scores ไม่มี reasoning คือ black-box output — oversight ต้องการ reasoning trail ไม่ใช่แค่ score

---

## [2026-04-19] ingest | Humans in the Loop: The Design of Interactive AI Systems — Stanford HAI

**แหล่งที่มา**: Ge Wang, Stanford HAI (Human-Centered AI), October 20, 2019
**URL**: https://hai.stanford.edu/news/humans-loop-design-interactive-ai-systems

**สร้างใหม่**:
- `wiki/summaries/stanford-hai-humans-in-the-loop-design.md` — full summary: BRB critique (3 structural shortcomings of full automation), jargon slider / Wekinator / interactive source separation examples, Wang's 4 design principles, Polanyi tacit knowledge, contrast table with IBM framing
- `wiki/concepts/interactive-machine-learning.md` — concept: human inside feedback loop during operation (not just at dataset creation); core loop diagram; Wekinator / source separation / jargon slider as canonical examples; reduced algorithm perfection pressure; connection to RLHF and active learning; IML limitations (scalability, fatigue, subjectivity drift)

**อัปเดต**:
- `wiki/concepts/automation-bias.md` — เพิ่ม "BRB Design as the Structural Cause" section: Wang's argument that BRB design *creates* the conditions for automation bias; tool-vs-oracle distinction: oracle interfaces structurally breed bias, tool interfaces structurally resist it; updated Related section
- `wiki/synthesis/ai-tool-selection-rubric.md` — เพิ่ม "Wang's Design Principles: The Philosophy Behind the Matrix" section: 4 principles mapped to tool-selection implications; "selective inclusion" reframe; reduced algorithm perfection pressure connects to llm-evals ReAct finding
- `wiki/concepts/agentic-ai.md` — เพิ่ม "Wang's Selective Inclusion Reframe" section: autonomy level choice reframed as "where does human participation create the most value?" — HITL checkpoints as designed inclusions, not fallbacks
- `wiki/_index.md` — เพิ่ม interactive-machine-learning ใน Concepts; stanford-hai-humans-in-the-loop-design ใน Summaries; page_count: 27, source_count: 9

**น่าสนใจ**: Wang's deepest contribution คือการ reframe automation: ไม่ใช่ "การนำมนุษย์ออก" แต่คือ "selective inclusion of human participation" เปลี่ยน engineering question → HCI design challenge Tacit knowledge (Polanyi) เป็น root ของทั้ง oracle problem (Key Theme #1) และ BRB failure: สิ่งที่มนุษย์ "รู้มากกว่าที่พูดได้" — taste, judgment, meaning — ไม่สามารถ specify เป็น input ให้ BRB system ได้ Wekinator case study เป็น existence proof ที่ powerful: single-layer network + good HITL interaction design > complex network alone ตรงกับ [[llm-evals]] finding (GPT-3.5 + ReAct 95.1% > GPT-4 zero-shot 67%)

---

## [2026-04-12] ingest | What Is Human-in-the-Loop (HITL)? — IBM Think

**แหล่งที่มา**: IBM Think Topics — "What Is Human In The Loop (HITL)?"
**URL**: https://www.ibm.com/think/topics/human-in-the-loop

**สร้างใหม่**:
- `wiki/summaries/ibm-human-in-the-loop.md` — full summary: HITL/HOTL/HOOTL taxonomy, 3 mechanisms (annotation, active learning, RLHF), use cases across healthcare/finance/autonomous vehicles, benefits and challenges, annotator subjectivity as fundamental constraint
- `wiki/concepts/rlhf.md` — concept: 3-stage process (SFT → reward model → PPO); connection to llm-as-judge pairwise; limitations (subjectivity, reward hacking, cost); variants (RLAIF, DPO)

**อัปเดต**:
- `wiki/concepts/agentic-ai.md` — เพิ่ม IBM HITL/HOTL/HOOTL taxonomy section: complements 4-level autonomy framework; HOOTL specifically flagged as risk category (acts "even when confidence is low or outcomes are irreversible")
- `wiki/concepts/automation-bias.md` — เพิ่ม "HITL as the Structural Countermeasure" section: IBM's key caveat that HITL creates the opportunity for oversight, not the guarantee — HITL itself can degrade into rubber-stamping
- `wiki/concepts/llm-as-judge.md` — เพิ่ม "Human Subjectivity — The Fundamental Constraint" section: annotators disagree on what "appropriate behavior" means; LLM judges inherit these subjectivities; practical implication: judge scores must be reported with human calibration data; added new open question and related links
- `wiki/_index.md` — เพิ่ม rlhf ใน Concepts; summary ใน Summaries; page_count: 25, source_count: 8

**น่าสนใจ**: IBM's sharpest contribution ไม่ใช่ taxonomy (HITL/HOTL/HOOTL) แต่คือ observation ที่ว่า **HOOTL คือ risk category ไม่ใช่แค่ end of spectrum** — "AI acts even when confidence is low or outcomes are irreversible" ทำให้ HOOTL ไม่ใช่แค่ human-free automation แต่คือ autonomous action under uncertainty without oversight ซึ่งแตกต่างจาก HOTL เชิงคุณภาพ Human subjectivity ใน annotation เป็น insight ที่ต่อกับ [[llm-as-judge]] โดยตรง: judge scores ที่ไม่ระบุ human calibration baseline คือ unfalsifiable claim — ไม่รู้ว่า "agree with humans" หมายถึง humans คนไหน

---

## [2026-04-12] ingest | EU AI Act — Article 14: Human Oversight

**แหล่งที่มา**: EU Artificial Intelligence Act, Article 14 (with Recitals 66 and 73)
**URL**: https://artificialintelligenceact.eu/article/14/
**บังคับใช้**: 2 สิงหาคม 2569 (2 August 2026)

**สร้างใหม่**:
- `wiki/summaries/eu-ai-act-article-14-human-oversight.md` — full summary: 5 mandatory oversight capabilities, dual provider/deployer obligation, enhanced biometric rule, practical compliance checklist, connections to existing wiki concepts
- `wiki/concepts/automation-bias.md` — concept: legally mandated risk under Art. 14(4)(b); how it manifests in AI workflows; design countermeasures; connections to llm-as-judge and self-healing tests

**อัปเดต**:
- `wiki/concepts/agentic-ai.md` — เพิ่ม "EU AI Act Constraint on Autonomy Level Choice" ใน Autonomy Level Framework section: Art. 14 mandates Human-on-the-Loop as minimum for high-risk AI; Human-above/behind-the-Loop likely non-compliant
- `wiki/concepts/agentops.md` — เพิ่ม "EU AI Act Compliance Implications" section: stop button (Art. 14(4)(e)), override capability (14(4)(d)), monitoring (14(4)(a)), interpretability (14(4)(c)), automation bias countermeasures (14(4)(b)); dual provider/deployer structure
- `wiki/concepts/agent-observability.md` — เพิ่ม "EU AI Act — Observability as Legal Requirement" section: Art. 14(4)(a) elevates observability from best practice to legal compliance for high-risk AI
- `wiki/_index.md` — เพิ่ม automation-bias ใน Concepts; summary ใน Summaries; page_count: 23, source_count: 7

**น่าสนใจ**: Article 14 เป็น source แรกใน wiki ที่นำมิติ **กฎหมาย** เข้ามา — สิ่งที่เคยเป็น "best practice" (observability, human oversight, stop mechanisms) กลายเป็น **ข้อบังคับทางกฎหมาย** สำหรับ high-risk AI ใน EU ที่น่าสังเกตที่สุดคือ: **automation bias** ถูกระบุชื่อในกฎหมาย EU เป็นครั้งแรก — ไม่ใช่แค่ concern ด้านการออกแบบ แต่เป็น legal risk ที่ provider ต้องออกแบบป้องกัน กรอบ 4 ระดับ autonomy ใน [[agentic-ai]] ซึ่งก่อนหน้านี้เป็นเพียง architectural choice ตอนนี้มีข้อจำกัดทางกฎหมายที่ชัดเจน: Human-above/behind-the-Loop อาจไม่ compliant สำหรับ high-risk AI systems ใน EU

---

## [2026-04-12] ingest | AI in Software Testing: Trend Update & Business Readiness Guide (WLB, April 2026)

**แหล่งที่มา**: We Love Bug Co., Ltd. (WLB). Internal Strategic Reference. April 2026.
**ไฟล์**: `sources/reports/AI-in-Software-Testing.md`

**สร้างใหม่**:
- `wiki/summaries/ai-in-software-testing-wlb-2026.md` — full summary with market stats, As-Is→To-Be for 4 areas, AI classification taxonomy, tools map, phased roadmap
- `wiki/concepts/risk-based-testing.md` — concept stub: AI-augmented risk scoring from defect history, complexity, change frequency; SeaLights/Tosca tools
- `wiki/concepts/pairwise-testing.md` — concept stub: combinatorial technique; AI adds parameter extraction, risk weighting, auto-regeneration

**อัปเดต**:
- `wiki/concepts/ai-test-generation.md` — เพิ่ม: BVA/EP/STT/DT automation section, pairwise/RBT integration, E2E alternative flows via chain-of-thought, 80% time benchmark, 2026 stats (61% org adoption, 42% QA leaders priority), updated tools list, new related links
- `wiki/concepts/self-healing-tests.md` — เพิ่ม BrowserStack 2026 confirmation: "up to 30% of QA team time" for script maintenance pre-AI
- `wiki/_index.md` — เพิ่ม risk-based-testing, pairwise-testing ใน Concepts; summary ใน Summaries; page_count: 21, source_count: 6

**น่าสนใจ**: **80% time efficiency improvement** (Thoughtworks) คือ benchmark ที่เป็นรูปธรรมที่สุดใน wiki สำหรับ AI test generation ROI ตัวเลข **61% org adoption** และ **88% budget increase intent** แสดงว่า AI testing ข้ามเส้น "early adopter" ไปแล้ว การที่ Integration ติดอันดับ 1 (37%) ขณะที่ budget ติดอันดับ 5 เป็น signal สำคัญ: bottleneck ไม่ใช่ความตั้งใจหรืองบประมาณ แต่เป็น workflow integration ความสัมพันธ์ระหว่าง **adoption timeline** (4+ years → 83% more likely >100% ROI) กับ ROI เสริม Key Theme #5 (Tool Selection Matters): เวลาที่เริ่มใช้ก็สำคัญไม่แพ้การเลือกเครื่องมือ

---

## [2026-04-12] query | How many levels of human-in-the-loop?

**คำถาม**: How many levels of human involvement exist in agentic AI autonomy frameworks?

**คำตอบ**: 4 levels (from [[prompts-to-production-agentic-playbook]] via [[agentic-ai]]):
1. Human-in-the-Loop — direct intervention at decision points
2. Human-on-the-Loop — meaningful real-time control
3. Human-above-the-Loop — strategic governance only
4. Human-behind-the-Loop — post-operational analysis only

Level choice determines testing strategy, observability requirements, and acceptable failure modes.

---

## [2026-04-12] query | The contractor model as an answer to the oracle problem

**คำถาม**: Does Google's contractor model (Agents Companion) constitute a meaningful answer to Key Theme #1 — the oracle problem?

**สร้างใหม่**:
- `wiki/synthesis/contractor-model-and-oracle-problem.md`

**อัปเดต**:
- `wiki/_index.md` — เพิ่ม synthesis entry, page_count: 18

**ข้อสรุป**: Contractor model เป็น contribution เชิงกระบวนการ — บังคับให้ระบุ oracle ก่อนเริ่ม execution ไม่ใช่หลังจากเห็น output แต่ยัง displace ปัญหาไม่ได้แก้: ยังต้องการผู้เชี่ยวชาญในการเขียน contract และสร้าง reference trajectory; emergent multi-agent behavior ยังคงเป็น open question

---

## [2026-04-12] ingest | Agents Companion (Google, February 2025)

**แหล่งที่มา**: Gulli, Nigam, Wiesinger, Vuskovic, Sigler, Nardini, Stroppa, Kartakis, Saribekyan, Nawalgaria, Bount. Google. February 2025.
**ไฟล์**: `sources/papers/Agents_Companion_v2.pdf`

**สร้างใหม่**:
- `wiki/summaries/google-agents-companion.md` — narrative digest of the paper's 5 key ideas
- `wiki/papers/google-agents-companion.md` — full academic summary (created in prior session; logged here)
- `wiki/concepts/agentops.md` — AgentOps ops hierarchy, success metrics, A/B experiments (created in prior session; logged here)
- `wiki/concepts/multi-agent-systems.md` — 4 system types, 5 architectural patterns, agent role taxonomy, challenges, evaluation (created in prior session; logged here)
- `wiki/concepts/agentic-rag.md` — iterative retrieval, 4 mechanisms, "better search first" principle (created in prior session; logged here)

**อัปเดต**:
- `wiki/concepts/llm-evals.md` — เพิ่ม `[[google-agents-companion]]` ใน Related section (trajectory 6 metrics, autorater, eval method comparison table)
- `wiki/_index.md` — เพิ่ม agentops, multi-agent-systems, agentic-rag ใน Concepts table; เพิ่ม paper ใน Papers table; เพิ่ม summary ใน Summaries table; page_count: 17, source_count: 5

**น่าสนใจ**: **Contractor model** คือ contribution ที่ใหม่ที่สุด — reframes agent-as-tool เป็น agent-as-service-provider พร้อม formal contract fields (deliverables, expected cost/duration, reporting) ตอบ open question ใน [[agentic-ai]]: "จะระบุพฤติกรรม agent ที่ถูกต้องอย่างเป็นทางการได้อย่างไร?" **Trajectory evaluation taxonomy** (6 metrics) เติมช่องว่างใน [[llm-evals]] — มี concept แต่ขาด metric ที่เฉพาะเจาะจง กระดาษนี้ reinforce Key Theme #4 (Agents Change the Testing Problem) ด้วยหลักฐานจาก production จริง

---

## [2026-04-11] ingest | From Prompts to Production: A Playbook for Agentic Development (Goswami, InfoQ)

**แหล่งที่มา**: Abhishek Goswami, InfoQ, February 11, 2026
URL: https://www.infoq.com/articles/prompts-to-production-playbook-for-agentic-development/

**สร้างใหม่**:
- `wiki/summaries/prompts-to-production-agentic-playbook.md`

**อัปเดต**:
- `wiki/concepts/agentic-ai.md` — เพิ่ม ASDLC framework, ReAct 8-step loop detail, Supervisor/Hierarchical/HITL patterns with evidence, Autonomy Level Framework (4 levels), fixed lint item C1 (axis: testing-for-ai → both)
- `wiki/concepts/llm-evals.md` — เพิ่ม "methodology beats model size" benchmark (GPT-3.5 iterative 95.1% > GPT-4 zero-shot 67%), eval datasets as versioned artifacts, behavioral QA section
- `wiki/concepts/agent-observability.md` — เพิ่ม "Tracing as Planning Requirement" section, 63% path variation stat, behavioral regression testing angle
- `wiki/synthesis/ai-tool-selection-rubric.md` — เพิ่ม Capability Matrix step-level decomposition, customer support example table, 4 reliability principles
- `wiki/_index.md` — เพิ่ม summaries entry, page_count: 12, source_count: 4

**น่าสนใจ**: ตัวเลข 95.1% (GPT-3.5 + ReAct iterative) กับ 67% (GPT-4 zero-shot) เป็น argument ที่แข็งแกร่งว่า methodology > model selection ซึ่งตรงประเด็นทั้งสองแกน: ทั้งการออกแบบ agentic testing architecture และการ justify การลงทุนใน eval infrastructure Capability Matrix เป็น framework ที่นำไปใช้ได้ทันทีสำหรับ wiki's Key Theme #5 (Tool Selection Matters)

---

## [2026-04-10] lint | Health check — 13 files

**ผลลัพธ์**: ไม่มี orphan pages · 4 ความขัดแย้ง · 6 concepts ที่กล่าวถึงแต่ไม่มีหน้า · 4 claim ที่น่าสงสัย · 3 ปัญหาโครงสร้าง
**รายงานฉบับเต็ม**: `wiki/lint-report.md`

**การแก้ไขเร่งด่วน**:
1. `concepts/agentic-ai.md` — เปลี่ยน `axis` เป็น `both`
2. สร้าง `wiki/concepts/oracle-problem.md` — Key Theme #1 ของ wiki ยังไม่มีหน้าของตัวเอง
3. อัปเดต `CLAUDE.md` — บันทึก `summaries/` directory และความแตกต่างจาก `papers/`

---

## [2026-04-10] ingest | LLM Wiki: A Pattern for Persistent, Compounding Knowledge Bases (Karpathy)

**แหล่งที่มา**: Andrej Karpathy, GitHub Gist, 2025
URL: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f

**สร้างใหม่**:
- `wiki/summaries/karpathy-llm-wiki-pattern.md`

**อัปเดต**:
- `wiki/concepts/agentic-ai.md` — เพิ่มส่วน "Non-Enterprise Example: LLM Wiki" เชื่อม ingest/lint loop กับ agentic workflow และ llm-evals
- `wiki/_index.md` — เพิ่ม summaries entry, page_count: 11, source_count: 3

**น่าสนใจ**: นี่คือ ingest แบบ self-referential — gist นี้คือเอกสารพื้นฐานที่อธิบายระบบที่กำลังรัน wiki นี้อยู่ การดำเนินการ lint เชื่อมโยงกับ [[llm-evals]] โดยตรง: ทั้งคู่เป็นกลไก self-evaluation ที่ LLM ตรวจสอบ output ของตัวเอง

---

## [2026-04-10] ingest | AI's Impact on Software Testing: The Evolution of QA Engineers, SDETs, and Automation Architects

**แหล่งที่มา**: Lana Begunova, Women in Technology / Medium, 2025
URL: https://medium.com/womenintechnology/ais-impact-on-software-testing-the-evolution-of-qa-engineers-sdets-and-automation-architects-71cd91e46401

**สร้างใหม่**:
- `wiki/summaries/ais-impact-on-software-testing-qa-evolution.md` (new `summaries/` directory — separate from `papers/`)
- `wiki/concepts/self-healing-tests.md`
- `wiki/concepts/ai-test-generation.md`

**อัปเดต**:
- `wiki/concepts/agentic-ai.md` — เพิ่มส่วน "Connection to AI for Testing" เชื่อม Wave 3 autonomous testing
- `wiki/_index.md` — เพิ่ม summaries section, 2 concept ใหม่, อัปเดต Key Themes (page_count: 10, source_count: 2)

**น่าสนใจ**: นี่คือแหล่ง AI-for-Testing แรกใน wiki ปรับสมดุลกับ McKinsey ที่เน้น testing-for-AI กรอบสามคลื่น (2025→2026→2030+) เชื่อมโยงกับ agentic-ai โดยตรง ตัวเลขเงินเดือน 20–40% premium น่าสนใจแต่ไม่มีแหล่งอ้างอิง

---

## [2026-04-10] update | เปลี่ยนภาษาเนื้อหาทั้งหมดเป็นภาษาไทย

เขียนหน้าทั้งหมดใหม่เป็นภาษาไทยตามคำขอของผู้ใช้ ชื่อไฟล์และ frontmatter key ยังคงเป็นภาษาอังกฤษ

---

## [2026-04-10] ingest | หนึ่งปีของ Agentic AI: หกบทเรียนจากผู้ลงมือทำจริง

**แหล่งที่มา**: McKinsey QuantumBlack, กันยายน 2568 — https://www.mckinsey.com/capabilities/quantumblack/our-insights/one-year-of-agentic-ai-six-lessons-from-the-people-doing-the-work

**สร้างใหม่**:
- `wiki/papers/one-year-of-agentic-ai-six-lessons.md`
- `wiki/concepts/agentic-ai.md`
- `wiki/concepts/llm-evals.md` — อนุกรมวิธาน eval 8 ประเภท
- `wiki/concepts/llm-as-judge.md`
- `wiki/concepts/agent-observability.md`
- `wiki/concepts/hallucination.md` (stub)
- `wiki/synthesis/ai-tool-selection-rubric.md`

**อัปเดต**: `wiki/_index.md` (page_count: 7, source_count: 1)

**น่าสนใจ**: ส่วน evals (บทที่ 3) ตรงกับแกน "testing for AI" โดยตรง ตัวเลข 30–50% เรื่อง reuse น่าสนใจแต่ไม่มีแหล่งอ้างอิงรองรับ กรอบคิด "การ onboard agent = การจ้างพนักงาน" มีประโยชน์สำหรับการคิดเรื่อง specification และ testing

---

## [2026-04-10] init | เริ่มต้น Wiki

- สร้างโครงสร้างไดเรกทอรี: `sources/`, `wiki/concepts/`, `wiki/tools/`, `wiki/papers/`, `wiki/people/`, `wiki/companies/`, `wiki/synthesis/`
- สร้าง `CLAUDE.md`, `wiki/_index.md`, `wiki/_log.md`
- ยังไม่มีแหล่งที่มาที่ ingest
