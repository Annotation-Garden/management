# Dataset Hierarchy

A formal placement of all 36 dataset entries collected in [`research/collection/data/`](../collection/data/) along the naturalistic to cognitive-task spectrum. The Phase 1 [`data/INDEX.md`](../collection/data/INDEX.md) sets the qualitative framing; this document elevates that framing to explicit, machine-checkable axes and surfaces the entries that are most under-annotated relative to their potential.

Abbreviations: Brain Imaging Data Structure (BIDS), Hierarchical Event Descriptors (HED), Natural Scenes Dataset (NSD), Healthy Brain Network (HBN), magnetoencephalography (MEG), electroencephalography (EEG), intracranial EEG (iEEG), functional magnetic resonance imaging (fMRI), diffusion-weighted MRI (DWI), data-use agreement (DUA).

## Axes

Each dataset is placed on six axes:

- **stimulus_type**: image, video, audio, multi-task, hybrid, single-stimulus benchmark.
- **modality_coverage**: which neural and behavioral channels are recorded against the same stimulus.
- **annotation_density**: `none` (no stimulus annotations beyond trial timing), `minimal` (a handful of event labels), `moderate` (a single or two annotation perspectives), `rich` (multi-perspective annotations spanning visual, semantic, emotional, narrative dimensions).
- **sample_size**: cohort size, ranges where mixed (e.g., scan vs. behavior).
- **copyright_tier**: `open` (annotations and stimulus redistributable), `pointer-required` (stimulus must be obtained separately, AGI hosts pointers and annotations), `restricted` (DUA gates either stimulus or recordings).
- **flagship_status**: `phase-1` (current AGI white-paper flagship), `phase-2-candidate` (extensible from current flagships with high payoff), `second-wave` (next-tier candidate for an AGI stimulus repository), `reference-only` (useful corpus context but not a near-term AGI repo).

The `annotation_density` and `AGI hook` columns recapitulate the [`data/INDEX.md`](../collection/data/INDEX.md) framing; the other axes are added here.

## Naturalistic, static images

Single-image stimuli paired with rich neuroimaging. The image is a stable referent, so annotation layers (object segmentation, captions, affect, HED tags) can propagate cleanly across modalities.

| Slug | Stimulus type | Modality coverage | Density | N | Copyright tier | Flagship status |
|---|---|---|---|---|---|---|
| [`nsd-fmri`](../collection/data/nsd-fmri/card.md) | image | fMRI 7T | rich (COCO inherits) | 8 | open | phase-1 |
| [`nsd-ieeg`](../collection/data/nsd-ieeg/card.md) | image | iEEG | rich (NSD inherits) | 12 | restricted (clinical DUA) | phase-1 |
| [`nsd-eeg-alljoined`](../collection/data/nsd-eeg-alljoined/card.md) | image | scalp EEG | rich (NSD inherits) | 8 | open | phase-1 |
| [`things-initiative`](../collection/data/things-initiative/card.md) | image | fMRI, MEG, EEG | rich | up to 17 per modality | open with mixed image-license terms | second-wave |
| [`nod-eeg`](../collection/data/nod-eeg/card.md) | image | MEG, EEG | rich (THINGS inherits) | 20+ | open | second-wave |
| [`things-eeg2`](../collection/data/things-eeg2/card.md) | image | scalp EEG | rich (THINGS inherits) | 10 | open | second-wave |
| [`bold5000`](../collection/data/bold5000/card.md) | image | fMRI 3T | moderate | 4 | open | second-wave |
| [`coco`](../collection/data/coco/card.md) | image (stimulus source) | n/a (image-only) | rich (annotations) | n/a | pointer-required (mixed Flickr terms) | reference-only |
| [`glmsingle-paper`](../collection/data/glmsingle-paper/card.md) | methods | n/a | n/a | n/a | open | reference-only |

Under-annotated relative to potential:

- **BOLD5000** has 5,000 images and four deeply-sampled subjects, all openly licensed, but only moderate annotation density. A HED layer plus per-image semantic tags would let it function as the 3T sibling to NSD across labs that cannot reach the 7T data; today it is mostly used as a methods-validation set.
- **THINGS-initiative** has the largest concept-set in cognitive neuroscience (1,854 concepts, 4.7 million similarity judgments) but per-image HED tags are absent and the Same-Person, SPoSE behavioral embedding is the only "annotation" layer at scale. A HED layer would unlock cross-modal alignment with NOD-EEG and THINGS-EEG2.

## Naturalistic, video and film

Long-form audiovisual stimuli. Annotation surface is the largest of any class (shot boundaries, character identity, emotion, theory-of-mind events, dialogue, sound design).

| Slug | Stimulus type | Modality coverage | Density | N | Copyright tier | Flagship status |
|---|---|---|---|---|---|---|
| [`studyforrest`](../collection/data/studyforrest/card.md) | video | fMRI 7T, audio | rich | 20 | open (annotations CC-BY) | phase-1 |
| [`studyforrest-eyegaze`](../collection/data/studyforrest-eyegaze/card.md) | video | fMRI 7T plus eye tracking | rich | 15 | open | phase-1 |
| [`hbn-mri`](../collection/data/hbn-mri/card.md) | video | fMRI 3T, MRI, EEG, behavior | minimal | 5,000+ | restricted (CMI DUA) | phase-1 |
| [`hbn-eeg`](../collection/data/hbn-eeg/card.md) | video | high-density EEG | rich (HED-tagged) | 3,000+ | open (BIDS) | phase-1 |
| [`bang-ieeg-fmri`](../collection/data/bang-ieeg-fmri/card.md) | video | iEEG, fMRI 3T | moderate | 51 plus 30 | restricted (clinical) | second-wave |
| [`bang-multimodal`](../collection/data/bang-multimodal/card.md) | video | iEEG plus single-unit, fMRI | rich | 29 | restricted (Cedars-Sinai or Caltech DUA) | second-wave |
| [`naturalistic-neuroimaging-db`](../collection/data/naturalistic-neuroimaging-db/card.md) | video | fMRI 3T | minimal | 86 | open | phase-2-candidate |
| [`courtois-neuromod`](../collection/data/courtois-neuromod/card.md) | video | fMRI 3T, eye tracking | minimal-to-moderate | 6 | restricted (CC-NC custom DUA) | phase-2-candidate |
| [`sherlock-fmri`](../collection/data/sherlock-fmri/card.md) | video | fMRI 3T | moderate | 17 | restricted (DUA), pointer for stimulus | second-wave |
| [`inscapes`](../collection/data/inscapes/card.md) | video | fMRI 3T | minimal | 36 | open with NC video terms | reference-only |

Under-annotated relative to potential:

- **HBN-MRI** combines naturalistic movie viewing with developmental phenotyping at unprecedented scale (5,000+ subjects, ages 5 to 21). The neuroimaging is rich; the stimulus annotation is essentially "movie ID and onset". A HED-tagged scene-and-character annotation would convert HBN-MRI into a developmental-trajectory benchmark for every theme on the [`science-map`](./science-map.md).
- **Naturalistic Neuroimaging Database** has 86 subjects watching 10 feature films and almost no annotation; films are well-known commercial titles where a pointer-architecture solution analogous to HBN movies would unlock community contribution.
- **Inscapes** is a paradigmatic exemplar (low-arousal abstract animation as a halfway point between rest and naturalistic) but has minimal annotation; it is `reference-only` until annotation density catches up to its conceptual importance.

## Naturalistic, audio and narrative

Spoken stories, podcasts, and audiobook stimuli. Annotation lives at phoneme, word, sentence, narrative-event, and prosodic levels.

| Slug | Stimulus type | Modality coverage | Density | N | Copyright tier | Flagship status |
|---|---|---|---|---|---|---|
| [`narratives-pieman`](../collection/data/narratives-pieman/card.md) | audio | fMRI 3T, audio | rich (HED-Lang sidecar) | 345 | open | phase-2-candidate |
| [`moth-radio-hour`](../collection/data/moth-radio-hour/card.md) | audio | fMRI 3T, audio | rich | 7 | open (data CC-BY), publisher-paywall (paper) | second-wave |
| [`little-prince-fmri`](../collection/data/little-prince-fmri/card.md) | audio | fMRI 3T, audio | rich (multilingual) | 49 | open | second-wave |
| [`natural-sounds-fmri`](../collection/data/natural-sounds-fmri/card.md) | audio | fMRI 3T, audio | moderate | 20+ | open | reference-only |

Under-annotated relative to potential:

- **Moth Radio Hour** has 2 hours per subject and is the canonical reference for continuous-language encoding (Huth 2016, Antonello 2023, LeBel 2023 successors). Annotations are word-aligned but pre-HED. Layering a HED-LANG annotation on top would re-anchor the entire encoding-model literature on a community-versioned annotation instead of per-paper transcripts.
- **Little Prince** is a natural cross-lingual benchmark; current annotations are English-aligned with Mandarin and French alignments inconsistent across releases. Standardizing the HED-LANG layer across languages is a single-PR-per-language deliverable.

## Cognitive task batteries

Structured paradigms with simple event vocabularies, large N, and high reproducibility. Annotation density is intrinsically lower (a handful of trial types per task), so the AGI value is community-curated HED Generation-3 sidecars rather than rich multi-perspective annotation.

| Slug | Stimulus type | Modality coverage | Density | N | Copyright tier | Flagship status |
|---|---|---|---|---|---|---|
| [`hcp-task`](../collection/data/hcp-task/card.md) | multi-task | fMRI 3T or 7T | moderate | 1,200 | restricted (HCP DUA) | second-wave |
| [`hcp-d-development`](../collection/data/hcp-d-development/card.md) | multi-task | fMRI 3T | moderate | 1,300 | restricted (HCP DUA) | second-wave |
| [`abcd-task`](../collection/data/abcd-task/card.md) | multi-task | fMRI 3T | moderate | 11,800 | restricted (NIMH DA DUA) | second-wave |
| [`cam-can`](../collection/data/cam-can/card.md) | multi-task | fMRI 3T, MEG | moderate | 700 | restricted (Cam-CAN DUA) | second-wave |
| [`aomic`](../collection/data/aomic/card.md) | multi-task | fMRI 3T | moderate | 1,500+ | open | second-wave |
| [`myconnectome`](../collection/data/myconnectome/card.md) | multi-task | fMRI 3T, multi-omics | minimal | 1 | open | reference-only |

Under-annotated relative to potential:

- **HCP-task, ABCD-task, Cam-CAN, AOMIC** all release events as TSV with custom columns and zero HED tags. Curating community-blessed HED Generation-3 sidecars per task (working memory, n-back, monetary-incentive-delay, stop-signal, language, motor) is one of the highest-leverage AGI-distinctive contributions because every cognitive-neuroscience reanalysis would benefit instantly. None of this is in the AGI white paper; none of this is in the ANNOTATE R01.
- **AOMIC** is fully open and built around BIDS, making it the lowest-friction AGI on-ramp for the cognitive-task wedge.

## Hybrid, mixed paradigms

Datasets that span naturalistic and structured task content, or combine resting state with task. They bridge the two ends of the spectrum.

| Slug | Stimulus type | Modality coverage | Density | N | Copyright tier | Flagship status |
|---|---|---|---|---|---|---|
| [`lemon-mpi`](../collection/data/lemon-mpi/card.md) | hybrid | fMRI 3T plus 62-channel EEG | minimal | 227 | open | second-wave |
| [`dhcp`](../collection/data/dhcp/card.md) | hybrid | fMRI 3T, MRI, DWI | none-to-minimal | 1,500+ | restricted (Imperial or KCL DUA) | reference-only |
| [`deap`](../collection/data/deap/card.md) | hybrid | 32-channel EEG plus physiology | moderate | 32 | restricted (QMUL DUA) | reference-only |
| [`seed`](../collection/data/seed/card.md) | hybrid | 62-channel EEG | moderate | 15 | restricted (BCMI DUA) | reference-only |

Hybrid datasets are the bridge between [`hbn-eeg`](../collection/data/hbn-eeg/card.md) (which combines movie watching plus task plus rest in a single subject visit) and the cognitive-task batteries above. AGI's value is to demonstrate that the same HED sidecar machinery handles task, movie, and rest within a single repository, with the [`hbn-eeg card`](../collection/data/hbn-eeg/card.md) being the existing exemplar.

## Single-stimulus benchmarks

Localizers and small canonical paradigms that anchor cohort-level analyses.

| Slug | Stimulus type | Modality coverage | Density | N | Copyright tier | Flagship status |
|---|---|---|---|---|---|---|
| [`fedorenko-language-localizer`](../collection/data/fedorenko-language-localizer/card.md) | single-stimulus | fMRI | minimal | 49 plus thousands | open (paper paywalled) | second-wave |
| [`pinel-localizer`](../collection/data/pinel-localizer/card.md) | single-stimulus | fMRI | minimal | 81 | open | second-wave |
| [`localizer-ds000114`](../collection/data/localizer-ds000114/card.md) | single-stimulus | fMRI | minimal | 1,311 | open | second-wave |

Single-stimulus benchmarks intrinsically have low annotation density but high reusability. A canonical AGI-hosted HED Generation-3 sidecar per localizer (language vs. nonword, Pinel ten-task, calculation, motor) is a one-PR contribution that would propagate across thousands of fMRI re-analyses.

## Aggregate AGI rollout map

Counting each dataset against its `flagship_status`:

- **phase-1 (current white-paper flagships)**: NSD-fMRI, NSD-iEEG, NSD-EEG-alljoined, StudyForrest, StudyForrest-eyegaze, HBN-MRI, HBN-EEG. Seven entries.
- **phase-2-candidate (extensible from current flagships)**: Naturalistic Neuroimaging DB, Courtois-Neuromod, Narratives-Pieman. Three entries.
- **second-wave (next-tier AGI stimulus repositories)**: THINGS-initiative, NOD-EEG, THINGS-EEG2, BOLD5000, Bang-iEEG-fMRI, Bang-multimodal, Sherlock-fMRI, Moth-Radio-Hour, Little-Prince-fMRI, HCP-task, HCP-D, ABCD-task, Cam-CAN, AOMIC, LEMON-MPI, Fedorenko-localizer, Pinel-localizer, ds000114-localizer. Eighteen entries.
- **reference-only**: COCO (stimulus source), GLMsingle-paper (methods), Inscapes, MyConnectome, Natural-Sounds-fMRI, dHCP, DEAP, SEED. Eight entries.

Total: 36.

The current white paper's three "flagships" (NSD, StudyForrest, HBN movies) collapse the seven phase-1 entries above into three stimulus repositories. The phase-2-candidate column gives Phase 3 a natural fourth-and-fifth flagship to recommend.

## Distinctive observations for Phase 3

- **The cognitive-task wedge is empty** in both the AGI white paper and the ANNOTATE R01. Six second-wave cognitive-task batteries (HCP, HCP-D, ABCD, Cam-CAN, AOMIC, MyConnectome) carry combined N greater than 16,000. None has a community-curated HED sidecar.
- **The non-imaging modality wedge is thin**. Eye-tracking (StudyForrest-eyegaze, Courtois-Neuromod), peripheral physiology (DEAP), and behavioral phenotyping (HBN-MRI, ABCD-task) all sit alongside neural recordings but have no AGI-style annotation companion repos.
- **Copyright tier is bimodal**, not continuous. Twenty-one entries are fully open; thirteen are DUA-restricted; two are pointer-required for stimulus. AGI's pointer-architecture mechanism (per [`agi-white-paper.md`](../../agi-white-paper.md)) handles the pointer tier cleanly; the DUA tier needs an explicit federation protocol that is not in the white paper today.
- **Annotation density and N are inversely correlated** across the corpus. Every entry with rich annotations has N less than 30 (NSD-fMRI, StudyForrest, Bang-multimodal, Moth-Radio-Hour, Little-Prince-fMRI). Every entry with N > 1,000 has minimal or moderate density (HBN-MRI, ABCD-task, dHCP, HCP-task). The single exception, [`hbn-eeg`](../collection/data/hbn-eeg/card.md), is rich and large and is the canonical AGI proof of concept.

## Coverage check

All 36 dataset entries listed in [`../collection/data/INDEX.md`](../collection/data/INDEX.md) are placed across the six categories above:

- Naturalistic static images (9): nsd-fmri, nsd-ieeg, nsd-eeg-alljoined, things-initiative, nod-eeg, things-eeg2, bold5000, coco, glmsingle-paper.
- Naturalistic video and film (10): studyforrest, studyforrest-eyegaze, hbn-mri, hbn-eeg, bang-ieeg-fmri, bang-multimodal, naturalistic-neuroimaging-db, courtois-neuromod, sherlock-fmri, inscapes.
- Naturalistic audio and narrative (4): narratives-pieman, moth-radio-hour, little-prince-fmri, natural-sounds-fmri.
- Cognitive task batteries (6): hcp-task, hcp-d-development, abcd-task, cam-can, aomic, myconnectome.
- Hybrid (4): lemon-mpi, dhcp, deap, seed.
- Single-stimulus benchmarks (3): fedorenko-language-localizer, pinel-localizer, localizer-ds000114.

Total: 36.
