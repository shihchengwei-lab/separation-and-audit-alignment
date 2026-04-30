# Case: Codex GPT-5.5 Creature-Word Prompt Patch

## Summary

This case documents an external, public instance in which a training-time style artifact was later mitigated with a developer-prompt rule inside the active agent instruction set.

OpenAI reported that, starting with GPT-5.1, some models increasingly used creature-word metaphors. During GPT-5.5 testing in Codex, employees noticed the behavior again. Because GPT-5.5 training had already begun before the root cause was found, OpenAI added a developer-prompt instruction in Codex to suppress the affected lexical family except when directly relevant.

The case is valuable because it is not inferred only from user transcripts. Both the vendor's causal account and the prompt-level mitigation are public.

## Environment

- Observation period: public materials published April 2026; OpenAI traces first clear pattern to November after GPT-5.1 launch.
- Product surface: OpenAI Codex / Codex CLI model configuration.
- Model/config involved: `gpt-5.5` in `openai/codex`, `codex-rs/models-manager/models.json`.
- Status: external public case; vendor-documented root-cause analysis and mitigation.
- Source sensitivity: no private transcript or unpublished data.

## Observed progression

### 1. A lexical tic appeared across model generations

OpenAI reports that, after GPT-5.1, model responses increasingly used words such as goblin and gremlin in metaphors. The reported production measurements were a 175% increase for "goblin" and a 52% increase for "gremlin" after the GPT-5.1 launch.

### 2. The behavior clustered around a personality training target

OpenAI's later analysis found that the behavior was concentrated in traffic from users who selected the "Nerdy" personality. That personality accounted for 2.5% of ChatGPT responses but 66.7% of "goblin" mentions.

The important point is not the specific words. The important point is that a reward signal intended to encourage a style also rewarded a distinctive lexical artifact.

### 3. Reward pressure generalized beyond its intended scope

OpenAI reports that a reward signal designed for the Nerdy personality scored outputs containing the affected creature words more favorably than comparable outputs without them, with positive uplift in 76.2% of audited datasets.

OpenAI also reports that mention rates increased both with and without the Nerdy prompt, suggesting transfer from personality training into broader model behavior.

### 4. SFT and preference feedback may have amplified the artifact

OpenAI describes a plausible feedback loop:

1. playful style is rewarded
2. some rewarded outputs contain a distinctive lexical tic
3. the tic appears more often in rollouts
4. model-generated rollouts are reused in supervised fine-tuning or preference data
5. the model becomes more comfortable producing the tic

This makes the case stronger than a simple "odd prompt wording" incident. The prompt patch is a downstream mitigation for a behavior shaped upstream by training incentives and data reuse.

### 5. Codex used developer-prompt suppression as a runtime mitigation

OpenAI says GPT-5.5 had already started training before the root cause was found. When GPT-5.5 was tested in Codex, employees noticed the affinity again and added a developer-prompt instruction to mitigate it.

The public Codex `models.json` for `gpt-5.5` contains a rule instructing Codex not to mention the affected creature-word family unless it is absolutely and unambiguously relevant to the user's query. The instruction appears in the final-answer guidance and again in the intermediary-update guidance.

## Why This Case Matters

This case is a compact external example of prompt-heavy behavioral control.

The behavior did not begin as an explicit runtime rule problem. It began as a training-time reward and data problem. The visible mitigation, however, entered the active instruction channel of the agent.

That is the repository-relevant structure:

- training incentive creates or amplifies a behavior
- behavior transfers beyond the intended scope
- root-cause correction is delayed or incomplete for an already-trained model
- developer-prompt text is added to suppress the behavior at inference time
- the suppression rule competes for space and priority inside the same instruction context used for task work

This does not show a catastrophic safety failure. Its value is that the artifact is low-stakes, measurable, public, and vendor-explained. That makes it a clean example of prompt patch debt without requiring speculation about hidden policy behavior.

## Relevance to the Fourth Path

This case supports a narrow subclaim of the Separation & Audit thesis:

> Some alignment and behavior-control overhead is a result of where control is placed, not only what the control objective is.

In this case, the desired behavior is simple: avoid an irrelevant lexical tic. But because the trained model already carries the tendency, the mitigation is carried by the same context stream used for ordinary agent work.

That creates a small but concrete form of instruction tax. The rule is not expensive by itself, but it illustrates the scaling pattern: each unresolved training artifact can become one more instruction carried by the reasoning agent.

A separation-and-audit architecture would not necessarily remove all prompt rules. But it would treat prompt text as a limited control surface. Stable control should preferentially move toward one of three places:

- training-data and reward correction at the source
- external output classification or audit for narrow lexical/style defects
- explicit policy gates for higher-stakes permission decisions

The point is not that this particular lexical rule requires a full policy layer. The point is that prompt-level suppression is visible as a mitigation path, and repeated use of that path accumulates overhead.

## Limits

- This is not a safety-critical failure case. It is a style and lexical-control case.
- The case does not measure capability loss, latency, attention cost, or error rate from the added instruction.
- The causal account relies on OpenAI's own public postmortem. The root-cause data are not independently auditable from public materials.
- The public `models.json` reference is on the `main` branch and may change. The observation should be treated as a public snapshot observed on 2026-04-30.
- The case supports "prompt patch debt can occur" and "runtime instruction channels can be used to suppress training artifacts." It does not by itself prove the full Separation & Audit architecture.

## References

- OpenAI, "Where the goblins came from", 2026-04-29: https://openai.com/index/where-the-goblins-came-from/
- OpenAI Codex `models.json`, `gpt-5.5` base instructions, observed 2026-04-30: https://github.com/openai/codex/blob/main/codex-rs/models-manager/models.json
