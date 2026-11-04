# START HERE — D-BTP

## Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution

**Research orientation · Proposed v1.0.0 · Apache-2.0**

> **Status and scope.** D-BTP is a proposed research framework with formalization and implementation contracts, not a demonstrated general-purpose solver. The documents distinguish proposed mechanisms, conditional correctness properties, and testable hypotheses from empirical results. No performance, open-ended intelligence, or recursive self-improvement claim should be read as established without independent validation.

## 1. What Is This Repository About?

**Dynamic Bucket Tree of Permutation (D-BTP)** explores a family of structural-search problems in which candidate relations, constraints, evidence, and search priorities can change as a hypothesis is developed. Its starting point is **BTP** for starmap matching, metric similarity, and unaligned structural correspondence. Its broader question is:

> Can a search system generate new structural possibilities from its evolving state, use directional information to decide what to explore, enforce constraints without confusing plausibility with feasibility, and learn from validated feedback?

The distinctive proposal is **coupling**, rather than a pipeline that generates every candidate first and scores them afterward. Directional fields can guide *what is generated*, *what is evaluated next*, *where computation is spent*, and *what evidence is sought*. Verified outcomes can subsequently modify those fields. This feedback loop is a design hypothesis to be tested, not a guarantee of improvement.

## 2. The Two-Minute Mental Model

Imagine matching two graphs whose nodes and edges represent structural observations. At first, several node correspondences seem plausible. Accepting one correspondence reveals another possible relation; rejecting it rules out some combinations; a newly observed relation changes which alternatives are worth exploring. A fixed candidate list may be convenient, but it may miss these **state-dependent discoveries**.

D-BTP represents a partial search result as a **dynamic bucket** containing:

- A **hypothesis ledger** recording accepted, excluded, pending, and deferred decisions.
- A **structural state** describing current correspondences and their constraints.
- An **evidence state** recording supporting and contrary observations with provenance.
- A **directional state** describing goals, perspectives, uncertainty, and search priorities.
- **Metadata and lineage** supporting versioning, budgets, audit, and replay.

At each step, the system generates candidates based on its current bucket, checks applicable hard constraints, and selects among admissible branches using directional objectives. It may seek discriminating evidence, retain alternative hypotheses, or end with explicit unresolved work.

```text
                    +-----------------------------+
                    | Dynamic Bucket State (B_t)  |
                    | hypotheses / structure /    |
                    | evidence / directions       |
                    +-------------+---------------+
                                  |
                                  v
                    State-dependent candidate generation
                                  |
                                  v
                      Constraint-plugin evaluation
                       /          |           \
                   FAIL        UNKNOWN        PASS
                    |             |             |
             justified reject  defer/test    admissible
                                                |
                                                v
                                    Directional prioritization
                                                |
                                                v
                                  branch / evidence / feedback
                                                |
                                                +----> update B_(t+1)
                                                +----> revise guidance
```

**Critical distinction:** a low directional score is not a proof of infeasibility. Weak evidence may help choose which hypothesis to investigate, but it cannot alone justify a hard rejection.

## 3. What Is New, and What Is Not Claimed?

D-BTP investigates four related extensions of the original structural-matching setting:

1. **Dynamic candidate discovery.** New candidates may emerge from prior accept/exclude decisions and constraint propagation.
2. **Constraint-guided structural composition.** Hypotheses are combined only when their required structural conditions are met; uncertain constraints remain explicit.
3. **Directional generation–selection coupling.** Multiple objectives and weak signals influence both proposal and priority, with feedback potentially revising search guidance.
4. **Relay and evolutionary extensions.** Hypotheses, evidence, search strategies, and eventually generation operators may be exchanged, tested, and improved across agents or tasks.

These ideas overlap with established areas such as constraint programming, heuristic search, active learning, Bayesian hypothesis evaluation, graph matching, multi-objective optimization, and multi-agent systems. The repository's contribution is a proposed **integrated structural contract and research program**; it does not claim these individual ingredients were invented here or that the combination has already surpassed established methods.

## 4. Choose Your Reading Path

### Path A — First-time reader (about 30–45 minutes)

1. [README.md](README.md) — scope, principles, and repository map.
2. [D-BTP-001 — From Metric Similarity to Structural Hypothesis Search](docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md) — why the search formulation is generalized.
3. [D-BTP-002 — Dynamic Bucket States and Candidate Generation](docs/foundations/D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md) — how the state and candidate frontier evolve.
4. [D-BTP-004 — Directional Fields for Generation and Selection](docs/foundations/D-BTP-004-Directional-Fields-for-Generation-and-Selection.md) — the central generation–selection coupling.
5. [CASE-002 — Dynamic Starmap Similarity](docs/cases/CASE-002-Dynamic-Starmap-Similarity.md) — return to the original structural-matching problem.

### Path B — Algorithm and implementation researcher

Read [D-BTP-002](docs/foundations/D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md), [D-BTP-003](docs/foundations/D-BTP-003-Constraint-Guided-Structural-Composition.md), and [D-BTP-006](docs/foundations/D-BTP-006-Coupled-Generation-Selection-and-Feedback.md), followed by the four contracts in `docs/specifications/`:

- [SPEC-001 — Dynamic Bucket State Contract](docs/specifications/SPEC-001-Dynamic-Bucket-State-Contract.md)
- [SPEC-002 — Candidate Generation and Constraint Plugins](docs/specifications/SPEC-002-Candidate-Generation-and-Constraint-Plugins.md)
- [SPEC-003 — Directional Scoring and Search Control](docs/specifications/SPEC-003-Directional-Scoring-and-Search-Control.md)
- [SPEC-004 — Evidence Relay and Learning Lifecycle](docs/specifications/SPEC-004-Evidence-Relay-and-Learning-Lifecycle.md)

**Recommended sequence:** define state invariants → implement a reference candidate generator → establish hard-constraint correctness → add directional policies → test feedback → consider agent relay. **Conformance before runtime optimization.**

### Path C — Weak evidence and directional intelligence

Read [D-BTP-004](docs/foundations/D-BTP-004-Directional-Fields-for-Generation-and-Selection.md), [D-BTP-005 — Weak Evidence and Directional Exploration](docs/foundations/D-BTP-005-Weak-Evidence-and-Directional-Exploration.md), [D-BTP-006](docs/foundations/D-BTP-006-Coupled-Generation-Selection-and-Feedback.md), and [EXT-002 — Recursive Directional Field Evolution](docs/extensions/EXT-002-Recursive-Directional-Field-Evolution.md).

Focus on **evidence reliability**, **dependency and double-counting**, **counterevidence**, **calibration**, and **adaptive-policy evaluation**. A promising search hint is not a validated causal explanation.

### Path D — Multi-agent, relay, and RSI research

Read [D-BTP-007 — Multi-Agent RSI and Collective Structural Learning](docs/foundations/D-BTP-007-Multi-Agent-RSI-and-Collective-Structural-Learning.md), [CASE-003 — Multi-Agent Hypothesis Competition](docs/cases/CASE-003-Multi-Agent-Hypothesis-Competition.md), [SPEC-004](docs/specifications/SPEC-004-Evidence-Relay-and-Learning-Lifecycle.md), and [EXT-003 — Open-Ended BTP and Structural Relay](docs/extensions/EXT-003-Open-Ended-BTP-and-Structural-Relay.md).

Distinguish *more agents*, *more hypothesis diversity*, *cross-task learning*, and *validated self-improvement*. None entails the others automatically.

### Path E — Applications and limits

Read [CASE-001 — Blockchain Actor Attribution](docs/cases/CASE-001-Blockchain-Actor-Attribution.md) and [CASE-002](docs/cases/CASE-002-Dynamic-Starmap-Similarity.md). The blockchain case studies **behavioral/structural attribution hypotheses**; they do not justify identifying real-world people from uncertain associations. Respect privacy, authorization, evidence quality, and domain-specific legal requirements.

## 5. Complete Research Map

| Track | Documents | Core question |
|---|---:|---|
| Foundations | D-BTP-001–008 | What is dynamic, directional structural hypothesis search? |
| Specifications | SPEC-001–004 | What states, interfaces, invariants, and lifecycle rules are required? |
| Cases | CASE-001–003 | How could the mechanisms be exercised and compared? |
| Extensions | EXT-001–003 | What might biomimetic, recursive, and open-ended extensions require? |

### Foundations

- [001 — From Metric Similarity to Structural Hypothesis Search](docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md)
- [002 — Dynamic Bucket States and Candidate Generation](docs/foundations/D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md)
- [003 — Constraint-Guided Structural Composition](docs/foundations/D-BTP-003-Constraint-Guided-Structural-Composition.md)
- [004 — Directional Fields for Generation and Selection](docs/foundations/D-BTP-004-Directional-Fields-for-Generation-and-Selection.md)
- [005 — Weak Evidence and Directional Exploration](docs/foundations/D-BTP-005-Weak-Evidence-and-Directional-Exploration.md)
- [006 — Coupled Generation, Selection and Feedback](docs/foundations/D-BTP-006-Coupled-Generation-Selection-and-Feedback.md)
- [007 — Multi-Agent RSI and Collective Structural Learning](docs/foundations/D-BTP-007-Multi-Agent-RSI-and-Collective-Structural-Learning.md)
- [008 — Open-Ended Structural Evolution and Intelligence](docs/foundations/D-BTP-008-Open-Ended-Structural-Evolution-and-Intelligence.md)

### Cases and extensions

- [CASE-001 — Blockchain Actor Attribution](docs/cases/CASE-001-Blockchain-Actor-Attribution.md)
- [CASE-002 — Dynamic Starmap Similarity](docs/cases/CASE-002-Dynamic-Starmap-Similarity.md)
- [CASE-003 — Multi-Agent Hypothesis Competition](docs/cases/CASE-003-Multi-Agent-Hypothesis-Competition.md)
- [EXT-001 — Biomimetic Directional Intelligence](docs/extensions/EXT-001-Biomimetic-Directional-Intelligence.md)
- [EXT-002 — Recursive Directional Field Evolution](docs/extensions/EXT-002-Recursive-Directional-Field-Evolution.md)
- [EXT-003 — Open-Ended BTP and Structural Relay](docs/extensions/EXT-003-Open-Ended-BTP-and-Structural-Relay.md)

For a navigable index, consult [CONTENTS.md](CONTENTS.md) when available. For terminology, see [GLOSSARY.md](GLOSSARY.md) when available.

## 6. Eight Planned Figures

The repository's figure plan is:

| Figure | Topic |
|---|---|
| Fig-001 | D-BTP Grand Architecture |
| Fig-002 | From Static to Dynamic BTP |
| Fig-003 | Dynamic Bucket State and Candidate Generation |
| Fig-004 | Constraint-Guided Structural Hypothesis Search |
| Fig-005 | Directional Generation and Selection Coupling |
| Fig-006 | Weak Evidence and Multi-Directional Scoring |
| Fig-007 | Blockchain Actor Attribution BTP |
| Fig-008 | Recursive Structural Evolution and Collective Learning |

The individual files are intended for `figures/` with the names specified in the repository plan. **Before publication, verify that each figure actually exists as an independent PNG and that all links resolve.** A composite eight-panel illustration is not, by itself, eight separate repository assets.

## 7. How to Evaluate the Research Claims

A useful first experiment is **synthetic dynamic starmap matching** with known ground truth, controlled candidate visibility, and a reproducible budget. Compare:

1. A fixed-candidate BTP or graph-matching baseline.
2. Dynamic candidate generation without directional guidance.
3. Dynamic generation with a fixed directional field.
4. Dynamic generation with feedback-updated guidance.
5. Multi-agent competition with and without shared learning, where relevant.

Keep the underlying data, allowed information, hard constraints, time budget, and evaluation criteria comparable. Report at least:

- **Solution quality:** structural consistency, ground-truth accuracy, and quality of the top-*k* hypotheses.
- **Search efficiency:** expanded states, constraint checks, wall-clock time, and compute cost.
- **Discovery:** useful candidates found after state updates that were absent from the initial frontier.
- **Evidence behavior:** calibration, false rejections, counterevidence handling, and robustness to misleading hints.
- **Reproducibility:** random seeds, plugin versions, search-policy versions, and complete termination status.
- **Agent overhead:** communication, coordination, and duplicated work.

Use ablations to identify *which mechanism* produces any gain. Dynamic search can be more expensive than static search on simple or fully enumerated tasks. Neither improved benchmark scores nor repeated self-modification alone demonstrates open-ended intelligence or RSI.

For the complete agenda, see [TESTABLE-HYPOTHESES.md](TESTABLE-HYPOTHESES.md) and [VALIDATION-ROADMAP.md](VALIDATION-ROADMAP.md) when available.

## 8. Common Misreadings

| Misreading | Correct interpretation |
|---|---|
| “Dynamic” means an unlimited search space. | The candidate frontier changes with state; computation remains budgeted and may be incomplete. |
| “Directional” means proven correctness. | Directional signals prioritize exploration; only valid constraints justify hard exclusion. |
| A high similarity score proves common identity. | Similarity supports a hypothesis under assumptions; attribution and real-world identification are separate claims. |
| “Closed,” “quiescent,” and “out of budget” mean the same thing. | They are distinct termination conditions and must be reported separately. |
| Multi-agent agreement establishes truth. | Agents can share biases and dependent evidence; independent validation remains necessary. |
| Self-modification is RSI. | Validated self-improvement requires controlled comparisons, generalization checks, and rollback. |
| Open-ended evolution has been demonstrated. | It is an extension and research hypothesis, not an established result of this repository. |

## 9. What Can a Contributor Work On?

Promising contributions include:

- A minimal reference implementation of the **Dynamic Bucket State Contract** with event logs and replay.
- A constraint-plugin test suite distinguishing **Fail**, **Unknown**, and **Error**.
- Synthetic benchmark generators for **state-dependent candidate emergence**.
- Directional-policy baselines and ablations, including **misleading weak evidence**.
- Portfolio search that preserves diverse, competing structural hypotheses.
- Agent-relay conformance tests with provenance and independent verification.
- Formal analyses of **conditional completeness**, admissible pruning, and safe state merging.
- Negative results identifying cases where D-BTP adds cost without benefit.

A strong contribution states its assumptions, defines measurable outcomes, preserves unresolved cases, and reports counterexamples. The framework is intended to remain open to correction, alternative formulations, and collective learning.

## 10. Suggested Next Steps

**For readers:** start with Foundations 001, 002, and 004, then choose a track above.

**For implementers:** begin with SPEC-001 and SPEC-002, and test conformance before adding adaptive direction fields.

**For evaluators:** establish static and unguided dynamic baselines before measuring feedback or multi-agent gains.

## 11. Citation, License, and Research Integrity

The proposed repository license is **Apache License 2.0**. Follow the repository's `LICENSE` and `CITATION.cff` once published. Do not infer a DOI from this guide: a persistent identifier should be added only after the relevant archive release has actually received one.

The repository favors **specifications and contracts first, conformance before runtime, explicit unresolved work, and collective-learning-friendly publication**. Claims about algorithmic advantage, general intelligence, or biological mechanisms are hypotheses unless independently supported.

---

**Next document:** [CONTENTS.md](CONTENTS.md).
