---
slug: mriqc
type: tool
strand: tools
year: 2017
authors: [Esteban, Birman, Schaer, Koyejo, Poldrack, Gorgolewski]
venue: PLOS ONE
doi: 10.1371/journal.pone.0184661
url: https://mriqc.readthedocs.io
license: Apache-2.0
modalities: [fmri, mri]
tags: [MRI, quality-control, BIDS-App, T1, fMRI, classifier, multi-site]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

MRI Quality Control (MRIQC) extracts a battery of image-quality metrics from anatomical and functional Magnetic Resonance Imaging (MRI) data, fits a binary accept/exclude classifier, and produces per-subject reports as a Brain Imaging Data Structure (BIDS) App.

## Summary

MRIQC computes no-reference image quality metrics (signal-to-noise ratio, contrast-to-noise ratio, foreground-to-background energy ratio, entropy focus criterion, ghost-to-signal ratio, and others) and aggregates them into per-subject Hyper Text Markup Language (HTML) reports for visual inspection. The 2017 paper trains a random-forest classifier on a 17-site, N=1102 dataset and evaluates leave-one-site-out generalization, reporting 76 percent accuracy on unseen sites. MRIQC runs locally as a containerized BIDS App and was historically also offered as a hosted service through OpenNeuro. Outputs are designed to be reviewed alongside fMRIPrep derivatives during quality assurance.

## Relevance to AGI

For AGI's fMRI-anchored datasets, especially Natural Scenes Dataset (NSD) and StudyForrest, MRIQC is the standard pre-flight check that ensures the response side of the stimulus-response pair is trustworthy. AGI does not run MRIQC directly, but AGI repositories that ship aligned fMRI derivatives should reference MRIQC reports as part of the provenance bundle. The BIDS-App execution model also illustrates the pattern AGI's own annotation tools should follow: mount a BIDS dataset, write outputs into derivatives/, and emit an HTML report.

## Notable details

- BIDS-App container (Docker, Singularity, Apptainer) executes against any BIDS-compliant dataset.
- Per-subject HTML report with embedded mosaic views.
- Classifier trained on Autism Brain Imaging Data Exchange (ABIDE) plus OpenfMRI data.
- 76 percent leave-one-site-out generalization accuracy.
- Group-level reports support cross-site distribution comparisons.

## Open questions / limitations

- Generalization to unseen sites tops out around 76 percent, indicating residual site effects.
- Some artifacts evade the chosen feature set entirely.
- No native quality control for diffusion or arterial spin labeling.
- Classifier requires retraining as scanner technology evolves.
- Hosted online service has lower availability since 2023; local execution is the recommended path.

## Citations

Primary: `esteban2017mriqc`. Related:
- `esteban2019fmriprep`, companion preprocessing tool.
- `gorgolewski2016bids`, input data standard.
- `markiewicz2021openneuro`, archive that surfaces MRIQC reports.
- `prince2022glmsingle`, downstream analysis that benefits from QC-filtered inputs.
- `nichols2017cobidas`, community best-practice document that mandates QC reporting.
