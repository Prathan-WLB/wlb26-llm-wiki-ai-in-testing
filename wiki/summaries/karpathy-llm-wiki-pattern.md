---
title: "LLM Wiki: A Pattern for Persistent, Compounding Knowledge Bases"
type: paper
axis: both
tags: [llm, knowledge-management, agentic-ai, rag, wiki-methodology, meta]
related: [[agentic-ai]], [[llm-evals]], [[agent-observability]]
created: 2026-04-10
updated: 2026-04-10
---

# LLM Wiki: A Pattern for Persistent, Compounding Knowledge Bases
# LLM Wiki: รูปแบบสำหรับฐานความรู้ที่ยั่งยืนและสะสมได้

## Citation / แหล่งอ้างอิง

Andrej Karpathy. GitHub Gist. 2025.
URL: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f

---

## Core Claim
Instead of retrieving raw document chunks at query time (RAG), have the LLM incrementally build and maintain a persistent wiki — a structured, interlinked markdown collection between the user and source materials. The wiki is a compounding artifact: knowledge compiled once, kept current, not re-derived on every query.

## ข้อสรุปหลัก
แทนที่จะดึงชิ้นส่วนเอกสารดิบในเวลาที่ query (RAG) ให้ LLM สร้างและดูแลรักษา wiki ที่ยั่งยืนอย่างต่อเนื่อง — คอลเล็กชัน markdown ที่มีโครงสร้างและเชื่อมโยงกันระหว่างผู้ใช้และเอกสารต้นฉบับ wiki คือสิ่งประดิษฐ์ที่สะสมได้: ความรู้ถูก compile ครั้งเดียวและรักษาให้ทันสมัย ไม่ต้องหาใหม่ทุกครั้งที่ query

---

## Key Contributions

- A clear architectural alternative to RAG for personal and team knowledge management
- Three-layer architecture: raw sources (immutable) → wiki (LLM-owned) → schema (configuration)
- Three core operations: **Ingest**, **Query**, **Lint**
- The role inversion: LLM as writer/maintainer, human as curator/director
- Practical applications across research, reading, teams, and personal knowledge
- Connection to Vannevar Bush's 1945 Memex vision — the LLM solves the maintenance problem Bush couldn't

## ผลงานหลักของบทความ

- ทางเลือกเชิงสถาปัตยกรรมที่ชัดเจนแทน RAG สำหรับการจัดการความรู้ส่วนตัวและทีม
- สถาปัตยกรรมสามชั้น: raw sources (immutable) → wiki (LLM-owned) → schema (configuration)
- สามการดำเนินการหลัก: **Ingest**, **Query**, **Lint**
- การสลับบทบาท: LLM เป็นผู้เขียน/ดูแล มนุษย์เป็นผู้คัดสรร/กำกับทิศทาง
- ความเชื่อมโยงกับ Vannevar Bush's Memex (1945) — LLM แก้ปัญหา maintenance ที่ Bush ทำไม่ได้

---

## The Three-Layer Architecture
## สถาปัตยกรรมสามชั้น

**Layer 1 — Raw Sources / เอกสารต้นฉบับ**
Immutable. The LLM reads but never modifies. Articles, papers, PDFs, transcripts. Source of truth.
Immutable — LLM อ่านแต่ไม่แก้ไข บทความ งานวิจัย PDF บันทึก เป็น source of truth

**Layer 2 — The Wiki / Wiki**
LLM-owned entirely. Summaries, entity pages, concept pages, comparisons, syntheses. The LLM creates, updates, cross-references, and maintains consistency. A single source ingest typically touches 10–15 pages.
LLM เป็นเจ้าของทั้งหมด สรุป หน้า entity หน้า concept การเปรียบเทียบ บทสังเคราะห์ การ ingest แหล่งหนึ่งมักกระทบ 10–15 หน้า

**Layer 3 — The Schema / Schema**
A configuration document (CLAUDE.md, AGENTS.md) that tells the LLM how the wiki is structured, what conventions to follow, and what workflows to run. The schema is co-evolved with the user over time.
เอกสาร configuration ที่บอก LLM ว่า wiki มีโครงสร้างอย่างไร conventions อะไร และ workflow ใดต้องรัน ถูกพัฒนาร่วมกันกับผู้ใช้ตามเวลา

---

## The Three Operations
## สามการดำเนินการ

### Ingest / การนำเข้า
LLM reads source → discusses key takeaways with user → writes summary page → updates index → revises all relevant existing pages → appends to log. The compounding effect: each new source strengthens existing pages rather than sitting in isolation.

LLM อ่านแหล่ง → พูดคุยประเด็นสำคัญกับผู้ใช้ → เขียนหน้าสรุป → อัปเดต index → แก้ไขหน้าที่มีอยู่ทั้งหมดที่เกี่ยวข้อง → เพิ่มใน log ผลสะสม: แหล่งใหม่แต่ละแหล่งเสริมความแข็งแกร่งหน้าที่มีอยู่แทนที่จะอยู่แยกต่างหาก

### Query / การค้นหา
LLM reads index first → identifies relevant pages → reads them → synthesizes answer with citations. Good answers can be filed back as new synthesis pages — explorations compound just like ingested sources.

LLM อ่าน index ก่อน → ระบุหน้าที่เกี่ยวข้อง → อ่าน → สังเคราะห์คำตอบพร้อมการอ้างอิง คำตอบที่ดีสามารถบันทึกเป็นหน้า synthesis ใหม่

### Lint / การตรวจสอบสุขภาพ
Periodic health check: contradictions, orphan pages, missing cross-references, stale claims, data gaps. The LLM also suggests new questions and sources. Keeps the wiki accurate as it grows.

การตรวจสอบสุขภาพเป็นระยะ: ความขัดแย้ง หน้าที่โดดเดี่ยว cross-reference ที่ขาด claim ที่ล้าสมัย ช่องว่างข้อมูล LLM ยังเสนอคำถามและแหล่งข้อมูลใหม่ รักษาความถูกต้องของ wiki เมื่อเติบโต

---

## Why It Works vs. RAG
## ทำไมถึงได้ผลเมื่อเทียบกับ RAG

| Aspect | RAG | LLM Wiki |
|--------|-----|----------|
| Knowledge persistence | Ephemeral — re-derived per query | Persistent — compiled once, kept current |
| Cross-references | Discovered at query time | Pre-built and maintained |
| Contradictions | Not flagged | Explicitly noted on update |
| Maintenance cost | Near-zero (indexing only) | Near-zero (LLM does it) |
| Human effort | Upload documents | Curate sources, direct analysis |
| Scales to | Millions of documents | ~100 sources, hundreds of pages |

The trade-off: LLM Wiki works at "moderate scale" — the index file navigates hundreds of pages without embedding infrastructure. Beyond that, search tooling (like qmd) is recommended.

การแลกเปลี่ยน: LLM Wiki ทำงานได้ดีใน "scale ปานกลาง" — ไฟล์ index นำทางหลายร้อยหน้าโดยไม่ต้องการโครงสร้างพื้นฐาน embedding หากเกินนั้น แนะนำเครื่องมือค้นหา (เช่น qmd)

---

## Connection to Agentic AI
## ความเชื่อมโยงกับ Agentic AI

The ingest and lint operations are **agentic workflows**: the LLM takes a multi-step task (read → analyze → write → update → log), uses tools (file read/write), and produces a persistent artifact. The autonomy level is human-directed (collaborative mode) to fully autonomous (batch mode). This is the same architecture described in [[agentic-ai]], applied to knowledge management rather than business processes.

The lint operation in particular resembles [[llm-evals]]: the LLM inspects its own prior work output, checks for quality issues (contradictions, gaps, orphans), and produces a structured report. It is the wiki's self-evaluation mechanism.

การดำเนินการ ingest และ lint คือ **agentic workflows**: LLM รับงานหลายขั้นตอน (อ่าน → วิเคราะห์ → เขียน → อัปเดต → log) ใช้เครื่องมือ (อ่าน/เขียนไฟล์) และสร้างสิ่งประดิษฐ์ที่ยั่งยืน

การดำเนินการ lint โดยเฉพาะคล้ายกับ [[llm-evals]]: LLM ตรวจสอบ output งานของตัวเอง ตรวจหาปัญหาคุณภาพ (ความขัดแย้ง ช่องว่าง หน้าที่โดดเดี่ยว) และสร้างรายงานที่มีโครงสร้าง มันคือกลไกการประเมินตัวเองของ wiki

---

## My Take / ความเห็นส่วนตัว

**Meta-note**: This gist is the foundational document for the system currently running this wiki. Ingesting it closes a self-referential loop — the wiki now contains a description of itself.

The core insight — LLMs are good at the bookkeeping that humans abandon — is the right explanation for why this works. Human wiki maintenance fails not from lack of interest but from cognitive overhead. The LLM removes that ceiling.

The connection to Bush's Memex is apt. The Memex imagined associative trails as the primary value unit. That's exactly what wikilinks and cross-references provide here — and the LLM maintains them without fatigue.

For this wiki's domain (Software Testing & AI), the pattern is directly applicable: test knowledge, research findings, tool evaluations, and evolving best practices are exactly the kind of content that benefits from a compounding structure rather than flat document storage.

**หมายเหตุ Meta**: gist นี้คือเอกสารพื้นฐานสำหรับระบบที่กำลังรัน wiki นี้อยู่ การ ingest มันทำให้ loop ที่อ้างอิงตัวเองปิด — wiki ตอนนี้มีคำอธิบายของตัวเองแล้ว

ข้อมูลเชิงลึกหลัก — LLM เก่งในการ bookkeeping ที่มนุษย์ละทิ้ง — เป็นคำอธิบายที่ถูกต้องว่าทำไมสิ่งนี้ถึงได้ผล การ maintenance wiki ของมนุษย์ล้มเหลวไม่ใช่จากการขาดความสนใจแต่จากภาระทางการรับรู้

---

## Related / หน้าที่เกี่ยวข้อง
[[agentic-ai]] · [[llm-evals]] · [[agent-observability]]
