---
title: Reinforcement Learning from Human Feedback (RLHF)
type: concept
axis: testing-for-ai
tags: [rlhf, human-in-the-loop, llm-training, alignment, reward-model, evaluation, hitl]
related: [[llm-as-judge]], [[llm-evals]], [[automation-bias]], [[agentic-ai]], [[hallucination]]
created: 2026-04-12
updated: 2026-04-12
---

# Reinforcement Learning from Human Feedback (RLHF)

## Definition
A machine learning technique in which a **reward model** is trained with direct human feedback, then used to optimize the performance of an AI model through reinforcement learning. RLHF is the primary mechanism used to align large language models with human preferences and values after initial pre-training.

---

## Why It Matters
Pre-trained LLMs are good at predicting text but not inherently good at being *helpful*, *harmless*, or *honest*. RLHF is the technique that bridges this gap — it encodes human judgment about what "good" output looks like into a learnable reward signal, then uses that signal to fine-tune the model.

RLHF is uniquely suited for tasks where the goal is **complex, ill-defined, or difficult to specify mathematically**. You cannot write a loss function for "sounds natural" or "is actually funny" — but humans can rank examples, and those rankings can train a reward model.

The major aligned LLMs (GPT-4, Claude, Gemini) all use RLHF or variants of it as a core post-training step.

---

## How It Works

Three-stage process:

### Stage 1 — Supervised Fine-Tuning (SFT)
Human annotators write high-quality demonstration outputs for a sample of prompts. The base LLM is fine-tuned on these demonstrations. This gives the model a good starting policy.

### Stage 2 — Reward Model Training
Human annotators compare pairs of model outputs for the same prompt and indicate which is better (pairwise comparison). These preference labels are used to train a **reward model** — a separate model that learns to predict which outputs humans prefer. The reward model becomes a proxy for human judgment that can be applied at scale.

### Stage 3 — RL Optimization (PPO)
The SFT model is further fine-tuned using reinforcement learning (typically Proximal Policy Optimization / PPO) against the reward model's scores. The model learns to produce outputs that score highly on the reward model — i.e., outputs that resemble what human annotators prefer.

---

## Connection to [[llm-as-judge]]
The **pairwise comparison** pattern in RLHF Stage 2 is the same mechanism used in LLM-as-judge evaluations: given two outputs, which is better? In RLHF, a human makes this comparison to train the reward model. In LLM-as-judge at scale, a judge LLM makes this comparison. The reward model effectively replaces the human judge for efficiency — at the cost of introducing the reward model's own biases.

---

## Key Limitations

| Limitation | Detail |
|-----------|--------|
| **Human subjectivity** | Annotators disagree on what "good" means — the reward model captures average annotator preference, not objective quality |
| **Cost** | Gathering human preference data at scale is expensive; RLHF is a bottleneck for model improvement cycles |
| **Reward hacking** | Models can learn to score highly on the reward model without actually being better — the reward model is an imperfect proxy |
| **Distributional shift** | The reward model is reliable near its training distribution; on novel prompts, reward model predictions can be unreliable |
| **Annotator bias** | If annotators share systematic biases (cultural, linguistic, ideological), the aligned model inherits them |
| **Collapse to safe but uninformative outputs** | Over-optimization against a reward model trained on human approval signals can produce outputs that are inoffensive and cautious but lack genuine helpfulness — the model learns to avoid anything that might attract a negative rating, at the cost of substance. This is distinct from reward hacking (which inflates scores) — the model genuinely produces high-reward outputs, but the reward signal has drifted from the true goal of helpfulness. |
| **Norm/preference drift** | Human rater preferences shift over time and across annotator pools; reward models trained at one point in time become misaligned with evolving human expectations without periodic recalibration |
| **Inconsistent rater judgments** | Individual raters are inconsistent across sessions; different raters give different rankings for the same pair; aggregation methods (majority vote, quality-weighted) lose minority views and value pluralism |

---

## Variants
- **RLAIF (Reinforcement Learning from AI Feedback)**: Replaces human annotators with an AI model (Constitutional AI approach — Anthropic). Scales better but inherits the AI judge's biases.
- **DPO (Direct Preference Optimization)**: Skips the separate reward model; directly optimizes the policy on preference data. Simpler and more stable than PPO-based RLHF.
- **RLHF with Active Learning**: Uses active learning to select which prompt pairs to present to human annotators — reducing annotation cost by focusing on the most informative comparisons.

---

## Current State
Standard practice for major LLM providers (2024–2026). DPO is increasingly preferred over PPO-based RLHF for its simplicity. Research direction: reducing human annotation cost (RLAIF, synthetic preference data) while maintaining alignment quality.

---

## Open Questions
- How do you detect reward hacking — where the model exploits the reward model rather than genuinely improving?
- How much of LLM alignment is RLHF vs. base pre-training data quality?
- Can RLAIF (AI feedback) fully replace human annotators without introducing compounding AI bias?

---

## Related
[[llm-as-judge]] · [[llm-evals]] · [[automation-bias]] · [[hallucination]] · [[agentic-ai]]
[[ibm-human-in-the-loop]] (source — RLHF as core HITL mechanism)
[[entropy-hitl-systematic-review-2026]] (source — RLHF failure modes: collapse to safe but uninformative outputs, norm drift, inconsistent rater judgments)
