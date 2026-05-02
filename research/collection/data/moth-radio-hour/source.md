# Source notes: Moth Radio Hour fMRI (Huth 2016)

> Paywalled at Nature. PMC version PMC5102795 exists but blocked by recaptcha at retrieval. Notes below distilled from the published abstract, the Gallant Lab GitHub (https://github.com/HuthLab/speechmodeltutorial), and the lit-review.

## Citation

Huth AG, de Heer WA, Griffiths TL, Theunissen FE, Gallant JL. **Natural speech reveals the semantic maps that tile human cerebral cortex.** *Nature* 532, 453 to 458 (2016). DOI: 10.1038/nature17637. PubMed Central: PMC5102795.

## Cohort and acquisition

- 7 healthy adults.
- 3 Tesla Siemens Tim Trio.
- Whole-brain coverage; 2.0-second repetition time (TR).
- Cortical surface reconstruction via FreeSurfer with manual edits.

## Stimulus

- 10 to 12 autobiographical stories from "The Moth Radio Hour" podcast.
- About 2 hours of audio per subject; presented across multiple sessions.

## Annotations released (Gallant Lab repo)

- Time-aligned word-by-word transcripts.
- Phoneme alignment (Penn Forced Aligner).
- Acoustic features: spectral envelope, broadband envelope.
- Word2Vec / GloVe semantic embeddings per word.
- Pre-computed encoding model regression weights for each subject.

## Outputs

- BIDS-compliant fMRI data (deposited in Berkeley OSF / Gallant lab repository).
- Interactive cortical "semantic atlas" viewer at gallantlab.org/huth2016.

## Access conditions

- Brain data: open via Berkeley deposit and via subsequent collected releases.
- Audio: The Moth Radio Hour holds copyright; researchers must obtain audio independently or use open-licensed equivalents.

## AGI annotation hooks

- Phoneme / word alignment is the gold-standard layer.
- HED-Lang sidecar mappings (lemma, part of speech, syntactic role) would be a strong Garden contribution.
- Continuous semantic embedding time series; AGI can host alternative embeddings (BERT, GPT, Llama) as parallel layers.

## Cross-references

- `narratives-pieman/`: open audio narrative counterpart.
- `little-prince-fmri/`: multilingual narrative counterpart.
