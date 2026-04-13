---
title: Risk-Based Testing
type: concept
axis: ai-for-testing
tags: [ai-for-testing, risk-based-testing, test-prioritization, defect-prediction, ml]
related: [[ai-test-generation]], [[pairwise-testing]], [[self-healing-tests]], [[agentic-ai]]
created: 2026-04-12
updated: 2026-04-12
---

# Risk-Based Testing

## Definition
A test prioritization strategy that allocates test effort proportionally to the risk of failure and business impact — focusing testing on areas most likely to contain defects or cause significant harm if they do. AI extends this from experience-based judgment to data-driven scoring.

---

## Why It Matters
No project has time to test everything. Risk-Based Testing (RBT) is the principled answer to the coverage problem: not all code is equally risky, not all failures are equally costly. The challenge has always been that risk classification depends on the analyst's domain knowledge and intuition — making it inconsistent across teams and projects.

AI changes this: defect history, code complexity metrics, change frequency, and usage analytics can be fed into ML models that produce objective, reproducible risk scores. Evidence-based RBT replaces gut-feel prioritization.

---

## How It Works

### Traditional RBT
Risk = Likelihood of failure × Impact of failure. Analysts manually classify features/modules on a risk matrix. Highest-risk areas get the deepest testing; lowest-risk areas get smoke tests or are skipped.

### AI-Augmented RBT
Diagnostic ML models analyze:
- **Defect history** — modules with prior defects are statistically more likely to have new ones
- **Code complexity metrics** — cyclomatic complexity, coupling, depth of inheritance correlate with defect density
- **Commit frequency and change volume** — recently changed code is higher risk than stable code
- **Usage analytics** — frequently used paths failing has higher business impact than rarely used ones

Tools like **Tricentis Tosca** (risk-based prioritization) and **SeaLights AI-Driven Test Impact Analysis** implement this in production — identifying which tests are needed based on specific code changes, reducing regression suite size without sacrificing defect detection.

---

## Connection to Test Case Design
In test case design (BVA/EP/Decision Tables), RBT determines *which* techniques are applied at *what depth*:
- High-risk modules → full BVA (3-value), full decision table coverage, pairwise at highest order
- Medium-risk → EP partitions + happy path BVA
- Low-risk → smoke test only

AI automates this triage, assigning a risk score per module that drives technique selection and coverage depth. See [[pairwise-testing]] for how RBT weighting integrates with combinatorial optimization.

---

## Strengths
- Converts subjective risk judgment into objective, reproducible scoring
- Enables regression suite optimization — run only tests relevant to what changed
- Data-driven confidence: risk score is benchmarked against historical defect correlation, not opinion

## Limitations
- Requires historical defect and commit data — new projects have no history to analyze
- Risk scores based on past defects can miss novel failure modes not seen before
- "High historical risk" ≠ "current risk" if the code was refactored or rewritten

---

## Connection to Autonomy Level Selection

Risk scores directly determine the appropriate human oversight level for AI testing decisions — not just test prioritization depth. From [[ai-testing-autonomy-decision-guide]]:

```
Risk Score = Likelihood of Failure (1–3) × Business Impact (1–3)

Score 7–9 (Critical)  → HITL required for AI decisions on this module
Score 4–6 (High)      → HOTL minimum; HITL for production-affecting gates
Score 2–3 (Medium)    → HAbL acceptable with validated AI + monitoring
Score 1   (Low)       → HBtL acceptable for fully automated tasks
```

This extends the RBT model beyond "how much testing to run" to "how much human oversight to require when AI makes testing decisions." A high-risk module does not just need more tests — it needs a human approving AI-generated tests before they enter the official suite.

---

## Current State
Commercially active (2026). SeaLights, Tricentis Tosca, and Inflectra SpiraTest implement AI-driven risk scoring. Integration with CI/CD pipelines (running tests based on what code changed) is the primary production use case. Standalone risk ML models are less common than integrated test impact analysis tools.

---

## Open Questions
- How do you bootstrap RBT for greenfield projects with no defect history?
- Can LLMs infer risk from requirements alone (without historical data), and how reliable is that inference?
- How do you prevent risk scores from calcifying around historically buggy modules that have since been refactored?

---

## Related
[[ai-test-generation]] · [[pairwise-testing]] · [[self-healing-tests]] · [[agentic-ai]]
[[ai-in-software-testing-wlb-2026]] (source — AI-augmented RBT in test case design)
[[ais-impact-on-software-testing-qa-evolution]] (source — AI capabilities taxonomy)
[[ai-testing-autonomy-decision-guide]] (source — risk score → autonomy level formula)
