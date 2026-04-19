# LLM Wiki — Software Testing & AI

A persistent, compounding knowledge base on the intersection of **Software Testing** and **AI/ML**, maintained as an [Obsidian](https://obsidian.md) vault.

---

## Two Axes

| Axis | Focus |
|------|-------|
| **AI for Testing** | Applying AI/ML to improve software testing — LLM-based test generation, self-healing tests, AI-driven fuzzing, autonomous bug detection |
| **Testing for AI** | Evaluating and validating AI/ML systems — LLM evals, benchmarking, hallucination testing, safety and alignment |

---

## Getting Started

1. **Clone the repo**
   ```bash
   git clone git@github.com:Prathan-WLB/wlb26-llm-wiki-ai-in-testing.git
   ```
2. **Open in Obsidian** — "Open folder as vault". Shared `.obsidian/` config is included so everyone gets the same setup.

No build step or dependencies required.

---

## Directory Structure

```
sources/            Raw source material (articles, papers, PDFs). Immutable.
  articles/
  books/
  papers/
  reports/
wiki/
  _index.md         Master index — overview, key themes, all pages by category.
  _log.md           Ingest log — one entry per session.
  concepts/         Core ideas and techniques (16 pages).
  tools/            Tools, frameworks, and libraries.
  papers/           Paper and article summaries (2 pages).
  summaries/        Source summaries (11 pages).
  people/           Key researchers and practitioners.
  companies/        Companies and products.
  synthesis/        Cross-cutting analysis (3 pages).
CLAUDE.md           Project instructions for Claude Code.
commit-message-convention.md  Commit message convention for the team.
```

---

## Current Content

### Concepts
- Agentic AI, Multi-Agent Systems, AgentOps
- LLM Evals, LLM-as-Judge, Hallucination
- AI Test Generation, Self-Healing Tests, Risk-Based Testing, Pairwise Testing
- Agentic RAG, Agent Observability
- Automation Bias, RLHF, Interactive Machine Learning, Explainability

### Papers & Summaries
- Google Agents Companion (2025)
- McKinsey: One Year of Agentic AI — Six Lessons (2025)
- AI's Impact on Software Testing & QA Evolution
- Karpathy LLM Wiki Pattern
- Prompts to Production: Agentic Playbook
- AI in Software Testing: WLB Trend Update & Business Readiness Guide (2026)
- AI in Software Testing: Autonomy Level Decision Guide — WLB (2026)
- EU AI Act Article 14 — Human Oversight Requirements
- IBM: Human-in-the-Loop — HITL/HOTL/HOOTL Taxonomy
- Stanford HAI: Humans in the Loop — Design of Interactive AI Systems
- MIT Sloan: AI Explainability and Rubber-Stamping (2025)
- Entropy: HITL Systematic Review — 134 Studies (2026)

### Synthesis
- AI Tool Selection Rubric
- Contractor Model and the Oracle Problem
- The Role of the Human in AI Agent Systems

---

## Key Themes

1. **The Oracle Problem** — defining "correct behavior" is the hard part in both axes
2. **LLM Test Generation** — most active area; oracle problem resurfaces here
3. **Evals as a Discipline** — LLM evaluation becoming its own engineering field
4. **Agents Change the Testing Problem** — Wave 3 autonomous testing is agentic AI applied to QA
5. **Tool Selection Matters** — AI tool choice determines downstream testing complexity
6. **QA Roles Are Restructuring** — from test executors to quality orchestrators
7. **Explainability Enables Oversight** — human oversight without explainability becomes rubber-stamping; the two are complementary safeguards, not substitutes (MIT Sloan, 77% expert panel)

---

## Workflows

This wiki supports three main workflows via Claude Code:

- **`ingest [source]`** — Process a source, create/update wiki pages, update index and log
- **`ask a question`** — Synthesize an answer from wiki pages with citations
- **`lint`** — Health check for contradictions, orphan pages, missing cross-references

See [`CLAUDE.md`](CLAUDE.md) for full workflow details.

---

## Commit Convention

See [`commit-message-convention.md`](commit-message-convention.md). Format:

```
[Tag]: <summary + file path + details>
```

Tags: `[Created]`, `[Added]`, `[Edited]`, `[Fixed]`, `[Updated]`, `[Deleted]`, `[Config]`

---

## License

Original content is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). Third-party materials in `sources/` remain under their respective authors' copyright.