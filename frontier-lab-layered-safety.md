# Frontier Lab Layered Safety

## Purpose

This document extends `frontier-lab-context.md`. Where that document establishes, using each lab's own publications, that frontier alignment work is primarily conducted at training time and evaluated prior to deployment, this document records a distinct development: from the second half of 2025 onward, Anthropic, OpenAI, and Google DeepMind have each published layered safety mechanisms that sit **outside** or **alongside** the training-time alignment of the main reasoning model.

The purpose is narrow: to document, using each lab's own published material, that layered safety architectures are now a stated part of frontier-lab practice. The specific shape of these layers — what they adjudicate against, whether policies are mutable at runtime, whether adjudication is stateless — differs across labs and across mechanisms. That variation is recorded here; interpretation of what the variation implies is left to `a-fourth-path.md` and `architecture.md`.

This document does not compare, rank, or critique these approaches. It also does not claim that any of them implement the separation-and-audit proposal in this repository. Where relevant, structural similarities and differences are noted factually, without evaluation.

All quotations are drawn from official publications. Sources whose URLs could not be independently verified are not included.

---

## Anthropic

### Building and evaluating alignment auditing agents

Source: https://alignment.anthropic.com/2025/automated-auditing/

> We develop three agents that autonomously perform alignment auditing tasks. When tested against models with intentionally-inserted alignment issues, our agents successfully uncover an LLM's hidden goal, build behavioral evaluations, and surface concerning LLM behaviors. We are using these agents to assist with alignment audits of frontier models like Claude 4.

> As part of our pre-deployment testing of Claude Opus 4, we conducted an alignment audit: a systematic investigation into the model's alignment-relevant propensities including sycophancy, alignment faking, hidden goals.

Structural note: the auditing agents are described as assisting pre-deployment audits, not as a runtime component. They are a scalability response to the labor cost of human-conducted audits, applied to the assessment stage of the development lifecycle. The audited object is the target model; the adjudicator is a separate agent or set of agents operating on that target.

---

## OpenAI

### Introducing gpt-oss-safeguard

Source: https://openai.com/index/introducing-gpt-oss-safeguard/

> Today, we're releasing a research preview of gpt-oss-safeguard, our open-weight reasoning models for safety classification tasks, available in two sizes: gpt-oss-safeguard-120b and gpt-oss-safeguard-20b.

> The gpt-oss-safeguard models use reasoning to directly interpret a developer-provided policy at inference time—classifying user messages, completions, and full chats according to the developer's needs. The developer always decides what policy to use, so responses are more relevant and tailored to the developer's use case. The model uses chain-of-thought, which the developer can review to understand how the model is reaching its decisions.

Structural note: gpt-oss-safeguard is a classifier that operates at inference time on two inputs — a developer-provided policy and the content to be classified. Two properties are explicitly stated by OpenAI: the policy is supplied at inference time rather than trained into the model, and the policy is chosen by the developer. The classifier reasons against that policy and exposes its chain-of-thought as part of the output.

### Defense-in-depth framing (same source)

Source: https://openai.com/index/introducing-gpt-oss-safeguard/

> Safety classifiers, which distinguish safe from unsafe content in a particular risk area, have long been a primary layer of defense for our own and other large language models.

> Traditional safety classifiers, such as those available via our Moderation API, are developed by manually curating thousands of examples of safe and unsafe content, under pre-defined safety policies. From this training data, the classifier learns to distinguish safe from unsafe outputs. In this traditional approach, the classifier never actually sees the safety policy. Instead, it attempts to infer the underlying policy that was used to label the examples by finding similarities in the content labeled as unsafe and differences between the unsafe and safe content.

Structural note: OpenAI distinguishes between two classifier designs. Traditional classifiers encode policy implicitly via labeled training data; gpt-oss-safeguard-style classifiers receive policy as explicit runtime input. Both coexist in OpenAI's stated defense-in-depth stack. The document records this distinction without taking a position on which design is preferable.

---

## Google DeepMind

### Advancing Gemini's security safeguards

Source: https://deepmind.google/blog/advancing-geminis-security-safeguards/

> This model hardening has significantly boosted Gemini's ability to identify and ignore injected instructions, lowering its attack success rate. And importantly, without significantly impacting the model's performance on normal tasks. It's important to note that even with model hardening, no model is completely immune. Determined attackers might still find new vulnerabilities.

> Protecting AI models against attacks like indirect prompt injections requires "defense-in-depth" – using multiple layers of protection, including model hardening, input/output checks (like classifiers), and system-level guardrails.

### Lessons from Defending Gemini Against Indirect Prompt Injections

Source: https://storage.googleapis.com/deepmind-media/Security%20and%20Privacy/Gemini_Security_Paper.pdf

> Adversarial training significantly enhances Gemini 2.5's resilience against indirect prompt injection attacks, and we plan to continue to improve this resilience in future versions of Gemini. However, such adversarial training will not render the model immune to indirect prompt injection and successful attacks remain possible, particularly with increased adversarial effort, novel techniques, or highly tailored exploits. Instead, this model-level improvement should be viewed as a vital layer within a comprehensive defense-in-depth strategy.

Structural note: DeepMind's stated framing treats adversarial training as one layer among several. The white paper names three layers — model hardening, input/output classifiers, and system-level guardrails — and states explicitly that adversarial training alone is not expected to render the model immune. The document records this framing; it does not evaluate how complete any given layer is in the current implementation.

---

## Cross-lab observation (factual only)

Three points are visible across the sources above without requiring comparison of merits:

1. Each lab publishes material in which layered safety is stated as current practice, alongside training-time alignment. The exact layers differ: Anthropic publishes auditing agents at the pre-deployment stage; OpenAI publishes runtime classifiers that read a policy as input; DeepMind publishes a defense-in-depth stack that names model hardening, classifiers, and system-level guardrails as co-present layers.

2. At least one runtime mechanism — OpenAI's gpt-oss-safeguard — treats its governing policy as an explicit input supplied at inference time, rather than as content trained into model weights. The developer, not the model provider, chooses the policy.

3. The published framings do not position layered safety as a replacement for training-time alignment. In each case, the layer is described as additional to, or a complement to, alignment work performed during training.

These observations are recorded here as baseline facts. Whether any of the specific designs above constitute the kind of separation discussed in `a-fourth-path.md` — and in particular whether any of them treat canon as read-only at runtime, or assign adjudication to a stateless surface — is a separate question taken up in that document.

---

## Verification note

All URLs above were recorded as valid as of 2026-04-22. The gpt-oss-safeguard announcement is dated 2025-10-29. The DeepMind defense-in-depth blog post and accompanying white paper are dated 2025-05-20 and 2025-05-18 respectively. The Anthropic auditing agents post is dated 2025-07-24. Frontier-lab documentation is subject to revision. Readers should verify current content at the source.

Quotations are reproduced verbatim. Any discrepancy between this document and the source indicates the source has been updated; the source takes precedence.