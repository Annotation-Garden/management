# Source notes: Inscapes (Vanderwal 2015)

> Paper paywalled at NeuroImage / Elsevier. PMC version exists (PMC4930087) but PMC PDF download was blocked by recaptcha at retrieval.
> Source markdown summary distilled from the published abstract, the project page (https://www.headspacestudios.org/inscapes), and the lit-review.

## Citation

Vanderwal T, Kelly C, Eilbott J, Mayes LC, Castellanos FX. **Inscapes: A movie paradigm to improve compliance in functional magnetic resonance imaging.** *NeuroImage* 122, 222 to 232 (2015). DOI: 10.1016/j.neuroimage.2015.07.069. PubMed Central: PMC4930087.

## Cohort

- N = 36 healthy adults (validation cohort).
- Subsequent applications: hundreds of subjects across HBN, ABCD pilot, paediatric clinical trials.

## Stimulus

- 7-minute high-definition animation of abstract shapes (geometric forms slowly evolving) with ambient electronic music.
- Designed to be visually engaging but narratively flat (no characters, no social content, no language).
- Distributed by Head Space Studios via institutional license.

## Validation outcomes (paper)

- Head motion was reduced relative to eyes-open resting state.
- Functional connectivity reliability comparable to resting state.
- Inter-subject correlation higher than resting state but lower than narrative film (e.g., Despicable Me).

## Annotations

- Low-level: luminance, motion energy, color shifts, music phrase boundaries.
- High-level: intentionally minimal; the stimulus is meant as a "natural fixation" alternative.

## Access conditions

- Stimulus distributed via Vanderwal lab / Head Space Studios with terms of use agreement (free for research).
- No central BIDS deposit; embedded in many studies (e.g., HBN, ds002080).

## AGI annotation hooks

- Audio-feature time series (loudness, spectral flux, music phrase markers).
- Visual feature time series (luminance, motion energy, color statistics).
- Useful as a control stimulus in Garden encoding-model benchmarks: shows how much performance is driven by social and narrative content versus pure low-level audiovisual statistics.

## Cross-references

- `studyforrest/`: high-narrative counterpart.
- `hbn-mri/`: uses Inscapes as a control stimulus in paediatric protocols.
