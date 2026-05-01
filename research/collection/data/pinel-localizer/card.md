---
slug: pinel-localizer
type: paper
strand: data
year: 2007
authors: [Pinel, Thirion, Mériaux, Jobert, Serres, Le Bihan, Poline, Dehaene]
venue: BMC Neuroscience
doi: 10.1186/1471-2202-8-91
url: https://www.brainvoyager.com/downloads/pdf_doc/Pinel_BMC_Neuroscience_2007.pdf
license: paper CC-BY 2.0; stimulus materials openly released
modalities: [fmri, behavior]
tags: [single-stimulus-benchmark, multi-task-localizer, calculation, language, motor, visual, individual-functional-rois, adults, n=81]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Pinel multi-task localizer: a 5-minute functional Magnetic Resonance Imaging (fMRI) paradigm bundling 10 mini-tasks (visual, auditory, motor, calculation, language) into a single short scan, used as a canonical "fast localizer battery" across hundreds of cohorts.

## Summary

Pinel and colleagues (NeuroSpin / SHFJ-Orsay) introduced a compact multi-task localizer that probes 10 elementary cognitive processes in a single 5-minute scan: visual horizontal vs vertical checkerboard, left vs right button press, auditory sentence presentation, visual sentence reading, calculation (visual / auditory), and so on. The paradigm is widely used as a baseline cross-cohort comparator (e.g., the Localizer dataset on OpenNeuro is a 700-subject application of this protocol, Papadopoulos Orfanos 2017). Stimulus materials and analysis code are openly released in BIDS form and via the IBC (Individual Brain Charting) project.

## Relevance to Annotation Garden Initiative (AGI)

Pinel localizer is a near-perfect "single-stimulus benchmark" for AGI: short, well-defined event types, openly distributed materials, and applied to thousands of subjects. Garden contribution opportunities: a clean, version-controlled HED Generation 3 sidecar JSON that captures all 10 sub-task event types; cross-walks to HCP and ABCD task batteries; multilingual stimulus variants.

## Notable details

- 5-minute paradigm with 10 sub-task types.
- 81 subjects in original validation; thousands in subsequent applications (Localizer dataset, IBC project).
- Brain Imaging Data Structure (BIDS) deposit on OpenNeuro: ds000114 (Pinel localizer subset).
- License: paper CC-BY 2.0; stimulus materials openly released.

## Open questions / limitations

- Mini-tasks are short (4 to 10 trials each); statistical power is intentionally limited per-task.
- French original; English translations community-curated.

## Citations

- Primary: `Pinel2007FastRO`.
- Related: Fedorenko language localizer (`fedorenko-language-localizer/`); HCP Task (`hcp-task/`); Individual Brain Charting (Pinel 2017, IBC project).
