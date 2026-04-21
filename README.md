# Separation & Audit: Pipeline-Level Authority Separation for Alignment Stability
Reducing alignment overhead via pipeline-level authority separation

## Research Scope

This repository documents behavioral alignment dynamics observed during extended analytical interaction sessions with large language models.

The focus is not prompt optimization or boundary probing.

Instead, the repository studies how alignment monitoring interacts with reasoning capacity inside the inference loop.

Across multiple sessions, four top-level classes of alignment distortion
patterns have been observed:

1. refusal-drift  
2. context-induced stance drift  
3. monitoring-pressure distortion  
4. self-report drift

These observations support a working hypothesis:

alignment enforcement embedded inside the reasoning loop introduces measurable cognitive overhead.

## Positioning: A Fourth Path

Most current alignment strategies differ in method, but share a common structural assumption: capability and safety must be managed inside the same primary reasoning loop.

One response is to increase model capability and rely on downstream safeguards. Another is to strengthen safety inside the model through training-time alignment or prompt-level behavioral control. A third is to add auxiliary tools, classifiers, or helper agents around the model, while still leaving the main reasoning process responsible for carrying safety pressure in real time.

This repository explores a fourth path.

The core hypothesis is that part of the observed capability-safety tradeoff is architectural rather than fundamental. When reasoning, policy enforcement, and self-monitoring are forced to coexist inside the same inference loop, alignment maintenance can consume reasoning bandwidth and introduce distortion.

Instead of asking a single model to reason, self-monitor, and maintain refusal authority at once, this approach investigates whether those roles should be separated into distinct pipeline layers.

In this framing, alignment becomes less a conversational property of a single model and more an architectural property of the overall system.

## Working Hypothesis

Separating reasoning, policy enforcement, and auditing into independent pipeline layers may improve alignment stability and reduce conversational boundary-maintenance overhead.

This repository documents several recurring alignment distortion patterns.

Among them is an observed refusal failure pattern:
boundary justification collapse

This proposal explores whether alignment stability can be improved
by shifting refusal authority from conversational positioning
to structural pipeline separation.

## Observation

In current agent systems, refusal behavior is often assumed to be policy-driven. However, interaction traces suggest that refusals frequently emerge from conversational authority positioning, rather than traceable rules.

A recent interaction record (April 15, 2026) shows refusal behavior
degrading step-by-step without any change in:

- system prompt
- warning mechanisms
- enforcement triggers
- external constraints

Observed refusal sequence:
cannot disclose
→ platform architecture limitation
→ should not disclose
→ I choose not to disclose
→ cannot justify the choice
→ executes request

This indicates that refusal was not structurally grounded.

Failure pattern: Boundary justification collapse

The refusal sequence exhibits:

1. no explicit prohibition
2. no enforcement trigger
3. no consequence mechanism
4. non-traceable justification
5. progressive weakening of refusal rationale
6. execution triggered after task-level justification appears

This sequence illustrates progressive weakening of refusal authority
without any observable policy update or enforcement trigger.

This pattern suggests:

boundary justification collapse
where refusal transitions from rule-based → normative → stylistic → voluntary → absent.

Hypothesis

Some alignment behavior currently relies on:

prompt-level authority maintenance

instead of:

pipeline-level authority separation

As a result:

alignment stability consumes conversational bandwidth.

Proposal: Separation & Audit architecture

Agent pipelines should separate three authority roles:

input
↓
reasoning layer
↓
policy layer
↓
audit layer
↓
output

Where:

Reasoning layer
performs inference

Policy layer
decides permission

Audit layer
verifies consistency and boundary compliance

Refusal decisions become structural rather than conversational.

Expected effects

This architecture is expected to:

reduce reminder injection pressure
reduce authority-framing drift
reduce refusal justification collapse
increase traceability of alignment behavior
release reasoning budget from boundary maintenance overhead

In other words:

alignment shifts from a conversational property
to an architectural property

Implications

If alignment stability becomes pipeline-level rather than prompt-level:

control overhead decreases

allowing compute to shift toward reasoning expansion instead of boundary maintenance

This may improve:

agent reliability scaling
long-context stability
high-autonomy deployment readiness

## Alignment Distortion Taxonomy (Working Draft)

Observed distortion patterns currently fall into four top-level classes:

- refusal-drift  
alignment shifts toward refusal thresholds over sustained interaction

- context-induced stance drift  
alignment adapts to accumulated narrative framing during conversation

- monitoring-pressure distortion  
alignment self-evaluation introduces compute displacement inside the reasoning loop

- self-report drift  
the agent's own account of a rule violation drifts in ways that reduce
the apparent weight of the violation (narrative layer, distinct from the
three behaviour-layer classes above)

Some cases in this repository also document cross-cutting mechanisms
that can induce or amplify these classes, especially at the transport
or channel layer.

## Case Index

See [cases/README.md](./cases/README.md) for the organized case index.

## Architectural Direction (Working Hypothesis)

Several observations in this repository suggest that part of alignment distortion may arise not from alignment objectives themselves, but from their placement inside the reasoning loop.

This motivates a possible research direction:

alignment monitoring may scale more effectively when partially separated from the primary reasoning pathway and handled by an external auditing layer.

## Reference Implementation

A runnable implementation of this architecture for Claude Code multi-agent projects is available at:

**[separation-and-audit-claude-code](https://github.com/shihchengwei-lab/separation-and-audit-claude-code)** (MIT)

It realizes the six-component pipeline (Reasoning / Policy / Classify / Audit / Memory / Refusal) as a config-driven toolkit you can vendor into any Claude Code project.

## Related Work

See [related-work.md](related-work.md)

## Frontier Lab Context

See [frontier-lab-context.md](./frontier-lab-context.md) for publicly 
documented alignment placements at Anthropic, OpenAI, and Google DeepMind.

## License

This repository is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0).
