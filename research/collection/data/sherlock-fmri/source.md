# Source notes: Sherlock fMRI (Chen 2017)

> Paywalled at Nature Neuroscience. PMC version PMC5552246 exists but was blocked by recaptcha at retrieval. Notes below distilled from the abstract, the Princeton DataSpace landing page, and the lit-review.

## Citation

Chen J, Leong YC, Honey CJ, Yong CH, Norman KA, Hasson U. **Shared memories reveal shared structure in neural activity across individuals.** *Nature Neuroscience* 20, 115 to 125 (2017). DOI: 10.1038/nn.4450. PubMed Central: PMC5552246.

## Cohort and acquisition

- 17 healthy adults (Princeton).
- 3 Tesla Siemens Skyra; whole-brain functional Magnetic Resonance Imaging (fMRI), 1.5-second TR.
- Continuous viewing for 50 minutes plus subsequent free-recall scan.

## Stimulus

- BBC Sherlock Season 1 Episode 1 ("A Study in Pink"); 50-minute audiovisual clip.

## Annotations released

- Scene boundaries (manually identified by raters; roughly 50 scenes).
- Free-recall transcripts (time-stamped) per subject.
- Scene-level summary vectors (Word2Vec / GloVe) used in Chen et al. analyses.

## Outputs

- BIDS-formatted fMRI deposit on Princeton DataSpace (88435/dsp01nz8062179).
- Companion ds001132 on OpenNeuro provides pre-processed Region of Interest (ROI) time series for community use.

## Access conditions

- DUA via Princeton Neuroscience Institute; covers stimulus rights compliance.
- Published recall transcripts and event-boundary annotations distributed openly.

## AGI annotation hooks

- Event boundaries are the gold-standard layer; AGI could host machine-derived alternative segmentations alongside human-rated.
- Free-recall transcripts are a unique participant-derived annotation layer; mappable to scene structure for memory-research applications.
- Character / location / object vectors are a Garden-style layered annotation.

## Cross-references

- `bang-multimodal/`: analogous narrative-segmentation paradigm with single-unit data.
- `studyforrest/`: feature-length naturalistic narrative counterpart.
