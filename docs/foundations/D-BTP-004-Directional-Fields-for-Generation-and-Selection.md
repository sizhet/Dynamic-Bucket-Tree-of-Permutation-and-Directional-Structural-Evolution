# D-BTP-004 — Directional Fields for Generation and Selection

**Project:** Dynamic Bucket Tree of Permutation (D-BTP): Directional Structural Generation and Hypothesis Evolution  
**Series:** Foundations · D-BTP-004  
**Status:** Research foundation / proposed formalization  
**Version:** 1.0.0-draft · 2026-11-03  
**Companions:** D-BTP-001 — From Metric Similarity to Structural Hypothesis Search; D-BTP-002 — Dynamic Bucket States and Candidate Generation; D-BTP-003 — Constraint-Guided Structural Composition  
**Next:** D-BTP-005 — Weak Evidence and Directional Exploration; D-BTP-006 — Coupled Generation, Selection and Feedback

## Abstract

A dynamic Bucket Tree of Permutation (D-BTP) does not merely score a fixed set of matching pairs. It constructs evolving structural hypotheses, discovers candidates in response to current state, and decides which branches deserve scarce computation. This paper develops **directional fields** as a unified but explicitly decomposable control mechanism for (i) generating structural candidates, (ii) choosing which hypotheses to expand, and (iii) allocating computational and evidential resources. A field is not necessarily a scalar similarity metric: it can be a state-dependent, multi-objective, perspective-specific policy over structural transitions. The essential proposal is **coupling**: directional guidance shapes what is generated, while the consequences of generated hypotheses can update subsequent guidance. We specify the semantics of directional fields, their interfaces to dynamic buckets, their separation from hard feasibility, feedback and governance boundaries, alternative search controllers, and a validation program. These are architectural hypotheses requiring empirical tests, not claims that any direction field is intrinsically reliable or that the approach guarantees superior search.

## 1. From measuring a structure to directing its growth

In baseline metric similarity, the common abstraction is to compare two structures, identify candidate correspondences, and maximize a score over compatible subsets. The objective evaluates a candidate alignment. The search is often described as selecting among pre-existing pairings.

D-BTP generalizes the setting. A decision can expose new latent actors, cluster candidates, relational patterns, or higher-order structural claims. The next set of candidates may not exist as an explicit list before the decision. Consequently, a scoring function that ranks completed alignments is insufficient to describe the entire computation.

The new question is:

> How should an evolving structural search use incomplete, multi-perspective guidance to decide **what to generate, what to pursue, and what to learn from the consequences**, without confusing heuristic direction with logical truth?

A directional field is a candidate answer. It gives the search a *purposeful orientation* while preserving the distinction between hypothesis, evidence, objective, and constraint.

## 2. The two inseparable dimensions

The core observation motivating this paper is that a dynamic BTP has two coupled dimensions:

1. **Generative branching:** the search proposes new candidate claims and creates successor buckets by accepting, excluding, or otherwise refining them.
2. **Directional selection:** the search prioritizes, retains, revisits, or suspends candidate branches in light of a direction field and resource constraints.

A simplistic pipeline would be `generate → score → select`. That is a useful baseline, but it misses the feedback loop. A more faithful conceptual cycle is:

```text
            ┌────────────────────────────────────────┐
            │ Directional field / search policy D_t  │
            └─────────────┬──────────────┬───────────┘
                          │              │
                 guides proposals   ranks expansion
                          │              │
                          ▼              ▼
              Candidate generation   Search frontier
                          │              ▲
                          ▼              │
                  Accept / exclude / refine
                          │
                          ▼
                Constraint propagation
                          │
                          ▼
               New bucket and evidence
                          │
                          ▼
               Feedback / field update
                          │
                          └───────────────► D_(t+1)
```

**Key distinction:** Generation and selection are logically separable for testing and implementation, but computationally interdependent when the generator uses current direction and the direction field uses information produced by earlier generations.

## 3. Formal setting

### 3.1 Dynamic bucket

Following D-BTP-002 and D-BTP-003, represent a bucket as

\[
\mathcal B_t=(H_t,S_t,E_t,P_t,M_t),
\]

where:

- \(H_t\) is a ledger of accepted, excluded, and pending structural claims;
- \(S_t\) is the current domain and inferred structural state;
- \(E_t\) stores evidence, provenance, dependencies, uncertainty, and relevant scoring information;
- \(P_t\) stores the direction-field references, control policies, and remaining resource budgets;
- \(M_t\) stores execution metadata, generation epochs, visited signatures, and reproducibility information.

The observation ledger should be distinguished from inferred structural claims. Generating a latent actor does not make that actor an observed real-world identity.

### 3.2 Candidate generation

For a bucket \(\mathcal B_t\), a generator may return a finite, budgeted set of proposed structural claims:

\[
C_t=G(\mathcal B_t,D_t;\,\omega_t,b_t),
\]

where \(D_t\) is a directional field, \(\omega_t\) is an optional recorded random seed, and \(b_t\) is a candidate-generation budget. The generator can produce pairs, edges, cluster merges, latent-object proposals, or typed multi-object claims. A generator may also report `unknown`, `temporarily exhausted`, or `certified complete`—these are **not equivalent** outcomes.

### 3.3 Branch transition

For an eligible candidate \(c\), a decision \(a\) may be `accept`, `exclude`, or a domain-approved refinement. A transition is

\[
\mathcal B_{t+1}=T(\mathcal B_t,c,a;K),
\]

where \(K\) is the applicable hard-constraint system. The transition updates hypotheses, inferred state, evidence dependencies, and candidate-generation context. Hard infeasibility is a property of the constraint contract, not of a low directional score.

### 3.4 Directional field

Rather than define a field as one number, define it as a state-dependent collection of guidance operators:

\[
D_t=\bigl(D_t^{\mathrm{gen}},D_t^{\mathrm{select}},D_t^{\mathrm{resource}},D_t^{\mathrm{learn}}\bigr).
\]

These components may share a model and evidence, but their outputs have different semantics. A scalar score, vector-valued preference, partial ordering, probability distribution, or policy over candidate classes can instantiate part of a field.

A useful formal interpretation is a **policy over structural transitions**, not a physical vector field. Any geometrical interpretation requires an explicit embedding and should not be presumed.

## 4. Generation guidance: deciding what is worth proposing

Generation guidance answers: *Given the current bucket, which structural claims should be considered next?*

Examples include:

- proposing an actor–behavior relation when temporal and transaction-flow patterns cohere;
- generating a latent cluster when several existing candidates share a recurring structural motif;
- preferring candidates that discriminate among competing explanations;
- exploring a cross-domain structural analogy that has not yet been evaluated;
- withholding redundant candidates already settled by a sound constraint implication.

A generator may use a proposal priority

\[
q_{\mathrm{gen}}(c\mid\mathcal B,D)=f(\mathrm{plausibility},\mathrm{novelty},\mathrm{expected\ information\ gain},\mathrm{cost},\mathrm{coverage}),
\]

where \(f\) is a policy-dependent combination, not a universal formula. A candidate can be valuable even if its present fit is modest, provided testing it may distinguish important hypotheses.

**Failure mode:** A direction-guided generator can become self-confirming, repeatedly proposing only candidates favored by its current beliefs. A practical implementation should reserve exploration capacity for alternative proposals, uncertainty-driven sampling, or controlled broad generation.

## 5. Selection guidance: deciding which bucket to expand

Selection guidance acts on the frontier of feasible buckets. Its output can be a ranking, a set of non-dominated buckets, a scheduling policy, or an allocation distribution.

For a scalarized controller, one possible *illustrative* priority is

\[
Q(\mathcal B)=\alpha F(\mathcal B)+\beta I(\mathcal B)+\gamma N(\mathcal B)-\delta C(\mathcal B)-\eta R(\mathcal B),
\]

where \(F\) is explanatory fit, \(I\) estimated information gain, \(N\) structural novelty, \(C\) computational cost, and \(R\) an evidence-quality or model-risk penalty. Weights depend on declared objectives and calibration. This priority is **not** a proof of posterior probability, optimality, or feasibility.

Different search regimes can implement the selection policy:

| Controller | Directional use | Main limitation |
|---|---|---|
| Best-first | Expand highest-priority frontier bucket | Susceptible to misleading priorities |
| Beam search | Retain a bounded portfolio per iteration | May discard globally best branch |
| Branch-and-bound | Order branches heuristically; prune only using sound bounds | Reliable bounds may be unavailable |
| Monte Carlo / stochastic search | Allocate samples using exploratory policies | Requires careful uncertainty and variance accounting |
| Multi-objective portfolio | Preserve non-dominated hypotheses | Frontier size and diversity control are difficult |

Direction should order exploration; it must not silently authorize unsound pruning.

## 6. Resource guidance: deciding how much effort to spend

Directional intelligence is partly an **allocation problem**. Two buckets with similar fit may deserve different effort if one is cheap to resolve and the other is expensive but highly informative.

A resource controller can allocate:

- candidate-generation calls and depth limits;
- constraint-propagation effort;
- independent evidence checks;
- model-inference tokens or compute;
- branch width and hypothesis diversity;
- validation and adversarial challenge budget.

Let \(b_t(\mathcal B)\) be the assigned budget to bucket \(\mathcal B\). Then a constrained controller may solve approximately

\[
\max_{\{b_t\}}\sum_{\mathcal B\in\mathcal F_t}\widehat V(\mathcal B,b_t(\mathcal B))
\quad\text{subject to}\quad
\sum_{\mathcal B\in\mathcal F_t}b_t(\mathcal B)\le B_t.
\]

Here \(\widehat V\) is a predicted marginal value of computation, which must be empirically calibrated. A practical controller also needs floors or quotas for underexplored perspectives.

## 7. Multi-directional fields and perspective-aware scoring

There may be no single authoritative direction. Consider a blockchain actor-attribution hypothesis: one perspective favors transaction-flow coherence, another temporal consistency, another simplicity, and another evidence provenance. These perspectives can conflict without creating a hard logical contradiction.

Represent a field as a vector:

\[
\mathbf d(\mathcal B)=(d_1(\mathcal B),\ldots,d_k(\mathcal B)).
\]

Possible combination rules include:

1. **Lexicographic priorities:** protect an explicitly higher-priority objective before optimizing secondary ones.
2. **Weighted aggregation:** convenient when units and tradeoffs are defensible.
3. **Pareto dominance:** preserve hypotheses not dominated across all chosen criteria.
4. **Perspective portfolios:** keep separate top candidates for distinct evaluators or stakeholders.
5. **Constraint-gated preferences:** first satisfy hard admissibility, then apply soft directional ranking.

A field should carry its **perspective identity**, measurement definitions, version, and authority. A change in weighting can be a legitimate policy revision, not evidence that the underlying observed facts changed.

## 8. Weak evidence as guidance rather than verdict

Weak evidence is often useful before it is strong enough to support a definitive claim. A weak signal may prioritize a test, propose a candidate relation, or identify a direction for information gathering. It should not be promoted into an absolute rejection rule without an independently justified constraint.

This separation creates three evidence roles:

| Role | Permitted use | Not justified by itself |
|---|---|---|
| Proposal cue | Suggest candidates and new structural relations | Establish truth of a candidate |
| Ranking cue | Prioritize feasible buckets | Declare excluded alternatives impossible |
| Update evidence | Revise calibrated beliefs when dependencies are accounted for | Treat correlated observations as independent confirmations |

Evidence records should identify source, timestamp, reliability assumptions, correlation group, counterevidence, and the exact hypothesis they bear upon. When uncertainty is substantial, abstention and unresolved alternatives are legitimate outcomes.

D-BTP-005 develops these distinctions in detail.

## 9. Coupling generation and selection

The most important architectural claim is **bidirectional coupling**:

\[
C_t=G(\mathcal B_t,D_t),
\]

\[
\mathcal B_{t+1}=T(\mathcal B_t,c_t,a_t),
\]

\[
D_{t+1}=U(D_t,\operatorname{Observe}(\mathcal B_{t+1}),F_t),
\]

where \(F_t\) represents validated feedback, not merely the model's own favorable score. A system may choose \(U\) to leave the field fixed during an episode; learning the field is an optional, higher-level capability.

The coupling can be decomposed into four mechanisms:

- **Directional proposal:** the current field biases what is generated.
- **Directional selection:** the field biases which successor states receive attention.
- **Structural feedback:** new states reveal constraints, residuals, and previously hidden candidates.
- **Field adaptation:** externally evaluated outcomes may revise future generation and selection policies.

A strong research design tests these mechanisms independently and together. Merely labeling a heuristic score a "field" does not establish a new algorithmic advantage.

## 10. Distinguishing three kinds of evolution

It is important not to conflate different forms of change:

**Level A — Structural-state evolution.** Hypotheses, inferred clusters, candidate relations, and evidence state change while the generator and evaluator remain fixed.

**Level B — Search-policy evolution.** The controller learns which candidate types, branch orderings, or budgets work better, while the task objective remains fixed.

**Level C — Direction-field evolution.** The criteria, weights, perspectives, or field models themselves are revised under an explicitly governed learning contract.

Level A does not imply B; B does not imply C. An adaptive field also does not by itself imply recursive self-improvement or open-ended intelligence. Those require additional demonstrations of learning stability, transfer, and externally verified improvement.

## 11. A reference directional D-BTP loop

The following pseudocode is a *contract sketch*, not a ready-made optimal solver.

```text
function directionalDBTP(initialBucket, pluginSet, policy, budget):
    frontier = PriorityPortfolio([initialBucket])
    archive = []
    visited = StateSignatureIndex()

    while frontier.notEmpty() and budget.available():
        bucket = frontier.select(policy.directionalSelection)
        if visited.isEquivalentWithSufficientCoverage(bucket):
            continue
        visited.record(bucket)

        constraints = pluginSet.propagateHardConstraints(bucket)
        if constraints.provenInfeasible:
            archive.addRejected(bucket, constraints.proof)
            continue

        field = policy.resolveDirectionalField(bucket)
        candidates, coverage = pluginSet.generateCandidates(
            bucket, field, budget.generationSlice()
        )
        candidates = deduplicateAndValidate(candidates, bucket)

        if candidates.isEmpty():
            if coverage.certifiedComplete and constraints.closed:
                archive.addClosed(bucket)
            else:
                archive.addQuiescentOrBudgetLimited(bucket, coverage)
            continue

        candidate = policy.chooseCandidate(candidates, bucket, field)
        for decision in pluginSet.allowedDecisions(candidate, bucket):
            successor = pluginSet.transition(bucket, candidate, decision)
            if not pluginSet.violatesHardConstraint(successor):
                successor = pluginSet.updateEvidence(successor)
                successor = policy.updateSearchContext(successor)
                frontier.offer(successor, field, diversityPolicy=policy.diversity)

    return archive + frontier.asUnresolvedPortfolio()
```

**Important:** A visited-state test is sound only if its equivalence relation includes all future-relevant information, including generation coverage and policy state where these affect reachable successors. `coverage.certifiedComplete` requires a domain-specific completeness contract; exhaustion of a generator call alone is insufficient.

## 12. Worked conceptual example: actor–behavior attribution

Suppose observed transactions \(T_1,T_2,T_3\) and latent actors \(A_1,A_2\) form a hypothesis search. The algorithm does **not** begin by claiming that these latent actors are identified people.

1. A transaction-flow cue proposes \((A_1,T_1)\).
2. Accepting that claim changes the inferred flow structure, exposing a new candidate \((A_1,T_2)\).
3. A temporal perspective ranks \((A_2,T_2)\) more highly, while a flow perspective favors \((A_1,T_2)\).
4. The search preserves both feasible alternatives in a diverse hypothesis portfolio.
5. A subsequent authorized observation may differentiate the two; if not, the result remains ambiguous.

This example illustrates the distinction between **control-attribution hypotheses**, **structural consistency**, and **real-world identity**. Shared control, custodial intermediaries, and automation can defeat naïve one-to-one identity assumptions. Candidate confidence should not be mistaken for a verified identity.

## 13. Worked conceptual example: dynamic starmap similarity

Let starmap \(A\) contain a partially observed motif and starmap \(B\) a different decomposition of a similar motif. A fixed-list matcher may fail to propose a useful node correspondence because the relevant intermediate structure is absent from its initial representation.

A dynamic generator can hypothesize a composite node or relation in one structure. A direction field favoring explanatory compression and consistency can prioritize evaluating that proposal. A constraint plugin verifies type and relational compatibility. If the composite correspondence survives evaluation, the algorithm has **discovered a candidate structural explanation**, not proven that the source graphs were intrinsically identical.

This is a testable generalization of unaligned matching: structural interpretation and candidate generation become part of the search.

## 14. Directional control planes and plugin contracts

A domain-neutral API should keep separate the following operations:

```text
CandidateBatch generateCandidates(Bucket, DirectionField, Budget)
ConstraintResult checkAndPropagate(Bucket, Candidate, Decision)
EvidenceResult evaluateEvidence(Bucket, Candidate, EvidenceContext)
DirectionalVector evaluateDirections(Bucket, PerspectiveSet)
Priority selectFrontier(Frontier, DirectionalVector, Policy)
BudgetAllocation allocateResources(Frontier, Budget, Policy)
FieldUpdate proposeFieldUpdate(Field, ValidatedFeedback, Governance)
```

Each plugin should declare:

- input and output schemas, type constraints, and version;
- whether its results are deterministic, stochastic, or approximate;
- provenance and correlation assumptions;
- whether an output is a hard proof, a soft estimate, or a proposal;
- budget and termination semantics;
- the effects of a policy or model update on cached scores;
- conformance tests and failure behavior.

**Control-plane principle:** A domain plugin can propose evidence or preferences, but only an explicitly authorized constraint contract may certify hard infeasibility. A learned scoring model must not silently change the admissible solution set.

## 15. Search complexity, coverage, and quality

For a fixed finite candidate set of size \(m\), binary accept/exclude branching has up to \(2^m\) decision combinations before pruning and equivalence reduction. In dynamic D-BTP, the total candidate universe may be unknown at initialization, and generation can expose additional choices. No finite worst-case bound follows from the architecture alone.

Directional guidance may improve **anytime performance**—the quality of the best available feasible hypothesis at a fixed budget—without reducing worst-case complexity. Conversely, an overly narrow field may worsen performance by suppressing critical alternatives.

Useful measures include:

- best feasible objective value versus elapsed compute;
- candidate precision, recall, and discovery latency on synthetic ground truth;
- diversity and calibration of the top-\(K\) hypothesis portfolio;
- percentage of search effort spent on duplicate or infeasible branches;
- number of certified closed states versus budget-limited unresolved states;
- cross-domain transfer and sensitivity to field miscalibration.

The **quality of a field** is therefore an empirical question, not an intrinsic property of directional terminology.

## 16. Failure modes and safeguards

| Failure mode | Consequence | Safeguard |
|---|---|---|
| Self-reinforcing proposal bias | Missing alternatives that contradict the field | Exploration quotas and diverse generators |
| Score/constraint confusion | Unsound exclusion of feasible branches | Typed hard-vs-soft plugin outputs |
| Evidence double counting | Inflated confidence | Dependency graphs and correlation groups |
| Premature field adaptation | Reward hacking or drift | Held-out feedback and bounded updates |
| Incomplete candidate coverage | False declaration of a terminal leaf | Explicit coverage certificates and quiescence state |
| Changing policy during replay | Non-reproducible search history | Versioned field and seed logs |
| Overaggressive state merging | Loss of distinct future possibilities | Future-relevant state signatures |
| Single-best-hypothesis collapse | Spurious certainty | Top-\(K\) and perspective portfolios |
| Latent actor treated as known identity | Invalid attribution claim | Separate structural, control, and identity assertions |

## 17. Testable hypotheses

**H1 — Direction-guided generation.** Under equal computational budgets, a calibrated field-informed candidate generator discovers a higher proportion of ground-truth-relevant candidates than an unguided generator on selected dynamic structural tasks.

**H2 — Coupling benefit.** Jointly guiding generation and selection outperforms either generation-only or selection-only guidance on tasks where accepted claims reveal new candidates.

**H3 — Diversity protection.** A multi-directional portfolio reduces catastrophic omission of viable hypotheses relative to a single scalarized best-first policy under deliberately misleading cues.

**H4 — Weak-evidence value.** Fallible cues improve information gained per unit of compute when used for ranking, while hard exclusion based on those same cues increases false negatives.

**H5 — Feedback adaptation.** Field updates trained on independent outcome feedback improve performance on held-out task distributions more reliably than updates trained solely on self-generated scores.

**H6 — Transfer limits.** A direction policy trained in one domain yields measurable gains in a related domain only when relevant structural and evidence semantics transfer; negative transfer is expected under mismatch.

These hypotheses can fail. Negative results should inform narrower applicability claims rather than being reinterpreted as success.

## 18. Validation design

### 18.1 Baselines and ablations

Compare at least six conditions with the same candidate evaluation budget:

| Condition | Dynamic generation | Generation guidance | Selection guidance | Field learning |
|---|---:|---:|---:|---:|
| B0: static BTP | No | No | Optional fixed score | No |
| B1: dynamic unguided | Yes | No | No | No |
| B2: generation only | Yes | Yes | No | No |
| B3: selection only | Yes | No | Yes | No |
| B4: coupled directional | Yes | Yes | Yes | No |
| B5: adaptive directional | Yes | Yes | Yes | Yes |

Use consistent hard constraints and evaluation rules. Report both candidate-generation compute and downstream search compute; otherwise apparent gains may simply move cost into an uncounted plugin.

### 18.2 Test environments

- **Synthetic actor-attribution graphs:** Known latent control assignments with configurable custodial, shared-control, and noisy evidence patterns.
- **Dynamic starmap benchmarks:** Hidden composite motifs, partial observation, and generated relation types.
- **Adversarial cue benchmarks:** Misleading but plausible directional signals to measure robustness.
- **Transfer suites:** Related and unrelated graph domains to quantify positive and negative transfer.

### 18.3 Reporting requirements

Pre-register objective definitions, constraint semantics, data splits, baselines, random seeds, compute budgets, and stop criteria. Include uncertainty intervals, failure cases, and unresolved outputs. Do not infer causal improvement from a single favorable example. Record field versions and all evidence provenance required for replay.

## 19. Relationship to the wider SI research program

D-BTP's directional field connects conceptually to several existing SI research themes while preserving their distinct roles:

- **Metric Similarity / Unaligned AND:** provides the original alignment problem and local relation measurements.
- **UCPSF:** suggests perspective-aware scoring and control-plane folding without requiring every perspective to collapse into one scalar.
- **BM-ODWEI and REN:** motivate weak-evidence navigation and directional cues whose usefulness can be tested by search outcomes.
- **SIF and structural residual growth:** motivate generating new structural candidates from unresolved gaps.
- **UIERU / Collective Learning:** suggest relaying evaluated candidate structures and reusable search experience.
- **AQSI:** suggests candidate questions and information-seeking operations as part of the exploration frontier.
- **SSICR and Multi-Agent RSI:** motivate competing search strategies and controlled policy learning.

These are **proposed architectural interfaces**, not evidence that the respective theories are equivalent or empirically validated by this paper.

## 20. Open questions

1. When is a vector of directions preferable to a scalar score or a strict partial ordering?
2. Can a direction field be learned from weak evidence without amplifying its systematic bias?
3. How can candidate-coverage certificates be defined for generators that introduce latent object types?
4. Which search-state summaries are sufficient for safe deduplication under field adaptation?
5. How should exploration budgets be reserved for perspectives that currently score poorly but might reveal counterexamples?
6. When does joint generation–selection guidance outperform strong conventional heuristic search, after full compute accounting?
7. Can field updates be constrained to preserve stable user-defined objectives while improving search efficiency?
8. Which kinds of directional transfer are robust across graph domains, and which produce negative transfer?
9. How can structural novelty be measured without rewarding meaningless proliferation of hypotheses?
10. What evidence would justify calling an adaptive D-BTP system recursive self-improvement rather than ordinary policy tuning?

## 21. Conclusion

The distinctive proposal of directional D-BTP is not that it attaches a score to each branch. It is that **the mechanism that generates new structural possibilities and the mechanism that selects promising directions can form a coupled, feedback-sensitive computation**. Direction may shape candidate discovery, frontier expansion, and resource allocation; newly discovered structure may in turn provide information for revising direction. Hard feasibility remains distinct from fallible guidance, and unresolved alternatives remain explicit.

This framework makes a broad intuition operational: *structural generation creates possibilities; directional fields make exploration purposeful; validated feedback can improve how both are coordinated*. The claim is scientifically useful precisely because its advantages, limits, and failure modes can be tested against explicit baselines.

---

## Suggested figure placement

- **Fig-005 — Directional Generation and Selection Coupling:** immediately after Section 2 or at the start of Section 9.
- **Fig-006 — Weak Evidence and Multi-Directional Scoring:** after Section 8 or Section 7, with detailed treatment reserved for D-BTP-005.
- **Fig-001 — D-BTP Grand Architecture:** optional cross-reference in Section 19; avoid duplicating it in every foundation paper.

## Research status and citation note

This document is a proposed research architecture within the D-BTP project. Its terminology and formal definitions are intended to support future specifications, implementations, and validation. It does not report completed benchmark results or establish novel mathematical optimality theorems. Cite the repository's eventual DOI and versioned `CITATION.cff` after publication; do not invent a DOI before release.
