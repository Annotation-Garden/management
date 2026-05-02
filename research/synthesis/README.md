# Phase 2 Synthesis

Phase 2 of the Annotation Garden Initiative (AGI) research foundation epic ([issue #3](https://github.com/Annotation-Garden/management/issues/3)) cross-references the [Phase 1 corpus](../collection/) into structured synthesis artifacts. No white-paper drafting or new direction documents live here, that is Phase 3.

Abbreviations used across all six docs: Brain Imaging Data Structure (BIDS), Hierarchical Event Descriptors (HED), Findable, Accessible, Interoperable, Reusable (FAIR). Each individual doc redefines these and any other abbreviations on their first use within that doc.

## Documents

- [`tool-ontology.md`](./tool-ontology.md), hierarchical map of the 33 tool, platform, and standard entries grouped into five layers, with per-node maturity, BIDS integration, HED integration, license, and AGI relevance.
- [`dataset-hierarchy.md`](./dataset-hierarchy.md), formal placement of all 36 dataset entries along the naturalistic to cognitive-task spectrum, with axes for stimulus type, modality coverage, annotation density, sample size, copyright, and AGI rollout phase.
- [`science-map.md`](./science-map.md), the 30 Strand C papers laid out across 7 methodological themes, each with representative work, methodological maturity, distilled open questions, and annotation-infrastructure dependencies.
- [`gap-analysis.md`](./gap-analysis.md), three-column comparison of ANNOTATE R01 coverage, the current AGI white paper coverage, and the uncovered terrain that defines AGI's distinctive scope. Names the concrete gaps that motivate Phase 3 deliverables.
- [`scope-diagram.md`](./scope-diagram.md), side-by-side AGI to ANNOTATE R01 dimensions and the explicit complementarity statement that should anchor Phase 3 framing.

## Phase 3 reading order

1. [`scope-diagram.md`](./scope-diagram.md), the framing piece. Establishes that AGI and ANNOTATE are complementary, not competing, and that AGI is community infrastructure rather than a research project.
2. [`gap-analysis.md`](./gap-analysis.md), the action piece. Names what AGI must cover that no one else does.
3. [`tool-ontology.md`](./tool-ontology.md), [`dataset-hierarchy.md`](./dataset-hierarchy.md), [`science-map.md`](./science-map.md), the inventories. Read in any order, depending on which Phase 3 deliverable is being drafted.

## Citation conventions

Every claim in these docs that depends on a specific tool, dataset, or paper cites the corresponding Phase 1 paper-card by relative path, e.g. [`../collection/data/nsd-fmri/card.md`](../collection/data/nsd-fmri/card.md). The card is the primary source. BibTeX keys, when needed inline, come from the strand `.bib` files at [`tools.bib`](../collection/tools/tools.bib), [`data.bib`](../collection/data/data.bib), and [`science.bib`](../collection/science/science.bib).

## Style

- Abbreviations defined on first use within each document.
- No em-dashes; commas or semicolons where appropriate.
- No emojis.
- Tables prefer machine-checkable categorical values (license SPDX-like strings, agi_relevance from card front-matter, BIDS / HED integration as native, partial, none, or none-yet).
