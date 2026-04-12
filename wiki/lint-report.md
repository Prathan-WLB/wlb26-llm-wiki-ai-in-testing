---
title: Wiki Health Report / รายงานสุขภาพ Wiki
type: meta
created: 2026-04-10
updated: 2026-04-10
---

# Wiki Health Report / รายงานสุขภาพ Wiki

**Scope / ขอบเขต**: 13 files — 7 concepts, 1 paper, 2 summaries, 1 synthesis, `_index.md`, `_log.md`
**Sources ingested / แหล่งที่มาที่ ingest แล้ว**: 3
**Run date / วันที่รัน**: 2026-04-10

---

## 1. Contradictions / ความขัดแย้ง

### C1 — `agentic-ai.md` axis mismatch ⚠️ HIGH
**File**: `wiki/concepts/agentic-ai.md` frontmatter: `axis: testing-for-ai`
**Problem**: The page now covers both axes. It contains a dedicated "Connection to AI for Testing" section, links to `[[ai-test-generation]]` and `[[self-healing-tests]]`, and the Wave 3 autonomous testing connection. The `testing-for-ai` axis tag is wrong.
**Fix**: Change frontmatter to `axis: both`

---

### C2 — Salary premium range is inconsistently presented ⚠️ LOW
**Files**: `wiki/summaries/ais-impact-on-software-testing-qa-evolution.md` vs `wiki/_index.md`
**Problem**: The summary page correctly states "20–30% premium for AI-Testing Specialists, 30–40% for AI-savvy Architects" (two separate figures). The index Key Theme 6 collapses these into "20–40% salary premium" — technically correct but loses the role-specific distinction.
**Fix**: Update Key Theme 6 in `_index.md` to: "20–30% premium for AI-Testing Specialists, 30–40% for Automation Architects with AI expertise (Begunova 2025, uncited)"

---

### C3 — `summaries/` directory is undocumented in schema ⚠️ MEDIUM
**Files**: `CLAUDE.md` (schema) vs actual directory structure
**Problem**: `CLAUDE.md` defines `papers/` for article summaries. The `summaries/` directory was created at user request but the schema was never updated. Future sessions won't know the difference between `papers/` and `summaries/`, or which one to use.
**Fix**: Update `CLAUDE.md` to document `summaries/` as a directory for shorter practitioner articles and blog posts, reserving `papers/` for academic/formal research. Or collapse them back into one directory — document the decision either way.

---

### C4 — `type: paper` used in `summaries/` directory ⚠️ LOW
**Files**: `wiki/summaries/ais-impact-on-software-testing-qa-evolution.md`, `wiki/summaries/karpathy-llm-wiki-pattern.md`
**Problem**: Both summaries files have `type: paper` in frontmatter, but they are practitioner blog posts / gists, not academic papers. The McKinsey piece in `papers/` is also a practitioner article — so the type label is used inconsistently and doesn't reflect actual source type.
**Fix**: Introduce `type: article` for practitioner/industry content, reserve `type: paper` for peer-reviewed research. Update CLAUDE.md frontmatter convention accordingly.

---

## 2. Orphan Pages / หน้าที่โดดเดี่ยว

**None found / ไม่พบ** — all content pages have ≥2 inbound wikilinks from other pages.

Inbound link counts for reference:
| Page | Inbound links |
|------|--------------|
| `[[llm-evals]]` | 12 |
| `[[agentic-ai]]` | 10 |
| `[[one-year-of-agentic-ai-six-lessons]]` | 7 |
| `[[agent-observability]]` | 6 |
| `[[hallucination]]` | 5 |
| `[[llm-as-judge]]` | 5 |
| `[[ai-tool-selection-rubric]]` | 3 |
| `[[ai-test-generation]]` | 4 |
| `[[self-healing-tests]]` | 4 |
| `[[ais-impact-on-software-testing-qa-evolution]]` | 4 |
| `[[karpathy-llm-wiki-pattern]]` | 2 |

`[[karpathy-llm-wiki-pattern]]` has the fewest inbound links (2) and is at orphan risk as the wiki grows.

---

## 3. Concepts Mentioned Without a Dedicated Page / แนวคิดที่กล่าวถึงแต่ไม่มีหน้าของตัวเอง

### M1 — Oracle Problem ⚠️ HIGH
**Mentioned in**: `_index.md` Key Theme #1, `wiki/concepts/ai-test-generation.md` ("The oracle problem" appears in Limitations), `wiki/synthesis/ai-tool-selection-rubric.md` (implicitly)
**Why it needs a page**: It is the #1 Key Theme for the entire wiki. It appears on both axes. Defining it precisely — what makes it hard, how different approaches address it, whether AI changes it — is foundational to the wiki's thesis. Currently it's invoked but never explained.
**Suggested page**: `wiki/concepts/oracle-problem.md`

---

### M2 — Bug Prediction ⚠️ MEDIUM
**Mentioned in**: `wiki/summaries/ais-impact-on-software-testing-qa-evolution.md` (AI capability #3: "ML models identifying high-risk code changes")
**Why it needs a page**: It is one of the 5 named AI capabilities reshaping testing in the Begunova article. It is distinct from test generation (predicts where bugs are before running tests) and from evals (evaluates model outputs). Predictive defect localization is an active research area.
**Suggested page**: `wiki/concepts/bug-prediction.md`

---

### M3 — Visual Testing ⚠️ MEDIUM
**Mentioned in**: `wiki/summaries/ais-impact-on-software-testing-qa-evolution.md` (AI capability #4: "computer vision detecting layout regressions and accessibility issues")
**Why it needs a page**: Named as a distinct AI capability. Computer vision-based visual regression testing (Applitools, Percy, etc.) is a real, commercially mature category. Not covered by self-healing-tests or ai-test-generation.
**Suggested page**: `wiki/concepts/visual-testing.md`

---

### M4 — RAG (Retrieval-Augmented Generation) ⚠️ MEDIUM
**Mentioned in**: `wiki/summaries/karpathy-llm-wiki-pattern.md` (compared to LLM Wiki), `wiki/concepts/llm-evals.md` (Retrieval Accuracy type), `wiki/concepts/hallucination.md` ("RAG reduces hallucination")
**Why it needs a page**: Referenced across 3 pages as a baseline or comparison point. It is the dominant architecture for grounding LLMs in external knowledge, relevant to both axes: RAG systems need evals (retrieval accuracy, faithfulness), and RAG is a tool for AI-in-testing systems.
**Suggested page**: `wiki/concepts/rag.md`

---

### M5 — Property-Based Testing ⚠️ LOW
**Mentioned in**: `wiki/concepts/ai-test-generation.md` (Compared To: "classic technique for automated test case generation, but rule-based")
**Why it needs a page**: Mentioned as the pre-AI baseline for automated test case generation. Understanding it clarifies what AI test generation actually adds. Also connects to fuzz testing and Hypothesis/QuickCheck tools.
**Suggested page**: `wiki/concepts/property-based-testing.md`

---

### M6 — Test Data Generation ⚠️ LOW
**Mentioned in**: `wiki/summaries/ais-impact-on-software-testing-qa-evolution.md` (AI capability #5), `wiki/concepts/ai-test-generation.md` ("From OpenAPI / schemas: AI generates API test suites")
**Why it needs a page**: Partially covered in `ai-test-generation.md` but is distinct — generating realistic test data (PII-safe synthetic data, edge-case datasets) is a separate problem from generating test logic. Tools like Faker, Gretel, and Mostly AI address this specifically.
**Suggested page**: `wiki/concepts/test-data-generation.md` (or merge into `ai-test-generation.md` with a dedicated section)

---

## 4. Stale or Weakly-Supported Claims / claim ที่อาจล้าสมัยหรืออ่อนแอ

### S1 — Wave 1 end date has passed ⚠️ MEDIUM
**File**: `wiki/summaries/ais-impact-on-software-testing-qa-evolution.md`
**Claim**: "Wave 1: Now–2026, AI-augmented tester"
**Issue**: The wiki was created April 2026. Wave 1 ("Now–2026") is ending or has ended by the wiki's own date. Wave 2 (2026–2030: AI orchestrators) should now be the current wave. The summary page presents Wave 1 as current without noting this.
**Fix**: Add a note: *"As of 2026, Wave 1 is concluding. Wave 2 (AI orchestrator era) is beginning per this framework — worth tracking whether this prediction is materializing."*

---

### S2 — Salary premium figures are uncorroborated across two sources ⚠️ MEDIUM
**Files**: `wiki/summaries/ais-impact-on-software-testing-qa-evolution.md`, `wiki/papers/one-year-of-agentic-ai-six-lessons.md`
**Claims**: Begunova: 20–30% / 30–40% salary premiums. McKinsey: 30–50% reuse efficiency.
**Issue**: Both papers flag these as uncited. They are repeated across the wiki as if established. The log notes this correctly, but the pages themselves don't flag the weakness prominently enough.
**Fix**: Add a `> **Uncorroborated claim**:` callout to each figure in the pages where it appears. Consider tracking whether Stack Overflow or LinkedIn surveys validate these numbers as future sources.

---

### S3 — `hallucination.md` marked as stub but linked as authoritative ⚠️ LOW
**File**: `wiki/concepts/hallucination.md`
**Issue**: The page is marked "*Stub — expand as more sources are ingested*" at the bottom, but it is cited as a reference from 5 other pages. The stub warning is at the very end, invisible to readers following a link. Key missing content: specific detection tooling, faithfulness scoring frameworks (RAGAS), and the open debate about whether hallucination is irreducible.
**Fix**: Move the stub warning to the top of the page (just below the title) so incoming readers see it. Prioritize expanding this page on next ingest.

---

### S4 — `agent-observability.md` tooling list may be outdated ⚠️ LOW
**File**: `wiki/concepts/agent-observability.md`
**Claim**: Lists LangSmith, Arize AI, Helicone, Braintrust, Phoenix as the tooling landscape "(2025)"
**Issue**: The observability tooling market is consolidating rapidly. By April 2026, significant M&A or new entrants may have changed this list. No sources after September 2025 exist in this wiki.
**Fix**: Mark the tools section with a staleness warning: *"Tooling list current as of Sep 2025. Verify before acting on this."*

---

## 5. Structural Issues / ปัญหาโครงสร้าง

### ST1 — `papers/` vs `summaries/` categorization is inconsistent
The McKinsey article (a practitioner consulting report) is in `papers/`, while two similar practitioner sources (a Medium blog post, a GitHub gist) are in `summaries/`. The distinction is unclear and not documented in `CLAUDE.md`. Recommend: document the distinction or consolidate.

### ST2 — `_index.md` has both "Papers & Articles" and "Summaries" sections with no stated difference
These two sections should be either merged or given clear, documented criteria for which sources go where.

### ST3 — `_log.md` page_count in the second ingest entry is wrong
The log entry for the QA evolution ingest says `page_count: 10, source_count: 2` but the Karpathy ingest that follows updated it to `page_count: 11, source_count: 3`. The intermediate values in the log are accurate snapshots — this is fine. But the `_index.md` frontmatter `page_count` should be updated to `13` (current total) from `11`, since `lint-report.md` now exists.

---

## 6. Recommended Next Sources / แหล่งที่มาที่แนะนำ

Based on gaps found above:

1. **A paper or post on the Oracle Problem in software testing** — the wiki's #1 Key Theme has no dedicated page and no source grounding it. Search for: "oracle problem software testing" or Weyuker (1982) original paper.

2. **A source on LLM hallucination measurement** — `hallucination.md` is a stub. Candidates: the RAGAS framework paper, "TruthfulQA" benchmark paper, or recent Anthropic/OpenAI technical reports on factuality.

3. **An industry survey on AI tool adoption in QA** — would corroborate or refute the salary premium and Wave timeline claims (S1, S2). Stack Overflow Developer Survey 2025 or the World Quality Report by Sogeti are good candidates.

4. **A source on RAG** — needed to create the `rag.md` concept page (M4). Candidates: the original RAG paper (Lewis et al., 2020) or a practitioner explainer.

5. **A source on Visual Testing tools** — Applitools blog or Percy documentation would ground `visual-testing.md` (M3).

---

## Priority Fix Summary / สรุปการแก้ไขที่มีลำดับความสำคัญ

| # | File(s) | Fix | Priority |
|---|---------|-----|----------|
| C1 | `concepts/agentic-ai.md` | Change `axis: testing-for-ai` → `axis: both` | HIGH |
| M1 | *(new file)* | Create `wiki/concepts/oracle-problem.md` | HIGH |
| C3 | `CLAUDE.md` | Document `summaries/` directory and difference from `papers/` | MEDIUM |
| M2 | *(new file)* | Create `wiki/concepts/bug-prediction.md` | MEDIUM |
| M3 | *(new file)* | Create `wiki/concepts/visual-testing.md` | MEDIUM |
| M4 | *(new file)* | Create `wiki/concepts/rag.md` | MEDIUM |
| S1 | `summaries/ais-impact-on-software-testing-qa-evolution.md` | Add note that Wave 1 is ending as of 2026 | MEDIUM |
| S2 | Multiple pages | Add `> **Uncorroborated claim**:` callouts to salary/reuse figures | MEDIUM |
| S3 | `concepts/hallucination.md` | Move stub warning to top; expand page | LOW |
| S4 | `concepts/agent-observability.md` | Add staleness warning to tooling list | LOW |
| C2 | `_index.md` | Refine Key Theme 6 salary range wording | LOW |
| C4 | `summaries/*.md` | Introduce `type: article` vs `type: paper` distinction | LOW |
| ST2 | `_index.md`, `CLAUDE.md` | Clarify or merge Papers & Articles vs Summaries | LOW |
