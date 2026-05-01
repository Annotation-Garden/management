---
slug: myconnectome
type: dataset
strand: data
year: 2015
authors: [Poldrack, Laumann, Koyejo, Gregory, Hover, Chen, Gorgolewski, Luci, Joo, Boyd, Hunicke-Smith, Simpson, Caven, Sochat, Shine, Gordon, Snyder, Adeyemo, Petersen, Glahn, Mckay, Curran, Bookheimer, Dapretto, Munoz, Buckner, Schweinhardt, Greenberg, Tatler, Barsalou, Marsh, Fair, Mumford]
venue: Nature Communications
doi: 10.1038/ncomms9885
url: http://myconnectome.org/
license: paper CC-BY 4.0; data CC-BY 4.0
modalities: [fmri-3t, mri-anat, dti, behavior, phenotyping, multi-omics]
tags: [cognitive-task, single-subject, deep-sampling, longitudinal, n=1, daily-scans, multi-omics]
agi_relevance: medium
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Single-subject (Russell Poldrack) deep-sampling study with 105 functional Magnetic Resonance Imaging (fMRI) sessions, daily behavioural and physiological tracking, and multi-omics measurements over 18 months. The proof-of-concept "individual N=1" paradigm.

## Summary

The MyConnectome project (Poldrack et al. 2015) is a one-subject longitudinal study where Russell Poldrack himself underwent 105 functional magnetic resonance imaging (fMRI) sessions plus daily behavioural / physiological / mood tracking and weekly biological sample collection over 18 months. Resting-state fMRI was paired with cognitive task scanning and a custom n-back battery on alternating sessions. The dataset has anchored debates about within-individual functional brain network reliability and is a frequent reference for "deep phenotyping of N=1" studies. The data are openly licensed and BIDS-compatible.

## Relevance to Annotation Garden Initiative (AGI)

MyConnectome is a unique data point at the cognitive-task end of the spectrum: deep-sampling but single-subject. It illustrates the upper-bound use of cognitive-task annotations to study within-subject network dynamics. AGI hosting of canonical HED-tagged events.tsv for the n-back and other task paradigms here is a small but high-value contribution for community reuse.

## Notable details

- N = 1 (Russell Poldrack).
- 105 fMRI sessions over 18 months, alternating between resting-state and task days.
- Paired multi-omics (gene expression, metabolomics, microbiome).
- Daily mood / sleep / physiological tracking.
- Open release on OpenfMRI / OpenNeuro and Stanford CRN.
- License: paper CC-BY 4.0; data CC-BY 4.0.

## Open questions / limitations

- N = 1: zero between-subject statistics; population inference impossible.
- Subject is a senior neuroscientist; not representative of general population.
- Some of the multi-omics layers are still under restricted release.

## Citations

- Primary: `Poldrack2015LongtermNA`.
- Related: midnight-scan-club Gordon 2017; courtois-neuromod (`courtois-neuromod/`); MyConnectome Plus.
