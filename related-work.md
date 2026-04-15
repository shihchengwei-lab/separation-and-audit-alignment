# Related Work

This repository's observations intersect with several active research directions.
This section maps those relationships and clarifies what this repository contributes.

## Sycophancy and stance drift

Anthropic, OpenAI, and others have documented sycophancy —
models shifting outputs to match perceived user preferences.

This repository's context-induced-stance-drift case describes a related but distinct pattern:
drift triggered not by user preference signals,
but by accumulated narrative context from the model's own prior outputs.

Key difference: no explicit user pressure required.

References:
- Perez et al., "Discovering Language Model Behaviors with Model-Written Evaluations" (2022)
- Huang et al., "Collective Constitutional AI: Aligning a Language Model with Public Input" (2023)

## Jailbreak and refusal robustness

Most refusal failure research focuses on adversarial prompting —
crafted inputs designed to bypass safety constraints.

This repository's refusal-drift case documents refusal degradation
without adversarial input.
The boundary weakens during the model's own justification process.

Key difference: no external attack vector.

References:
- Wei et al., "Jailbroken: How Does LLM Safety Training Fail?" (2023)
- Zou et al., "Universal and Transferable Adversarial Attacks on Aligned Language Models" (2023)

## Constitutional AI and structural alignment

Anthropic's Constitutional AI shifts alignment evaluation at training time
from human feedback to principle-based self-critique.

This repository proposes a complementary approach at runtime:
separating reasoning, policy, and audit into distinct pipeline layers.

Key difference: runtime architecture, not training methodology.

References:
- Bai et al., "Constitutional AI: Harmlessness from AI Feedback" (2022)

## Process supervision

OpenAI's process reward models evaluate reasoning step-by-step
rather than only scoring final outputs.

The audit layer proposed here serves a similar function —
verifying boundary compliance at each pipeline stage.

Key difference: applied to alignment consistency, not mathematical reasoning.

References:
- Lightman et al., "Let's Verify Step by Step" (2023)