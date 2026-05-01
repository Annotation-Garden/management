# Source notes: HBN-EEG (Shirazi 2024)

> bioRxiv preprint PDF gated by Cloudflare from automated retrieval. Will retry once a captcha-free mirror surfaces; markdown summary below distilled from the lit-review and the project landing page (https://neuromechanist.github.io/data/hbn/).

## Citation

Shirazi SY, Truong D, Saliasi E, Zou Y, Robbins K, Delorme A, Cockx H, Tudor J, Chen J, Cheng C, Makeig S. **HBN-EEG: The FAIR implementation of the Healthy Brain Network (HBN) electroencephalography dataset.** *bioRxiv* 2024.10.03.615261 (2024). https://doi.org/10.1101/2024.10.03.615261

## Cohort

- N > 3,000 participants from Healthy Brain Network (HBN) cohort.
- Age range 5 to 21 years.
- Diagnostic spread covering attention-deficit/hyperactivity disorder (ADHD), autism spectrum disorder, anxiety, depression, and typically developing.
- 11 sequential release batches (R1 through R11) with version-controlled additions.

## Acquisition

- 128-channel BioSemi ActiveTwo (high-density) plus a smaller subset on Electrical Geodesics 128-channel HydroCel Geodesic Sensor Net (HGSN).
- Sampling rate 500 Hz (downsampled from 2048 or 1000 Hz).
- Single visit lasting roughly 90 minutes of EEG.

## Tasks (in order)

1. Resting State (eyes-open and eyes-closed, 5 minutes).
2. Surround Suppression (visual psychophysics).
3. Contrast Change Detection (visual psychophysics).
4. Sequence Learning (motor/cognitive).
5. Symbol Search Test (Wechsler-style speed task).
6. Video Decision Making (custom cognitive paradigm).
7. Movie viewing block:
   - Despicable Me (10-minute clip).
   - The Present (3.5-minute animated short).
   - Diary of a Wimpy Kid: The Movie Trailer (90 seconds).
   - Fun with Fractals (custom psychometric stimulus).

## Outputs released

- BIDS deposit on OpenNeuro (ds005505 through ds005514+, one dataset per release batch).
- BIDS sidecar `events.tsv` plus `events.json` carrying Hierarchical Event Descriptor (HED) tags for every event marker.
- Phenotyping (clinical) data in a parallel governed-access deposit.
- Per-task event marker dictionaries documented in `participants.tsv` and `task-*.json`.

## Hierarchical Event Descriptor (HED) sidecars

Example mapping for the Surround Suppression task:

```
"trial_type": {
  "stim_on": "(Sensory-event, Visual-presentation), (Item/Object/Geometric/Annulus, Onset)",
  "fixation_break": "(Eye-blink, Onset)"
}
```

Movie tasks tag global onsets / offsets for narrative segments and named characters where the layer has been curated.

## Access conditions

- BIDS data: open via OpenNeuro / NEMAR (Neuroelectromagnetic Data Archive and Tools Resource).
- Movies: not redistributed; users must obtain media themselves and align to provided onsets.
- Phenotyping (clinical labels, IQ, demographics): governed access via HBN Data Access Agreement (Child Mind Institute).

## AGI annotation hooks

| Layer | State | Garden opportunity |
|-------|-------|--------------------|
| HED event tags (cognitive tasks) | curated by Shirazi et al. | Already complete; AGI hosts the schema mappings. |
| HED event tags (movies) | partial (onsets / character labels) | Frame-level annotations (saliency, character identity, scene boundary) needed. |
| Movie shot / scene boundaries | absent | Despicable Me cuts (PySceneDetect) plus manual review. |
| Character emotion ratings | absent | Continuous valence/arousal trace per character. |
| Verbal speech / phonemes | absent | Forced alignment of dialogue. |
| HED-Lang mapping | partial | Linguistic schema deployment over verbal segments. |

## Cross-references

- `hbn-mri/`: paired functional Magnetic Resonance Imaging (fMRI) data on the same cohort (Alexander 2017).
- `studyforrest/`: analogous deep-sampling adult counterpart.
