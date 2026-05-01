# Source notes: Natural Sounds fMRI (Norman-Haignere 2015)

> Paywalled at Cell Press / Neuron. PMC version PMC4732138 exists but blocked by recaptcha at retrieval. Notes below are a structured summary based on the published abstract, the Norman-Haignere lab GitHub (https://github.com/snormanhaignere/natural-sound-encoding-2015), and the lit-review.

## Citation

Norman-Haignere S, Kanwisher NG, McDermott JH. **Distinct cortical pathways for music and speech revealed by hypothesis-free voxel decomposition.** *Neuron* 88, 1281 to 1296 (2015). DOI: 10.1016/j.neuron.2015.11.035. PubMed Central: PMC4732138.

## Cohort and acquisition

- More than 20 healthy adults (multiple cohorts).
- 3 Tesla Siemens scanner; 2-second TR.
- Sparse-imaging design to allow stimulus presentation in silence.

## Stimulus

- 165 two-second natural sound clips selected to span six categories (music, speech, mechanical, environmental, animal, other).
- Hand-curated; presented in randomized blocks.

## Annotations released (lab GitHub)

- Acoustic feature time series: spectro-temporal modulation power spectra, modulation transfer functions.
- Category labels (broad: music / speech / etc.).

## Outputs

- Voxel responses per sound; voxel decomposition components (the famous "music-selective" and "speech-selective" components).
- Cortical maps in fsaverage and native space.

## Access conditions

- Stimulus set distributed openly via McDermott / Norman-Haignere lab GitHub.
- Brain data: subject-level data has been distributed in subsequent papers; original Neuron release was group-level.

## AGI annotation hooks

- Fine-grained category tags (instrument family, speech accent, scene type) would extend the annotation density beyond the original six categories.
- HED `Sound/Music/Instrument/Piano` and HED `Sound/Speech/Language/English/Speaker-{ID}` patterns map naturally.
- Affective ratings (valence, arousal, pleasantness) would enable hedonic neural-encoding studies.

## Cross-references

- `narratives-pieman/`: long-form spoken language counterpart.
- `moth-radio-hour/`: long-form spoken language counterpart.
