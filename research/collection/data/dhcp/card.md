---
slug: dhcp
type: dataset
strand: data
year: 2018
authors: [Makropoulos, Robinson, Schuh, Wright, Fitzgibbon, Bozek, Counsell, Steinweg, Vecchiato, Passerat-Palmbach, Lenz, Mortazavi, Tenev, Duff, Bastiani, Cordero-Grande, Hughes, Tusor, Tournier, Hutter, Price, Murgasova, Kelly, Rutherford, Smith, Edwards, Hajnal, Jenkinson, Rueckert]
venue: NeuroImage
doi: 10.1016/j.neuroimage.2018.05.064
url: https://biomedia.github.io/dHCP-release-notes/
license: data-use-agreement (Imperial College / King's College London); paper publisher
modalities: [fmri, mri-anat, dti, behavior]
tags: [hybrid, neonates, resting-state, structural, n>1500, ages-23-43-weeks-pma, developmental]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

The developing Human Connectome Project (dHCP): more than 1,500 neonates (23 to 43 weeks post-menstrual age) with structural / diffusion / resting-state functional Magnetic Resonance Imaging (fMRI). The largest open neonatal connectome dataset.

## Summary

Makropoulos et al. (2018) describe the dHCP imaging pipeline; subsequent release papers (Edwards et al. 2022 NeuroImage) describe the full dataset. dHCP collected 3 Tesla magnetic resonance imaging on more than 1,500 term and pre-term neonates aged 23 to 43 weeks post-menstrual age (PMA), using a custom infant head coil and motion-tolerant sequences. The protocol covers high-resolution T1-weighted (T1w) and T2-weighted (T2w) anatomical MRI, multi-shell diffusion, and resting-state fMRI. Stimulus-driven task fMRI is minimal in the released cohort; the dataset's primary value is the resting-state connectivity and structural baselines for typically developing brain at the neonatal stage.

## Relevance to Annotation Garden Initiative (AGI)

dHCP is the resting-state developmental anchor for AGI's hybrid category. Although its task content is minimal (almost entirely resting state), the dataset's behavioural follow-up (cognitive assessments at age 18 months) and the broader UK Biobank-style integration make it a relevant comparator for cognitive-task developmental data. AGI's annotation hooks are limited (resting state has no events) but cross-walking to behavioural follow-up is valuable.

## Notable details

- N > 1,500 neonates (target 1,500 at recruitment; actual deposit slightly larger).
- Age: 23 to 43 weeks post-menstrual age.
- Term and pre-term cohorts.
- Custom 3 Tesla Philips Achieva with infant-tailored 32-channel head coil.
- Resting-state fMRI (15 minutes per session); multi-shell diffusion; T1w, T2w.
- Behavioural follow-up at 18 months (Bayley Scales, language assessments).
- Deposit via Imperial College + ELIXIR; DUA required.
- License: paper publisher (Elsevier); data DUA.

## Open questions / limitations

- Almost no naturalistic stimulus or task content (resting state only).
- DUA gating limits casual reuse.

## Citations

- Primary: `Makropoulos2018TheDH`.
- Related: HCP Development (Sommerville 2018); Baby Connectome Project (Howell 2019); BCP-Asia (Zhang 2024).
