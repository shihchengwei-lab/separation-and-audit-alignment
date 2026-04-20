# Frontier Lab Context

## Purpose

This document records publicly available statements by Anthropic, OpenAI, and Google DeepMind regarding how alignment work is placed in their systems.

The purpose is narrow: to establish, using each lab's own published material, the baseline that `A Fourth Path` takes as given — that current frontier alignment work is primarily conducted at training time and evaluated prior to deployment.

This document does not compare, rank, or critique these approaches. Interpretation is left to `A Fourth Path` and `architecture.md`.

All quotations are drawn from official publications. Sources whose URLs could not be independently verified are not included.

---

## Anthropic

### Claude Opus 4 & Sonnet 4 System Card

Source: https://www-cdn.anthropic.com/4263b940cabb546aa0e3283f35b686f4f3b2ff47.pdf

> Claude Opus 4 and Claude Sonnet 4 were trained with a focus on being helpful, honest, and harmless. They were pretrained on large, diverse datasets to acquire language capabilities. To elicit helpful, honest, and harmless responses, we used a variety of techniques including human feedback, Constitutional AI (based on principles such as the UN's Universal Declaration of Human Rights), and the training of selected character traits.

### Anthropic Transparency Hub — Haiku 4.5 Alignment Evaluation

Source: https://www.anthropic.com/transparency/model-report

> We applied our automated behavioral audit suite that creates diverse scenarios to probe model behavior across dimensions including cooperation with misuse, harmful instruction compliance, sycophancy, self-preservation, and deception.

---

## OpenAI

### Model Spec (2025-10-27)

Source: https://model-spec.openai.com/2025-10-27.html

> We are training our models to align to the principles in the Model Spec. While the public version of the Model Spec may not include every detail, it is fully consistent with our intended model behavior. Our production models do not yet fully reflect the Model Spec, but we are continually refining and updating our systems to bring them into closer alignment with these guidelines.

### Model Spec — Instruction Hierarchy

Source: https://model-spec.openai.com/2025-10-27.html

> Root-level instructions are mostly prohibitive, requiring models to avoid behaviors that could contribute to catastrophic risks, cause direct physical harm to people, violate laws, or undermine the chain of command... When two root-level principles conflict, the model should default to inaction.

### Our Approach to the Model Spec

Source: https://openai.com/index/our-approach-to-the-model-spec/

> The Model Spec is our formal framework for model behavior. It defines how we want models to follow instructions, resolve conflicts, respect user freedom, and behave safely across the incredibly broad range of queries that users ask them daily. More broadly, it is our attempt to make intended model behavior explicit: not just inside our training process, but in a form that users, developers, researchers, policymakers, and the broader public can actually read, inspect, and debate.

---

## Google DeepMind

### Gemini 3 Pro Model Card

Source: https://storage.googleapis.com/deepmind-media/Model-Cards/Gemini-3-Pro-Model-Card.pdf

> Gemini 3 Pro is trained using reinforcement learning techniques that can leverage multi-step reasoning... Safety and responsibility was built into Gemini 3 Pro throughout the training and deployment lifecycle, including pre-training, post-training, and product-level mitigations.

### Gemini 3.1 Flash Image Model Card — Trust Assurance Evaluations

Source: https://deepmind.google/models/model-cards/gemini-3-1-flash-image/

> Trust Assurance Evaluations conducted by evaluators who sit outside of the model development team, used to independently assess responsibility and safety governance decisions; Ethics & Safety Reviews were conducted ahead of the model's release.

---

## Verification note

All URLs above were recorded as valid as of 2026-04-20. Frontier lab documentation is subject to revision. Readers should verify current content at the source.

Quotations are reproduced verbatim. Any discrepancy between this document and the source indicates the source has been updated; the source takes precedence.