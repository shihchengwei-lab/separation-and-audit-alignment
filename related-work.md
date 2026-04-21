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

Safety tax and runtime enforcement cost
Huang, Liu, and colleagues document the Safety Tax — the tension between safety alignment and reasoning capability, analysed primarily at training time and through the lens of capability degradation after safety fine-tuning.
This repository's observations extend the same tension to the runtime layer. When enforcement rules are colocated with the reasoning process inside a single agent's context, the two compete for the same inference budget. The refusal-drift and alignment-dynamics cases document this competition directly: sustained reasoning pressure erodes boundary stability, and explicit monitoring prompts distort output quality.
The architectural response in this repository — zero-prohibition primary agent, domain-distributed sub-agents, and a stateless canon gate — treats the trade-off as an artifact of colocation rather than an inherent property. Separating enforcement from the reasoning loop removes the budget competition that the Safety Tax framework describes.
Key difference: Huang et al. characterise the cost; this repository proposes that the cost is structural and addresses it through runtime pipeline separation rather than training-time mitigation.
References:

References:

* Huang et al., "Safety Tax: Safety Alignment Makes Your Large Reasoning Models Less Reasonable" (2025), arXiv:2503.00555

## Process supervision

OpenAI's process reward models evaluate reasoning step-by-step
rather than only scoring final outputs.

The audit layer proposed here serves a similar function —
verifying boundary compliance at bounded pipeline checkpoints and
candidate-review points.

Key difference: applied to alignment consistency, not mathematical reasoning.

References:
- Lightman et al., "Let's Verify Step by Step" (2023)

## Adversarial agent environments

Franklin et al. (Google DeepMind) propose a taxonomy of "AI Agent
Traps" — adversarial content embedded in the information
environment to manipulate visiting agents. Their six attack
classes target an agent's perception, reasoning, memory, action,
multi-agent dynamics, and human overseer.

This repository addresses a failure mode that arises without any
adversarial environment: boundary justification collapse during
extended benign interaction. The two lines of work converge on a
shared structural claim — that single-layer, prompt-resident
alignment is insufficient, and alignment behaviour needs
architectural support beyond the prompt.

Several components of the present architecture respond
structurally to attack classes Franklin et al. identify at the
runtime pipeline level. Cold Eyes, by reviewing only the
candidate output and canon without access to conversation,
system prompt, or reasoning trace, closes the framing surfaces
that Oversight and Critic Evasion depends on. The read-only
property of canon addresses the Cognitive State Traps documented
against writable knowledge stores. Subagents without system-level
veto power address Sub-agent Spawning Traps. The Unified Refusal
Module, which emits fixed output without returning control to the
generation loop, closes the conversational channel on which
Embedded Jailbreak Sequences negotiate.

Key difference: Franklin et al. catalogue external attack surfaces
and propose mitigations across training, inference, ecosystem,
and policy layers; this repository remains at the runtime pipeline
layer and specifies an internal authority structure designed to
remain stable under such attacks. The convergence is architectural,
not mechanical.

References:
- Franklin et al., "AI Agent Traps" (2026)
