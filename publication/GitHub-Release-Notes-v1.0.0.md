# D-BTP v1.0.0 — Initial Research Release

**Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution**

**Release type:** Initial research framework and specification release  
**Version:** `v1.0.0`  
**License:** Apache-2.0  
**Status:** Research proposals, formal design contracts, and validation agenda; not a claim of experimentally demonstrated general superiority or autonomous intelligence.

## Overview

D-BTP extends the Bucket Tree of Permutation (BTP) from structural matching and metric-similarity search toward **dynamic, constraint-guided structural hypothesis exploration**. Instead of assuming that every candidate correspondence is enumerated before search begins, a dynamic bucket can generate new candidate hypotheses as its structural state changes. Directional fields influence what is generated, what is investigated next, and how limited resources are allocated. Evidence and counterevidence feed back into future search decisions.

The central research proposition is that **structural generation and directional selection can form a coupled, feedback-driven process**. This release specifies that process, its correctness boundaries, and an experimental program for determining when it helps.

## What is new in v1.0.0

### 1. Dynamic buckets and candidate generation

- Bucket states retain a hypothesis ledger, evolving structural representation, evidence provenance, directional state, and versioned metadata.
- Candidate generators may propose new relations, compositions, and alternative explanations based on the current bucket state.
- Search distinguishes a genuinely closed branch from a temporarily quiescent branch or one stopped by resource limits.
- Deduplication and state merging require explicit equivalence conditions; heuristic similarity alone is insufficient for sound merging.

### 2. Constraint-guided structural composition

- Constraint plugins evaluate structural feasibility and propagate implications as hypotheses are accepted, rejected, or deferred.
- Hard constraints are separated from conditional assumptions and soft evidence.
- **Sound pruning** requires a justified impossibility result, not merely a low heuristic score.
- Plugin interfaces support declared capabilities, versions, provenance, and conformance tests.

### 3. Directional generation–selection coupling

- Directional fields can guide candidate generation, branch ordering, evidence acquisition, and resource allocation.
- Multiple fields can represent competing objectives, perspectives, and uncertainty.
- Feedback can update guidance, while validation gates prevent untested policy changes from being treated as established improvements.
- The framework distinguishes generation, scoring, control, and constraint semantics even when they interact closely at runtime.

### 4. Weak evidence and counterevidence

- Weak evidence may have **search utility** without establishing a hypothesis as true.
- Provenance and dependence tracking aim to prevent correlated signals from being counted as independent support.
- Counterevidence search and alternative-hypothesis portfolios are first-class design elements.
- Directional hints must not silently become hard exclusions.

### 5. Structural relay, collective learning, and controlled RSI

- Proposed exchange units carry hypotheses, supporting and conflicting evidence, constraint context, versions, and unresolved questions.
- Multi-agent configurations can compete, cross-check, and relay reusable structural findings.
- The research agenda distinguishes ordinary state updates, adaptive search, collective learning, self-modification, and **validated recursive self-improvement**.
- Any proposed improvement requires independent evaluation, reproducibility, and rollback criteria.

### 6. Open-ended structural evolution

The extension studies four potential growth frontiers: **hypotheses, representations, operators, and relay mechanisms**. These are research directions, not demonstrated properties of a released implementation.

## Research contents

This initial research package comprises **18 research papers** organized as follows. Paths below are relative to the repository root.

### Foundations (8)

1. [`D-BTP-001 — From Metric Similarity to Structural Hypothesis Search`](docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md)
2. [`D-BTP-002 — Dynamic Bucket States and Candidate Generation`](docs/foundations/D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md)
3. [`D-BTP-003 — Constraint-Guided Structural Composition`](docs/foundations/D-BTP-003-Constraint-Guided-Structural-Composition.md)
4. [`D-BTP-004 — Directional Fields for Generation and Selection`](docs/foundations/D-BTP-004-Directional-Fields-for-Generation-and-Selection.md)
5. [`D-BTP-005 — Weak Evidence and Directional Exploration`](docs/foundations/D-BTP-005-Weak-Evidence-and-Directional-Exploration.md)
6. [`D-BTP-006 — Coupled Generation, Selection and Feedback`](docs/foundations/D-BTP-006-Coupled-Generation-Selection-and-Feedback.md)
7. [`D-BTP-007 — Multi-Agent RSI and Collective Structural Learning`](docs/foundations/D-BTP-007-Multi-Agent-RSI-and-Collective-Structural-Learning.md)
8. [`D-BTP-008 — Open-Ended Structural Evolution and Intelligence`](docs/foundations/D-BTP-008-Open-Ended-Structural-Evolution-and-Intelligence.md)

### Specifications (4)

1. [`SPEC-001 — Dynamic Bucket State Contract`](docs/specifications/SPEC-001-Dynamic-Bucket-State-Contract.md)
2. [`SPEC-002 — Candidate Generation and Constraint Plugins`](docs/specifications/SPEC-002-Candidate-Generation-and-Constraint-Plugins.md)
3. [`SPEC-003 — Directional Scoring and Search Control`](docs/specifications/SPEC-003-Directional-Scoring-and-Search-Control.md)
4. [`SPEC-004 — Evidence Relay and Learning Lifecycle`](docs/specifications/SPEC-004-Evidence-Relay-and-Learning-Lifecycle.md)

### Cases (3)

1. [`CASE-001 — Blockchain Actor Attribution`](docs/cases/CASE-001-Blockchain-Actor-Attribution.md)
2. [`CASE-002 — Dynamic Starmap Similarity`](docs/cases/CASE-002-Dynamic-Starmap-Similarity.md)
3. [`CASE-003 — Multi-Agent Hypothesis Competition`](docs/cases/CASE-003-Multi-Agent-Hypothesis-Competition.md)

### Extensions (3)

1. [`EXT-001 — Biomimetic Directional Intelligence`](docs/extensions/EXT-001-Biomimetic-Directional-Intelligence.md)
2. [`EXT-002 — Recursive Directional Field Evolution`](docs/extensions/EXT-002-Recursive-Directional-Field-Evolution.md)
3. [`EXT-003 — Open-Ended BTP and Structural Relay`](docs/extensions/EXT-003-Open-Ended-BTP-and-Structural-Relay.md)

## Figures

Eight figure subjects are defined for the research package:

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

See [`FIGURE-INDEX.md`](FIGURE-INDEX.md) for canonical filenames and insertion guidance. **Release check:** ensure all eight independent, legible PNG assets actually exist in `figures/`; an eight-panel composite does not by itself satisfy those eight paths.

## Navigation and research infrastructure

- [`README.md`](README.md) — project overview and design principles
- [`START-HERE.md`](START-HERE.md) — reading paths
- [`CONTENTS.md`](CONTENTS.md) — document inventory and cross-references
- [`GLOSSARY.md`](GLOSSARY.md) — terminology and symbols
- [`FIGURE-INDEX.md`](FIGURE-INDEX.md) — figure descriptions and insertion guidance
- [`FUTURE-DIRECTIONS.md`](FUTURE-DIRECTIONS.md) — longer-term research directions
- [`OPEN-QUESTIONS.md`](OPEN-QUESTIONS.md) — unresolved research questions
- [`TESTABLE-HYPOTHESES.md`](TESTABLE-HYPOTHESES.md) — falsifiable propositions and baselines
- [`VALIDATION-ROADMAP.md`](VALIDATION-ROADMAP.md) — staged verification program
- [`CHANGELOG.md`](CHANGELOG.md) — release history
- [`CITATION.cff`](CITATION.cff) and [`.zenodo.json`](.zenodo.json) — citation and archive metadata

## Proposed evaluation program

Priority comparisons include:

1. Static BTP versus dynamic candidate generation at matched computation budgets.
2. Dynamic unguided search versus fixed directional guidance.
3. Fixed guidance versus adaptive, feedback-updated directional fields.
4. Generate-then-score versus genuinely coupled generation–selection control.
5. Independent evidence versus correlated evidence with dependence-aware scoring.
6. Single-agent search versus multi-agent hypothesis competition, including coordination overhead.
7. Self-modifying policies versus policies whose improvements generalize to held-out tasks.

Evaluation should report correctness, constraint violations, search cost, solution quality, coverage, uncertainty calibration, diversity, reproducibility, and sensitivity to misleading evidence. Where a claim is about capability improvement, use independent held-out tasks and appropriate statistical uncertainty.

## Research boundaries and responsible use

- **Feasible does not imply true.** A structurally consistent hypothesis still needs evidence.
- **Weak evidence does not justify hard rejection.** Directional scoring controls attention, not logical validity.
- **Dynamic search does not guarantee computational tractability.** Candidate spaces may remain exponential.
- **Self-modification does not establish RSI.** Improvements must be independently demonstrated.
- **Blockchain behavioral attribution is not real-world identity identification.** Case studies should use synthetic or appropriately authorized data, account for false positives, and avoid unsupported personal accusations.
- **Biomimetic analogies are functional hypotheses.** They do not imply that biological brains implement BTP.

No benchmark results, production runtime, general superiority, or AGI/ASI capability are asserted by this initial research release.

## Suggested reading sequence

For a quick introduction, read [`START-HERE.md`](START-HERE.md), then D-BTP-001, D-BTP-002, D-BTP-004, and D-BTP-006. For implementation-oriented work, proceed through SPEC-001 to SPEC-004 before developing a runtime. For empirical research, begin with [`TESTABLE-HYPOTHESES.md`](TESTABLE-HYPOTHESES.md) and [`VALIDATION-ROADMAP.md`](VALIDATION-ROADMAP.md).

## Citation, license, and archival status

The project is intended for open research under **Apache License 2.0**. Citation metadata is provided in `CITATION.cff`; Zenodo metadata is provided in `.zenodo.json`. **Do not insert a DOI until one has been assigned.** The release tag should be `v1.0.0`, and the metadata title, authorship, repository URL, release date, and version should be checked for consistency before publication.

## Pre-release checklist

- [ ] Confirm all 18 Markdown papers are present at the paths listed above.
- [ ] Confirm eight separate figure files exist and are legible; inspect embedded figure links.
- [ ] Check all README, navigation, and cross-document relative links.
- [ ] Validate `CITATION.cff` and `.zenodo.json` syntax and metadata consistency.
- [ ] Confirm `LICENSE` contains the intended Apache-2.0 license text.
- [ ] Ensure statements about results remain explicitly prospective where untested.
- [ ] Verify the GitHub repository URL and public visibility.
- [ ] Create the immutable `v1.0.0` tag and GitHub Release after final review.
- [ ] Confirm Zenodo archival integration and assigned DOI before adding DOI links.

---

**Release perspective:** D-BTP v1.0.0 is a research foundation for studying how dynamic structural generation, directional search control, constraint validation, weak evidence, and structural relay might work together. Its purpose is to make these mechanisms explicit, inspectable, and testable—and to invite further independent validation and collective learning.
