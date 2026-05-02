# Data Direction, Dataset Coverage and the Cognitive-Task Wedge

A focused mini lit review on the data strand of the Annotation Garden Initiative (AGI). Walks the dataset landscape catalogued in the Phase 1 corpus, defends an explicit tier policy for which datasets become AGI repositories at which milestone, and argues that the cognitive-task wedge is where AGI's coverage diverges most sharply from the ANNOTATE R01.

Abbreviations: Brain Imaging Data Structure (BIDS), Hierarchical Event Descriptors (HED), Natural Scenes Dataset (NSD), Healthy Brain Network (HBN), Human Connectome Project (HCP), Adolescent Brain Cognitive Development (ABCD), Amsterdam Open MRI Collection (AOMIC), data-use agreement (DUA), magnetoencephalography (MEG), electroencephalography (EEG), intracranial EEG (iEEG), functional magnetic resonance imaging (fMRI).

## 1. The dataset landscape, in one paragraph

The Phase 1 corpus collected 36 dataset entries spanning four classes of stimulus (image, video, audio, multi-task) and a sixth catch-all class for hybrid paradigms and single-stimulus localizers. The Phase 2 [`dataset-hierarchy`](../research/synthesis/dataset-hierarchy.md) places each entry on six axes: stimulus type, modality coverage, annotation density, sample size, copyright tier, and AGI flagship status. The single most useful observation is that annotation density and sample size are inversely correlated across the corpus: every entry with rich annotations has fewer than thirty subjects, and every entry with more than a thousand subjects has minimal or moderate annotation density. The single exception, [`hbn-eeg`](../research/collection/data/hbn-eeg/card.md), is the canonical AGI proof of concept: rich and large.

The argument of this direction paper is that AGI's job is to flip that correlation. The infrastructure exists to combine dense annotations with large cohorts; the operational pattern that today blocks the combination is the one-paper-one-annotation-effort cycle. AGI's branches-as-layers model amortizes the annotation effort across the community, and the rollout phasing below specifies which datasets get the treatment first.

## 2. The under-annotated-relative-to-potential thesis

Five datasets in the corpus are paradigmatic exemplars of large neural data with thin stimulus annotation:

[`hbn-mri`](../research/collection/data/hbn-mri/card.md) combines naturalistic movie viewing with developmental phenotyping at unprecedented scale (more than 5,000 subjects, ages 5 to 21). The neural side is rich: 3T fMRI, structural MRI, diffusion-weighted imaging, EEG, and behavioral phenotyping. The stimulus side is essentially "movie identifier and onset". A community-curated HED-tagged scene-and-character annotation layer would convert HBN-MRI into a developmental-trajectory benchmark for almost every theme in the [`science-map`](../research/synthesis/science-map.md), from event segmentation through semantic encoding.

[`bold5000`](../research/collection/data/bold5000/card.md) has 5,000 mixed Common Objects in Context, Scenes Understanding, and ImageNet images and four deeply-sampled subjects under a Creative Commons BY-4.0 license. The neural side is mature 3T fMRI; the annotation side is moderate at best. A HED layer plus per-image semantic tags would let BOLD5000 function as the 3T accessible sibling to NSD across the many labs that cannot reach the 7T data, but today it is mostly used as a methods-validation set.

[`abcd-task`](../research/collection/data/abcd-task/card.md) is the largest paediatric task fMRI study to date, with 11,800 subjects and three canonical paradigms (monetary incentive delay, n-back, stop-signal). The events are released as TSV files with custom column names and zero HED tags. A community-curated HED Generation 3 sidecar set would propagate across thousands of fMRI re-analyses without changing a single line of imaging-pipeline code.

[`naturalistic-neuroimaging-db`](../research/collection/data/naturalistic-neuroimaging-db/card.md) has 86 subjects watching 10 feature films and almost no annotation. The films are well-known commercial titles, so a pointer-architecture solution analogous to HBN movies would unlock community contribution without redistribution issues.

[`inscapes`](../research/collection/data/inscapes/card.md) is a paradigmatic exemplar (low-arousal abstract animation as a halfway point between rest and naturalistic) but has minimal annotation. It earns "reference-only" status in the [`dataset-hierarchy`](../research/synthesis/dataset-hierarchy.md) only because the annotation deficit is so severe.

The pattern is uniform: the neural data is mature, the imaging quality is high, and the annotation layer is the bottleneck.

## 3. The cognitive-task wedge

The current AGI white paper's three flagships (NSD, StudyForrest, HBN movies) are all naturalistic-stimulus datasets. The ANNOTATE R01's three datasets are likewise all naturalistic. Yet the corpus contains nine cognitive-task entries with combined sample size greater than 16,000 subjects and zero community-curated HED Generation 3 sidecars.

The entries: [`hcp-task`](../research/collection/data/hcp-task/card.md) (1,200 subjects, seven canonical adult tasks), [`hcp-d-development`](../research/collection/data/hcp-d-development/card.md) (1,300 subjects, developmental complement, ages 5 to 21), [`abcd-task`](../research/collection/data/abcd-task/card.md) (11,800 subjects, three paediatric paradigms), [`cam-can`](../research/collection/data/cam-can/card.md) (700 subjects, lifespan multimodal cognitive battery with both fMRI and MEG), [`aomic`](../research/collection/data/aomic/card.md) (1,500-plus subjects, three deposits combining cognitive task and naturalistic-meets-task hybrid content), [`myconnectome`](../research/collection/data/myconnectome/card.md) (single-subject deep-sampling, 105 sessions), [`fedorenko-language-localizer`](../research/collection/data/fedorenko-language-localizer/card.md) (the reference language localizer), [`pinel-localizer`](../research/collection/data/pinel-localizer/card.md) (the canonical multi-task ten-paradigm localizer), and [`localizer-ds000114`](../research/collection/data/localizer-ds000114/card.md) (the Brainomics 1,311-subject mass deployment of the Pinel battery).

Every one of these datasets has well-defined event vocabularies (a handful of trial types per task), wide community use, and stable BIDS-conformant releases. The marginal cost of producing a community-blessed HED Generation 3 sidecar per task is low. The marginal benefit is large because every cognitive-neuroscience paper using these datasets would inherit the annotation. AOMIC is the lowest-friction on-ramp because it is fully open under CC-BY-4.0 with no data-use agreement.

The cognitive-task wedge is the single highest-leverage AGI-distinctive contribution per the [`gap-analysis`](../research/synthesis/gap-analysis.md). Neither the white paper nor the R01 covers it; the corpus shows the demand; the infrastructure for hosting it is the same Stim-BIDS plus HED machinery that handles the naturalistic flagships.

## 4. Hybrid datasets bridge the wedges

[`lemon-mpi`](../research/collection/data/lemon-mpi/card.md), [`deap`](../research/collection/data/deap/card.md), [`seed`](../research/collection/data/seed/card.md), and [`hbn-eeg`](../research/collection/data/hbn-eeg/card.md) span task, rest, and naturalistic content within a single subject visit. HBN-EEG already proves that the same HED sidecar machinery handles all three modalities of paradigm in a single repository: scene boundaries from movie viewing, surround-suppression events, contrast-change-detection events, and sequence-learning events all coexist as separate annotation layers under one stimulus-anchored repository.

The hybrid datasets are the methodological bridge between the cognitive-task wedge and the naturalistic-flagship core. AGI repositories hosting them establish that the same tooling, the same governance, and the same per-stimulus repository convention extend across the entire stimulus space.

## 5. Copyright tier handling

Twenty-one of the 36 dataset entries are fully open. Thirteen are restricted by data-use agreement. Two are pointer-required for stimulus distribution. The white paper's pointer-based architecture handles the pointer tier cleanly: AGI hosts unique identifiers, timestamps, and annotations while annotations reference publicly available copies of the stimulus. [`hbn-mri`](../research/collection/data/hbn-mri/card.md) is the canonical pointer-tier dataset because the HBN movies (Despicable Me, The Present, Pixar shorts) are commercial.

The DUA tier is harder. The current white paper has no documented protocol for federating annotations across institutions where the underlying neural data cannot leave the host institution. Datasets like [`courtois-neuromod`](../research/collection/data/courtois-neuromod/card.md) (six subjects, hundreds of hours, custom DUA), [`bang-multimodal`](../research/collection/data/bang-multimodal/card.md) (Cedars-Sinai or Caltech IRB, plus CC0 metadata), and [`sherlock-fmri`](../research/collection/data/sherlock-fmri/card.md) (Princeton DUA) have rich annotation potential and restricted distribution constraints simultaneously. The solution is a federation protocol with three explicit tiers: open (annotations and stimulus redistributable), pointer-only (annotations open, stimulus pointed at), and federated (annotations open, neural data stays at host institution, computational pipelines run there). The protocol design itself is a Phase 4 governance deliverable; the data-direction commitment is to name the datasets that need it.

## 6. The rollout map

Pulling directly from the [`dataset-hierarchy`](../research/synthesis/dataset-hierarchy.md) flagship-status column:

**Phase 1, current white-paper flagships (3 stimulus repositories collapsing 7 dataset entries)**:
- NSD images repository, hosting [`nsd-fmri`](../research/collection/data/nsd-fmri/card.md), [`nsd-ieeg`](../research/collection/data/nsd-ieeg/card.md), [`nsd-eeg-alljoined`](../research/collection/data/nsd-eeg-alljoined/card.md), with [`coco`](../research/collection/data/coco/card.md) as the upstream stimulus source.
- StudyForrest repository, hosting [`studyforrest`](../research/collection/data/studyforrest/card.md) and [`studyforrest-eyegaze`](../research/collection/data/studyforrest-eyegaze/card.md).
- HBN movies repository, hosting annotations referenced by both [`hbn-eeg`](../research/collection/data/hbn-eeg/card.md) and [`hbn-mri`](../research/collection/data/hbn-mri/card.md).

**Phase 2 candidates, extensible from current flagships**:
- [`narratives-pieman`](../research/collection/data/narratives-pieman/card.md) extends the audio-narrative side with the largest open spoken-narrative corpus (345 subjects, 27 stories) and an existing HED-LANG sidecar template that AGI can adopt with minimal modification.
- [`naturalistic-neuroimaging-db`](../research/collection/data/naturalistic-neuroimaging-db/card.md) extends the video-film side with 86 subjects across 10 feature films, demonstrating the pointer-architecture protocol on commercial titles other than HBN movies.
- [`courtois-neuromod`](../research/collection/data/courtois-neuromod/card.md) extends the deep-sampling pattern of NSD into the video domain, with hundreds of hours per subject.

**Second-wave repositories**:
- Static-image strand: [`things-initiative`](../research/collection/data/things-initiative/card.md), [`nod-eeg`](../research/collection/data/nod-eeg/card.md), [`things-eeg2`](../research/collection/data/things-eeg2/card.md), [`bold5000`](../research/collection/data/bold5000/card.md). The THINGS family is the cross-modal sibling to NSD with the largest concept set in cognitive neuroscience.
- Video strand: [`bang-ieeg-fmri`](../research/collection/data/bang-ieeg-fmri/card.md), [`bang-multimodal`](../research/collection/data/bang-multimodal/card.md), [`sherlock-fmri`](../research/collection/data/sherlock-fmri/card.md). The Bang family is the gold standard for short-clip multimodal recordings; Sherlock is the canonical event-segmentation benchmark.
- Audio strand: [`moth-radio-hour`](../research/collection/data/moth-radio-hour/card.md), [`little-prince-fmri`](../research/collection/data/little-prince-fmri/card.md). Moth-Radio-Hour is the canonical reference for continuous-language encoding; Little Prince provides cross-lingual replication.
- Cognitive-task wedge: [`hcp-task`](../research/collection/data/hcp-task/card.md), [`hcp-d-development`](../research/collection/data/hcp-d-development/card.md), [`abcd-task`](../research/collection/data/abcd-task/card.md), [`cam-can`](../research/collection/data/cam-can/card.md), [`aomic`](../research/collection/data/aomic/card.md). AOMIC first because of license openness; ABCD-task next because of cohort scale.
- Localizers: [`fedorenko-language-localizer`](../research/collection/data/fedorenko-language-localizer/card.md), [`pinel-localizer`](../research/collection/data/pinel-localizer/card.md), [`localizer-ds000114`](../research/collection/data/localizer-ds000114/card.md). One PR per localizer; HED sidecar plus stimulus-pointer.
- Hybrid: [`lemon-mpi`](../research/collection/data/lemon-mpi/card.md). The cleanest open hybrid dataset for demonstrating multi-paradigm-per-repository.

**Reference-only**:
- [`coco`](../research/collection/data/coco/card.md) (stimulus source for NSD and BOLD5000 already covered by upstream repositories), [`glmsingle-paper`](../research/collection/data/glmsingle-paper/card.md) (methods reference), [`inscapes`](../research/collection/data/inscapes/card.md) (paradigmatic exemplar but minimal annotation), [`myconnectome`](../research/collection/data/myconnectome/card.md) (single-subject), [`natural-sounds-fmri`](../research/collection/data/natural-sounds-fmri/card.md), [`dhcp`](../research/collection/data/dhcp/card.md) (neonatal, mostly resting state), [`deap`](../research/collection/data/deap/card.md), [`seed`](../research/collection/data/seed/card.md).

## 7. Coordination with the science direction

The science strand argues that five of the seven Strand C themes are gated by annotation supply. The dataset-rollout sequencing above is the operational complement: each science-thesis claim becomes testable when the corresponding dataset gets a HED-tagged annotation layer.

- Encoding-model libraries on canonical stimuli mature once NSD and Forrest Gump and Moth-Radio-Hour carry community-versioned annotation layers.
- Annotation-supervised foundation-model pretraining matures once HBN-EEG plus NSD-EEG-alljoined plus NOD-EEG plus THINGS-EEG2 are aggregated with shared HED tags.
- Annotation-response curves at scale mature once the ANNOTATE R01 produces the curves on NSD and AGI replicates the experiment on second-wave datasets.
- Cross-modal alignment papers mature once the NSD triangle generalizes to the Forrest Gump quartet (7T fMRI plus 3T fMRI plus MEG plus eye-gaze) and the THINGS triangle (fMRI plus MEG plus EEG).
- Annotation-decomposed ISC and event-segmentation papers mature once Sherlock and Bang carry HED-tagged scene-boundary and character-emotion annotation layers.

The dataset-side investment unlocks the science-side claims. The reverse is also true: each scientific success on a particular dataset attracts contribution and use of the corresponding AGI repository, which in turn feeds the next round of annotation richness. The Wikipedia analogy from [`VISION.md`](../VISION.md) captures the dynamic.

## 8. What this paper is not

It is not a dataset-curation manual; the per-dataset import scripts and HED-tag mapping tables belong in the AGI image-annotation tool repository, not here. It is also not a complete coverage survey; entries the corpus did not include (Algonauts, ECoG-libet, the various OpenNeuro single-task collections beyond ds000114) will land in repositories on their own merits. The contribution of this direction paper is the explicit tier policy and the cognitive-task wedge thesis.

## References

Citations resolve to BibTeX keys in [`../research/collection/data/data.bib`](../research/collection/data/data.bib). Direct paper-card links are in the prose above; the keys here are for downstream manuscript export.

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
