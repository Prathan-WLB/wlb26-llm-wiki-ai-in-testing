---
title: Wiki Health Report / รายงานสุขภาพ Wiki
type: meta
created: 2026-04-10
updated: 2026-04-19
---

# Wiki Health Report / รายงานสุขภาพ Wiki

**Scope / ขอบเขต**: 32 files — 16 concepts, 11 summaries, 3 synthesis, 2 papers, 2 meta
**Sources ingested / แหล่งที่มาที่ ingest แล้ว**: 12
**Run date / วันที่รัน**: 2026-04-19

---

## Previous Lint Runs

| Date | Files | Issues Found | Issues Fixed |
|------|-------|-------------|-------------|
| 2026-04-10 | 13 | C1–C4, M1–M6, S1–S4, ST1–ST3 | — |
| 2026-04-19 | 32 | X1–X5 (new), others carried forward | C1 (axis fix confirmed), S3 (stub warning moved to top), X1–X5 (cross-refs added) |

---

## 1. Resolved Issues / ปัญหาที่แก้ไขแล้ว

### ✅ C1 — `agentic-ai.md` axis corrected
`axis: testing-for-ai` → `axis: both`. Confirmed fixed.

### ✅ X1 — `human-role-in-ai-agents.md` missing HITL/XAI cross-refs
Added: `[[automation-bias]]`, `[[explainability]]`, `[[ibm-human-in-the-loop]]`, `[[stanford-hai-humans-in-the-loop-design]]`, `[[mit-sloan-ai-explainability-rubber-stamping]]`, `[[entropy-hitl-systematic-review-2026]]`, `[[contractor-model-and-oracle-problem]]`. Fixed 2026-04-19.

### ✅ X2 — `hallucination.md` missing links to new concepts
Added: `[[automation-bias]]`, `[[explainability]]`. Fixed 2026-04-19.

### ✅ X3 — `llm-evals.md` missing links to new concept pages
Added: `[[rlhf]]`, `[[automation-bias]]`, `[[explainability]]`, `[[interactive-machine-learning]]`. Fixed 2026-04-19.

### ✅ X4 — `contractor-model-and-oracle-problem.md` missing link to `human-role-in-ai-agents`
Added. Fixed 2026-04-19.

### ✅ S3 — `hallucination.md` stub warning at bottom
Stub warning moved to top (below title), visible to readers following inbound links. Fixed 2026-04-19.

---

## 2. Open Issues — HIGH / ปัญหาที่ยังเปิดอยู่ — สูง

### M1 — Oracle Problem has no concept page ⚠️ HIGH
**Mentioned in**: `_index.md` (Key Theme #1), `ai-test-generation.md`, `contractor-model-and-oracle-problem.md`, `llm-evals.md`, `llm-as-judge.md`
**Problem**: The wiki's #1 Key Theme is referenced across 5+ pages but never formally defined. What makes it hard? Why doesn't AI solve it? Where does it appear in each axis? The contractor model page uses it as its central concept but assumes the reader already understands it.
**Fix**: Create `wiki/concepts/oracle-problem.md`

---

## 3. Open Issues — MEDIUM / ปัญหาที่ยังเปิดอยู่ — กลาง

### M2 — `bug-prediction.md` missing ⚠️ MEDIUM
**Mentioned in**: `ais-impact-on-software-testing-qa-evolution.md` (AI capability #3)
**Fix**: Create `wiki/concepts/bug-prediction.md`

### M3 — `visual-testing.md` missing ⚠️ MEDIUM
**Mentioned in**: `ais-impact-on-software-testing-qa-evolution.md` (AI capability #4)
**Fix**: Create `wiki/concepts/visual-testing.md`

### M4 — `rag.md` (basic RAG) missing ⚠️ MEDIUM
**Mentioned in**: `hallucination.md`, `karpathy-llm-wiki-pattern.md`, `llm-evals.md`
**Note**: `agentic-rag.md` exists but the baseline concept is undefined. Agentic RAG extends RAG; readers following links from `hallucination.md` find no grounding page.
**Fix**: Create `wiki/concepts/rag.md` as the base; `agentic-rag.md` links to it as an extension.

### S1 — Wave 1 timeline is past-tense ⚠️ MEDIUM
**File**: `summaries/ais-impact-on-software-testing-qa-evolution.md`
**Claim**: "Wave 1: Now–2026, AI-augmented tester"
**Issue**: Wiki date is April 2026. Wave 1 is ending; Wave 2 (AI orchestrators) should be framed as current. No note acknowledges this.
**Fix**: Add note: *"As of April 2026, Wave 1 is concluding. Wave 2 (AI orchestrator era) is beginning per this framework."*

### S2 — Uncorroborated figures repeat without visible callout ⚠️ MEDIUM
**Files**: `ais-impact-on-software-testing-qa-evolution.md`, `papers/one-year-of-agentic-ai-six-lessons.md`, `_index.md`
**Claims**: 20–30% / 30–40% salary premium (Begunova 2025, uncited); 30–50% test reuse efficiency (McKinsey, uncorroborated)
**Fix**: Add `> **Uncorroborated claim**:` callout inline where each figure appears.

### C3 — `summaries/` directory undocumented in CLAUDE.md ⚠️ MEDIUM
**Problem**: CLAUDE.md defines only `papers/` for article summaries. The `summaries/` directory holds 11 files but has no documented criteria distinguishing it from `papers/`. Future sessions won't know which to use.
**Fix**: Update CLAUDE.md to document both directories and the distinction (e.g., `papers/` = academic/formal research; `summaries/` = practitioner articles, reports, blog posts).

### X5 — `lint-report.md` was an orphan ⚠️ MEDIUM
**Problem**: `lint-report.md` was referenced only in `_log.md` and itself — not in `_index.md`.
**Fix**: Added to `_index.md` under a new "Meta" section. Fixed 2026-04-19. *(Note: update _index.md if not yet done.)*

---

## 4. Open Issues — LOW / ปัญหาที่ยังเปิดอยู่ — ต่ำ

### S4 — `agent-observability.md` tooling list dated ⚠️ LOW
**File**: `concepts/agent-observability.md`
**Issue**: Lists LangSmith, Arize AI, Helicone, Braintrust, Phoenix as the landscape "(2025)". Observability tooling market is consolidating; list may be outdated.
**Fix**: Add staleness note: *"Tooling list current as of late 2025. Verify before acting on this."*

### C2 — Key Theme 6 salary wording loses role-specificity ⚠️ LOW
**File**: `_index.md`
**Issue**: Theme 6 says "20–40% salary premium" — collapses "20–30% for AI-Testing Specialists, 30–40% for Automation Architects" into one range.
**Fix**: Restore the two-figure breakdown with role labels.

### C4 — `type: paper` inconsistently used ⚠️ LOW
**Files**: `summaries/ais-impact-on-software-testing-qa-evolution.md`, `summaries/karpathy-llm-wiki-pattern.md` (both are practitioner content, not peer-reviewed)
**Fix**: Introduce `type: article` for practitioner/industry content; reserve `type: paper` for peer-reviewed research. Update CLAUDE.md convention.

### M5 — `property-based-testing.md` missing ⚠️ LOW
**Mentioned in**: `ai-test-generation.md` (Compared To section)
**Fix**: Create stub or merge a dedicated section into `ai-test-generation.md`.

### M6 — `test-data-generation.md` missing ⚠️ LOW
**Mentioned in**: `ais-impact-on-software-testing-qa-evolution.md`, `ai-test-generation.md`
**Fix**: Create `wiki/concepts/test-data-generation.md` or expand `ai-test-generation.md` with a dedicated section.

---

## 5. Orphan Status / สถานะ Orphan

**None confirmed as of 2026-04-19.**

Inbound link counts (estimated):

| Page | Inbound links |
|------|--------------|
| `[[llm-evals]]` | 13 |
| `[[agentic-ai]]` | 11 |
| `[[automation-bias]]` | 8 |
| `[[explainability]]` | 7 |
| `[[hallucination]]` | 6 |
| `[[llm-as-judge]]` | 6 |
| `[[agent-observability]]` | 6 |
| `[[ai-tool-selection-rubric]]` | 4 |
| `[[interactive-machine-learning]]` | 4 |
| `[[human-role-in-ai-agents]]` | 4 |
| `[[karpathy-llm-wiki-pattern]]` | 2 |
| `[[lint-report.md]]` | 2 |

`[[karpathy-llm-wiki-pattern]]` has the fewest content inbound links (2). At orphan risk as the wiki grows.

---

## 6. Recommended Next Sources / แหล่งที่มาที่แนะนำ

1. **Barr et al. (2015) "The Oracle Problem in Software Testing: A Survey"** — IEEE Transactions on Software Engineering. Grounds Key Theme #1. Would enable creating `oracle-problem.md`.

2. **NIST AI 600-1** — already in `sources/papers/`. Not yet ingested. Covers AI risk, trustworthiness, and governance; would enrich `automation-bias.md`, `explainability.md`, and `human-role-in-ai-agents.md`.

3. **RAGAS framework** — benchmarks for RAG evaluation (faithfulness, answer relevance, context recall). Would ground `hallucination.md` and enable `rag.md`.

4. **World Quality Report 2025 (Sogeti/Capgemini)** — largest annual QA survey. Would corroborate or refute salary premium and Wave timeline claims (S1, S2).

5. **Applitools or Percy documentation** — grounds `visual-testing.md` with concrete tooling.

---

## 7. Priority Fix Summary / สรุปลำดับความสำคัญ

| # | File(s) | Fix | Priority |
|---|---------|-----|----------|
| M1 | *(new)* | Create `wiki/concepts/oracle-problem.md` | HIGH |
| M4 | *(new)* | Create `wiki/concepts/rag.md` | MEDIUM |
| S1 | `summaries/ais-impact-on-software-testing-qa-evolution.md` | Add Wave 1 end note | MEDIUM |
| S2 | Multiple pages | Add uncorroborated claim callouts | MEDIUM |
| C3 | `CLAUDE.md` | Document `summaries/` vs `papers/` | MEDIUM |
| M2 | *(new)* | Create `wiki/concepts/bug-prediction.md` | MEDIUM |
| M3 | *(new)* | Create `wiki/concepts/visual-testing.md` | MEDIUM |
| S4 | `concepts/agent-observability.md` | Add tooling staleness note | LOW |
| C2 | `_index.md` | Restore role-specific salary figures | LOW |
| C4 | Multiple | Introduce `type: article` for practitioner content | LOW |
| M5 | *(new or expand)* | Create `property-based-testing.md` stub | LOW |
| M6 | *(new or expand)* | Create `test-data-generation.md` stub | LOW |
