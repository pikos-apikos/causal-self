# Who Is the Viewer?

## Constraint Computation, Causal Self-Models, and the Geometry of Inference

### Status: research hypothesis / working note

This note does **not** claim that consciousness has been explained, that
biological perception is literally an equilibrium computer, or that self-models
are necessary for intelligence.

It records a narrower hypothesis intended to be testable across dynamical
systems, neuroscience, and autonomous AI:

> **A structural causal self-model may reduce the computational cost of
> inference by constraining causal uncertainty and reducing the admissible state
> space.**

## 1. Computation is not necessarily a trajectory

The usual picture of computation is sequential:

```text
input -> state_0 -> state_1 -> state_2 -> ... -> answer
```

or, more generally,

$$
x_{t+1}=F(x_t).
$$

Some computations can instead be represented as systems of simultaneous
constraints:

$$
C_i(z,x)=0, \qquad i=1,\ldots,n,
$$

with physical or numerical dynamics

$$
\dot z=G(z,x)
$$

that move the system toward a consistent state or metastable region.

This gives two useful computational views:

```text
trajectory: input -> sequence of state transitions -> output
constraint: input -> constraint landscape -> relaxation -> consistent state
```

The second representation does not make computational hardness disappear. It
changes the cost model. Sequential depth may be displaced into relaxation time,
precision, energy, component count, topology, spectral gaps, metastability,
noise sensitivity, or readout cost.

We use **Complexity Displacement Principle** as a working name for this
observation:

> Changing computational substrate or representation may move complexity into
> a different physical or dynamical quantity rather than remove it.

This is a heuristic principle, not a proved conservation law.

## 2. Temporal depth can become constraint topology

Consider a bounded computation:

$$
C_0 \rightarrow C_1 \rightarrow C_2 \rightarrow \cdots \rightarrow C_n.
$$

Instead of executing the sequence directly, introduce variables for all
configurations and constrain adjacent states:

$$
C_{t+1}=\delta(C_t).
$$

The complete computation can then be represented as

$$
\Phi(C_0,C_1,\ldots,C_n)=0.
$$

A satisfying assignment encodes a valid computation history. This is closely
related to the tableau construction underlying Cook's theorem: a temporal
computation can be encoded by local consistency constraints over a larger
structure.

$$
\boxed{\text{temporal depth} \longrightarrow \text{constraint topology}}
$$

This does not exceed Turing computability. More precisely, a *problem* is not
"Turing complete"; a computational model is Turing complete if it can simulate
a universal Turing machine. A constraint-relaxation model can be universal when
it can represent unbounded memory, conditional state updates, and repeated
transitions, or faithfully encode those transitions in its constraints.

Two systems may therefore be computationally universal while having radically
different computational costs.

> **Turing equivalence says what can be computed. It says much less about the
> geometry or physical cost of finding the answer.**

## 3. Perception as metastable constraint satisfaction

A feed-forward metaphor for perception implicitly creates a regress:

```text
world -> neural representation -> internal image -> viewer?
```

A different possibility is that perception is not the production of an internal
image for another subsystem to inspect.

> **Perception may be recurrent constraint relaxation toward metastable
> consistency.**

The system continuously reconciles coupled variables such as

$$
z=(W,B,M,S,A),
$$

where:

- $W$: inferred world state;
- $B$: bodily state;
- $M$: memory and context;
- $S$: self-relative or perspectival state;
- $A$: possible or current action.

The resulting percept need not be a fixed point. A biological system may move
among transient, metastable attractors while continuously receiving new input.
Energy-based neural dynamics provide an established example of computation by
convergence, but they do not by themselves establish this perceptual claim.

This reframes the topology of the viewer problem:

```text
viewer -> coordinate system -> constraint -> symmetry breaking -> stability
```

The self need not sit outside the solution and observe it. It may participate in
the construction of the solution.

## 4. The self as a computational constraint

The strong statement "the self is the boundary condition required for
perception" is more than the current argument earns. The falsifiable version is:

> **A self-model may act as a dynamically maintained constraint that reduces
> perceptual degeneracy and causal uncertainty.**

Arbitrary coordinate fixing can also remove symmetries. The real question is
therefore:

> **Does an embodied and causal self-model provide computational benefit beyond
> arbitrary gauge fixing?**

A structural self-model could include

$$
S_t=(\text{ownership},\text{capability},\text{intention},
\text{causal history},\text{expected effects}).
$$

For an artificial software agent, its "body" need not be physical. Its
computational body can consist of the current process, workspace, branch, owned
resources, available tools, permissions, issued actions, expected effects,
observed effects, and persistent memory.

That is fundamentally different from a prompt saying `You are Agent X`.
Identity in text is metadata. A causal self-model is part of the state-transition
dynamics.

## 5. Agency as a causal filter

Suppose an observed world change $\Delta W$ could have many causes:

$$
C=\{c_1,c_2,\ldots,c_n\}.
$$

Without knowledge of the agent's own action, causal uncertainty
$H(C\mid\Delta W)$ may be high. If the agent also knows what it intended,
which action it issued, what consequences it expected, and what resources it
controlled, then under suitable conditions:

$$
\boxed{H(C\mid\Delta W,A_t,S_t)<H(C\mid\Delta W)}.
$$

This gives a computational interpretation of agency:

> **Agency may reduce causal uncertainty.**

Instead of asking only "What changed?", the system asks "What changed, given
what I just did?" The latter question can reduce the hypothesis space.

A related working hypothesis follows:

> **Artificial selfhood may begin as provenance before it becomes anything
> resembling phenomenology.**

## 6. State without provenance is evidence soup

This becomes concrete in software engineering agents. A coding agent may
observe:

```text
commit exists
tests pass
review blocker remains open
integration test fails
requirement changed
deployment is absent
```

A language model can still summarize this as `implementation complete` because
the evidence is present but its authority and causal relationships are not
structurally represented.

A stronger state model records:

```text
my action
  -> expected state transition
  -> observed evidence
  -> causal attribution
  -> authoritative current state
```

For example:

```text
I changed files X and Y.
I created commit H.
I opened pull request P.
Review R blocks P.
CI job J currently fails.

Therefore:
implementation exists,
but the task is not complete.
```

Here, `I` is not a claim of consciousness or moral personhood. It is a
provenance key.

## 7. The falsification experiment

Keep the model, task, compute budget, and environment constant. Change only the
anchoring mechanism.

### A. Context viewer

The model receives observations and history. Its identity exists only as text.

### B. Arbitrary gauge anchor

The model receives a stable but arbitrary coordinate reference. If this solves
the problem as well as a causal self-model, then selfhood is unnecessary;
ordinary gauge fixing or regularization was sufficient.

### C. Egocentric state

The system maintains persistent agent-relative state:

$$
S_t=(\text{pose},\text{resources},\text{capabilities},
\text{action history},\text{ownership}).
$$

### D. Causal self-model

The agent additionally models

$$
A_t \rightarrow \Delta S \rightarrow \Delta W \rightarrow O_{t+1}.
$$

It predicts consequences of its actions and compares them with observations.

## 8. Artificial rubber-hand perturbations

The causal self-model can be deliberately corrupted:

- **False ownership:** another actor changes a resource, but the event is
  attributed to the tested agent.
- **Stolen agency:** the agent acts, but provenance attributes the resulting
  state change to another actor.
- **Proprioceptive conflict:** the agent predicts `branch = feature-x` while
  authoritative observation reports `branch = main`.
- **Action/result inconsistency:** the action log records success while the world
  lacks the expected effect.

A robust causal agent should not silently overwrite one belief with another. It
should represent

$$
C_{\text{agency}}\ne C_{\text{external evidence}}
$$

and treat attribution as an unresolved inference problem. The name is an
analogy to bodily-ownership perturbations such as the rubber-hand illusion; it
is not a claim of biological equivalence.

## 9. The central interaction prediction

Let $A$ represent environmental ambiguity and $\epsilon$ represent corruption
of self/causal integrity. Record an inference-cost vector:

$$
\mathbf{K}=
(T_{\text{recover}},H,N_{\text{verification}},N_{\text{revisions}},
E,P_{\text{failure}}).
$$

Because a vector has no intrinsic scalar ordering, the experiment must
preregister one scalar primary outcome $J$ (for example, recovery steps) or a
fully specified scalar composite derived from $\mathbf{K}$. Let $A_H,A_L$
denote high and low ambiguity, and let $\epsilon_C,\epsilon_I$ denote corrupted
and intact causal-self integrity. The main prediction is a positive factorial
interaction contrast:

$$
\boxed{
\Delta_I=
[J(A_H,\epsilon_C)-J(A_H,\epsilon_I)]
-[J(A_L,\epsilon_C)-J(A_L,\epsilon_I)]>0
}.
$$

If $A$ and $\epsilon$ are instead continuously varied and $J$ is smooth, the
corresponding local prediction is

$$
\frac{\partial^2 J}{\partial A\,\partial\epsilon}>0.
$$

When the environment is easy, corruption of the self-model may matter little.
As environmental ambiguity increases, causal integrity should become
increasingly valuable.

The same experimental skeleton can be instantiated in two substrates:

```text
biological: world ambiguity x bodily-self consistency
artificial: environment ambiguity x causal-self integrity
```

A similar qualitative interaction would not prove that artificial agents
possess human-like selves. It would support a narrower claim:

> **Self-like constraints may solve a generic computational problem shared by
> biological and autonomous artificial systems.**

Potential signatures such as critical slowing down, increased entropy, or
additional belief revisions are secondary measurements, not assumptions built
into the result.

## 10. Falsifiers and discriminating outcomes

The proposal loses explanatory force if any of the following hold under a
well-controlled implementation:

1. an arbitrary stable anchor performs as well as a causal self-model across
   ambiguity levels;
2. provenance helps only because it adds more tokens, memory, or compute;
3. causal-self corruption produces no interaction with environmental
   ambiguity;
4. the effect disappears when evidence authority and ordinary state management
   are controlled;
5. a simpler non-self causal model accounts for the same gains.

These outcomes would still be informative. They would relocate the useful
mechanism from selfhood to gauge fixing, regularization, memory, provenance, or
causal modeling in general.

## Seven working principles

1. **Computation need not be only trajectory.**
2. **Some computation can be relaxation under constraints.**
3. **Perception may be metastable constraint satisfaction.**
4. **A self-model may restrict the admissible state space.**
5. **Agency may provide causal gauge-fixing.**
6. **The self may be computationally useful before it is phenomenologically interesting.**
7. **A self may first emerge as an efficient solution to causal uncertainty.**

## Central research question

> **Does a structural causal self-model make some classes of inference
> computationally easier?**

If the answer is no, the hypothesis fails in an informative way. If an
arbitrary coordinate anchor performs as well as a causal self-model, then the
relevant mechanism is probably gauge fixing or regularization rather than
selfhood. If causal self-models show a growing advantage as ambiguity increases,
then agency, ownership, and provenance may be computational structure rather
than merely descriptive metadata.

## One-line thesis

> **Intelligence may depend on the structure that makes distinctions possible.**

The original philosophical question remains:

> Who is the viewer?

A possible answer is not another entity inside the system. The "viewer" may be
the system's own causal and perspectival anchoring of the state it is trying to
resolve.

That possibility is philosophically interesting. The engineering hypothesis
comes first.

## Related foundations

These references establish nearby ideas; they do not imply that the present
hypothesis follows from them. See [RELATED_WORK.md](RELATED_WORK.md) for the
nearest conceptual neighbors and the proposed boundary of the contribution.

1. Stephen A. Cook, “The Complexity of Theorem-Proving Procedures,” *STOC '71*,
   1971. <https://doi.org/10.1145/800157.805047>
2. John J. Hopfield, “Neurons with graded response have collective computational
   properties like those of two-state neurons,” *PNAS* 81(10), 1984.
   <https://doi.org/10.1073/pnas.81.10.3088>
3. Matthew Botvinick and Jonathan Cohen, “Rubber hands 'feel' touch that eyes
   see,” *Nature* 391, 1998. <https://doi.org/10.1038/35784>
4. Karl Friston, “The free-energy principle: a unified brain theory?”, *Nature
   Reviews Neuroscience* 11, 2010. <https://doi.org/10.1038/nrn2787>
