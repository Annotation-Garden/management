---
slug: neuroscout
type: platform
strand: tools
year: 2022
authors: ["de la Vega", Rocca, Blair, Markiewicz, Mentch, Kent, Herholz, Ghosh, Poldrack, Yarkoni]
venue: eLife
doi: 10.7554/eLife.79277
url: https://neuroscout.org
license: MIT (code); CC-BY (data)
modalities: [fmri, video, audio, image]
tags: [Neuroscout, fMRI, naturalistic, Pliers, BIDS, encoding-model, reproducibility, feature-extraction]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Neuroscout is an end-to-end web platform for analyzing naturalistic functional Magnetic Resonance Imaging (fMRI) datasets, automatically annotating stimuli with machine-learning-derived predictors (via Pliers), letting researchers build statistical models in a browser, and executing them reproducibly on Brain Imaging Data Structure (BIDS) datasets.

## Summary

Neuroscout addresses two pain points in naturalistic fMRI: the labor of annotating stimulus features, and the variability of analysis workflows. The platform pre-annotates dozens of public naturalistic fMRI datasets with hundreds of features extracted by Pliers (visual saliency, faces, scene categories, speech envelope, sentiment, language-model embeddings), stores them in a shared database, and exposes an analysis builder that lets users assemble General Linear Model (GLM) designs from those features. Once a model is specified, the Neuroscout execution engine runs it through BIDS-compatible pipelines (fmriprep + FitLins) on cloud infrastructure, returning fully reproducible results with provenance bundles. The 2022 eLife paper validates the approach via meta-analytic case studies.

## Relevance to AGI

Neuroscout is the closest existing precedent for what AGI aims to be on the analysis side: a community resource that makes annotations of naturalistic stimuli first-class objects. The crucial difference is scope. Neuroscout focuses on fMRI analysis with Pliers as the only annotator. AGI generalizes to multi-modal annotations (HED, manual ratings, multi-agent VLM outputs) and across response modalities (EEG, MEG, behavior). Neuroscout's Pliers feature graph and BIDS execution engine are concrete templates AGI should reuse rather than reinvent, and a Neuroscout-AGI bridge (AGI annotations consumed as Neuroscout predictors) is the obvious near-term collaboration target.

## Notable details

- Pre-annotates dozens of naturalistic fMRI datasets with Pliers features.
- Browser-based analysis builder mirrors BIDS-StatsModels specification.
- Execution engine: fmriprep plus FitLins on cloud or local Docker.
- Provenance bundles capture model definition, code version, container hashes.
- Validated through meta-analytic case studies replicating known effects.

## Open questions / limitations

- Limited to fMRI; no native support for EEG/MEG response models.
- Dependency on Pliers means coverage of features is whatever Pliers wrappers exist.
- Annotations are treated as observational predictors; HED tags are not yet first-class.
- User-uploaded datasets must be already BIDS-compliant and on OpenNeuro.
- Scaling to interactive video annotation is not in scope; works at the predictor level only.

## Citations

Primary: `delavega2022neuroscout`. Related:
- `mcnamara2017pliers` — feature-extraction backbone.
- `gorgolewski2016bids` — input data standard.
- `markiewicz2021openneuro` — primary archive feeding Neuroscout.
- `esteban2019fmriprep` — preprocessing pipeline used in execution.
- `prince2022glmsingle` — alternative single-trial estimator that complements Neuroscout's GLM.
