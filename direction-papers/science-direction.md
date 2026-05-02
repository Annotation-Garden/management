# Science Direction, Annotation as the Gate to a New Cognitive-Neuroscience Paradigm

A focused review on the science strand of the Annotation Garden Initiative (AGI). This paper argues that the absence of standardized, community-curated stimulus annotations is the proximal reason naturalistic-stimulus datasets remain under-used by mainstream cognitive-neuroscience analytics, and that AGI's stimulus-anchored commons is the gating piece of infrastructure for the next paradigm shift in the field. The argument was first articulated in [issue #1](https://github.com/Annotation-Garden/management/issues/1); this paper develops it into a literature-grounded position by surveying the seven methodological themes catalogued in the Phase 1 corpus and the Phase 2 [`science-map`](../research/synthesis/science-map.md).

Abbreviations: Hierarchical Event Descriptors (HED), Brain Imaging Data Structure (BIDS), Natural Scenes Dataset (NSD), Healthy Brain Network (HBN), inter-subject correlation (ISC), temporal receptive window (TRW), hidden Markov model (HMM), generalized linear model (GLM), large language model (LLM), vision-language model (VLM), magnetoencephalography (MEG), electroencephalography (EEG), intracranial EEG (iEEG), functional magnetic resonance imaging (fMRI).

## 1. Introduction

### 1.1 The naturalistic turn and what it costs

Cognitive neuroscience has been shifting toward naturalistic stimuli for two decades. The arc began with [`hasson2004-intersubject-synchronization`](../research/collection/science/hasson2004-intersubject-synchronization/card.md), where the discovery that movie viewing produces stimulus-locked synchrony across subjects opened a continuous-stimulus alternative to the block and event-related designs that dominated the field. The arc accelerated with single-subject deep-sampling fMRI ([`huth2016-semantic-maps`](../research/collection/science/huth2016-semantic-maps/card.md)), with the release of the Natural Scenes Dataset ([`nsd-fmri`](../research/collection/data/nsd-fmri/card.md)) and the studyforrest project ([`studyforrest`](../research/collection/data/studyforrest/card.md)), and most recently with the Healthy Brain Network EEG release powering the NeurIPS 2025 EEG Foundation Challenge ([`hbn-eeg`](../research/collection/data/hbn-eeg/card.md)). The investment is real: tens of millions of dollars per dataset, hundreds of derivative papers per flagship.

And yet the methodologies used to analyze these datasets continue to over-represent stimulus-agnostic measures. Most labs that work with naturalistic recordings publish either inter-subject correlation, hyperalignment, hidden-Markov-model event segmentation, or stimulus-feature correlations against pre-existing automated extractors. Fewer labs publish multi-perspective, dense, theoretically grounded encoding analyses on naturalistic stimuli. Fewer still publish them on multiple datasets. The reason is operational, not conceptual: each naturalistic-stimulus encoding analysis pays an annotation cost twice, once when designing the experiment and once when analyzing it. The annotations are bespoke to the paper, undocumented, lab-specific, and discarded after publication.

### 1.2 Gap statement

What is missing in the literature is not better methods. The methods are mature: voxel-wise encoding ([`naselaris2011-encoding-decoding-review`](../research/collection/science/naselaris2011-encoding-decoding-review/card.md)), GLM trial-by-trial estimation ([`prince2022-glmsingle`](../research/collection/science/prince2022-glmsingle/card.md)), temporal response functions ([`mtrf-toolbox`](../research/collection/tools/mtrf-toolbox/card.md)), HMM-based event segmentation ([`baldassano2017-event-structure`](../research/collection/science/baldassano2017-event-structure/card.md)), Procrustes hyperalignment ([`haxby2011-common-high-dim-model`](../research/collection/science/haxby2011-common-high-dim-model/card.md)), and the foundation-model pretraining frameworks of the past two years ([`jiang2024-labram`](../research/collection/science/jiang2024-labram/card.md), [`han2025-diver1`](../research/collection/science/han2025-diver1/card.md), [`lahner2025-mosaic`](../research/collection/science/lahner2025-mosaic/card.md)) are all available and validated. What is missing is the substrate: a community-curated, versioned annotation layer that the methods can subscribe to without each paper re-annotating its stimuli from scratch.

### 1.3 Thesis

This paper argues that the substrate is the gating piece of infrastructure. With it, five of the seven Strand C themes become directly accessible to ordinary labs rather than only to groups that can afford bespoke annotation campaigns; the remaining two gain interpretive depth that bare-signal analyses cannot supply. Section 2 reviews the prior-work landscape across the seven themes. Section 3 walks through the gating evidence theme by theme. Section 4 anchors the argument in NeuroScout as an existence proof. Section 5 sketches the new-science roadmap and Section 6 the operational coordination with the ANNOTATE R01. Section 7 discusses interpretation, limitations, and counterarguments. Section 8 concludes.

## 2. Background, the seven themes of annotation-driven brain-behavior science

The Phase 1 corpus organizes thirty Strand C papers into seven methodological themes; the Phase 2 [`science-map`](../research/synthesis/science-map.md) inventories each theme. This section summarizes the prior-work landscape that the rest of the paper draws on. The themes group into two analytic kinds, *production-gated* and *interpretation-gated*, terms developed in Section 3.

**Theme 1, annotation-driven encoding models.** Voxel-wise encoding has been the dominant analytic for naturalistic-stimulus fMRI for fifteen years ([`naselaris2011-encoding-decoding-review`](../research/collection/science/naselaris2011-encoding-decoding-review/card.md), [`huth2016-semantic-maps`](../research/collection/science/huth2016-semantic-maps/card.md)). Recent work expanded the feature space from lexical to deep neural network embeddings ([`yamins2014-performance-optimized`](../research/collection/science/yamins2014-performance-optimized/card.md), [`conwell2024-inductive-biases`](../research/collection/science/conwell2024-inductive-biases/card.md)), refined trial-level signal estimation ([`prince2022-glmsingle`](../research/collection/science/prince2022-glmsingle/card.md)), and surfaced the question of whether annotation richness rather than embedding sophistication explains the remaining variance ([`antonello2023-scaling-laws`](../research/collection/science/antonello2023-scaling-laws/card.md)).

**Theme 2, annotation-driven decoding.** Closed-set image identification ([`kay2008-identifying-natural-images`](../research/collection/science/kay2008-identifying-natural-images/card.md)) opened the field; semantic decoding from cortex during narrative listening ([`tang2023-semantic-reconstruction`](../research/collection/science/tang2023-semantic-reconstruction/card.md)) and cross-subject image reconstruction ([`scotti2024-mindeye2`](../research/collection/science/scotti2024-mindeye2/card.md)) define its current frontier.

**Theme 3, inter-subject correlations and hyperalignment.** Stimulus-locked shared signal ([`hasson2004-intersubject-synchronization`](../research/collection/science/hasson2004-intersubject-synchronization/card.md), [`hasson2010-reliability`](../research/collection/science/hasson2010-reliability/card.md)) generalized to a temporal-receptive-window hierarchy ([`lerner2011-temporal-receptive-windows`](../research/collection/science/lerner2011-temporal-receptive-windows/card.md)), to a shared representational space recoverable across subjects ([`haxby2011-common-high-dim-model`](../research/collection/science/haxby2011-common-high-dim-model/card.md), [`guntupalli2020-hyperalignment`](../research/collection/science/guntupalli2020-hyperalignment/card.md)), and to individual-difference signals derived from shared-response residuals ([`finn2020-idiosynchrony`](../research/collection/science/finn2020-idiosynchrony/card.md)).

**Theme 4, event segmentation and boundaries.** A verbal Event Segmentation Theory ([`zacks2007-event-perception`](../research/collection/science/zacks2007-event-perception/card.md)) was operationalized for fMRI by HMM-based event discovery ([`baldassano2017-event-structure`](../research/collection/science/baldassano2017-event-structure/card.md)) and extended to a partially nested cortical hierarchy ([`geerligs2022-nested-hierarchy`](../research/collection/science/geerligs2022-nested-hierarchy/card.md)). Hippocampal selectivity for boundary events ([`benyakov2018-hippocampal-film-editor`](../research/collection/science/benyakov2018-hippocampal-film-editor/card.md)) was confirmed at the single-neuron level ([`zheng2022-cognitive-boundaries`](../research/collection/science/zheng2022-cognitive-boundaries/card.md)).

**Theme 5, foundation models with annotation supervision.** First-generation EEG foundation models scaled parameters and channels ([`jiang2024-labram`](../research/collection/science/jiang2024-labram/card.md), [`han2025-diver1`](../research/collection/science/han2025-diver1/card.md)) but a critical review documented that they often fail to beat hand-engineered baselines ([`xiong2025-eegfm-review`](../research/collection/science/xiong2025-eegfm-review/card.md)). Cross-dataset aggregation in fMRI ([`lahner2025-mosaic`](../research/collection/science/lahner2025-mosaic/card.md)) used CLIP features rather than HED tags as supervision.

**Theme 6, annotation-response curves and sufficiency.** Log-linear scaling of fMRI language encoding with data and model size ([`antonello2023-scaling-laws`](../research/collection/science/antonello2023-scaling-laws/card.md)) and the dissociation of true and false memory by annotation granularity in ventral-temporal cortex ([`naspi2021-perceptual-semantic`](../research/collection/science/naspi2021-perceptual-semantic/card.md)) opened the question. The recent open per-subject narrative-listening benchmark ([`lebel2023-natural-language-fmri`](../research/collection/science/lebel2023-natural-language-fmri/card.md)) provides the data substrate; the controlled annotation-richness experiment has not yet been run, and it is precisely what the ANNOTATE R01 Aim 2 targets.

**Theme 7, cross-modal and cross-dataset generalization.** MEG-fMRI fusion via representational similarity analysis ([`cichy2014-resolving-object-recognition`](../research/collection/science/cichy2014-resolving-object-recognition/card.md)), iEEG-fMRI alignment on shared audiovisual stimulus ([`berezutskaya2022-multimodal-iEEG-fMRI`](../research/collection/science/berezutskaya2022-multimodal-iEEG-fMRI/card.md)), the THINGS multimodal benchmark ([`hebart2023-things-data`](../research/collection/science/hebart2023-things-data/card.md)), and variance-partitioning across feature spaces ([`deheer2017-hierarchical-speech`](../research/collection/science/deheer2017-hierarchical-speech/card.md)) define this theme.

## 3. The annotation-gating evidence

Five of the seven themes are *production-gated* by annotation supply: the analyses cannot be run without per-stimulus annotation features. The remaining two are *interpretation-gated*: the methods produce results without annotation, but the explanatory power of those results is bounded by what the field can say about *which* stimulus features drive observed patterns.

### 3.1 Production-gated themes

**Encoding (theme 1).** Every paper in the theme either generates its own per-stimulus features ([`huth2016-semantic-maps`](../research/collection/science/huth2016-semantic-maps/card.md) used lexical co-occurrence; [`yamins2014-performance-optimized`](../research/collection/science/yamins2014-performance-optimized/card.md) used CNN activations; [`conwell2024-inductive-biases`](../research/collection/science/conwell2024-inductive-biases/card.md) ran a 1.8-billion-regression battery against many embeddings) or assumes a feature space provided by another paper. None operates on a community-versioned annotation layer. The Huth 2016 card asks how much variance is missed by lexical co-occurrence relative to LLM contextual embeddings; the Antonello 2023 card asks the complementary question of whether data quantity and annotation richness can be dissociated, since current scaling-law experiments conflate them.

**Decoding (theme 2).** Subject-specific layers remain required even for the strongest cross-subject decoders ([`scotti2024-mindeye2`](../research/collection/science/scotti2024-mindeye2/card.md)); zero-shot decoding from no per-subject data is unsolved. Sixteen hours per subject ([`tang2023-semantic-reconstruction`](../research/collection/science/tang2023-semantic-reconstruction/card.md)) is operationally infeasible for clinical translation, and data-efficient variants via annotation-conditioned pretraining are untested because the annotation layer does not yet exist outside per-paper artifacts.

**Foundation models (theme 5).** This is the most acute case. The Xiong 2025 review identifies pretraining-without-annotation-supervision as a possibly missing ingredient in the current generation of EEG foundation models. None of the theme-5 papers exposes annotation supervision as a controlled variable. The aggregation pipeline in [`lahner2025-mosaic`](../research/collection/science/lahner2025-mosaic/card.md) uses CLIP features rather than HED tags and explicitly flags the absence as a limitation.

**Annotation-response curves (theme 6).** No paper to date has varied annotation richness as an independent experimental variable while holding stimulus and model fixed. The reason is operational: producing the same stimulus's annotations at five distinct richness levels exceeds the cost any single lab is willing to absorb for a single paper. The ANNOTATE R01 Aim 2 will produce the curves on NSD; AGI's branches-as-layers model provides the distribution and replication infrastructure that makes the curves a public scientific output rather than a methods appendix.

**Cross-modal generalization (theme 7).** Cross-modal alignment depends on the stimulus side being identical across modalities. Today that identity is enforced informally, paper by paper. The NSD-fMRI plus NSD-iEEG plus NSD-EEG-alljoined triangle works only because the underlying stimulus set is curated under a single license and a stable identifier scheme. Generalizing the pattern to studyforrest, to THINGS, and to the Bang family requires the same architectural commitment that AGI's stimulus-anchored commons makes formal.

### 3.2 Interpretation-gated themes

**ISC and hyperalignment (theme 3).** ISC says that regions co-fluctuate; it cannot say what makes them co-fluctuate. The TRW hierarchy of [`lerner2011-temporal-receptive-windows`](../research/collection/science/lerner2011-temporal-receptive-windows/card.md) was inferred from temporal scrambling rather than from feature-by-feature analysis. Hyperalignment ([`haxby2011-common-high-dim-model`](../research/collection/science/haxby2011-common-high-dim-model/card.md), [`guntupalli2020-hyperalignment`](../research/collection/science/guntupalli2020-hyperalignment/card.md)) builds shared representational spaces that are powerful for cross-subject prediction but opaque for semantic interpretation. Idiosynchrony ([`finn2020-idiosynchrony`](../research/collection/science/finn2020-idiosynchrony/card.md)) extracts individual-difference signals from shared-response residuals; the card explicitly notes that residual analyses cannot be pinned to specific stimulus features without machine-actionable annotations. Annotation layers convert these methods from black-box predictors into hypothesis-generating tools without changing the methods themselves.

**Event segmentation (theme 4).** HMM-based segmentation ([`baldassano2017-event-structure`](../research/collection/science/baldassano2017-event-structure/card.md), [`geerligs2022-nested-hierarchy`](../research/collection/science/geerligs2022-nested-hierarchy/card.md)) discovers events from brain data alone and does not validate against multi-perspective stimulus annotations. Adding the annotation layer would let the field test whether HMM events correspond to visual cuts, semantic shifts, character changes, or none of the above. Single-rater boundary annotations have variable reliability ([`benyakov2018-hippocampal-film-editor`](../research/collection/science/benyakov2018-hippocampal-film-editor/card.md)); a multi-rater consensus annotation hosted in a versioned repository becomes a public good that every event-segmentation paper can use as ground truth.

## 4. NeuroScout as existence proof

The user-facing framing in [issue #1](https://github.com/Annotation-Garden/management/issues/1) cites [`neuroscout`](../research/collection/tools/neuroscout/card.md) as a project that already exploits richer annotations to lift naturalistic-stimulus analytics out of the per-paper annotation cycle. NeuroScout is the closest existing precedent for what AGI proposes on the analysis side: a community resource that makes annotations of naturalistic stimuli first-class objects. Its scope is fMRI-only and its annotation layer is whatever [`pliers`](../research/collection/tools/pliers/card.md) automatically extracts from the stimuli.

NeuroScout proves the operational point. Once Pliers feature graphs were available for Forrest Gump, encoding-model analyses on Forrest Gump became routine instead of bespoke. The lift was not in the methods, which were the same voxel-wise encoding analyses already standard in the field; the lift was in the infrastructure that supplied the annotation layer to those methods at zero marginal cost per paper. AGI generalizes the lift across modalities (NeuroScout is fMRI-only), across annotation provenance (NeuroScout uses Pliers extractors only; AGI accepts Pliers, HEDit, ELAN, Praat, BORIS, Datavyu, Label Studio, and human-curated PR contributions), and across dataset coverage (NeuroScout covers a curated set; AGI covers any stimulus that admits a Stim-BIDS repository).

## 5. The new-science roadmap

When annotation flows, the order of paradigm-shifting outputs is approximately:

1. **Encoding-model libraries on canonical stimuli (theme 1).** With HED-tagged events on NSD, Forrest Gump, and Moth-Radio-Hour, the standard voxel-wise pipeline becomes a one-line invocation against a shared feature graph. Labs that today cannot afford the annotation overhead publish encoding-model results within weeks rather than months.
2. **Annotation-supervised foundation-model pretraining (theme 5).** The Xiong 2025 critique becomes testable. A LaBraM-class model pretrained on HBN-EEG with HED supervision is benchmarked against the same model pretrained without supervision, on the same downstream task suite. The current absence of that experiment is a corpus-availability problem, not a methodological one.
3. **Annotation-response curves at scale (theme 6).** ANNOTATE produces the curves on NSD; AGI hosts the resulting annotation layers and replicates the experiment on second-wave datasets ([`bold5000`](../research/collection/data/bold5000/card.md), [`things-eeg2`](../research/collection/data/things-eeg2/card.md), [`narratives-pieman`](../research/collection/data/narratives-pieman/card.md), [`moth-radio-hour`](../research/collection/data/moth-radio-hour/card.md), [`little-prince-fmri`](../research/collection/data/little-prince-fmri/card.md)) without each replication being a separate methods paper.
4. **Cross-modal alignment papers (theme 7).** The NSD triangle generalizes to the studyforrest quartet (7T fMRI plus 3T fMRI plus MEG plus eye-gaze) once the annotation layer is shared. THINGS-data plus NOD-EEG plus THINGS-EEG2 becomes the same kind of triangle for static images.
5. **Annotation-decomposed ISC and event-segmentation papers (themes 3 and 4).** Once a HED-tagged layer exists, the move from "regions co-fluctuate" to "regions co-fluctuate during character-emotion shifts" or from "cortical events occur at HMM-discovered timepoints" to "cortical events align with annotated visual cuts but not with annotated semantic shifts" is a few lines of code rather than a new annotation campaign.

The order is approximate; the dependencies are real. Theme 1 ships first because the analytic infrastructure is already mature and waiting on annotation. Theme 5 ships next because the foundation-model literature is the loudest current demand for annotation-supervised pretraining data. Theme 6 ships in coordinated parallel with the ANNOTATE R01. Themes 7, 3, and 4 follow.

## 6. Operational coordination with ANNOTATE

The relationship is documented in detail in [`scope-diagram`](../research/synthesis/scope-diagram.md). In short: ANNOTATE is the empirical engine that produces the annotation-response curves and the HEDit annotation client; AGI is the durable distribution layer that hosts the resulting annotations as versioned repositories and extends the work to datasets and modalities ANNOTATE cannot reach within a five-year three-modality three-dataset grant. ANNOTATE produces curves on NSD across all three modalities (Aim 1), validates EEG generalization on HBN-EEG (Aim 3), and validates fMRI generalization on StudyForrest (Aim 3). AGI extends to MEG, eye-tracking, behavior, the cognitive-task wedge, and second-wave naturalistic datasets. The two projects are complementary; the parallel construction of empirical findings (ANNOTATE) and durable infrastructure (AGI) is the strongest strategic argument for both.

## 7. Discussion

### 7.1 Interpretation

The argument advanced here can be read in two ways. The conservative reading: AGI lowers the operational cost of naturalistic-stimulus encoding analyses, expanding the set of labs that can publish them and replacing per-paper annotation churn with community-curated layers. The strong reading: the current dominance of resting-state and tightly controlled-paradigm designs in cognitive neuroscience reflects not a scientific preference but an annotation-cost asymmetry, and removing that asymmetry redirects the field toward richer designs whose hypotheses better match the brains being studied. The strong reading is the one that matches the user's framing in [issue #1](https://github.com/Annotation-Garden/management/issues/1).

The two readings agree on the operational consequences. They disagree on the magnitude of paradigm shift to expect. The Phase 1 corpus does not adjudicate the disagreement; the experiments that would adjudicate it (ANNOTATE Aim 2, plus AGI-hosted replications) have not yet been run.

### 7.2 Limitations

This paper is a literature-grounded position, not a meta-analysis. It draws on thirty Strand C papers and synthesizes their open-questions sections into a thesis; it does not estimate effect sizes for the predicted shifts, and it cannot bound the rate at which the community will adopt AGI-hosted annotations. The interpretation-gating argument for themes 3 and 4 is in particular a forward-looking claim about explanatory power, not a tested hypothesis. The roadmap order in Section 5 reflects the corpus's emphasis on encoding and foundation-model work; teams whose priorities differ may sequence outputs differently.

A related limitation is that the corpus over-represents fMRI relative to MEG, EEG, and iEEG. Twenty-three of the thirty Strand C entries are fMRI-only or fMRI-primary. The five EEG-and-iEEG entries cluster in theme 5; the THINGS-data entry ([`hebart2023-things-data`](../research/collection/science/hebart2023-things-data/card.md)) is the only multimodal-with-EEG paper in the corpus. This skew matches the historical distribution of naturalistic-stimulus literature and reflects publication norms rather than an oversight in collection.

### 7.3 Future work

The empirical experiments that would test the thesis are: (a) annotation-richness sufficiency curves at multiple levels per stimulus, replicated across modalities and across datasets; (b) annotation-supervised foundation-model pretraining benchmarked head-to-head against unsupervised pretraining on the same downstream tasks; (c) cross-modal alignment papers that share a single HED-tagged annotation layer across two or more recording modalities on the same stimulus; (d) interpretive ISC and event-segmentation analyses that decompose shared signal by annotated stimulus features. Each requires the AGI substrate. None requires methodological innovation beyond what the field has already validated.

### 7.4 Anticipated objection

A reader could argue that the field's preference for resting-state and controlled paradigms reflects substantive scientific judgment about confound control and inferential clarity, not annotation-cost economics, and that lifting the annotation cost will not substantially shift the methodological mix. The Phase 1 corpus does not refute that argument directly. It provides circumstantial evidence against it: every theme in the corpus that uses naturalistic stimuli flags its annotation-side limitation in the open-questions section of one or more constituent papers. The cumulative weight of those flags suggests that the community has been actively waiting on the annotation layer; the substantive-judgment alternative would predict less consensus on what the bottleneck actually is.

## 8. Conclusion

The cognitive-neuroscience literature on annotation-driven brain-behavior science is methodologically mature and infrastructurally starved. The methods to extract scientific signal from naturalistic neural recordings exist; the annotation layer those methods would consume does not yet exist as a community-versioned, FAIR-compliant resource. AGI's contribution is the substrate. With it, five of seven canonical themes become production-gated to the point of routine publication; the remaining two gain the interpretive ceiling that bare-signal analyses cannot supply. The science strand of the Annotation Garden Initiative is therefore not a research program; it is the infrastructure that makes a generation of latent research programs operational.

## References

Citations resolve to BibTeX keys in [`../research/collection/science/science.bib`](../research/collection/science/science.bib), [`../research/collection/data/data.bib`](../research/collection/data/data.bib), and [`../research/collection/tools/tools.bib`](../research/collection/tools/tools.bib). Direct paper-card links appear inline in the prose; the keys here are for downstream manuscript export.

Science (Strand C):
- `antonello2023scaling`, [`antonello2023-scaling-laws`](../research/collection/science/antonello2023-scaling-laws/card.md)
- `baldassano2017event`, [`baldassano2017-event-structure`](../research/collection/science/baldassano2017-event-structure/card.md)
- `benyakov2018hippocampal`, [`benyakov2018-hippocampal-film-editor`](../research/collection/science/benyakov2018-hippocampal-film-editor/card.md)
- `berezutskaya2022multimodal`, [`berezutskaya2022-multimodal-iEEG-fMRI`](../research/collection/science/berezutskaya2022-multimodal-iEEG-fMRI/card.md)
- `cichy2014resolving`, [`cichy2014-resolving-object-recognition`](../research/collection/science/cichy2014-resolving-object-recognition/card.md)
- `conwell2024inductive`, [`conwell2024-inductive-biases`](../research/collection/science/conwell2024-inductive-biases/card.md)
- `deheer2017hierarchical`, [`deheer2017-hierarchical-speech`](../research/collection/science/deheer2017-hierarchical-speech/card.md)
- `finn2020idiosynchrony`, [`finn2020-idiosynchrony`](../research/collection/science/finn2020-idiosynchrony/card.md)
- `geerligs2022nested`, [`geerligs2022-nested-hierarchy`](../research/collection/science/geerligs2022-nested-hierarchy/card.md)
- `guntupalli2020hyperalignment`, [`guntupalli2020-hyperalignment`](../research/collection/science/guntupalli2020-hyperalignment/card.md)
- `han2025diver`, [`han2025-diver1`](../research/collection/science/han2025-diver1/card.md)
- `hasson2004intersubject`, [`hasson2004-intersubject-synchronization`](../research/collection/science/hasson2004-intersubject-synchronization/card.md)
- `hasson2010reliability`, [`hasson2010-reliability`](../research/collection/science/hasson2010-reliability/card.md)
- `haxby2011common`, [`haxby2011-common-high-dim-model`](../research/collection/science/haxby2011-common-high-dim-model/card.md)
- `hebart2023things`, [`hebart2023-things-data`](../research/collection/science/hebart2023-things-data/card.md)
- `huth2016semantic`, [`huth2016-semantic-maps`](../research/collection/science/huth2016-semantic-maps/card.md)
- `jiang2024labram`, [`jiang2024-labram`](../research/collection/science/jiang2024-labram/card.md)
- `kay2008identifying`, [`kay2008-identifying-natural-images`](../research/collection/science/kay2008-identifying-natural-images/card.md)
- `lahner2025mosaic`, [`lahner2025-mosaic`](../research/collection/science/lahner2025-mosaic/card.md)
- `lebel2023natural`, [`lebel2023-natural-language-fmri`](../research/collection/science/lebel2023-natural-language-fmri/card.md)
- `lerner2011temporal`, [`lerner2011-temporal-receptive-windows`](../research/collection/science/lerner2011-temporal-receptive-windows/card.md)
- `naselaris2011encoding`, [`naselaris2011-encoding-decoding-review`](../research/collection/science/naselaris2011-encoding-decoding-review/card.md)
- `naspi2021perceptual`, [`naspi2021-perceptual-semantic`](../research/collection/science/naspi2021-perceptual-semantic/card.md)
- `prince2022glmsingle`, [`prince2022-glmsingle`](../research/collection/science/prince2022-glmsingle/card.md)
- `scotti2024mindeye`, [`scotti2024-mindeye2`](../research/collection/science/scotti2024-mindeye2/card.md)
- `tang2023semantic`, [`tang2023-semantic-reconstruction`](../research/collection/science/tang2023-semantic-reconstruction/card.md)
- `xiong2025eegfm`, [`xiong2025-eegfm-review`](../research/collection/science/xiong2025-eegfm-review/card.md)
- `yamins2014performance`, [`yamins2014-performance-optimized`](../research/collection/science/yamins2014-performance-optimized/card.md)
- `zacks2007event`, [`zacks2007-event-perception`](../research/collection/science/zacks2007-event-perception/card.md)
- `zheng2022cognitive`, [`zheng2022-cognitive-boundaries`](../research/collection/science/zheng2022-cognitive-boundaries/card.md)

Tools (Strand A):
- `delavega2022neuroscout`, [`neuroscout`](../research/collection/tools/neuroscout/card.md)
- `mcnamara2017pliers`, [`pliers`](../research/collection/tools/pliers/card.md)
- `crosse2016mtrf`, [`mtrf-toolbox`](../research/collection/tools/mtrf-toolbox/card.md)

Data (Strand B):
- `allen2022massive`, [`nsd-fmri`](../research/collection/data/nsd-fmri/card.md)
- `chang2019bold5000`, [`bold5000`](../research/collection/data/bold5000/card.md)
- `gifford2022thingseeg2`, [`things-eeg2`](../research/collection/data/things-eeg2/card.md)
- `hanke2014studyforrest`, [`studyforrest`](../research/collection/data/studyforrest/card.md)
- `huth2016moth`, [`moth-radio-hour`](../research/collection/data/moth-radio-hour/card.md)
- `li2022littleprince`, [`little-prince-fmri`](../research/collection/data/little-prince-fmri/card.md)
- `nastase2021narratives`, [`narratives-pieman`](../research/collection/data/narratives-pieman/card.md)
- `shirazi2024hbneeg`, [`hbn-eeg`](../research/collection/data/hbn-eeg/card.md)
