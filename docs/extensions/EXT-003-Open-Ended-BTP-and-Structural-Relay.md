# EXT-003 — Open-Ended BTP and Structural Relay

**Project:** D-BTP — Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution  
**Document class:** Research extension / hypothesis and architecture proposal  
**Status:** v1.0.0 research proposal; not an implementation or empirical result  
**License:** Apache-2.0

## Abstract

Dynamic Bucket Tree of Permutation (D-BTP) generalizes structural matching into a stateful search over composable hypotheses. Its core cycle couples candidate generation, constraint validation, directional selection, and evidence-driven feedback. This extension asks a further question: can the search process enlarge not only its collection of hypotheses but also the *structural vocabulary, generative operators, and reusable capabilities* with which future hypotheses are constructed? We propose an open-ended D-BTP architecture in which bounded, verifiable structural discoveries are packaged as relay units, evaluated across contexts, and selectively incorporated into future search systems. The proposal separates hypothesis-level expansion, representation-level innovation, operator-level adaptation, and system-level capability growth. It also specifies explicit residuals, governance gates, provenance, transfer contracts, and counterfactual evaluation. Open-endedness is a research target, not a guaranteed property of D-BTP; neither recursive modification nor accumulated artifacts alone establishes general intelligence or recursive self-improvement.

**Keywords:** dynamic BTP; open-ended search; structural relay; structural intelligence; compositional hypotheses; residual-driven growth; directional fields; collective learning; recursive self-improvement; capability transfer.

---

## 1. Motivation: Beyond a Larger Search Tree

A conventional search algorithm operates over a fixed representation and a fixed family of admissible moves. Dynamic BTP relaxes the assumption that all candidate relations must be enumerated in advance: the current Bucket state can generate new candidates, which are tested under constraints and prioritized by directional fields. Yet a dynamically generated candidate list may still inhabit a closed representational universe.

This extension distinguishes four questions:

1. **Which hypothesis should be explored next?** Search within an existing language.
2. **Which new structural description should become expressible?** Extend the language or schema.
3. **Which new construction or evaluation procedure should be available?** Extend the operator library.
4. **Which validated discovery should other agents or future tasks inherit?** Relay and capability accumulation.

The transition from the first question to the other three is the central subject of this document. It is not implied by larger compute budgets, longer search traces, or more agents.

## 2. Scope and Epistemic Boundaries

This document proposes mechanisms, interfaces, invariants, and experiments. It does **not** claim that D-BTP is complete for arbitrary structural discovery, that its search is polynomial-time, or that a prototype would constitute AGI or ASI. A system may generate an unbounded sequence of syntactically distinct artifacts without discovering useful new capabilities. Likewise, the appearance of novelty is not sufficient evidence of transferability.

The intended object of study is **controlled open-ended structural evolution**: the ability to propose extensions to the search system, verify them against specified contracts, and reuse successful extensions without silently invalidating earlier results.

## 3. From Dynamic Search to Open-Ended Evolution

Let a search configuration at time `t` be

\[
\mathcal{X}_t=(\mathcal{B}_t,\mathcal{L}_t,\mathcal{O}_t,\mathcal{D}_t,\mathcal{R}_t,\mathcal{K}_t),
\]

where:

- `B_t`: portfolio of dynamic Buckets and hypothesis ledgers;
- `L_t`: structural representation language, schemas, and relation types;
- `O_t`: admissible generation, validation, propagation, and scoring operators;
- `D_t`: directional fields and search-control policies;
- `R_t`: evidence, provenance, and residual records;
- `K_t`: validated reusable structural knowledge and relay artifacts.

An ordinary D-BTP transition updates the Bucket portfolio under a mostly fixed `L_t` and `O_t`. A proposed evolutionary transition may instead modify the language, operators, directional policies, or reusable knowledge:

\[
\mathcal{X}_{t+1}=\mathsf{GovernedUpdate}(\mathcal{X}_t,\Delta_t,\mathsf{Validation}_t).
\]

The update is **provisional** until relevant conformance, safety, and task-performance gates have been passed. A rejected proposal remains an auditable candidate, not a silently adopted capability.

## 4. Four Growth Frontiers

### 4.1 Hypothesis frontier

Contains unresolved candidate mappings, relations, compositions, and competing explanations within the current structural vocabulary. Its primary metric is useful hypothesis discovery under resource constraints.

### 4.2 Representation frontier

Contains proposed new types, abstractions, granularity levels, equivalence relations, or schema transformations. Its metric is whether the representation improves expressivity *without destroying interpretability, decidability of required checks, or backward compatibility where promised*.

### 4.3 Operator frontier

Contains proposed generators, constraint propagators, evidence acquisition methods, directional policies, and deduplication procedures. Its metric is incremental, reproducible performance on held-out tasks, including cost and error.

### 4.4 Relay frontier

Contains artifacts that have passed the applicable gates and can be imported into another task, agent, or system. Its metric is successful reuse under explicitly recorded assumptions. The four frontiers interact, but should not be collapsed into one scalar novelty score.

## 5. Residual-Driven Structural Invention

A residual is a structured description of what current hypotheses or operators fail to explain or accomplish. Examples include:

- Observations not covered by any feasible structural hypothesis;
- Recurring conflicts between otherwise plausible mappings;
- Repeated candidate-generation failures in a specific context;
- Evidence patterns that existing relation types cannot express;
- Excessive search cost concentrated in one subproblem;
- Cross-task transfer failures revealing missing preconditions.

A residual record should include its observation basis, applicable task scope, failure class, confidence, provenance, and alternative explanations. The system may then propose a minimal structural extension that would explain or resolve the residual.

**Important distinction:** A residual motivates an experiment; it does not establish that a new structural primitive is necessary. Existing models may be undertrained, misconfigured, or supplied with incomplete data.

## 6. Candidate Structural Extensions

We propose four extension classes:

| Class | Example | Main verification question |
|---|---|---|
| `RELATION` | New relation type between structural nodes | Is the relation well-defined and empirically useful? |
| `ABSTRACTION` | Higher-level motif or macro-node | Does compression preserve required constraints? |
| `OPERATOR` | New candidate generator or propagation rule | Is it sound where soundness is claimed? |
| `POLICY` | New directional search or resource policy | Does it improve held-out outcomes at acceptable cost? |

Each extension must specify an applicability domain and a **non-applicability domain** where known. Claims of generality are hypotheses requiring cross-domain evidence.

## 7. Coupling Directional Fields with Structural Invention

Directional fields may guide both ordinary hypothesis search and the invention of new structures. They may prioritize residuals according to expected information gain, task relevance, anticipated transfer value, verification cost, and risk.

A conceptual utility is:

\[
U(e\mid x)=w_1\,\widehat{\Delta Q}(e,x)+w_2\,\widehat{I}(e,x)
+w_3\,\widehat{T}(e,x)-w_4\,\widehat{C}(e,x)-w_5\,\widehat{R}(e,x),
\]

where `e` is a proposed extension, `x` the current context, and the terms estimate quality gain, information gain, transfer potential, verification cost, and risk. These estimates are **search heuristics**, not validity proofs. Weight selection, calibration, and sensitivity should be logged and evaluated.

Critically, the coupling is bidirectional: new representations can change which directional features are measurable; validated feedback can change which extensions are generated next. Neither operation authorizes bypassing hard constraints.

## 8. Structural Relay as the Growth Mechanism

Structural Relay transfers more than a textual answer. It transfers a *bounded, testable structural artifact* with enough context to assess whether it can be reused. A relay recipient should not have to infer hidden assumptions from the sender's prose.

We propose a **Structural Evolution Relay Unit (SERU)** as a conceptual extension of the Structural Hypothesis Unit (SHU) introduced in the D-BTP specifications. A SERU may package an ordinary hypothesis, a representation extension, an operator, or a directional-policy improvement.

### 8.1 Minimum SERU envelope

```yaml
seru_version: "0.1-proposal"
unit_id: "seru:example:0001"
kind: "OPERATOR"  # HYPOTHESIS | RELATION | ABSTRACTION | OPERATOR | POLICY
origin:
  agent_id: "agent-A"
  task_id: "synthetic-task-17"
  parent_unit_ids: []
artifact:
  reference: "content-addressed-artifact-id"
  schema_version: "operator-schema-v1"
contracts:
  inputs: ["bucket-state-v1"]
  outputs: ["candidate-set-v1"]
  preconditions: ["typed-graph-input"]
  invariants: ["no-unjustified-hard-rejection"]
evidence:
  supporting_refs: []
  counterevidence_refs: []
  provenance_refs: []
validation:
  status: "PROPOSED"  # PROPOSED | SANDBOXED | VERIFIED | REJECTED | REVOKED
  test_suite_ref: null
  benchmark_ref: null
  limitations: ["synthetic-only"]
governance:
  allowed_use: ["sandbox"]
  expiry_or_review: "review-required-before-production"
```

This is a **research example**, not a claim that an existing runtime implements the schema. A production contract must define canonical serialization, signature verification where needed, version compatibility, and explicit error semantics.

### 8.2 Relay lifecycle

`PROPOSED → SANDBOXED → VERIFIED → ADOPTED` is one possible success path. `REJECTED`, `QUARANTINED`, `REVOKED`, and `SUPERSEDED` are necessary alternative states. Adoption is recipient-specific: an artifact verified in one context is not automatically valid in another.

## 9. Transfer Contracts and Applicability

Every imported artifact should declare:

1. Input and output schema compatibility;
2. Semantic assumptions and preconditions;
3. Hard constraints that must remain invariant;
4. Evidence provenance and uncertainty;
5. Validation context, benchmarks, and known counterexamples;
6. Required resources and side effects;
7. Version, revocation, and rollback behavior.

A relay receipt should distinguish **received**, **parsed**, **compatible**, **validated**, and **adopted**. These are different events. In particular, receipt of an artifact is not evidence that its claims are true.

## 10. Collective Learning without Consensus Collapse

Multiple agents may discover distinct structural explanations or competing extensions. A collective-learning layer should preserve meaningful diversity rather than forcing an early majority vote. We propose a portfolio with explicit categories:

- Verified and broadly reusable;
- Verified under restricted assumptions;
- Promising but unverified;
- Contradicted or falsified;
- Deprecated, superseded, or revoked.

Negative results are relay-worthy when they contain reproducible counterexamples or failure conditions. Repeated agreement from agents trained on correlated evidence must not be counted as independent confirmation.

## 11. Multi-Agent Roles and Accountability

A practical experimental configuration may separate proposal generation, constraint verification, adversarial counterexample search, transfer testing, resource allocation, and governance approval. These are **logical roles**, not a requirement for six separate models. Independent validation matters more than the number of agents.

To limit correlated failure, evaluation should use disjoint holdout sets where feasible, alternate model families or verification methods when appropriate, and a traceable evidence-dependency graph.

## 12. Controlled Recursive Self-Improvement

An agent that proposes a new operator has modified its candidate toolkit; it has not thereby demonstrated RSI. A stronger RSI claim requires that the change is causally responsible for improved future capability under a controlled comparison and that the improvement is not merely due to additional compute, leaked evaluation data, or an easier task distribution.

We distinguish:

- **Search adaptation:** change the next candidate or its priority;
- **Policy learning:** update scoring or resource allocation;
- **Operator learning:** improve the generator or validator;
- **Recursive improvement:** validated improvements to the process that produces and evaluates further improvements.

A controlled upgrade should pass a predeclared test suite, held-out transfer tasks, regression tests, cost accounting, and rollback checks. Recursive upgrades should be rate-limited and monitored for specification drift.

## 13. Reference Architecture

```text
Observations / Tasks / Evidence
             |
             v
   Dynamic BTP Hypothesis Search <------ Directional Control Plane
             |                                  ^
             v                                  |
     Residual & Failure Registry ---------------+
             |
             v
  Structural Extension Generator
             |
             v
  Candidate SERU + Provenance
             |
             v
  Sandbox / Constraint / Counterexample Tests
             |
             v
  Held-out Evaluation + Transfer Trials
             |
             v
  Governance Gate ---- rejected/revoked ---> Audit Registry
             |
             v
  Versioned Relay & Capability Registry
             |
             +----> Recipient-Specific Validation
                          |
                          v
                   Future D-BTP Search
```

The arrows denote information and control flow, not proof of improvement. Every path back into future search should be versioned and reversible.

## 14. A Bounded Reference Algorithm

```text
procedure OPEN_ENDED_DBTP(task, base_system, budgets):
    state := initialize_search(task, base_system)
    registry := load_verified_artifacts(base_system)
    while within_budget(budgets):
        buckets := expand_and_validate_hypotheses(state)
        residuals := extract_auditable_residuals(buckets, task)
        if should_attempt_extension(residuals, budgets):
            proposals := generate_extension_candidates(residuals, state)
            for proposal in proposals:
                if not static_contract_check(proposal):
                    record_rejection(proposal, "contract")
                    continue
                sandbox_result := sandbox_test(proposal)
                counterexamples := adversarial_test(proposal)
                transfer_result := heldout_transfer_test(proposal)
                verdict := independent_governance_review(
                    proposal, sandbox_result, counterexamples, transfer_result)
                record_verdict(proposal, verdict)
                if verdict.allows_adoption:
                    unit := package_seru(proposal, verdict)
                    registry := versioned_adopt(registry, unit)
                    state := controlled_upgrade(state, unit)
        state := update_directional_policy_from_validated_feedback(state)
        if no_actionable_work(state) or task_stop_condition(state):
            break
    return report(state, registry, unresolved_residuals(state))
```

The procedure is deliberately abstract. Soundness of each hard-constraint plugin, semantics of `no_actionable_work`, and adoption authority must be specified in an implementation. Budget exhaustion is not a proof that all valid hypotheses have been explored.

## 15. Worked Synthetic Example: Discovering a Reusable Motif

Consider synthetic starmaps in which several small node clusters share a repeated three-edge motif. A baseline dynamic matcher treats each edge independently and repeatedly incurs the same constraint-propagation cost. A residual registry detects the recurrence of this expensive substructure.

**Proposal A:** Introduce a macro-node abstraction for the motif.  
**Proposal B:** Introduce a specialized candidate generator that proposes motif-level matches.  
**Proposal C:** Retain the original representation and tune the directional priority heuristic.

All three are legitimate competing hypotheses. The evaluator tests whether A preserves edge-level constraints, whether B misses valid mappings, and whether C achieves similar performance without representation change. Only after held-out evaluation could one claim that an extension yields a useful reusable capability. If motif-level abstraction hides a critical edge conflict, it must fail the relevant contract even if it appears faster.

This example is illustrative; no measured results are asserted.

## 16. When Relay Fails

Relay may fail because a structural relation changes meaning across domains, an operator assumes a different cardinality constraint, a policy overfits a benchmark, or evidence provenance cannot be checked. A receiver should be able to decline an artifact without losing the underlying hypothesis ledger.

A particularly important failure is **semantic laundering**: a weakly supported conjecture becomes labeled as established knowledge after several relay hops. Each hop must preserve the original epistemic status and add only the validation actually performed by that recipient.

## 17. Safety, Privacy, and Governance

Open-ended structural search can be applied to sensitive domains. Structural similarity or behavioral clustering must not be promoted into personal identity attribution without independent, lawful evidence and appropriate safeguards. Evidence stores should minimize personal data, enforce access controls, support retention limits, and prevent cross-task leakage.

Operator extensions should be sandboxed with explicit resource, data-access, and side-effect permissions. Governance should be capable of suspending or revoking an artifact and identifying dependent descendants that require reevaluation.

## 18. Core Invariants

**OE-01 — Constraint preservation.** An extension must not silently weaken a hard constraint.  
**OE-02 — Evidence separation.** Heuristic support is never automatically a proof of validity.  
**OE-03 — Provenance continuity.** Every adopted artifact traces to its source, dependencies, and tests.  
**OE-04 — Version coherence.** Search results identify the representation and operator versions used.  
**OE-05 — Reversible adoption.** An upgrade has a defined rollback or containment path.  
**OE-06 — Recipient validation.** Relay reception does not imply compatibility or acceptance.  
**OE-07 — Counterexample retention.** Known failures remain attached to affected artifacts.  
**OE-08 — Budget honesty.** Resource termination is distinct from search completeness.  
**OE-09 — Novelty discrimination.** Syntactic novelty is not equated with useful capability growth.  
**OE-10 — Causal evaluation.** Claimed improvement requires appropriate baselines and cost controls.  
**OE-11 — Portfolio diversity.** Alternative explanations are not discarded solely for weak heuristic ranking.  
**OE-12 — Revocation propagation.** Dependent artifacts are flagged when a parent is invalidated.

## 19. Testable Hypotheses

The following are **proposals for experiments**, not empirical findings.

| ID | Hypothesis | Falsifiable observation |
|---|---|---|
| H1 | Residual-driven extension proposals improve useful discovery per unit cost | No gain versus random or frequency-based proposals |
| H2 | A representation frontier improves transfer to structurally related unseen tasks | No gain over a fixed representation with equal compute |
| H3 | Operator relay reduces repeated search work | Imported operators add overhead or regress performance |
| H4 | Counterexample-preserving relay reduces invalid adoption | Failure rate unchanged versus provenance-only relay |
| H5 | Multi-directional portfolios discover more valid novel structures | Diversity rises but valid discovery does not |
| H6 | Recipient-specific validation reduces negative transfer | No reduction in transfer errors |
| H7 | Controlled recursive operator improvement produces compounding gains | Improvements plateau or disappear under held-out tests |
| H8 | Revocation propagation reduces downstream use of invalid artifacts | Dependency invalidations remain undetected |
| H9 | Explicit non-applicability contracts improve cross-domain precision | Transfer precision unchanged |
| H10 | Two-level search over hypotheses and operators outperforms a single fixed-operator search | No gain after accounting for operator-search cost |

## 20. Evaluation Protocol

Use synthetic typed-graph families with known ground truth, controllable structural shifts, and deliberately misleading weak evidence. Partition tasks into development, held-out within-family, and held-out cross-family sets. Pre-register metrics and computational budgets.

### Baselines

1. Static BTP with pre-enumerated candidates;
2. Dynamic BTP with fixed representation and operators;
3. Dynamic BTP with adaptive directional scoring only;
4. Dynamic BTP with extension generation but no relay;
5. Relay of unvalidated artifacts;
6. Proposed governed extension-and-relay architecture.

### Metrics

Report valid hypothesis recall, precision, constraint-violation rate, time-to-solution, compute and communication cost, representation complexity, operator regression rate, transfer success, negative transfer, provenance completeness, rollback success, and diversity of independently supported hypotheses. Include confidence intervals or repeated-run distributions where feasible.

For claims of cumulative improvement, plot performance against **total cumulative cost**, not only per-task runtime after prior training and exploration have been paid for.

## 21. Conformance Scenarios

- **CT-01:** Import a relay unit with an incompatible schema; receiver rejects it without mutating live state.
- **CT-02:** Import a generator that rejects valid candidates under an unproved heuristic; soundness claim is rejected.
- **CT-03:** Reuse an abstraction that hides a hard structural conflict; validation catches the conflict.
- **CT-04:** Re-relay a weakly supported hypothesis; its evidence status remains unchanged.
- **CT-05:** Revoke a parent operator; dependent units are flagged for revalidation.
- **CT-06:** Exhaust the exploration budget; system reports partial results, not completeness.
- **CT-07:** Produce syntactically novel but behaviorally equivalent operators; novelty metric does not credit capability growth.
- **CT-08:** Evaluate a candidate upgrade on leaked training tasks; governance gate rejects the performance claim.
- **CT-09:** Relay conflicting hypotheses; both remain representable with their provenance.
- **CT-10:** Roll back an adopted operator; prior state and result versions remain auditable.
- **CT-11:** A receiver changes constraint cardinality assumptions; compatibility is reevaluated.
- **CT-12:** A directional policy ranks a candidate poorly; hard feasibility remains independent of that rank.

## 22. Implementation and Research Roadmap

**Phase 1 — Bounded search baseline.** Implement reproducible dynamic Bucket states, constraints, candidate generation, and fixed directional policies. Establish baseline quality and cost.

**Phase 2 — Residual registry.** Add structured failure descriptions and counterexample retention. Measure whether residual categories predict productive extension proposals.

**Phase 3 — Sandboxed extension frontier.** Support one extension class at a time, starting with new candidate generators. Require versioned contracts, test fixtures, and rollback.

**Phase 4 — Relay interoperability.** Exchange validated artifacts between isolated agents and domains. Measure compatibility, transfer benefit, and negative transfer.

**Phase 5 — Controlled recursive experiments.** Permit improvements to extension-generation and evaluation policies only after independent validation. Assess whether improvements persist under new task families and full cost accounting.

## 23. Relationship to the D-BTP Corpus

- **D-BTP-001–003:** Structural hypothesis search, dynamic states, and constraint-guided composition provide the base semantics.
- **D-BTP-004–006:** Directional fields, weak evidence, and coupled feedback provide the exploration mechanism.
- **D-BTP-007:** Multi-agent RSI and collective learning introduce cooperation, competition, and validated reuse.
- **D-BTP-008:** Open-ended structural evolution motivates the distinction between candidate growth and capability growth.
- **SPEC-001:** Bucket-state identity, versioning, and lifecycle remain binding.
- **SPEC-002:** Generator and constraint-plugin contracts govern new operators.
- **SPEC-003:** Directional scoring and search control govern resource allocation.
- **SPEC-004:** Evidence relay and learning lifecycle govern provenance and adoption.
- **CASE-001–003:** Attribution, starmap matching, and multi-agent hypothesis competition provide candidate evaluation settings.
- **EXT-001:** Biomimetic directional intelligence suggests functional analogies for active exploration.
- **EXT-002:** Recursive directional field evolution studies search-policy improvement; this document adds representation/operator evolution and cross-system relay.

Related SI ideas include residual-driven growth, structural folding/unfolding, UIERU-style relay, AQSI-style autonomous questioning, and SSICR-style competing strategy portfolios. These are conceptual connections; interoperability is subject to explicit contracts rather than assumed from shared terminology.

## 24. Open Research Questions

1. What minimal extension language can express genuinely new structural operators while keeping verification tractable?
2. Can a system distinguish missing evidence from missing representation without exhaustive search?
3. How should novelty, compression, transfer, and explanatory value be jointly evaluated without rewarding artifacts that merely game the metric?
4. Which classes of operator modifications permit formal soundness proofs, and which require empirical risk bounds?
5. How can weak evidence guide invention without becoming self-confirming evidence?
6. When does the cost of an extension frontier exceed the benefit of adaptive search in a fixed language?
7. What evidence supports a claim of recursive improvement rather than benchmark adaptation?
8. How can independent agents validate artifacts while minimizing duplicated computation?
9. What is the right unit of transfer: hypothesis, motif, operator, policy, or a composite capability?
10. How can a system revoke a widely reused but subsequently falsified structural abstraction?
11. How can open-endedness be operationalized on finite experiments without making untestable claims?
12. Which domain shifts expose the limits of a proposed general structural primitive?

## 25. Conclusion

D-BTP offers a useful starting point for studying structural evolution because it already treats hypotheses as dynamically generated, constrained, directionally prioritized, and revisable. A further research program can treat *representations, operators, and transferable structural capabilities* as candidates for the same disciplined cycle. The essential advance would not be unlimited branching; it would be the verified creation and reuse of new ways to search.

Structural Relay is the proposed bridge from local discovery to collective capability accumulation. Its value depends on provenance, compatibility, counterexamples, recipient-specific validation, and reversible adoption. Open-ended structural intelligence therefore remains a falsifiable architectural hypothesis, with explicit limits and measurable milestones—not a property established by naming the mechanism.

---

### Research note

This document is a conceptual research extension for the D-BTP corpus. Equations, schemas, and algorithms are proposed models; numerical performance and capability claims require future implementation and independent empirical validation.
