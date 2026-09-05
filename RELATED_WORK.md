# Related Work and Contribution Boundary

## Status

This is a map of the nearest prior ideas, not a comprehensive literature review.
Its purpose is to prevent a new vocabulary from hiding an old mechanism.

## Nearest neighbors

| Area | Established idea | Relation to this project |
| --- | --- | --- |
| Reafference and efference copy | A copy of a motor command helps distinguish self-produced sensory change from externally produced change. | This is a direct biological precedent for using action information in causal attribution. The present proposal does not claim to originate that mechanism. |
| Forward and internal models | A system predicts the sensory consequences of action and compares prediction with incoming evidence. | The causal-self arm uses this structure. Its additional commitment is explicit ownership and durable provenance across software actions and authoritative state. |
| Sensorimotor accounts | Perception depends on structured relations between action and sensory change. | This supports treating perspective as an enacted constraint rather than an inner spectator. It does not establish the proposed artificial-agent interaction. |
| Active inference | Perception and action can be formulated as inference under a generative model. | The current experiment isolates a narrower question: whether self-indexed causal variables add value beyond a matched generic model. |
| World models and Dyna | Learned transition models support prediction, planning, and action. | These are strong null models. If generic transition prediction matches the causal-self arm, the result belongs here. |
| Body ownership | Multisensory consistency and conflict alter the attribution of a body or limb to oneself. | The artificial "rubber-hand" perturbation borrows the experimental logic while making no claim of biological equivalence. |
| Computational provenance | Provenance models represent entities, activities, agents, and derivation relations. | This project asks whether provenance improves online inference and control, rather than serving only audit, interchange, or retrospective explanation. |

## What would merely rename prior work?

The statement **"agency can reduce causal uncertainty"** is not new. Reafference,
efference-copy, and forward-model theories already explain how action-related
signals can disambiguate self-caused and externally caused change.

The statement **"predicting consequences helps an agent act"** is also not new.
Model-based reinforcement learning and world-model research already establish
the value of transition prediction.

The project earns a distinct contribution only if the following combination
survives experiment:

1. causal provenance is represented explicitly across persistent software
   state;
2. a causally irrelevant stable anchor is included as a control;
3. the benefit of intact provenance grows as environmental ambiguity grows;
4. a matched generic world model does not explain the entire effect;
5. the same interaction structure can be meaningfully tested in another
   substrate without claiming equivalence between substrates.

If those conditions fail, the vocabulary should collapse back to the nearest
established account: forward modeling, world modeling, provenance, memory, or
regularization.

## Proposed contribution boundary

The proposed contribution is an experimental decomposition:

$$
\text{stable anchor}
\quad\text{vs.}\quad
\text{generic transition model}
\quad\text{vs.}\quad
\text{self-indexed causal provenance},
$$

tested across controlled levels of causal ambiguity.

The central object is not a conscious observer. It is the structure that makes
causal distinctions available to the system.

## References

1. Erich von Holst and Horst Mittelstaedt, “Das Reafferenzprinzip,”
   *Naturwissenschaften* 37, 1950, pp. 464–476.
   <https://doi.org/10.1007/BF00622503>
2. Daniel M. Wolpert, Zoubin Ghahramani, and Michael I. Jordan, “An Internal
   Model for Sensorimotor Integration,” *Science* 269(5232), 1995,
   pp. 1880–1882. <https://doi.org/10.1126/science.7569931>
3. Rick Grush, “The Emulation Theory of Representation: Motor Control, Imagery,
   and Perception,” *Behavioral and Brain Sciences* 27(3), 2004,
   pp. 377–396. <https://doi.org/10.1017/S0140525X04000093>
4. J. Kevin O'Regan and Alva Noë, “A Sensorimotor Account of Vision and Visual
   Consciousness,” *Behavioral and Brain Sciences* 24(5), 2001,
   pp. 939–973. <https://doi.org/10.1017/S0140525X01000115>
5. Karl Friston, Jean Daunizeau, James Kilner, and Stefan J. Kiebel, “Action and
   Behavior: A Free-Energy Formulation,” *Biological Cybernetics* 102, 2010,
   pp. 227–260. <https://doi.org/10.1007/s00422-010-0364-z>
6. Richard S. Sutton, “Dyna, an Integrated Architecture for Learning, Planning,
   and Reacting,” *SIGART Bulletin* 2(4), 1991, pp. 160–163.
   <https://doi.org/10.1145/122344.122377>
7. David Ha and Jürgen Schmidhuber, “World Models,” 2018.
   <https://arxiv.org/abs/1803.10122>
8. Manos Tsakiris, “My Body in the Brain: A Neurocognitive Model of Body
   Ownership,” *Neuropsychologia* 48(3), 2010, pp. 703–712.
   <https://doi.org/10.1016/j.neuropsychologia.2009.09.034>
9. Tim Lebo et al., “PROV-O: The PROV Ontology,” W3C Recommendation, 2013.
   <https://www.w3.org/TR/prov-o/>

The next literature pass should cover recent agent-state, audit-trail, and
multi-agent provenance systems using the same standard: a work belongs here
only when its mechanism or control condition is close enough to change the
experimental design.
