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
   git clone git@github.com:Prathan-WLB/llm-wiki-ai-in-testing.git
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
  concepts/         Core ideas and techniques (10 pages).
  tools/            Tools, frameworks, and libraries.
  papers/           Paper and article summaries (2 pages).
  summaries/        Source summaries (4 pages).
  people/           Key researchers and practitioners.
  companies/        Companies and products.
  synthesis/        Cross-cutting analysis (2 pages).
CLAUDE.md           Project instructions for Claude Code.
commit-message-convention.md  Commit message convention for the team.
```

---

## Current Content

### Concepts
- Agentic AI, Multi-Agent Systems, AgentOps
- LLM Evals, LLM-as-Judge, Hallucination
- AI Test Generation, Self-Healing Tests
- Agentic RAG, Agent Observability

### Papers & Summaries
- Google Agents Companion (2025)
- McKinsey: One Year of Agentic AI — Six Lessons (2025)
- AI's Impact on Software Testing & QA Evolution
- Karpathy LLM Wiki Pattern
- Prompts to Production: Agentic Playbook

### Synthesis
- AI Tool Selection Rubric
- Contractor Model and the Oracle Problem

---

## Key Themes

1. **The Oracle Problem** — defining "correct behavior" is the hard part in both axes
2. **LLM Test Generation** — most active area; oracle problem resurfaces here
3. **Evals as a Discipline** — LLM evaluation becoming its own engineering field
4. **Agents Change the Testing Problem** — Wave 3 autonomous testing is agentic AI applied to QA
5. **Tool Selection Matters** — AI tool choice determines downstream testing complexity
6. **QA Roles Are Restructuring** — from test executors to quality orchestrators

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

Internal use.