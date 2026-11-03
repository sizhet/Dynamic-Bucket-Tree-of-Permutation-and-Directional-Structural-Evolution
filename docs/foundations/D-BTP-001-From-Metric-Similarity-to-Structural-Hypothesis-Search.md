# D-BTP-001 — From Metric Similarity to Structural Hypothesis Search

**Project:** Dynamic Bucket Tree of Permutation (D-BTP)  
**Series:** Foundations  
**Status:** Research foundation / proposed generalization  
**Version:** 1.0.0 (draft)  
**Date:** 2026-11-03  
**License:** Apache-2.0

## Abstract

Bucket Tree of Permutation (BTP) was motivated by metric-structure and starmap similarity: given two potentially unaligned structures, identify compatible node-pair correspondences and evaluate their joint structural fit. This paper argues that the more general computational object is not a similarity score but a *structural hypothesis search*: a constrained exploration of candidate relations whose acceptance or exclusion changes the state in which subsequent hypotheses are generated and assessed. We distinguish the baseline finite-candidate interpretation from a dynamic extension in which candidate generation, evidence accumulation, structural state transitions, and search control are coupled. Blockchain actor attribution serves as a motivating example, not as a claim that an on-chain address identifies a real-world person. We propose formal semantics, invariants, falsifiable hypotheses, and an agenda for specification and empirical validation. No superiority, completeness, or biological correspondence is assumed without evidence.

## 1. Motivation and Scope

Structural similarity is often framed as a terminal calculation:

\[
(A,B) \mapsto \operatorname{Similarity}(A,B).
\]

Yet an alignment search may do more than return a scalar. Accepting a correspondence can reveal new constraints, expose a previously latent relation, and suggest further correspondences. The key research question is whether the search mechanism can be separated from the particular *metric similarity* objective and reused for other structural inference tasks.

This paper makes three distinctions:

1. **Baseline BTP:** a constrained accept/exclude search over a fixed, finite collection of candidate node pairs.
2. **Dynamic BTP:** a search whose candidate universe and structural state can evolve as hypotheses are explored.
3. **Learning or directionally guided BTP:** optional extensions in which evidence, directional objectives, and learned policies influence generation, selection, and computational resource allocation.

The latter two are proposed research generalizations. Their value must be established by contracts, implementations, and comparisons against strong baselines.

## 2. Baseline BTP: Unaligned AND of Metric Structures

Let the two input starmaps be

\[
G_A=(V_A,E_A,\alpha_A),\qquad G_B=(V_B,E_B,\alpha_B),
\]

where attributes and metrics are represented by \(\alpha_A\) and \(\alpha_B\). A matching procedure, possibly supporting wildcard nodes, proposes a finite set

\[
C_0 \subseteq V_A\times V_B.
\]

Each candidate pair \(p=(a,b)\) asserts a possible correspondence. A baseline bucket can be represented as

\[
B=(R,U,S),
\]

where \(R\) is the accepted set of pairs, \(U\) is the unresolved candidate set, and \(S\) contains current structural states and evaluation caches. For a chosen \(p\in U\), two branches are considered:

- **Accept:** include \(p\) in \(R\), provided it is compatible with all hard constraints; update the state.
- **Exclude:** remove \(p\) from unresolved consideration; update the state as appropriate.

A baseline leaf is reached when \(U=\varnothing\). The feasible leaves encode compatible correspondence sets, interpretable as candidate Unaligned-AND alignments. A search controller attempts to find high-quality leaves under a computational budget.

### 2.1 Compatibility is domain-defined

The prohibition against contradictory accepted pairs is an invariant, not necessarily a universal one-to-one mapping rule. Some applications require injective matching; others permit many-to-one or one-to-many relations. Wildcards likewise require explicit semantics. The constraint plugin defines which combinations are admissible.

### 2.2 A notation correction

A rigorous implementation should distinguish *excluded* from merely *not yet considered* pairs. One useful baseline representation is \(B=(R,X,U,S)\), with \(X\) an explicit exclusion set. This prevents an excluded candidate from being silently reintroduced when dynamic generation is later enabled.

## 3. The Generalization: Search Over Structural Hypotheses

The decisive abstraction is to treat a pair not merely as a match contributing to a score, but as a **hypothesis-bearing relation**. A search state can then contain hypotheses, constraints, evidence, and structures that change as those hypotheses are tested.

A generalized bucket is

\[
B_t=(H_t,S_t,P_t,E_t),
\]

where:

- \(H_t\): accepted, excluded, and pending hypotheses, with their identifiers and provenance;
- \(S_t\): domain structural state, including derived relations and caches;
- \(P_t\): generation, evaluation, and search-control policy state;
- \(E_t\): accumulated evidence and scoring state.

The next candidate is produced by a state-dependent generator:

\[
C_t=\operatorname{Generate}(H_t,S_t,P_t,E_t).
\]

The generator need not materialize the full candidate universe. It may propose a small frontier, return a ranked stream, or report that no further admissible expansion is currently known. Thus a static `remaining_Unresolved_Node_Pairs_List` is an implementation option, not a defining requirement of dynamic BTP.

The controller selects a candidate \(p_t\), checks feasibility, and applies a transition:

\[
B_{t+1}=\operatorname{Transition}(B_t,p_t,a_t),
\qquad a_t\in\{\mathrm{accept},\mathrm{exclude}\}.
\]

State transitions may create new derived nodes or edges, alter candidate priorities, and reveal previously unenumerated candidate relations. They must not rewrite the historical meaning of accepted or excluded decisions without an explicit revision mechanism.

## 4. Dynamic Search Is Not Merely a Larger Static List

Dynamic candidate generation has two qualitatively distinct roles:

**Hypothesis-state evolution.** Accepting or excluding a candidate changes what is believed, what remains consistent, and how existing candidates score.

**Structural-model evolution.** A transition can derive new entities, relations, clusters, or abstractions that make previously unavailable hypotheses expressible.

A useful separation is:

\[
\text{Generate}\to\text{Validate}\to\text{Branch}\to\text{Update}\to\text{Generate again}.
\]

This does not imply that the generator is always correct or complete. A new hypothesis may be exploratory rather than established, and a newly derived structural object must retain the evidence and assumptions that produced it.

### 4.1 Termination and search frontiers

For a fixed finite candidate set, a leaf can be defined by exhaustion of unresolved candidates. With dynamic generation, the distinction is essential:

- **Closed leaf:** no admissible new expansion exists under a specified generator-completeness contract.
- **Budget-terminated partial result:** search stops due to time, memory, node-count, or other resource limits.
- **Paused frontier:** candidates remain possible, but exploration is deferred.

An empty *currently generated* frontier is not proof that no candidates exist. Cycle detection, canonical state identifiers, exclusion memory, and bounded generation are needed to avoid duplicate or infinite exploration.

## 5. Directional Fields and Weak Evidence

A directional field can influence which candidates are generated, which buckets are expanded, and where computation is spent. Let \(D_t\) denote directional guidance. A proposed coupled formulation is

\[
C_t=G(B_t,D_t),\qquad
B_{t+1}=T(B_t,p_t,a_t),\qquad
D_{t+1}=U(D_t,B_{t+1},\Delta E_t).
\]

This is a *research model*, not a demonstrated universal law. The key claim to test is that direction-aware generation can outperform a generate-then-rank pipeline at equal resource budgets.

Weak evidence is especially relevant here. A low-confidence cue need not justify accepting a hypothesis as true; it may only justify exploring that hypothesis sooner. Accordingly, the architecture must distinguish:

1. **Hard feasibility:** violations that make a state inadmissible under a stated contract.
2. **Soft evidence:** uncertain observations that adjust plausibility or exploration priority.
3. **Search utility:** expected value of further computation, potentially including information gain and cost.

Related or duplicated observations must not be treated as independent corroboration. Evidence provenance, correlation, calibration, and counterevidence belong in the evaluation contract.

## 6. Motivating Case: Blockchain Actor Attribution

Consider a graph of observed blockchain transactions and a set of latent controlling actors. Candidate hypotheses associate an actor or actor-cluster with one or more behaviors. Unlike ordinary one-to-one graph alignment, this may require one-to-many assignments, shared-control hypotheses, and multiple competing explanations.

For example, accepting a tentative association between two transactions and an actor-cluster might expose a temporal pattern and cause a generator to propose further associations. Other evidence may then support, weaken, or invalidate that cluster.

The distinctions below are mandatory:

- An on-chain address is not necessarily a distinct actor.
- Shared transaction patterns do not establish common control.
- Common control does not establish a real-world identity.
- A cryptographic signature verifies a specified key/message relation, not a person's identity.

The case is suitable for **synthetic or appropriately authorized data** with known ground truth. Evaluation should focus on calibrated uncertainty, false-positive rates, alternative hypotheses, and the ability to abstain when evidence is insufficient.

## 7. Search Objective and Hypothesis Portfolios

Maximizing the number of accepted pairs is generally inadequate. A generic objective may combine fit, structural consistency, complexity, contradiction penalties, and computational cost:

\[
J(H)=F_{\mathrm{evidence}}(H)+\nu F_{\mathrm{consistency}}(H)
-\lambda C_{\mathrm{complexity}}(H)-\mu C_{\mathrm{soft\ conflict}}(H).
\]

Hard-constraint violations instead make \(H\) infeasible. Weights, calibration, and the treatment of correlated evidence are domain-specific; the expression is illustrative rather than canonical.

A dynamic BTP implementation should be able to return a **diverse top-\(K\) portfolio** of feasible hypotheses, together with scores, provenance, unresolved alternatives, and resource-limit flags. High scoring is not the same as identifiable truth. Two incompatible hypotheses can fit the same observations equally well.

## 8. Algorithmic Contracts and Invariants

The following invariants are proposed for specification:

**I1 — Accepted-set consistency.** Every accepted hypothesis satisfies all active hard constraints, including those propagated from prior decisions.

**I2 — Explicit exclusion memory.** Excluded hypotheses cannot be regenerated as fresh unresolved hypotheses within the same decision context without a declared revision operation.

**I3 — Provenance.** Derived candidates, structural changes, and evidence updates retain their source and derivation history.

**I4 — Deterministic replay where claimed.** A deterministic configuration can replay generation and transitions from a serialized state and plugin versions; stochastic configurations record seeds and relevant policy versions.

**I5 — Separation of truth and priority.** Heuristic search priority is not presented as posterior probability or proof of attribution.

**I6 — Resource accounting.** Budget exhaustion and partial results are reported distinctly from complete search.

**I7 — Plugin safety.** Plugins expose declared inputs, outputs, side effects, and state mutation boundaries; failures cannot silently corrupt the search state.

A further research question is whether useful completeness or optimality guarantees can be recovered under bounded generation, finite candidate universes, admissible bounds, and fair expansion policies.

## 9. Complexity and Search Control

For \(m\) fixed binary candidates, naive enumeration has up to \(2^m\) accept/exclude combinations. Dynamic generation can make the effective hypothesis universe state-dependent and potentially unbounded. Therefore, no general fixed complexity bound follows from the BTP label alone.

Practical performance depends on candidate quality, constraint propagation, symmetry reduction, structural decomposition, heuristic ranking, pruning bounds, memoization, and computational budgets. Candidate policies may be guided by information gain or learned value estimates. Exactness claims require admissible pruning and sufficiently complete generation; beam search and other approximate controllers generally sacrifice such guarantees.

The aim is not to assert that a universal optimizer has been found, but to isolate a reusable search skeleton from domain-specific generators, constraints, evidence models, and controllers.

## 10. Relation to the Wider SI Research Program

The proposed D-BTP abstraction provides interfaces to several complementary directions:

- **Metric similarity / Unaligned AND:** the original correspondence-scoring application.
- **Structural Folding / Unfolding:** derived abstractions may change what can be matched or hypothesized.
- **Directional Weak Evidence:** uncertain cues may guide exploration without becoming hard facts.
- **Universal Control Planes and Scoring Folding:** multi-perspective evaluation and resource allocation.
- **Structural Relay and Collective Learning:** hypotheses, evidence, and policy improvements can be shared across compatible agents.
- **Autonomous Questioning and RSI:** candidate generation and search policy may themselves become learning targets.

These are architectural connections and proposed research interfaces, not evidence that the systems are already integrated or that dynamic BTP produces recursive self-improvement automatically.

## 11. Testable Hypotheses

**H1 — Cross-domain expressibility.** A common bucket/transition contract can represent both starmap similarity and actor-behavior attribution without modifying the core branching semantics.

**H2 — Dynamic-generation value.** On tasks with latent or emergent relations, state-dependent generation improves quality at equal budget relative to fixed-candidate BTP, under specified benchmarks.

**H3 — Directional coupling value.** Directional guidance applied to both generation and selection outperforms guidance applied only after candidate enumeration, under matched budgets.

**H4 — Weak-evidence utility.** Calibrated weak evidence improves search efficiency or discovery without increasing false-positive attribution beyond an agreed threshold.

**H5 — Portfolio robustness.** Diverse top-\(K\) hypotheses and explicit abstention yield better uncertainty representation than a single best-leaf report.

Negative or mixed results are informative. In particular, highly misleading directional fields may perform worse than unguided exploration.

## 12. Validation Roadmap

1. **Formal conformance:** implement a minimal state machine with accepted/excluded decisions, explicit invariants, deterministic replay, and finite-candidate baseline tests.
2. **Synthetic dynamic benchmark:** construct ground-truth graphs where new candidate relations become discoverable only after selected state transitions.
3. **Controlled ablations:** compare static BTP, dynamic generation without directional guidance, directional selection only, and fully coupled directional generation/selection.
4. **Stress tests:** vary weak-evidence noise, misleading cues, graph sparsity, ambiguity, candidate branching, and constraint strength.
5. **Measurement:** report solution quality, recall, precision, calibration, abstention, wall time, memory, expanded buckets, generated candidates, and search-budget utilization.
6. **Cross-domain transfer:** test a second non-blockchain structural task using the same core contracts and distinct plugins.
7. **Independent reproduction:** publish synthetic datasets, plugin versions, random seeds, and failure cases when feasible.

The baseline comparisons should include appropriate non-BTP methods, such as constraint programming, graph matching, or probabilistic inference, where applicable.

## 13. Limitations and Open Questions

- What minimal conditions make dynamically generated hypothesis search complete or terminating?
- How should canonical bucket identity be defined when states contain derived structures?
- Can exclusion memory be preserved without blocking legitimate revisions of earlier hypotheses?
- Which directional-field representations generalize across domains without hiding incompatible objectives?
- How can weak evidence guide search without contaminating final evidential confidence?
- When does dynamic generation outperform exhaustive or well-designed static candidate enumeration?
- Can learned generation policies transfer across tasks, and how can negative transfer be detected?
- What distinguishes structural evolution within a fixed algorithm from learning that changes the algorithm's own policy?

## 14. Conclusion

BTP can be understood more generally as a constrained search over structural hypotheses, with metric similarity as one application. The proposed dynamic extension replaces a necessarily fixed candidate list with state-dependent hypothesis generation, explicit transitions, evidence provenance, and budget-aware search. Directional fields and weak evidence may then guide what to generate, what to examine, and what to retain, while feedback may revise future guidance. This offers a concrete path from *structural measurement* toward *structural hypothesis generation and evaluation*. The claim is a research program to be formalized and tested, not a demonstrated universal intelligence mechanism.

## Related Documents in the D-BTP Series

- `D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md`
- `D-BTP-003-Constraint-Guided-Structural-Composition.md`
- `D-BTP-004-Directional-Fields-for-Generation-and-Selection.md`
- `D-BTP-005-Weak-Evidence-and-Directional-Exploration.md`
- `D-BTP-006-Coupled-Generation-Selection-and-Feedback.md`
- `SPEC-001-Dynamic-Bucket-State-Contract.md`
- `CASE-001-Blockchain-Actor-Attribution.md`

---

*This document records a proposed structural-intelligence research framework. Its algorithmic claims, generality, and practical benefits remain subject to formal specification and empirical validation.*
