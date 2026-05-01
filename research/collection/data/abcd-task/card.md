---
slug: abcd-task
type: dataset
strand: data
year: 2018
authors: [Casey, Cannonier, Conley, Cohen, Barch, Heitzeg, Soules, Teslovich, Dellarco, Garavan, Orr, Wager, Banich, Speer, Sutherland, Riedel, Dick, Bjork, Thomas, Chaarani, Mejia, Hagler, Daly Cornejo, Sicat, Harms, Dosenbach, Rosenberg, Earl, Bartsch, Watts, Polimeni, Kuperman, Fair, Dale]
venue: Developmental Cognitive Neuroscience
doi: 10.1016/j.dcn.2018.03.001
url: https://abcdstudy.org/
license: data-use-agreement (NIMH Data Archive); paper publisher
modalities: [fmri-3t, mri-anat, dti, behavior, phenotyping]
tags: [cognitive-task, developmental, large-cohort, monetary-incentive-delay, n-back, stop-signal, n=11800, ages-9-10]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

The Adolescent Brain Cognitive Development (ABCD) study: 11,800 children aged 9 to 10 with paired structural / diffusion / resting / task functional Magnetic Resonance Imaging (fMRI), longitudinal annual follow-up, and deep phenotyping. The largest paediatric neuroimaging study in history.

## Summary

Casey et al. (2018) describe the ABCD imaging protocol: 11,800 children enrolled at age 9 to 10 across 21 US sites, scanned on harmonized 3 Tesla protocols (Siemens Prisma, GE 750, Philips Achieva). The task fMRI battery includes Monetary Incentive Delay (MID), Emotional N-back, and Stop-Signal Task (SST). Annual follow-up imaging continues through age 19 to 20. The dataset includes structural T1w / T2w MRI, diffusion-weighted imaging (DWI) at multiple b-values, resting-state fMRI, and full behavioural / clinical / environmental / genetic phenotyping. ABCD is the most ambitious developmental neuroimaging effort ever undertaken.

## Relevance to Annotation Garden Initiative (AGI)

ABCD is the developmental anchor at the cognitive-task end of the AGI spectrum. The three task fMRI paradigms have well-defined event structures (button presses, stimulus onsets, feedback events) that map cleanly onto Hierarchical Event Descriptor (HED) Generation 3 templates. AGI hosting of canonical HED sidecars for ABCD's MID / N-back / SST tasks would be an immediate community contribution: ABCD's existing events.tsv files have inconsistent formats across sites and waves, and HED tagging is currently absent.

## Notable details

- N = 11,800 enrolled at baseline (age 9 to 10).
- Three task fMRI paradigms: Monetary Incentive Delay, Emotional N-back, Stop-Signal Task.
- Multi-site harmonized 3 Tesla acquisition (21 sites).
- Annual follow-up imaging waves (Year 2, 4, 6, 8 mid-adolescence).
- Deep phenotyping: cognition, mental health, environment, genetics.
- Access via DUA at NIMH Data Archive (NDA).

## Open questions / limitations

- Access controlled (DUA required for raw imaging; aggregate summary statistics openly).
- Site-to-site harmonization remains a methodological challenge.
- Paper paywalled.

## Citations

- Primary: `Casey2018TheAB`.
- Related: HCP Development (Sommerville 2018); HBN-MRI (`hbn-mri/`); IMAGEN (Schumann 2010).
