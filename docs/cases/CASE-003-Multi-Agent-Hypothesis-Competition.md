# CASE-003 — Multi-Agent Hypothesis Competition

**Project:** D-BTP — Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution  
**Document class:** Research case / proposed experimental protocol  
**Status:** Conceptual design; no empirical performance claims  
**Version:** 1.0.0

## Abstract

This case examines how multiple agents can jointly explore a dynamic structural-hypothesis space while maintaining competing explanations, independently checking constraints, seeking counterevidence, and relaying reusable discoveries. The objective is not to make agents agree quickly. It is to improve the quality, diversity, auditability, and cost-effectiveness of the hypotheses considered under a finite budget. We propose a reproducible synthetic benchmark, a versioned Structural Hypothesis Unit (SHU), an arbitration protocol, explicit directional control, and ablation studies that distinguish the effects of competition, evidence sharing, feedback adaptation, and verified recursive self-improvement (RSI). Multi-agent operation is treated as an architectural hypothesis to test, not as a guarantee of superior inference.

## 1. Research question and scope

A conventional search controller may operate one frontier, one candidate generator, and one scoring policy. D-BTP allows the frontier to evolve as structural decisions change the set of generable hypotheses. A multi-agent variant asks whether independent agents with complementary policies can discover useful alternatives that a single controller overlooks.

The central question is:

> Under equivalent evidence access and computational budgets, when does controlled multi-agent competition produce better structural hypotheses than a single-agent dynamic BTP search?

This case concerns synthetic structural puzzles and auditable hypothesis reasoning. It does not require identification of real persons or unrestricted access to external data. It assumes the state, generation, constraints, directional scoring, and relay contracts defined in SPEC-001 through SPEC-004.

## 2. Relationship to the D-BTP foundations

D-BTP-001 frames structural matching as hypothesis search. D-BTP-002 specifies dynamic Bucket states and state-dependent candidate generation. D-BTP-003 separates hard constraints from evidence-based preferences. D-BTP-004 and D-BTP-005 describe directional fields and weak-evidence exploration. D-BTP-006 couples generation, selection, and feedback. D-BTP-007 provides the multi-agent and collective-learning motivation, while D-BTP-008 distinguishes bounded search from open-ended structural evolution.

This case turns those ideas into a controlled experiment: agents may propose different branches, but their claims remain subject to common validity rules and independent review.

## 3. Problem model

Let a structural task be

$$
\mathcal T=(X,\mathcal R,\mathcal C_h,\mathcal E,\mathcal B,\mathcal O),
$$

where $X$ denotes observed structural elements, $\mathcal R$ possible relations, $\mathcal C_h$ hard constraints, $\mathcal E$ available evidence, $\mathcal B$ a resource budget, and $\mathcal O$ evaluation objectives. A hypothesis $h$ is a partial or complete structural assignment. Its feasibility is

$$
F(h)=\bigwedge_{c\in\mathcal C_h}c(h),
$$

where unresolved constraints may return `UNKNOWN`, not automatically `PASS`. Feasible hypotheses are ranked using evidence and directional objectives, which must not redefine feasibility.

Each agent $a_i$ maintains a local view $\mathcal B_{i,t}$, a directional policy $\pi_{i,t}$, and an evidence ledger. The collective system maintains a shared registry of versioned hypotheses and provenance, not a single unquestioned consensus.

## 4. Synthetic benchmark: the hidden relay network

Consider a generated network of six observed event nodes $e_1,\ldots,e_6$ and four latent functional units $u_A,u_B,u_C,u_D$. The ground-truth simulator constructs a directed workflow with branching, a shared relay unit, and occasional missing observations. Each observed event has a timestamp band, an operation label, and noisy relation evidence. The agent's task is to infer a parsimonious latent structural explanation consistent with known hard rules.

The generator controls:

- **Ambiguity:** multiple latent assignments explain the same observations.
- **Missingness:** some edges or node attributes are hidden.
- **Distractors:** noisy similarities favor an incorrect but plausible grouping.
- **Constraint strength:** some relation types are mutually exclusive while others allow many-to-one assignment.
- **Evidence dependence:** several signals may derive from one shared underlying source.
- **Novelty:** later tasks introduce unseen motifs or a changed relation grammar.

The simulator stores the ground truth separately from agents. Synthetic identifiers and features are used throughout; no real-world identity attribution is involved.

## 5. Competing initial hypotheses

For illustration, three plausible starting hypotheses are:

| Hypothesis | Structural explanation | Initial attraction | Key vulnerability |
|---|---|---|---|
| H-A | One central relay explains events $e_2,e_3,e_5$ | Strong temporal co-occurrence | May violate capacity or ordering constraints |
| H-B | Two specialized relays divide those events | Better operation-type consistency | Requires an additional latent unit |
| H-C | One relay plus an unobserved intermediate unit | Explains missing edge pattern | Adds unsupported structural complexity |

These are **illustrative hypotheses, not computed results**. A valid search should allow all three to remain live until evidence or sound constraints distinguish them. A high initial score for H-A cannot be treated as proof that H-B and H-C are false.

## 6. Agent roles and independence

A reference configuration includes six logical roles. They may be implemented as separate processes or as isolated policies within one runtime.

1. **Generator agent:** proposes new assignments, splits, merges, and relation hypotheses based on the current Bucket.
2. **Constraint agent:** independently evaluates hard rules, propagates sound implications, and returns proof or diagnostic artifacts.
3. **Directional explorer:** prioritizes candidates using specified objectives and uncertain evidence.
4. **Counterevidence agent:** seeks observations or counterexamples that discriminate among leading hypotheses.
5. **Portfolio steward:** preserves non-dominated, diverse alternatives and allocates search budgets.
6. **Relay auditor:** validates SHU provenance, versions, compatibility, and the distinction between findings and unverified proposals.

Role separation is not evidence of statistical independence. If all agents share one model, training corpus, or data source, correlated errors must be measured explicitly. Independent constraint implementations and withheld test cases provide stronger checks than differently worded agent prompts alone.

## 7. Structural Hypothesis Unit (SHU)

A relayable SHU carries sufficient information for another agent to inspect, challenge, or extend a hypothesis.

```yaml
shu_id: shu-example-014
schema_version: 1.0
hypothesis:
  assignments: ["e2 -> uA", "e3 -> uA"]
  proposed_relations: ["uA -> uC"]
  unresolved: ["source of e5"]
constraints:
  checked:
    - rule_id: ordering-v2
      outcome: PASS
      checker_version: 2.1
  pending: [capacity-v1]
evidence:
  supporting: [obs-12, obs-19]
  counter: [obs-23]
  dependencies: [[obs-12, obs-19]]
directional_assessment:
  objectives: [coverage, simplicity, discrimination]
  status: provisional
provenance:
  producing_agent: generator-A
  parent_shu_ids: [shu-example-009]
  task_version: synthetic-task-07
  timestamp: logical-step-42
lifecycle: proposed
```

A SHU's lifecycle can include `proposed`, `under_review`, `contested`, `validated_for_scope`, `superseded`, and `archived`. `validated_for_scope` means the stated checks passed within a specified domain and version; it does not mean the hypothesis is universally true.

## 8. Competition and arbitration protocol

Competition should be explicit and bounded:

**Round 1 — Independent proposals.** Generator policies receive the same task specification and evidence snapshot, but may use different exploration objectives. Each submits a bounded number of SHUs.

**Round 2 — Constraint review.** A separate checker classifies each proposal as `PASS`, `FAIL`, `UNKNOWN`, or `ERROR`, with a rule identifier and reproducible diagnostic. Only soundly established failures justify feasibility pruning.

**Round 3 — Adversarial challenge.** The counterevidence role identifies a falsifiable distinction between leading candidates. Challenges may request new synthetic observations or propose a test; requests consume budget.

**Round 4 — Portfolio arbitration.** The steward selects a diverse set of feasible or provisionally feasible hypotheses. Ranking is based on declared objectives, evidence uncertainty, novelty, and expected information gain. The selection record preserves rejected alternatives and reasons.

**Round 5 — Feedback.** Confirmed simulator feedback updates local evidence and, when permitted, the directional policy. Any policy update is versioned and evaluated against held-out tasks before promotion.

Arbitration never converts agent vote counts into hard truth. A majority can share the same error.

## 9. Directional competition without premature convergence

Let each agent have a vector-valued assessment

$$
\mathbf s_i(h)=(s_{\text{fit}},s_{\text{coverage}},s_{\text{simplicity}},s_{\text{novelty}},s_{\text{information}}).
$$

A controller may assign an agent-specific priority

$$
P_i(h)=w_i^\top\mathbf s_i(h)+\beta_i U_i(h)-\lambda_i C_i(h),
$$

where $U_i$ represents uncertainty or exploration value and $C_i$ expected computation cost. This is a scheduling heuristic, not a feasibility theorem or calibrated probability unless separately validated.

The portfolio should include Pareto-non-dominated candidates and optionally reserve a fraction of budget for deliberately different hypotheses. Diversity can be measured by assignment disagreement, graph edit distance, or distinct explanatory motifs. A quota prevents the highest-scoring policy from monopolizing all future generation.

## 10. Dynamic candidate generation

Candidate sets are conditional on current structural decisions:

$$
\mathcal K_{i,t}=G_i(\mathcal B_{i,t},\mathcal E_t,\pi_{i,t},\mathcal R_t).
$$

Accepting a relation may reveal a new candidate through constraint propagation or an inferred motif. Rejecting one relation may trigger a split hypothesis or an alternative latent node. Thus, generation and selection interact: a directional field influences which branch is explored, while that branch changes the future generable space.

A candidate generator must report its generation scope and any known incompleteness. If a generator cannot enumerate all relevant candidates, the system must not claim that a quiescent frontier proves exhaustive search.

## 11. Hard constraints versus weak evidence

Hard constraints include rules explicitly guaranteed by the synthetic task, such as a prohibited operation transition or an impossible temporal ordering. Soft evidence includes noisy co-occurrence, partial motif similarity, and learned directional predictions. Conditional constraints apply only when their preconditions are established.

For example, a strong temporal association between $e_2$ and $e_3$ may raise the priority of a shared-unit hypothesis, but it cannot establish identity of the latent unit. Conversely, a verified task rule forbidding one unit from executing two simultaneous exclusive operations can invalidate a proposed assignment. Unknown timestamps must not be treated as proof of exclusivity.

## 12. Evidence independence and provenance

Suppose two evidence features, $z_1$ and $z_2$, derive from the same underlying observation. Treating them as independent can inflate support. SHUs therefore carry evidence dependency identifiers. An evaluator should either use an explicit dependence-aware model or conservatively avoid double counting. Agents should record when they derive claims from another agent's SHU; relay is not independent corroboration.

A useful audit graph links each conclusion to its source observations, transformations, checker versions, and parent hypotheses. This graph enables selective invalidation when a source is corrected or withdrawn.

## 13. Counterevidence and active tests

The counterevidence agent asks questions designed to separate hypotheses rather than merely confirm the current leader. Given hypotheses $h_a,h_b$, a proposed test $q$ may be prioritized by expected discrimination:

$$
V(q)=\mathbb E[\Delta D(h_a,h_b)\mid q]-\eta\mathrm{Cost}(q),
$$

where $D$ is a declared measure of distinguishability. Expected values require either a simulator model or explicitly acknowledged approximations. In a synthetic environment, an active test may reveal a withheld event attribute or evaluate a specific relation, subject to a common evidence-query budget.

Negative results remain first-class evidence and can revise a directional field without erasing the history of why a hypothesis was explored.

## 14. Relay and collective learning

Agents may relay four kinds of artifacts: structural hypotheses, constraint certificates, evidence-dependency annotations, and validated policy improvements. Receiving an artifact requires schema validation, scope compatibility, version checking, and independent acceptance of its claims.

Collective learning occurs when experience from multiple tasks improves future search, for example by identifying which candidate-generation motifs or counterevidence tests are useful in certain problem classes. A shared precedent registry should store both successes and failures, including cases where a popular heuristic produced a false lead.

The relay system should retain explicit leftovers: unresolved hypotheses, rejected but instructive branches, and unexplained residuals. Repeated execution can itself create useful comparative evidence, but repeated agreement is not necessarily independent validation.

## 15. Controlled RSI: a separate threshold

Changing the Bucket state is ordinary search. Updating a scoring weight from feedback is adaptive control. Sharing effective motifs across agents is collective learning. **RSI** is a stronger claim: a system modifies its own search machinery and demonstrates that the modification improves performance under independent evaluation.

A proposed improvement therefore follows:

`candidate modification -> sandbox tests -> held-out comparison -> safety/conformance checks -> versioned promotion or rollback`.

Changes to hard-constraint semantics require especially strong review. An agent must not weaken a constraint merely because it blocks a favored hypothesis. Report the scope and cost of any demonstrated improvement; do not infer unbounded self-improvement from one benchmark.

## 16. Reference orchestration pseudocode

```python

def competitive_dynamic_btp(task, agents, budget, registry):
    frontier = initialize_diverse_buckets(task)
    portfolio = []
    while budget.remaining() and frontier:
        snapshot = select_snapshot(frontier, budget)
        proposals = bounded_parallel_generate(agents.generators, snapshot)
        for proposal in proposals:
            if not schema_and_provenance_valid(proposal):
                registry.record_rejection(proposal, "invalid-envelope")
                continue
            result = agents.constraint_checker.check(proposal, task.rules)
            registry.record_check(proposal, result)
            if result.status == "FAIL" and result.sound_certificate:
                continue
            if result.status == "ERROR":
                quarantine_for_review(proposal)
                continue
            frontier.add(proposal)  # PASS or UNKNOWN, with status preserved
        challenges = agents.counterevidence.propose(frontier, budget)
        observations = execute_bounded_tests(challenges, task, budget)
        update_evidence_with_dependencies(frontier, observations)
        portfolio = agents.steward.select_diverse(frontier, budget)
        registry.relay_reviewed(portfolio)
        frontier = schedule_next(frontier, portfolio, budget)
    return portfolio, registry.audit_log(), termination_reason(frontier, budget)
```

The pseudocode omits implementation details such as concurrency locks, deterministic replay, and safe state equivalence. It is a protocol sketch, not a tested reference implementation. In particular, a sound certificate requires a trusted checker; a plugin's unverified assertion of soundness is insufficient.

## 17. Baselines and ablation design

All comparisons should use matched wall-clock and/or normalized compute budgets, equivalent evidence-query allowances, and the same synthetic task distribution.

| Configuration | Dynamic generation | Multiple agents | Counterevidence | Shared learning |
|---|---|---|---|---|
| B0: Static BTP | No | No | No | No |
| B1: Dynamic BTP | Yes | No | No | No |
| B2: Dynamic + directional | Yes | No | No | No |
| B3: Independent ensemble | Yes | Yes | No | No |
| B4: Competition + challenges | Yes | Yes | Yes | No |
| B5: Relay + collective learning | Yes | Yes | Yes | Yes |
| B6: Controlled RSI candidate | Yes | Yes | Yes | Versioned policy changes |

B6 must be evaluated on held-out tasks after each proposed change. Improvements attributable only to additional compute, leaked ground truth, or a larger evidence budget should not be credited to competition or RSI.

## 18. Evaluation metrics

**Hypothesis quality:** ground-truth structural precision/recall, graph-edit distance, relation F1, and top-K oracle coverage on synthetic tasks.

**Search effectiveness:** best feasible objective reached per compute unit, time to first valid solution, number of unique feasible hypotheses, and coverage of distinct structural motifs.

**Evidence discipline:** rate of unsupported hard rejections, calibration where probabilistic confidence is claimed, duplicate-evidence inflation, counterevidence discovery rate, and provenance completeness.

**Collective value:** transfer improvement on held-out task families, reduction in repeated invalid branches, useful relay acceptance rate, and robustness to a misleading agent.

**Governance:** rollback success, replay determinism within declared nondeterministic tolerances, audit completeness, and rate of unauthorized constraint changes.

Report distributions and confidence intervals across independent task seeds. Averages alone may conceal catastrophic failures or collapse in difficult cases.

## 19. Testable hypotheses

- **H1 — Diversity:** Under a fixed budget, competitive agents improve top-K structural diversity over a single directional controller on ambiguous tasks.
- **H2 — Validity:** Independent constraint checking reduces unsupported feasibility claims compared with unchecked agent voting.
- **H3 — Counterevidence:** Dedicated challenge agents reduce persistence of misleading high-scoring hypotheses when distractor evidence is present.
- **H4 — Relay:** Versioned SHU exchange reduces duplicated search effort without increasing false corroboration when provenance is enforced.
- **H5 — Adaptation:** Collective learning improves held-out search efficiency on recurring structural motifs, compared with task-local feedback alone.
- **H6 — Novelty:** Diverse generator policies increase discovery of valid unseen motifs, provided candidate-coverage reporting is honest.
- **H7 — RSI discipline:** Promotion gates reject harmful policy modifications more reliably than immediate online deployment.
- **H8 — Boundary conditions:** Multi-agent overhead can outweigh benefits on small, deterministic, fully constrained tasks.

Each hypothesis is falsifiable; none is reported here as empirically established.

## 20. Failure modes and safeguards

| Failure mode | Mechanism | Safeguard |
|---|---|---|
| Premature consensus | Agents converge on one early explanation | Diversity quotas and independent generation |
| Correlated hallucination | Shared model produces matching unsupported claims | Independent rule checker and source lineage |
| Evidence laundering | Relayed claim treated as new observation | Provenance dependency graph |
| Soft-to-hard promotion | Low score used as infeasibility proof | Typed constraint outcomes and proof checks |
| Agent gaming | Policies optimize leaderboard proxy | Held-out evaluation and multiple objectives |
| Search explosion | Dynamic generation grows combinatorially | Explicit budgets, deduplication, bounded branching |
| Unsafe deduplication | Distinct states merged under weak fingerprints | State-equivalence contract and conservative merging |
| Feedback contamination | Evaluation answers leak into training | Separate task partitions and immutable test sets |
| Relay incompatibility | Different rule or schema versions mixed | Versioned envelopes and compatibility checks |
| False RSI claims | Ordinary adaptation called self-improvement | Explicit promotion and transfer criteria |

## 21. Minimal conformance scenarios

1. A proposed SHU with an absent parent reference is quarantined rather than silently accepted.
2. Two agents repeat one source observation; the system records a single dependency lineage.
3. A checker returns `UNKNOWN`; the candidate remains provisional, not automatically feasible or infeasible.
4. A valid hard-constraint failure prevents the corresponding branch from entering the feasible portfolio.
5. An agent submits a high-scoring but invalid hypothesis; arbitration does not override the hard failure.
6. A challenge invalidates the current leader; alternative hypotheses remain recoverable.
7. A new candidate becomes generable only after a state transition; the dynamic generator discovers it.
8. A relay carries a different task-rule version; the receiver requires compatibility review.
9. A policy update improves training tasks but harms held-out tasks; promotion is rejected.
10. A budget expires with unresolved candidates; the result is marked budget-terminated, not exhaustively closed.
11. A generator claims frontier closure without coverage evidence; the system labels the result quiescent only.
12. A repeated experiment reproduces the audit trail under fixed seeds and declared deterministic components.

## 22. Suggested experimental phases

**Phase A — Single-agent control:** implement a synthetic task generator, trusted constraint checker, state ledger, and reproducible dynamic BTP baseline.

**Phase B — Competitive search:** introduce multiple generation policies and compare diversity and quality under matched budgets.

**Phase C — Adversarial evidence:** introduce distractors and active counterevidence queries; measure false-lead persistence.

**Phase D — Structural relay:** add SHU exchange, dependency tracking, and cross-task precedent retrieval; test transfer and contamination resistance.

**Phase E — Controlled improvement:** propose versioned modifications to generators or directional policies; use held-out gates and rollback to evaluate RSI claims.

Each phase should have exit criteria, a published failure report, and a frozen evaluation protocol before advancing.

## 23. Interpretation and limits

Multi-agent competition is valuable only when its additional perspectives produce independently useful search information. An ensemble of nearly identical agents can consume more resources while reproducing the same mistakes. Likewise, structural relay may accelerate reuse but can amplify errors if provenance and receiving-side validation are weak.

The synthetic benchmark provides a controlled environment for attributing performance differences to architectural components. It does not establish effectiveness on open-world attribution, scientific discovery, or other high-stakes applications. Such transfers require separate datasets, domain-specific constraints, and additional governance.

The D-BTP framework offers a way to test how dynamic hypothesis generation, directional selection, counterevidence, and collective learning interact. The strongest defensible outcome would be a reproducible map of **when** and **why** competitive structural search helps—not a universal assertion that more agents are always better.

## 24. Connections and next steps

- **SPEC-001:** Dynamic Bucket state and lifecycle contract.
- **SPEC-002:** Candidate generation and constraint plugin contract.
- **SPEC-003:** Directional scoring and search-control contract.
- **SPEC-004:** Evidence relay and learning lifecycle contract.
- **CASE-001:** Blockchain actor attribution as a domain-specific structural hypothesis problem.
- **CASE-002:** Dynamic starmap similarity as a controlled matching benchmark.
- **EXT-001:** Biomimetic directional intelligence as a bounded analogy.
- **EXT-002:** Recursive evolution of directional fields and policies.
- **EXT-003:** Open-ended structural relay and growth.

## 25. Conclusion

Multi-agent D-BTP can be understood as a **competition of auditable structural explanations**, not a competition of unverified assertions. Agents contribute by generating different candidates, checking constraints, challenging weak evidence, and relaying reusable discoveries. A directional control plane manages finite attention while preserving alternatives. Collective learning becomes meaningful when validated experience changes later behavior; RSI requires a further, independently verified improvement in the search machinery itself.

The proposed case supplies a benchmark and contract-oriented protocol for testing these distinctions. Its success or failure should be established experimentally, with explicit resource accounting, soundness boundaries, and reproducible evidence trails.

---

*Research note:* This document proposes an architecture and experimental design. Examples, agent outputs, and hypotheses are illustrative. No benchmark results or production capabilities are claimed.
