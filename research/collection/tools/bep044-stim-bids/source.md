# BEP044: Stimuli BIDS (Stim-BIDS)

Source snapshot: https://github.com/bids-standard/bids-specification/pull/2022

BEP044, also known as Stim-BIDS, is a BIDS Extension Proposal that defines a folder layout and metadata schema for stimulus repositories that are referenced from one or more Brain Imaging Data Structure (BIDS) datasets. The proposal extends the existing BIDS specification so that stimuli (still images, audio clips, video clips, complex experimental scripts) can be packaged independently of any single brain-recording dataset and reused across studies.

Key elements of the proposal:

- A stimulus repository contains `stimuli/` with the source media (or pointers / hashes when not redistributable), `annotations/` with one subfolder per annotation type, and a top-level `dataset_description.json` describing the stimulus collection, its license, and provenance.
- Each annotation type carries an `events.tsv` and a sidecar `events.json` describing column meanings, including Hierarchical Event Descriptor (HED) tags.
- BIDS recording datasets reference a stimulus by stable identifier (DOI, ResearchObject ID, or git commit hash) so that downstream analyses can pin themselves to a specific stimulus version.
- A `participants.tsv`-like file at the stimulus side captures rater or annotator identity.

Status as of 2026-04-30: under active community review; merge into the main specification expected during BIDS 2.0 cycle.

Related artifacts:

- Tracking pull request: https://github.com/bids-standard/bids-specification/pull/2022
- Discussion: BIDS Maintainers monthly meetings, BrainHack outputs, OpenNeuro working group.
- Cross-cutting consumers: NEMAR (events HED search), Neuroscout (Pliers feature ingest), Annotation Garden Initiative (entire repository pattern).
