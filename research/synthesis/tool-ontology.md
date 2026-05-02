# Tool Ontology

A hierarchical map of the 33 tool, platform, and standard entries collected in [`research/collection/tools/`](../collection/tools/). The map sorts entries into five layers running from the closest-to-the-stimulus surface (manual annotators) up through the closest-to-the-community surface (specifications). Per-layer tables record maturity, integration with the Brain Imaging Data Structure (BIDS), integration with Hierarchical Event Descriptors (HED), license, and the calibrated `agi_relevance` from the entry's paper-card.

Abbreviations: vision-language model (VLM), large language model (LLM), small language model (SLM), automatic speech recognition (ASR), magnetoencephalography (MEG), electroencephalography (EEG), intracranial EEG (iEEG), magnetic resonance imaging (MRI), functional MRI (fMRI), application programming interface (API).

## Legend for the integration columns

- **Maturity**: `proven` (in routine production use across multiple labs for ≥5 years), `emerging` (active development, growing user base, last 2 to 5 years), `nascent` (recent release, narrow adoption, last 2 years).
- **BIDS integration**: `native` (the entry is BIDS or implements a BIDS app), `aware` (reads or writes BIDS via official adapters), `partial` (community plugin or third-party adapter), `none-yet` (no BIDS path).
- **HED integration**: `native` (the entry is HED or a HED library schema), `aware` (validates or emits HED tags directly), `partial` (downstream tooling or plugin handles HED), `none-yet` (no HED path).
- **AGI relevance**: copied verbatim from each card's front-matter; calibration anchors are documented in [`../collection/_schema/paper-card.md`](../collection/_schema/paper-card.md).

## Layer 1, Annotation surface (manual and semi-automatic)

Tools the annotator drives directly. They predate BIDS and HED, so the integration story is always "AGI builds the bridge", as the [BORIS card](../collection/tools/boris/card.md), [ELAN card](../collection/tools/elan/card.md), and [Datavyu card](../collection/tools/datavyu/card.md) make explicit.

| Entry | Role | Maturity | BIDS | HED | License | AGI relevance |
|---|---|---|---|---|---|---|
| [`elan`](../collection/tools/elan/card.md) | Hierarchical, time-aligned audio and video annotation, the de facto standard in linguistics, ethology, and infant cognition | proven | none-yet | none-yet | GPL-3.0 | medium |
| [`praat`](../collection/tools/praat/card.md) | Phonetic analysis and time-aligned audio annotation, built around the TextGrid format | proven | none-yet | none-yet | GPL-3.0 | low |
| [`boris`](../collection/tools/boris/card.md) | Time-aligned event coding of video and audio, widely used in animal behavior and naturalistic research | proven | none-yet | none-yet | GPL-3.0 | low |
| [`datavyu`](../collection/tools/datavyu/card.md) | Sheet-based video and audio coding, integrated with the Databrary repository | proven | none-yet | none-yet | GPL-3.0 | low |
| [`label-studio`](../collection/tools/label-studio/card.md) | Web-based labeling platform with a pluggable machine-learning backend | proven | none-yet | none-yet | Apache-2.0 | low |

Layer 1 synthesis: the manual annotation tools are mature, GPL-licensed, and tightly bound to specific domain communities (linguistics, ethology, developmental psychology). None reach out to BIDS or HED on their own. AGI's job at this layer is bidirectional adapters: ingest ELAN `.eaf`, Praat TextGrid, BORIS CSV, and Datavyu spreadsheet exports into Stim-BIDS `events.tsv` with HED tag mapping, and round-trip back so the contributor never leaves their preferred interface. Label Studio is the natural human-in-the-loop review front-end for AI-generated annotations from Layer 2.

## Layer 2, AI-assisted annotation

Foundation models and orchestration libraries that produce stimulus features at scale. Per the [CLIP card](../collection/tools/clip/card.md), [Whisper card](../collection/tools/whisper/card.md), [Grounding-DINO card](../collection/tools/grounding-dino/card.md), [LLaVA-Video card](../collection/tools/llava-video/card.md), [Pliers card](../collection/tools/pliers/card.md), and [CrowdAgent card](../collection/tools/crowdagent/card.md), none of these write `events.tsv` natively; they emit model-specific JSON or tensors.

| Entry | Role | Maturity | BIDS | HED | License | AGI relevance |
|---|---|---|---|---|---|---|
| [`clip`](../collection/tools/clip/card.md) | Image-text contrastive embedding for zero-shot tagging | proven | none-yet | none-yet | MIT (code), custom checkpoint terms | medium |
| [`whisper`](../collection/tools/whisper/card.md) | Multilingual ASR with word-level alignment | proven | none-yet | none-yet | MIT | medium |
| [`grounding-dino`](../collection/tools/grounding-dino/card.md) | Open-set object detection from natural-language prompts | emerging | none-yet | none-yet | Apache-2.0 | medium |
| [`llava-video`](../collection/tools/llava-video/card.md) | Video LLM for captioning and event description | nascent | none-yet | none-yet | Apache-2.0 | medium |
| [`crowdagent`](../collection/tools/crowdagent/card.md) | Multi-agent orchestration of LLMs, SLMs, and human raters with quality-assurance and budget tracking | nascent | none-yet | none-yet | MIT | high |
| [`pliers`](../collection/tools/pliers/card.md) | Multimodal feature-extraction orchestration via a unified Stim plus Extractor abstraction | proven | aware | none-yet | BSD-3-Clause | high |
| [`pyscenedetect`](../collection/tools/pyscenedetect/card.md) | Shot-boundary detection in video | proven | none-yet | none-yet | BSD-3-Clause | medium |
| [`huggingface`](../collection/tools/huggingface/card.md) | Pretrained-model hub and Transformers library | proven | none-yet | none-yet | Apache-2.0 (library), per-model | medium |

Layer 2 synthesis: AI annotators are an explosion of capability with no annotation-format discipline. Pliers is the closest existing orchestration layer with BIDS awareness, and Neuroscout demonstrates that a Pliers feature graph can drive BIDS-conformant analyses end-to-end. The white paper's "multi-agent AI assistants accelerate annotation through automated tools" sentence is operationally vacuous without an adapter layer that converts CLIP scene embeddings, Whisper transcripts, Grounding-DINO bounding boxes, and LLaVA-Video captions into HED-tagged `events.tsv`. AGI defines that layer; CrowdAgent provides the multi-source coordination pattern.

## Layer 3, Analysis pipelines and encoding-model libraries

Where annotated data becomes neural inferences. These tools are mature and modality-specific, with stronger BIDS integration than Layer 1 or 2 because BIDS Apps were designed against them.

| Entry | Role | Maturity | BIDS | HED | License | AGI relevance |
|---|---|---|---|---|---|---|
| [`eeglab`](../collection/tools/eeglab/card.md) | MATLAB EEG processing with the largest plugin ecosystem in the field, including HED tagging via the HEDTools plugin | proven | aware (BIDS importer plugin) | aware (HEDTools plugin) | GPL-2.0-or-later | high |
| [`mne-python`](../collection/tools/mne-python/card.md) | Python suite for MEG, EEG, iEEG processing | proven | aware (mne-bids) | partial (via mne-bids and HED libraries) | BSD-3-Clause | high |
| [`fmriprep`](../collection/tools/fmriprep/card.md) | Containerized BIDS App for fMRI preprocessing | proven | native (BIDS App) | none-yet | Apache-2.0 | medium |
| [`mriqc`](../collection/tools/mriqc/card.md) | BIDS App for MRI quality metrics | proven | native (BIDS App) | none-yet | Apache-2.0 | medium |
| [`glmsingle`](../collection/tools/glmsingle/card.md) | Single-trial fMRI BOLD response estimation | proven | aware | none-yet | CC-BY-4.0 | high |
| [`unfold`](../collection/tools/unfold/card.md) | Regression-ERP and overlap-correction toolbox | emerging | partial (via EEGLAB BIDS importer) | partial (via EEGLAB) | GPL-3.0 | high |
| [`mtrf-toolbox`](../collection/tools/mtrf-toolbox/card.md) | Temporal response function fitting for continuous stimuli | proven | none-yet | none-yet | BSD-3-Clause | high |

Layer 3 synthesis: BIDS coverage is strong on the imaging side (fMRIPrep, MRIQC are BIDS Apps; mne-bids has matured) but uneven on the electrophysiology side (EEGLAB, MNE-Python, Unfold all reach BIDS through importers, not natively). HED coverage is partial throughout, concentrated in the EEGLAB ecosystem via HEDTools and SCORE-aware extensions. The toolboxes most central to the encoding-model paradigm of the [Strand C corpus](../collection/science/INDEX.md) (GLMsingle, mTRF-Toolbox) sit one step away from AGI annotations: they consume per-trial event tables but do not validate HED tags. AGI's leverage here is to define the canonical data flow `events.tsv` with HED tags to encoder predictors, and to bundle that flow as Pliers extractors plus EEGLAB plugins so adoption is friction-free.

## Layer 4, Infrastructure platforms

Where datasets, code, and provenance live. AGI does not duplicate any of these; it interconnects them.

| Entry | Role | Maturity | BIDS | HED | License | AGI relevance |
|---|---|---|---|---|---|---|
| [`openneuro`](../collection/tools/openneuro/card.md) | Public BIDS archive with Creative Commons Zero (CC0) defaults | proven | native | aware (validator integration) | CC0 (datasets), MIT (code) | high |
| [`nemar`](../collection/tools/nemar/card.md) | Web gateway for BIDS-formatted EEG, MEG, iEEG with quality reports, HED-tag search, and a high-performance computing path | proven | native | aware (HED-tag search) | CC-BY-NC | high |
| [`datalad`](../collection/tools/datalad/card.md) | Distributed, modular, provenance-tracked data-and-code management on Git plus git-annex | proven | aware | none-yet | MIT | high |
| [`neuroscout`](../collection/tools/neuroscout/card.md) | End-to-end web platform that auto-annotates naturalistic fMRI stimuli with Pliers and runs BIDS pipelines | emerging | native | partial (via Pliers and BIDS) | MIT (code), CC-BY (data) | high |
| [`dandi`](../collection/tools/dandi/card.md) | BRAIN Initiative archive for cellular neurophysiology, hosting Neurodata Without Borders (NWB) and BIDS datasets | proven | aware | none-yet | BSD-3-Clause | medium |
| [`bids-validator`](../collection/tools/bids-validator/card.md) | Reference implementation that checks dataset conformance to the BIDS specification | proven | native | aware (HED-validator integration) | MIT | high |

Layer 4 synthesis: the platform layer is BIDS-saturated and HED-aware in the EEG-MEG-iEEG quadrant (NEMAR, BIDS-Validator integration with the HED-validator). NeuroScout is the closest precedent for AGI's analysis side, restricted to fMRI and to Pliers as the only annotator. DataLad provides the cross-cutting provenance substrate that AGI's "branches as annotation layers" Wikipedia-like model (per [`VISION.md`](../../VISION.md)) leans on whether or not it appears in the white paper. AGI's role at this layer is to publish stimulus-anchored repositories that NEMAR, OpenNeuro, NeuroScout, and DANDI can index by reference rather than copy.

## Layer 5, Standards and specifications

The semantic and structural substrate. Every entry here is a normative reference; the question is only which one(s) AGI inherits.

| Entry | Role | Maturity | BIDS | HED | License | AGI relevance |
|---|---|---|---|---|---|---|
| [`bids-spec`](../collection/tools/bids-spec/card.md) | Community specification for organizing, naming, and describing neuroimaging datasets | proven | native | aware (validator integration) | CC-BY-4.0 | high |
| [`bep044-stim-bids`](../collection/tools/bep044-stim-bids/card.md) | BIDS Extension Proposal that defines stimulus-repository packaging with annotations as standalone BIDS datasets | emerging | native | aware | CC-BY-4.0 | high |
| [`hed-spec`](../collection/tools/hed-spec/card.md) | Hierarchical Event Descriptors framework with library-schema extensions | proven | aware | native | CC-BY-4.0 (schema), permissive (tools) | high |
| [`hed-score`](../collection/tools/hed-score/card.md) | HED library schema encoding the SCORE clinical EEG vocabulary, endorsed by the International League Against Epilepsy (ILAE) and the International Federation of Clinical Neurophysiology (IFCN) | emerging | aware | native | CC-BY-4.0 | high |
| [`fair-principles`](../collection/tools/fair-principles/card.md) | Findable, Accessible, Interoperable, Reusable principles | proven | none-yet | none-yet | CC-BY-4.0 | high |
| [`cobidas`](../collection/tools/cobidas/card.md) | OHBM Committee on Best Practices in Data Analysis and Sharing checklist | proven | none-yet | none-yet | CC-BY (checklist), publisher-paywall (paper) | low |
| [`nwb`](../collection/tools/nwb/card.md) | Neurodata Without Borders, an extensible neurophysiology data language serialized in HDF5 or Zarr | proven | aware (BIDS-NWB bridges) | none-yet | BSD-3-Clause | medium |

Layer 5 synthesis: AGI's substrate is unambiguous: BIDS for organization (via Stim-BIDS, BEP044), HED for semantics (via the core schema and SCORE-style libraries), FAIR for governance principles. NWB is a sibling rather than a parent for AGI because AGI's primary medium is stimulus annotation, not raw signal. COBIDAS is reference-only for now, useful in the rigor-and-reproducibility wing of any future grant or governance document but not on the critical path.

## Cross-layer synthesis

Three observations bind the layers together:

1. **BIDS is the substrate; HED is the semantics; AGI is the choreographer.** BIDS appears as a `native` or `aware` integration in 14 of 33 entries, concentrated in Layers 4 and 5 and reaching Layer 3 via importers. HED appears `native` only in the standards layer and `aware` in three Layer-3 entries (EEGLAB, mne-bids, MNE-Python via plugins) plus three Layer-4 platforms (NEMAR, BIDS-Validator, NeuroScout). The AI-assisted layer (Layer 2) and the manual annotation layer (Layer 1) are HED-blind. AGI's distinctive contribution is the missing middleware that makes Layer 1 and Layer 2 emit HED-tagged Stim-BIDS-conformant `events.tsv`.

2. **The maturity gradient runs the wrong way for AGI's roadmap.** Manual annotators (Layer 1) are the most mature and the least HED-aware; AI annotators (Layer 2) are the least mature and the most format-agnostic. AGI must invest disproportionately in the youngest tools to set the format expectations early. CrowdAgent is the canonical pattern.

3. **Licensing favors aggregation.** Twenty-six of 33 entries carry permissive licenses (MIT, BSD, Apache, CC-BY, CC0). Six entries are copyleft GPL (ELAN, Praat, BORIS, Datavyu, EEGLAB, Unfold); this requires derivative works that link or modify the source to be released under the same terms but does not impede AGI's mission because AGI consumes their file-format outputs rather than redistributing modified binaries. NEMAR is CC-BY-NC, which constrains downstream commercial reuse but does not impede non-commercial research re-use. CLIP and HuggingFace model checkpoints carry per-model terms requiring per-stimulus diligence; AGI's federation model handles this gracefully because annotations can be permissively licensed even when stimulus-specific weights cannot.

## Coverage check

All 33 tool entries listed in [`../collection/tools/INDEX.md`](../collection/tools/INDEX.md) are placed:

- Layer 1 (5): elan, praat, boris, datavyu, label-studio.
- Layer 2 (8): clip, whisper, grounding-dino, llava-video, crowdagent, pliers, pyscenedetect, huggingface.
- Layer 3 (7): eeglab, mne-python, fmriprep, mriqc, glmsingle, unfold, mtrf-toolbox.
- Layer 4 (6): openneuro, nemar, datalad, neuroscout, dandi, bids-validator.
- Layer 5 (7): bids-spec, bep044-stim-bids, hed-spec, hed-score, fair-principles, cobidas, nwb.

Total: 33.
