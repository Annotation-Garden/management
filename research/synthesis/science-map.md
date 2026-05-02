# Science Map

Walk through the 30 Strand C papers in [`research/collection/science/`](../collection/science/), grouped by the seven methodological themes already used in [`science/INDEX.md`](../collection/science/INDEX.md). Each theme records representative work, methodological maturity, distilled open questions from the per-card "Open questions / limitations" sections, and the annotation-infrastructure dependencies that feed back into AGI's roadmap.

Abbreviations: large language model (LLM), vision-language model (VLM), inter-subject correlation (ISC), temporal receptive window (TRW), hidden Markov model (HMM), generalized linear model (GLM), representational similarity analysis (RSA), Hierarchical Event Descriptors (HED), Brain Imaging Data Structure (BIDS), Natural Scenes Dataset (NSD), Healthy Brain Network (HBN), magnetoencephalography (MEG), electroencephalography (EEG), intracranial EEG (iEEG), functional magnetic resonance imaging (fMRI).

## Maturity legend

- **well-established**: paradigm has been replicated across labs and datasets for ten or more years; methods are textbook.
- **active**: paradigm is on the publication frontier with current methods consolidating; replication is underway but the analysis recipe is still moving.
- **nascent**: paradigm has emerged within the last two to four years and the methodological consensus has not yet stabilized.

## Theme 1, Annotation-driven encoding models

| Card | Year | Modalities | Maturity contribution |
|---|---|---|---|
| [`huth2016-semantic-maps`](../collection/science/huth2016-semantic-maps/card.md) | 2016 | fMRI | Voxel-wise semantic atlas tiling cortex from naturalistic narrative listening |
| [`naselaris2011-encoding-decoding-review`](../collection/science/naselaris2011-encoding-decoding-review/card.md) | 2011 | fMRI | Canonical review unifying encoding and decoding fMRI frameworks |
| [`yamins2014-performance-optimized`](../collection/science/yamins2014-performance-optimized/card.md) | 2014 | fMRI, electrophysiology | Task-optimized hierarchical CNNs predict ventral-stream activity |
| [`conwell2024-inductive-biases`](../collection/science/conwell2024-inductive-biases/card.md) | 2024 | fMRI | 1.8-billion-regression NSD benchmark showing model-design saturation at the noise ceiling |
| [`prince2022-glmsingle`](../collection/science/prince2022-glmsingle/card.md) | 2022 | fMRI | GLMsingle toolbox for trial-level beta estimation |

**Maturity**: well-established for the linear voxel-wise framework; active for deep-network feature spaces; nascent for the question of whether annotations themselves (rather than feature embeddings derived from generic web data) yield additive variance.

**Open questions distilled from the cards** (each bullet attributes its source card):
- *Huth 2016*: lexical embeddings ignore context that LLM contextual embeddings (LeBel 2023, Antonello 2023) capture; how much of the variance gap is closed by annotation richness rather than embedding sophistication is unanswered. Also, only seven subjects are deeply sampled, so cross-subject generalizability and population variance are untested.
- *Conwell 2024*: cross-stimulus generalization is mostly absent because the saturation plateau may be specific to NSD's static-image, COCO-derived stimuli; whether dynamic, narrative, or multi-modal stimuli reveal new inductive-bias differences is open.
- *Cross-card*: no paper in the theme directly tests whether **annotation-conditioned** training (e.g., HED-grounded captions) yields different encoding behavior from generic captions.
- *Antonello 2023*: compute cost is large and replication-limiting. AGI commons could provide pre-computed embeddings for canonical stimuli to allow community replication without 7-billion-parameter inference.

**Annotation-infrastructure dependency**: per-stimulus features are the input. Today every encoding study computes them in-house. AGI's contribution is canonical, versioned, HED-tagged feature layers that any encoder can subscribe to.

## Theme 2, Annotation-driven decoding

| Card | Year | Modalities | Maturity contribution |
|---|---|---|---|
| [`kay2008-identifying-natural-images`](../collection/science/kay2008-identifying-natural-images/card.md) | 2008 | fMRI | First natural-image identification from voxel-wise encoding |
| [`tang2023-semantic-reconstruction`](../collection/science/tang2023-semantic-reconstruction/card.md) | 2023 | fMRI | Non-invasive semantic decoder from narrative-listening fMRI using GPT features |
| [`scotti2024-mindeye2`](../collection/science/scotti2024-mindeye2/card.md) | 2024 | fMRI | Cross-subject NSD image reconstruction with one hour of new-subject data |

**Maturity**: well-established for closed-set identification; active for cross-subject and cross-stimulus reconstruction; nascent for population-level transferable decoders.

**Open questions distilled from the cards**:
- Subject-specific layers are still required even for the strongest cross-subject decoders; "zero-shot" decoding from no per-subject data is unsolved (Scotti 2024).
- Sixteen hours per subject (Tang 2023) is operationally infeasible for clinical translation; data-efficient variants via foundation-model pretraining are untested.
- No decoder evaluated to date has been **annotation-conditioned**: would HED tags or per-image semantic graphs as auxiliary supervision tighten the decoder more than scaling LLM features further?
- Privacy and consent frameworks for sharing brain-image-decoder weights are not community-standard; AGI's federation protocol is the natural place to formalize them.

**Annotation-infrastructure dependency**: decoders need the same feature-layer subscription that encoders need, plus a per-subject calibration scaffold. AGI's role is to host the calibration scaffold (per-subject anchor stimuli) alongside the per-stimulus annotation.

## Theme 3, Inter-subject correlations and hyperalignment

| Card | Year | Modalities | Maturity contribution |
|---|---|---|---|
| [`hasson2004-intersubject-synchronization`](../collection/science/hasson2004-intersubject-synchronization/card.md) | 2004 | fMRI | Origin of inter-subject correlation: shared cortical activity during natural movie viewing |
| [`hasson2010-reliability`](../collection/science/hasson2010-reliability/card.md) | 2010 | fMRI | Methodological review framing reliability as complement to amplitude |
| [`lerner2011-temporal-receptive-windows`](../collection/science/lerner2011-temporal-receptive-windows/card.md) | 2011 | fMRI | Narrative-scrambling experiment exposing temporal-receptive-window hierarchy |
| [`haxby2011-common-high-dim-model`](../collection/science/haxby2011-common-high-dim-model/card.md) | 2011 | fMRI | Foundational hyperalignment paper for shared ventral-temporal representational space |
| [`guntupalli2020-hyperalignment`](../collection/science/guntupalli2020-hyperalignment/card.md) | 2020 | fMRI | Unified review of response-based versus connectivity-based hyperalignment |
| [`finn2020-idiosynchrony`](../collection/science/finn2020-idiosynchrony/card.md) | 2020 | fMRI | Framework for individual-difference signals from shared-response residuals |

**Maturity**: well-established for ISC and Procrustes hyperalignment; active for connectivity-based and end-to-end-learned alignment; nascent for cross-modality alignment across fMRI, MEG, EEG, iEEG on shared stimuli.

**Open questions distilled from the cards**:
- ISC is feature-agnostic (Hasson 2004, 2010); decomposing synchrony into "what" makes regions co-fluctuate requires annotation layers, exactly the AGI deliverable.
- Hyperalignment on the same stimulus across modalities (fMRI to MEG to EEG to iEEG) is largely untested (Haxby 2011, Guntupalli 2020).
- Idiosynchrony in clinical and developmental populations is undocumented (Finn 2020); HBN-EEG is uniquely positioned to fill the gap.
- TRW depth (Lerner 2011) was inferred from temporal scrambling without a direct annotation layer; with HED-tagged events, the same hierarchy could be tested feature-by-feature.

**Annotation-infrastructure dependency**: every theme-3 advance going forward depends on annotation layers that decompose the stimulus into machine-actionable features. AGI's HED-tagged commons is the substrate.

## Theme 4, Event segmentation and boundaries

| Card | Year | Modalities | Maturity contribution |
|---|---|---|---|
| [`zacks2007-event-perception`](../collection/science/zacks2007-event-perception/card.md) | 2007 | behavior, fMRI | Event Segmentation Theory mind-brain framework |
| [`baldassano2017-event-structure`](../collection/science/baldassano2017-event-structure/card.md) | 2017 | fMRI | Hidden-Markov-model-based cortical event segmentation with hippocampal boundary signal |
| [`geerligs2022-nested-hierarchy`](../collection/science/geerligs2022-nested-hierarchy/card.md) | 2022 | fMRI | Partially nested cortical hierarchy of neural states |
| [`zheng2022-cognitive-boundaries`](../collection/science/zheng2022-cognitive-boundaries/card.md) | 2022 | single-unit, iEEG | Single-neuron boundary and event cells in human medial temporal lobe |
| [`benyakov2018-hippocampal-film-editor`](../collection/science/benyakov2018-hippocampal-film-editor/card.md) | 2018 | fMRI | Hippocampal BOLD selectivity for subjective event boundaries |

**Maturity**: well-established for the verbal Event Segmentation Theory and the HMM-based imaging operationalization; active for cross-modality (fMRI to iEEG to single-unit) replication; nascent for cross-modal alignment of stimulus-derived boundaries (visual cuts, semantic shifts) with neural boundaries.

**Open questions distilled from the cards**:
- HMM-based segmentation (Baldassano 2017, Geerligs 2022) discovers events from brain data alone; does not validate against multi-perspective stimulus annotations. AGI's commons supplies the missing annotation side.
- Single-rater boundary annotations have variable reliability (Ben-Yakov 2018); multi-rater consensus is a public-good Phase 2 candidate.
- No paper to date compares **VLM- or LLM-derived** boundaries to human boundary judgments at scale; CrowdAgent-style pipelines would enable this.
- Sub-field hippocampal differences (CA1, CA3, DG) require iEEG or single-unit data; cross-modality cooperation between fMRI HMM events and single-unit boundary firing is implied but not directly tested (Zheng 2022, Bang-multimodal).

**Annotation-infrastructure dependency**: boundary annotations must be portable, multi-rater, and HED-tagged. The [`bang-multimodal card`](../collection/data/bang-multimodal/card.md) and [`hbn-eeg card`](../collection/data/hbn-eeg/card.md) already validate this approach; AGI generalizes.

## Theme 5, Foundation models with annotation supervision

| Card | Year | Modalities | Maturity contribution |
|---|---|---|---|
| [`jiang2024-labram`](../collection/science/jiang2024-labram/card.md) | 2024 | EEG | LaBraM, 369-million-parameter EEG foundation model with channel-patch tokenization |
| [`han2025-diver1`](../collection/science/han2025-diver1/card.md) | 2025 | EEG, iEEG | DIVER-1, 1.82-billion-parameter EEG and iEEG foundation model on 1.6-million channel-hours |
| [`xiong2025-eegfm-review`](../collection/science/xiong2025-eegfm-review/card.md) | 2025 | EEG | Critical review showing EEG foundation models often fail to beat baselines |
| [`lahner2025-mosaic`](../collection/science/lahner2025-mosaic/card.md) | 2025 | fMRI | MOSAIC framework aggregating eight fMRI datasets in shared surface space |

**Maturity**: nascent across the board. The first generation of EEG foundation models has just landed and is already under critical review.

**Open questions distilled from the cards**:
- Pretraining data is dominated by clinical recordings; naturalistic-stimulus EEG and iEEG are under-represented (Jiang 2024, Han 2025). HBN-EEG and NSD-EEG are the obvious counterweight.
- No theme-5 model has been pretrained with **annotation supervision**; the Xiong 2025 card flags this absence as "a possibly missing ingredient" worth investigating, without claiming causal certainty.
- Annotation-response evaluation is absent: no theme-5 paper characterizes how downstream accuracy scales with task-specific annotated data on top of pretraining (a Theme-6 sufficiency question).
- Cross-modality alignment (EEG to fMRI to behavior on shared subjects) is unaddressed.
- Privacy and consent for cross-dataset model release is informal; AGI's commons would need a formal opt-in framework (Lahner 2025).

**Annotation-infrastructure dependency**: theme-5 progress is annotation-bottlenecked even more than theme-1. Without HED-tagged events on naturalistic stimuli, foundation-model pretraining remains a scaling-on-noise exercise.

## Theme 6, Annotation-response curves and sufficiency studies

| Card | Year | Modalities | Maturity contribution |
|---|---|---|---|
| [`antonello2023-scaling-laws`](../collection/science/antonello2023-scaling-laws/card.md) | 2023 | fMRI | Log-linear scaling of fMRI language encoding with data and model size |
| [`naspi2021-perceptual-semantic`](../collection/science/naspi2021-perceptual-semantic/card.md) | 2021 | fMRI | Annotation-granularity dissociates true vs false memory in ventral-temporal cortex |
| [`lebel2023-natural-language-fmri`](../collection/science/lebel2023-natural-language-fmri/card.md) | 2023 | fMRI | Open 27+ hour per-subject narrative-listening fMRI benchmark |

**Maturity**: nascent. This theme is the gap that the ANNOTATE R01 specific aims (`R01/2026-nlm-annotation/submission/specific-aims.tex` in the internal grant-proposals repository) explicitly target.

**Open questions distilled from the cards**:
- Antonello 2023 scaling laws hold for fewer than five subjects on a single English narrative; non-narrative, multilingual, and cross-modality scaling is unknown.
- Naspi 2021 dissociates granularity at the perceptual-semantic axis but not at the annotation-density axis (how many feature dimensions are enough?).
- LeBel 2023 has English-only word-aligned transcripts but no HED tagging or event-segmentation annotations; sufficiency curves cannot yet be estimated for richer annotation spaces.
- No theme-6 paper directly varies annotation richness as the independent variable while holding stimulus and model fixed; this is precisely what ANNOTATE Aim 2 will produce.

**Annotation-infrastructure dependency**: theme 6 cannot proceed without a corpus that supports annotation richness as a controllable variable. AGI's role is to host annotation versions at multiple richness levels (the same stimulus repository carrying coarse, medium, and dense annotation branches) so the curves can be drawn empirically.

## Theme 7, Cross-modal and cross-dataset generalization

| Card | Year | Modalities | Maturity contribution |
|---|---|---|---|
| [`cichy2014-resolving-object-recognition`](../collection/science/cichy2014-resolving-object-recognition/card.md) | 2014 | MEG, fMRI | Foundational MEG-fMRI fusion via RSA on shared object set |
| [`berezutskaya2022-multimodal-iEEG-fMRI`](../collection/science/berezutskaya2022-multimodal-iEEG-fMRI/card.md) | 2022 | iEEG, fMRI | Open multimodal iEEG-fMRI dataset on shared audiovisual stimulus |
| [`hebart2023-things-data`](../collection/science/hebart2023-things-data/card.md) | 2023 | fMRI, MEG, EEG, behavior | THINGS-data multimodal recordings on the 1854-concept stimulus space |
| [`deheer2017-hierarchical-speech`](../collection/science/deheer2017-hierarchical-speech/card.md) | 2017 | fMRI | Variance-partitioned spectral-articulatory-semantic encoding hierarchy |

**Maturity**: well-established for static-stimulus RSA (Cichy 2014); active for dynamic-stimulus cross-modal (Berezutskaya 2022, Hebart 2023); nascent for full quartet (fMRI, MEG, EEG, iEEG) on a single naturalistic stimulus.

**Open questions distilled from the cards**:
- Berezutskaya 2022 covers a single short clip (Hitchcock); longer naturalistic stimuli with cross-modal coverage at the Forrest-Gump scale do not exist.
- THINGS-data (Hebart 2023) covers static images at scale but lacks per-image HED-grounded annotations and EEG at the same scale as fMRI and MEG.
- Cross-modality generalization is not characterized for dynamic stimuli at all; AGI's commons makes this tractable by anchoring fMRI, MEG, EEG, iEEG datasets to the same stimulus repository (the existing NSD-fMRI plus NSD-iEEG plus NSD-EEG-alljoined triangle is a working proof of concept).
- Variance-partitioning approaches (de Heer 2017) work for two or three feature spaces; modern multi-perspective annotations require extensions to many more layers and have not been demonstrated.

**Annotation-infrastructure dependency**: cross-modal generalization needs annotations to be **stimulus-anchored** rather than dataset-anchored. AGI's "stimulus as a repository" is exactly the architectural commitment that lets a HED-tagged annotation propagate from NSD-fMRI to NSD-EEG without per-dataset re-annotation.

## Cross-theme synthesis

Three patterns recur across the seven themes:

1. **Annotation richness gates progress in five of seven themes.** Themes 1, 2, 5, 6, and 7 each contain at least one paper whose distilled open questions explicitly invoke annotation supervision, HED tagging, or per-stimulus feature layers as the missing ingredient. Theme 3 (ISC and hyperalignment) and theme 4 (event segmentation) are partial exceptions because their methods are stimulus-agnostic, but every theme-3 or theme-4 paper in the corpus would gain interpretability from annotation-decomposed analyses.

2. **Theme 6 is the gating theme.** Annotation-response curves (theme 6) determine the experimental designs that can proceed for themes 1, 2, and 5. Without sufficiency results, every encoding-model paper invents its own feature-richness defaults; foundation-model pretraining is conducted blind to whether the labels would help. ANNOTATE R01 Aim 2 is the empirical engine; AGI is the distribution layer.

3. **Cross-modality alignment is the next frontier.** Theme 3 (hyperalignment), theme 4 (single-unit events to fMRI HMM), theme 5 (cross-dataset foundation models), and theme 7 (RSA-style fusion) all flag cross-modality alignment as their central open question. AGI's stimulus-anchored commons is the only architectural commitment in the entire corpus that makes this question structurally tractable.

## Coverage check

All 30 science entries listed in [`../collection/science/INDEX.md`](../collection/science/INDEX.md) are placed across the seven themes above:

- Theme 1 (5): huth2016, naselaris2011, yamins2014, conwell2024, prince2022.
- Theme 2 (3): kay2008, tang2023, scotti2024.
- Theme 3 (6): hasson2004, hasson2010, lerner2011, haxby2011, guntupalli2020, finn2020.
- Theme 4 (5): zacks2007, baldassano2017, geerligs2022, zheng2022, benyakov2018.
- Theme 5 (4): jiang2024, han2025, xiong2025, lahner2025.
- Theme 6 (3): antonello2023, naspi2021, lebel2023.
- Theme 7 (4): cichy2014, berezutskaya2022, hebart2023, deheer2017.

Total: 30.
