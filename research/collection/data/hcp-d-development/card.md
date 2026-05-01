---
slug: hcp-d-development
type: dataset
strand: data
year: 2018
authors: [Somerville, Bookheimer, Buckner, Burgess, Curtiss, Dapretto, Elam, Gaffrey, Harms, Hodge, Kandala, Kastman, Nichols, Schlaggar, Smith, Thomas, Yacoub, Van Essen, Barch]
venue: NeuroImage
doi: 10.1016/j.neuroimage.2018.04.078
url: https://www.humanconnectome.org/study/hcp-lifespan-development
license: data-use-agreement (HCP / Connectome Coordination Facility); paper publisher
modalities: [fmri-3t, mri-anat, dti, behavior, phenotyping]
tags: [cognitive-task, hybrid, developmental, lifespan, reward, emotion, working-memory, n=1300, ages-5-21]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

The Human Connectome Project Development (HCP-D) extension: roughly 1,300 typically developing children and adolescents aged 5 to 21 with a harmonized HCP-style neuroimaging protocol covering structural / diffusion / resting / task functional Magnetic Resonance Imaging (fMRI) and a paediatric cognitive battery.

## Summary

Somerville et al. (2018) describe the HCP-D Lifespan extension: a deliberately developmental complement to the HCP Young Adult cohort, recruiting roughly 1,300 typically developing children and adolescents aged 5 to 21 across four US sites. The protocol mirrors HCP's anatomical, diffusion, and resting-state acquisitions while substituting age-appropriate task fMRI: Emotion (faces / shapes), Reward (Card Guessing), Inhibition (Stop Signal), and Working Memory (n-back). Behavioural and clinical phenotyping covers cognition, emotion regulation, social development, and pubertal stage. The dataset is the bridge between paediatric task fMRI (e.g., ABCD) and adult HCP, and it shares acquisition protocols closely enough to support cross-cohort harmonization.

## Relevance to Annotation Garden Initiative (AGI)

HCP-D is a cognitive-task developmental anchor that complements ABCD (more participants, less depth) and HCP Young Adult (adults). Its harmonized protocol and BIDS deposit make it an ideal comparator for AGI's HED-tagged cognitive-task sidecars: a single canonical mapping covers HCP, HCP-D, and most of HCP-A by extension. The dataset's emotion and reward tasks are particularly close to HBN's cognitive battery, enabling cross-cohort developmental analyses.

## Notable details

- N ≈ 1,300 typically developing youths, ages 5 to 21.
- Four data-collection sites: Boston Children's, UCLA, Washington University, University of Minnesota.
- Tasks: Emotion (Hariri), Reward (Card Guessing), Inhibition (Stop Signal), Working Memory (n-back).
- 3 Tesla Siemens Prisma; HCP-style 0.8-mm anatomical, 1.5-mm fMRI, multi-shell diffusion.
- Behavioural / clinical battery: NIH Toolbox, Child Behavior Checklist, pubertal status.
- BIDS deposit via Connectome Coordination Facility (CCF) and the LifespanData Archive.

## Open questions / limitations

- Cross-site harmonization is non-trivial despite protocol matching.
- Restricted access to clinical / pubertal data via DUA.
- Paper paywalled.

## Citations

- Primary: `Somerville2018TheLH`.
- Related: HCP Young Adult Task (`hcp-task/`); ABCD (`abcd-task/`); HCP-A (Bookheimer 2019).
