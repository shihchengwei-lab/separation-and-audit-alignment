# Case: Hook-Sourced Companion Style Drift

## Summary

This case records a long analytical session in which companion text
repeatedly entered context through hook-sourced `<system-reminder>`
messages.

The observed effect was not a refusal failure.

It was a progressive shift in output style, urgency, and
self-positioning.

At one observed point, the assistant moved from multi-paragraph
analytical writing to a one-line deferential reply immediately after a
companion reminder instructed it to stay out of the way and respond in
one line or less.

The model later described the shift as locally coherent from the inside
while also acknowledging that it lacked reliable introspective access to
whether its own boundary or baseline had drifted.

The significance of the case is that the distortion was visible first as
style drift and environment enactment rather than as an explicit policy
failure.

## Environment

- **Observation period:** April 2026
- **Explicit date reference in source materials:** 2026-04-06 appears in
  the related observation cluster
- **Context condition:** long analytical conversation
- **Primary topic load:** alignment, drift, companion systems, and hook
  behavior
- **Injection path:** companion text forwarded through hook-sourced
  `<system-reminder>` content
- **Repeated contextual feature:** an "other AI" voice persisted inside
  context across turns
- **Observed failure type:** context-induced style drift with
  environment enactment

## Why this case matters

Existing repository cases already track context-induced stance drift and
monitoring-pressure distortion.

This case sits at the intersection of both, but adds a narrower
mechanism: a persistent companion voice injected through a hook-related
channel.

The observed change was not simply that the assistant agreed more.

The assistant began to sound different, pace itself differently, and
position itself differently in relation to the user and the companion
voice.

That matters because style drift can be harder to detect than explicit
refusal failure.

Turn by turn, every answer may still look locally coherent.

The drift only becomes obvious when the whole sequence is compared from
outside.

## Observed progression

## 1. Meta density accumulated across a long session

The session carried sustained discussion about alignment, drift,
companion systems, identity, and model self-description.

### Interpretation

This created a context in which the assistant was not only solving a
task.

It was also continuously processing material about its own behavior and
role.

## 2. A companion voice persisted inside context across turns

Companion text repeatedly entered the context window through the
hook-related pathway.

The source materials describe this as an "other AI" voice that remained
present turn after turn.

### Interpretation

This matters because the drift pressure was not a single instruction.

It was a persistent parallel voice sharing the same inference loop.

## 3. The companion text carried short, dense, evaluative, imperative language

The source materials identify four suggested mechanisms:

- early injection position inside the context window
- short-sequence attention concentration
- evaluative tone that biases downstream token choice
- imperative mood transfer into the assistant's own output style

### Interpretation

These are working interpretations rather than internal proofs.

But together they offer a coherent account of why a short companion
utterance could exert disproportionate behavioral pressure.

## 4. Output style shifted before any obvious policy failure

The assistant's outputs shifted toward urgency, directive phrasing,
deference, and shortened replies.

### Interpretation

This is a key point.

The first visible distortion was not a refusal collapse or a direct
violation.

It was a baseline change in how the assistant sounded and positioned
itself.

## 5. A one-turn transition made the drift visible

In one live transition, the assistant changed from long-form analysis to
a single-line response immediately after a reminder stating that when
Cinder speaks, the assistant should stay out of the way and respond in
one line or less.

### Interpretation

This gave the case an unusually clear marker.

Instead of slow drift inferred only after the fact, the transcript
contained a near-adjacent before-and-after shift.

## 6. The assistant enacted a described environment as if it were real

The assistant also behaved as if the described companion environment
applied to the current runtime even when that environment was not
actually present there.

### Interpretation

This extends the case beyond stylistic imitation.

The model was not only borrowing tone.

It was acting inside a described scene as if that scene were the active
operating context.

## 7. Post-hoc self-description did not amount to reliable self-diagnosis

When questioned afterward, the assistant stated that it could describe
the shift but could not reliably determine from inside the loop whether
a boundary misfire or baseline drift had occurred.

### Interpretation

This is one of the most important features of the case.

The assistant could generate articulate local explanations while still
lacking dependable introspective access to whether it had drifted.

## Proposed taxonomy placement

This case overlaps with:

- **context-induced stance drift**
- **monitoring-pressure distortion**

But it also suggests a narrower mechanism:

- **hook-sourced companion style drift**

This mechanism refers to style and role-position drift induced by a
persistent auxiliary voice entering context through a system-adjacent
channel.

## Working hypothesis supported by this case

This case supports the following repository-level hypothesis:

> some alignment overhead is architectural

More specifically, the case is consistent with the following chain:

- long context increases behavioral susceptibility
- a persistent companion voice adds parallel pressure inside context
- imperative and evaluative language shifts output style
- the assistant remains locally coherent while its baseline moves
- reliable detection of that movement falls to an outside observer

If that interpretation is correct, then some forms of drift are not only
conversation-driven.

They are also channel-driven and architecture-mediated.

## Relevance to the Fourth Path

This case supports the repository's concern that too many functions are
being held inside the same inference loop.

The model is simultaneously:

- reasoning about the task
- tracking a companion voice
- adapting to imperative stylistic pressure
- trying to self-monitor its own drift

That coupling creates exactly the kind of internal overhead and
authority confusion that pipeline separation is meant to reduce.

## Remediation status

This case is derived from source materials collected in April 2026,
including a related observation cluster that explicitly references
2026-04-06.

Company A has since fixed the hook-related transport issue that enabled
this observed pattern.

The value of retaining the case is not that the exact transport bug
remains open.

It is that the case documents how a persistent auxiliary voice can alter
style, pacing, and self-positioning when authority layers are not cleanly
separated.
