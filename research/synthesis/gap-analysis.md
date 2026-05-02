# Gap Analysis

A three-column accounting of what the ANNOTATE R01 covers, what the current AGI white paper covers, and what falls outside both. The third column defines AGI's distinctive scope and is the input to Phase 3's white-paper update and direction documents.

Sources for the columns:

- **ANNOTATE R01**, drawn from [`specific-aims.tex`](file:///Users/yahya/Documents/git/grant-proposals/proposals/R01/2026-nlm-annotation/submission/specific-aims.tex), Aims 1, 2, 3, plus the research-strategy section list (Significance, Innovation, Approach with Aims 1, 2, 3, Rigor and Reproducibility, Timeline, Summary).
- **AGI white paper**, drawn from [`agi-white-paper.md`](../../agi-white-paper.md) and the supporting [`VISION.md`](../../VISION.md).
- **Uncovered terrain**, derived from the [`tool-ontology`](./tool-ontology.md), [`dataset-hierarchy`](./dataset-hierarchy.md), and [`science-map`](./science-map.md) syntheses.

Abbreviations: Hierarchical Event Descriptors (HED), Brain Imaging Data Structure (BIDS), Natural Scenes Dataset (NSD), Healthy Brain Network (HBN), magnetoencephalography (MEG), electroencephalography (EEG), intracranial EEG (iEEG), data-use agreement (DUA), foundation model (FM), large language model (LLM), vision-language model (VLM).

## Topic-by-topic comparison

| Topic | ANNOTATE R01 covers | AGI white paper covers | Uncovered, AGI distinctive scope |
|---|---|---|---|
| Stimulus repositories | Cites NSD, HBN, StudyForrest as targets for annotation production | Three flagship stimulus repositories (NSD, Forrest Gump, HBN movies) with hub-and-spoke architecture | Operationalize repository governance, contribution workflow, federation for restricted stimuli (see gaps 4 and 8 below) |
| Annotation production | Empirical curves at five richness levels on NSD; HEDit-driven multi-agent annotation; video extension of HEDit | Branches as annotation layers; pull requests as contribution unit; CLIP, Whisper, emotion-detection models as automated drafters | Define the adapter layer that turns AI-annotator outputs into HED-tagged Stim-BIDS `events.tsv` (gap 6); define the multi-rater consensus and credit attribution mechanism (gap 3) |
| Datasets covered | NSD (deep), HBN (validation), StudyForrest (validation) | Same three flagships, plus aspirational reach to OpenNeuro datasets | Cognitive task batteries (gap 1), second-wave naturalistic datasets (gap 5), hybrid task-naturalistic datasets (gap 7) |
| Modalities covered | EEG, iEEG, fMRI | Same three plus aspirational MEG | MEG concretely; eye-tracking, peripheral physiology, behavioral phenotyping (sub-gap of gap 1 below) |
| Tools used | HEDit, EEGLAB, NeuroScout pipelines | HEDit-class platform, generic GitHub workflows, automated annotators | Broad annotation tooling beyond neuroimaging-native (gap 2); explicit BIDS-Validator and HED-validator integration in CI |
| Standards anchored | HED Generation 3, BIDS, BEP044 implicit | BIDS, Stim-BIDS BEP044, HED, references DataLad informally | DataLad provenance and credit infrastructure as an explicit AGI commitment (gap 3) |
| Governance | Out of scope (it is a research grant) | Open-source code, openly licensed annotations, transparent governance asserted but not specified | FAIR commons governance, deprecation policy, fork etiquette, version sunset (gap 8) |
| Time horizon | Five-year project | Indefinite, three-phase rollout | Sustainability planning beyond initial NIH funding |

## Concrete gap list

Eight gaps, each citing the paper-cards or documents that establish the gap. The acceptance bar from [issue #5](https://github.com/Annotation-Garden/management/issues/5) is "≥5 concrete uncovered areas"; this list deliberately exceeds that bar to give Phase 3 room to prioritize.

### Gap 1, Cognitive task batteries with HED Generation-3 sidecars

**Established by**: [`hcp-task`](../collection/data/hcp-task/card.md), [`hcp-d-development`](../collection/data/hcp-d-development/card.md), [`abcd-task`](../collection/data/abcd-task/card.md), [`cam-can`](../collection/data/cam-can/card.md), [`aomic`](../collection/data/aomic/card.md), [`myconnectome`](../collection/data/myconnectome/card.md), [`fedorenko-language-localizer`](../collection/data/fedorenko-language-localizer/card.md), [`pinel-localizer`](../collection/data/pinel-localizer/card.md), [`localizer-ds000114`](../collection/data/localizer-ds000114/card.md).

ANNOTATE R01 is naturalistic-stimuli only (NSD images, HBN movies, Forrest Gump). The white paper's three flagships are likewise all naturalistic. Yet the corpus contains nine cognitive-task entries with combined N greater than 16,000 and zero community-curated HED Generation-3 sidecars. AGI is the only candidate party that should host them.

Proposed Phase 3 commitment: a `task-bids` collection of stimulus-anchored repositories, each carrying a HED-tagged sidecar for a canonical task (working memory, n-back, monetary incentive delay, stop-signal, language localizer, motor localizer). One task per repository, one PR per HED revision.

### Gap 2, Broad annotation tooling beyond neuroimaging-native

**Established by**: [`elan`](../collection/tools/elan/card.md), [`praat`](../collection/tools/praat/card.md), [`boris`](../collection/tools/boris/card.md), [`datavyu`](../collection/tools/datavyu/card.md), [`label-studio`](../collection/tools/label-studio/card.md).

The R01's tool stack is HEDit, EEGLAB, NeuroScout. The white paper mentions ELAN and Praat once each as fragmentation evidence and never returns to them. Yet linguistics, infant-cognition, and ethology labs that already annotate the same stimuli (Forrest Gump dialog, HBN Pixar shorts, Despicable Me child-viewing data) live in ELAN, Praat, BORIS, and Datavyu. Their existing investment is invisible to AGI without bidirectional adapters.

Proposed Phase 3 commitment: an explicit interoperability section of the white paper that names the bidirectional adapter contract for each Layer-1 tool, with concrete file-format mappings (`.eaf` to `events.tsv`, TextGrid to `events.tsv`, BORIS CSV to `events.tsv`, Datavyu spreadsheet to `events.tsv`).

### Gap 3, Provenance and credit infrastructure

**Established by**: [`datalad`](../collection/tools/datalad/card.md), [`crowdagent`](../collection/tools/crowdagent/card.md), [`hbn-eeg`](../collection/data/hbn-eeg/card.md).

The white paper asserts "credit attribution for all contributors" and "incentivizing high-quality contributions through transparent impact metrics" without specifying the mechanism. The R01 is silent on credit (it is grant-funded production). DataLad already supplies the substrate (provenance via Git plus git-annex), and CrowdAgent supplies the multi-source coordination pattern (per-source quality scores, per-rater budgets). AGI must operationalize both.

Proposed Phase 3 commitment: a `governance/credit-attribution.md` document that names: (1) the per-PR contributor record, (2) the inter-rater agreement metric and its public visibility, (3) the deprecation rule for outdated annotations, (4) the citation pattern for downstream papers.

### Gap 4, Federation for restricted stimuli

**Established by**: [`hbn-mri`](../collection/data/hbn-mri/card.md), [`courtois-neuromod`](../collection/data/courtois-neuromod/card.md), [`bang-ieeg-fmri`](../collection/data/bang-ieeg-fmri/card.md), [`bang-multimodal`](../collection/data/bang-multimodal/card.md), [`sherlock-fmri`](../collection/data/sherlock-fmri/card.md).

The white paper proposes a pointer-based architecture for HBN movies and acknowledges "copyright considerations". The R01 does not address federation. Of the 36 datasets in the corpus, thirteen carry data-use agreements and two are pointer-required for stimulus distribution. The white paper's pointer architecture is necessary but not sufficient: there is no documented protocol for federating annotations across institutions where the underlying data cannot leave the host institution.

Proposed Phase 3 commitment: a `governance/federation-protocol.md` that distinguishes three federation tiers (open, pointer-only, full-federation with annotation export but no data export) and specifies the metadata sidecar each tier requires.

### Gap 5, Second-wave datasets with under-annotated potential

**Established by**: [`things-initiative`](../collection/data/things-initiative/card.md), [`bold5000`](../collection/data/bold5000/card.md), [`sherlock-fmri`](../collection/data/sherlock-fmri/card.md), [`bang-ieeg-fmri`](../collection/data/bang-ieeg-fmri/card.md), [`narratives-pieman`](../collection/data/narratives-pieman/card.md), [`courtois-neuromod`](../collection/data/courtois-neuromod/card.md), [`naturalistic-neuroimaging-db`](../collection/data/naturalistic-neuroimaging-db/card.md), [`moth-radio-hour`](../collection/data/moth-radio-hour/card.md), [`little-prince-fmri`](../collection/data/little-prince-fmri/card.md).

The white paper's three flagships are deliberately conservative starting points. The R01's three datasets are also conservative. Both leave eighteen second-wave datasets in the corpus without a clear AGI on-ramp, several of which (THINGS, BOLD5000, Sherlock, Pieman, Bang) are field-defining naturalistic-stimulus benchmarks.

Proposed Phase 3 commitment: a `roadmap/second-wave.md` that lists the eighteen datasets in priority order with the criteria used (open license, existing community annotations, stimulus-pointer feasibility), so that AGI's second wave is principled rather than opportunistic.

### Gap 6, AI-annotator to BIDS and HED export adapters

**Established by**: [`clip`](../collection/tools/clip/card.md), [`whisper`](../collection/tools/whisper/card.md), [`grounding-dino`](../collection/tools/grounding-dino/card.md), [`llava-video`](../collection/tools/llava-video/card.md), [`pliers`](../collection/tools/pliers/card.md).

The R01 covers HEDit (a single annotation client). The white paper mentions "Whisper for dialogue transcription, CLIP for scene description, emotion detection models for affective ratings" without an export contract. Pliers is the closest existing orchestration layer with BIDS awareness; CrowdAgent provides multi-source coordination. AGI must define the adapter layer that converts model-specific outputs (CLIP embeddings, Whisper word timings, Grounding-DINO bounding boxes, LLaVA-Video captions) into HED-tagged Stim-BIDS `events.tsv`.

Proposed Phase 3 commitment: a `tooling/ai-adapters.md` describing the canonical adapter pattern, with one worked example per Layer-2 tool.

### Gap 7, Hybrid task and naturalistic datasets

**Established by**: [`lemon-mpi`](../collection/data/lemon-mpi/card.md), [`deap`](../collection/data/deap/card.md), [`seed`](../collection/data/seed/card.md), [`hbn-eeg`](../collection/data/hbn-eeg/card.md).

R01 is naturalistic-only; AGI white paper is naturalistic-only. Hybrid datasets like LEMON, DEAP, SEED, and HBN-EEG combine task, rest, and naturalistic content within a single subject visit. They are the methodological bridge between gap 1 (cognitive tasks) and the white paper's naturalistic core. The [`hbn-eeg card`](../collection/data/hbn-eeg/card.md) already proves the same HED sidecar machinery handles all three; AGI should generalize.

Proposed Phase 3 commitment: a worked example in the white paper showing a hybrid-paradigm AGI repository (HBN-EEG) with separate HED sidecars per condition (movie viewing, surround suppression, contrast change detection, sequence learning).

### Gap 8, FAIR commons governance for annotation

**Established by**: [`fair-principles`](../collection/tools/fair-principles/card.md), [`cobidas`](../collection/tools/cobidas/card.md), [`bids-spec`](../collection/tools/bids-spec/card.md), [`VISION.md`](../../VISION.md), and [issue #2](https://github.com/Annotation-Garden/management/issues/2) (FAIR space survey).

The white paper invokes FAIR principles indirectly and uses a Wikipedia metaphor for community contribution but does not specify the FAIR commons governance. The R01 is silent on governance. Issue #2 already names this as a Phase 3 deliverable; the gap analysis here scopes it.

Proposed Phase 3 commitment: a stand-alone direction document, the FAIR commons survey of issue #2, that maps governance practices in adjacent commons (Wikipedia, OpenStreetMap, Wikidata, OpenNeuro, DataLad-distributed datasets, Hugging Face datasets) and proposes AGI's governance choices with explicit alternatives considered and rejected.

## How the gaps cluster

Three clusters emerge:

- **Scope clusters**: gaps 1, 5, 7 expand AGI's dataset and paradigm coverage. They are addressable by adding repositories, not by changing AGI's architecture.
- **Tooling clusters**: gaps 2, 6 widen AGI's interoperability surface. They are addressable by writing adapters and naming integration contracts in the white paper.
- **Governance clusters**: gaps 3, 4, 8 require AGI to commit to specific institutional and procedural choices. They are addressable only through new direction documents.

Phase 3 should produce one direction document per cluster (scope roadmap, interoperability spec, governance manifesto) plus the white-paper update that threads them.

## Anticipated objection

A reader could argue that AGI is ambitious enough already and that gaps 1, 5, 6, 7 expand scope past what infrastructure can support. The argument is partly right and partly wrong. It is right that AGI cannot produce all of the missing annotations itself; it is wrong because AGI's value is precisely that it provides the stable substrate on which others produce them. The white paper's "branches as layers" formulation already implies this: AGI hosts the repository, the community hosts the annotations. Phase 3 should make that division of labor explicit so the gap list above is read as "the surface AGI exposes" rather than "the work AGI commits to performing".
