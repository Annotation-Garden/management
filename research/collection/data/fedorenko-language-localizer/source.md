# Source notes: Fedorenko Language Localizer (2010)

> Paywalled at Journal of Neurophysiology. PMC equivalent (PMC2932639) blocked by recaptcha at retrieval. Notes below distilled from the abstract, the EvLab funcloc landing page (https://evlab.mit.edu/funcloc/), and the lit-review.

## Citation

Fedorenko E, Hsieh PJ, Nieto-Castañón A, Whitfield-Gabrieli S, Kanwisher N. **New method for fMRI investigations of language: defining ROIs functionally in individual subjects.** *Journal of Neurophysiology* 104(2), 1177 to 1194 (2010). DOI: 10.1152/jn.00032.2010. PubMed Central: PMC2932639.

## Cohort

- N = 49 adults in original validation.
- Subsequent replication cohorts span thousands of subjects worldwide.

## Stimulus and design

- 5-minute functional Magnetic Resonance Imaging (fMRI) paradigm.
- Block design: 12 blocks alternating sentence and nonword conditions.
- Each block: 18 seconds, 12 trials of 8-word sentences (or 8-nonword lists).
- Rapid serial visual presentation (RSVP) at 350 ms per word.
- Sentence stimuli: roughly 240 unique sentences sampled from Brown corpus.
- Nonword stimuli: pronounceable but meaningless letter strings.

## Outputs

- Subject-specific language ROIs at p < 0.001 voxel threshold.
- Group-level network maps in MNI space.
- Open analysis code (SPM-based) in MATLAB and Python ports.

## Annotations and materials

- Stimulus lists openly released at evlab.mit.edu/funcloc.
- Multilingual translations: English, Spanish, Mandarin Chinese community-curated.
- Stimulus presentation scripts: PsychToolbox / PsychoPy variants.

## Access conditions

- Paper paywalled; PMC PDF currently gated by recaptcha.
- Stimulus materials openly downloadable.

## AGI annotation hooks

- HED-Lang sidecar mapping for sentence vs nonword conditions.
- Cross-walk between localized regions of interest (ROIs) and naturalistic-stimulus encoding studies (Moth Radio, Narratives, Little Prince).
- Multilingual stimulus variants require translated word-lists with HED-Lang phoneme-aligned tags.

## Cross-references

- `pinel-localizer/`: multi-task localizer counterpart.
- `hcp-task/`: language sub-task within HCP battery.
- `narratives-pieman/`: naturalistic language counterpart.
