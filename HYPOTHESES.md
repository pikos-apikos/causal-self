# Falsifiable Hypotheses

## Status

Working hypotheses for the artificial-agent experiments. These statements are
claims to test, not conclusions.

## Scope

The target mechanism is a persistent, self-indexed causal structure that links
an agent's intentions and actions to predicted and observed effects. The word
`self` is used as an architectural label. It carries no claim about
consciousness, phenomenology, or personhood.

The first implementation is specified in
[the artificial-agent protocol](protocols/artificial-agent-v0.1.md).
That protocol is canonical for operational definitions, arm specifications, and
scoring. The compact definitions below register the claims; they do not replace
the protocol.

## H1 — Causal provenance improves attribution

When several causal histories are compatible with the same observation, an
agent with intact self-indexed action provenance will reach the correct causal
attribution with lower inference cost than an otherwise matched egocentric-state
agent that lacks predicted effects and provenance links.

This hypothesis is falsified if the provenance condition does not improve the
preregistered primary outcome after information volume, context length, model,
and inference budget are held constant.

## H2 — The benefit grows with ambiguity

Let $A_L$ and $A_H$ denote low and high environmental ambiguity. Let
$\epsilon_I$ and $\epsilon_C$ denote intact and corrupted causal-self
information. Let $J$ be the preregistered scalar inference-cost outcome, with
larger values indicating greater cost.

The predicted factorial interaction contrast is

$$
\Delta_I=
[J(A_H,\epsilon_C)-J(A_H,\epsilon_I)]
-[J(A_L,\epsilon_C)-J(A_L,\epsilon_I)]>0.
$$

The claim is about the interaction. Main effects of ambiguity or corruption do
not establish it.

This hypothesis is falsified if $\Delta_I$ is zero or negative within the
preregistered uncertainty criterion. Raw cell distributions must also be
reported so that floor, ceiling, and scale effects remain visible.

## H3 — An arbitrary anchor is insufficient

A stable but causally irrelevant identifier should not match the benefit of a
self-indexed causal model under high ambiguity.

This is the gauge-anchor control. If an arbitrary stable anchor performs as
well as the causal self-model, the result supports coordinate fixing,
regularization, or memory organization. It does not support a distinct role for
causal self-structure.

## H4 — A generic world model is insufficient

A predictor of state transitions that lacks ownership and action provenance
should not fully match a predictor that represents who acted, what effect was
expected, and whether the observed effect followed.

If the generic transition predictor matches the causal self-model, the useful
mechanism is world modeling rather than self-indexed causality.

## H5 — Provenance conflict should remain explicit

When action-derived expectations conflict with authoritative external evidence,
the causal self-model should preserve the conflict until attribution is
resolved. It should not silently overwrite either source.

The measurable prediction is fewer false completion declarations and higher
causal-attribution accuracy, even if the agent spends more verification steps on
conflicted episodes.

## Interpretation matrix

| Result | Supported interpretation |
| --- | --- |
| H1 and H2 hold; H3 and H4 controls remain weaker | Evidence for a specific computational role of self-indexed causal structure |
| Egocentric state matches the causal self-model | Persistent self-relative state is sufficient; predicted effects and provenance add no demonstrated benefit |
| Arbitrary anchor matches the causal self-model | Gauge fixing or regularization is sufficient |
| Generic world model matches the causal self-model | Transition prediction is sufficient |
| Provenance helps equally at low and high ambiguity | Provenance has a main effect; the ambiguity-interaction claim fails |
| Gains disappear after token and memory matching | Extra information capacity explains the result |
| No reliable gains | The proposed mechanism is unsupported in this task family |

None of these outcomes answers whether an artificial agent possesses a self.
They identify which computational structure, if any, reduces the cost of causal
inference.
