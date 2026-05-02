# Science Direction, Annotation as the Gate to a New Cognitive-Neuroscience Paradigm

A focused mini lit review on the science strand of the Annotation Garden Initiative (AGI). Argues that the absence of standardized, community-curated stimulus annotations is the proximal reason naturalistic-stimulus datasets remain under-used by mainstream cognitive-neuroscience analytics, and that AGI's stimulus-anchored commons is the gating piece of infrastructure for the next paradigm shift. Addresses [issue #1](https://github.com/Annotation-Garden/management/issues/1).

Abbreviations: Hierarchical Event Descriptors (HED), Brain Imaging Data Structure (BIDS), Natural Scenes Dataset (NSD), Healthy Brain Network (HBN), inter-subject correlation (ISC), temporal receptive window (TRW), hidden Markov model (HMM), generalized linear model (GLM), large language model (LLM), vision-language model (VLM), magnetoencephalography (MEG), electroencephalography (EEG), intracranial EEG (iEEG), functional magnetic resonance imaging (fMRI).

## 1. The framing

A view from the field, captured in the phrasing of [issue #1](https://github.com/Annotation-Garden/management/issues/1): rich annotations of naturalistic stimuli could be the main factor that lifts these datasets to a much higher fraction of their potential, because naturalistic stimuli come with minimal annotation but very high-dimensional descriptive surface. Most labs default to resting-state or controlled-paradigm designs not because rest is more interesting but because the analytics they are trained on (the GLM, voxel-wise encoding, evoked-potential averaging) require event tables that resting-state and controlled paradigms produce mechanically. Naturalistic stimuli do not produce those tables for free. Producing them is laborious, lab-specific, and almost always discarded after the paper that motivated them is published.

That history is what AGI inherits. The argument of this direction paper is that AGI is not a tool, a dataset archive, or a competing analysis platform. It is the missing substrate that turns one-off annotation work into a public good, and once that substrate exists, a large fraction of the open scientific questions catalogued in the Phase 2 [`science-map`](../research/synthesis/science-map.md) become tractable for ordinary labs rather than only for groups that can afford bespoke annotation campaigns.

Five of the seven Strand C themes in the Phase 1 corpus are gated by annotation supply. The remaining two are nominally annotation-agnostic but gain large amounts of interpretability when annotation layers exist. The next two sections walk through the gating evidence in detail, and the rest of the paper sketches the roadmap that follows.

## 2. The annotation-gated themes

### 2.1 Annotation-driven encoding models (theme 1)

Voxel-wise encoding has been the dominant analytic for naturalistic-stimulus fMRI for fifteen years. The canonical works in the corpus are [`naselaris2011-encoding-decoding-review`](../research/collection/science/naselaris2011-encoding-decoding-review/card.md), [`huth2016-semantic-maps`](../research/collection/science/huth2016-semantic-maps/card.md), [`yamins2014-performance-optimized`](../research/collection/science/yamins2014-performance-optimized/card.md), [`prince2022-glmsingle`](../research/collection/science/prince2022-glmsingle/card.md), and [`conwell2024-inductive-biases`](../research/collection/science/conwell2024-inductive-biases/card.md). Every one of these papers either generates its own per-stimulus features (Huth's lexical co-occurrence vectors, Yamins's CNN activations, Conwell's 1.8-billion-regression battery) or assumes a feature space provided by another paper. None operates on a community-versioned annotation layer, and the open-questions sections of the cards make explicit that this is the next-step gap. The Huth 2016 card asks how much of the variance shortfall against modern contextual embeddings is closed by richer annotations rather than fancier embeddings; the Conwell 2024 card flags that "diet" axes treat training corpora as labels and never analyze which annotation properties drive the brain-prediction differences.

The point is structural: the encoding-model literature has saturated against per-paper feature pipelines and is now waiting on a substrate where multiple annotation types can be composed. The infrastructure piece sits exactly where AGI lives.

### 2.2 Annotation-driven decoding (theme 2)

The decoding literature is shorter but trends in the same direction. [`kay2008-identifying-natural-images`](../research/collection/science/kay2008-identifying-natural-images/card.md) opened the field on closed-set image identification; [`tang2023-semantic-reconstruction`](../research/collection/science/tang2023-semantic-reconstruction/card.md) and [`scotti2024-mindeye2`](../research/collection/science/scotti2024-mindeye2/card.md) push toward open-set reconstruction. Tang and Scotti both rely on per-subject feature spaces and do not test whether explicit HED tags or per-image semantic graphs as auxiliary supervision would reduce the per-subject calibration cost. The Tang card asks this directly: would explicit HED-grounded annotation augment LLM features? No paper to date has run that experiment because the augmented annotation layer does not exist outside of bespoke per-paper annotation drives.

### 2.3 Foundation models with annotation supervision (theme 5)

This is the most acute case. [`jiang2024-labram`](../research/collection/science/jiang2024-labram/card.md) and [`han2025-diver1`](../research/collection/science/han2025-diver1/card.md) are the first generation of large EEG and iEEG foundation models. [`xiong2025-eegfm-review`](../research/collection/science/xiong2025-eegfm-review/card.md) is a critical review of that generation showing they often fail to beat hand-engineered baselines on downstream tasks. The Xiong card identifies pretraining-without-annotation-supervision as a possibly missing ingredient. [`lahner2025-mosaic`](../research/collection/science/lahner2025-mosaic/card.md) extends the same critique to fMRI: the MOSAIC framework aggregates eight datasets but uses CLIP features rather than HED-tagged annotations as supervision, and the card flags that explicit HED-tagged annotations are not yet integrated.

The diagnosis is consistent. EEG foundation models scale parameters and channels but not the supervision. The supervision they would benefit from, dense per-stimulus annotations on naturalistic data with cross-modality coverage, exists in pieces (HBN-EEG, NSD-EEG-alljoined, NOD-EEG, THINGS-EEG2) but is not aggregated and not HED-tagged at scale. Building that aggregation is exactly what a Garden-style commons does.

### 2.4 Annotation-response curves and sufficiency (theme 6)

This is the theme the ANNOTATE R01 explicitly targets. [`antonello2023-scaling-laws`](../research/collection/science/antonello2023-scaling-laws/card.md) shows log-linear scaling of fMRI language encoding with data and model size; [`naspi2021-perceptual-semantic`](../research/collection/science/naspi2021-perceptual-semantic/card.md) shows that annotation granularity dissociates true and false memory traces in ventral-temporal cortex; [`lebel2023-natural-language-fmri`](../research/collection/science/lebel2023-natural-language-fmri/card.md) provides the open per-subject narrative-listening benchmark that future sufficiency work will run on.

What none of these papers has yet done, and what AGI is uniquely positioned to enable, is to vary annotation richness as an independent experimental variable while holding stimulus and model fixed. The reason that experiment has not run is operational: producing the same stimulus's annotations at five distinct richness levels is a cost no single lab is incentivized to pay. AGI's branches-as-layers model lets the cost be amortized across the community, and the resulting curves become a public scientific output rather than a methods appendix.

### 2.5 Cross-modal and cross-dataset generalization (theme 7)

[`cichy2014-resolving-object-recognition`](../research/collection/science/cichy2014-resolving-object-recognition/card.md) established MEG-fMRI fusion via representational similarity analysis on a shared object set; [`berezutskaya2022-multimodal-iEEG-fMRI`](../research/collection/science/berezutskaya2022-multimodal-iEEG-fMRI/card.md) provides the first open multimodal iEEG-fMRI dataset on a shared audiovisual stimulus; [`hebart2023-things-data`](../research/collection/science/hebart2023-things-data/card.md) covers fMRI, MEG, and EEG on the THINGS concept space; [`deheer2017-hierarchical-speech`](../research/collection/science/deheer2017-hierarchical-speech/card.md) introduces variance partitioning across spectral, articulatory, and semantic feature spaces.

Cross-modal alignment depends on the stimulus side being identical across modalities. Today that identity is enforced informally, by referencing the same paper or the same supplementary file. AGI's "stimulus as a repository" architectural commitment makes the identity formal: when the NSD images become a versioned repository with HED tags, the same tagged annotation layer propagates to the fMRI, iEEG, and EEG datasets that use those images, and the cross-modal alignment problem reduces to per-modality response decoding rather than re-annotation. The current NSD-fMRI plus NSD-iEEG plus NSD-EEG-alljoined triangle is the working proof of concept; AGI generalizes the pattern.

## 3. The annotation-agnostic themes that gain interpretability

### 3.1 ISC and hyperalignment (theme 3)

The classic ISC and hyperalignment literature is methodologically agnostic to annotation. [`hasson2004-intersubject-synchronization`](../research/collection/science/hasson2004-intersubject-synchronization/card.md) showed that movie viewing produces stimulus-locked synchrony across subjects; [`hasson2010-reliability`](../research/collection/science/hasson2010-reliability/card.md) framed reliability as a complement to amplitude; [`lerner2011-temporal-receptive-windows`](../research/collection/science/lerner2011-temporal-receptive-windows/card.md) used narrative scrambling to expose a TRW hierarchy. None requires annotations to operate.

What they require to *interpret* is a different matter. ISC says that regions co-fluctuate; it cannot say what makes them co-fluctuate. The TRW hierarchy says that long-window regions integrate over narrative timescales; it cannot say which narrative features they integrate. [`haxby2011-common-high-dim-model`](../research/collection/science/haxby2011-common-high-dim-model/card.md) and [`guntupalli2020-hyperalignment`](../research/collection/science/guntupalli2020-hyperalignment/card.md) build shared representational spaces that are powerful for cross-subject prediction but opaque for semantic interpretation. [`finn2020-idiosynchrony`](../research/collection/science/finn2020-idiosynchrony/card.md) extracts individual-difference signals from shared-response residuals, and the card explicitly notes that residual analyses cannot be pinned to specific stimulus features without machine-actionable annotations.

The annotation layer turns these methods from black-box predictors into hypothesis-generating tools. AGI does not change the methods themselves; it changes what those methods can say about brains.

### 3.2 Event segmentation and boundaries (theme 4)

Similar story. [`zacks2007-event-perception`](../research/collection/science/zacks2007-event-perception/card.md) is the verbal theory; [`baldassano2017-event-structure`](../research/collection/science/baldassano2017-event-structure/card.md) and [`geerligs2022-nested-hierarchy`](../research/collection/science/geerligs2022-nested-hierarchy/card.md) are the HMM-based imaging operationalizations; [`zheng2022-cognitive-boundaries`](../research/collection/science/zheng2022-cognitive-boundaries/card.md) and [`benyakov2018-hippocampal-film-editor`](../research/collection/science/benyakov2018-hippocampal-film-editor/card.md) are the single-unit and hippocampal companion findings. The Baldassano card flags directly that the HMM discovers events from brain data alone and does not validate against multi-perspective stimulus annotations. Adding the annotation layer would let the field test whether the HMM events correspond to visual cuts, semantic shifts, character changes, or none of the above.

The annotation layer also resolves a coordination problem. Single-rater boundary annotations have variable reliability (Ben-Yakov 2018 card); a multi-rater consensus annotation hosted in a versioned repository becomes a public good that every event-segmentation paper can use as ground truth, ending the per-paper re-annotation cycle.

## 4. NeuroScout as existence proof

The user's framing in [issue #1](https://github.com/Annotation-Garden/management/issues/1) explicitly cites [`neuroscout`](../research/collection/tools/neuroscout/card.md) as a project that could exploit richer annotations. NeuroScout is the closest existing precedent to what AGI proposes for the analysis side: a community resource that makes annotations of naturalistic stimuli first-class objects. Its scope is fMRI-only and its annotation layer is whatever [`pliers`](../research/collection/tools/pliers/card.md) extracts from the stimuli. The card for NeuroScout makes the relationship explicit: it is the closest existing template for the analysis side of an annotation commons, and a NeuroScout-AGI bridge in which AGI annotations become NeuroScout predictors is the obvious near-term collaboration.

NeuroScout proves the operational point. Once Pliers feature graphs were available for Forrest Gump, encoding-model analyses on Forrest Gump became routine instead of bespoke. The same lift, applied across more datasets, more modalities, and a richer annotation vocabulary than Pliers's automated extractors produce, is the AGI value proposition for the science strand.

## 5. The new-science roadmap

What ships first when annotation flows:

1. **Encoding-model libraries on canonical stimuli (theme 1)**. With HED-tagged events on NSD and on Forrest Gump, the standard voxel-wise pipeline becomes a one-line invocation against a shared feature graph. Labs that today cannot afford the annotation overhead can publish encoding-model results within weeks rather than months.
2. **Annotation-supervised foundation-model pretraining (theme 5)**. The Xiong 2025 critique becomes testable. A LaBraM-class model pretrained on HBN-EEG with HED supervision can be benchmarked against the same model pretrained without it, on the same downstream task suite. The current absence of that experiment is a corpus-availability problem, not a methodological one.
3. **Annotation-response curves at scale (theme 6)**. The ANNOTATE R01 produces the curves on NSD; AGI hosts the resulting annotation layers and replicates the experiment on second-wave datasets ([`bold5000`](../research/collection/data/bold5000/card.md), [`things-eeg2`](../research/collection/data/things-eeg2/card.md), [`narratives-pieman`](../research/collection/data/narratives-pieman/card.md), [`moth-radio-hour`](../research/collection/data/moth-radio-hour/card.md), [`little-prince-fmri`](../research/collection/data/little-prince-fmri/card.md)) without each replication being a separate methods paper.
4. **Cross-modal alignment papers (theme 7)**. The NSD-fMRI plus NSD-iEEG plus NSD-EEG-alljoined triangle generalizes to Forrest Gump (the studyforrest 7T fMRI plus the 3T variants plus the MEG release plus eye-gaze) once the annotation layer is shared. THINGS-data plus NOD-EEG plus THINGS-EEG2 becomes the same kind of triangle for static images.
5. **Annotation-decomposed ISC and event-segmentation papers (themes 3 and 4)**. Once a HED-tagged layer exists, the move from "regions co-fluctuate" to "regions co-fluctuate during character-emotion shifts" is a few lines of code rather than a new annotation campaign.

The order is approximate; the dependencies are real. Theme 1 ships first because the analytic infrastructure is already mature and waiting on annotation. Theme 5 ships next because the foundation-model literature is the loudest current demand for annotation-supervised pretraining data. Theme 6 ships in coordinated parallel with the ANNOTATE R01. Themes 7, 3, and 4 follow.

## 6. Coordination with ANNOTATE

The relationship is documented in detail in [`scope-diagram`](../research/synthesis/scope-diagram.md). The short form: ANNOTATE is the empirical engine that produces the annotation-response curves and the HEDit annotation client; AGI is the durable distribution layer that hosts the resulting annotations as versioned repositories and extends the work to datasets and modalities ANNOTATE cannot reach within a five-year three-modality three-dataset grant. The two projects are complementary, not competing, and the parallel construction of empirical findings (ANNOTATE) and durable infrastructure (AGI) is the single most important strategic argument for AGI's existence.

## 7. What this paper is not

It is not a literature review of every annotation-related paper in cognitive neuroscience. The Phase 1 [`science-map`](../research/synthesis/science-map.md) is the inventory; this is the thesis. It is also not a methods paper. The empirical work that turns the thesis into a number lives in ANNOTATE, in NeuroScout, and in the next generation of annotation-supervised foundation models. AGI's job is to make sure the infrastructure exists when those papers are ready to write.

## References

Citations resolve to BibTeX keys in [`../research/collection/science/science.bib`](../research/collection/science/science.bib) and [`../research/collection/data/data.bib`](../research/collection/data/data.bib) and [`../research/collection/tools/tools.bib`](../research/collection/tools/tools.bib). Direct paper-card links are above; the keys here are for downstream manuscript export.

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

Data (Strand B):
- `allen2022massive`, [`nsd-fmri`](../research/collection/data/nsd-fmri/card.md)
- `chang2019bold5000`, [`bold5000`](../research/collection/data/bold5000/card.md)
- `gifford2022thingseeg2`, [`things-eeg2`](../research/collection/data/things-eeg2/card.md)
- `huth2016moth`, [`moth-radio-hour`](../research/collection/data/moth-radio-hour/card.md)
- `li2022littleprince`, [`little-prince-fmri`](../research/collection/data/little-prince-fmri/card.md)
- `nastase2021narratives`, [`narratives-pieman`](../research/collection/data/narratives-pieman/card.md)
