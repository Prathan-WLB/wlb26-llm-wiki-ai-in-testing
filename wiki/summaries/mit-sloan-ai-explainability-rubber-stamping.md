---
title: "AI Explainability: How to Avoid Rubber-Stamping Recommendations — MIT Sloan"
type: paper
axis: both
tags: [explainability, xai, human-oversight, automation-bias, rubber-stamping, accountability, eu-ai-act, human-in-the-loop]
related: [[automation-bias]], [[explainability]], [[eu-ai-act-article-14-human-oversight]], [[ibm-human-in-the-loop]], [[llm-as-judge]], [[interactive-machine-learning]]
created: 2026-04-19
updated: 2026-04-19
---

# AI Explainability: How to Avoid Rubber-Stamping Recommendations — MIT Sloan

**Source**: MIT Sloan Management Review, June 12, 2025
**URL**: https://sloanreview.mit.edu/article/ai-explainability-how-to-avoid-rubber-stamping-recommendations/
**Authors**: Elizabeth M. Renieris, David Kiron, Steven Mills, Anne Kleppe
**Research Partner**: Boston Consulting Group (BCG)
**Method**: 30-person international expert panel + global executive survey (n=1,221; organizations >$100M revenue)

---

## The Research Question

Does effective human oversight reduce the need for AI explainability? Or do explainability and oversight serve distinct, non-substitutable functions?

The provocation was put to the expert panel directly. The answer was unambiguous.

---

## The Central Finding

**77% of panelists disagreed or strongly disagreed** that human oversight diminishes explainability requirements:

| Response | % |
|----------|---|
| Strongly disagree | 37% |
| Disagree | 40% |
| Neither agree nor disagree | 20% |
| Agree | 0% |
| Strongly agree | 3% |

The consensus: explainability and human oversight are **complementary, not competing, safeguards**. They constitute "complementary and intersecting" accountability mechanisms — each necessary, neither sufficient alone.

---

## Why Oversight Without Explainability Fails: The Rubber-Stamping Mechanism

The article's core mechanism is explicit. Without explainability:

> "Opacity over time can encourage a rubber-stamping role for any human only notionally 'in the loop.'"

Without insight into AI reasoning, oversight becomes "superficial and reactive rather than proactive and corrective." The human approves what the system proposes — not because they evaluated it, but because they cannot evaluate it.

This is the **rubber-stamping failure mode**: formal oversight structures that produce a **"dangerous illusion of control"** — comfort without substantive accountability. The human is structurally in the loop but functionally a stamp.

The connection to [[automation-bias]] is direct: opacity is the *enabler* of automation bias. Wang's BRB critique ([[stanford-hai-humans-in-the-loop-design]]) identified black-box output as structurally causing passive acceptance; this article names the long-run organizational consequence: rubber-stamping becomes the norm.

---

## Distinct Functions: Why Both Are Required

**Human oversight** addresses:
- Ensuring system accuracy
- Preventing unforeseen risks
- Maintaining alignment with organizational values
- Enabling intervention and control (the EU AI Act's five capabilities)

**Explainability** enables:
- Understanding *why* the AI reached a specific conclusion
- Identifying and correcting biases
- Supporting regulatory compliance
- Substantive (not formal) accountability

These are different functions. A system can have oversight mechanisms (override button, monitoring dashboard) while remaining entirely opaque — the oversight is real but the overseer cannot exercise informed judgment. As one panelist states: "If the person overseeing the system doesn't understand how the AI is making decisions, it becomes much harder to guide or adjust it in the right way."

Healthcare example: a doctor should not accept a diagnosis from an AI system without understanding the reason, given error-proneness concerns. The oversight capability (override) exists; it cannot be meaningfully exercised without explainability.

---

## Explainability Theater: The Symmetrical Failure

The article introduces a critical counter-risk: **"explainability theater"** — performative explanations that lack substance. Feature importance heat maps, confidence percentages, and boilerplate reasoning templates can all satisfy a formal explainability requirement while providing no genuine insight into system behavior.

Explainability theater is dangerous precisely because it provides false confidence. One panelist advocates for "empirical audits and human override authority over 'today's often performative explainable AI heat maps.'"

The practical implication: explainability should be tested for whether it actually enables overseer understanding — not merely for whether it exists. This aligns with MIT Sloan Recommendation #4 (Ensure Meaningful Accountability): test whether explainability and oversight "actually drive understanding and accountability in practice."

---

## Practical Limitations

Panelists acknowledge genuine constraints:

- **Complexity trade-offs**: transparency sometimes conflicts with system performance
- **Technical feasibility**: "Modern AI systems have become way too complex for us to cling to this type of explainability"
- **Context-dependency**: requirements should be tailored to use case, stakeholder, and purpose — what to explain, to whom, and for what

David Hardoon (Standard Chartered Bank): the right question is "what needs to be explained, to whom, and for what purpose" — not "is there an explanation?"

---

## Organizational Implementation: Survey Data

What organizations are actually doing (n=1,221; multiple selections permitted):

| Practice | % Adoption |
|----------|-----------|
| Educate users on system strengths, limitations, risks | 54% |
| Establish clear HITL vs. HOOTL criteria | 36% |
| Design systems to provide supporting/opposing evidence | 34% |
| Implement concern-reporting mechanisms | 34% |
| Implement reviewer quality control | 30% |
| Assess incorrect-output flagging rates | 28% |
| Define minimum reviewer qualifications | 20% |

User education leads (54%) — but only one in three organizations design systems to produce evidence supporting or opposing outputs (34%), and only one in five define minimum reviewer qualifications (20%). The gap between education and structural design is notable.

---

## Four Strategic Recommendations

### 1. Design Systems for Human Oversight
Auditable evidence trails, detailed change logs, flagging for escalation, contextual confidence indicators. The system should surface *why* it reached its output, not just *what* the output is.

### 2. Cultivate Human Oversight Competencies
Technical content expertise alone is insufficient. Users require: AI fundamentals, system-specific operation, and understanding of limitations, biases, and failure modes. Knowing a system exists ≠ knowing when to doubt it.

### 3. Address Multiple Explainability Types
Explanation depth requirements vary by context. Some decisions (counterintuitive medical diagnoses) always require explanation review. Others (inventory management) may require less frequent review. Organizations should map which scenarios demand transparency — context-dependent explainability policy, not one-size-fits-all.

### 4. Ensure Meaningful Accountability
Test whether explainability and oversight actually produce understanding and accountability — not just whether they formally exist. Adjust approaches to match contextual realities. Avoid both: (a) opacity that enables rubber-stamping, and (b) explainability theater that provides false confidence.

---

## Regulatory Context

- **EU AI Act Art. 14(4)(c)**: High-risk AI systems must enable overseers to "correctly interpret" output — implicitly requiring explainability at a standard a human can act on. See [[eu-ai-act-article-14-human-oversight]].
- **EU AI Act Art. 13**: Separate transparency obligation — individuals must receive "clear and meaningful explanations" of decisions affecting them.
- **South Korea's AI Law**: High-impact systems (healthcare, energy, public services) must explain decision reasoning.
- **Explainability market projection**: $16.2 billion by 2028.

---

## What This Adds to the Wiki

| MIT Sloan Insight | Wiki Connection | What Changes |
|------------------|----------------|-------------|
| Explainability + oversight are complementary, not competing | [[automation-bias]] | Explainability is the upstream enabler of effective oversight — opacity is the root cause of rubber-stamping |
| Rubber-stamping = oversight without explainability | [[automation-bias]] | Concrete mechanism: opacity → passive acceptance → formal-but-hollow oversight |
| "Explainability theater" | [[explainability]] | Performative explanations can be as dangerous as opacity — false confidence is its own failure mode |
| Context-dependent explainability | [[explainability]] | What to explain, to whom, for what purpose — not binary explain/don't |
| Art. 14(4)(c) interpretability standard | [[eu-ai-act-article-14-human-oversight]] | MIT Sloan empirically supports the regulatory requirement: unintelligible output makes oversight hollow |
| 54% educate users; only 34% design for evidence | [[ibm-human-in-the-loop]] | The gap: education ≠ structural design; HITL requires both |

---

## Related
[[automation-bias]] · [[explainability]] · [[eu-ai-act-article-14-human-oversight]] · [[ibm-human-in-the-loop]] · [[stanford-hai-humans-in-the-loop-design]] · [[llm-as-judge]] · [[interactive-machine-learning]]
