# บันทึกการดำเนินงาน

เพิ่มเฉพาะ (append-only) ล่าสุดอยู่บน แต่ละรายการขึ้นต้นด้วย `## [YYYY-MM-DD] ประเภท | ชื่อ` เพื่อให้ grep ได้

```bash
# 5 รายการล่าสุด:
grep "^## \[" wiki/_log.md | head -5
# รายการ ingest ทั้งหมด:
grep "^## \[.*\] ingest" wiki/_log.md
```

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
