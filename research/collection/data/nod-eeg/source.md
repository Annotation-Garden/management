# Source notes: Natural Object Dataset MEG/EEG (Zhang 2025)

> Paper PDF gated by Springer Nature recaptcha at PubMed Central; not redistributed.
> OpenNeuro deposit (ds005811) is openly accessible.

## Citation

Zhang Y, Song Y, He B, Cui Y, Du Y, Yu S, Liu J. **A large-scale MEG and EEG dataset for object recognition in naturalistic scenes.** *Scientific Data* 12:1234 (2025). DOI: 10.1038/s41597-025-05174-7. PubMed Central: PMC12102372.

## Cohort and acquisition

- 20 to 30 adult subjects (precise N varies per modality).
- High-density EEG (typical 64- or 128-channel) and 306-channel magnetoencephalography (MEG) recordings.
- Brain Imaging Data Structure (BIDS)-formatted on OpenNeuro: ds005811.

## Stimulus design

- Image set drawn from THINGS (1,854 object concepts, multiple exemplars each).
- Subjects viewed thousands of images per session in rapid serial visual presentation (RSVP) and slower paradigms.
- Companion behavioral tasks: similarity judgments, naming.

## Outputs released

- Continuous EEG/MEG raw recordings.
- Pre-processed epoched event-related potentials (ERPs) / event-related fields (ERFs) per concept.
- BIDS sidecar `events.tsv` with `concept` and `exemplar` columns.

## Access conditions

- OpenNeuro CC0/CC-BY (per dataset metadata).
- Hosted on AWS Simple Storage Service (S3) via OpenNeuro mirror.
- Stimuli covered by THINGS license terms (research use; redistribution restricted).

## AGI annotation hooks

- THINGS concept identifiers anchor the entire dataset; Garden contributors can attach feature ratings (animacy, size, manipulability) once and the layer joins to NSD-fMRI, Things-fMRI, Things-MEG, Things-EEG2, and this dataset.
- Hierarchical Event Descriptor (HED) tagging is straightforward via `Item/Object/Living-thing/Animal/...` and `Item/Object/Manmade/...` branches.

## Cross-references

- `things-initiative/`: the source concept set.
- `nsd-fmri/`: visual benchmark with overlapping methodology.
