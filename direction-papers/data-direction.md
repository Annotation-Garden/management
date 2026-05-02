# Data Direction, Dataset Coverage and the Cognitive-Task Wedge

A focused review on the data strand of the Annotation Garden Initiative (AGI). This paper surveys the dataset landscape catalogued in the Phase 1 corpus, defends an explicit tier policy for which datasets become AGI repositories at which milestone, and argues that the cognitive-task wedge is the part of AGI's coverage that diverges most sharply from the ANNOTATE R01 and from prior community framings of stimulus annotation.

Abbreviations: Brain Imaging Data Structure (BIDS), Hierarchical Event Descriptors (HED), Natural Scenes Dataset (NSD), Healthy Brain Network (HBN), Human Connectome Project (HCP), Adolescent Brain Cognitive Development (ABCD), Amsterdam Open MRI Collection (AOMIC), data-use agreement (DUA), magnetoencephalography (MEG), electroencephalography (EEG), intracranial EEG (iEEG), functional magnetic resonance imaging (fMRI).

## 1. Introduction

### 1.1 The dataset side of the annotation lifecycle

Every annotation effort presupposes a dataset to annotate. The white paper and the science direction paper both argue that AGI's distinctive contribution is the substrate for community-curated annotation layers; the data direction paper asks the complementary question: which datasets does AGI annotate, in which order, and on what evidentiary basis?

The Phase 1 corpus collected 36 dataset entries spanning four classes of stimulus (image, video, audio, multi-task) and a sixth catch-all class for hybrid paradigms and single-stimulus localizers. The Phase 2 [`dataset-hierarchy`](../research/synthesis/dataset-hierarchy.md) places each entry on six axes: stimulus type, modality coverage, annotation density, sample size, copyright tier, and AGI flagship status. The single most useful empirical observation in the synthesis is that annotation density and sample size are inversely correlated across the corpus: every entry with rich annotations has fewer than thirty subjects, and every entry with more than a thousand subjects has minimal or moderate annotation density. The single exception ([`hbn-eeg`](../research/collection/data/hbn-eeg/card.md)) is rich and large and is the canonical AGI proof of concept.

### 1.2 Gap statement

The current AGI white paper proposes three flagship stimulus repositories (NSD, studyforrest, HBN movies). The ANNOTATE R01 proposes three datasets (NSD, HBN-EEG, studyforrest). Both framings are naturalistic-stimulus only. Neither addresses the cognitive-task batteries, the second-wave naturalistic datasets, the localizers, or the hybrid paradigms that make up the bulk of the corpus. The Phase 1 collection therefore exposes a coverage gap that neither prior framing has named.

### 1.3 Thesis

This paper argues that AGI's dataset coverage tiers should be explicit and principled. The current flagships demonstrate the pattern; the second-wave extends it; the cognitive-task wedge is where AGI's coverage divergence is most consequential. Section 2 reviews the dataset landscape category by category, drawing on the Phase 2 [`dataset-hierarchy`](../research/synthesis/dataset-hierarchy.md). Section 3 defends the under-annotated-relative-to-potential thesis using five exemplars where neural data is rich and stimulus annotation is thin. Section 4 introduces the cognitive-task wedge as the largest concrete coverage gap and the highest-leverage AGI-distinctive contribution. Section 5 walks the hybrid datasets that bridge the cognitive-task and naturalistic wedges. Section 6 specifies the rollout map. Section 7 discusses interpretation, limitations, and counterarguments. Section 8 concludes.

## 2. Background, the dataset landscape

The 36 entries collected in [`research/collection/data/`](../research/collection/data/) sort into six categories already used by the Phase 2 [`dataset-hierarchy`](../research/synthesis/dataset-hierarchy.md). This section summarizes each category at the policy level.

**Naturalistic, static images.** Single-image stimuli paired with rich neuroimaging form the cleanest end of the corpus. The image is a stable referent, so annotation layers (object segmentation, captions, affect, HED tags) propagate cleanly across modalities. NSD ([`nsd-fmri`](../research/collection/data/nsd-fmri/card.md), [`nsd-ieeg`](../research/collection/data/nsd-ieeg/card.md), [`nsd-eeg-alljoined`](../research/collection/data/nsd-eeg-alljoined/card.md)) and the THINGS family ([`things-initiative`](../research/collection/data/things-initiative/card.md), [`things-eeg2`](../research/collection/data/things-eeg2/card.md), [`nod-eeg`](../research/collection/data/nod-eeg/card.md)) anchor the category. BOLD5000 ([`bold5000`](../research/collection/data/bold5000/card.md)) provides 3T-accessible data with thinner annotation. COCO ([`coco`](../research/collection/data/coco/card.md)) is the upstream stimulus source for NSD and several siblings.

**Naturalistic, video and film.** Long-form audiovisual stimuli have the largest annotation surface (shot boundaries, character identity, emotion, theory-of-mind events, dialogue, sound design) of any class. The studyforrest project ([`studyforrest`](../research/collection/data/studyforrest/card.md), [`studyforrest-eyegaze`](../research/collection/data/studyforrest-eyegaze/card.md)) is the deepest community annotation effort to date. The HBN family ([`hbn-mri`](../research/collection/data/hbn-mri/card.md), [`hbn-eeg`](../research/collection/data/hbn-eeg/card.md)) is the largest cohort. The Bang family ([`bang-ieeg-fmri`](../research/collection/data/bang-ieeg-fmri/card.md), [`bang-multimodal`](../research/collection/data/bang-multimodal/card.md)) provides multimodal short-clip recordings at gold-standard precision. The Naturalistic Neuroimaging Database ([`naturalistic-neuroimaging-db`](../research/collection/data/naturalistic-neuroimaging-db/card.md)), Courtois NeuroMod ([`courtois-neuromod`](../research/collection/data/courtois-neuromod/card.md)), Sherlock-fMRI ([`sherlock-fmri`](../research/collection/data/sherlock-fmri/card.md)), and Inscapes ([`inscapes`](../research/collection/data/inscapes/card.md)) round out the category at varying density.

**Naturalistic, audio and narrative.** Narratives-Pieman ([`narratives-pieman`](../research/collection/data/narratives-pieman/card.md)) is the largest open spoken-narrative corpus (345 subjects across 27 stories). Moth-Radio-Hour ([`moth-radio-hour`](../research/collection/data/moth-radio-hour/card.md)) is the canonical reference for continuous-language encoding. Little-Prince-fMRI ([`little-prince-fmri`](../research/collection/data/little-prince-fmri/card.md)) provides cross-lingual replication. Natural-Sounds-fMRI ([`natural-sounds-fmri`](../research/collection/data/natural-sounds-fmri/card.md)) covers environmental sounds and music.

**Cognitive task batteries.** Six entries anchor this category: HCP-task ([`hcp-task`](../research/collection/data/hcp-task/card.md)), HCP-D ([`hcp-d-development`](../research/collection/data/hcp-d-development/card.md)), ABCD-task ([`abcd-task`](../research/collection/data/abcd-task/card.md)), Cam-CAN ([`cam-can`](../research/collection/data/cam-can/card.md)), AOMIC ([`aomic`](../research/collection/data/aomic/card.md)), and MyConnectome ([`myconnectome`](../research/collection/data/myconnectome/card.md)). Combined sample size is greater than 16,500 across the first five entries.

**Hybrid paradigms.** LEMON-MPI ([`lemon-mpi`](../research/collection/data/lemon-mpi/card.md)), dHCP ([`dhcp`](../research/collection/data/dhcp/card.md)), DEAP ([`deap`](../research/collection/data/deap/card.md)), and SEED ([`seed`](../research/collection/data/seed/card.md)) span task, rest, and naturalistic content within a single subject visit.

**Single-stimulus benchmarks.** Three localizer cohorts: Fedorenko-language ([`fedorenko-language-localizer`](../research/collection/data/fedorenko-language-localizer/card.md)), Pinel ([`pinel-localizer`](../research/collection/data/pinel-localizer/card.md)), and the Brainomics deployment ds000114 ([`localizer-ds000114`](../research/collection/data/localizer-ds000114/card.md), 1,311 subjects).

## 3. The under-annotated-relative-to-potential thesis

Five datasets in the corpus are paradigmatic exemplars of large neural data with thin stimulus annotation. They illustrate the gap that AGI's branches-as-layers model is designed to close.

[`hbn-mri`](../research/collection/data/hbn-mri/card.md) combines naturalistic movie viewing with developmental phenotyping at unprecedented scale (more than 5,000 subjects, ages 5 to 21). The neural side is rich: 3T fMRI, structural MRI, diffusion-weighted imaging, EEG, and behavioral phenotyping. The stimulus side is essentially "movie identifier and onset". A community-curated HED-tagged scene-and-character annotation layer would convert HBN-MRI into a developmental-trajectory benchmark for almost every theme in the [`science-map`](../research/synthesis/science-map.md), from event segmentation through semantic encoding.

[`bold5000`](../research/collection/data/bold5000/card.md) has 5,000 mixed Common Objects in Context, Scenes Understanding, and ImageNet images and four deeply-sampled subjects under a Creative Commons BY-4.0 license. The neural side is mature 3T fMRI; the annotation side is moderate at best. A HED layer plus per-image semantic tags would let BOLD5000 function as the 3T accessible sibling to NSD across the many labs that cannot reach the 7T data, but today it is mostly used as a methods-validation set.

[`abcd-task`](../research/collection/data/abcd-task/card.md) is the largest paediatric task fMRI study to date, with 11,800 subjects and three canonical paradigms (monetary incentive delay, n-back, stop-signal). The events are released as TSV files with custom column names and zero HED tags. A community-curated HED Generation 3 sidecar set would propagate across thousands of fMRI re-analyses without changing a single line of imaging-pipeline code.

[`naturalistic-neuroimaging-db`](../research/collection/data/naturalistic-neuroimaging-db/card.md) has 86 subjects watching 10 feature films and almost no annotation. The films are well-known commercial titles, so a pointer-architecture solution analogous to HBN movies would unlock community contribution without redistribution issues.

[`inscapes`](../research/collection/data/inscapes/card.md) is a paradigmatic exemplar (low-arousal abstract animation as a halfway point between rest and naturalistic) but has minimal annotation. It earns "reference-only" status in the [`dataset-hierarchy`](../research/synthesis/dataset-hierarchy.md) only because the annotation deficit is so severe.

The pattern is uniform: the neural data is mature, the imaging quality is high, and the annotation layer is the bottleneck. Across all five exemplars, no single lab has commercial or academic incentive to absorb the annotation cost in service of the broader community. AGI's commitment is to host the substrate so the cost can be amortized.

## 4. The cognitive-task wedge

The current AGI white paper's three flagships and the ANNOTATE R01's three datasets are all naturalistic-stimulus datasets. Yet the corpus contains five canonical cognitive-task batteries that together carry combined sample size greater than 16,000 subjects, plus the deep-sampling single-subject MyConnectome cohort and three single-stimulus localizers, all with zero community-curated HED Generation 3 sidecars across the entire group. The sub-categories follow the [`dataset-hierarchy`](../research/synthesis/dataset-hierarchy.md) taxonomy.

**Cognitive-task batteries** (six entries): [`hcp-task`](../research/collection/data/hcp-task/card.md) (1,200 subjects, seven canonical adult tasks), [`hcp-d-development`](../research/collection/data/hcp-d-development/card.md) (1,300 subjects, developmental complement, ages 5 to 21), [`abcd-task`](../research/collection/data/abcd-task/card.md) (11,800 subjects, three paediatric paradigms), [`cam-can`](../research/collection/data/cam-can/card.md) (700 subjects, lifespan multimodal cognitive battery with both fMRI and MEG), [`aomic`](../research/collection/data/aomic/card.md) (1,500-plus subjects, three deposits combining cognitive task and naturalistic-meets-task hybrid content), and [`myconnectome`](../research/collection/data/myconnectome/card.md) (single-subject deep-sampling, 105 sessions).

**Single-stimulus localizers** (three entries): [`fedorenko-language-localizer`](../research/collection/data/fedorenko-language-localizer/card.md) (the reference language localizer), [`pinel-localizer`](../research/collection/data/pinel-localizer/card.md) (the canonical multi-task ten-paradigm localizer), and [`localizer-ds000114`](../research/collection/data/localizer-ds000114/card.md) (the Brainomics 1,311-subject mass deployment of the Pinel battery).

Every one of these datasets has well-defined event vocabularies (a handful of trial types per task), wide community use, and stable BIDS-conformant releases. The marginal cost of producing a community-blessed HED Generation 3 sidecar per task is low. The marginal benefit is large because every cognitive-neuroscience paper using these datasets would inherit the annotation. AOMIC is the lowest-friction on-ramp among the batteries because it is fully open under CC-BY-4.0 with no data-use agreement; the three localizers are each one-PR contributions because the stimulus materials are openly released.

The cognitive-task wedge is the single most important divergence between AGI and prior framings of stimulus annotation. It is not in the white paper; it is not in the R01; it is not in the synthesis briefs of the FAIR neuroscience commons. The Phase 2 [`gap-analysis`](../research/synthesis/gap-analysis.md) names it as Gap 1, the highest-leverage AGI-distinctive contribution. Bringing the wedge under AGI's repository convention gives the field a deliverable nobody else is positioned to produce.

## 5. Hybrid datasets bridge the wedges

LEMON-MPI ([`lemon-mpi`](../research/collection/data/lemon-mpi/card.md)), DEAP ([`deap`](../research/collection/data/deap/card.md)), SEED ([`seed`](../research/collection/data/seed/card.md)), and HBN-EEG ([`hbn-eeg`](../research/collection/data/hbn-eeg/card.md)) span task, rest, and naturalistic content within a single subject visit. HBN-EEG already proves that the same HED sidecar machinery handles all three modalities of paradigm in a single repository: scene boundaries from movie viewing, surround-suppression events, contrast-change-detection events, and sequence-learning events all coexist as separate annotation layers under one stimulus-anchored repository.

The hybrid datasets are the methodological bridge between the cognitive-task wedge and the naturalistic-flagship core. AGI repositories hosting them establish that the same tooling, the same governance, and the same per-stimulus repository convention extend across the entire stimulus space. Once that pattern is normalized, naturalistic-only and task-only framings of stimulus annotation become legacy framings.

## 6. The rollout map

Pulling directly from the [`dataset-hierarchy`](../research/synthesis/dataset-hierarchy.md) flagship-status column.

**Phase 1, current white-paper flagships (3 stimulus repositories collapsing 7 dataset entries).** The NSD images repository hosts [`nsd-fmri`](../research/collection/data/nsd-fmri/card.md), [`nsd-ieeg`](../research/collection/data/nsd-ieeg/card.md), [`nsd-eeg-alljoined`](../research/collection/data/nsd-eeg-alljoined/card.md), with [`coco`](../research/collection/data/coco/card.md) as the upstream stimulus source. The studyforrest repository hosts [`studyforrest`](../research/collection/data/studyforrest/card.md) and [`studyforrest-eyegaze`](../research/collection/data/studyforrest-eyegaze/card.md). The HBN movies repository hosts annotations referenced by both [`hbn-eeg`](../research/collection/data/hbn-eeg/card.md) and [`hbn-mri`](../research/collection/data/hbn-mri/card.md).

**Phase 2 candidates, extensible from current flagships.** [`narratives-pieman`](../research/collection/data/narratives-pieman/card.md) extends the audio-narrative side with 345 subjects across 27 stories and an existing HED-LANG sidecar template that AGI can adopt with minimal modification. [`naturalistic-neuroimaging-db`](../research/collection/data/naturalistic-neuroimaging-db/card.md) extends the video-film side with 86 subjects across 10 feature films, demonstrating the pointer-architecture protocol on commercial titles other than HBN movies. [`courtois-neuromod`](../research/collection/data/courtois-neuromod/card.md) extends the deep-sampling pattern of NSD into the video domain with hundreds of hours per subject.

**Second-wave repositories.** Static-image strand: [`things-initiative`](../research/collection/data/things-initiative/card.md), [`nod-eeg`](../research/collection/data/nod-eeg/card.md), [`things-eeg2`](../research/collection/data/things-eeg2/card.md), [`bold5000`](../research/collection/data/bold5000/card.md). Video strand: [`bang-ieeg-fmri`](../research/collection/data/bang-ieeg-fmri/card.md), [`bang-multimodal`](../research/collection/data/bang-multimodal/card.md), [`sherlock-fmri`](../research/collection/data/sherlock-fmri/card.md). Audio strand: [`moth-radio-hour`](../research/collection/data/moth-radio-hour/card.md), [`little-prince-fmri`](../research/collection/data/little-prince-fmri/card.md). Cognitive-task wedge: [`hcp-task`](../research/collection/data/hcp-task/card.md), [`hcp-d-development`](../research/collection/data/hcp-d-development/card.md), [`abcd-task`](../research/collection/data/abcd-task/card.md), [`cam-can`](../research/collection/data/cam-can/card.md), [`aomic`](../research/collection/data/aomic/card.md), with AOMIC first because of license openness and ABCD-task next because of cohort scale. Localizers: [`fedorenko-language-localizer`](../research/collection/data/fedorenko-language-localizer/card.md), [`pinel-localizer`](../research/collection/data/pinel-localizer/card.md), [`localizer-ds000114`](../research/collection/data/localizer-ds000114/card.md), one PR per localizer with HED sidecar plus stimulus-pointer. Hybrid: [`lemon-mpi`](../research/collection/data/lemon-mpi/card.md) as the cleanest open hybrid for demonstrating multi-paradigm-per-repository.

**Reference-only entries.** [`coco`](../research/collection/data/coco/card.md) (stimulus source already covered upstream), [`glmsingle-paper`](../research/collection/data/glmsingle-paper/card.md) (methods reference), [`inscapes`](../research/collection/data/inscapes/card.md) (paradigmatic exemplar but minimal annotation), [`myconnectome`](../research/collection/data/myconnectome/card.md) (single-subject), [`natural-sounds-fmri`](../research/collection/data/natural-sounds-fmri/card.md), [`dhcp`](../research/collection/data/dhcp/card.md), [`deap`](../research/collection/data/deap/card.md), [`seed`](../research/collection/data/seed/card.md).

## 7. Discussion

### 7.1 Coordination with the science direction

The science strand argues that five of the seven Strand C themes are gated by annotation supply. The dataset-rollout sequencing in Section 6 is the operational complement: each science-thesis claim becomes testable when the corresponding dataset gets a HED-tagged annotation layer.

- Encoding-model libraries on canonical stimuli mature once NSD and Forrest Gump and Moth-Radio-Hour carry community-versioned annotation layers.
- Annotation-supervised foundation-model pretraining matures once HBN-EEG plus NSD-EEG-alljoined plus NOD-EEG plus THINGS-EEG2 are aggregated with shared HED tags.
- Annotation-response curves at scale mature once the ANNOTATE R01 produces the curves on NSD and AGI replicates the experiment on second-wave datasets.
- Cross-modal alignment papers mature once the NSD triangle generalizes to the studyforrest quartet and the THINGS triangle.
- Annotation-decomposed ISC and event-segmentation papers mature once Sherlock and Bang carry HED-tagged scene-boundary and character-emotion annotation layers.

The dataset-side investment unlocks the science-side claims. The reverse is also true: each scientific success on a particular dataset attracts contribution and use of the corresponding AGI repository, which feeds the next round of annotation richness. The Wikipedia analogy from [`VISION.md`](../VISION.md) captures the dynamic.

### 7.2 Copyright tier handling

Twenty-one of the 36 dataset entries are fully open. Thirteen are restricted by data-use agreement. Two are pointer-required for stimulus distribution. The white paper's pointer-based architecture handles the pointer tier cleanly: AGI hosts unique identifiers, timestamps, and annotations while annotations reference publicly available copies of the stimulus. The DUA tier is harder. Datasets like [`courtois-neuromod`](../research/collection/data/courtois-neuromod/card.md), [`bang-multimodal`](../research/collection/data/bang-multimodal/card.md), and [`sherlock-fmri`](../research/collection/data/sherlock-fmri/card.md) have rich annotation potential and restricted distribution constraints simultaneously. The solution is a federation protocol with three explicit tiers (open, pointer-only, federated) that this paper names but that an upcoming governance document will specify.

### 7.3 Limitations

This paper documents the dataset-coverage strategy but does not implement any of the AGI repositories. The implementation is scoped wave by wave by the [`tools-direction`](./tools-direction.md) build order. The rollout map in Section 6 reflects the corpus's coverage, not the universe of relevant datasets; entries the corpus did not include (Algonauts, ECoG-libet, the various OpenNeuro single-task collections beyond ds000114) will land in repositories on their own merits when contributors propose them. The empirical case for the under-annotated-relative-to-potential thesis is qualitative: it identifies five exemplars where the gap is severe, but it does not estimate the rate at which annotation richness translates into downstream-paper output.

A second limitation is that the cognitive-task-wedge argument assumes that HED Generation 3 sidecars on canonical task batteries will see broad uptake. The assumption is plausible because the marginal cost is low and the BIDS-conformant releases of the underlying datasets already exist. But uptake depends on reanalysis-paper authors learning that the sidecars exist and consuming them; documentation, tutorials, and integration into the standard analysis pipelines all matter.

### 7.4 Future work

The forward-looking experiments are: (a) measure the per-paper annotation cost on representative naturalistic-stimulus datasets to baseline the lift AGI provides; (b) track adoption of community-curated HED sidecars on the cognitive-task wedge by observing reanalysis-paper citations; (c) evaluate whether the federation protocol unlocks DUA-restricted datasets that today have no realistic public-annotation path. None of these experiments require methodological innovation; all of them require AGI repositories to exist as the measurement surface.

### 7.5 Anticipated objection

A reader could argue that the cognitive-task wedge is methodologically uninteresting because cognitive-task batteries have well-defined event vocabularies that need only minor schema work, and that the annotation density is intrinsically low. The first half of the argument is precisely the reason the wedge is high-leverage: low marginal cost per HED sidecar plus broad reanalysis impact equals best-in-class return on annotation effort. The second half misses the point: low annotation density is fine for tasks; what is missing is the *standardization* of even that minimal density across labs, which is exactly what HED Generation 3 provides and what no community-versioned repository today hosts.

## 8. Conclusion

AGI's dataset coverage tiers are explicit and principled. Phase 1 hosts the three flagships of the white paper. Phase 2 candidates extend along the audio-narrative, video-film, and deep-sampling axes. The second wave covers eighteen entries spanning static-image, video, audio, cognitive-task, hybrid, and localizer categories. The cognitive-task wedge in particular is the single highest-leverage AGI-distinctive contribution because it lifts more than 16,000 subjects of community data into the BIDS-plus-HED commons that no prior framing of stimulus annotation has reached. The dataset direction of AGI is therefore not naturalistic-stimulus-only but stimulus-general: the same Stim-BIDS plus HED machinery handles every entry in the corpus, and the rollout map sequences contributions to maximize impact within the substrate the white paper and the tools direction together specify.

## References

Citations resolve to BibTeX keys in [`../research/collection/data/data.bib`](../research/collection/data/data.bib). Direct paper-card links appear inline in the prose; the keys here are for downstream manuscript export.

Naturalistic, static images:
- `allen2022massive`, [`nsd-fmri`](../research/collection/data/nsd-fmri/card.md)
- `huang2024nsdieeg`, [`nsd-ieeg`](../research/collection/data/nsd-ieeg/card.md)
- `xu2024alljoined`, [`nsd-eeg-alljoined`](../research/collection/data/nsd-eeg-alljoined/card.md)
- `hebart2023things`, [`things-initiative`](../research/collection/data/things-initiative/card.md)
- `nodeeg2025`, [`nod-eeg`](../research/collection/data/nod-eeg/card.md)
- `gifford2022thingseeg2`, [`things-eeg2`](../research/collection/data/things-eeg2/card.md)
- `chang2019bold5000`, [`bold5000`](../research/collection/data/bold5000/card.md)
- `lin2014coco`, [`coco`](../research/collection/data/coco/card.md)
- `prince2022glmsinglepaper`, [`glmsingle-paper`](../research/collection/data/glmsingle-paper/card.md)

Naturalistic, video and film:
- `hanke2014studyforrest`, [`studyforrest`](../research/collection/data/studyforrest/card.md)
- `hanke2016eyegaze`, [`studyforrest-eyegaze`](../research/collection/data/studyforrest-eyegaze/card.md)
- `alexander2017hbn`, [`hbn-mri`](../research/collection/data/hbn-mri/card.md)
- `shirazi2024hbneeg`, [`hbn-eeg`](../research/collection/data/hbn-eeg/card.md)
- `aly2022bang`, [`bang-ieeg-fmri`](../research/collection/data/bang-ieeg-fmri/card.md)
- `zheng2024bangmultimodal`, [`bang-multimodal`](../research/collection/data/bang-multimodal/card.md)
- `aliko2020nndb`, [`naturalistic-neuroimaging-db`](../research/collection/data/naturalistic-neuroimaging-db/card.md)
- `boyleneuromod2022`, [`courtois-neuromod`](../research/collection/data/courtois-neuromod/card.md)
- `chen2017sherlock`, [`sherlock-fmri`](../research/collection/data/sherlock-fmri/card.md)
- `vanderwal2015inscapes`, [`inscapes`](../research/collection/data/inscapes/card.md)

Naturalistic, audio and narrative:
- `nastase2021narratives`, [`narratives-pieman`](../research/collection/data/narratives-pieman/card.md)
- `huth2016moth`, [`moth-radio-hour`](../research/collection/data/moth-radio-hour/card.md)
- `li2022littleprince`, [`little-prince-fmri`](../research/collection/data/little-prince-fmri/card.md)
- `normanhaignere2015`, [`natural-sounds-fmri`](../research/collection/data/natural-sounds-fmri/card.md)

Cognitive task batteries:
- `barch2013hcp`, [`hcp-task`](../research/collection/data/hcp-task/card.md)
- `somerville2018hcpd`, [`hcp-d-development`](../research/collection/data/hcp-d-development/card.md)
- `casey2018abcd`, [`abcd-task`](../research/collection/data/abcd-task/card.md)
- `shafto2014camcan`, [`cam-can`](../research/collection/data/cam-can/card.md)
- `snoek2021aomic`, [`aomic`](../research/collection/data/aomic/card.md)
- `poldrack2015myconnectome`, [`myconnectome`](../research/collection/data/myconnectome/card.md)

Hybrid and single-stimulus benchmarks:
- `babayan2019lemon`, [`lemon-mpi`](../research/collection/data/lemon-mpi/card.md)
- `makropoulos2018dhcp`, [`dhcp`](../research/collection/data/dhcp/card.md)
- `koelstra2012deap`, [`deap`](../research/collection/data/deap/card.md)
- `zheng2015seed`, [`seed`](../research/collection/data/seed/card.md)
- `fedorenko2010localizer`, [`fedorenko-language-localizer`](../research/collection/data/fedorenko-language-localizer/card.md)
- `pinel2007localizer`, [`pinel-localizer`](../research/collection/data/pinel-localizer/card.md)
- `localizer000114`, [`localizer-ds000114`](../research/collection/data/localizer-ds000114/card.md)
