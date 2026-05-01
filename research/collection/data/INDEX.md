# Strand B, Data Index

One-line summaries organized along the naturalistic ↔ cognitive-task spectrum. Read top-to-bottom to walk from richly-annotated naturalistic stimuli (NSD, studyforrest, HBN movies) toward minimally-annotated single-purpose cognitive tasks (Pinel localizer, HCP tasks).

Notation: **N** = participants, **density** = annotation density (none / minimal / moderate / rich), **AGI hook** = why a Garden contributor would care.

## Naturalistic, static images

The visual-stimulus end of the AGI universe. Single image annotations (object segmentation, captions, affect ratings, Hierarchical Event Descriptor (HED) tags) propagate across paired functional Magnetic Resonance Imaging (fMRI), magnetoencephalography (MEG), electroencephalography (EEG), and intracranial EEG (iEEG) recordings.

| Slug | Year | Modalities | N | Density | AGI hook |
|------|------|-----------|---|---------|----------|
| [`nsd-fmri`](nsd-fmri/) | 2022 | 7T fMRI | 8 | rich (COCO inherits) | Flagship deep-sampling visual benchmark; 73,000 COCO images; cross-modal anchor. |
| [`nsd-ieeg`](nsd-ieeg/) | 2024 | iEEG | 12 | rich (NSD inherits) | NSD's intracranial sibling; millisecond temporal precision on the same 1,000 images. |
| [`nsd-eeg-alljoined`](nsd-eeg-alljoined/) | 2024 | scalp EEG | 8 | rich (NSD inherits) | Low-cost scalp EEG counterpart that closes NSD's modality triangle. |
| [`things-initiative`](things-initiative/) | 2023 | fMRI, MEG, EEG | 17 across modalities | rich | 1,854 object concepts; cross-modal benchmark; 4.7M similarity judgments. |
| [`nod-eeg`](nod-eeg/) | 2025 | MEG, EEG | 20+ | rich (THINGS inherits) | Large-scale paired MEG and EEG on naturalistic object images. |
| [`things-eeg2`](things-eeg2/) | 2022 | scalp EEG | 10 | rich (THINGS inherits) | Largest single-trial scalp-EEG object decoding benchmark. |
| [`bold5000`](bold5000/) | 2019 | 3T fMRI | 4 | moderate | Mixed COCO / SUN / ImageNet stimulus set; 3T accessibility makes it a Phase-1 Garden target. |
| [`coco`](coco/) | 2014 | image (stimulus source) | n/a | rich | Upstream "annotation source of truth" for NSD, BOLD5000, Algonauts. |
| [`glmsingle-paper`](glmsingle-paper/) | 2022 | fMRI methods | n/a (methods) | n/a | Reference single-trial estimation pipeline; required for stimulus-by-stimulus annotation analyses. |

## Naturalistic, video / film

Long-form audiovisual stimuli. Annotation surface is the largest of any naturalistic-stimulus class: shot boundaries, character identity, emotion, theory-of-mind events, dialogue, sound design.

| Slug | Year | Modalities | N | Density | AGI hook |
|------|------|-----------|---|---------|----------|
| [`studyforrest`](studyforrest/) | 2014 | 7T fMRI, audio | 20 | rich | Reference long-form deep-sampling movie dataset; ecosystem of community annotations. |
| [`studyforrest-eyegaze`](studyforrest-eyegaze/) | 2016 | 7T fMRI + eye tracking | 15 | rich | Eye-gaze as participant-derived annotation layer; pointer-architecture exemplar. |
| [`hbn-mri`](hbn-mri/) | 2017 | 3T fMRI, MRI, EEG, behaviour | 5,000+ | minimal | Largest paediatric naturalistic MRI biobank; Despicable Me + The Present. |
| [`hbn-eeg`](hbn-eeg/) | 2024 | high-density EEG | 3,000+ | rich (HED-tagged) | HED Generation 3 reference deployment on Despicable Me, The Present, Pixar shorts. |
| [`bang-ieeg-fmri`](bang-ieeg-fmri/) | 2022 | iEEG, 3T fMRI | 51 + 30 | moderate | Hitchcock 7-minute clip; flagship multimodal short-clip benchmark. |
| [`bang-multimodal`](bang-multimodal/) | 2024 | iEEG + single-unit + fMRI | 29 | rich | Single-neuron event cells; gold-standard event-boundary annotations. |
| [`naturalistic-neuroimaging-db`](naturalistic-neuroimaging-db/) | 2020 | 3T fMRI | 86 | minimal | 10 feature films; cross-film generalization benchmark. |
| [`courtois-neuromod`](courtois-neuromod/) | 2022 | 3T fMRI, eye tracking | 6 | minimal-moderate | Hundreds of hours per subject; Friends + 10 films + games; deepest naturalistic individual sampling. |
| [`sherlock-fmri`](sherlock-fmri/) | 2017 | 3T fMRI | 17 | moderate | BBC Sherlock 50-min clip; canonical event-segmentation benchmark. |
| [`inscapes`](inscapes/) | 2015 | 3T fMRI | 36 | minimal | Low-arousal abstract animation; ecologically richer than rest, narratively flat. |

## Naturalistic, audio / narrative

Spoken stories, podcasts, and audiobook stimuli. The audio counterpart to the static-image and video tracks. Annotations live at phoneme, word, sentence, narrative-event, and prosodic levels.

| Slug | Year | Modalities | N | Density | AGI hook |
|------|------|-----------|---|---------|----------|
| [`narratives-pieman`](narratives-pieman/) | 2021 | 3T fMRI, audio | 345 | rich | Largest open spoken-narrative corpus; 27 stories; HED-Lang sidecar template. |
| [`moth-radio-hour`](moth-radio-hour/) | 2016 | 3T fMRI, audio | 7 | rich | Canonical reference for continuous-language encoding; 2 hours of stories per subject. |
| [`little-prince-fmri`](little-prince-fmri/) | 2022 | 3T fMRI, audio | 49 | rich | Multilingual (English / Mandarin / French); cross-linguistic encoding. |
| [`natural-sounds-fmri`](natural-sounds-fmri/) | 2015 | 3T fMRI, audio | 20+ | moderate | 165-clip natural-sounds benchmark; auditory cortex semantic atlas. |

## Cognitive task batteries

The right end of the spectrum: structured paradigms with simple event vocabularies, large N, and high reproducibility. Annotation density is intrinsically lower (a handful of trial types per task) but HED Generation 3 sidecars are valuable community goods.

| Slug | Year | Modalities | N | Density | AGI hook |
|------|------|-----------|---|---------|----------|
| [`hcp-task`](hcp-task/) | 2013 | 3T / 7T fMRI | 1,200 | moderate | Reference adult cognitive battery (7 tasks). HED sidecar gap is a clear Garden contribution. |
| [`hcp-d-development`](hcp-d-development/) | 2018 | 3T fMRI | 1,300 | moderate | Developmental complement to HCP Young Adult; 4 tasks, ages 5 to 21. |
| [`abcd-task`](abcd-task/) | 2018 | 3T fMRI | 11,800 | moderate | Largest paediatric task fMRI study; MID, n-back, Stop-Signal; HED sidecars absent. |
| [`cam-can`](cam-can/) | 2014 | 3T fMRI, MEG | 700 | moderate | Lifespan cognitive battery; multimodal fusion test bed. |
| [`aomic`](aomic/) | 2021 | 3T fMRI | 1,500+ | moderate | Three deposits (PIOP1, PIOP2, ID1000); naturalistic-meets-task hybrid. |
| [`myconnectome`](myconnectome/) | 2015 | 3T fMRI, multi-omics | 1 | minimal | Single-subject deep-sampling proof of concept; 105 sessions. |

## Hybrid / mixed paradigms

Datasets that span naturalistic and structured task content, or combine resting state with task. Useful as bridges when comparing across the spectrum.

| Slug | Year | Modalities | N | Density | AGI hook |
|------|------|-----------|---|---------|----------|
| [`lemon-mpi`](lemon-mpi/) | 2019 | 3T fMRI + 62-channel EEG | 227 | minimal | EEG-fMRI fusion; lifespan; brief task plus resting. |
| [`dhcp`](dhcp/) | 2018 | 3T fMRI, MRI, DTI | 1,500+ | none-minimal | Largest open neonatal connectome; mostly resting state but rich follow-up phenotyping. |
| [`deap`](deap/) | 2012 | 32-channel EEG + physiology | 32 | moderate | Music-video emotion-elicitation benchmark for affective computing / brain-computer interface. |
| [`seed`](seed/) | 2015 | 62-channel EEG | 15 | moderate | Film-clip emotion classification benchmark; SEED-IV / V / VIG extensions. |

## Single-stimulus benchmark sets

Localizers and small canonical paradigms that anchor cohort-level analyses. Annotation density is intentionally minimal but every single one would benefit from a canonical Garden-hosted HED Gen-3 sidecar.

| Slug | Year | Modalities | N | Density | AGI hook |
|------|------|-----------|---|---------|----------|
| [`fedorenko-language-localizer`](fedorenko-language-localizer/) | 2010 | fMRI | 49 + thousands | minimal | Reference language localizer; multilingual variants, openly distributed materials. |
| [`pinel-localizer`](pinel-localizer/) | 2007 | fMRI | 81 | minimal | Multi-task 5-minute localizer; 10 sub-tasks; OpenNeuro reference cohort. |
| [`localizer-ds000114`](localizer-ds000114/) | 2017 | fMRI | 1,311 | minimal | Brainomics-Localizer mass deployment of Pinel; cross-cohort reliability anchor. |

## How to read this index

Read top to bottom: each section descends in stimulus richness and ascends in trial-level event simplicity. The same Hierarchical Event Descriptor (HED) Generation 3 schema covers every entry; only the density of distinct event types differs. AGI's task is to make sure the schema, the annotation contributions, and the cross-references propagate across this entire stack.
