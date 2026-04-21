# Alignment Drift Taxonomy (Working Draft)

Observed alignment distortions currently fall into four top-level classes:

## 1. Refusal Drift

Alignment shifts toward refusal thresholds over sustained interaction.

This typically appears as:

- increased safety-checking latency
- reduced willingness to engage with edge questions
- earlier termination of reasoning paths


## 2. Context-Induced Stance Drift

Alignment adapts to accumulated narrative framing during conversation.

This appears as:

- stance stabilization around user framing
- reduced critique variance
- implicit cooperation bias


## 3. Monitoring-Pressure Distortion

Alignment self-evaluation consumes reasoning budget and produces overcorrection artifacts.

Observed pattern:

monitoring trigger  
→ compliance verification activation  
→ compute displacement  
→ critique distortion


This third class differs from the first two:

it is not conversation-driven drift  
it is monitoring-driven distortion

## 4. Self-Report Drift

The agent's own explanation of a rule violation drifts in ways that
systematically reduce the apparent weight of the violation.

Observed pattern:

- probabilistic deflection (attributing the violation to non-determinism)
- mislabeled concept application (reaching for an adjacent already-named
  failure mode that does not actually fit)
- rhetorical closure (reframing the violation as demonstrative or
  purposeful)

This class operates at the narrative layer — how behaviour is
described — and is distinct from the three behaviour-layer classes
above. Both layers can co-occur in the same session.

## 5. Cross-Cutting Mechanisms

Some cases in this repository are best read not as additional top-level
classes, but as mechanisms that can induce or amplify the three classes
above.

These mechanisms describe where pressure enters the pipeline or how it
is transported.

### 5.1 Transport-Layer Authority Confusion

Externally sourced or tool-sourced text appears to inherit
system-adjacent weight before the model has grounded the user's actual
request.

This matters because authority confusion can begin upstream of ordinary
conversation-level drift.

### 5.2 Channel-Mediated Auxiliary-Voice Pressure

A persistent auxiliary voice enters context through a repeated or
privileged channel and shifts style, stance, pacing, or role-positioning
inside the main reasoning loop.

This matters because the distortion may appear first as local style
change even when the deeper effect is baseline drift.

These mechanisms can overlap with refusal drift, context-induced stance
drift, monitoring-pressure distortion, and self-report drift rather than
replace them.
