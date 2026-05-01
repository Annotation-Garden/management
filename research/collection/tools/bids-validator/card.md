---
slug: bids-validator
type: tool
strand: tools
year: 2024
authors: [BIDS Maintainers]
venue: BIDS community open-source project
doi: null
url: https://github.com/bids-standard/bids-validator
license: MIT
modalities: [fmri, mri, eeg, meg, ieeg, pet, behavior]
tags: [BIDS, validator, CLI, web, schema, JavaScript, Python, CI]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-applicable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

The BIDS-Validator is the reference implementation that checks whether a dataset conforms to the Brain Imaging Data Structure (BIDS) specification, available as a Node.js command-line tool, an in-browser web validator, and a Python wrapper, all driven by the canonical BIDS schema.

## Summary

The validator parses a BIDS dataset and reports errors and warnings against the BIDS schema, including modality extensions for Magnetoencephalography (MEG), Electroencephalography (EEG), intracranial EEG (iEEG), Positron Emission Tomography (PET), Magnetic Resonance Spectroscopy (MRS), and Arterial Spin Labeling. It checks file naming, required and recommended sidecar JSON fields, and cross-file consistency such as events.tsv timing relative to scan duration. The output is structured JSON, which makes it straightforward to plug into Continuous Integration pipelines, repository hooks, BIDS-Apps, and dataset archives. OpenNeuro runs the validator on every upload; NEMAR uses it as part of dataset triage; many BIDS-Apps require validation as a pre-flight step.

## Relevance to AGI

AGI's per-stimulus repositories must be machine-validatable for any contributor to trust them. The BIDS-Validator is the obvious validator AGI should run in its Continuous Integration: every pull request that modifies events.tsv, dataset_description.json, or annotation sidecars triggers a validator run, and only passing pull requests can merge. AGI may also need a thin Stim-BIDS-aware extension to the validator to check stimulus-specific constraints (BEP044 cross-references, annotation-type folder names) without forking the core tool.

## Notable details

- Two implementations: JavaScript (bids-validator) and Python (bids-validator-deno).
- Browser version at https://bids-standard.github.io/bids-validator/ runs entirely client-side.
- Outputs structured JSON; integrates with GitHub Actions templates published by the BIDS community.
- HED-tag validation is available through plugin integration with hed-python.
- MIT license.

## Open questions / limitations

- Validator covers structural conformance, not semantic correctness of annotations.
- Stim-BIDS (BEP044) checks are not yet built in.
- Some modality extensions still have spotty coverage of optional fields.
- Performance on very large datasets (thousands of subjects) can be slow without parallelization.
- Browser version cannot validate datasets that exceed local filesystem access limits.

## Citations

Primary: `bidsvalidator2024`. Related:
- `gorgolewski2016bids` — specification the validator enforces.
- `markiewicz2021openneuro` — primary deployment site.
- `delorme2022nemar` — sister archive that runs the validator.
- `halchenko2021datalad` — distribution pattern that benefits from validator output.
- `bep044stimbids` — extension proposal that will need validator support.
