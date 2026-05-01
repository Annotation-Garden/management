# Source notes: HCP-D (Somerville 2018)

> Paywalled at NeuroImage / Elsevier. PMC PDF (PMC6132038) blocked by recaptcha at retrieval. Notes below distilled from the abstract, the HCP Lifespan landing page (https://www.humanconnectome.org/study/hcp-lifespan-development), and the lit-review.

## Citation

Somerville LH, Bookheimer SY, Buckner RL, Burgess GC, Curtiss SW, Dapretto M, Elam JS, Gaffrey MS, Harms MP, Hodge C, Kandala S, Kastman EK, Nichols TE, Schlaggar BL, Smith SM, Thomas KM, Yacoub E, Van Essen DC, Barch DM. **The Lifespan Human Connectome Project in Development: A large-scale study of brain connectivity development in 5 to 21 year olds.** *NeuroImage* 183, 456 to 468 (2018). DOI: 10.1016/j.neuroimage.2018.04.078. PubMed Central: PMC6132038.

## Cohort

- N ≈ 1,300 typically developing children and adolescents.
- Age range: 5 to 21.
- Recruited across four US sites: Boston Children's, UCLA, Washington University in St. Louis, University of Minnesota.

## Acquisition

- 3 Tesla Siemens Prisma (harmonized across sites).
- Anatomical: T1-weighted 0.8-mm, T2-weighted 0.8-mm.
- Diffusion: multi-shell (b = 1500 / 3000), 92 directions.
- Resting-state functional Magnetic Resonance Imaging (fMRI): 4 runs of 6.5 minutes each, TR = 0.8 s.
- Task fMRI: 4 paradigms (Emotion, Reward / Card Guessing, Inhibition / Stop Signal, Working Memory / n-back).

## Tasks

| Task | Description | Duration |
|------|-------------|----------|
| Emotion | Hariri faces / shapes | 5 minutes |
| Reward | Card Guessing | 6 minutes |
| Inhibition | Stop Signal | 6 minutes |
| Working Memory | n-back (with emotional and neutral stimuli) | 7 minutes |

## Behavioural and clinical

- NIH Toolbox cognitive and emotional batteries.
- Child Behavior Checklist (CBCL).
- Pubertal status, demographics, family history.

## Outputs

- Brain Imaging Data Structure (BIDS) deposit via Connectome Coordination Facility / db.humanconnectome.org.
- Pre-processed via the HCP Lifespan pipeline (extension of HCP Young Adult pipeline).

## Access conditions

- Open via Data Use Agreement.
- Restricted-access supplement for clinical and pubertal data.

## AGI annotation hooks

- HED Generation 3 sidecars per task, harmonized with HCP Young Adult and (where applicable) ABCD.
- Cross-cohort developmental annotation crosswalks.

## Cross-references

- `hcp-task/`: adult counterpart.
- `abcd-task/`: paediatric large-N counterpart.
- `cam-can/`: adult lifespan counterpart.
