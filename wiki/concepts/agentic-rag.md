---
title: Agentic RAG
type: concept
axis: both
tags: [rag, agentic-ai, retrieval, search, grounding, multi-agent]
related: [[agentic-ai]], [[multi-agent-systems]], [[hallucination]], [[llm-evals]], [[google-agents-companion]]
created: 2026-04-12
updated: 2026-04-12
---

# Agentic RAG

## Definition
Agentic Retrieval-Augmented Generation (Agentic RAG) is an evolution of traditional RAG where intelligent agents actively orchestrate the retrieval process — iteratively refining queries, selecting sources, and cross-validating retrieved content — rather than performing a single static lookup.

Traditional RAG: query → vector search → retrieve → generate. One pass.

Agentic RAG: query → agent reasons about retrieval strategy → multiple targeted searches → agent evaluates retrieved content → agent decides if more retrieval is needed → generate grounded answer. Iterative.

## ความหมาย
Agentic RAG คือการวิวัฒนาการของ RAG แบบดั้งเดิม โดย agent อัจฉริยะประสานงานกระบวนการ retrieval อย่างแข็งขัน — ปรับแต่ง query ซ้ำ เลือกแหล่งข้อมูล และตรวจสอบข้าม content ที่ดึงมา แทนที่จะ lookup ครั้งเดียวแบบ static

---

## Why It Matters
Traditional RAG fails on three common query types:
- **Ambiguous queries** — a single vector search may retrieve irrelevant content
- **Multi-step queries** — "what changed between version 2 and 3, and how does that affect the pricing model?" requires sequential, dependent retrievals
- **Multi-perspective queries** — "what are the risks and benefits of X?" benefits from retrieving from multiple source types

These failure modes are the norm in enterprise contexts (legal research, scientific discovery, business intelligence), not the exception. Agentic RAG specifically addresses them. Traditional RAG was designed for simple factual lookup; Agentic RAG is designed for knowledge work.

## ความสำคัญ
RAG แบบดั้งเดิมล้มเหลวกับ query ที่คลุมเครือ, query หลายขั้นตอน, และ query หลายมุมมอง ซึ่งเป็นบรรทัดฐานในบริบทองค์กร (การวิจัยกฎหมาย, การค้นพบทางวิทยาศาสตร์, ธุรกิจ intelligence) Agentic RAG แก้ปัญหาเหล่านี้โดยเฉพาะ

---

## How It Works

Agentic RAG introduces **autonomous retrieval agents** that enhance retrieval through four mechanisms:

### 1. Context-Aware Query Expansion
Instead of one search pass, retrieval agents generate multiple query refinements based on what they learn from initial results. If the first search returns tangential results, the agent reformulates.

### 2. Multi-Step Reasoning
Agents decompose complex queries into smaller logical steps and retrieve information sequentially, where each step builds on the previous. The final response assembles these structured retrievals into a coherent answer.

### 3. Adaptive Source Selection
Rather than always querying a single vector database, retrieval agents dynamically select from multiple knowledge sources based on query context — graph DBs for relationships, relational DBs for structured data, vector DBs for semantic similarity, web search for real-time information.

### 4. Validation and Correction
Evaluator agents cross-check retrieved knowledge for hallucinations and contradictions before integrating it into the final response. This is the RAG equivalent of code review — a second agent checks the first agent's retrieval work.

## วิธีการทำงาน

Agentic RAG แนะนำ **autonomous retrieval agent** ที่ปรับปรุง retrieval ผ่าน 4 กลไก:

1. **Context-Aware Query Expansion** — สร้าง query หลายรูปแบบแทนที่จะ search ครั้งเดียว
2. **Multi-Step Reasoning** — แยกย่อย query ซับซ้อนเป็นขั้นตอนย่อยและ retrieve ตามลำดับ
3. **Adaptive Source Selection** — เลือกแหล่งข้อมูลที่เหมาะสม (graph DB, relational DB, vector DB, web) ตาม context
4. **Validation and Correction** — Evaluator agent ตรวจสอบข้าม content ที่ดึงมาก่อน generate คำตอบ

---

## Comparison to Traditional RAG

| Dimension | Traditional RAG | Agentic RAG |
|-----------|----------------|-------------|
| Retrieval | Single pass | Iterative, multi-pass |
| Query strategy | Fixed | Dynamic, context-adapted |
| Source | Usually one vector DB | Multiple source types |
| Validation | None (or post-generation) | Pre-generation by evaluator agents |
| Complexity | Low | Higher |
| Cost | Low | Higher (multiple LLM calls) |
| Handles ambiguity | Poorly | Well |
| Handles multi-step queries | Poorly | Well |

---

## Better Search = Better RAG

A key practical finding: **improve search quality first, add agents second**. For most RAG implementations, search recall is the binding constraint. Techniques to improve search quality before introducing agents:

- **Parse and chunk** with a layout-aware parser that understands tables, charts, and document hierarchy (semantic chunker with heading hierarchy)
- **Add metadata** to chunks (synonyms, keywords, authors, dates, tags) — enables boost, bury, and filter operations
- **Fine-tune embedding models** or use a search adaptor to make the vector space represent your specific domain better than a general-purpose embedding
- **Use a ranker** — vector search returns dozens of approximate results; a re-ranking model ensures the top few are the most relevant
- **Implement grounding checks** — verify each generated phrase is actually citable by retrieved chunks

The insight: an agentic retrieval wrapper on top of poor search just means the agent burns more compute on bad results.

## การ search ที่ดี = RAG ที่ดี

ข้อค้นพบทางปฏิบัติหลัก: **ปรับปรุงคุณภาพ search ก่อน แล้วค่อยเพิ่ม agent** เทคนิค: แยก chunk ด้วย parser ที่รู้จักโครงสร้างเอกสาร, เพิ่ม metadata ให้ chunk, fine-tune embedding model, ใช้ ranker, implement grounding check

---

## Where It Fits in Multi-Agent Systems

In multi-agent architectures, Agentic RAG is often implemented as dedicated **Retriever Agents** — specialized agents whose only job is knowledge acquisition. The system might have:

- A **Query Planning Agent** that decides what to search for
- Multiple **Retrieval Agents** querying different source types in parallel
- A **Validation Agent** cross-checking results
- A **Synthesis Agent** that generates the final answer from validated, retrieved content

This is the multi-agent specialization principle applied to the retrieval sub-problem.

---

## Use Cases

Particularly valuable in domains where information is constantly evolving and queries are inherently complex:

- **Healthcare**: navigating medical databases, research papers, and patient records simultaneously
- **Legal research**: multi-jurisdiction queries requiring sequential retrieval across statutes, case law, and regulations
- **Scientific discovery**: hypothesis generation requiring synthesis across multiple research areas
- **Business intelligence**: multi-step financial or market analysis where each step depends on the previous

---

## Current State
Active area (2025). The shift from static to agentic RAG is underway in enterprise contexts. Tooling: RAG Engine (Google), LlamaIndex, LangChain RAG pipelines. The "better search before adding agents" principle is not yet widely followed — most teams add retrieval agents on top of poor search infrastructure and are disappointed with results. Agentic RAG evaluation is its own challenge: retrieval accuracy, answer grounding, and hallucination rate all require separate measurement.

## สถานะปัจจุบัน
กำลังพัฒนาอย่างแข็งขัน (ปี 2568) การเปลี่ยนจาก RAG แบบ static สู่ agentic กำลังเกิดขึ้นในบริบทองค์กร หลักการ "ปรับปรุง search ก่อนเพิ่ม agent" ยังไม่แพร่หลาย

---

## Open Questions
- How do you set the stopping criterion for iterative retrieval? Too few passes = incomplete information; too many = prohibitive cost.
- How do you evaluate the retrieval steps of Agentic RAG independently from the final answer quality?
- For very large knowledge bases, does the overhead of agentic retrieval justify the quality gains vs. better-engineered static RAG?

---

## Related
[[agentic-ai]] · [[multi-agent-systems]] · [[hallucination]] · [[llm-evals]]
[[google-agents-companion]] (source)
