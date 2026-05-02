# Source notes: developing Human Connectome Project (Makropoulos 2018)

> Paywalled at NeuroImage / Elsevier. PMC PDF not directly accessible at retrieval. Notes below distilled from the abstract, the dHCP release notes (https://biomedia.github.io/dHCP-release-notes/), and downstream release papers.

## Citation

Makropoulos A, Robinson EC, Schuh A, Wright R, Fitzgibbon S, Bozek J, Counsell SJ, Steinweg J, Vecchiato K, Passerat-Palmbach J, Lenz G, Mortazavi F, Tenev V, Duff E, Bastiani M, Cordero-Grande L, Hughes E, Tusor N, Tournier JD, Hutter J, Price AN, Murgasova M, Kelly C, Rutherford MA, Smith S, Edwards AD, Hajnal JV, Jenkinson M, Rueckert D. **The developing human connectome project: A minimal processing pipeline for neonatal cortical surface reconstruction.** *NeuroImage* 173, 88 to 112 (2018). DOI: 10.1016/j.neuroimage.2018.05.064.

## Cohort

- More than 1,500 neonates.
- Age range: 23 to 43 weeks post-menstrual age (PMA).
- Term and pre-term subsamples.
- Behavioural follow-up at 18 months: Bayley Scales of Infant and Toddler Development, language and motor assessments.

## Acquisition

- 3 Tesla Philips Achieva with custom 32-channel infant head coil.
- T1-weighted (T1w) and T2-weighted (T2w) anatomical at 0.5-mm isotropic.
- Multi-shell diffusion (b = 400 / 1000 / 2600).
- Resting-state functional Magnetic Resonance Imaging (fMRI) (15 minutes per session).

## Outputs

- Brain Imaging Data Structure (BIDS)-compliant deposit via Imperial College / King's College London.
- Pre-processed surface reconstruction via dHCP custom pipeline (Makropoulos 2018).
- Connectivity matrices, parcellations.

## Access conditions

- Data Use Agreement required.
- Pseudo-anonymized identifiers; no neonatal images redistributable.

## AGI annotation hooks

- Resting-state has no events; AGI annotation surface is essentially zero for the imaging side.
- Behavioural follow-up at 18 months can be cross-walked into a participants.tsv-style sidecar.
- Limited applicability to AGI's stimulus-annotation focus; included as a hybrid baseline reference.

## Cross-references

- `hcp-task/`: adult counterpart.
- `abcd-task/`: paediatric counterpart.
