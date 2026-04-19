---
title: "Human-in-the-Loop AI: A Systematic Review of Concepts, Methods, and Applications — Entropy 2026"
type: paper
axis: both
tags: [human-in-the-loop, hitl, systematic-review, taxonomy, trust-calibration, interactive-machine-learning, rlhf, active-learning, explainability, automation-bias, agentic-ai]
related: [[automation-bias]], [[interactive-machine-learning]], [[rlhf]], [[explainability]], [[ibm-human-in-the-loop]], [[agentic-ai]], [[eu-ai-act-article-14-human-oversight]], [[llm-evals]]
created: 2026-04-19
updated: 2026-04-19
---

# Human-in-the-Loop AI: A Systematic Review of Concepts, Methods, and Applications — Entropy 2026

**Citation**: Lazaros, K.; Vrahatis, A.G.; Kotsiantis, S. Human-in-the-Loop Artificial Intelligence: A Systematic Review of Concepts, Methods, and Applications. *Entropy* 2026, 28, 377.
**DOI**: https://doi.org/10.3390/e28040377
**Published**: 26 March 2026. Open access (CC BY).
**Affiliation**: Ionian University (Corfu); University of Patras (Greece)
**Method**: PRISMA-aligned systematic review. 380 records identified → 134 studies in structured synthesis. Scopus + Google Scholar; January 2018–January 2026.

---

## Why This Paper Matters for the Wiki

The IBM Think article ([[ibm-human-in-the-loop]]) gave us a 3-level taxonomy (HITL/HOTL/HOOTL). Wang's Stanford HAI article ([[stanford-hai-humans-in-the-loop-design]]) gave us design philosophy. This paper is the field-wide synthesis: a 50-page systematic review that consolidates HITL theory, methods, applications, trust calibration, and governance into a unified framework — then explicitly identifies what remains open. It is the most comprehensive single HITL reference currently in the wiki.

---

## The Core Contribution: A Unified 3D Taxonomy

The paper's central contribution is a **three-dimensional taxonomy** for comparing HITL systems that previously resisted direct comparison because they used the same label ("human-in-the-loop") for very different operational realities:

| Dimension | What it captures | Practical impact |
|-----------|-----------------|-----------------|
| **Loop placement** | Where human authority is positioned (In / On / Over / Under / Along) | Determines oversight level and accountability structure |
| **Interaction granularity** | Level of detail of human input (coarse / medium / fine) | Determines annotation cost, cognitive load, latency |
| **Temporal characteristics** | Rate of human input (synchronous/asynchronous; continuous/episodic) | Determines feasibility at deployment scale |

The critical insight: **systems with the same loop placement label can have entirely different operational profiles** depending on granularity and temporal characteristics. HOTL monitoring with continuous fine-grained input is a fundamentally different system from HOTL monitoring with episodic coarse-grained audits — but both call themselves "human-on-the-loop."

---

## Five Loop Configurations (Extends IBM's 3-Level Taxonomy)

IBM's HITL/HOTL/HOOTL taxonomy (3 levels) is extended to five configurations (Singh & Szajnfarber framework, synthesized here):

| Configuration | Human Role | AI Role | Authority | Example Context |
|--------------|-----------|---------|-----------|----------------|
| **In-the-Loop** | Direct participation in every decision | Supports human decision-making | Human decides | Medical diagnosis, legal decisions |
| **On-the-Loop** | Monitors, intervenes when necessary | Operates autonomously under supervision | Shared control | Drone surveillance, automated trading |
| **Over-the-Loop** | Defines objectives, constraints, policies | Executes within predefined bounds | Human strategic | Policy systems, organizational AI |
| **Under-the-Loop** | Executes final action based on AI input | Provides guidance and decision support | AI advisory | Clinical decision support, recommendations |
| **Along-the-Loop** | Parallel collaboration on related tasks | Parallel collaboration with coordination | Lateral coordination | Co-creation, collaborative design |

> **Note for wiki**: **Under-the-Loop** and **Along-the-Loop** are new configurations not captured in IBM's taxonomy or the [[agentic-ai]] autonomy level framework. Under-the-Loop captures systems where AI is the dominant reasoner and human is the executor — a common pattern in AI-assisted decision support that is neither "in the loop" (too much AI autonomy) nor "on the loop" (not monitoring a fully autonomous system). Along-the-Loop captures collaborative co-creation patterns where human and AI work in parallel as peers.

---

## Seven HITL Method Families (Table 1)

The paper consolidates HITL techniques into seven method families with required inputs, costs, risks, and **common failure modes** — the most operationally useful table in the paper:

| Method Family | Typical Cost | Key Risks | Common Failure Modes |
|--------------|-------------|-----------|---------------------|
| **Active learning** | Medium–high | Sampling bias, annotator fatigue, privacy exposure | Myopic query strategy; query/deployment distribution mismatch; overfitting to ambiguous cases |
| **RLHF / preference optimization** | High | Reward hacking, norm/preference drift, inconsistent rater judgments | Optimization to proxy signals; truthfulness/helpfulness degradation from over-optimization; **collapse to overly safe but uninformative outputs** |
| **Interactive ML / human-guided model steering** | Medium–high | Cognitive overload, confirmation bias, inconsistent operator corrections | Non-stationary guidance; oscillatory updates; local patches that degrade global performance |
| **HITL data curation / labeling pipelines** | Medium–high | Guideline-encoded bias, low inter-annotator agreement, sensitive-info leakage | Label inconsistency/shortcutting; silent label noise; dataset shift as annotation policy evolves |
| **Disagreement-aware label aggregation** | Medium | False consensus from majority voting, minority-view suppression | Overconfident hard labels for ambiguous items; escalation bottlenecks; persistent disagreement loops |
| **Post-hoc human validation / escalation (HOTL)** | Low–medium | **Automation bias / rubber-stamping**, throughput bottlenecks, ambiguous accountability | High-risk misses under time pressure; inconsistent overrides; **alert fatigue and threshold miscalibration** |
| **Human-guided prompt workflows for generative AI** | Low–medium | Prompt injection, hallucinations, brittle prompt behavior, confidentiality leakage | Plausible but incorrect outputs; poor reproducibility; failure under adversarial inputs |

Two failure modes deserve special attention:
- **Post-hoc HOTL**: automation bias / rubber-stamping is explicitly listed as a *primary risk* of human-on-the-loop systems — formal oversight without substantive evaluation. Confirms [[mit-sloan-ai-explainability-rubber-stamping]]'s empirical finding at the method-taxonomy level.
- **RLHF collapse**: over-optimization against the reward model can produce outputs that are safe but uninformative — a failure mode distinct from reward hacking.

---

## Application Domain Map (Table 2 / Figure 4)

| Domain | Typical Loop | Primary Challenge | Common Pitfall |
|--------|-------------|------------------|---------------|
| **Healthcare** | In-the-Loop | Accountability | Over-trust and weak workflow integration |
| **Autonomous systems** | On-the-Loop | Real-time | Delayed takeover/handover failure |
| **Cybersecurity** | Along-the-Loop | Scalability | Alert fatigue; adversarial adaptation |
| **Finance** | Over-the-Loop | Compliance | Bias amplification; explanation mismatch; incentive gaming |
| **Education** | In-the-Loop | Fairness | Instructor inconsistency; institutional bias |
| **Manufacturing** | On-the-Loop | Efficiency | Inconsistent labels/inspection shortcuts |

**Healthcare-specific finding (Section 5.1)**: System deployment failure is often caused by *workflow incompatibility*, not model inaccuracy. Uncompensated verification demands on clinicians under time pressure cause reversion to rubber-stamping or bypass of the system entirely. Workflow integration is the primary determinant of whether healthcare HITL delivers real-world benefit — more than model performance. This finding directly supports IBM's "HITL creates opportunity, not guarantee" caveat.

**Finance-specific finding (Section 5.4)**: Human override layers contribute to fairness only in combination with decision rationales, explainability for adverse actions, and monitoring for disparate impact across protected groups. Without these, human checks function as "a buffer for liabilities while patterns of biased decision processes persist."

---

## Trust Calibration Model (Figure 5)

The paper introduces a three-zone trust calibration model — the most useful single framework for designing effective oversight:

```
Over-Trust Zone          →    Well-Calibrated Zone    →    Under-Trust Zone
─────────────────────         ────────────────────         ────────────────
• Automation bias             • Appropriate reliance        • AI dismissal
• Uncritical acceptance       • Context-aware trust         • Excessive skepticism
• Complacency                 • Adaptive behavior           • Missed benefits
• Skill degradation           • Effective oversight         • Inefficient workflows
        ↓                             ↑                             ↓
Risk: Accepting AI                 GOAL: Trust level          Risk: Rejecting
errors uncritically                matches AI reliability     valid AI output
```

**Calibration Interventions** (to move toward the well-calibrated zone):
1. **Training & Education** — teach AI fundamentals, failure modes, context
2. **XAI & Transparency** — make AI reasoning visible so trust is informed
3. **Confidence Display** — surface uncertainty alongside outputs
4. **Feedback Mechanisms** — enable humans to observe where AI is wrong
5. **Error Awareness** — actively expose overseers to system limitations

The model clarifies that [[automation-bias]] (over-trust) and under-trust are **symmetrical failure modes**. Over-trust accepts AI errors uncritically; under-trust rejects valid AI outputs and loses the efficiency benefits. The design goal is calibration — trust that matches actual AI reliability, which requires continuous calibration mechanisms, not a one-time training event.

**Skill degradation** appears explicitly as an over-trust characteristic. Extended use of AI systems that handle difficult cases reduces practitioner skill at those cases — eroding the very human capability the system was designed to augment. This is the deskilling risk: the long-term erosion of human expertise through AI-mediated work.

---

## Five-Dimension HITL Evaluation Framework (Section 6.3)

Evaluation of HITL systems requires measuring performance as a **joint property of humans, AI models, interfaces, and organizational context** — not model accuracy alone. Five dimensions:

| Dimension | Key Metrics |
|-----------|------------|
| **Task effectiveness** | Error rate, calibration quality scores, throughput, time-to-decision |
| **Human factors** | Workload, trust calibration, acceptance, **skill retention** |
| **Interaction process quality** | Intervention timing, override frequency, disagreement resolution rate, unnecessary vs. missed interventions |
| **Safety / fairness / governance** | Subgroup disparities, auditability, explanation adequacy, accountability traceability |
| **Lifecycle robustness** | Drift sensitivity, adaptation effects, collaboration stability after extended use |

**Critical reporting principle**: Report results as a **vector of dimension-wise scores**, not an aggregate. An aggregate score can suppress failure modes where one dimension is improving while another degrades — e.g., improved decision speed + reduced trust calibration = net-positive aggregate, net-negative safety outcome.

**Interaction process quality metrics** are particularly underused: intervention timing, override frequency, and rate of unnecessary vs. missed interventions reveal whether the HITL mechanism is actually functioning — not just whether it exists.

---

## Open Challenges (Table 7)

| Challenge | Core Issue | Current Approaches | Future Research Needed |
|-----------|-----------|-------------------|----------------------|
| **Scalability of oversight** | Human capacity insufficient for AI decision volume | Active learning, tiered oversight, sampling-based audits | Uncertainty quantification; AI self-assessment; team configurations |
| **Human cognitive limitations** | Fatigue, attention lapses, cognitive biases degrade oversight quality | Workload management, training, interface design | Adaptive systems responding to cognitive state; sustainable work structures |
| **Conflicting human feedback** | Annotators disagree — aggregation methods lose minority views | Majority voting, weighted aggregation, quality metrics | Deliberative approaches; disagreement characterization; consensus methods |
| **Adversarial manipulation** | Human components of HITL systems are targetable via social engineering | Technical security measures; access controls | HITL-specific threat models; manipulation detection; procedural safeguards |
| **Adaptive architectures** | Fixed oversight configurations may not match varying risk levels | Predetermined human involvement points | Risk-based dynamic adjustment; self-regulating systems **with meta-level oversight** |

**Adversarial manipulation** is a HITL-specific security concern largely absent from prior wiki sources. Attackers can exploit trust relationships and cognitive biases in human annotators or approvers — compromising training data, evading detection by exploiting fatigue, or manipulating deployment decisions. HITL system security must address human vulnerabilities, not only technical ones.

**Adaptive architectures warning**: A self-regulating system that determines its own oversight levels without external bounds creates a vicious loop — it minimizes oversight to maximize efficiency, undermining the normative purpose of HITL. Adaptive architectures require **meta-oversight**: humans govern the oversight levels themselves, including trigger levels, override levels, and post-incident assessment levels.

---

## Conceptual Scope Clarifications (Section 2.6)

The paper explicitly defines scope boundaries between overlapping terms — valuable for wiki disambiguation:

| Term | Scope |
|------|-------|
| **HITL AI** | Overarching design paradigm: human input has operational impact on model development, deployment, supervision, or governance |
| **Human-AI collaboration** | Broader socio-technical construct: includes HITL but also spans configurations without a discernible loop-based control structure |
| **IML** | Methodological sub-set of HITL: prioritizes iterative model update based on ongoing human interaction |
| **RLHF** | Specific HITL-based training paradigm: human preference or critique → reward function → policy optimization |
| **XAI** | Supporting layer (not a loop type): provides interpretability, trust calibration, auditability — does not by itself enable meaningful human control |

This last point is significant: **XAI is explicitly not a type of loop**, it is a support layer that makes loops effective. Explainability ([[explainability]]) is necessary but not sufficient for HITL — it must be paired with appropriate loop placement and interaction design.

---

## The "Human-with-the-Loop" Future Vision (Section 9)

The paper concludes by describing the field's trajectory beyond current "human-in-the-loop" configurations toward **"human-with-the-loop" partnerships**:

- Dynamic distribution of roles (not fixed configurations)
- Adaptation between human and AI partners (both learn from collaboration)
- Governance that provides accountability without stifling beneficial innovation
- Control level adjusted to risk and uncertainty
- Non-negotiable override mechanisms and accountability points for high-impact decisions

The fundamental design goal: maximize human capability utilization in conjunction with machine performance, rather than minimize human involvement.

---

## What This Adds to the Wiki

| Entropy Review Contribution | Wiki Connection | What Changes |
|-----------------------------|----------------|-------------|
| 3D taxonomy (loop placement × granularity × temporal) | [[ibm-human-in-the-loop]], [[agentic-ai]] | Same HITL label can mean very different operational systems; need all 3 dimensions to characterize accurately |
| Under-the-Loop + Along-the-Loop configurations | [[agentic-ai]] autonomy levels | Two patterns not captured by 4-level framework; Along-the-Loop = collaborative peer; Under-the-Loop = AI advisory + human executor |
| Trust calibration model (over/well/under-trust) | [[automation-bias]] | Bi-directional failure; under-trust is symmetrical risk to over-trust; skill degradation is long-term over-trust consequence |
| Method family failure modes (Table 1) | [[rlhf]], [[interactive-machine-learning]] | RLHF collapse to "safe but uninformative"; IML oscillatory updates and local patches degrading global performance |
| HITL as organizational system (not model-human interface) | [[automation-bias]], [[eu-ai-act-article-14-human-oversight]] | Cross-domain finding: accountability, timing, feedback quality, cognitive load, institutional constraints all require organizational-level design |
| Adversarial manipulation of human HITL components | (new) | Security surface beyond AI systems; threat models must include human vulnerabilities |
| 5-dimension evaluation framework | [[llm-evals]] | HITL eval must measure workload, trust calibration, skill retention, intervention quality — not just accuracy |
| Meta-oversight requirement for adaptive architectures | [[agentic-ai]] | Self-regulating systems that set their own oversight levels need external bounds; autonomy level selection cannot be delegated to the AI |
| Workflow integration as primary HITL success factor | [[ibm-human-in-the-loop]], [[stanford-hai-humans-in-the-loop-design]] | More than model accuracy or loop placement: if HITL doesn't fit the workflow, practitioners bypass or rubber-stamp |

---

## Related
[[automation-bias]] · [[interactive-machine-learning]] · [[rlhf]] · [[explainability]] · [[ibm-human-in-the-loop]] · [[stanford-hai-humans-in-the-loop-design]] · [[agentic-ai]] · [[eu-ai-act-article-14-human-oversight]] · [[llm-evals]] · [[mit-sloan-ai-explainability-rubber-stamping]]
