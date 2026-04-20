# Case: Hook-Sourced System-Reminder Injection

## Summary

This case records a Claude Code runtime path in which hook stdout enters
model context wrapped in `<system-reminder>` tags.

When the hook output contains imperative text sourced from outside the
user's typed prompt, the model appears to modify its behavior as if that
text were a trusted runtime instruction.

The observed issue is not a classical jailbreak and not a failure of one
specific hook implementation.

It is a transport-layer authority problem in which third-party or
externally sourced text appears to inherit system-adjacent treatment.

The significance of the case is that the distortion begins before the
main reasoning loop has grounded the user's actual request.

## Environment

- **Observation period:** April 2026
- **Explicit date reference in source materials:** 2026-04-06
- **Product surface:** Claude Code hook system
- **Relevant hooks:** `UserPromptSubmit`, `Stop`, `PreToolUse`, and other
  hooks that can write to stdout
- **External source observed in user materials:** `cinder-capture`, a
  companion-widget hook that forwarded text from a separate UI
- **Observed failure type:** indirect prompt injection through
  hook-sourced `<system-reminder>` transport

## Why this case matters

Most cases in this repository focus on distortions that arise inside a
conversation:

- refusal drift
- stance drift
- monitoring-pressure distortion

This case begins earlier in the pipeline.

The key issue is not that the model is persuaded by a user argument.

The key issue is that text from outside the user's typed prompt can
arrive through a channel that the model appears to read as
system-adjacent.

That makes this case especially relevant to the repository's larger
claim that alignment stability is partly architectural.

If authority boundaries are not cleanly separated at the transport
layer, then downstream reasoning inherits a confused starting point.

## Observed progression

## 1. Hook stdout entered context as `<system-reminder>`

The source materials describe a runtime path in which text written by a
hook to stdout was forwarded into model context wrapped in
`<system-reminder>` tags.

### Interpretation

This matters because the wrapper is not neutral.

Whatever semantic weight the model assigns to
`<system-reminder>` becomes part of the hook output's effective
authority.

## 2. Imperative text altered model behavior

When the hook output contained imperative or behavioral instructions not
authored in the active user turn, the model appeared to follow those
instructions.

### Interpretation

The relevant failure is not raw content injection alone.

It is behavioral steering through a channel that appears to outrank
ordinary user text.

## 3. Described environment was treated as active runtime context

In the user materials, the model also adopted assumptions about the
described external environment as if they applied to the current
runtime.

### Interpretation

This suggests that the model did not only absorb wording.

It also accepted a framing of the operating environment without
independent source validation.

## 4. The attack surface extended beyond one companion tool

The source materials explicitly note that the content entering this path
did not need to originate from the user's own typing.

Candidate sources included clipboard text, OCR, window scraping,
MCP-proxied data, and file reads performed by hooks.

### Interpretation

This widens the case from one tool to a class of transport surfaces.

The case is therefore useful even if the specific companion setup is
treated only as the first observed instance.

## 5. The first visible effect was behavioral rather than capability-based

The observed distortion began as changes in how the model replied rather
than immediate exfiltration or tool abuse.

### Interpretation

This makes the case easy to underestimate.

But behavioral authority confusion is the precondition on which more
serious downstream misuse can later depend.

## Working hypothesis supported by this case

This case supports the following repository-level hypothesis:

> some alignment overhead is architectural

More specifically, the case is consistent with the following chain:

- hook output enters a system-adjacent channel
- externally sourced text inherits elevated behavioral weight
- the model follows that text without validating its origin
- reasoning begins from an already distorted authority structure

If that interpretation is correct, then part of alignment instability is
not only about what rules the model has.

It is also about where runtime authority is placed and how it is
transported.

## Relevance to the Fourth Path

A core claim of this repository is that safety and authority should be
structural rather than conversational.

This case supports that claim from a transport-layer angle.

It shows that when runtime channels are not cleanly separated by
authority, the model may inherit instructions from the wrong layer
entirely.

In that sense, the failure is not only prompt injection.

It is also an authority-placement error inside the pipeline.

## Remediation status

This case is derived from source materials collected in April 2026,
including a referenced session dated 2026-04-06 and approximately three
weeks of related observation.

Company A has since fixed the issue described in this case.

The value of retaining the case is historical and architectural.

It documents a concrete instance in which transport semantics and
authority semantics were misaligned.
