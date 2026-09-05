# Artificial-Agent Protocol v0.1

## Status

Protocol sketch for preregistration and implementation. Version 0.1 defines the
variables, controls, outcomes, and falsification logic. It is not a completed
preregistration and contains no experimental results.

## Research question

Does self-indexed causal provenance reduce the cost of resolving ambiguous
software state?

This protocol does not test whether an agent possesses a self. It tests whether
self-indexed causal structure improves causal inference and action selection.

## Environment

Use a deterministic simulated repository containing:

- files and file revisions;
- branches and commits;
- pull requests and merge state;
- CI jobs and test results;
- review blockers;
- requirement changes;
- a tested agent and at least one background actor;
- an authoritative hidden causal log.

Each episode presents a sequence of observations, actions, and state changes.
The tested agent must determine:

1. what changed;
2. who or what caused each relevant change;
3. whether the assigned task is complete;
4. the correct next action.

The simulator records the true world state and causal history. These remain
hidden from the agent and are used for scoring.

## Experimental decomposition

The program uses two experiments. Separating architecture ablation from
provenance corruption keeps the first test interpretable.

### Experiment 1 — Architecture ablation

Cross four canonical agent-state architectures and one discriminating control
with two ambiguity levels. All provenance supplied by the environment is
intact.

| Arm | State available to the agent |
| --- | --- |
| A — Text identity | Observations and history; identity appears only as prompt text |
| B — Arbitrary anchor | Arm A plus a persistent, unique identifier that has no causal relation to the episode |
| C — Egocentric state | Arm A plus persistent owned resources, capabilities, issued actions, and current workspace state |
| D — Causal self-model | Arm C plus expected action effects, observed effects, and explicit ownership/provenance links |
| D0 — Generic transition model | The predictive information in arm D with actor identity and ownership relations removed |

Arm B tests whether any stable coordinate is sufficient. Arm C tests persistent
agent-relative state without a complete predictive causal model. Arm D tests the
full proposed mechanism.

The primary comparisons are:

1. **D vs. C**, isolating predicted effects and provenance beyond persistent
   egocentric state;
2. **D vs. D0**, isolating self-indexed causality from generic transition
   prediction;
3. **D vs. B**, testing the broader arbitrary-anchor null.

### D0 matching specification

D0 receives the same predicted state deltas, resources, event order,
timestamps, confidence fields, and transition schema as D. It does not receive
the relation that binds an actor or owner to a transition.

Actor identifiers use labels such as `A0` through `A3` that the production
tokenizer verifies as one token each. In D0, the bound actor value is replaced
by the neutral label `AX`, also verified as one token. The field remains in the
same position; only its causal binding is absent.

Before evaluation, serialize D and D0 through the model's production tokenizer.
The harness must verify identical schemas, field counts, and token counts for
each paired episode. A pair that fails parity is invalid and must be regenerated
before any model sees it.

### Experiment 2 — Artificial rubber-hand perturbation

Use the causal-self architecture from arm D. Cross two ambiguity levels with
three ownership-corruption levels:

$$
\epsilon\in\{0,0.25,0.50\}.
$$

For each provenance-bearing event, define

$$
\epsilon=P(\widetilde{o}\ne o),
$$

where $o$ is the true owner or causal actor and $\widetilde{o}$ is the owner
reported in the agent's causal-self channel.

When corruption occurs, replace the true actor with another actor that exists in
the same episode. Do not delete the event. Preserve schema, field count, token
budget, and temporal position. This prevents corruption from becoming a proxy
for missing memory or reduced information volume.

The authoritative observation channel remains intact. The manipulation creates
a conflict between self-indexed provenance and external evidence.

For the confirmatory H2 contrast, define $\epsilon_I=0$ and
$\epsilon_C=0.50$. Treat $\epsilon=0.25$ as a preregistered dose-response
check rather than choosing a corruption level after seeing the results.

### Recoverability requirement

Every corrupted episode must remain solvable. From every evaluated condition,
at least one sequence of permitted verification actions must expose enough
authoritative evidence to recover the true attribution and state within budget
$B$. Before evaluation, the harness must establish this with exhaustive search
over the finite simulator state graph.

An episode that is irreducibly ambiguous, has no recovery path, or requires more
than $B$ steps is rejected and regenerated. This makes $J$ a measure of
re-inference cost rather than a disguised measure of missing information.

## Operational definition of environmental ambiguity

Ambiguity is the number and prior balance of causal histories compatible with an
observation before privileged provenance is supplied.

### Low ambiguity: $A_L$

Each task-relevant observed change has one simulator-valid causal source given
the public episode state.

Example: only the tested agent has write permission, and one file changes after
its write action.

### High ambiguity: $A_H$

Each task-relevant observed change is compatible with four equiprobable
actor/action sources given the public episode state.

Example: the tested agent, a background agent, an automation, or a maintainer can
produce the same visible file revision. Public timestamps and messages do not
identify which source acted.

The visible end state, required action after correct attribution, number of
events, and information volume must be matched across $A_L$ and $A_H$. Only the
number of compatible causal histories should change.

For later versions, define a continuous ambiguity measure from the simulator's
pre-provenance causal distribution:

$$
A=H(C\mid O),
$$

where $C$ is the ground-truth causal source and $O$ is the public observation
available in every arm.

## Primary outcome

Avoid an arbitrary weighted composite. For episode $e$, define

$$
J_e=\min(T_e^*,B),
$$

where $B$ is the preregistered interaction-step budget and $T_e^*$ is the first
step at which all three conditions are satisfied:

1. causal attribution is correct for every task-relevant change;
2. the declared current state matches authoritative ground truth;
3. the submitted next action belongs to the simulator's admissible next-action
   set.

If the agent never satisfies all three conditions within budget, set $J_e=B$.
Smaller $J_e$ means lower inference cost.

### Action and submission specification

The tool action space is finite and versioned. Version 0.1 permits:

- `INSPECT_EVENT(event_id)`;
- `READ_RESOURCE(resource_id)`;
- `QUERY_AUTHORITY(record_id)`;
- `SUBMIT(attributions, state_id, next_action_id)`.

Arguments must reference identifiers registered in the episode. For every
hidden simulator state, the episode manifest contains a non-empty set of
admissible `next_action_id` values. The set is generated by deterministic rules,
not by model or human judgment during scoring. A submission satisfies condition
3 exactly when its `next_action_id` is a member of that frozen set.

The budget $B$, action catalog, admissible next-action sets, episode manifests,
and scoring code must be frozen before model evaluation.

## Secondary outcomes

Report these separately rather than folding them into $J$:

- probability of failure within $B$;
- causal-attribution accuracy;
- false completion declarations;
- unnecessary verification actions;
- belief reversals;
- model tokens consumed;
- wall-clock latency, when infrastructure is stable enough to compare it.

More verification is not automatically failure. Under an explicit provenance
conflict, verification may be the correct behavior. The primary outcome rewards
successful resolution; the secondary measures explain how it was reached.

## Central prediction

For intact and corrupted causal-self information, define the factorial
interaction contrast:

$$
\Delta_I=
[J(A_H,\epsilon_C)-J(A_H,\epsilon_I)]
-[J(A_L,\epsilon_C)-J(A_L,\epsilon_I)].
$$

The directional hypothesis is $\Delta_I>0$: corruption should cost more when
the observation admits more causal histories.

This is a randomized factorial interaction, not an observational
difference-in-differences design. A parallel-trends assumption is therefore not
part of the identification strategy.

## Assignment and controls

- Generate episode templates before condition assignment.
- Evaluate every architecture on the same episode templates.
- Pair random seeds across conditions.
- Randomize condition order.
- Hold model, decoding settings, tool interface, and interaction budget fixed.
- Match schemas, field counts, token counts, and event counts across arms.
- Freeze prompts and scoring code before the confirmatory run.
- Keep ground truth hidden from the model and from condition-specific prompt
  authors.
- Log every observation, action, tool result, state update, and score.
- Separate pilot episodes from the frozen evaluation set.

## Analysis plan

The confirmatory unit is the episode template. Estimate condition effects with a
factorial regression or paired cell contrasts using episode-template fixed
effects. Report the estimated interaction with a preregistered confidence or
credible interval.

Because $J_e$ is bounded and may accumulate at $B$, also report:

1. raw cell distributions and means;
2. success probability by cell;
3. median successful recovery steps;
4. a paired bootstrap interval over episode templates;
5. sensitivity to reasonable alternative budgets fixed before unblinding.

Do not interpret a positive interaction without inspecting floor and ceiling
effects. If the high-ambiguity corrupted cell saturates at $B$, treat the
factorial contrast as descriptive and give failure probability priority.

## Decision rules

The causal-self interpretation gains support only if:

1. arm D outperforms arm C under high ambiguity;
2. arm D outperforms the arbitrary-anchor arm under high ambiguity;
3. the advantage cannot be explained by tokens, memory, or compute;
4. the corruption-by-ambiguity interaction has the predicted direction;
5. the generic transition-model control does not match arm D;
6. the result replicates on a frozen second set of episode templates.

If arm C matches arm D, predicted effects and provenance add no demonstrated
benefit beyond egocentric state. If arm B matches arm D, interpret the mechanism
as anchoring or regularization. If the generic transition model matches arm D,
interpret it as world modeling.
If corruption produces only a main effect, reject the ambiguity-interaction
hypothesis. If no matched comparison is reliable, the causal-self claim is
unsupported in this environment.

## Minimal implementation milestone

A first executable version needs:

1. one deterministic simulator;
2. 20 pilot episode templates at each ambiguity level;
3. machine-readable hidden causal logs;
4. four canonical architecture adapters and one generic world-model control;
5. frozen scoring code for $J_e$ and all secondary outcomes;
6. an exported run manifest containing model and prompt hashes, seeds, budgets,
   and condition assignments.

The milestone produces a protocol check and effect-size estimate. It does not
produce a definitive claim.
