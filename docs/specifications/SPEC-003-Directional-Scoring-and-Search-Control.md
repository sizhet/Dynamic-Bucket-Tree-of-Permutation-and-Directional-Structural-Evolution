# SPEC-003 — Directional Scoring and Search Control

**Project:** D-BTP — Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution  
**Document class:** Normative research specification  
**Status:** Proposed v1.0.0 contract; not a claim of implementation or empirical validation  
**Version:** 1.0.0-draft  
**License:** Apache-2.0

## Abstract

This specification defines interoperable contracts for directional scoring, search-frontier control, resource allocation, field adaptation, and evidence-aware feedback in Dynamic Bucket Tree of Permutation (D-BTP). A directional field is a versioned, explicitly scoped policy object that can influence which structural candidates are generated, evaluated, explored, retained, and revisited. It is not a substitute for a hard-constraint checker or an evidentiary finding. The specification separates *feasibility*, *evidence*, *directional utility*, *selection policy*, and *learning* while allowing them to interact through a traceable control loop. It specifies required data objects, state transitions, invariants, interfaces, failure behavior, audit events, and conformance tests.

## 1. Purpose and Scope

D-BTP starts with a dynamic Bucket state and generates structural hypotheses conditioned on the state, constraints, evidence, and policy. A search controller must prioritize finite computational resources without confusing promising hypotheses with verified ones. The present contract addresses five questions:

1. How are directional fields represented, versioned, and interpreted?
2. How do scoring services evaluate candidates and Bucket states under multiple objectives?
3. How does the controller select, suspend, resume, or terminate work under budgets?
4. How can feedback update guidance without corrupting feasibility or evidence semantics?
5. How can independent implementations produce auditable and comparable outcomes?

This contract is intended for research prototypes, distributed agent systems, and conformance testing. It does **not** guarantee globally optimal search, universal completeness, calibrated probabilities, or autonomous improvement.

### 1.1 Normative language

**MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** indicate contract strength. Conformance is relative to a declared profile and configuration. Examples and pseudocode are illustrative unless explicitly designated normative.

### 1.2 Dependencies

- `SPEC-001-Dynamic-Bucket-State-Contract.md`: Bucket identity, hypothesis ledger, state transitions, lifecycle, provenance, and versioning.
- `SPEC-002-Candidate-Generation-and-Constraint-Plugins.md`: candidate-generation and constraint-plugin boundaries.
- `D-BTP-004-Directional-Fields-for-Generation-and-Selection.md`: conceptual foundation for coupled generation and selection.
- `D-BTP-005-Weak-Evidence-and-Directional-Exploration.md`: weak-evidence semantics and counterevidence.
- `D-BTP-006-Coupled-Generation-Selection-and-Feedback.md`: integrated feedback loop.

When documents differ, the declared versioned specification profile and explicit interoperability mappings govern implementation behavior; conceptual papers do not silently override normative contracts.

## 2. Architectural Separation

A conforming system MUST distinguish the following functions, even when a runtime combines them physically:

| Function | Input | Output | Authority |
|---|---|---|---|
| Candidate generation | Bucket, generator policy, context | candidate proposals | proposes possibilities |
| Constraint validation | proposal, Bucket, constraint registry | hard feasibility findings | may establish infeasibility when sound |
| Evidence evaluation | observations, provenance, hypotheses | evidence assessments | assesses support, not logical validity |
| Directional scoring | state, candidates, objectives, field | score vectors and explanations | ranks opportunities |
| Search control | frontier, scores, budgets, policy | scheduling and retention decisions | allocates effort |
| Field adaptation | feedback, evaluation protocol, history | proposed field revisions | proposes policy changes |
| Governance/approval | proposed revisions, guardrails | accept/reject/rollback | authorizes deployment |

A low directional score MUST NOT be translated into a hard constraint failure. An `UNKNOWN` constraint outcome MUST NOT be treated as `FAIL`. Evidence strength MUST NOT be equated with the magnitude of a heuristic priority score.

## 3. Canonical Objects

### 3.1 DirectionalField

```yaml
field_id: "field:exploration:001"
field_version: "1.0.0"
field_schema_version: "dbtp-directional-field/1"
owner_scope: "experiment:synthetic-01"
objectives:
  - objective_id: "coverage"
    orientation: "maximize"
    measure_id: "measure:novel-feasible-coverage"
    weight: 0.35
  - objective_id: "expected_information_gain"
    orientation: "maximize"
    measure_id: "measure:ig-estimator-v1"
    weight: 0.40
  - objective_id: "compute_cost"
    orientation: "minimize"
    measure_id: "measure:estimated-cost-v1"
    weight: 0.25
normalization_profile: "profile:bounded-0-1-v1"
aggregation_policy: "weighted-sum-v1"
exploration_policy: "epsilon-mixture-v1"
exploration_parameters: {epsilon: 0.15}
update_policy_id: "policy:held-out-gated-v1"
constraints_boundary: "guidance-only"
validity_scope: {domain: "synthetic", task_family: "structural-hypothesis-search"}
created_from: ["event:field-init:001"]
```

Fields MUST have stable identifiers, version identifiers, explicit objectives, measure references, aggregation semantics, and a declared applicability scope. Every weight and normalization rule MUST be interpretable within the declared profile. Fields SHOULD identify owners, update policies, provenance, uncertainty, and expiration or revalidation conditions.

Weights are policy parameters, not empirical likelihoods. A change to weights, measure implementations, normalization, aggregation, or exploration behavior MUST increment the field version or otherwise create an immutable, uniquely identified field snapshot.

### 3.2 DirectionalScoreRecord

```yaml
score_id: "score:00042"
subject_type: "candidate" # or bucket, branch, query, portfolio
subject_id: "candidate:007"
bucket_id: "bucket:011"
field_id: "field:exploration:001"
field_version: "1.0.0"
scorer_id: "scorer:directional-v1"
scorer_version: "1.0.0"
components:
  - {objective_id: "coverage", raw_value: 0.6, normalized_value: 0.6, status: "estimated"}
  - {objective_id: "expected_information_gain", raw_value: 0.8, normalized_value: 0.8, status: "estimated"}
  - {objective_id: "compute_cost", raw_value: 0.2, normalized_value: 0.8, status: "estimated"}
aggregate_priority: 0.73
uncertainty: {kind: "interval", lower: 0.58, upper: 0.84}
evidence_refs: ["evidence:003"]
constraint_snapshot_ref: "constraints:rev-12"
state_snapshot_ref: "bucket:011:rev-5"
explanation_refs: ["explain:00042"]
scored_at_event: "event:0042"
```

The example uses cost inversion in normalization: a raw cost of 0.2 becomes a desirability value of 0.8. The displayed aggregate is illustrative: 0.35(0.6)+0.40(0.8)+0.25(0.8)=0.73. A score record MUST preserve the exact scoring context, or a content-addressed immutable reference to it. Missing measures MUST be represented explicitly; an implementation MUST NOT silently substitute zero without an agreed missing-data policy.

### 3.3 SearchControlDecision

```yaml
decision_id: "decision:0081"
frontier_snapshot_id: "frontier:rev-29"
selected_work_items: ["work:101", "work:104"]
action: "schedule"
policy_id: "control:portfolio-v1"
policy_version: "1.0.0"
score_refs: ["score:00042", "score:00043"]
budget_reservation: {compute_units: 120, wall_time_ms: 5000}
selection_reason: "diversity-and-information-gain"
random_seed_ref: "seed:run-9:decision-81"
event_id: "event:0081"
```

The controller MUST record decisions affecting search reachability, priority, retention, or termination. If stochastic policies are used, reproducibility metadata MUST include a seed or a documented nondeterminism boundary.

## 4. Mathematical Semantics

Let a Bucket state be \(B_t\), the current directional field be \(F_t\), and the active resource state be \(R_t\). A state-dependent generator proposes:

\[
C_t = G(B_t,F_t,R_t;\theta_G).
\]

A constraint plugin evaluates \(K(B_t,c)\in\{\mathrm{PASS},\mathrm{FAIL},\mathrm{UNKNOWN},\mathrm{ERROR}\}\). Only a sound, applicable `FAIL` finding can justify a hard-feasibility prune.

For candidate \(c\), let \(m_i(c,B_t)\) denote a measure and \(N_i\) its declared normalization. The objective vector is

\[
\mathbf{s}(c\mid B_t,F_t)=\big(N_1(m_1),\ldots,N_k(m_k)\big).
\]

A field-defined aggregation \(A_{F_t}\) yields a priority value:

\[
q(c\mid B_t,F_t)=A_{F_t}\big(\mathbf{s}(c\mid B_t,F_t)\big).
\]

The controller selects a work portfolio, not necessarily one winner:

\[
P_t=\Pi(\mathcal{W}_t,\{q(w)\},D_t,R_t,F_t),
\]

where \(\mathcal{W}_t\) is the frontier and \(D_t\) represents diversity or coverage constraints. Feedback \(Y_t\) may induce a *proposed* field update:

\[
\widehat F_{t+1}=U(F_t,Y_t,\mathcal H_t).
\]

The field actually deployed is \(F_{t+1}=\widehat F_{t+1}\) only after policy validation and approval; otherwise \(F_{t+1}=F_t\). These equations describe a family of algorithms, not a claim that every instantiation converges.

## 5. Objective and Measure Contracts

Every objective MUST specify: stable ID; orientation (maximize/minimize/target); measure ID and version; unit; normalization profile; handling of unknown values; uncertainty representation; and provenance requirements. Measures SHOULD report whether their values are observed, estimated, predicted, or imputed.

### 5.1 Recommended objective families

- Structural plausibility: coherence of candidate relations under non-hard evidence.
- Expected information gain: anticipated reduction in uncertainty from a proposed probe.
- Feasible-region coverage: new regions or relation patterns reached.
- Novelty and residual reduction: unexplained structure addressed without double-counting.
- Computational cost: expected compute, latency, or external query expense.
- Hypothesis diversity: separation among retained explanations.
- Counterevidence exposure: ability to test falsifying alternatives.
- Risk and governance cost: privacy, operational, or misuse exposure.

An objective MUST NOT imply a universal definition of intelligence. Different applications MAY use different objective sets, but comparative experiments MUST disclose them.

### 5.2 Aggregation profiles

Supported profiles MAY include weighted sums, lexicographic preferences, Pareto-front selection, constrained utility, and risk-sensitive bounds. A weighted sum requires compatible normalization and a declared weight policy. Pareto methods MUST specify dominance and tie handling. Risk-sensitive policies MUST state whether uncertainty enters via lower-confidence bounds, penalties, robust worst-case values, or explicit exploration bonuses.

Scores from different field versions are not directly comparable unless a compatibility or rescoring rule is declared.

## 6. Uncertainty, Weak Evidence, and Counterevidence

Weak evidence may raise the *priority* of a candidate without raising its *verified status*. Scorers MUST distinguish at least:

- **Hard feasibility:** independently determined by constraint plugins.
- **Evidence assessment:** support, contradiction, provenance, dependence, and reliability.
- **Directional utility:** estimated value of exploring a hypothesis next.
- **Decision confidence:** uncertainty in the controller's priority estimate.

A scorer SHOULD expose uncertainty intervals, qualitative uncertainty classes, or a documented alternative. If evidence sources are correlated, the scoring profile MUST specify how dependence is detected or bounded. Duplicate or derivative observations MUST NOT be counted as independent confirmations without justification.

A conforming system SHOULD reserve some budget for counterevidence or alternative hypotheses, particularly when feedback is derived from previously prioritized candidates. Field updates MUST NOT convert a self-generated prediction into independent observational evidence.

## 7. Coupling Generation and Selection

Directional fields can affect the generator's proposal distribution and the controller's selection policy. This coupling MUST remain inspectable:

1. The generator receives a versioned field reference or immutable field snapshot.
2. Each generated candidate records generator and field provenance.
3. The scorer evaluates candidates against a declared field and Bucket snapshot.
4. The controller records which proposals were selected, deferred, or discarded.
5. Feedback updates may propose a new field, but MUST NOT rewrite historical candidate or score records.

This design permits genuinely coupled generation–selection rather than a static candidate list followed by a score. It also permits ablation tests with generation-only, selection-only, both, and neither guided by a field.

## 8. Frontier and Work-Item Semantics

A `WorkItem` MUST identify its Bucket, proposed operation, state revision, estimated cost, status, and provenance. Recommended statuses are `READY`, `RESERVED`, `RUNNING`, `DEFERRED`, `COMPLETED`, `INVALIDATED`, `FAILED`, and `CANCELLED`.

- `READY -> RESERVED` requires a budget reservation.
- `RESERVED -> RUNNING` requires confirmation that the relevant Bucket and policy revisions remain acceptable.
- `RUNNING -> COMPLETED` records result references and actual cost.
- `READY/DEFERRED -> INVALIDATED` requires an explicit state, constraint, or policy reason.
- `FAILED` records recoverability and retry policy.

The frontier MUST distinguish **not yet examined** from **proven impossible**. Budget exhaustion, temporary quiescence, and sound closure are different terminal conditions. A controller MUST NOT label a budget-terminated search as exhaustive.

## 9. Search Policy Contract

A policy MUST declare:

- Eligible work-item types and lifecycle states.
- Scoring and ranking method, including missing-score handling.
- Exploration/exploitation rule and any minimum exploration quota.
- Portfolio diversity and deduplication rules.
- Tie-breaking, randomization, and reproducibility semantics.
- Aging, starvation prevention, and deferred-work revisit policy.
- Budget and deadline behavior.
- Error, timeout, and stale-snapshot behavior.

### 9.1 Search policies and completeness

Beam width, top-K pruning, score thresholds, and heuristic rejection can improve efficiency but may sacrifice completeness. Such actions MUST be labeled **policy exclusion**, **deferment**, or **heuristic pruning**, not sound constraint pruning. Conditional completeness claims require a specified generator coverage assumption, fair scheduling policy, finite or effectively enumerable reachable state space, and adequate budget.

### 9.2 Diversity-preserving portfolio

A controller SHOULD be able to retain mutually competing hypotheses when evidence is insufficient to resolve them. Diversity may be based on structural distance, explanation equivalence classes, causal alternatives, evidence-source independence, or coverage of disjoint regions. Diversity metrics MUST be versioned and should not be confused with truthfulness.

## 10. Budget and Resource Allocation

A `BudgetLedger` MUST track authorized limits, reserved amounts, actual consumption, and remaining resources. Resource types MAY include compute units, wall time, memory, external tool calls, evidence-acquisition cost, and risk budget. Reservation and actual expenditure MUST be distinguishable.

A controller MUST NOT schedule work exceeding a hard budget unless the governance profile explicitly permits an overrun and records authorization. It SHOULD use cost estimates to allocate effort across exploration, exploitation, verification, and counterevidence. An information-gain estimate does not authorize unlimited evidence collection or access to restricted data.

## 11. Feedback Taxonomy

Feedback events MUST identify what was measured and by which protocol. Recommended types:

| Type | Example | Appropriate use |
|---|---|---|
| Feasibility feedback | constraint contradiction confirmed | refine candidate feasibility model |
| Evidence feedback | independent observation supports or challenges hypothesis | update evidence assessments |
| Search efficiency feedback | compute used per feasible candidate | tune scheduling |
| Coverage feedback | new structurally distinct feasible region | tune generation/exploration |
| Calibration feedback | predicted vs observed outcomes | tune uncertainty and scoring |
| Governance feedback | privacy boundary or policy violation | block or rollback a policy |

Feedback MUST carry provenance, timestamp or event sequence, subject ID, measurement version, and validation status. Training feedback and held-out evaluation feedback MUST be separable to prevent evaluation leakage.

## 12. Field Adaptation and Governance

Field adaptation follows a controlled lifecycle:

`PROPOSED -> VALIDATING -> {APPROVED | REJECTED} -> DEPLOYED -> {RETIRED | ROLLED_BACK}`.

An update proposal MUST identify the parent field, exact parameter or component changes, evidence used, intended scope, and predicted benefit. Approval SHOULD require held-out or prospective validation, hard-invariant checks, and regression comparisons. Field updates MUST NOT mutate the historical interpretation of prior decisions. Rollback MUST restore an immutable prior version and record why the replacement was withdrawn.

An implementation MAY use multi-agent proposals, evolutionary optimization, or learned policies. None of these constitutes demonstrated RSI without measured improvement in the search mechanism on independent tasks under a controlled evaluation protocol.

## 13. Core Interfaces

### 13.1 Score request and response

```text
score(request: {
  bucket_snapshot_ref,
  candidate_refs[],
  field_snapshot_ref,
  constraint_snapshot_ref,
  evidence_snapshot_ref,
  scoring_profile_id,
  evaluation_context
}) -> {
  score_records[],
  unsupported_objectives[],
  errors[],
  scorer_version,
  event_ref
}
```

Scoring MUST be side-effect-free with respect to Bucket feasibility state. Partial responses MUST identify missing or failed components. Implementations SHOULD support deterministic replay for fixed snapshots and declared random seeds.

### 13.2 Select work

```text
select(request: {
  frontier_snapshot_ref,
  score_record_refs[],
  policy_snapshot_ref,
  budget_snapshot_ref,
  governance_snapshot_ref
}) -> {
  selected_work_refs[],
  deferred_work_refs[],
  invalidated_work_refs[],
  reservations[],
  decision_record_ref,
  errors[]
}
```

Selection MUST NOT implicitly accept a structural hypothesis. A controller MUST reject stale or incompatible score records, or rescore under a declared compatibility policy.

### 13.3 Propose field update

```text
propose_field_update(request: {
  parent_field_ref,
  feedback_refs[],
  training_window_ref,
  evaluation_protocol_ref,
  governance_profile_ref
}) -> {
  proposed_field_ref,
  change_manifest_ref,
  validation_plan_ref,
  status
}
```

The updater MUST NOT self-deploy a field when approval is required by the governance profile.

## 14. Compatibility and Snapshot Consistency

A scoring or control decision MUST reference compatible Bucket, field, constraint, evidence, and policy snapshots. If any referenced snapshot changes before execution, the implementation MUST apply a declared strategy: revalidate, rescore, rebase, or cancel. Silent mixing of incompatible revisions is prohibited.

Schema evolution MUST use explicit version identifiers. Unknown required fields MUST cause a validation error; unknown optional fields MAY be ignored if the profile permits it. A field's objective ID MUST NOT silently change meaning across versions.

## 15. Events and Auditability

A minimal event chain SHOULD include `FIELD_CREATED`, `CANDIDATE_PROPOSED`, `SCORE_COMPUTED`, `WORK_SELECTED`, `BUDGET_RESERVED`, `WORK_COMPLETED`, `FEEDBACK_RECORDED`, `FIELD_UPDATE_PROPOSED`, `FIELD_UPDATE_VALIDATED`, `FIELD_DEPLOYED`, and `FIELD_ROLLED_BACK`.

Events MUST support attribution to a run, actor or service identity, object revision, and causal predecessors. Privacy-sensitive provenance MAY be pseudonymized or access-controlled; auditability does not require publishing sensitive raw records.

## 16. Multi-Agent and Structural Relay

Agents MAY specialize in generating, scoring, adversarial checking, exploration, or policy improvement. Cross-agent messages MUST include versioned object references, evidence provenance, declared authority, and a receiving-side validation status. A receiving agent MUST NOT inherit a sender's directional score as an independently validated fact. Relay may transfer candidate structures, failed search trails, residuals, or policy proposals; transfer does not imply correctness or domain portability.

For competing agents, the controller SHOULD avoid winner-take-all feedback that prematurely suppresses alternatives. A shared portfolio can combine independent exploration with periodic evidence reconciliation and explicit conflict reporting.

## 17. Safety, Privacy, and Domain Boundaries

Directional control can intensify surveillance or bias when applied to human-related inference. A domain profile MUST define permissible evidence sources, authorization boundaries, data minimization, retention, access control, and limits on identity claims. For blockchain actor analysis, behavioral clustering MUST NOT be presented as proof of a real-world identity without independent corroboration and appropriate authorization. IP addresses, device fingerprints, or public keys are not inherently unique person identifiers.

A controller MUST NOT use directional utility to bypass privacy constraints, authorization requirements, or hard governance rules. The system SHOULD report uncertainty and alternative explanations in consequential applications.

## 18. Reference Control Loop (Illustrative)

```python
def directional_search(initial_bucket, field, budgets, services):
    frontier = services.frontier.initialize(initial_bucket)
    history = []
    while frontier.has_schedulable_work() and budgets.available():
        snapshot = services.snapshot.capture(frontier, field, budgets)
        proposals = services.generator.propose(snapshot, field)
        checked = services.constraints.evaluate(proposals, snapshot)
        # Only sound, applicable FAIL may be hard-pruned.
        eligible = [p for p in checked if not p.sound_hard_fail]
        scores = services.scorer.score(eligible, snapshot, field)
        decision = services.controller.select(frontier, eligible, scores, budgets)
        services.audit.record(decision)
        results = services.executor.execute_with_revalidation(decision)
        frontier = services.frontier.integrate(results)
        budgets = services.budgets.reconcile(results)
        feedback = services.feedback.assess(results)
        history.append(feedback)
        proposal = services.field_updater.maybe_propose(field, history)
        if proposal and services.governance.validate_and_approve(proposal):
            field = services.fields.deploy_immutable(proposal)
    return services.report.build(frontier, budgets, field, history)
```

An actual implementation MUST handle failures, retries, cancellation, concurrent revisions, work-item invalidation, and distinct termination statuses. The loop is a reference architecture, not a claim of verified executable behavior.

## 19. Conformance Profiles

### Profile A — Directional Scoring Core

Requires immutable fields, objective and measure contracts, explicit missing-data behavior, score provenance, feasibility/priority separation, and snapshot consistency.

### Profile B — Controlled Search

Includes Profile A plus work-item lifecycle, auditable selection, budgets, exploration policy, and explicit termination semantics.

### Profile C — Adaptive Directional Control

Includes Profile B plus feedback provenance, gated field updates, rollback, and held-out evaluation controls.

### Profile D — Multi-Agent Relay

Includes Profile C plus cross-agent provenance, version negotiation, receiving-side validation, and portfolio conflict handling.

A conformance report MUST name its profile, versions, optional features, known deviations, and test evidence.

## 20. Conformance Test Matrix

| ID | Test | Expected result |
|---|---|---|
| DSC-001 | Field missing objective version | reject invalid field |
| DSC-002 | Objective orientation absent | reject or explicitly map under profile |
| DSC-003 | Missing score component | preserve `missing`, no silent zero |
| DSC-004 | Weighted aggregation example | reproduce 0.73 under declared profile |
| DSC-005 | Hard `FAIL` from sound plugin | permit sound pruning with proof reference |
| DSC-006 | `UNKNOWN` constraint result | retain as unresolved, not hard-fail |
| DSC-007 | Low directional score | defer/policy-exclude, not mark infeasible |
| DSC-008 | Evidence source duplicated | apply dependence rule; no double confirmation |
| DSC-009 | Score uses stale Bucket snapshot | reject, revalidate, or rescore explicitly |
| DSC-010 | Field version changes | preserve old scores and rescore if needed |
| DSC-011 | Frontier contains competing hypotheses | preserve per diversity policy |
| DSC-012 | Budget reservation exceeds limit | deny without explicit override |
| DSC-013 | Actual cost differs from estimate | reconcile budget ledger |
| DSC-014 | Budget exhaustion | report partial termination, not closure |
| DSC-015 | Quiescent frontier | report quiescence separately from proof of closure |
| DSC-016 | Heuristic beam discard | label policy exclusion, not sound pruning |
| DSC-017 | Deterministic replay with fixed snapshots | reproduce decision under declared profile |
| DSC-018 | Randomized selection | record seed/nondeterminism boundary |
| DSC-019 | Field update trained on feedback | require separate validation before deployment |
| DSC-020 | Rejected field update | leave deployed field unchanged |
| DSC-021 | Rollback | restore prior immutable version and audit |
| DSC-022 | Cross-agent score relay | receiving agent preserves source and authority |
| DSC-023 | Counterevidence contradicts favored candidate | update evidence and re-evaluate priority |
| DSC-024 | Generator changes with field | record both generator and field versions |
| DSC-025 | Unapproved evidence source | block collection/use per governance profile |
| DSC-026 | Search policy risks starvation | enforce declared fairness/aging rule |
| DSC-027 | Corrupted provenance chain | flag nonconformance and quarantine record |
| DSC-028 | Measure changes meaning under same ID | reject incompatible versioning |
| DSC-029 | Candidate accepted solely due to priority | reject invalid transition |
| DSC-030 | Agent claims RSI from repeated search | reject unsupported improvement claim |

Passing these tests establishes contract behavior for the tested configuration, not global algorithmic soundness or empirical usefulness.

## 21. Evaluation Protocol and Falsifiable Hypotheses

A validation program SHOULD compare at least four matched baselines: (A) dynamic generation with no directional guidance; (B) generation-guided only; (C) selection-guided only; and (D) coupled generation and selection. Add fixed-field versus adaptively updated-field variants when studying learning. Hold constraint plugins, budgets, and task distributions constant where possible.

Suggested metrics include feasible-hypothesis discovery rate, time or compute to first valid hypothesis, solution diversity, calibrated information gain, independent counterevidence coverage, false exclusion rate, policy regret, and performance on held-out task families. Report medians, dispersion, seeds, budget sensitivity, and failed runs.

- **H1:** Coupled guidance improves feasible-structure discovery per compute unit over unguided dynamic search on at least some structured task families.
- **H2:** Explicit weak-evidence uncertainty reduces premature policy exclusion relative to uncalibrated point estimates.
- **H3:** Diversity-preserving portfolios improve recovery from misleading early evidence.
- **H4:** Counterevidence allocation reduces self-confirming search trajectories.
- **H5:** Gated field adaptation improves held-out performance more reliably than unconstrained online adaptation.
- **H6:** Snapshot-version discipline improves reproducibility and auditability under concurrent agents.
- **H7:** Cost-aware scheduling improves utility per bounded resource on heterogeneous workloads.
- **H8:** Improvements in search efficiency need not imply improvement in attribution correctness or real-world identity inference.

These are research hypotheses, not established results. Negative outcomes should be retained as structural learning evidence.

## 22. Failure Modes and Mitigations

| Failure mode | Consequence | Mitigation |
|---|---|---|
| Field collapse into one objective | neglected alternatives | diversity quotas, Pareto selection |
| Feedback self-reinforcement | spurious confidence | held-out tests, counterevidence, provenance |
| Score/feasibility conflation | unsound pruning | authority separation, conformance tests |
| Objective drift | incomparable scores | immutable field and measure versions |
| Distribution shift | misdirected exploration | scope checks, recalibration, fallback |
| Cost underestimation | budget overrun | reservations, reconciliation, caps |
| Starvation of low-priority regions | lost feasible hypotheses | fairness, aging, bounded exploration |
| Correlated evidence | inflated support | dependency graphs and conservative aggregation |
| Multi-agent consensus illusion | false independence | lineage-aware relay and source tracking |
| Adaptation overfit | apparent RSI without transfer | independent evaluation and rollback |
| Sensitive-source leakage | privacy harm | source authorization and data minimization |

## 23. Implementation Roadmap

**Stage 1 — Contract harness.** Implement field schemas, scoring records, version validation, and deterministic tests with synthetic measures.

**Stage 2 — Controlled frontier.** Add work-item lifecycle, budget ledger, score-based scheduling, and transparent deferment/termination reporting.

**Stage 3 — Coupled ablations.** Integrate field-aware generation and selection, then compare factorial ablations on reproducible synthetic starmap tasks.

**Stage 4 — Evidence and feedback.** Add provenance-aware weak evidence, counterevidence budgets, calibrated uncertainty, and held-out field update gates.

**Stage 5 — Multi-agent relay.** Add interoperable agent services, versioned relay units, portfolio reconciliation, and policy rollback tests.

Each stage SHOULD publish its conformance profile, datasets or generation seeds, negative cases, evaluation scripts, and known limitations before claiming improvement.

## 24. Relationship to the D-BTP Research Program

This specification operationalizes the central idea that structural generation and directional selection are **organically coupled**, not merely two sequential independent modules. `SPEC-001` defines what a Bucket is; `SPEC-002` defines how candidates and constraints are handled; this document defines how limited attention and computation are directed, recorded, and adapted. `SPEC-004-Evidence-Relay-and-Learning-Lifecycle.md` is expected to specify the detailed lifecycle of evidence, relay artifacts, and validated learning across runs and agents.

The design also interfaces conceptually with UCPSF (scoring/control planes), BM-ODWEI and REN (directional weak evidence), AQSI (autonomous question generation), UIERU (relay units), and SIF (structural growth). Such conceptual connections do not imply implementation interoperability without explicit mappings and conformance tests.

## 25. Open Questions

1. Under which generator coverage and scheduler fairness assumptions can conditional completeness be established?
2. Which field representations best balance interpretability, expressiveness, and computational cost?
3. Can directional guidance be learned without inheriting the search policy's selection bias?
4. How should multi-objective Pareto portfolios be bounded under tight memory budgets?
5. When should counterevidence collection take priority over exploiting a high-scoring hypothesis?
6. Which measures of novelty and residual reduction remain stable across domains?
7. How can field updates be tested for transfer rather than task-specific overfitting?
8. What are the minimal cryptographic or content-addressing requirements for trustworthy multi-agent provenance?
9. How should risk, privacy, and human oversight be represented in a general search-control profile?
10. What empirical evidence would distinguish adaptive search from genuine improvement of the search-generating mechanism?

## 26. Conclusion

Directional scoring is a mechanism for allocating search attention under uncertainty. It is not an oracle of feasibility or truth. A robust D-BTP implementation couples dynamic candidate generation, directional selection, and feedback while preserving the boundaries between hard constraints, weak evidence, policy choices, and validated learning. This specification makes those boundaries explicit, testable, and auditable. Its central engineering rule is simple: **guide aggressively when useful, but validate claims and preserve the right to explore alternatives.**

---

*Research note:* This is a proposed specification and test framework. No experimental performance, deployment readiness, completeness, or real-world attribution accuracy is asserted. Contributions, counterexamples, and alternative profiles are welcome through an evidence-preserving collective-learning process.
