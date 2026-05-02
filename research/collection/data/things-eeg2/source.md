# Source notes: Things-EEG2 (Gifford 2022)

> Paywalled at NeuroImage / Elsevier. PMC equivalent not yet released at retrieval. Notes below distilled from the abstract, the OSF deposit (https://osf.io/3jk45/), and the lit-review.

## Citation

Gifford AT, Dwivedi K, Roig G, Cichy RM. **A large and rich EEG dataset for modeling human visual object recognition.** *NeuroImage* 264, 119754 (2022). DOI: 10.1016/j.neuroimage.2022.119754.

## Cohort

- 10 healthy adults.
- Mixed gender, ages roughly 22 to 30.

## Stimulus

- 16,540 unique training images (1,654 THINGS concepts, 10 exemplars each).
- 200-concept test set with multiple presentations per concept.
- All images sourced from the THINGS database.

## Acquisition

- 64-channel BrainProducts ActiCAP electroencephalography (EEG), 1000 Hz sampling rate.
- 5 Hz rapid serial visual presentation (RSVP): 200 ms image-on, no inter-stimulus interval.
- Subjects performed an unrelated oddball detection task to maintain attention.

## Outputs

- Pre-processed epoched EEG (per image, per subject).
- Trial-averaged event-related potential (ERP) tensors.
- Baseline decoding pipelines (Linear Discriminant Analysis, deep learning classifiers).
- Brain Imaging Data Structure (BIDS)-compliant deposit on OSF and Zenodo.

## Access conditions

- Data released under CC-BY 4.0.
- THINGS image set has separate research-use terms.

## AGI annotation hooks

- Concept-level annotations propagate from THINGS (1,854 concepts).
- Per-image annotations (saliency, object position, color statistics) would extend the surface.
- HED `Item/Object/...` mapping per concept.

## Cross-references

- `things-initiative/`: multi-modal counterpart.
- `nsd-fmri/`: fMRI counterpart on different image set.
