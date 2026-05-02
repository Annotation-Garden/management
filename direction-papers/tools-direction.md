# Tools Direction, FAIR Services Survey and the AGI Adapter Layer

A focused review on the tools strand of the Annotation Garden Initiative (AGI). This paper surveys the existing Findable, Accessible, Interoperable, Reusable (FAIR) services in the neuroimaging annotation lifecycle, accounts for what AGI inherits rather than reimplements, and scopes AGI's distinctive contribution: the missing middleware that turns AI-assisted and manual annotation outputs into Hierarchical Event Descriptors (HED) tagged Brain Imaging Data Structure (BIDS) Stim-BIDS `events.tsv`. Addresses [issue #2](https://github.com/Annotation-Garden/management/issues/2).

Abbreviations: Findable, Accessible, Interoperable, Reusable (FAIR), Brain Imaging Data Structure (BIDS), Hierarchical Event Descriptors (HED), Natural Scenes Dataset (NSD), Healthy Brain Network (HBN), magnetoencephalography (MEG), electroencephalography (EEG), intracranial EEG (iEEG), functional magnetic resonance imaging (fMRI), large language model (LLM), small language model (SLM), vision-language model (VLM), automatic speech recognition (ASR), graphical user interface (GUI), continuous integration (CI), command-line interface (CLI), application programming interface (API).

## 1. Introduction

### 1.1 The annotation lifecycle in modern neuroimaging

Producing a publishable analysis of a naturalistic-stimulus neuroimaging dataset traverses a long pipeline. Stimuli are selected and shared. Per-stimulus annotations are produced, either manually (by linguistics labs working in ELAN, by ethologists working in BORIS, by developmental groups working in Datavyu) or automatically (by computer-vision and speech-recognition models). Annotations are aligned to the recording timeline and exported as event tables. Datasets are organized according to BIDS, deposited in OpenNeuro or NEMAR, processed through pipelines such as fMRIPrep or EEGLAB, and analyzed with encoding-model libraries that consume the event tables as feature predictors.

The neuroinformatics community has invested heavily in standardizing each segment of the pipeline. The Brain Imaging Data Structure ([`bids-spec`](../research/collection/tools/bids-spec/card.md)) defined the dataset organization. The Hierarchical Event Descriptors framework ([`hed-spec`](../research/collection/tools/hed-spec/card.md)) defined the controlled annotation vocabulary. OpenNeuro ([`openneuro`](../research/collection/tools/openneuro/card.md)) and NEMAR ([`nemar`](../research/collection/tools/nemar/card.md)) provide the public archives. DataLad ([`datalad`](../research/collection/tools/datalad/card.md)) handles versioned distribution and provenance. NeuroScout ([`neuroscout`](../research/collection/tools/neuroscout/card.md)) demonstrates that automated stimulus annotation plus BIDS-conformant pipelines yields reproducible naturalistic-stimulus encoding analyses at scale on fMRI.

### 1.2 What is missing from the lifecycle

The pipeline is well-served at its endpoints. The dataset archive layer is mature; the analysis-pipeline layer is mature; the standards layer is stable and adopted. What is incomplete is the *annotation production* layer at the interface between domain-specific annotation tools and the canonical BIDS-plus-HED form. AI-assisted annotators (CLIP, Whisper, Grounding-DINO, LLaVA-Video, PySceneDetect) emit model-specific outputs; manual annotators (ELAN, Praat, BORIS, Datavyu, Label Studio) write tool-specific formats; CrowdAgent-pattern multi-source orchestration coordinates the sources but is annotation-format-agnostic. Each pipeline that ships an annotated dataset to OpenNeuro or NEMAR re-implements the conversion glue from scratch.

### 1.3 Gap statement and thesis

The gap is a contract layer rather than a tool. The standards exist; the analysis pipelines exist; the platforms exist; the AI annotators exist; the manual annotators exist. What is missing is the bidirectional adapter set that lets the upstream annotators write Stim-BIDS `events.tsv` with HED tags and lets the downstream platforms consume them without per-paper conversion code. AGI's distinctive technical commitment is to define and ship that contract layer.

This paper supports the thesis through a structured survey of the existing FAIR services across the five layers of the Phase 1 [`tool-ontology`](../research/synthesis/tool-ontology.md), then names the missing adapters precisely, then sketches a three-wave build order. Section 2 walks the inheritance accounting layer by layer. Section 3 names the missing middleware. Section 4 makes the composition argument. Section 5 sequences the build. Section 6 discusses interpretation and limitations. Section 7 concludes.

## 2. Background, what AGI inherits

The Phase 2 [`tool-ontology`](../research/synthesis/tool-ontology.md) sorts the 33 entries in the Phase 1 corpus into five layers. This section walks each layer at the policy level, identifying what already exists and what AGI consumes rather than rebuilds.

### 2.1 Layer 5, standards and specifications

Two standards anchor the entire stack. The BIDS specification ([`bids-spec`](../research/collection/tools/bids-spec/card.md)) defines dataset organization and file conventions; BEP044 Stim-BIDS ([`bep044-stim-bids`](../research/collection/tools/bep044-stim-bids/card.md)) defines stimulus-repository packaging and is exactly the AGI substrate. The HED specification ([`hed-spec`](../research/collection/tools/hed-spec/card.md)) defines the controlled annotation vocabulary; HED-SCORE ([`hed-score`](../research/collection/tools/hed-score/card.md)) is the clinical-EEG library schema. The FAIR principles ([`fair-principles`](../research/collection/tools/fair-principles/card.md)) define the governance rubric. NWB ([`nwb`](../research/collection/tools/nwb/card.md)) is a sibling format for raw neurophysiology; COBIDAS ([`cobidas`](../research/collection/tools/cobidas/card.md)) is a reporting checklist. The BIDS-validator ([`bids-validator`](../research/collection/tools/bids-validator/card.md)) ties the standards to runtime checks.

AGI inherits all of these. None requires modification or extension. AGI repositories ship as conformant BIDS plus Stim-BIDS plus HED-tagged datasets and pass the existing validators without AGI-specific patches.

### 2.2 Layer 4, infrastructure platforms

OpenNeuro ([`openneuro`](../research/collection/tools/openneuro/card.md)) is the canonical public BIDS archive with Creative Commons Zero defaults. NEMAR ([`nemar`](../research/collection/tools/nemar/card.md)) is the EEG, MEG, and iEEG gateway with HED-tag search and a high-performance computing path. DataLad ([`datalad`](../research/collection/tools/datalad/card.md)) provides the distributed, modular, provenance-tracked Git plus git-annex substrate. DANDI ([`dandi`](../research/collection/tools/dandi/card.md)) is the BRAIN Initiative archive for cellular neurophysiology. NeuroScout ([`neuroscout`](../research/collection/tools/neuroscout/card.md)) is the end-to-end web platform that auto-annotates naturalistic fMRI stimuli with Pliers and runs BIDS pipelines.

AGI does not duplicate any of these. The Garden architecture is hub-and-spoke: each stimulus becomes a versioned repository (the spoke) that NEMAR, OpenNeuro, NeuroScout, and DANDI index by reference. DataLad provides the cross-cutting provenance substrate that the white paper's branches-as-layers model depends on. NeuroScout in particular is the closest existing precedent for AGI's analysis side; the [`neuroscout` card](../research/collection/tools/neuroscout/card.md) makes the relationship explicit, calling out a NeuroScout-AGI bridge in which AGI annotations are consumed as NeuroScout predictors as the obvious near-term collaboration.

### 2.3 Layer 3, analysis pipelines and encoding-model libraries

EEGLAB ([`eeglab`](../research/collection/tools/eeglab/card.md)) is the MATLAB EEG analysis hub with the largest plugin ecosystem in the field, including HED tagging via the HEDTools plugin. MNE-Python ([`mne-python`](../research/collection/tools/mne-python/card.md)) is the Python suite for MEG, EEG, and iEEG with BIDS support via `mne-bids`. fMRIPrep ([`fmriprep`](../research/collection/tools/fmriprep/card.md)) and MRIQC ([`mriqc`](../research/collection/tools/mriqc/card.md)) are the canonical BIDS Apps for fMRI preprocessing and quality control. GLMsingle ([`glmsingle`](../research/collection/tools/glmsingle/card.md)) handles single-trial fMRI estimation. Unfold ([`unfold`](../research/collection/tools/unfold/card.md)) extends EEGLAB with regression-ERP and overlap correction. The mTRF-Toolbox ([`mtrf-toolbox`](../research/collection/tools/mtrf-toolbox/card.md)) fits temporal response functions for continuous-stimulus encoding.

AGI inherits all of these as the analysis endpoints for the data its repositories anchor. A successful AGI annotation flow ends with a HED-tagged events table that any of these tools consumes without AGI-specific code. The integration target is the existing BIDS importer in each tool, plus the HED-aware extensions where they exist.

### 2.4 Layer 2, AI-assisted annotation

CLIP ([`clip`](../research/collection/tools/clip/card.md)), Whisper ([`whisper`](../research/collection/tools/whisper/card.md)), Grounding-DINO ([`grounding-dino`](../research/collection/tools/grounding-dino/card.md)), LLaVA-Video ([`llava-video`](../research/collection/tools/llava-video/card.md)), PySceneDetect ([`pyscenedetect`](../research/collection/tools/pyscenedetect/card.md)), HuggingFace ([`huggingface`](../research/collection/tools/huggingface/card.md)), and Pliers ([`pliers`](../research/collection/tools/pliers/card.md)) are the AI annotators. CrowdAgent ([`crowdagent`](../research/collection/tools/crowdagent/card.md)) is the multi-agent orchestration layer that coordinates LLMs, SLMs, and human raters under a Quality Assurance Agent and a Scheduling Agent.

AGI inherits the model capabilities and the orchestration patterns. It does not inherit the output formats. None of these tools writes HED-tagged Stim-BIDS `events.tsv` natively. CLIP emits embeddings. Whisper emits transcripts and word-level timestamps in JSON or VTT. Grounding-DINO emits bounding boxes. LLaVA-Video emits free-form captions or multiple-choice answers. PySceneDetect emits frame indices. Pliers wraps the heterogeneous outputs behind a unified Stim plus Extractor abstraction whose ExtractorResult is a pandas DataFrame; standalone Pliers does not produce BIDS-conformant `events.tsv` and does not emit HED tags. Its BIDS path is realized through NeuroScout, which composes Pliers feature graphs into BIDS-execution pipelines. CrowdAgent coordinates sources but is annotation-format agnostic.

### 2.5 Layer 1, manual annotation

ELAN ([`elan`](../research/collection/tools/elan/card.md)) is the de facto standard for hierarchical, time-aligned audio and video annotation in linguistics and infant cognition. Praat ([`praat`](../research/collection/tools/praat/card.md)) is the canonical phonetic annotation tool with the TextGrid format. BORIS ([`boris`](../research/collection/tools/boris/card.md)) is the de facto event-coding tool in animal behavior and ethology. Datavyu ([`datavyu`](../research/collection/tools/datavyu/card.md)) is integrated with the Databrary repository for developmental video coding. Label Studio ([`label-studio`](../research/collection/tools/label-studio/card.md)) is the web-based labeling platform with a pluggable machine-learning backend.

These tools predate BIDS and HED by a decade or more and are unlikely to gain native BIDS or HED support through their own roadmaps. Their formats (`.eaf`, TextGrid, BORIS CSV, Datavyu spreadsheet, Label Studio XML) are stable, well-documented, and widely supported in the communities that produce naturalistic-stimulus annotations. AGI inherits the existing investment those communities have made in these tools; the cost of forcing labs to migrate to a new annotation interface is high enough that AGI must instead come to where the annotators already work.

## 3. The missing middleware

The inheritance accounting in Section 2 makes the gap precise. Three concrete adapter layers do not exist today.

### 3.1 Manual-tool to Stim-BIDS adapter (Layer 1 to standards)

Every Layer 1 tool writes a stable, well-documented format. AGI commits to bidirectional adapters that ingest those formats into Stim-BIDS `events.tsv` with HED tag mapping, and round-trip back so contributors keep working in their preferred interface. The contracts are concrete:

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

The middleware described in Section 3 is small in code volume but large in coordination. Each adapter is a few hundred lines plus a HED tag-mapping table. The expensive part is the standardization across tools: agreeing on which Hierarchical Event Descriptors map to ELAN tier "speaker", agreeing on the canonical word-level alignment format, agreeing on the bounding-box-to-event lossy reduction. The Phase 2 [`tool-ontology`](../research/synthesis/tool-ontology.md) shows that 14 of 33 entries already integrate with BIDS at the `native` or `aware` level and that HED appears in the integration column for 6 entries; the missing middleware lives almost entirely in the BIDS column for Layer 1 and Layer 2 entries.

AGI does not own any of the upstream tools or any of the downstream platforms. It owns the contract between them. The contract is what makes a community-versioned annotation layer possible at all, because without the contract every annotation effort produces a per-paper artifact and the layered branches-as-perspectives model in [`VISION.md`](../VISION.md) cannot operate. The composition argument is therefore not a software-engineering claim; it is an institutional claim about which body (AGI) is best placed to host the contract that no single tool maintainer is incentivized to write.

## 5. Build order

The middleware ships in three waves, each driven by an obvious near-term application.

**Wave 1, demonstrate the round-trip on Forrest Gump.** ELAN to Stim-BIDS to ELAN. The studyforrest community has the largest existing investment in ELAN-coded annotations of any AGI flagship; round-tripping their annotations into a versioned repository without losing fidelity is the existence proof. Pair with Whisper to seed dialogue transcripts and Praat for phoneme refinement. Closes the Layer 1 adapter gap concretely on a single repository.

**Wave 2, automate the AI-annotator stack on NSD.** Pliers extractors with HED emission, run on the NSD images, deposited as a versioned annotation branch in a stimulus repository. Coordinated with the ANNOTATE R01 Aim 2 work, where HEDit produces the higher-richness branches and AGI distributes them. Closes the Layer 2 adapter gap.

**Wave 3, multi-source quality control on HBN movies.** Label Studio as the human-review front-end, Whisper plus LLaVA-Video for the AI baseline, CrowdAgent-pattern coordination, public agreement metrics in the repository CI. The HBN-EEG corpus is the existence proof that HED Generation 3 sidecars work at scale; HBN movies extend the annotation-richness side. Closes the multi-source quality-control gap.

Each wave is scoped so that a single milestone PR delivers the adapter, the worked example, and the documentation for the next adapter to reuse the pattern.

## 6. Discussion

### 6.1 Interpretation

The argument is structural. A field needs a single body to write the contract layer between annotation production and annotation consumption; otherwise the contract is implicit, lab-specific, and fragmented. Identifying that body is half the work; the technical contributions follow. The Phase 2 [`tool-ontology`](../research/synthesis/tool-ontology.md) shows that no existing project occupies that position. NeuroScout writes part of the contract for fMRI plus Pliers; OpenNeuro writes part of the contract for BIDS deposits; HEDit (under ANNOTATE) writes part of the contract for multi-agent annotation production. None covers the full surface AGI defines.

The argument predicts that adopting AGI's adapter layer will reduce the per-paper annotation cost in three practically observable ways. First, ELAN-coded annotations will round-trip to Stim-BIDS without data loss, so the existing investment of linguistics and infant-cognition labs becomes consumable by the encoding-model literature. Second, automated annotation runs on canonical stimuli will publish to AGI repositories as versioned branches, so any future paper that needs scene tags or speech transcripts on those stimuli starts from the published branch rather than running its own pipeline. Third, multi-source quality metrics will be public per branch, so the field's evaluation of annotation reliability becomes a comparable measurement rather than a per-paper aspiration.

### 6.2 Limitations

This paper surveys the existing FAIR services and names the missing adapters; it does not implement them. The implementation is scoped in [`tools-direction.md`](./tools-direction.md) as a build order but not as a per-adapter technical specification. The technical specs belong in a forthcoming `tooling/` directory. The composition argument also assumes that maintainers of the upstream tools (ELAN, Praat, BORIS, Datavyu, Pliers) will accept AGI as the canonical bridge to BIDS. The assumption is plausible because the bridge is bidirectional and does not require any upstream-tool changes, but it is not pre-negotiated.

A second limitation is that the survey reflects the Phase 1 corpus's collection scope. Tools used heavily in adjacent communities (CVAT for video segmentation, Prodigy for active learning, web-based crowdsourcing tools beyond Label Studio) are not in the corpus and are therefore not in the inheritance accounting. The omission does not invalidate the missing-middleware argument but it does mean that some of those tools will need adapter contracts that this paper does not specify.

A third limitation is that the AI-annotator landscape moves fast. CLIP and Whisper were canonical choices in 2023; LLaVA-Video and Grounding-DINO are now state of the art for video and open-set object detection respectively; the next generation of vision-language models will be incumbents within twelve months. The adapter contract is designed to be model-agnostic (Pliers extractor pattern plus HED tag emission), but each specific model adapter has a finite half-life.

### 6.3 Future work

The empirical question that would test the thesis is whether labs that adopt AGI adapters subsequently publish more annotated-stimulus encoding analyses than they would otherwise, controlling for funding and lab size. Quantifying that lift requires (a) baseline measurement of the per-paper annotation cost in the current literature, (b) an adoption-tracking mechanism for AGI repositories, and (c) a comparable lab-level outcome measure. None of these exist today. They are reasonable Phase 4-or-later AGI deliverables.

A complementary line of future work is to extend the inheritance accounting beyond the Phase 1 corpus. CVAT, Prodigy, web-based crowdsourcing platforms, BIDS Apps beyond fMRIPrep and MRIQC, and the rapidly evolving foundation-model adapter ecosystem each merit their own per-tool analysis. The Phase 2 [`tool-ontology`](../research/synthesis/tool-ontology.md) is the natural document to extend.

### 6.4 Anticipated objection

A reader could argue that AGI is taking on too much: that integrating five Layer 1 manual-annotation tools, eight Layer 2 AI annotators, and a CrowdAgent-pattern quality-control layer is operationally infeasible for a community-governed project. The response is that the per-adapter cost is small (a few hundred lines plus a HED-mapping table) and the cumulative cost is amortized across the community of users who would otherwise pay it per paper. The build order in Section 5 also keeps the cost compounded: each wave delivers a working example and the adapter pattern that the next wave reuses.

## 7. Conclusion

The FAIR neuroscience commons has a missing middleware layer at the contract between annotation production and annotation consumption. The Phase 1 corpus shows that the upstream and downstream sides of the contract are well-served; the contract itself is not written. AGI's distinctive technical commitment is to write it and to ship it as a versioned adapter library. The build order is concrete: Wave 1 demonstrates the round-trip on Forrest Gump, Wave 2 automates the AI annotator stack on NSD, Wave 3 deploys multi-source quality control on HBN movies. The composition argument is not a software-engineering claim but an institutional one: the field needs a single body to write the contract, and AGI is the candidate body.

## References

Citations resolve to BibTeX keys in [`../research/collection/tools/tools.bib`](../research/collection/tools/tools.bib). Direct paper-card links appear inline in the prose; the keys here are for downstream manuscript export.

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
