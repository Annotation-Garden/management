# Source notes: DEAP (Koelstra 2012)

> Paywalled at IEEE. Notes below distilled from the abstract, the dataset landing page (https://www.eecs.qmul.ac.uk/mmv/datasets/deap/), and the lit-review.

## Citation

Koelstra S, Mühl C, Soleymani M, Lee J-S, Yazdani A, Ebrahimi T, Pun T, Nijholt A, Patras I. **DEAP: A database for emotion analysis using physiological signals.** *IEEE Transactions on Affective Computing* 3(1), 18 to 31 (2012). DOI: 10.1109/T-AFFC.2011.15.

## Cohort

- 32 healthy adults (university students, age 19 to 37).
- Mixed gender; predominantly Western European.

## Stimulus

- 40 1-minute music videos selected from 120 candidates to span a 4-quadrant valence-arousal grid.
- Selection grounded in initial online ratings on Last.fm tags and the EmuSE selection procedure.

## Acquisition

- 32-channel BioSemi ActiveTwo EEG.
- Peripheral physiology: galvanic skin response (GSR), respiration belt, blood volume pulse, electromyography (EMG) on zygomaticus and trapezius.
- Frontal face video (RGB).

## Annotations

- Per-video self-ratings: valence, arousal, dominance, liking, familiarity (9-point Self-Assessment Manikin).
- Continuous annotation by external raters available for 14 of 40 videos in subsequent extensions.

## Outputs

- Pre-processed EEG (band-pass 4 to 45 Hz, downsampled 128 Hz, ICA artifact removal).
- Raw and pre-processed releases distributed.
- MATLAB and Python format.

## Access conditions

- Data Use Agreement via Queen Mary University of London.
- Music video files not redistributed; YouTube IDs and timing released.

## AGI annotation hooks

- Per-second valence / arousal trajectories from external raters (AGI candidate aggregation).
- Music features (tempo, key, lyrics presence, instrumentation) per video.
- HED tagging via candidate `Property/Affective/Valence/...` and `Property/Affective/Arousal/...`.

## Cross-references

- `seed/`: analogous emotion-EEG dataset on different stimuli.
- `naturalistic-neuroimaging-db/`: long-form naturalistic counterpart.
