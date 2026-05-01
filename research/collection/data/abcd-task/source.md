# Source notes: ABCD Task fMRI (Casey 2018)

> Paywalled at Developmental Cognitive Neuroscience / Elsevier. PMC equivalent (PMC5999559) blocked by recaptcha at retrieval. Notes below distilled from the abstract, the ABCD study landing page (https://abcdstudy.org/), and the lit-review.

## Citation

Casey BJ, Cannonier T, Conley MI, Cohen AO, Barch DM, Heitzeg MM, Soules ME, Teslovich T, Dellarco DV, Garavan H, Orr CA, Wager TD, Banich MT, Speer NK, Sutherland MT, Riedel MC, Dick AS, Bjork JM, Thomas KM, Chaarani B, Mejia MH, Hagler DJ Jr, Daly Cornejo M, Sicat CS, Harms MP, Dosenbach NUF, Rosenberg M, Earl E, Bartsch H, Watts R, Polimeni JR, Kuperman JM, Fair DA, Dale AM. **The Adolescent Brain Cognitive Development (ABCD) study: Imaging acquisition across 21 sites.** *Developmental Cognitive Neuroscience* 32, 43 to 54 (2018). DOI: 10.1016/j.dcn.2018.03.001. PubMed Central: PMC5999559.

## Cohort

- N = 11,800 children at baseline (target 11,500 met).
- Age range at enrolment: 9.0 to 10.9 years.
- 21 US data-collection sites; recruitment stratified for socioeconomic, racial / ethnic, and geographic diversity.

## Acquisition

- 3 Tesla Siemens Prisma, GE 750, or Philips Achieva, harmonized protocol.
- Anatomical: T1-weighted, T2-weighted at 1.0 mm isotropic.
- Diffusion: multi-shell (b = 500 / 1000 / 2000 / 3000), 96 directions.
- Resting-state functional Magnetic Resonance Imaging (fMRI) (4 runs, 5 minutes each).
- Task fMRI: 3 paradigms (Monetary Incentive Delay, Emotional N-back, Stop-Signal Task) at 0.8-second TR, 2.4-mm isotropic.

## Tasks

| Task | Description | Approximate duration |
|------|-------------|----------------------|
| Monetary Incentive Delay (MID) | reward / loss anticipation | 10 minutes |
| Emotional N-back | working memory with face stimuli | 10 minutes |
| Stop-Signal Task (SST) | response inhibition | 10 minutes |

## Annotations

- Trial events.tsv per task (BIDS-formatted in re-released versions).
- HED Generation 3 mapping is not curated; community gap.
- Behavioural performance: accuracy, reaction time, post-error slowing.

## Outputs

- BIDS-compliant deposit on the National Institute of Mental Health Data Archive (NDA).
- Pre-processed via the ABCD Data Analysis, Informatics and Resource Center (DAIRC) pipeline.

## Access conditions

- Data Use Agreement required (institutional approval + signed agreement).
- Aggregate summary statistics openly available via ABCD Reproducible Brain Charts and ABCD-BIDS.

## AGI annotation hooks

- HED Gen-3 sidecars per task (community gap).
- Cross-mapping to HCP / HCP-Development tasks (overlap on N-back; useful for cross-cohort meta-analysis).
- Stimulus-image annotation: Emotional N-back uses a defined image set (Tottenham NIMH-CHEFS); image-level annotations would propagate.

## Cross-references

- `hcp-task/`: adult counterpart.
- `hbn-mri/`: comparable paediatric naturalistic-stimulus counterpart.
- `cam-can/`: adult lifespan counterpart.
