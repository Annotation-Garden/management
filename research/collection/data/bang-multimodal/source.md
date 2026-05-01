# Source notes: Bang! You're Dead multimodal (Aly et al., ds004798)

> No standalone descriptor PDF is available at retrieval. Notes below distilled from the OpenNeuro deposit README, the lit-review, and the Zheng et al. 2022 analysis paper.

## Citation

OpenNeuro deposit ds004798 v1.0.2: **Multimodal brain responses during movie watching: single-neuron, intracranial EEG, and fMRI in human patients.** Aly M, Tsao A, Reber TP, Rey HG, Adolphs R, Rutishauser U. https://openneuro.org/datasets/ds004798/versions/1.0.2

Companion analysis: Zheng J et al. **Neurons detect cognitive boundaries to structure episodic memories in humans.** *Nature Neuroscience* 25, 358 to 368 (2022).

## Cohort and acquisition

- 29 epilepsy patients across Cedars-Sinai and Toronto Western (Behnke-Fried microwire bundles in mesial temporal lobe).
- Single-unit (sorted clusters), local field potentials, and broader stereo-EEG coverage.
- Companion 3 Tesla functional Magnetic Resonance Imaging (fMRI) cohort viewing the same clip.

## Stimulus

- 8-minute clip from Alfred Hitchcock Presents (1961) episode "Bang! You're Dead".
- Identical clip used in Berezutskaya et al. (ds003688) plus extended end segment.

## Movie annotations included

- Shot boundaries (timestamps of cuts).
- Face appearances per character (face identity over time).
- Location changes (room transitions).
- Narrative event-boundary ratings collected from human raters (continuous response).
- Speech onsets (dialogue timestamps).

## Outputs

- BIDS-iEEG (single-unit spike times, local field potential) and BIDS-MRI deposits.
- behavioural ratings tsv files per task.

## Access conditions

- OpenNeuro deposit metadata under CC0; raw single-unit data under DUA in some sub-collections.
- Stimulus clip is copyright; researchers must comply with redistribution terms.

## AGI annotation hooks

- Event-boundary annotations are the keystone layer that yielded the "event cell" finding; AGI hosts these as the gold-standard reference.
- Open invitation for additional layers: continuous suspense, theory-of-mind state, perspective shifts.

## Cross-references

- `bang-ieeg-fmri/`: Berezutskaya 2022 ds003688 sister deposit.
- `studyforrest/`: long-form deep-sampling counterpart.
