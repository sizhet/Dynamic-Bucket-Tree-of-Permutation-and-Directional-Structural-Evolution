# Changelog

All notable changes to **D-BTP — Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution** are documented here.

This research repository uses a versioned publication history. Version numbers identify the state of the published research materials; they do **not** imply that a production-ready implementation or empirically validated capability exists.

The format follows the principles of [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), with research-specific notes. The project intends to use semantic-style release tags (for example, `v1.0.0`) for archival clarity, without asserting API compatibility guarantees until a reference implementation and conformance suite are available.

## [Unreleased]

### Planned

- Independently export and verify the eight figures under `figures/` (the initial artwork was produced as a composite sheet; individual PNG assets require verification).
- Complete and cross-check publication metadata (`CITATION.cff`, `.zenodo.json`), release notes, and ResearchGate materials.
- Audit internal links, figure captions, terminology, specification cross-references, and repository paths.
- Define executable conformance fixtures and reproducible benchmark datasets for SPEC-001 through SPEC-004.
- Evaluate the core research hypotheses against static BTP, unguided dynamic search, fixed directional guidance, and adaptive guidance under matched computational budgets.

## [1.0.0] — 2026-11-03 (research manuscript baseline; release pending)

### Added — Research foundations

- `docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md` — motivates the generalization from structural similarity to hypothesis search.
- `docs/foundations/D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md` — defines evolving Bucket state and state-dependent candidate generation.
- `docs/foundations/D-BTP-003-Constraint-Guided-Structural-Composition.md` — develops composition, hard/soft constraints, propagation, and sound pruning.
- `docs/foundations/D-BTP-004-Directional-Fields-for-Generation-and-Selection.md` — introduces coupled generative and selective directional guidance.
- `docs/foundations/D-BTP-005-Weak-Evidence-and-Directional-Exploration.md` — separates evidential support from exploratory utility.
- `docs/foundations/D-BTP-006-Coupled-Generation-Selection-and-Feedback.md` — integrates generation, selection, and feedback into a dynamic control loop.
- `docs/foundations/D-BTP-007-Multi-Agent-RSI-and-Collective-Structural-Learning.md` — examines multi-agent competition, structural relay, and controlled improvement.
- `docs/foundations/D-BTP-008-Open-Ended-Structural-Evolution-and-Intelligence.md` — examines representation, operator, and search-capability growth and their limits.

### Added — Specifications

- `docs/specifications/SPEC-001-Dynamic-Bucket-State-Contract.md` — state, ledger, provenance, lifecycle, and conformance requirements.
- `docs/specifications/SPEC-002-Candidate-Generation-and-Constraint-Plugins.md` — candidate-generation and constraint-plugin interfaces and behavior.
- `docs/specifications/SPEC-003-Directional-Scoring-and-Search-Control.md` — scoring, resource allocation, field adaptation, and search-control semantics.
- `docs/specifications/SPEC-004-Evidence-Relay-and-Learning-Lifecycle.md` — evidence provenance, structural hypothesis exchange, learning, and governance.

### Added — Cases

- `docs/cases/CASE-001-Blockchain-Actor-Attribution.md` — a hypothesis-driven study of latent behavioral actors in blockchain data; explicitly distinguishes behavioral inference from real-world identity.
- `docs/cases/CASE-002-Dynamic-Starmap-Similarity.md` — revisits the original BTP structural-matching setting with dynamic candidate generation.
- `docs/cases/CASE-003-Multi-Agent-Hypothesis-Competition.md` — explores competing hypotheses, counterevidence, and relay.

### Added — Extensions

- `docs/extensions/EXT-001-Biomimetic-Directional-Intelligence.md` — functional analogies with biological exploration, without claiming neural implementation equivalence.
- `docs/extensions/EXT-002-Recursive-Directional-Field-Evolution.md` — treats directional fields as versioned objects of search and validated adaptation.
- `docs/extensions/EXT-003-Open-Ended-BTP-and-Structural-Relay.md` — examines hypothesis, representation, operator, and relay growth frontiers.

### Added — Repository guidance and research agenda

- `README.md` — project scope, architecture, and research positioning.
- `START-HERE.md` — suggested reading routes.
- `CONTENTS.md` — document inventory and cross-reference map.
- `GLOSSARY.md` — terminology, symbols, and conceptual boundaries.
- `FIGURE-INDEX.md` — figure inventory, captions, and intended placements.
- `FUTURE-DIRECTIONS.md` — forward research agenda.
- `OPEN-QUESTIONS.md` — unresolved research questions.
- `TESTABLE-HYPOTHESES.md` — falsifiable hypotheses, baselines, and evaluation ideas.
- `VALIDATION-ROADMAP.md` — staged conformance and empirical validation plan.
- `CHANGELOG.md` — version history and publication-status distinctions.

### Proposed visual assets

The figure plan specifies the following **target filenames**. Listing them here does not assert that all eight independent, publication-ready PNGs already exist:

1. `figures/Fig-001-D-BTP-Grand-Architecture.png`
2. `figures/Fig-002-From-Static-to-Dynamic-BTP.png`
3. `figures/Fig-003-Dynamic-Bucket-State-and-Candidate-Generation.png`
4. `figures/Fig-004-Constraint-Guided-Structural-Hypothesis-Search.png`
5. `figures/Fig-005-Directional-Generation-and-Selection-Coupling.png`
6. `figures/Fig-006-Weak-Evidence-and-Multi-Directional-Scoring.png`
7. `figures/Fig-007-Blockchain-Actor-Attribution-BTP.png`
8. `figures/Fig-008-Recursive-Structural-Evolution-and-Collective-Learning.png`

### Research principles established

- Dynamic candidate generation depends on evolving Bucket state rather than requiring a fixed, exhaustive initial pair list.
- Hard feasibility constraints are distinguished from soft scores, uncertain evidence, and directional heuristics.
- Directional fields can jointly influence generation, selection, and resource allocation, while feedback can update the fields.
- Weak evidence can have exploratory utility without constituting proof; counterevidence and provenance are first-class concerns.
- Structural Relay enables exchange and reuse, but receiving a hypothesis does not validate it.
- Search adaptation, collective learning, self-modification, and *validated* recursive self-improvement are distinct claims.
- Computational efficiency, completeness, generalization, and open-ended growth remain conditional research questions, not established guarantees.

### Validation status

- **Research design and documentation:** drafted.
- **Formal specification conformance:** proposed; no executed test results claimed.
- **Reference runtime:** not established by this manuscript release.
- **Benchmark superiority:** not established.
- **Cross-domain transfer or validated RSI:** not established.

## Release and archival notes

- **Planned initial public release:** `v1.0.0`, after repository and publication checks.
- **License intention:** Apache-2.0; confirm that the repository includes the actual `LICENSE` file before release.
- **DOI:** pending assignment; do not insert a placeholder DOI into citations as if it were issued.
- **Publication date:** the date above records the research manuscript baseline, not a verified GitHub Release or Zenodo publication event. Replace or annotate it with the actual release date if different.
- **Attribution and citation:** follow the final `CITATION.cff` and archival record once verified.

## Maintenance conventions

1. Add new work to **Unreleased** until an immutable release is prepared.
2. Record substantial changes to research claims, contracts, benchmark methodology, or figures under the appropriate category: **Added**, **Changed**, **Fixed**, **Deprecated**, **Removed**, or **Security**.
3. Keep a distinction between *proposed*, *implemented*, *tested*, and *independently validated* capabilities.
4. Update `CONTENTS.md`, `GLOSSARY.md`, `FIGURE-INDEX.md`, and cross-references whenever filenames, interfaces, or terminology change.
5. For changes affecting normative specifications, identify compatibility implications and update conformance tests before making runtime claims.
6. Preserve archived release assets and publish corrections in subsequent versions rather than silently altering the historical record.

---

*D-BTP is a research framework. This changelog tracks the evolution of its published design, not a claim of demonstrated general intelligence or deployment-ready actor attribution.*
