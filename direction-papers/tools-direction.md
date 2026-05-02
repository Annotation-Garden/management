# Tools Direction, FAIR Services Survey and the AGI Adapter Layer

A focused mini lit review on the tools strand of the Annotation Garden Initiative (AGI). Surveys the existing Findable, Accessible, Interoperable, Reusable (FAIR) services in the neuroimaging annotation lifecycle, names what AGI does NOT need to build because the substrate already exists, and scopes AGI's distinctive contribution: the missing middleware that turns AI-assisted and manual annotation outputs into Hierarchical Event Descriptors (HED) tagged Brain Imaging Data Structure (BIDS) Stim-BIDS `events.tsv`. Addresses [issue #2](https://github.com/Annotation-Garden/management/issues/2).

Abbreviations: Findable, Accessible, Interoperable, Reusable (FAIR), Brain Imaging Data Structure (BIDS), Hierarchical Event Descriptors (HED), Natural Scenes Dataset (NSD), Healthy Brain Network (HBN), magnetoencephalography (MEG), electroencephalography (EEG), intracranial EEG (iEEG), functional magnetic resonance imaging (fMRI), large language model (LLM), small language model (SLM), vision-language model (VLM), automatic speech recognition (ASR), graphical user interface (GUI), continuous integration (CI), command-line interface (CLI), application programming interface (API), brain-computer interface (BCI).

## 1. Why a survey, and what to look for

[Issue #2](https://github.com/Annotation-Garden/management/issues/2) frames the goal as finding and linking the FAIR services that already exist for creating rich annotation layers and re-analyzing neuroimaging data. The Phase 1 corpus collected 33 such entries; the Phase 2 [`tool-ontology`](../research/synthesis/tool-ontology.md) sorted them into five layers from manual annotation surface (Layer 1) through AI-assisted annotation (Layer 2) up through analysis pipelines (Layer 3), infrastructure platforms (Layer 4), and standards (Layer 5).

This direction paper takes that ontology and turns it into a survey of which existing services AGI inherits. The discipline is the same as in software composition: do not rebuild what exists; do build the connectors that turn separate pieces into a working pipeline. The first half of the paper is the inheritance accounting. The second half names the missing middleware. The third half sketches the build order.

## 2. What AGI inherits, by layer

### 2.1 Layer 5, standards and specifications

Two standards anchor the entire stack. [`bids-spec`](../research/collection/tools/bids-spec/card.md) defines the dataset organization; [`bep044-stim-bids`](../research/collection/tools/bep044-stim-bids/card.md) is the BIDS Extension Proposal that defines stimulus-repository packaging and is exactly the AGI substrate. [`hed-spec`](../research/collection/tools/hed-spec/card.md) defines the controlled annotation vocabulary, with library-schema extensions including [`hed-score`](../research/collection/tools/hed-score/card.md) for clinical EEG. [`fair-principles`](../research/collection/tools/fair-principles/card.md) defines the governance rubric. [`nwb`](../research/collection/tools/nwb/card.md) is a sibling format for raw neurophysiology; [`cobidas`](../research/collection/tools/cobidas/card.md) is a reporting checklist. [`bids-validator`](../research/collection/tools/bids-validator/card.md) is the reference compliance tool that ties the standards to runtime checks.

AGI inherits all five. None requires modification or extension; AGI's repositories ship as conformant BIDS plus Stim-BIDS plus HED-tagged datasets.

### 2.2 Layer 4, infrastructure platforms

[`openneuro`](../research/collection/tools/openneuro/card.md) is the canonical public BIDS archive with Creative Commons Zero defaults; [`nemar`](../research/collection/tools/nemar/card.md) is the EEG, MEG, and iEEG gateway with HED-tag search and a high-performance computing path; [`datalad`](../research/collection/tools/datalad/card.md) provides the distributed, modular, provenance-tracked Git plus git-annex substrate; [`dandi`](../research/collection/tools/dandi/card.md) is the BRAIN Initiative archive for cellular neurophysiology hosting NWB and BIDS datasets; [`neuroscout`](../research/collection/tools/neuroscout/card.md) is the end-to-end web platform that auto-annotates naturalistic fMRI stimuli with [`pliers`](../research/collection/tools/pliers/card.md) and runs BIDS pipelines.

AGI does not duplicate any of these. The Garden architecture is hub-and-spoke: each stimulus becomes a versioned repository (the spoke) that NEMAR, OpenNeuro, NeuroScout, and DANDI can index by reference. DataLad provides the cross-cutting provenance substrate that the white paper's branches-as-layers model already leans on whether or not it appears in the white paper text. NeuroScout in particular is the closest existing precedent for AGI's analysis side; the [`neuroscout` card](../research/collection/tools/neuroscout/card.md) makes the relationship explicit, calling out a NeuroScout-AGI bridge in which AGI annotations are consumed as NeuroScout predictors as the obvious near-term collaboration.

### 2.3 Layer 3, analysis pipelines and encoding-model libraries

[`eeglab`](../research/collection/tools/eeglab/card.md) is the MATLAB EEG analysis hub with the largest plugin ecosystem in the field, including HED tagging via the HEDTools plugin; [`mne-python`](../research/collection/tools/mne-python/card.md) is the Python suite for MEG, EEG, and iEEG with BIDS support via `mne-bids`; [`fmriprep`](../research/collection/tools/fmriprep/card.md) and [`mriqc`](../research/collection/tools/mriqc/card.md) are the canonical BIDS Apps for fMRI preprocessing and quality control; [`glmsingle`](../research/collection/tools/glmsingle/card.md) handles single-trial fMRI estimation; [`unfold`](../research/collection/tools/unfold/card.md) extends EEGLAB with regression-ERP and overlap correction; [`mtrf-toolbox`](../research/collection/tools/mtrf-toolbox/card.md) fits temporal response functions for continuous-stimulus encoding.

AGI inherits all of these as the analysis endpoints for the data its repositories anchor. A successful AGI annotation flow ends with a HED-tagged events table that EEGLAB, MNE-Python, fMRIPrep, GLMsingle, Unfold, or mTRF-Toolbox consumes without any AGI-specific code. The integration target is the existing BIDS importer in each tool, plus the HED-aware extensions where they exist.

### 2.4 Layer 2, AI-assisted annotation

[`clip`](../research/collection/tools/clip/card.md), [`whisper`](../research/collection/tools/whisper/card.md), [`grounding-dino`](../research/collection/tools/grounding-dino/card.md), [`llava-video`](../research/collection/tools/llava-video/card.md), [`pyscenedetect`](../research/collection/tools/pyscenedetect/card.md), [`huggingface`](../research/collection/tools/huggingface/card.md), and [`pliers`](../research/collection/tools/pliers/card.md) are the AI annotators. [`crowdagent`](../research/collection/tools/crowdagent/card.md) is the multi-agent orchestration layer that coordinates LLMs, SLMs, and human raters under a Quality Assurance Agent and a Scheduling Agent.

AGI inherits the model capabilities and the orchestration patterns. It does not inherit the output formats. None of these tools writes HED-tagged Stim-BIDS `events.tsv` natively. CLIP emits embeddings. Whisper emits transcripts and word-level timestamps in JSON or VTT. Grounding-DINO emits bounding boxes. LLaVA-Video emits free-form captions or multiple-choice answers. PySceneDetect emits frame indices. Pliers wraps the heterogeneous outputs behind a unified Stim plus Extractor abstraction whose ExtractorResult is a pandas DataFrame; standalone Pliers does not produce BIDS-conformant `events.tsv` and does not emit HED tags. Its BIDS path is realized through NeuroScout, which composes Pliers feature graphs into BIDS-execution pipelines. CrowdAgent coordinates sources but is annotation-format agnostic.

### 2.5 Layer 1, manual annotation

[`elan`](../research/collection/tools/elan/card.md) is the de facto standard for hierarchical, time-aligned audio and video annotation in linguistics and infant cognition; [`praat`](../research/collection/tools/praat/card.md) is the canonical phonetic annotation tool with the TextGrid format; [`boris`](../research/collection/tools/boris/card.md) is the de facto event-coding tool in animal behavior and ethology; [`datavyu`](../research/collection/tools/datavyu/card.md) is integrated with the Databrary repository for developmental video coding; [`label-studio`](../research/collection/tools/label-studio/card.md) is the web-based labeling platform with a pluggable machine-learning backend.

These tools predate BIDS and HED by a decade or more and are unlikely to gain native BIDS or HED support through their own roadmaps. Their formats (`.eaf`, TextGrid, BORIS CSV, Datavyu spreadsheet, Label Studio XML) are stable, well-documented, and widely supported in the communities that produce naturalistic-stimulus annotations. AGI inherits the existing investment those communities have made in these tools; the cost of forcing labs to migrate to a new annotation interface is high enough that AGI must instead come to where the annotators already work.

## 3. The missing middleware

The inheritance accounting names the gaps. Three concrete adapter layers do not exist today:

### 3.1 Manual-tool to Stim-BIDS adapter (Layer 1 to standards)

Every Layer 1 tool writes a stable, well-documented format. AGI must implement bidirectional adapters that ingest those formats into Stim-BIDS `events.tsv` with HED tag mapping, and round-trip back so contributors can keep working in their preferred interface. The contracts are concrete:

- ELAN `.eaf` to `events.tsv`: tier hierarchies become nested HED tags or sidecar JSON. The [`elan` card](../research/collection/tools/elan/card.md) names this adapter as a precondition for capturing the existing investment of linguistics and infant-cognition labs.
- Praat TextGrid to `events.tsv`: phonemes, words, prosody become separate annotation types. Whisper plus Praat is a natural pairing in which Whisper produces the initial transcription and Praat annotators refine it; the [`praat` card](../research/collection/tools/praat/card.md) documents the round-trip requirement.
- BORIS CSV or `.eaf` export to `events.tsv` with HED tag mapping. Inter-rater reliability matters because AGI's quality story depends on agreement metrics.
- Datavyu spreadsheet to `events.tsv` with column mapping. Cooperation with Databrary's managed-access model is required when consented child videos cannot be redistributed.
- Label Studio XML to `events.tsv`. Label Studio is also the most plausible front-end for AGI's manual review of AI-generated annotations.

### 3.2 AI-annotator to Stim-BIDS adapter (Layer 2 to standards)

The harder case. CLIP scene embeddings, Whisper word timings, Grounding-DINO bounding boxes, LLaVA-Video captions, and PySceneDetect cuts are all useful annotations, but converting them into HED-tagged events requires per-tool semantic glue. The AGI commitment is to publish that glue as a versioned adapter library:

- Whisper transcripts plus alignments to `events.tsv` with HED-LANG tags for words and prosodic units.
- CLIP scene embeddings with a similarity-based scene-tag emitter that maps each embedding to one or more HED tags.
- Grounding-DINO bounding boxes to per-frame object events with HED object-category tags.
- LLaVA-Video captions to event-segmented temporal annotations with HED narrative-event tags.
- PySceneDetect cuts to scene-boundary events with HED scene-boundary tags.

Pliers is the natural orchestration substrate for the entire adapter stack because it already wraps these models behind a Stim plus Extractor abstraction. AGI's contribution is to extend Pliers extractors with HED tag emission, then publish the extended extractor catalog as a versioned package.

### 3.3 Multi-source quality control (CrowdAgent pattern)

When ELAN-coded annotations from a linguistics lab, Whisper-derived transcripts from an automated run, and human rater corrections from a Label Studio deployment all coexist for the same stimulus, AGI must compute and surface inter-source agreement. CrowdAgent provides the architectural pattern: a Quality Assurance Agent computes inter-annotator agreement against a HED-tagged golden set, a Scheduling Agent routes hard frames to humans while easy frames go to a VLM, and a Cost Agent tracks budget and credit allocation. AGI implements this as a CI workflow in the stimulus repository, with public agreement metrics per branch.

## 4. The composition argument

The middleware described above is small in code volume but large in coordination. Each adapter is a few hundred lines plus a HED tag-mapping table. The expensive part is the standardization across tools: agreeing on which Hierarchical Event Descriptors map to ELAN tier "speaker", agreeing on the canonical word-level alignment format, agreeing on the bounding-box-to-event lossy reduction. The Phase 2 [`tool-ontology`](../research/synthesis/tool-ontology.md) shows that 14 of 33 entries already integrate with BIDS at the `native` or `aware` level and that HED appears in the integration column for 6 entries; the missing middleware lives almost entirely in the BIDS column for Layer 1 and Layer 2 entries.

AGI does not own any of the upstream tools or any of the downstream platforms. It owns the contract between them. The contract is what makes a community-versioned annotation layer possible at all, because without the contract every annotation effort produces a per-paper artifact and the layered branches-as-perspectives model in [`VISION.md`](../VISION.md) cannot operate.

## 5. Build order

The middleware ships in three waves, each driven by an obvious near-term application:

**Wave 1, demonstrate the round-trip on Forrest Gump**. ELAN to Stim-BIDS to ELAN. The studyforrest community has the largest existing investment in ELAN-coded annotations of any AGI flagship; round-tripping their annotations into a versioned repository without losing fidelity is the existence proof. Pair with Whisper to seed dialogue transcripts and Praat for phoneme refinement. Closes the Layer 1 adapter gap concretely on a single repository.

**Wave 2, automate the AI-annotator stack on NSD**. Pliers extractors with HED emission, run on the NSD images, deposited as a versioned annotation branch in a stimulus repository. Coordinated with the ANNOTATE R01 Aim 2 work, where HEDit produces the higher-richness branches and AGI distributes them. Closes the Layer 2 adapter gap.

**Wave 3, multi-source quality control on HBN movies**. Label Studio as the human-review front-end, Whisper plus LLaVA-Video for the AI baseline, CrowdAgent-pattern coordination, public agreement metrics in the repository CI. The HBN-EEG corpus is the existence proof that HED Generation 3 sidecars work at scale; HBN movies extend the annotation-richness side. Closes the multi-source quality-control gap.

Each wave is scoped so that a single milestone PR delivers the adapter, the worked example, and the documentation for the next adapter to reuse the pattern.

## 6. What this paper is not

It is not a tooling design document; the per-adapter implementation specifications belong in a Phase 4 technical-spec document under `tooling/`. It is also not a competitive analysis of the FAIR neuroscience commons; the goal is composition, not displacement. NeuroScout already does the analysis side for fMRI naturalistic-stimulus encoding; OpenNeuro already does the dataset archive; DataLad already does provenance. AGI is the contract layer that lets them work together on a community-versioned annotation surface.

## References

Citations resolve to BibTeX keys in [`../research/collection/tools/tools.bib`](../research/collection/tools/tools.bib). Direct paper-card links are in the prose above; the keys here are for downstream manuscript export.

Standards (Layer 5):
- `bids-spec`, [`bids-spec`](../research/collection/tools/bids-spec/card.md)
- `bep044-stim-bids`, [`bep044-stim-bids`](../research/collection/tools/bep044-stim-bids/card.md)
- `hed-spec`, [`hed-spec`](../research/collection/tools/hed-spec/card.md)
- `hed-score`, [`hed-score`](../research/collection/tools/hed-score/card.md)
- `fair-principles`, [`fair-principles`](../research/collection/tools/fair-principles/card.md)
- `cobidas`, [`cobidas`](../research/collection/tools/cobidas/card.md)
- `nwb`, [`nwb`](../research/collection/tools/nwb/card.md)

Infrastructure platforms (Layer 4):
- `openneuro2021`, [`openneuro`](../research/collection/tools/openneuro/card.md)
- `nemar`, [`nemar`](../research/collection/tools/nemar/card.md)
- `datalad`, [`datalad`](../research/collection/tools/datalad/card.md)
- `neuroscout2022`, [`neuroscout`](../research/collection/tools/neuroscout/card.md)
- `dandi`, [`dandi`](../research/collection/tools/dandi/card.md)
- `bids-validator`, [`bids-validator`](../research/collection/tools/bids-validator/card.md)

Analysis pipelines (Layer 3):
- `delorme2004eeglab`, [`eeglab`](../research/collection/tools/eeglab/card.md)
- `gramfort2013mne`, [`mne-python`](../research/collection/tools/mne-python/card.md)
- `esteban2019fmriprep`, [`fmriprep`](../research/collection/tools/fmriprep/card.md)
- `esteban2017mriqc`, [`mriqc`](../research/collection/tools/mriqc/card.md)
- `prince2022glmsingle`, [`glmsingle`](../research/collection/tools/glmsingle/card.md)
- `ehinger2019unfold`, [`unfold`](../research/collection/tools/unfold/card.md)
- `crosse2016mtrf`, [`mtrf-toolbox`](../research/collection/tools/mtrf-toolbox/card.md)

AI-assisted annotation (Layer 2):
- `radford2021clip`, [`clip`](../research/collection/tools/clip/card.md)
- `radford2023whisper`, [`whisper`](../research/collection/tools/whisper/card.md)
- `liu2024groundingdino`, [`grounding-dino`](../research/collection/tools/grounding-dino/card.md)
- `zhang2024llavavideo`, [`llava-video`](../research/collection/tools/llava-video/card.md)
- `pyscenedetect`, [`pyscenedetect`](../research/collection/tools/pyscenedetect/card.md)
- `wolf2020transformers`, [`huggingface`](../research/collection/tools/huggingface/card.md)
- `mcnamara2017pliers`, [`pliers`](../research/collection/tools/pliers/card.md)
- `qin2025crowdagent`, [`crowdagent`](../research/collection/tools/crowdagent/card.md)

Manual annotation (Layer 1):
- `elan`, [`elan`](../research/collection/tools/elan/card.md)
- `praat`, [`praat`](../research/collection/tools/praat/card.md)
- `boris2016`, [`boris`](../research/collection/tools/boris/card.md)
- `datavyu`, [`datavyu`](../research/collection/tools/datavyu/card.md)
- `labelstudio`, [`label-studio`](../research/collection/tools/label-studio/card.md)
