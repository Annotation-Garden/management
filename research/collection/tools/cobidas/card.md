---
slug: cobidas
type: standard
strand: tools
year: 2017
authors: [Nichols, Das, Eickhoff, Evans, Glatard, Hanke, Kriegeskorte, Milham, Poldrack, Poline, Proal, Thirion, "Van Essen", White, Yeo]
venue: Nature Neuroscience
doi: 10.1038/nn.4500
url: https://www.nature.com/articles/nn.4500
license: publisher-paywall (paper); checklist is CC-BY
modalities: [fmri, mri]
tags: [COBIDAS, OHBM, best-practices, reporting, transparency, reproducibility, checklist]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

The Committee on Best Practices in Data Analysis and Sharing (COBIDAS) report, published in 2017 by the Organization for Human Brain Mapping (OHBM), is a community-endorsed checklist of acquisition, analysis, and sharing practices that functional Magnetic Resonance Imaging (fMRI) studies should report.

## Summary

COBIDAS itemizes what every fMRI paper should disclose: scanner and sequence parameters, subject selection and exclusions, preprocessing pipeline including motion-correction strategy, model specification, multiple-comparison correction, and data and code sharing. The 2017 Nature Neuroscience summary highlights the most important categories; a longer technical report and a maintained checklist on the Open Science Framework (OSF) provide the operational form. COBIDAS-MEEG, a sibling document for Magnetoencephalography (MEG) and Electroencephalography (EEG), extends the same approach. The checklist is widely cited by journals and funders as a baseline rigor expectation.

## Relevance to AGI

COBIDAS is a procedural standard rather than a data format, but it is directly relevant to AGI's quality story. AGI annotations must themselves report enough about how they were produced (annotator identity, model version, prompt, multi-agent path, reliability metrics) for downstream studies that use those annotations to satisfy COBIDAS-style transparency requirements. AGI's events.json sidecars, annotation provenance files, and pull-request review templates should align with COBIDAS-MEEG so that an AGI-enriched dataset is publishable with no additional reporting work.

## Notable details

- Published as a Nature Neuroscience commentary; companion technical report and OSF checklist.
- Categories: acquisition, subjects, preprocessing, analysis, sharing.
- Sister document COBIDAS-MEEG covers MEG and EEG.
- Adopted by NeuroImage, Imaging Neuroscience, OHBM 2018+.
- Updated periodically by the OHBM Open Science Special Interest Group.

## Open questions / limitations

- The checklist is long and adoption depends on author goodwill; few journals enforce it.
- Items tied to specific software versions become outdated quickly.
- Annotation provenance is not yet a first-class category; AGI work could extend it.
- Reproducibility checking is manual; no automated COBIDAS validator exists.
- Coverage of newer modalities (functional Near-Infrared Spectroscopy, Optically Pumped Magnetometers) lags.

## Citations

Primary: `nichols2017cobidas`. Related:
- `wilkinson2016fair` — broader principles COBIDAS instantiates.
- `gorgolewski2016bids` — data structure that supports several COBIDAS items.
- `esteban2019fmriprep` — pipeline whose use simplifies COBIDAS reporting.
- `markiewicz2021openneuro` — sharing infrastructure aligned with COBIDAS.
- `robbins2021hed` — annotation rigor complementary to COBIDAS.
