# Source notes: SEED (Zheng & Lu 2015)

> Paywalled at IEEE. Notes below distilled from the abstract, the dataset landing page (https://bcmi.sjtu.edu.cn/home/seed/), and the lit-review.

## Citation

Zheng W-L, Lu B-L. **Investigating critical frequency bands and channels for EEG-based emotion recognition with deep neural networks.** *IEEE Transactions on Autonomous Mental Development* 7(3), 162 to 175 (2015). DOI: 10.1109/TAMD.2015.2431497.

## Cohort

- 15 healthy adults (Chinese university students).
- Mixed gender; ages roughly 21 to 25.

## Stimulus

- 15 Chinese film clips, roughly 4 minutes each.
- Hand-curated for emotional valence: 5 positive (e.g., comedy moments), 5 neutral (e.g., documentary), 5 negative (e.g., dramatic / sad scenes).
- Each subject watches the same 15 clips across 3 sessions (1-week intervals).

## Acquisition

- 62-channel actiCAP scalp electroencephalography (EEG), 1000 Hz sampling.
- Self-reported emotion ratings collected after each clip.

## Outputs

- Pre-processed EEG (band-pass 1 to 75 Hz, downsampled 200 Hz, ICA artifact cleaning).
- Power spectral density features per channel and sub-band (delta, theta, alpha, beta, gamma).
- MATLAB and Python format.

## Access conditions

- Data Use Agreement via Shanghai Jiao Tong University Brain-Computer Interface and Machine Intelligence (BCMI) Lab.
- Film clips not redistributed; clip identifiers and timing released.

## SEED extensions

| Variant | Stimuli | Emotion classes | Modality additions |
|---------|---------|-----------------|-------------------|
| SEED-IV | 24 clips | 4 | eye tracking |
| SEED-V | 15 clips | 5 | peripheral physiology |
| SEED-VIG | driving simulation | drowsiness states | |
| SEED-Genuine | image stimuli | 4 | static images |

## AGI annotation hooks

- Per-clip continuous valence / arousal (community gap; current ratings are clip-level).
- Audio feature time series (loudness, spectral flux, music presence).
- Scene-shot boundaries via PySceneDetect.

## Cross-references

- `deap/`: analogous emotion-EEG dataset on music videos.
- `naturalistic-neuroimaging-db/`: long-form naturalistic counterpart.
