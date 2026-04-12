---
title: "One Year of Agentic AI: Six Lessons from the People Doing the Work"
type: paper
axis: testing-for-ai
tags: [agentic-ai, evals, observability, workflow, human-in-the-loop]
related: [[agentic-ai]], [[llm-evals]], [[llm-as-judge]], [[agent-observability]], [[ai-tool-selection-rubric]]
created: 2026-04-10
updated: 2026-04-10
---

# One Year of Agentic AI: Six Lessons from the People Doing the Work
# หนึ่งปีของ Agentic AI: หกบทเรียนจากผู้ลงมือทำจริง

## Citation / แหล่งอ้างอิง
Lareina Yee, Michael Chui, Roger Roberts, Stephen Xu. McKinsey QuantumBlack. September 12, 2025.
URL: https://www.mckinsey.com/capabilities/quantumblack/our-insights/one-year-of-agentic-ai-six-lessons-from-the-people-doing-the-work

---

## Core Claim
Deploying agentic AI successfully is hard, and most organizations are doing it wrong — focusing on the agent instead of the workflow, under-investing in evals, and failing to design human-agent collaboration deliberately.

## ข้อสรุปหลัก
การนำ Agentic AI ไปใช้งานจริงนั้นยากกว่าที่คิด และส่วนใหญ่องค์กรทำผิดทิศทาง — มุ่งสนใจที่ตัว agent มากกว่า workflow โดยรวม ลงทุนกับ evals น้อยเกินไป และไม่ออกแบบความร่วมมือระหว่างมนุษย์กับ agent อย่างจริงจัง

---

## Key Contributions
- A six-lesson framework drawn from 50+ agentic AI builds at McKinsey
- A practical taxonomy of 8 eval types for agent assessment
- A decision rubric for when to use agents vs. simpler tools
- Case studies from legal, financial services, and insurance domains

## ผลงานหลักของบทความ
- กรอบ 6 บทเรียนจากการวิเคราะห์โปรเจกต์ Agentic AI กว่า 50 รายการของ McKinsey
- อนุกรมวิธานของ eval 8 ประเภทสำหรับการประเมิน agent
- กรอบการตัดสินใจว่าควรใช้ agent หรือเครื่องมืออื่นที่ง่ายกว่า
- กรณีศึกษาจากวงการกฎหมาย การเงิน และประกันภัย

---

## Method / วิธีวิจัย
Practitioner synthesis: analysis of 50+ agentic AI deployments led by McKinsey, plus review of additional marketplace builds. No formal research methodology — applied consulting insight, not peer-reviewed research.

การสังเคราะห์จากประสบการณ์จริง: วิเคราะห์โปรเจกต์กว่า 50 รายการที่ McKinsey เป็นผู้นำ ไม่มีระเบียบวิธีวิจัยเชิงวิชาการ — เป็นข้อมูลเชิงปฏิบัติจากที่ปรึกษา

---

## Results — Six Lessons / ผลลัพธ์ — หกบทเรียน

**Lesson 1 — It's not about the agent; it's about the workflow.**
Agents that improve a workflow beat technically impressive agents. Map processes, identify user pain points, build feedback loops. Every user edit should be logged and used to teach the agent.

**บทที่ 1 — ไม่ใช่เรื่องของ agent แต่เรื่องของ workflow**
agent ที่ทำให้ workflow โดยรวมดีขึ้นมีคุณค่ามากกว่า agent ที่ดูน่าประทับใจ แมปกระบวนการ ระบุจุดเจ็บปวด สร้าง feedback loop ทุก edit ที่ผู้ใช้ทำควรถูกบันทึกและนำไปสอน agent

**Lesson 2 — Agents aren't always the answer.**
Low-variance, high-standardization tasks are better served by rule-based automation. Agents win for high-variance, multistep workflows with long-tail inputs. See [[ai-tool-selection-rubric]].

**บทที่ 2 — agent ไม่ใช่คำตอบเสมอไป**
งานที่มีความผันแปรต่ำ มาตรฐานสูง เหมาะกับ rule-based automation มากกว่า agent เหมาะกับงานที่มีความผันแปรสูง ตัดสินใจหลายขั้น ดู [[ai-tool-selection-rubric]]

**Lesson 3 — Invest in evals; stop "AI slop".**
"Onboarding agents is more like hiring a new employee than deploying software." Agents need clear job descriptions, onboarding, and continual feedback. Eight eval types specified — see [[llm-evals]]. No "launch and leave."

**บทที่ 3 — ลงทุนกับ evals หยุด "AI slop"**
"การ onboard agent นั้นเหมือนการจ้างพนักงานใหม่มากกว่าการ deploy ซอฟต์แวร์" agent ต้องการ job description ที่ชัดเจน การ onboard และ feedback ต่อเนื่อง ไม่มีการ "launch แล้วทิ้ง" ดู [[llm-evals]]

**Lesson 4 — Track and verify every step.**
At scale, outcome-only tracking makes root cause impossible. Build observability into the workflow at each step. See [[agent-observability]].

**บทที่ 4 — ติดตามและตรวจสอบทุกขั้นตอน**
เมื่อ scale ขึ้น การดูแค่ผลลัพธ์สุดท้ายทำให้หา root cause ไม่ได้ ต้องสร้าง observability ในทุกขั้นตอน ดู [[agent-observability]]

**Lesson 5 — The best use case is the reuse case.**
Building one agent per task creates redundancy. Reusable agent components can eliminate 30–50% of nonessential work.

**บทที่ 5 — use case ที่ดีที่สุดคือ reuse case**
การสร้าง agent ใหม่สำหรับทุกงานทำให้เกิดความซ้ำซ้อน component ที่ใช้ซ้ำได้สามารถลดงานที่ไม่จำเป็นได้ 30–50%

**Lesson 6 — Humans remain essential, but roles and numbers change.**
Humans still needed for oversight, compliance, judgment, edge cases. Headcount in transformed workflows will often be lower. UX matters — one insurer achieved ~95% user acceptance with good UI.

**บทที่ 6 — มนุษย์ยังจำเป็น แต่บทบาทและจำนวนจะเปลี่ยน**
มนุษย์ยังต้องดูแลความถูกต้อง compliance การตัดสินใจ และ edge case แต่จำนวนคนมักลดลงหลัง transform UX มีผลอย่างมาก — บริษัทประกันรายหนึ่งได้รับ user acceptance ~95%

---

## Limitations / ข้อจำกัด
- Selection bias toward large enterprise McKinsey clients / อาจมี selection bias ไปทางองค์กรขนาดใหญ่
- No quantitative performance data beyond the 30–50% reuse claim and 95% acceptance figure / ไม่มีข้อมูลเชิงปริมาณนอกจากตัวเลขดังกล่าว
- Practitioner perspective, not peer-reviewed / เป็นมุมมองที่ปรึกษา ไม่ผ่าน peer review
- September 2025 — field is moving fast / กันยายน 2568 — สาขานี้เปลี่ยนแปลงเร็ว

---

## My Take / ความเห็นส่วนตัว
The evals taxonomy (lesson 3) is the most durable content for this wiki's "testing for AI" axis. The rest is sound deployment strategy but closer to change management. The framing of "agent onboarding as employee onboarding" is useful for thinking about how to specify and test agent behavior. The 30–50% reuse claim is striking but unsourced.

อนุกรมวิธานของ eval ในบทที่ 3 เป็นเนื้อหาที่มีคุณค่ามากที่สุดสำหรับแกน "testing for AI" ของ wiki นี้ กรอบคิด "การ onboard agent = การจ้างพนักงาน" มีประโยชน์สำหรับการคิดเรื่อง specification และ testing ตัวเลข 30–50% น่าสนใจแต่ไม่มีแหล่งอ้างอิงรองรับ

---

## Related / หน้าที่เกี่ยวข้อง
[[agentic-ai]] · [[llm-evals]] · [[llm-as-judge]] · [[agent-observability]] · [[ai-tool-selection-rubric]]
