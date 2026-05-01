# Strand A — Tools Index

One-line summary per entry. Sorted by category. 33 entries total.

## Annotation tools

- [elan](./elan/card.md) — Desktop tool for hierarchical, time-aligned annotations of audio and video, the de facto standard for naturalistic stimulus annotation in linguistics, ethology, and infant research.
- [praat](./praat/card.md) — Canonical desktop tool for phonetic analysis and time-aligned audio annotation, built around the TextGrid format and a built-in scripting language.
- [boris](./boris/card.md) — Free desktop application for time-aligned event coding of video and audio, widely used in animal behavior, child development, and naturalistic-stimulus research.
- [datavyu](./datavyu/card.md) — Open-source video and audio coding tool with a sheet-based interface, used heavily in developmental psychology and integrated with the Databrary repository.
- [label-studio](./label-studio/card.md) — Web-based labeling platform supporting text, image, audio, video, and time-series annotation, with a pluggable Machine Learning backend for pre-annotation.

## Analysis pipelines

- [eeglab](./eeglab/card.md) — MATLAB toolbox with a graphical interface for processing single-trial EEG data, the de facto plugin host for most EEG analysis innovations.
- [mne-python](./mne-python/card.md) — Python implementation of the MNE software suite for processing MEG, EEG, and intracranial EEG with full preprocessing, source localization, and decoding.
- [fmriprep](./fmriprep/card.md) — Containerized BIDS App that preprocesses functional MRI data with a robust automated pipeline combining ANTs, FSL, and FreeSurfer.
- [mriqc](./mriqc/card.md) — Tool that extracts MRI quality metrics, fits an accept/exclude classifier, and produces per-subject HTML reports as a BIDS App.
- [glmsingle](./glmsingle/card.md) — MATLAB and Python toolbox that improves single-trial fMRI BOLD response estimates via per-voxel HRF selection, noise regressors, and ridge regression.
- [unfold](./unfold/card.md) — EEGLAB-compatible MATLAB toolbox for regression ERPs, linear deconvolution to correct overlap, and Generalized Additive Model covariates.
- [mtrf-toolbox](./mtrf-toolbox/card.md) — MATLAB package that fits regularized linear regression models mapping continuous sensory stimuli to neural responses with built-in regularization tuning.

## AI-assisted annotators

- [clip](./clip/card.md) — Contrastive Language-Image Pre-training model that learns a shared image-text embedding space supporting zero-shot transfer to diverse vision tasks via natural language prompts.
- [whisper](./whisper/card.md) — Multilingual, multitask Automatic Speech Recognition model trained on 680,000 hours of weakly supervised audio, achieving strong zero-shot performance without fine-tuning.
- [grounding-dino](./grounding-dino/card.md) — Open-set object detector that marries DINO with grounded language pre-training to detect arbitrary objects from natural-language prompts.
- [llava-video](./llava-video/card.md) — Video Large Multimodal Model trained on 178k synthetic instruction-following clips with detailed captions, open-ended QA, and multiple-choice QA.
- [crowdagent](./crowdagent/card.md) — Multi-agent annotation system that coordinates LLMs, Small Language Models, and human experts under task-assignment, quality-assurance, and budget-tracking agents.
- [pliers](./pliers/card.md) — Python framework that wraps heterogeneous feature extractors behind a unified Stim plus Extractor abstraction for multimodal time-aligned feature pipelines.
- [pyscenedetect](./pyscenedetect/card.md) — Python and CLI tool for automatic shot-boundary detection in video with multiple detector strategies and direct FFmpeg integration.
- [huggingface](./huggingface/card.md) — Transformers library and Hugging Face Hub distribute thousands of pretrained Transformer models behind a unified API for text, vision, audio, and multimodal tasks.

## Infrastructure platforms

- [openneuro](./openneuro/card.md) — Open neuroscience data archive built on BIDS, hosting human neuroimaging datasets under a Creative Commons Zero default license.
- [nemar](./nemar/card.md) — Web gateway exposing BIDS-formatted EEG, MEG, and intracranial EEG datasets with quality reports, HED tag search, and a direct path to high-performance computing.
- [datalad](./datalad/card.md) — Layer on Git plus git-annex for distributed, modular, provenance-tracked management of code, data, and computational environments.
- [neuroscout](./neuroscout/card.md) — End-to-end web platform for analyzing naturalistic fMRI datasets, automatically annotating stimuli with Pliers features and executing reproducible BIDS pipelines.
- [dandi](./dandi/card.md) — BRAIN Initiative archive for cellular neurophysiology data, hosting Neurodata Without Borders and BIDS datasets with versioning and a hosted JupyterHub.
- [bids-validator](./bids-validator/card.md) — Reference implementation that checks dataset conformance to the BIDS specification, available as Node.js CLI, web validator, and Python wrapper.

## Standards and specifications

- [bids-spec](./bids-spec/card.md) — Community-driven specification for organizing, naming, and describing neuroimaging datasets using plain text formats and lightweight folder conventions.
- [bep044-stim-bids](./bep044-stim-bids/card.md) — BIDS Extension Proposal that defines how to package stimulus repositories with their annotations as standalone BIDS-compliant datasets.
- [hed-spec](./hed-spec/card.md) — Hierarchical Event Descriptors framework for annotating time-series neuroscience events with formally defined hierarchical tags and library-schema extensions.
- [hed-score](./hed-score/card.md) — HED library schema encoding the SCORE clinical EEG vocabulary in a machine-readable form endorsed by ILAE and IFCN.
- [fair-principles](./fair-principles/card.md) — Findable, Accessible, Interoperable, Reusable Guiding Principles articulating fifteen criteria for scholarly data management for both humans and machines.
- [cobidas](./cobidas/card.md) — OHBM Committee on Best Practices in Data Analysis and Sharing checklist for transparent reporting and rigorous methodology in fMRI studies.
- [nwb](./nwb/card.md) — Neurodata Without Borders, an extensible data language for neurophysiology serialized in HDF5 or Zarr that unifies cellular ephys, optical imaging, and behavior.
