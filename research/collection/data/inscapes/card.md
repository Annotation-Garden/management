---
slug: inscapes
type: dataset
strand: data
year: 2015
authors: [Vanderwal, Kelly, Eilbott, Mayes, Castellanos]
venue: NeuroImage
doi: 10.1016/j.neuroimage.2015.07.069
url: https://www.headspacestudios.org/inscapes
license: paper publisher (Elsevier); video CC-BY-NC for research use
modalities: [fmri, behavior]
tags: [naturalistic-video, abstract-animation, passive-viewing, low-arousal, head-motion-mitigation, developmental, mixed-ages]
agi_relevance: low
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

Inscapes is a 7-minute abstract animated video designed to maintain attention without inducing strong emotion or narrative load, used as a low-demand naturalistic alternative to resting state for paediatric and clinical functional Magnetic Resonance Imaging (fMRI).

## Summary

Vanderwal et al. (Yale Child Study Center / NYU / Head Space Studios) created Inscapes, a 7-minute high-quality animation of slowly evolving abstract shapes set to ambient music, as a controlled "passive viewing" naturalistic stimulus. Compared to feature films or cartoons, Inscapes minimizes social and narrative content, reducing variance from individual interpretation while still suppressing head motion and increasing compliance relative to resting state. The original NeuroImage 2015 paper validated Inscapes against resting state and Despicable Me viewing in 36 healthy adults, showing comparable connectivity reliability with markedly reduced motion. The stimulus is now widely used in HBN, ABCD-like paediatric protocols, and clinical research.

## Relevance to Annotation Garden Initiative (AGI)

Inscapes occupies a unique position on the naturalistic-to-controlled spectrum: ecologically richer than blank fixation but with intentionally minimal semantic content. AGI annotation layers for Inscapes are necessarily about low-level audiovisual features (scene shapes, color shifts, music phrase boundaries), which makes it a useful template for "minimal-annotation" Garden contributions and for benchmarking how much annotation density actually drives encoding-model gains.

## Notable details

- 7-minute video; rendered animation of abstract shapes with ambient music.
- Validation cohort: 36 healthy adults; cross-validated in HBN paediatric data.
- Distributed (with usage agreement) via headspacestudios.org.
- Annotations available: low-level audiovisual features (luminance, motion energy), phrase boundaries.

## Open questions / limitations

- Paper paywalled (Elsevier) at retrieval.
- Stimulus is provided via Vanderwal lab; not open-source.
- Annotation density is intentionally low.

## Citations

- Primary: `Vanderwal2015InscapesAM`.
- Related: Movies in the Magnet (Vanderwal 2019); HBN-MRI (Alexander 2017).
