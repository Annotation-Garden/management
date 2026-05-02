# Source notes: NSD-iEEG (Huang et al. 2024)

> No paper PDF is publicly available. The descriptor is a Vision Sciences Society 2024 conference abstract published in Journal of Vision.
> URL: https://jov.arvojournals.org/article.aspx?articleid=2801527

## Citation

Huang H, Magnotti J, Tandon N. **An intracranial EEG Natural Scenes Dataset to integrate human visual cortex dynamics with computational vision models.** *Journal of Vision* 24(10):379 (2024). VSS 2024 abstract.

## Cohort and recording

- 12 patients undergoing presurgical evaluation for medication-resistant epilepsy at the Texas Comprehensive Epilepsy Program (Memorial Hermann / UTHealth).
- Stereo-electroencephalography (sEEG) depth electrodes; subset with subdural grid coverage.
- Channel counts ranged across patients (typical 100 to 200 contacts).

## Stimulus design

- 1,000 NSD images drawn from the NSD shared subset.
- Each image presented 2 to 3 times.
- Visual angle and timing matched as closely as possible to the original NSD fMRI design (3 s on / 1 s off).
- One-back oddity task to maintain attention.

## Outputs

- Broadband gamma activity (BGA) envelopes (70 to 150 Hz, log power normalized to inter-trial baseline).
- Event-selective electrode list per patient (face, body, place, food, scene, animate vs inanimate).
- Some preliminary results report BGA peaks at roughly 100 to 200 ms post-stimulus over fusiform contacts.

## Access and licensing

- Not currently on OpenNeuro. Access via direct collaboration with Tandon lab; subject to institutional review board (IRB) and patient consent constraints.
- Stimulus annotations and trial logs share NSD's licensing model.

## AGI annotation hooks

- Same 1,000 NSD shared stimuli; any annotation layer added to NSD propagates to this dataset.
- Particularly useful for evaluating temporal precision of stimulus-feature encoding (e.g., when does HED `Item/Object/Animal/Dog` become decodable).
- Single-electrode Hierarchical Event Descriptor (HED) `Action/Cognitive/Recognize` tags could anchor cross-modal Representational Similarity Analysis (RSA).

## Cross-references

- NSD-fMRI: `nsd-fmri/`.
- THINGS-iEEG: not in this collection (not yet released as a full dataset).
- Berezutskaya 2022 "Bang!" iEEG-fMRI: `bang-ieeg-fmri/` for movie-based equivalent.
