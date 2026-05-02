# Scope Diagram, AGI and ANNOTATE

A side-by-side framing piece. Reads first in the [Phase 3 reading order](./README.md), because every downstream Phase 3 deliverable depends on the reader knowing that the Annotation Garden Initiative (AGI) and the ANNOTATE R01 are complementary, not competing.

Abbreviations: National Library of Medicine (NLM), Hierarchical Event Descriptors (HED), Brain Imaging Data Structure (BIDS), Natural Scenes Dataset (NSD), Healthy Brain Network (HBN), magnetoencephalography (MEG), electroencephalography (EEG), intracranial EEG (iEEG), functional magnetic resonance imaging (fMRI), data-use agreement (DUA), foundation model (FM).

## Side-by-side dimensions

| Dimension | ANNOTATE R01 | AGI |
|---|---|---|
| Type | Funded research project, principal-investigator-led | Open infrastructure, community-governed |
| Funding model | Five-year NLM grant | Mixed: project staffing during overlap with ANNOTATE; community contribution thereafter |
| Scope of authorship | Defined investigator team | Anyone with a pull request |
| Datasets in scope | NSD ([`nsd-fmri`](../collection/data/nsd-fmri/card.md), [`nsd-ieeg`](../collection/data/nsd-ieeg/card.md), [`nsd-eeg-alljoined`](../collection/data/nsd-eeg-alljoined/card.md)), HBN ([`hbn-eeg`](../collection/data/hbn-eeg/card.md), [`hbn-mri`](../collection/data/hbn-mri/card.md)), StudyForrest ([`studyforrest`](../collection/data/studyforrest/card.md)) | All naturalistic and cognitive-task datasets reachable via Stim-BIDS, see [`dataset-hierarchy`](./dataset-hierarchy.md) |
| Modalities in scope | EEG, iEEG, fMRI | Plus MEG, eye-tracking, peripheral physiology, behavior, multi-omics |
| Annotation production | Empirical curves at five richness levels on NSD; HEDit-driven multi-agent generation; video extension of HEDit | Community accumulation via pull requests; multi-source orchestration via [`crowdagent`](../collection/tools/crowdagent/card.md)-pattern adapters |
| Tools relied on | HEDit, [`eeglab`](../collection/tools/eeglab/card.md), [`neuroscout`](../collection/tools/neuroscout/card.md) pipelines | HEDit plus [`elan`](../collection/tools/elan/card.md) plus [`praat`](../collection/tools/praat/card.md) plus [`boris`](../collection/tools/boris/card.md) plus [`datavyu`](../collection/tools/datavyu/card.md) plus [`label-studio`](../collection/tools/label-studio/card.md) plus Layer-2 AI annotators (see [`tool-ontology`](./tool-ontology.md)) |
| Output artifacts | Annotation-response curves; HED-Generation-3 sidecars at five levels; foundation-model demonstrations; analysis pipelines integrated with EEGLAB and NeuroScout | Stimulus repositories; FAIR commons governance; federation protocols; bidirectional adapters; visualization at annotation.garden |
| Time horizon | Five-year project | Indefinite, evolving |
| Failure mode | Aim does not generalize, scientific finding is null | A repository becomes unmaintained, the federation fails, governance fragments |
| Deprecation policy | Project ends, deliverables persist via NIH data sharing | Versioning, sunset rules, fork etiquette (Phase 3 deliverable, see [`gap-analysis`](./gap-analysis.md) gap 8) |

## Overlap diagram

```
                             ┌──────────────────────────┐
                             │      ANNOTATE R01        │
                             │   (research project)     │
                             │                          │
                             │  Aim 1: NSD encoding     │
                             │  Aim 2: response curves  │
                             │  Aim 3: HBN +            │
                             │         StudyForrest     │
                             │         generalization   │
                             │                          │
       ┌─────────────────────┤  HEDit annotation client │
       │                     │                          │
       │                     └────────────┬─────────────┘
       │                                  │
       │                                  │  shared substrate
       │                                  │  (NSD, HBN, StudyForrest;
       │                                  │   HED Generation 3; BIDS;
       │                                  │   EEGLAB; NeuroScout)
       │                                  │
       │                     ┌────────────┴─────────────┐
       │                     │                          │
       │                     │    ANNOTATION GARDEN     │
       │                     │      INITIATIVE          │
       │                     │   (open infrastructure)  │
       │                     │                          │
       │                     │  Stimulus repositories   │
       │                     │  Branches as layers      │
       │                     │  FAIR commons governance │
       │                     │  Federation protocols    │
       │                     │  Cognitive-task wedge    │
       │                     │  Layer-1 adapter contract│
       │                     │                          │
       └─────────────────────┤  Visualization at        │
                             │  annotation.garden       │
                             │                          │
                             └──────────────────────────┘
```

The shared substrate (center) is what allows ANNOTATE deliverables to land in AGI repositories without re-annotation.

## Complementarity statement

ANNOTATE is a research project; AGI is open infrastructure. The two relate as follows:

1. **ANNOTATE produces empirical findings; AGI translates them into community guidelines.** The annotation-response curves of Aim 2 will state, for the first time, how much annotation is enough on NSD across EEG, iEEG, and fMRI. That finding, by itself, is not a community guideline. AGI translates it into curation defaults: the recommended HED-tag depth for the NSD stimulus repository, the recommended annotation density tier for new repositories, and the canonical evaluation harness (a Stim-BIDS-conformant test set) that future contributors run their annotations through.

2. **HEDit is the canonical AGI annotation client; AGI does not duplicate HEDit.** ANNOTATE develops HEDit as a multi-agent annotation platform (Aim 2 Goal 2C extends it to video). AGI does not build a competing client. Instead, AGI commits to ingesting HEDit output as a first-class input format and to publishing the per-stimulus annotations HEDit generates as branches in the relevant AGI repositories.

3. **AGI's stimulus repositories are ANNOTATE's distribution layer.** When ANNOTATE Aim 1 releases NSD HED-Generation-3 sidecars at Level 5, they land in `Annotation-Garden/nsd-stimuli` as a versioned annotation branch. When Aim 2 releases the five richness levels, they land as five branches. When Aim 3 generalizes to HBN and StudyForrest, the same pattern applies. ANNOTATE does not need to maintain its own distribution infrastructure; AGI does that.

4. **AGI broadens beyond what ANNOTATE can reach.** AGI's distinctive scope (per [`gap-analysis`](./gap-analysis.md)) is precisely the territory ANNOTATE cannot cover within a five-year, three-modality, three-dataset grant: the cognitive-task wedge (gap 1), the broader tool ecosystem (gap 2), provenance and credit (gap 3), federation (gap 4), the second-wave datasets (gap 5), AI-annotator adapters (gap 6), hybrid paradigms (gap 7), and FAIR commons governance (gap 8).

5. **AGI is the durable artifact; ANNOTATE is the catalyzing event.** When ANNOTATE concludes, its findings persist in AGI repositories as versioned annotations and in AGI documentation as guidelines. The infrastructure that makes those findings durable was built in parallel with the science; that parallel construction is the single most important strategic argument for AGI's existence.

## What AGI must explicitly **not** do

To keep the complementarity clean, AGI should commit to **not** doing the following:

- **Compete with HEDit on annotation production.** AGI consumes; HEDit produces.
- **Run encoding-model competitions or sufficiency studies.** That is ANNOTATE territory; AGI hosts the resulting annotations and the canonical test sets, but does not replicate the empirical work.
- **Choose between annotation perspectives.** When two contributor branches disagree, AGI hosts both as distinct branches and lets the community evaluate. This is the Wikipedia-style commitment in [`VISION.md`](../../VISION.md).
- **Restrict modality coverage.** AGI is modality-general. ANNOTATE narrows for empirical tractability; AGI does not.

These non-commitments are themselves a Phase 3 white-paper deliverable, paired with the affirmative commitments in [`gap-analysis`](./gap-analysis.md).

## Risk and mitigation under the complementarity model

If ANNOTATE is delayed or de-funded, AGI persists; the cost is that AGI's annotation production rate drops because HEDit improvements stall. If AGI fails to launch its governance and federation deliverables, ANNOTATE still produces its science, but the resulting sidecars and curves get distributed by ad-hoc OSF or supplementary-materials channels rather than landing in versioned repositories. Each project mitigates the other's worst-case failure mode.

## Phase 3 framing recommendation

Open the updated white paper with this complementarity. The current white paper does not mention ANNOTATE; that is appropriate for the public-facing initial document, but a research-foundation update should make the relationship explicit so that grant reviewers, potential contributors, and partner labs can locate the boundary between project and infrastructure on first read.
