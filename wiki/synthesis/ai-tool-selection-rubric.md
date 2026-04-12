---
title: กรอบการเลือกเครื่องมือ AI / AI Tool Selection Rubric
type: synthesis
axis: both
tags: [agentic-ai, automation, decision-framework, tool-selection]
related: [[agentic-ai]], [[llm-evals]], [[one-year-of-agentic-ai-six-lessons]], [[prompts-to-production-agentic-playbook]]
created: 2026-04-10
updated: 2026-04-11
---

# กรอบการเลือกเครื่องมือ AI / AI Tool Selection Rubric

When to use agents vs. simpler tools. Synthesized from McKinsey's practitioner analysis ([[one-year-of-agentic-ai-six-lessons]]).

เมื่อไหร่ควรใช้ agent และเมื่อไหร่ควรใช้เครื่องมืออื่นที่ง่ายกว่า สังเคราะห์จากการวิเคราะห์ของ McKinsey

---

## The Core Question / คำถามหลัก

> "What is the work to be done and what are the relative talents of each potential team member — or agent — to work together to achieve those goals?"

> "งานที่ต้องทำคืออะไร และแต่ละสมาชิกทีม — หรือ agent — มีความสามารถเฉพาะอะไรที่จะทำงานร่วมกันบรรลุเป้าหมาย?"

The common failure mode: defaulting to agents because they seem powerful, without asking whether simpler automation would be more reliable, cheaper, and easier to test.

รูปแบบความล้มเหลวที่พบบ่อย: เลือก agent เพราะดูมีประสิทธิภาพ โดยไม่ถามว่า automation ที่ง่ายกว่าจะน่าเชื่อถือกว่า ถูกกว่า และทดสอบได้ง่ายกว่าหรือไม่

---

## Decision Framework / กรอบการตัดสินใจ

| Task / ลักษณะของงาน | Recommended Tool / เครื่องมือที่แนะนำ |
|---|---|
| Rule-based, repetitive, structured input (data entry, forms) / Rule-based ทำซ้ำ input มีโครงสร้าง | Rule-based automation |
| Unstructured input (long docs), extractive or generative task / Input ไม่มีโครงสร้าง งาน extractive | Gen AI / NLP / predictive analytics |
| Classification or forecasting from historical data / จัดประเภทหรือพยากรณ์จากข้อมูลอดีต | Predictive analytics or gen AI |
| Synthesis, judgment, or creative interpretation / การสังเคราะห์ การตัดสิน การตีความ | Gen AI |
| Multistep decision-making, long tail of variable inputs / การตัดสินใจหลายขั้น input ผันแปรสูง | AI Agents |

---

## The Two Dimensions / สองมิติหลัก

**Standardization** — how predictable and codifiable is correct behavior?
**ความเป็นมาตรฐาน** — พฤติกรรมที่ถูกต้องสามารถคาดเดาและ codify ได้แค่ไหน?

**Variance** — how much do inputs and contexts differ across instances?
**ความผันแปร** — input และบริบทแตกต่างกันมากแค่ไหนในแต่ละ instance?

```
                High Standardization / ความเป็นมาตรฐานสูง
                        │
    Rule-based          │         Hybrid (rules + gen AI)
    automation          │
                        │
Low Variance ───────────┼─────────────────── High Variance
ความผันแปรต่ำ           │                    ความผันแปรสูง
                        │
    Predictive          │         AI Agents
    analytics           │
                        │
                Low Standardization / ความเป็นมาตรฐานต่ำ
```

- **Top-left / บน-ซ้าย** — tightly governed, predictable logic → rule-based. Adding LLM non-determinism adds complexity without value. / workflow ที่ควบคุมเข้มงวด ตรรกะคาดเดาได้ → rule-based
- **Bottom-right / ล่าง-ขวา** — complex, multistep, judgment-heavy → agents. / ซับซ้อน หลายขั้นตอน ต้องใช้การตัดสิน → agents
- **Middle / ตรงกลาง** — most real workflows. Use a targeted mix. / workflow จริงส่วนใหญ่ ใช้ผสมผสานตามความเหมาะสม

---

## Relevance to Testing / ความเกี่ยวข้องกับการทดสอบ

This rubric matters for test automation design, not just production AI deployment.

กรอบนี้สำคัญสำหรับการออกแบบ test automation ไม่ใช่แค่ production AI

- **AI for testing** — Should you use an LLM to generate tests, or a rule-based template? Apply the same rubric. Highly structured test generation (CRUD endpoints) → templates win. Complex business logic → LLM generation may win. / ควรใช้ LLM สร้าง test หรือ template แบบ rule-based? ใช้กรอบเดียวกัน
- **Testing for AI** — Simpler AI systems (classifiers) are easier to test than agents. The tool choice upstream determines the complexity of the testing problem downstream. / ระบบ AI ที่ง่ายกว่าทดสอบได้ง่ายกว่า การเลือกเครื่องมือ upstream กำหนดความซับซ้อน downstream

---

## Capability Matrix: Step-Level Decomposition

[[prompts-to-production-agentic-playbook]] extends this rubric with a concrete **Capability Matrix** methodology — a workflow-by-workflow, step-by-step decomposition rather than a high-level heuristic. The core question per step: *Can fixed rules make this decision unambiguously?* If yes → deterministic. If the decision requires interpreting unstructured inputs, synthesizing variable context, or reasoning under uncertainty → agentic.

**Four reliability principles from the Capability Matrix:**

1. **Determinism for fixed-rule decisions** — if the answer follows clearly from data, don't add LLM reasoning
2. **Agentic for genuine uncertainty** — intent analysis, relevance scoring, free-text reasoning are the right candidates
3. **Significant non-agentic remainder** — most workflows suitable for agents still contain the majority of their steps as rule-based
4. **Cost optimization follows automatically** — restricting LLM calls to genuinely nondeterministic tasks reduces inference spend

**Concrete example** — Customer support workflow decomposition:

| Step | Deterministic | Agentic |
|------|--------------|---------|
| Ticket reception | ID generation, SLA timer, customer lookup | Intent analysis, issue identification |
| Classification | Queue assignment (from agentic output) | Category, priority, complexity assessment |
| Knowledge base search | DB lookup, caching | Query generation, relevance scoring |
| Solution initiation | Command execution | Which solution to apply |
| Response generation | Template + routing | Personalization, verbiage |
| Closure | Notifications, SLA tracking | Closure recommendation, summary |

The dividing line: **understanding unstructured intent is agentic; acting on known system state is deterministic.**

## Capability Matrix: การแยกย่อยระดับขั้นตอน

บทความ Goswami ขยาย rubric นี้ด้วยวิธีการ **Capability Matrix** ที่เป็นรูปธรรม — การแยกย่อยแบบ workflow ต่อ workflow, ขั้นตอนต่อขั้นตอน แทนที่จะเป็น heuristic ระดับสูง คำถามหลักต่อขั้นตอน: *กฎตายตัวสามารถตัดสินใจนี้ได้อย่างชัดเจนหรือไม่?* ถ้าใช่ → deterministic ถ้าไม่ → agentic

---

## Source / แหล่งที่มา
[[one-year-of-agentic-ai-six-lessons]] — lesson 2 / บทที่ 2: "Agents aren't always the answer"
[[prompts-to-production-agentic-playbook]] — Capability Matrix methodology and step-level decomposition / วิธีการ Capability Matrix และการแยกย่อยระดับขั้นตอน
