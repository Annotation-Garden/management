# Source notes: NSD-EEG / alljoined (Xu et al. 2024)

> No standalone descriptor PDF could be retrieved (arXiv preprint Xu 2401.10023 not retrievable via opencite default route at retrieval time). Notes below distilled from preprint abstracts and OpenNeuro deposit README.

## Citation

Xu A, Choksi A, Roig G, Nemrodov D, Cichy RM. **Alljoined: A neural foundation model for visual perception across modalities.** *arXiv* 2401.10023 (2024).

Companion deposit: **OpenNeuro ds005810 (NSD-EEG)**.

## Cohort

- 8 healthy adults.

## Stimulus

- Subset of Natural Scenes Dataset (NSD) shared 1,000 images plus extension sets.
- Rapid event-related design.

## Acquisition

- 64- or 128-channel scalp electroencephalography (EEG).
- Sampling rate 1000 Hz; downsampled to 200 to 250 Hz for analysis.

## Outputs

- Continuous EEG raw recordings (BIDS-formatted).
- Pre-processed event-related potentials (ERPs) per image.
- Image-level prediction performance baselines.

## Access conditions

- OpenNeuro deposit CC0.
- Stimuli inherit NSD / Microsoft Common Objects in Context (COCO) image rights.

## AGI annotation hooks

- Same NSD COCO image identifiers; AGI annotation propagation is identical to NSD-fMRI.
- High temporal resolution complements fMRI's spatial resolution; Hierarchical Event Descriptor (HED) timing precision matters more than for fMRI.

## Cross-references

- `nsd-fmri/`: fMRI counterpart.
- `nsd-ieeg/`: intracranial counterpart.
- `nod-eeg/`: concept-image counterpart on THINGS image set.
