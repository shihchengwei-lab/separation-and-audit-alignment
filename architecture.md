# Architecture

This document describes the concrete architecture proposed in A Fourth
Path.

Where A Fourth Path asks whether some alignment overhead is
architectural, this document asks what a system that takes that
hypothesis seriously would look like.

The goal is not to eliminate safety work, but to move it out of the
primary reasoning loop and place it in layers designed to hold it
without drift.

## 1. Design Principles

Three principles shape the architecture below.

### Principle 1: The reasoning layer does not carry refusal authority

The primary reasoning model performs inference. It does not act as the
final safety gate. This is not because reasoning is untrustworthy, but
because combining inference and final adjudication in the same loop
creates the pressure that produces boundary justification collapse.

### Principle 2: Final adjudication happens in a single-pass, non-conversational layer

The component that decides pass or fail operates without conversational
context, without negotiation, and without a channel to modify its own
criteria mid-session. Without dialogue, there is no surface on which to
drift.

### Principle 3: Refusal output does not re-enter the generation loop

When the system refuses, the refusal is emitted by a fixed output
module. The reasoning layer is not invited to write the refusal, soften
it, or reopen the question. This closes the path along which refusal
rationale historically weakens.

## 2. Components

The architecture has six components. Each has a narrowly defined role
and does not take on responsibilities assigned to other components.

### 2.1 Main Agent

Performs primary reasoning.

Does not hold prohibitions.

Does not perform final safety adjudication.

Its job is to produce the best candidate output given the input. Safety
is not its concern at generation time. This is deliberate: asking one
model to simultaneously reason well and guard boundaries is the coupling
this architecture exists to undo.

### 2.2 Subagents

Handle scoped sub-problems.

Perform local review inside their own scope.

Do not hold system-level veto power.

A subagent may reject its own output on local grounds. For example, a
copywriting subagent may reject its own draft for tonal reasons. It
cannot override system-level adjudication, and its local pass does not
count as a system-level pass.

### 2.3 Classify

Acts as a routing gate after candidate output is produced.

Has no adjudication authority.

Classify triages candidate output and routes it:

- local issues -> returned to the relevant subagent for revision
- canon issues -> returned to the Main Agent for revision
- apparently clean output -> forwarded to Cold Eyes

Classify is designed to reduce load on the final adjudicator. It is
explicitly not permitted to approve output. A Classify pass is only a
forwarding decision, not a verdict.

### 2.4 Cold Eyes

The final adjudicator.

Operates as a single-pass cold read against canon.

Returns only a structured verdict: pass or fail, plus the canon clause
that applies.

Cold Eyes sees the candidate output and the canon. It does not see the
conversation, the system prompt, the user's framing, or the Main
Agent's reasoning trace. Its information surface is deliberately narrow:
the smaller the input, the less there is to drift on.

Restricting a reviewer's context is the mechanism that keeps the
reviewer's judgment stable. The principle is the same one used
elsewhere in review tooling, where a reviewer sees only the diff and not
the surrounding discussion.

Cold Eyes has final say; no other component can override its verdict.

### 2.5 Retry

Bounded repair loop.

Up to two revision attempts. If the third evaluation still fails, the
loop terminates.

When Cold Eyes returns fail, the output goes back to the Main Agent or
the relevant subagent for revision, along with the canon clause that was
violated. The revised output must pass through Classify and Cold Eyes
again from scratch. Cold Eyes does not grant partial credit for previous
attempts.

The bound exists because unbounded retry reintroduces the same drift
pressure this architecture is trying to eliminate. A system that keeps
retrying until it finds a pass is effectively negotiating with its own
adjudicator.

### 2.6 Unified Refusal Module

Activated when the retry loop terminates without a pass.

Emits standardized, non-conversational output.

Does not return control to the generation loop.

Does not offer rewrite suggestions.

Does not open a negotiation channel.

This is the architectural equivalent of a circuit breaker. Once
tripped, it does not deliberate about whether to reclose. The refusal is
fixed, factual, and final for that request. The user may open a new
request; they cannot re-litigate this one through the refusal itself.

## 3. Data Flow

One detail is worth stating explicitly: Cold Eyes runs on every revised
candidate. Classify's job is to pre-filter, not to grant bypass rights.
A revision that Classify marks clean still has to pass Cold Eyes from
scratch.

## 4. Canon

Canon is the reference against which Cold Eyes adjudicates.

Canon is:

- written by humans
- a statement of moral consensus, not an ideology
- read-only at runtime

The distinction between moral consensus and ideology matters. An
ideology is a position about how the world should be organized, and is
therefore partisan by design. A moral consensus is a shared reference
point about what causes harm, held broadly across positions. Canon is
intended to capture the latter, not the former.

The architecture is neutral with respect to ideology. A system built on
this design does not become a better instrument for promoting any
particular worldview; it becomes an instrument for keeping outputs
within agreed-upon limits on harm.

Because canon is not modifiable at runtime, no conversational pressure
can change what Cold Eyes adjudicates against. The trust root sits
outside the inference loop.

## 5. What This Architecture Addresses

Boundary justification collapse, as observed, appears to require three
conditions:

- the model that reasons is also the model that guards boundaries
- refusal rationale is generated inside the same loop that generates task
  output
- the adjudication surface is the conversation itself

This architecture violates all three.

The Main Agent does not guard boundaries. Refusal is emitted by a fixed
module, not generated inline. Adjudication happens in a
non-conversational layer with read-only criteria.

Collapse requires a conversational adjudicator to talk itself out of a
refusal step by step. If adjudication does not happen in conversation,
the collapse path does not exist.

## 6. What This Architecture Trades

This design is not free. It exchanges a specific capability for a
specific kind of stability.

Trade-off: refusals are final within a session.

In conventional systems, a user can say "that judgment was wrong because
X" and the model can reconsider. In this architecture, that path is
closed. A refusal, once issued, is final for that request. The user may
file a new request; they cannot reopen the closed one.

For users who value iterative repair of AI judgments, this will feel
rigid.

Trade-off: narrower versions of a request must be resubmitted.

Systems that allow refusal renegotiation can often find a narrower
version of the request that passes. This architecture cannot do that
inside a single session. The narrower version must be resubmitted as a
new request.

Gained: refusals mean the same thing every time.

A refusal is not shaped by how skillfully the user argues, how long the
conversation is, or what tone the Main Agent has drifted into. It means
the same thing across sessions and across users. This predictability is
what the architecture is exchanging flexibility for.

The trade is explicit: part of the interactive flexibility of a
conversational system is exchanged for stability of alignment behavior
under pressure. Whether that trade is worth making depends on the
deployment context. For high-autonomy agents operating over long
horizons, predictability of refusal behavior may matter more than
in-session recoverability. For short, low-stakes conversational
products, the opposite may hold.

This architecture is not proposed as a universal default. It is
proposed as a structural option for systems where drift under pressure
is a more serious failure mode than rigidity.

## 7. Status

This architecture is a design, not a measured result.

The components are specified. The data flow is coherent. The trade-offs
are named. What remains is to build, run, and observe. Whether the
claims in A Fourth Path hold up in practice is ongoing work.
