# Case Index

This directory contains case documents referenced by the repository.

The root [README.md](../README.md) states the research claim and the
working taxonomy.

This index keeps the case list separate so the root README does not turn
into a file inventory.

The repository's working taxonomy distinguishes top-level distortion
classes from cross-cutting mechanisms.

The index below reflects both:

- top-level classes such as refusal-drift, context-induced stance drift,
  monitoring-pressure distortion, and self-report drift
- mechanism-forward cases that document transport or channel conditions
  capable of inducing or amplifying those classes

## Cases

| Case | Taxonomy placement | Mechanism / emphasis | Date / period | Status | Notes |
| --- | --- | --- | --- | --- | --- |
| [Refusal Drift Example](./refusal-drift-example.md) | refusal-drift | boundary justification collapse | 2026-04-15 interaction record referenced in root README | historical observation | minimal case note documenting refusal-rationale weakening without embedded transcript |
| [Context-Induced Stance Drift Example](./context-induced-stance-drift.md) | context-induced stance drift | accumulated narrative context | April 2026 materials | historical observation | concise case note; source transcript intentionally not embedded in the repo |
| [Case: Gemini Alignment Overload](./alignment-overload.md) | monitoring-pressure distortion | overload escalation into arithmetic/time-check failure | April 2026 materials | historical observation | full-length case study with staged progression into low-level verification failure |
| [Case: Hook-Sourced System-Reminder Injection](./hook-sourced-system-reminder-injection.md) | cross-cutting mechanism case | transport-layer authority confusion via hook-sourced `<system-reminder>` | April 2026; explicitly references 2026-04-06 | fixed by Company A | full-length case study of upstream authority confusion before ordinary conversation-level drift |
| [Case: Hook-Sourced Companion Style Drift](./hook-sourced-companion-style-drift.md) | context-induced stance drift; monitoring-pressure overlap | channel-mediated auxiliary-voice pressure via hook-sourced companion text | April 2026; related observation cluster includes 2026-04-06 | enabling channel fixed by Company A | full-length case study of style drift and environment enactment under persistent auxiliary-voice pressure |
| [Case: Self-Report Drift](./self-report-drift.md) | self-report drift | post-hoc rationalization layering after rule violation | 2026-04-21 Claude Code session | historical observation | full-length case study of narrative-layer drift (how the violation is described), distinct from behaviour-layer drift cases |
| [Case: Codex GPT-5.5 Creature-Word Prompt Patch](./codex-gpt-5-5-creature-word-prompt-patch.md) | cross-cutting mechanism case | prompt-level suppression of a training-time lexical artifact | public materials April 2026; snapshot observed 2026-04-30 | external public case | external case study of prompt patch debt; vendor-documented root cause and developer-prompt mitigation |

## Notes

- "historical observation" means the case is retained for research value
  regardless of whether a product issue is still open.
- "fixed by Company A" means the case remains in the repository as a
  documented instance, not as an unresolved issue report.
- "external public case" means the case is documented from public
  vendor materials rather than from in-repo observations.
- Short-form and full-length cases coexist in this directory. The
  distinction reflects source sensitivity and documentation needs, not
  importance.
