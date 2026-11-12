# GLOSSARY — Dynamic Bucket Tree of Permutation (D-BTP)

**Project:** Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution  
**Document role:** Cross-document terminology and notation reference  
**Status:** Research vocabulary and specification companion, v1.0.0 draft  
**Scope:** Foundations D-BTP-001–008; SPEC-001–004; CASE-001–003; EXT-001–003

> **Reading convention.** This glossary distinguishes *defined research constructs*, *normative specification semantics*, and *hypotheses to be tested*. A named mechanism is not evidence that it has been implemented or empirically validated. Where terminology varies between papers, the four SPEC documents control their respective implementation contracts.

## 1. Quick orientation

**D-BTP** generalizes Bucket Tree of Permutation (BTP) from a structural matching/search formulation into a state-driven framework in which structural candidates can be generated during search, checked against constraints, prioritized by directional guidance, and revised using validated feedback. Its characteristic loop is:

```text
Current Bucket State
      |
      v
Dynamic Candidate Generation <---- Directional Field / Search Policy
      |
      v
Constraint Evaluation and Propagation
      |
      v
Accept / Exclude / Defer / Branch
      |
      v
Directional Ranking and Portfolio Control
      |
      v
Evidence Acquisition, Feedback, Relay
      |
      +----> Updated Bucket / Candidate Frontier
      +----> Evaluated Field or Operator Improvements
```

The loop is conceptual: implementations may interleave operations, and not every feedback event authorizes a change to the search policy. **Constraint validity and evidence reliability must not be inferred from a high directional score.**

## 2. Foundational structural terms

### BTP — Bucket Tree of Permutation

The antecedent structural search approach associated with assembling compatible node-pair or structural correspondence decisions. The name reflects branching among alternative combinations. **Static BTP** in this series is a comparison baseline with an initially enumerated candidate set; it is not a claim that every original BTP implementation was static. The original conception may include dynamic search behavior.

### D-BTP — Dynamic Bucket Tree of Permutation

A generalized, dynamically expanding structural hypothesis search framework. Candidate proposals depend on the current Bucket, structural context, constraints, evidence and directional policy. The term names a research architecture, not a claim of universal optimality or polynomial-time complexity.

### Bucket

A search-state unit recording a partial structural hypothesis and the information needed to extend, evaluate, audit, branch or terminate it. A Bucket is **not** merely a bag of candidate pairs. See **SPEC-001** for required state fields and lifecycle semantics.

### Dynamic Bucket State

A versioned snapshot of a Bucket's hypothesis decisions, structural composition, evidence, directional control references, candidate frontier and operational metadata. A useful conceptual shorthand is

$$
B_t=(H_t,S_t,E_t,P_t,M_t),
$$

where $H$ is the hypothesis ledger, $S$ structural state, $E$ evidence state, $P$ policy/directional references and $M$ metadata. This is **illustrative notation**, not a substitute for the canonical serialization in SPEC-001.

### Bucket Tree

A search graph or tree of Bucket states connected by candidate decisions or other authorized transitions. Deduplication or state merging may make the realized structure a directed acyclic graph; the historical name does not mandate a literal tree at runtime.

### Structural Hypothesis

A proposed configuration of entities, correspondences, relations, constraints and explanations. A hypothesis may be partial, competitive with alternatives, or underdetermined by current evidence.

### Structural Composition

The operation of combining accepted structural assertions into a coherent candidate explanation subject to applicable constraints. Composition can introduce new relations, derived requirements or conflicts.

### Starmap

A structural representation of entities/nodes and their relations, attributes or metric features. Starmaps can be observed, inferred or partially latent; matching two starmaps need not imply a bijection.

### Structural Correspondence / Match Pair

A candidate relation linking elements or substructures from different representations. It may represent equivalence, similarity, participation or another typed relation; its semantics must be explicit. A candidate match is **not** an accepted fact.

### Unaligned AND

A structural combination operation that seeks compatible relationships or common structure across representations without assuming prior alignment. In the BTP lineage it is associated with structural/metric similarity; D-BTP extends the search machinery beyond that original application.

### Metric Similarity / Metric Distance

Quantitative measures of resemblance or separation under a declared representation and metric. They can be search objectives, candidate-generation signals or components of directional scores; they are not universal proof of structural equivalence.

### Latent Structure

A structural element or relationship posited to explain observations but not directly observed. A latent actor in a blockchain case is a behavioral explanatory variable, not necessarily a named person.

### Structural Residual

An unexplained discrepancy, uncovered relation, constraint conflict or predictive error remaining under the current hypothesis. Residuals can motivate new candidates or representation changes, but their interpretation is itself uncertain.

## 3. Candidate generation and hypothesis decisions

### Candidate

A proposed structural assertion or operation available for evaluation. Candidates may be atomic (a relation or match) or composite (a split, merge, subgraph or coordinated set of assertions).

### Dynamic Candidate Generation

The process of constructing new candidates from the evolving Bucket and external or learned context. Abstractly,

$$
C_t=G(B_t;\theta_G,R_t),
$$

where $G$ is a generator, $\theta_G$ its versioned configuration, and $R_t$ accessible contextual resources. Generated candidates must retain identity and provenance.

### Candidate Frontier

The set or queue of generated candidates not yet fully resolved for the current search state. It is distinct from the frontier of Bucket states awaiting expansion.

### Search Frontier

The collection of Bucket states or work items eligible for future processing. Search control policies determine their priority, scheduling and budget allocation.

### Hypothesis Ledger

A traceable record of proposed assertions and decisions, including accepted, excluded, deferred, superseded or reopened entries as supported by the state contract. It enables explanation, replay and conflict analysis.

### Accept / Exclude

Branch decisions that respectively incorporate a candidate into a hypothesis or record its exclusion from that branch. Exclusion can be a search decision rather than a globally proven impossibility; the reason and scope must be recorded.

### Defer

Retain a candidate or decision for later examination without asserting acceptance or infeasibility. Deferment may reflect uncertainty, resource limits or unresolved dependencies.

### Reopen / Retract

Reconsider or withdraw a prior decision when new evidence, changed assumptions or a corrected plugin warrants it. Such operations require versioned provenance and must respect the governing transition contract.

### Constraint Propagation

Deriving consequences of current accepted decisions and constraints, such as eliminating incompatible candidates or narrowing domains. Only sound deductions under declared assumptions justify hard pruning.

### Structural Closure

A condition under which no further relevant candidate extension remains under a specified generation scope and closure contract. Closure is **relative to declared generator coverage and assumptions**, not an unconditional proof that no other explanation exists.

### Quiescence

A state with no immediately available work under the present generator or scheduling conditions. Quiescence is not necessarily closure: new evidence, a newly enabled plugin or a revised policy may produce work.

### Budget-Terminated Partial Result

A search state stopped because a time, compute, memory or other budget was exhausted. It is a partial result and must not be labeled an exhaustive solution.

### Conditional Completeness

A completeness statement valid only under explicit conditions, such as generator coverage, fair scheduling, sound constraints and adequate resources. D-BTP makes no unconditional completeness guarantee.

## 4. Constraints, feasibility and pruning

### Hard Constraint

A requirement that a valid structural composition must satisfy under declared assumptions. A demonstrated violation can justify rejecting the relevant branch, provided the checker is sound and its assumptions apply.

### Soft Constraint

A preference, penalty or graded measure affecting ranking, not logical admissibility. A poor soft score alone must not be treated as a hard contradiction.

### Conditional Constraint

A requirement activated only when specified antecedents, contexts or assumptions hold. The activation condition and its provenance must be recorded.

### Constraint Plugin

A versioned, capability-declared component that evaluates or propagates constraints over candidates and Bucket states. Plugin results must distinguish evaluated validity from unavailable or failed evaluation. See **SPEC-002**.

### Feasibility / Admissibility

Whether a proposed structural composition satisfies applicable hard constraints. **Feasible** means not ruled out under the current constraint model; it does not mean empirically true.

### Pass / Fail / Unknown / Error

Operational result categories for constraint evaluation. **Pass** means the evaluated constraint is satisfied; **Fail** means a demonstrated violation; **Unknown** means insufficient information; **Error** means evaluation could not be completed reliably. A plugin must not silently convert Unknown or Error into Fail.

### Sound Pruning

Removal of a branch only when a valid, applicable proof or logically sound constraint deduction establishes that the branch cannot meet the declared admissibility requirements.

### Heuristic Pruning / Search Suppression

Resource-driven decisions to deprioritize, pause or discard work because of low estimated value. These may improve efficiency but can lose feasible or optimal solutions; they must not be represented as sound infeasibility proofs.

### Non-Bijective Mapping

A correspondence allowing one-to-many, many-to-one or many-to-many relations where the domain model permits them. In actor attribution, one latent actor may be associated with multiple observed behaviors or addresses.

### Constraint Conflict / Unsatisfiable Core

A contradiction among accepted assertions and applicable hard constraints. An **unsatisfiable core** is a subset of assumptions or constraints sufficient to explain the conflict, if the implementation can produce one.

## 5. Directional intelligence and search control

### Directional Field

A structured, versioned collection of objectives, preferences, contextual signals, uncertainties and policy parameters used to guide what to generate, what to inspect next and where to allocate resources. It is broader than a single scalar score. See **SPEC-003**.

### Directional Scoring

An evaluation of a candidate or Bucket relative to one or more declared directions. Its outputs may include vectors, uncertainty bounds, evidence references and policy-specific aggregations.

### Multi-Directional Scoring

Evaluation against several objectives or perspectives, such as structural coherence, explanatory coverage, information gain, novelty, resource cost and evidential support. Objectives need not be commensurable or collapsed into one number.

### Generation–Selection Coupling

The feedback relationship in which directional guidance influences candidate generation as well as candidate ranking, while generated outcomes and verified evidence inform future guidance. This is not merely a one-way generate-then-score pipeline.

### Search Control Plane

The policy layer that governs work queues, prioritization, exploration diversity, budgets, scheduling and policy updates without overriding hard constraint semantics.

### Search Policy

A versioned rule or procedure for choosing search actions, including candidate generation, branch expansion, evidence acquisition and termination decisions.

### Exploration–Exploitation Trade-off

Balancing the examination of novel or uncertain possibilities against concentrating resources on currently promising hypotheses. No single balance is optimal for every task.

### Hypothesis Portfolio

A maintained collection of competing partial or complete explanations. Portfolios preserve alternatives and diversity rather than collapsing prematurely to one winner.

### Pareto Dominance / Pareto Frontier

For multiple objectives, one candidate dominates another when it is at least as good on every declared objective and strictly better on at least one, assuming consistent comparison direction. The Pareto frontier contains currently nondominated candidates; it does not establish truth.

### Directional Field Unit (DFU)

A proposed portable and versioned representation of a directional field, its objectives, calibration, applicability, provenance and validation history. Developed as an extension concept in **EXT-002**; not necessarily a mandatory wire format of SPEC-003.

### Field Frontier

A search frontier of proposed new or modified directional fields. It is conceptually separate from the frontier of structural hypotheses.

### Feedback

Information from search outcomes, new observations, tests or external evaluation. Feedback may update a Bucket, recalibrate a directional field or motivate operator changes, subject to governance and validation.

## 6. Evidence, uncertainty and responsible inference

### Evidence Record

A versioned, attributable record of an observation, measurement, testimony, derived signal or test result, including provenance, scope, quality and dependencies as applicable. See **SPEC-004**.

### Weak Evidence

A signal that may be informative for prioritizing hypotheses or evidence collection but is insufficient by itself to establish the claimed conclusion. Weak evidence can be useful without becoming a hard constraint.

### Directional Weak Evidence

Weak evidence whose value lies partly in suggesting *where to search* or *what to test next*, not merely in supporting a final assertion. Related research includes BM-ODWEI and REN.

### Counterevidence

Evidence tending to weaken or contradict a hypothesis, or favor a competing explanation. Systems should actively seek discriminating counterevidence, not only accumulate supportive signals.

### Evidence Provenance

The origin, acquisition method, transformations, custody, version and contextual limitations of evidence. Provenance enables audit and helps assess reliability and independence.

### Evidence Dependency Graph

A representation of shared sources, derived observations or causal/statistical dependencies among evidence records. Its purpose includes preventing double counting of correlated signals.

### Evidence Calibration

The empirical alignment between assigned confidence or likelihood values and observed frequencies or outcomes. Calibration must be tested; confidence labels alone do not demonstrate reliability.

### Evidence Acquisition / Active Sensing

Selecting an observation, query or experiment expected to reduce uncertainty or distinguish competing hypotheses. Its expected benefit should be weighed against cost, risk and permitted access.

### Information Gain

A measure of expected uncertainty reduction from an observation or action under a declared probabilistic or other uncertainty model. Estimated information gain is model-dependent.

### Behavioral Attribution

A hypothesis that observed actions or addresses may belong to a common latent behavioral actor or coordinated structure. It is not equivalent to identifying a real-world individual.

### Real-World Identity Attribution

An assertion connecting observed behavior to an identifiable person or organization. It requires independent, appropriate evidence and legal/ethical safeguards; structural similarity alone is insufficient.

### Privacy and Evidence Governance

Policies restricting collection, access, retention, relay and interpretation of evidence, especially when it could expose personal information. Auditability does not authorize indiscriminate surveillance.

## 7. Relay, multi-agent learning and RSI

### Agent

A computational participant that proposes, checks, challenges, ranks, relays or learns from structural hypotheses. Roles may be specialized but are not required to correspond to separate models or machines.

### Multi-Agent Hypothesis Competition

A process in which agents produce and test alternative explanations under shared or differing directional policies. Competition is useful when it improves coverage, error discovery or evidence discrimination—not merely because multiple agents agree.

### Structural Hypothesis Unit (SHU)

A proposed portable package of a hypothesis and its constraints, evidence, counterevidence, lineage, uncertainties and unresolved issues. The normative relay semantics are defined in **SPEC-004**.

### Structural Relay

The transfer of a structural hypothesis, evidence package, validated operator or other reusable intelligence artifact between agents, tasks or systems, with explicit provenance and receiving-side checks.

### Relay Envelope / Relay Receipt

Respectively, the metadata and content wrapper used to transmit a relay artifact, and a record of the receiver's handling, validation or rejection. Receipt does not imply acceptance of truth.

### Collective Structural Learning

Improvement through the accumulation, comparison, validation and reuse of structural findings across agents or tasks. It requires demonstrable transfer or adaptation, not merely shared storage.

### Recursive Self-Improvement (RSI)

A process in which a system modifies mechanisms that influence its future capability, and those modifications contribute to further improvement. In this series, **validated RSI** additionally requires controlled comparisons, independent evaluation, provenance, safety gates and rollback paths.

### Controlled RSI

A governed improvement lifecycle in which proposed policy, field, generator or operator changes are tested before deployment and monitored after deployment. Automatic self-modification alone is not proof of improvement.

### Structural Evolution Relay Unit (SERU)

An extension-level proposed artifact carrying a reusable structural invention, such as a representation change or generator improvement, with its contract, dependencies, evidence and validation status. See **EXT-003**.

### Conformance Before Runtime

The engineering principle of defining interfaces, state semantics, invariants and tests before treating an implementation as compliant. Conformance is not the same as scientific validation of claimed performance benefits.

## 8. Open-ended structural evolution

### Open-Ended Structural Evolution

The research objective of a system that can expand not only its candidate set but also its representational vocabulary, structural operators and transferable capabilities. Mere production of more candidates is insufficient.

### Hypothesis Frontier

The set of structural explanations currently available for expansion or testing.

### Representation Frontier

Candidate new entity types, relation types, abstractions or encoding schemes that may make previously inaccessible structures expressible.

### Operator Frontier

Candidate new or revised generation, composition, inference, pruning or control operators that may alter future search capability.

### Relay Frontier

Candidate structural artifacts or capabilities available for transfer, integration and validation across agents or tasks.

### Operator Evolution

Proposing, testing and potentially adopting changes to algorithms that generate, compose, evaluate or search hypotheses. A changed operator is not automatically a better one.

### Residual-Driven Invention

Using persistent explanatory gaps, failures or structural mismatches to propose new relations, representations or operators. Such inventions remain hypotheses until evaluated.

### Open-Endedness Boundary

A limitation imposed by representation, generators, data access, computation, evaluation, governance or the external environment. A finite demonstration does not establish unbounded open-endedness.

## 9. Symbols and notation

| Symbol | Intended meaning | Qualification |
|---|---|---|
| $B_t$ | Bucket state at step $t$ | Conceptual state snapshot |
| $H_t$ | Hypothesis decision ledger | Not necessarily all possible hypotheses |
| $S_t$ | Structural composition state | May be partial or latent |
| $E_t$ | Evidence state | Includes dependencies and provenance where needed |
| $P_t$ | Policy / directional state | Can reference separately versioned field objects |
| $M_t$ | Metadata, lineage and resource accounting | Contract details in SPEC-001 |
| $C_t$ | Candidates generated at step $t$ | Not necessarily exhaustive |
| $G$ | Candidate generation operator | May be policy-conditioned |
| $\theta_G$ | Generator configuration or learned parameters | Must be versioned for reproducibility |
| $R_t$ | Accessible context/resources | Scope and permissions matter |
| $D_t$ | Directional field at step $t$ | May be vector-valued and uncertain |
| $T$ | Authorized state transition | Subject to invariants |
| $s_k(c)$ | Candidate score on objective $k$ | Units and normalization must be declared |
| $w_k$ | Objective weight | Not intrinsically comparable across contexts |
| $\mathcal F_t$ | Search frontier | Exact notation may vary by document |
| $\Pi_t$ | Portfolio or policy, context-dependent | Define locally when used |

A weighted aggregation such as $S(c)=\sum_k w_k s_k(c)$ is **one possible policy**, not the definition of directional intelligence. In particular, it does not replace hard constraint checking or uncertainty reporting.

## 10. Commonly confused distinctions

| Distinction | Why it matters |
|---|---|
| Candidate vs. accepted hypothesis | Generation does not establish admissibility or truth. |
| Feasible vs. true | Constraint consistency is not empirical confirmation. |
| Weak evidence vs. hard constraint | Directional usefulness does not authorize logical rejection. |
| Low priority vs. impossible | Search scheduling and sound pruning have different guarantees. |
| Quiescent vs. closed | No immediate work does not imply exhaustive exploration. |
| Budget termination vs. completion | Resource exhaustion leaves unresolved alternatives. |
| Dynamic search vs. open-ended evolution | State-dependent candidate generation need not invent new representations/operators. |
| Self-modification vs. validated RSI | A change in strategy is not demonstrated capability improvement. |
| Relay receipt vs. evidence acceptance | Transfer does not establish correctness or applicability. |
| Behavioral attribution vs. identity identification | Structural clustering is not proof of who a person is. |
| Conformance vs. performance validation | Correct interfaces do not establish superior search results. |

## 11. Normative and research-status vocabulary

- **MUST / MUST NOT:** mandatory behavior in the applicable specification; not retroactively imposed on all conceptual examples.
- **SHOULD / SHOULD NOT:** recommended behavior with documented exceptions possible.
- **MAY:** optional, permitted behavior.
- **Invariant:** a property intended to hold for every valid transition or state in a declared contract.
- **Conformance test:** checks whether an implementation obeys a specification.
- **Testable hypothesis:** an empirical claim whose truth remains open pending controlled evaluation.
- **Baseline:** a comparison algorithm or system used to isolate a claimed benefit.
- **Ablation:** an experiment removing one mechanism (for example, field feedback) to estimate its contribution.
- **Proposed / exploratory:** research constructs whose interface or performance is not yet established as standard.

## 12. Where to read next

| Topic | Primary references |
|---|---|
| From BTP to D-BTP | [D-BTP-001](docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md), [D-BTP-002](docs/foundations/D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md) |
| Constraint semantics | [D-BTP-003](docs/foundations/D-BTP-003-Constraint-Guided-Structural-Composition.md), [SPEC-002](docs/specifications/SPEC-002-Candidate-Generation-and-Constraint-Plugins.md) |
| Directional generation, scoring and feedback | [D-BTP-004](docs/foundations/D-BTP-004-Directional-Fields-for-Generation-and-Selection.md), [D-BTP-006](docs/foundations/D-BTP-006-Coupled-Generation-Selection-and-Feedback.md), [SPEC-003](docs/specifications/SPEC-003-Directional-Scoring-and-Search-Control.md) |
| Weak evidence | [D-BTP-005](docs/foundations/D-BTP-005-Weak-Evidence-and-Directional-Exploration.md), [SPEC-004](docs/specifications/SPEC-004-Evidence-Relay-and-Learning-Lifecycle.md) |
| Multi-agent, relay and learning | [D-BTP-007](docs/foundations/D-BTP-007-Multi-Agent-RSI-and-Collective-Structural-Learning.md), [CASE-003](docs/cases/CASE-003-Multi-Agent-Hypothesis-Competition.md) |
| Open-ended evolution | [D-BTP-008](docs/foundations/D-BTP-008-Open-Ended-Structural-Evolution-and-Intelligence.md), [EXT-002](docs/extensions/EXT-002-Recursive-Directional-Field-Evolution.md), [EXT-003](docs/extensions/EXT-003-Open-Ended-BTP-and-Structural-Relay.md) |
| Canonical Bucket state | [SPEC-001](docs/specifications/SPEC-001-Dynamic-Bucket-State-Contract.md) |
| Applied examples | [CASE-001](docs/cases/CASE-001-Blockchain-Actor-Attribution.md), [CASE-002](docs/cases/CASE-002-Dynamic-Starmap-Similarity.md) |

See [README.md](README.md), [START-HERE.md](START-HERE.md), and [CONTENTS.md](CONTENTS.md) for project orientation and the complete reading map.

## 13. Glossary maintenance policy

1. Prefer one canonical meaning per term; explicitly qualify domain-specific variants.
2. Do not silently promote extension proposals into mandatory specification fields.
3. When changing normative terms, update the affected SPEC document and its conformance tests first.
4. Preserve historical terminology where needed to explain the original BTP lineage.
5. Add references for new terms and distinguish proposed mechanisms from demonstrated results.
6. Check internal links against the actual repository tree before release.

---

**Research note:** D-BTP is presented as an open, testable structural intelligence research program. Its terminology is intended to support interoperability, falsifiable experiments and collective learning, not to imply that open-ended intelligence or recursive self-improvement has already been demonstrated.
