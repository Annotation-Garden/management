# Annotation Garden Archive — Product Requirements Document

**Status:** v1.2 draft, dated 2026-05-03. Builds on v1.1 by integrating the full RFA-MH-25-110 mechanism specifics into Sections 11.2 and 11.3, naming Amit Majumdar (SDSC) as the compute-side MPI on the R24 application, recording the UCSD philosophy ethics-adviser role, and tightening the framing of Section 12 to satisfy the NOFO's responsiveness discipline (data archive first; analyses integrated per permitted scope). The change log lives in Section 16.

**Companion documents:** [`agi-white-paper.md`](agi-white-paper.md) for the scientific position, [`direction-papers/science-direction.md`](direction-papers/science-direction.md), [`direction-papers/tools-direction.md`](direction-papers/tools-direction.md), [`direction-papers/data-direction.md`](direction-papers/data-direction.md) for the strand-specific elaborations.

---

## 0. How to read this document

This is a Product Requirements Document for the Annotation Garden Archive — the FAIR commons of stimuli, annotations, and dataset back-pointers that AGI is being built to host. It captures mission, vision, three operational commitments, stakeholder requirements, an identifier and data model, the categorization spine, representation patterns, FAIR commitments, governance, operational policy (federation, sustainability, data-sharing-plan readiness, licensing), Phase 1 scope, and open questions. It is deliberately not an implementation plan; that comes after this PRD is approved.

The novel commitment of AGI is that stimulus annotations are first-class scientific objects — independently identified, community-versioned, semantically tagged with the Hierarchical Event Descriptors (HED) framework, and joinable to every brain dataset that used the stimulus. Getting the data model and governance right matters because no prior project has treated annotations this way; mistakes here propagate into every downstream pipeline.

Reading order for reviewers: Sections 1–3 for the thesis, Section 5 for who AGI is for, Section 6 for the data model, Sections 10–11 for the governance and operational policy that will be load-bearing in any funder review, Section 12 for the annotation-driven analyses capability that distinguishes the archive from a static FAIR commons, Section 13 for what ships in Phase 1, Section 14 for what is still open.

---

## 1. Mission

> The Annotation Garden Archive is the FAIR commons that promotes stimulus annotations to first-class scientific objects — independently identified, community-versioned, HED-tagged, and joinable to every brain dataset that used the stimulus — so that brain-behavior research accumulates against a shared annotation substrate rather than re-annotating per paper.

## 2. Vision

Today, neuroscience datasets are catalogued; their stimuli are not. AGI inverts that posture. The stimulus and its annotations become persistent indexed entities, and brain datasets are *consumers* that join them by stable identifier. A researcher browsing the studyforrest shot-boundary annotation should see, in one view, every functional Magnetic Resonance Imaging (fMRI), Electroencephalography (EEG), and intracranial Electroencephalography (iEEG) dataset that used that movie, every alternative annotation perspective on the same shots, every published analysis that consumed those annotations, and a citation surface that credits each annotator. The archive is the connective tissue that makes that view possible.

The conservative reading of the AGI thesis is that annotation duplication is an operational tax on naturalistic-stimulus research, and a community-versioned annotation commons amortizes that tax so the value compounds. This reading is sufficient to motivate the archive on its own. A stronger reading — that annotation poverty is itself the gating variable for the next paradigm shift in mainstream cognitive-neuroscience analytics — is plausible but unproven; it is held as a hypothesis to be tested empirically, not as a load-bearing claim of this document. The white paper [`agi-white-paper.md`](agi-white-paper.md) Section 8.1 should be read with the same calibration.

A garden requires cultivation. The archive's value compounds with each annotation perspective contributed, each dataset that reuses an existing annotation rather than re-annotating, and each cross-modal alignment paper made tractable because the annotation layer was already sitting on a shelf.

AGI is positioned to do this credibly because the infrastructure layer is already in place at the host institution. The Swartz Center for Computational Neuroscience (SCCN) at UCSD operates NEMAR as an Amazon Web Services Open Data Sponsorship resource with a per-dataset GitHub-repository pattern, `nemar-cli` (the user-facing command-line tool), `nemar-tools` (the publication pipeline that mints Zenodo Digital Object Identifiers and generates metadata), `neuroschema` (an extensible JavaScript Object Notation (JSON) Schema for neuroimaging metadata), and the SCCN-maintained `NEMAR-pipeline` for processing. AGI inherits this stack: dataset-per-repo, Zenodo-via-nemar-tools, AWS Open Data hosting, neuroschema as the metadata substrate, and the Neuroscience Gateway plus San Diego Supercomputer Center (SDSC) for compute. The archive layers an annotation commons on top of these services rather than rebuilding them.

## 3. The three operational commitments

Three claims define what makes AGI distinct. Each is a testable architectural commitment, not a slogan; if any fails to hold operationally, AGI has not delivered its distinguishing value.

1. **Annotations are independently identified.** Every annotation perspective on every stimulus has a stable identifier, a version history, a license, a contributor record, and a citation surface (Digital Object Identifier (DOI) at release). Annotations are findable, citable, and forkable on their own terms — not as inert columns in someone else's events table. The empirical precedent is Common Objects in Context (COCO), where annotations carry their own first-class IDs and many perspectives co-exist on a single image; AGI generalizes the pattern across stimulus types and modalities.
2. **Stimulus is a first-class join key between annotations and datasets.** The archive maintains a registry-level inverted index that, given a stimulus identifier, returns every brain dataset that used it (with stable accession identifiers from OpenNeuro, the Neuroelectromagnetic Data Archive and Tools Resource (NEMAR), DANDI, and others). Discovery is bidirectional: the archive is queried stimulus-first; peer archives query the archive dataset-first via its public application programming interfaces. AGI does not replace dataset-first discovery in OpenNeuro or DANDI; it adds the inverse axis that none of them currently surface.
3. **Multiple annotation perspectives on the same stimulus are normal.** Branches in the underlying Git substrate hold parallel annotation efforts. A movie may carry shot-boundary, speech, music, emotion, eye-gaze, and several more tiers; users mount the union or the intersection as their analysis requires. Each perspective is independently versioned and citable.

## 4. Position relative to existing work

AGI is built in concert with several maturing efforts and inherits as much as possible from them. The relationship language matters: AGI is a partner, not a replacement, and not a competitor.

- **Brain Imaging Data Structure (BIDS) and the Stim-BIDS extension proposal (BEP044, https://bids.neuroimaging.io/extensions/process.html).** AGI repositories conform to the BIDS stimulus specification: `stim-<label>` entity for stimuli, `annot-<label>` entity for annotation perspectives, `stimuli.tsv` and `annotations.tsv` index files, `stim-<label>_annot-<label>_events.tsv` for time-varying annotations. The `annot-<label>` entity is part of BEP044 and remains provisional pending merge into the canonical BIDS specification; AGI tracks the BEP and updates accordingly. AGI does not invent a parallel format; it adopts BIDS verbatim and surfaces gaps to the BIDS Maintainers Group as proposed amendments. The dataset back-pointer field in Section 6 is the most concrete gap AGI proposes upstream. If the upstream proposal is declined, AGI maintains the back-pointer at the registry level via per-repository `usedby.tsv` files, and the BIDS validator does not need to know about it.
- **HED working group, including the `hed-task` catalog (https://github.com/hed-standard/hed-task), HEDit annotation client, and HED Generation 3 schema (https://www.hedtags.org/).** AGI and the HED working group co-construct the cognitive-task and event-vocabulary substrate. AGI consumes `hed-task` taxonomy verbatim, contributes back gap reports and tag proposals, and relies on HEDit as the canonical annotation interface for multi-agent annotation flows. The `hedtsk_*` task catalog and `hed_*` process catalog are version-stamped per AGI repository so dependency drift is visible.
- **The ANNOTATE R01.** AGI hosts ANNOTATE-produced annotation layers as versioned branches. ANNOTATE delivers empirical annotation-response curves on Natural Scenes Dataset (NSD) and validates on Healthy Brain Network EEG (HBN-EEG) and studyforrest; AGI extends the resulting layers to additional datasets and modalities and provides their distribution surface.
- **OpenNeuro (https://openneuro.org), NEMAR (https://nemar.org), DANDI (https://dandiarchive.org).** Peer archives that hold the brain datasets. AGI references their accessions; they reference AGI stimulus identifiers. No data duplication; cross-pointers in both directions. NEMAR is operated by SCCN at UCSD and is an inherited infrastructure resource for AGI: `nemar-cli` access, NEMAR-side DOI minting, AWS Open Data Sponsorship hosting, and SDSC disk and compute. AGI extends NEMAR resources where needed rather than duplicating them.
- **Neuroscience Gateway (NSG, https://www.nsgportal.org/) and San Diego Supercomputer Center (SDSC, https://www.sdsc.edu/).** Compute partners. NSG provides the REST API surface for AGI's annotation-driven on-the-fly analyses (Section 12); SDSC provides backing compute and disk. Both are co-located at UCSD, which simplifies the institutional relationship to the host. AGI does not host its own compute; the compute partner relationship is a project commitment, not an implementation artifact.
- **NeuroScout (https://neuroscout.org).** Closest existing analysis-side precedent. AGI annotations become NeuroScout predictors via a bridge; NeuroScout's fMRI-only and Pliers-only scope generalizes to EEG, Magnetoencephalography (MEG), and iEEG, and to non-Pliers annotators, once AGI ships the relevant layers. AGI does not assume NeuroScout will extend; AGI must build the per-annotation-perspective citation surface itself.
- **Cognitive Atlas (https://cognitiveatlas.org), Research Domain Criteria (RDoC) matrix (https://www.nimh.nih.gov/research/research-funded-by-nimh/rdoc), BrainMap (https://brainmap.org), Cognitive Paradigm Ontology (http://www.cogpo.org/).** Active and legacy cognitive-task taxonomies that AGI links to via adapter mappings. AGI does not fork them; it cites them.
- **DataLad (https://datalad.org).** Provenance and versioning substrate; AGI stimulus repositories are valid DataLad datasets. The DataLad maintainer (Halchenko) is a project collaborator and the canonical reference for DataLad-side design decisions in the archive.
- **Hugging Face Datasets (https://huggingface.co/docs/hub/datasets-cards) and Zenodo Communities (https://about.zenodo.org/communities/).** AGI adopts the Hugging Face dataset-card pattern (YAML front-matter plus Markdown body) for per-annotation-perspective documentation, and Zenodo Communities as the default registrar for concept-DOI plus per-version-DOI minting (Section 6).

## 5. Stakeholder requirements

The archive is built simultaneously for several user populations whose requirements partially overlap and partially conflict. Section 5.1–5.6 are user lenses; Section 5.7–5.12 are gatekeeper lenses identified during PRD review. The implementation must satisfy all of them.

### 5.1 Cognitive neuroscientist
- Find every stimulus used in a given paradigm, modality, or population.
- Mount the union or intersection of all annotation branches on a stimulus.
- Confirm that two datasets using "the same" stimulus did, in fact, use the same stimulus version (Section 6 stimulus-equivalence protocol).
- Cite each annotation used in an analysis with a DOI and contributor list.
- Submit a corrected or extended annotation as a pull request and have it reviewed.

### 5.2 Computational and Machine Learning (ML) researcher
- Bulk download with parquet manifests and machine-readable schemas.
- Annotations as predictor matrices joinable to brain data along a common stimulus identifier.
- Train/test split awareness that respects stimulus-level and dataset-level leakage.
- Annotation-supervised pretraining recipes for foundation models on multimodal brain data.
- Hugging Face-style dataset cards including license, citation, intended use, and known limitations.

### 5.3 BIDS / HED standards contributor
- AGI as a co-developed production user of the standards layer; surfaces real-world gaps to the BIDS Maintainers Group and HED working group through the standard proposal process.
- Validators in continuous integration on every pull request: BIDS validator, HED validator, link checker, custom AGI consistency checks. The CI gate is non-negotiable.
- Reference datasets that exercise edge cases of the spec.

### 5.4 Software / FAIR steward
- Per-stimulus repositories with a known shape, generated and validated by tooling.
- DataLad provenance from the first commit forward.
- Automated continuous-integration on every contribution.
- Per-stimulus and per-annotation licensing distinct from repository-level license, with Software Package Data Exchange (SPDX) identifiers and REUSE Software compliance.
- Restricted-stimulus federation tier with a documented hash-equivalence protocol (Section 11).

### 5.5 Contributor and educator
- Low-friction path from a researcher's existing annotation file (Eudico Linguistic Annotator (ELAN) `.eaf`, Praat TextGrid, BORIS, Datavyu, Label Studio JSON) to a valid AGI submission.
- Per-contributor credit on every pull request, surfaced on the archive site, with Open Researcher and Contributor Identifier (ORCID) attribution and Contributor Roles Taxonomy (CRediT) roles.
- Annotation literacy curriculum that uses AGI as the reference resource.
- Onboarding documentation that brings a new lab to a first contribution within one working session.

### 5.6 Copyright and restricted-stimulus steward
- Pointer-only architecture for restricted stimuli (HBN movies, International Affective Picture System (IAPS), copyrighted music, clinical recordings).
- Hash-equivalence verification: users supply their own copy of the stimulus; the archive verifies it matches what the annotations were created against per Section 11.
- Federation tier policy distinguishing freely shareable annotations from restricted stimulus content.
- Audit logging and access control where required.

### 5.7 Institutional Review Boards and Human Research Protections Programs
- A clear statement of which stimulus categories (clinical, paediatric, identifiable subject content) trigger institutional review and what AGI's role is in that review.
- A subject-reidentification risk analysis for any annotation tier whose contents could indirectly identify subjects through rare-stimulus + small-cohort matching.
- Takedown procedure with a Service Level Agreement and a named institutional contact.

### 5.8 Journal editors, peer reviewers, and data-availability statement reviewers
- Annotations citable in a way that journal editorial systems (Nature, eLife, Journal of Neuroscience, NeuroImage, Cerebral Cortex) accept: CrossRef-registered DOI, ORCID-attributed authors, persistent landing page, machine-readable citation metadata.
- A paste-able data-availability-statement template grantees and authors can include in their manuscripts.
- Citation rendering demonstrated in at least three target-journal styles before launch.

### 5.9 Dataset originators with retained rights
- Named consultation and notification protocol when AGI hosts annotations of a stimulus the originator released. Phase 1 originators (Hanke for studyforrest; Kay and Naselaris for NSD; Milham and Child Mind Institute for HBN movies) are first-class collaborators, not passive third parties.
- Consent or non-objection in writing before launch of an originator's stimulus repository.
- A transparent process for originator-raised objections to third-party annotation perspectives.

### 5.10 Clinical and developmental researchers
- Age-appropriateness flags on stimuli; cohort-aware annotation perspectives where stimulus interpretation varies by age.
- Compliance with paediatric-data IRB norms when annotations interact with subject-level data (e.g., HBN, ABCD, Cam-CAN).
- Cohort-distribution views on stimuli (Section 8).

### 5.11 Computational psychiatry and dimensional-phenotype researchers
- Adapter mappings to RDoC matrix cells, Hierarchical Taxonomy of Psychopathology (HiTOP) dimensions, and other phenotypic schemes beyond the cognitive-task spine.
- Population-overlay representation patterns (Section 8).

### 5.12 Funders, data-coordinating centers, and patient advocates
- Alignment with the National Institutes of Health (NIH) 2023 Data Management and Sharing Policy and analogous policies of the National Science Foundation, Wellcome, European Research Council, and Bundesministerium für Bildung und Forschung. AGI is funder-agnostic.
- Named relationship to the NIH-supported domain repositories and the Generalist Repository Ecosystem Initiative, expressed in Section 11.3.
- Subject-and-advocate-aware stewardship for any annotations of clinically-derived stimuli.

## 6. Identifier system and data model

The archive's value depends on stable, machine-derivable, dereferenceable identifiers and on a precise specification of what equivalence means.

### 6.1 Identifier classes

| Class | Form | Example | Source |
|---|---|---|---|
| Stimulus | `stim-<label>` (Stim-BIDS entity) | `stim-nsd02951`, `stim-forrest`, `stim-thepresent` | BEP044 |
| Annotation perspective | `annot-<label>` scoped to a stimulus | `stim-forrest_annot-shotbounds`, `stim-thepresent_annot-music` | BEP044 |
| Annotation release | Git tag plus per-version DOI plus concept DOI | `v1.0.0` tagged in `Annotation-Garden/forrest-stimuli`, archived to Zenodo Community | Zenodo, DataCite |
| Dataset back-pointer | Triple `(stimulus_hash, presentation_record, dataset_accession)` | `(sha256:abc..., presentation:nsd-fmri-7T-3s-isi, openneuro:ds002791)` | AGI registry |
| Cognitive-task category | `hedtsk_<slug>` and `hed_<slug>` from `hed-task` | `hedtsk_eriksen_flanker`, `hed_response_inhibition` | HED working group |
| Annotation-tier type | `tier:<slug>` from the proposed HED library schema | `tier:shot-segmentation`, `tier:speech-transcript` | HED library schema candidate (Section 7.3) |
| Contributor | ORCID iD | `0000-0002-1825-0097` | ORCID |

### 6.2 Stimulus equivalence

Two datasets that claim to use "the same" stimulus may not, in fact, use the same stimulus. AGI specifies equivalence at three levels:

1. **Byte-identity.** The Secure Hash Algorithm 256-bit (SHA-256) of the canonical stimulus file matches. This is the strict equivalence used for static images, audio assets that are not re-encoded, and any stimulus where byte-identity is achievable. AGI publishes the SHA-256 of every canonical stimulus.
2. **Codec-tolerant fingerprint.** For audiovisual stimuli that are routinely re-encoded (HBN movies; studyforrest movie), AGI publishes a codec-tolerant perceptual fingerprint (frame-rate-independent visual hash plus audio fingerprint over fixed time windows) plus the canonical metadata triple `(release_version, frame_rate, duration_ms)`. A user-supplied copy is a match if the perceptual fingerprint clears a documented threshold and the metadata triple matches.
3. **Manual attestation.** When neither (1) nor (2) is achievable, the originator or a designated curator attests that the user-supplied copy is equivalent. The attestation is recorded and attributed.

The equivalence level used for a given stimulus is recorded in `stimuli.json`. Annotations always join on the equivalence level of the stimulus they target.

### 6.3 Dataset back-pointer

The back-pointer is a triple, not a pair, because the same byte-identical stimulus may be presented under different parameters in different datasets, and a back-pointer that flattens presentation context is ambiguous. The triple is `(stimulus_hash, presentation_record, dataset_accession)`. Each tuple is recorded in the per-repository `usedby.tsv` and mirrored in the archive-level inverted index; the index supports both stimulus-first lookup ("which datasets used this stimulus?") and dataset-first lookup ("which stimuli does this dataset reference?").

The presentation record is a small structured object naming the experimental task or paradigm (with `hedtsk_*` reference where applicable), the presentation timing, and the modality. For cognitive-task stimuli the presentation record is dominated by the `hedtsk_*` reference; for naturalistic stimuli it is dominated by timing and viewing-geometry parameters.

The back-pointer index is updated by three mechanisms in parallel: (a) contributor-submitted records on the pull request that adds a stimulus or dataset, (b) periodic crawl of OpenNeuro, NEMAR, and DANDI metadata for accessions that reference AGI stimuli, (c) optional webhook integration with peer archives where they support it. The canonical mechanism is (a); (b) backfills; (c) is opportunistic.

### 6.4 Annotation versioning

Each annotation perspective release receives a Git tag, a Zenodo per-version DOI, and a Zenodo concept DOI. The concept DOI cites "the annotation perspective as a navigable object across versions"; the per-version DOI cites a specific snapshot. Citation defaults to the concept DOI when "the latest stable" is meant and to a specific per-version DOI when a paper analyzed a specific snapshot.

Each release also carries an explicit change-type tag drawn from a controlled vocabulary, because Semantic Versioning's patch/minor/major scheme does not match how annotations evolve. The tag is one of:

- `additive` — new rows or stimuli added; existing rows unchanged.
- `corrected` — existing rows fixed for data-entry, alignment, or transcription errors.
- `re-rated` — existing rows replaced with values from a different rater or a re-rating procedure; schema unchanged.
- `consolidated` — multiple rater outputs merged into a consensus; disagreement columns may be added.
- `schema-bumped` — column schema or HED-tag set updated, typically to track an upstream HED Generation bump; semantic content of judgments unchanged.
- `restructured` — column schema deliberately restructured; semantic content of judgments may also change.

Releases use monotonic-integer versioning (`r1`, `r2`, `r3`) with the change-type tag. Calendar versioning is also acceptable for repositories whose cadence is human-scale; the archive registry treats both schemes as first-class. Old releases remain dereferenceable indefinitely; their DOIs are never withdrawn (DataCite forbids withdrawal). Removal under legal compulsion is handled by tombstoning per Section 10.

### 6.5 Per-row provenance

Every annotation row carries provenance columns as standard fields in the `events.tsv` sidecar specification: `annotator` (an ORCID iD or a controlled-vocabulary tool identifier), `tool` and `tool_version` (when machine-generated), `model_checkpoint` (a content hash of the model weights when applicable), and `timestamp` (when the annotation was produced). These fields are mandatory for new annotation files; legacy annotation files without them are accepted with a CI warning and a documented deprecation horizon.

### 6.6 Citation export and authorship

Every annotation release exposes BibTeX, Citation Style Language (CSL) JSON, and a plain-text citation block. Authorship is captured in a per-release `CITATION.cff` file with CRediT roles per contributor; ORCID iD is required for substantive contributors; the file is a release blocker if contributors have not agreed on author order. Authorship by commit count is explicitly rejected as a default; AGI follows the BIDS, DataLad, and Open Source Initiative practice of curated author lists with declared roles.

Citation rendering is verified in three target-journal styles (Nature, eLife, NeuroImage) before launch; the verification is part of the v1 launch checklist.

## 7. The categorization spine

Two orthogonal axes carry the categorization, plus a third axis that is a current gap and that AGI proposes to seed in collaboration with the HED working group.

### 7.1 Naturalistic axis — stimulus modality and content

Drawn from the Stim-BIDS suffix set (`image`, `audio`, `video`, `audiovideo`) and a community-curated set of content-family tags (narrative film, animation, music with vocals, ambient soundscape, social-interaction clip, abstract visual, photographic scene, illustrated scene, and others to be added). This axis is loose; tags accumulate, and there is no enforced single-parent hierarchy. WordNet-anchored synset URIs from ImageNet are preserved when stimulus content is already labelled under that scheme (notably NSD via COCO).

### 7.2 Cognitive-task axis — co-developed with `hed-task`

AGI co-develops with the `hed-task` catalog (Robbins and collaborators; https://github.com/hed-standard/hed-task) as its cognitive-paradigm spine. The catalog provides 19 process categories, approximately 100 tasks with `hedtsk_*` identifiers, approximately 170 processes with `hed_*` identifiers, inclusion-test triples (procedure, manipulation, measurement), variation criteria with explicit DROP categories, and a stable cross-reference structure.

The relationship is collaborative: AGI consumes the catalog, version-stamps the dependency in each repository, and contributes back gap reports and proposed entries through the catalog's standard process when archived stimuli expose paradigms or processes not yet in it. AGI does not fork the taxonomy. The dependency on `hed-task` is recorded in each repository's `dataset_description.json`.

Adapter mappings to legacy task ontologies (Cognitive Atlas concept Uniform Resource Identifiers (URIs), RDoC constructs, BrainMap behavioral-domain codes, Cognitive Paradigm Ontology classes) are maintained as a separate registry so external systems labelled under any of those schemes can find their AGI counterparts.

For any stimulus used in a paradigm with an existing `hedtsk_*` entry, the `hedtsk_*` reference is required metadata in `stimuli.json` (Section 14 resolves prior open question 4). Stimuli used in paradigms without an existing entry carry a sentinel value and are flagged for upstream contribution.

### 7.3 Annotation-tier axis — proposed as a HED library schema

Real-world stimuli carry many parallel annotation tiers. The studyforrest corpus, developed under Hanke and collaborators across more than a decade of annotation papers, carries shot boundaries, character speech with phoneme timing, music type, location changes, character body contact, character emotion (valence/arousal continuous), eye-gaze patterns, semantic conflict, lies, and additional layers — a heterogeneous tier inventory that has accumulated through a sustained release cadence. The Healthy Brain Network movie collection (including The Present) carries shot boundaries plus a documented set of higher-level tiers including action, story, audio, video, content, existence, and music. The two corpora overlap on common tiers (shot boundaries, music) and diverge on stimulus-specific or annotator-specific tiers (forrest's "lies"; HBN's "existence").

There is no community-curated controlled vocabulary for what an annotation tier is. AudioSet covers content within audio tiers; ActivityNet covers content within action tiers; Visual Genome covers structure within scene-graph tiers; MovieNet operationalizes tier conventions on movies but does not publish them as an ontology; ELAN tier conventions are descriptive, not standardized. None covers the union.

AGI proposes the tier-type vocabulary as a HED library schema candidate, populated from the union of MovieNet's tier inventory, AudioSet's audio-event hierarchy, ActivityNet's action ontology, the existing studyforrest tier inventory, and the HBN movie-tier inventory. AGI partners explicitly with the AudioSet and ActivityNet maintainers so the audio and action leaves of the schema reuse their content vocabularies rather than forking them. The schema's stewardship lives with the HED working group, not with AGI alone, consistent with Section 4's relationship language. Each tier-type term has a stable URI; substantial referent change mints a new URI rather than silently redefining the old one (Open Biomedical Ontologies Foundry stability discipline).

The mechanics:
- Each annotation tier on a stimulus is one `annot-<label>` entity.
- The label is short and descriptive (`shotbounds`, `speech`, `music`, `emotion`, `gaze`, `bodycontact`, `semconflict`).
- Each tier carries a `tier-type` field referencing the proposed HED library schema (e.g., `tier:shot-segmentation`, `tier:speech-transcript`, `tier:music-segmentation`, `tier:affective-rating`, `tier:gaze-classification`, `tier:object-bounding-box`, `tier:scene-graph`).
- Stimulus-specific tiers (forrest's "lies" tier) carry a free-form descriptive label without a `tier-type` reference and are flagged for upstream proposal.

## 8. Representation patterns to support

Different stimulus types invite different views of their annotations. The archive's user interface must accommodate at least five patterns.

| Pattern | Stimulus types | Reference precedents |
|---|---|---|
| Multi-track timeline | Movies, audio, music, narratives | studyforrest data portal, ELAN tier view, Audacity, WaveSurfer.js, ActivityNet Captions explorer, Label Studio video timeline |
| Lightbox / grid with overlay layers | Static-image collections (NSD, THINGS, ImageNet) | ImageNet, Common Objects in Context (COCO) explorer, Visual Genome explorer, Open Images |
| Trial schematic | Cognitive tasks, oddball, event-related paradigms | PsychoPy Builder visual flow, Cognitive Atlas task pages, `hed-task` documentation site |
| Graph view | Cross-references between stimuli, annotations, datasets, contributors | Wikidata graph viewer / Reasonator, Open Biomedical Ontologies (OBO) Foundry browsers, NeuroVault link graph |
| Cohort-overlay timeline / grid | Large-N developmental and clinical cohorts (HBN, ABCD, HCP-D, Cam-CAN) overlaid on stimuli | UK Biobank cohort browsers, ABCD Data Exploration and Analysis Portal, HBN biobank viewer |

The pragmatic recommendation is to prototype one example from each pattern (forrest movie for the timeline, an NSD subset for the grid, a flanker paradigm from `hed-task` for the trial schematic, the NSD-deposit-by-stimulus graph for the graph view, an HBN movie with ABCD-cohort overlay for cohort-overlay) before deciding whether the archive ships one unified viewer that switches modes or several view templates.

The annotation-perspective page itself (independent of which view it embeds) follows the Hugging Face dataset-card pattern — YAML front-matter plus Markdown body — and the NeuroScout predictor-page model (per-perspective navigable, citable, with extraction provenance and dataset coverage visible).

## 9. FAIR commitments

Each Findable, Accessible, Interoperable, Reusable sub-principle is mapped to an artifact, a test, a cadence, and a responsible role. The archive publishes an annual FAIR maturity self-assessment using F-UJI or the Research Data Alliance FAIR Data Maturity Model.

| Sub-principle | Artifact | Test | Cadence | Responsible role |
|---|---|---|---|---|
| F1 (globally unique persistent identifier) | `stim-<label>`, `annot-<label>`, Zenodo DOI | Registry probe | Per-PR CI | Software steward |
| F2 (metadata describes the data) | `dataset_description.json`, `stimuli.json`, `annotations.json` | BIDS validator | Per-PR CI | Software steward |
| F3 (metadata includes the data identifier) | DataCite metadata schema 4.5 records | DataCite probe | Per-release | DOI minting service |
| F4 (registered in searchable resource) | AGI registry index | Search probe | Daily | Registry operator |
| A1 (retrievable via standardised protocol) | HTTPS, Git, DataLad | URL/protocol probe | Per-PR CI | Software steward |
| A1.1 (protocol open, free, universally implementable) | HTTP, Git | Static documentation | At launch | Software steward |
| A1.2 (protocol allows authentication where needed) | OAuth via institutional IdP for restricted tier | Manual audit | Annual | Federation steward |
| A2 (metadata persists when data does not) | Tombstone records on legal removal | Manual audit | On request | Governance lead |
| I1 (formal, accessible, broadly applicable language) | TSV + JSON + parquet only | Format probe | Per-PR CI | Software steward |
| I2 (vocabularies follow FAIR principles) | HED Generation 3 + `hed-task` + proposed tier schema | Validator | Per-PR CI | HED collaborator |
| I3 (qualified references to other (meta)data) | Back-pointer triples; ORCID iDs; CRediT roles | Reference probe | Per-PR CI | Software steward |
| R1 (rich metadata) | Per-stimulus and per-annotation cards | Card-completeness check | Per-PR CI | Contributor + reviewer |
| R1.1 (clear data usage license) | SPDX identifiers per file; REUSE compliance | REUSE check in CI | Per-PR CI | Software steward |
| R1.2 (detailed provenance) | DataLad provenance; per-row `annotator`/`tool`/`timestamp` | Provenance probe | Per-PR CI | Software steward |
| R1.3 (community standards) | BIDS, HED, DataCite, ORCID, CRediT | Standards conformance audit | Annual | Standards collaborator |

## 10. Governance and credit

The launch-blocking governance commitments are recorded here. A more detailed governance manifesto elaborates them in a separate document. This section is binding from launch; the manifesto is non-blocking elaboration.

### 10.1 Maintainership and decision-making

- **Co-leads.** Seyed Yahya Shirazi (UCSD/SCCN, GitHub `neuromechanist`, contact lead) and Yaroslav Halchenko (Dartmouth College, GitHub `yarikoptic`, DataLad maintainer).
- **Advisory board.** Kay Robbins (U. Texas San Antonio, HED working group); Arnaud Delorme (UCSD/SCCN, EEGLAB and NEMAR); Scott Makeig (UCSD/SCCN Director, HED, founder of SCCN); Dora Hermes (Mayo Clinic, ECoG and NSD); Monique Denissen (Austrian Neuro Cloud, language annotation). The advisory roster is maintained in [`website/src/components/Team.tsx`](../website/src/components/Team.tsx) as the canonical source.
- **Core archive-maintainers group.** A small named group derived from the co-leads plus 1–2 additional maintainers per major stimulus area (initial members named in the forthcoming governance manifesto), with declared institutional affiliations and conflict-of-interest disclosures. Modeled on the BIDS Maintainers Group structure.
- **Per-stimulus working groups.** Each major stimulus repository has a named working group of 2–5 maintainers with declared institutional affiliations. Maintainers may self-merge non-substantive changes; substantive changes require a second reviewer; cross-cutting changes (changes to the BIDS profile, the HED schema dependency, the back-pointer registry) escalate to the core group.
- **Conflict-of-interest policy.** Reviewers with a direct interest in a contribution (co-authorship on the underlying paper; institutional affiliation with the contributor; financial relationship with a tool referenced in the contribution) recuse from the merge decision; recusal is recorded in the pull request.
- **Contested-annotation escalation ladder.** Disagreements escalate through (a) the relevant working group, (b) the core archive-maintainers group, (c) the advisory board for substantive scientific disputes, (d) external arbitration where (a)–(c) cannot resolve. Most disagreements are resolved by hosting both perspectives as parallel branches; the ladder applies when one perspective seeks to deprecate or block another.
- **Code of Conduct.** AGI adopts a BIDS-style Code of Conduct based on Contributor Covenant 2.1, mirroring the BIDS community's adoption pattern. The role is institutionally located at SCCN; the specific enforcement contact is in flux, with a likely candidate being the project's UCSD philosophy ethics adviser (see ethics line below).
- **Ethical considerations and human-subjects protections.** A UCSD philosophy department contact (specific name pending) advises on ethical considerations for AGI, including clinical and paediatric stimulus annotation, restricted-tier federation, dataset-originator dissent, the machine-versus-human peer status of annotations, and the human-subjects-protections content required in the R24 Research Strategy. The same contact is a candidate for the Code of Conduct enforcement role.
- **Contributor identity.** ORCID iD required for substantive contributors; pseudonymous contribution is permitted via documented procedure for early-career researchers in punitive lab environments or contributors in restrictive jurisdictions (Section 14 question 14).
- **Developer Certificate of Origin.** AGI uses the Developer Certificate of Origin (DCO) pattern (Linux kernel, Kubernetes precedent) rather than a Contributor License Agreement. `Signed-off-by` on every commit is required.

### 10.2 Annotation lifecycle

- **Versioning and citation.** Per Section 6.4 and 6.6.
- **Deprecation.** Annotations are never deleted by AGI; they are deprecated, with a deprecation note in the annotations index pointing users to the recommended successor where one exists.
- **Forks.** Forks of an annotation perspective are first-class. Promotion of a fork to the canonical pointer for a stimulus requires working-group consensus and originator non-objection; refusal to host a fork is reserved for cases where the fork removes attribution, violates the Code of Conduct, or violates a Data Use Agreement.
- **Removal under legal compulsion.** Tombstoning, not deletion. The DOI persists; the content is replaced with a tombstone record explaining the removal and naming the legal basis. A General Data Protection Regulation Article 17 procedure, copyright takedown procedure, and court-ordered-removal procedure are documented in the governance manifesto.
- **Retraction propagation.** When an annotation perspective is retracted because of a fundamental error (mis-aligned timestamps; retracted upstream paper), AGI issues a retraction notice and propagates it through CrossRef Crossmark to citing journals.

### 10.3 Credit

- Per-PR contributor records with ORCID iDs and CRediT roles.
- `CITATION.cff` per release as a release blocker.
- Per-version DOI plus concept DOI per Section 6.4.
- Citation rendering verified in three target-journal styles before v1 launch.
- Alignment with the FORCE11 Joint Declaration of Data Citation Principles.

## 11. Operational policy

Four operational-policy regimes that the v0 review identified as launch-blocking.

### 11.1 Federation and restricted-tier policy

Restricted content covers three legally distinct regimes that AGI does not conflate.

1. **Copyrighted content the user can legally obtain commercially.** Despicable Me, The Present, Pixar shorts. Pointer-only architecture. Annotations may be derivative works under the Berne Convention adaptation right; AGI consults with originators and, where necessary, with the rightsholder before publishing detailed annotations (frame-accurate dialogue transcripts are more legally exposed than shot-boundary timestamps).
2. **Content under non-redistribution research-use agreements.** International Affective Picture System (IAPS), the Human Connectome Project restricted package, ABCD restricted variables. AGI hosts annotations only when the upstream Data Use Agreement permits; the agreement is documented per-stimulus in `stimuli.json`.
3. **Content protected by IRB-approved Data Use Agreements with reidentification risk.** Clinical recordings, paediatric video. AGI does not host annotations of these stimuli unless the originator's IRB has explicitly approved the annotation effort and the annotation content has been reviewed for reidentification risk.

Access control for the restricted tier lives at the repository level: open-tier annotations are publicly readable on GitHub; restricted-tier annotations live in access-controlled GitHub repositories or DataLad siblings whose credentials are issued by the dataset originator (not by AGI). AGI provides the registry index; AGI never makes the access decision.

The hash-equivalence protocol is specified in Section 6.2. Verification runs at indexing time when the user registers a copy of a restricted stimulus and on download when the user attempts to fetch annotations that depend on that stimulus.

The Phase 1 federation-tier proof-of-concept lives with HBN movies (Section 13) and is contingent on a written Data Use Agreement from Child Mind Institute and the relevant rightsholders being in hand before launch.

### 11.2 Sustainability

- **Institutional host.** University of California San Diego, via the Swartz Center for Computational Neuroscience (SCCN). AGI is and remains a SCCN project. The host provides governance backing, archival commitment, and the institutional contact for takedown and Institutional Review Board referral. NEMAR, NSG, and SDSC resources are inherited via the host institution.
- **Funding target.** National Institutes of Health Funding Opportunity **RFA-MH-25-110**, "BRAIN Initiative: Data Archives for the BRAIN Initiative (R24 Clinical Trial Optional)." Issued by the National Institute of Mental Health, with co-funding from NEI, NIA, NIAAA, NIBIB, NICHD, NIDCD, NIDA, NINDS, NCCIH, and possibly OBSSR. Reissue of RFA-MH-20-600. Five-year project period; current pool is 4 million United States dollars per receipt date for 3–4 awards.
- **MPI team.** Seyed Yahya Shirazi (contact, UCSD/SCCN), Yaroslav Halchenko (Dartmouth, DataLad), Amit Majumdar (SDSC, Neuroscience Gateway), Kay Robbins (U. Texas San Antonio, HED working group).
- **Submission target.** Next application due date is June 24, 2026, with Letter of Intent due 30 days prior (approximately May 25, 2026). The NOFO expires June 25, 2026. Until award, AGI operates against bridge funding and existing SCCN/NEMAR infrastructure capacity.
- **Sub-domain framing.** The R24 mechanism funds one data archive per BRAIN sub-domain. AGI's sub-domain is **stimulus annotations** — a sub-domain not currently covered by any funded archive. OpenNeuro (human Magnetic Resonance Imaging / Electroencephalography / Magnetoencephalography / intracranial Electroencephalography), DANDI (cellular neurophysiology), and NEMAR (EEG / MEG / iEEG search) are peer archives in adjacent sub-domains; AGI extends NEMAR rather than overlapping with it. Sub-domain-overlap inquiries are routed to Christina Liu, PhD, PE (NIMH Scientific/Research Contact, christina.liu@nih.gov, 301-827-9193).
- **Responsiveness discipline.** The NOFO declares applications non-responsive if they are primarily focused on (i) generating experimental data, (ii) software tools / computational platforms / methods / models for data analysis / data standards, or (iii) data analysis / re-analysis / data curation. AGI's pitch is therefore a **data archive whose data is annotations**: standards (BIDS, HED, `hed-task`) are consumed not developed; tools (DataLad, `nemar-cli`, `nemar-tools`, NSG) are integrated not built as primary deliverables; analyses (Section 12) are integrated capabilities of the archive per the NOFO's permitted scope ("data archives teams will work with the research community to incorporate software tools that allow users to analyze and visualize the data"), not the primary deliverable. The Research Strategy of the application contains all five required sub-sections: standards and identifiers, data storage and protection, data accessibility, analysis and visualization tools, and timeline.
- **Storage and CI cost cap.** Open-tier text annotations and manifests are inexpensive and ride the existing NEMAR AWS Open Data hosting; CI compute and DOI minting flow through `nemar-tools`. The archive commits a documented cost cap per stimulus repository per year and a registry-level cost ceiling. CI runs on GitHub Actions for the open tier; the restricted tier runs on SCCN-managed CI when required.
- **Archive transfer on sunset.** If AGI loses funding or SCCN can no longer host, the final-state archive is deposited to a Zenodo Community via the same `nemar-tools` pipeline that mints per-version DOIs; per-stimulus repository contents and registry indices migrate to the Community deposit. The transfer policy is documented before launch and referenced in every Data Management and Sharing Plan that names AGI.
- **DOI tombstoning commitment.** Per DataCite rules, DOIs once minted are never withdrawn; tombstoning is the only acceptable response to legally-required removal.
- **Succession plan.** Each maintainer role carries a named successor or a named succession process. The core archive-maintainers group cannot fall below two members; if it does, an emergency succession process documented in the governance manifesto activates.

### 11.3 NIH Data Management and Sharing Policy alignment

AGI is positioned as an annotation overlay on top of the NIH-supported domain repositories (OpenNeuro for human Magnetic Resonance Imaging / Electroencephalography / Magnetoencephalography / intracranial Electroencephalography; DANDI for cellular Brain Research through Advancing Innovative Neurotechnologies neurophysiology; NEMAR for EEG / MEG / iEEG search), not as a replacement. The R24 mechanism's expectation that BRAIN-funded data be deposited to BRAIN Initiative data archives (NOT-MH-19-010) is satisfied because brain data continues to flow to the existing peer archives; AGI overlays an annotation commons whose primary data are the annotations themselves, with stable joins to those archives via the back-pointer index of Section 6.3.

Investigators using AGI in a Data Management and Sharing Plan can name AGI as the sharing destination for stimulus annotations and reference the relevant peer archive for the underlying brain data. AGI publishes a Data Management and Sharing Plan-readiness statement that maps each NIH "Desirable Characteristics for Data Repositories" criterion to an AGI commitment, names AGI's relationship to the relevant domain repository per stimulus, and provides a paste-able Data Management and Sharing Plan-language template that grantees include in their applications. AGI is funder-agnostic; analogous statements are provided for National Science Foundation, Wellcome, European Research Council, and Bundesministerium für Bildung und Forschung where requested.

For human-subjects-derived annotations, AGI is compliant with the 2023 NIH Policy for Data Management and Sharing, the NIH Genomic Data Sharing Policy where applicable, and the Genomic Data Sharing Plans guidance from August 2022 (NOT-OD-22-198); the compliance check is part of the per-PR CI for affected stimuli. The R24 application's required Protections for Human Subjects content is drafted in coordination with the UCSD philosophy ethics adviser (Section 10.1) and reflects the policies of NOT-MH-19-027 for clinical research data and safety monitoring.

### 11.4 Licensing

- **Defaults.** Stimuli that AGI hosts directly default to Creative Commons Zero (CC0) where redistributable; annotations default to Creative Commons Attribution 4.0 International (CC-BY-4.0). Share-alike (CC-BY-SA, ODbL) and non-commercial (CC-NC-*) clauses are avoided unless an originator requires them, because they create license-composition incompatibilities downstream.
- **Per-file licensing.** SPDX license identifiers in every sidecar; REUSE Software compliance verified in CI on every PR.
- **License composition.** A derived work that joins stimulus and annotation files inherits the most restrictive applicable license; in case of license incompatibility, the join is flagged at validation time and the user must obtain explicit permission. The composition rule is documented and referenced in every per-stimulus README.
- **DOI registrar.** AGI inherits NEMAR's dual DOI pipeline: Zenodo Communities for community-tier releases (via `nemar-tools`) and the University of California California Digital Library DataCite membership for institutional-grade library-persistent DOIs. The library-grade pipeline is preferred for long-term persistence of canonical annotation-perspective releases; Zenodo is used for development snapshots and community contributions. AGI can either reuse the existing NEMAR pipeline directly or extend it with an AGI-side configuration; the choice is implementation-level. DataCite Metadata Schema 4.5 is the underlying record format in both cases. The registrar choice piggy-backs on existing UCSD/SCCN institutional credentials and NEMAR operational practice rather than standing up a parallel pipeline.

## 12. Annotation-driven analyses and compute integration

AGI is a data archive; annotations are the data. This section describes an *integrated capability* of the archive — analysis and visualization tools that operate on archived annotations and on the brain datasets that join them — not a primary deliverable. The framing matches the NOFO's permitted scope ("data archives teams will work with the research community to incorporate software tools that allow users to analyze and visualize the data") and the R24 mechanism's "Analysis and Visualization Tools" Research Strategy sub-section.

Users select an annotation tier and a contrast or analysis recipe; AGI dispatches the job to the Neuroscience Gateway via REST application programming interface; NSG runs the job on SDSC compute; the result is fetched back and surfaced in the archive view. Users can extend with their own custom contrasts in the same NSG environment without leaving the archive's interaction surface. The pattern turns archived annotations into directly actionable analytic primitives rather than inert metadata, while the *primary archive deliverable* remains the FAIR commons of stimulus annotations and the back-pointer index.

This capability is differentiating because no peer archive offers it at the annotation-perspective level. NeuroScout offers fMRI predictor analyses against Pliers-extracted features only; OpenNeuro, NEMAR, and DANDI host data without running analyses on demand. NEMAR's existing NSG integration runs whole-pipeline EEGLAB jobs against a dataset; AGI extends the pattern from "run any pipeline against this dataset" to "run a standard recipe against this annotation, joining whatever datasets back-point to it." NEMAR and NSG are AGI collaborators, not external dependencies; the integration extends the existing stack rather than duplicating it.

### 12.1 Canonical analysis recipes (Phase 1)

For Electroencephalography datasets that consume an AGI stimulus:
- Per-annotation Event-Related Potential (ERP) locked to events in any `annot-<label>` tier.
- Per-annotation Event-Related Spectral Perturbation (ERSP) over a configurable time-frequency window.
- Cross-stimulus and cross-cohort grand average. The canonical Phase 1 example is HBN-EEG ERP locked to The Present's per-shot annotations, grand-averaged across the cohort: per-shot annotations are merged before averaging, producing a single grand-average ERP / ERSP indexed by the shot-boundary tier.
- Custom contrast: user-defined regressor against any annotation column.

For functional Magnetic Resonance Imaging datasets that consume an AGI stimulus:
- General Linear Model (GLM) with regressors derived programmatically from annotation columns.
- Standard contrasts (annotation-conditioned versus baseline; A-versus-B contrasts on categorical annotation columns).

For intracranial Electroencephalography (fast-follow modality):
- Event-locked high-gamma broadband power.
- Cross-stimulus grand averages where electrode coverage permits.

### 12.2 Architectural commitments

- **Recipes are first-class.** Each recipe has a stable identifier, a version history, a citation, and a contributor list, mirroring the data model for annotation perspectives. New recipes are contributed through pull request with the same review machinery.
- **Run-tracked.** Each invocation produces a job receipt with input identifiers (stimulus, annotation perspective version, dataset accession), recipe version, NSG job identifier, and output content hash. Job receipts are themselves citable; a paper that reports a recipe-derived figure can cite the receipt rather than a re-run.
- **Compute partner integration via REST.** NSG REST API is the dispatch surface; SDSC backs the compute and disk. AGI does not host its own compute. The connector is documented in the forthcoming `tooling/` directory with explicit conformance tests against NSG's published interface.
- **No silent re-runs.** When the underlying annotation perspective updates, prior job receipts remain valid and dereferenceable; users explicitly request a re-run against the new version.

### 12.3 Why this is load-bearing for the funding strategy

The annotation-driven-analyses capability is what turns AGI from a static FAIR commons into a productive analytic substrate. It is the strongest single argument for the BRAIN R24 application (Section 11.2): the archive does not just store annotations, it makes them computable against existing brain datasets through inherited compute infrastructure. The NSG and SDSC partnership is not aspirational; it is the same partnership SCCN already operates for NEMAR and EEGLAB users. The marginal infrastructure work for AGI is the recipe registry and the REST connector, not the compute fabric.

## 13. Phase 1 scope

The archive launches with two flagship stimulus repositories chosen to demonstrate the platform's value, plus a parallel cognitive-task track. A third flagship covering restricted-tier federation is held to Phase 2 contingent on legal readiness.

### 13.1 Phase 1 flagships

**Flagship 1 — Studyforrest (`Annotation-Garden/forrest-stimuli`).** Single-movie repository hosting the full annotation tier inventory developed by Hanke and collaborators across more than a decade of annotation papers. Pointer architecture for the copyrighted video; annotations published openly. Demonstrates the multi-track-timeline pattern, exercises the hash-equivalence protocol for codec-tolerant fingerprinting on audiovisual content, and round-trips existing ELAN annotations as the canonical adapter test. Hanke is a project collaborator. This is the launch flagship; the archive ships when Studyforrest ships.

**Flagship 2 — Natural Scenes Dataset (`Annotation-Garden/nsd-stimuli`).** Collection-level repository hosting 73,000 image identifiers and accumulating annotation layers (saliency, objects, scene graphs, captions, HED-tagged categorical annotations). Demonstrates the lightbox-grid pattern, the WordNet-anchored content tagging via COCO synset URIs, and the dataset back-pointer triple across the multiple OpenNeuro NSD deposits. Originator engagement (Kay, Naselaris) is a launch prerequisite per Section 5.9.

**Parallel cognitive-task track — single-PR contributions per localizer and per task battery.** Each carries canonical HED Generation 3 sidecars and `hedtsk_*` references: Fedorenko language localizer, Pinel localizer, ds000114 localizer, Human Connectome Project (HCP) task battery, Adolescent Brain Cognitive Development (ABCD) task battery, Cambridge Centre for Ageing and Neuroscience (Cam-CAN), Amsterdam Open MRI Collection (AOMIC), HCP Development. The cognitive-task track has its own dedicated maintainership (named in the governance manifesto) and runs in parallel to the flagships rather than as a fast-follow; the marginal cost of a localizer PR is low and the marginal benefit propagates broadly.

### 13.2 Phase 2 (deferred from v0 Phase 1)

**HBN movies (`Annotation-Garden/hbn-movies-stimuli`).** Multi-movie repository hosting the HBN movie collection (Despicable Me, The Present, Pixar shorts). The Present is the proof-of-concept for the per-movie annotation taxonomy: shot boundaries, action, story, audio, video, content, existence, and music as documented annotation tiers from the HBN-side annotation effort. Demonstrates the federation tier and the tier-type ontology seed.

This flagship is held to Phase 2 contingent on (a) a written Data Use Agreement from Child Mind Institute and the relevant rightsholders, (b) institutional general-counsel review of the annotation publication model relative to the Berne Convention adaptation right, (c) the federation-tier policy of Section 11.1 implemented end-to-end on at least one less legally complex stimulus first. The deferral reflects converging recommendations from the v0 review across both science and policy lenses.

### 13.3 Modality priority

Phase 1 prioritizes EEG and fMRI datasets that consume the flagship stimuli. iEEG is the immediate fast-follow modality once the EEG and fMRI surfaces are stable. The justification leads with corpus density: the Phase 1 corpus identifies the highest stimulus-and-annotation density in EEG and fMRI deposits across studyforrest, NSD, and HBN-EEG; iEEG datasets are smaller-N, electrode-coverage-idiosyncratic, and clinically constrained. The community size that benefits from EEG and fMRI launch is larger than the community that benefits from iEEG launch. The collaborator pool (Halchenko for DataLad and MRI; the HBN-EEG and ANNOTATE collaborations for EEG) is a supporting reason but not the primary one.

## 14. Open questions for v1.1 review

The following items remain open after v0 review. Some of v0's open questions are now resolved (resolutions noted).

- **Q1 — Repository granularity. RESOLVED.** Single-stimulus repos for stimuli with independent annotation effort histories (Forrest, individual HBN movies); collection repos for stimuli that are presented as a set and annotated at the set level (NSD images, THINGS images, AudioSet clips); dataset-family repos for cognitive-task localizers where the task is the unit. The dataset back-pointer triple is uniform on the tuple `(repo, stim_id, presentation_record)`.
- **Q2 — Where the back-pointer index lives. RESOLVED.** Per-repository `usedby.tsv` for portability; archive-level inverted index for query performance. Both are maintained; the registry is canonical for query.
- **Q3 — Annotation versioning semantics. RESOLVED.** Monotonic-integer versioning plus the change-type tag of Section 6.4. Calendar versioning is acceptable. Semantic Versioning is not used.
- **Q4 — `hedtsk_*` identifier surfacing. RESOLVED.** Required metadata in `stimuli.json` for any stimulus used in a paradigm with an existing `hedtsk_*` entry; sentinel value for paradigms not yet in the catalog, flagged for upstream proposal.
- **Q5 — Annotation-tier ontology. RESOLVED.** Proposed as a HED library schema candidate, populated from the union of MovieNet, AudioSet, ActivityNet, and existing studyforrest and HBN tier inventories; partner with AudioSet and ActivityNet maintainers for content vocabularies; HED working group is the steward.
- **Q6 — Federation tier mechanics. RESOLVED.** Repository-level access control. Hash-equivalence verification at indexing time and on download per Section 6.2.
- **Q7 — Credit attribution on forks.** Open. Forks inherit the upstream `CITATION.cff` until their first independent release; from that release forward they maintain their own. Whether a fork can "share" attribution with its upstream when it is a corrective rebase versus a divergent perspective needs case-by-case judgment in the working group.
- **Q8 — Sustainability funding model. RESOLVED.** Section 11.2 records the institutional host (UCSD/SCCN), the funding target (NIH BRAIN R24 RFA-MH-25-110 with the named MPI team), the bridge-funding posture until award, the inherited NEMAR / NSG / SDSC infrastructure that absorbs day-one operating cost, and the archive-transfer policy on sunset. The award itself is pending application submission and review; the PRD does not depend on award timing.
- **Q9 — Internationalization.** Per-annotation BCP-47 language tag is mandatory metadata. Translation representation is deferred to v1.1.
- **Q10 — Adapter conformance for community annotation tools.** Open. Bidirectional adapters to ELAN, Praat, BORIS, Datavyu, Label Studio are scoped in [`direction-papers/tools-direction.md`](direction-papers/tools-direction.md); the conformance contract (round-trip lossless on the canonical examples; CI test suite per adapter) is to be specified in the forthcoming `tooling/` directory.
- **Q11 — Originator dissent.** Open. When a dataset originator objects to a third-party annotation perspective, the working-group escalation ladder of Section 10.1 applies. The procedure for refusing to host a fork on originator-objection grounds is to be spelled out in the governance manifesto.
- **Q12 — Machine-generated versus human-authored annotations.** Open. Both share the same identifier, citation, and provenance model. Whether a `tier-type:machine-generated` flag is required at the perspective level (in addition to per-row provenance) needs review.
- **Q13 — Retraction propagation.** Substantially specified in Section 10.2; the CrossRef Crossmark integration is the next concrete deliverable.
- **Q14 — Anonymous and pseudonymous contribution.** Open. Pseudonymous contribution is permitted under a documented procedure; the procedure (institutional escrow of identity; per-jurisdiction templates) is to be drafted in the governance manifesto.

## 15. What this PRD is not

- Not an implementation plan. The implementation plan is a follow-on document drafted after this PRD is approved.
- Not the governance manifesto. The manifesto elaborates Section 10 and the open governance questions of Section 14; it is a separate document.
- Not the tooling specification. Per-adapter and per-pipeline specifications live in a `tooling/` directory to be created.
- Not the data-rollout plan. The dataset rollout phasing lives in [`direction-papers/data-direction.md`](direction-papers/data-direction.md).
- Not the science-thesis paper. The new-science argument lives in [`direction-papers/science-direction.md`](direction-papers/science-direction.md) and [`agi-white-paper.md`](agi-white-paper.md). The white paper's strong-reading framing (Section 1.2 / Section 8.1) should be revised to match the conservative-reading framing of Section 2 here.

## 16. Review process and change log

This document was reviewed by three independent agents acting as senior reviewers between PRD v0 (2026-05-03 draft) and v1 (this document). The reviewers were independent and did not coordinate; their findings converged on several points.

### 15.1 Reviewers

- **Senior cognitive-neuroscience reviewer.** 14 issues, 2 critical. Critique of mission framing, identifier model, taxonomy fit, Phase 1 scope.
- **Senior policy and FAIR steward reviewer.** 18 issues, 4 critical. Critique of FAIR commitments, federation policy, governance, sustainability, NIH data-sharing alignment, licensing.
- **Open-source systems prior-art surveyor.** Three-section deliverable (Adopt / Adapt / Differentiate) covering BIDS, DataLad, OpenNeuro, DANDI, Hugging Face Datasets, ImageNet, COCO, Visual Genome, AudioSet, ActivityNet, Wikidata, OBO Foundry, MovieNet, MovieGraphs, NeuroScout, Cognitive Atlas, RDoC, BrainMap, CogPO, Zenodo, DataCite, NEMAR.

### 15.2 Convergent findings (high-confidence v1 changes)

- **HBN movies demoted from Phase 1.** Three-way convergence (scientist: governance complexity; policy: Data Use Agreement not in hand; prior-art: hash-equivalence protocol unsolved). HBN movies move to Phase 2 contingent on legal readiness. Section 13.2.
- **Authorship-by-commit-count default removed.** Two-way convergence (scientist + policy). Replaced with `CITATION.cff` plus CRediT roles plus mandatory ORCID; release blocker if contributors disagree on order. Section 6.6.
- **Stakeholder lenses expanded.** Two-way convergence (scientist + policy). Added IRB / HRPP, journal editors, dataset originators, clinical and developmental researchers, computational psychiatry, funders / DCCs / advocates. Section 5.7–5.12.
- **Annotation-tier vocabulary as HED library schema.** Two-way convergence (scientist + prior-art). AGI proposes the vocabulary as a HED library schema candidate, partnering with AudioSet and ActivityNet maintainers; not minted as an AGI artifact. Section 7.3.
- **Stronger framing of Stim-BIDS provisional status.** BEP044 noted as provisional pending merge; back-pointer field has documented contingency if upstream declines. Section 4.

### 15.3 Major v1 additions

- **Section 6.2 — Stimulus equivalence.** Three-level protocol (byte-identity, codec-tolerant fingerprint, manual attestation) replacing v0's single-line hash claim. Addresses scientist Issue 2 and policy Issue 9.
- **Section 6.3 — Dataset back-pointer triple.** `(stimulus_hash, presentation_record, dataset_accession)` replaces v0's pair. Update protocol specified. Addresses scientist Issue 2.
- **Section 6.4 — Annotation versioning by change-type tag.** Replaces SemVer analogue. Addresses scientist Issue 3 and prior-art ADOPT 2 (Zenodo concept-DOI plus per-version-DOI).
- **Section 6.5 — Per-row provenance columns.** Mandatory `annotator`, `tool`, `tool_version`, `model_checkpoint`, `timestamp`. Addresses prior-art lesson 3 (Wikidata-style inline provenance).
- **Section 8 fifth representation pattern — Cohort overlay.** Addresses scientist Issue 9.
- **Section 9 — FAIR table replacing prose.** Addresses policy Issue 1; commits to annual F-UJI / RDA Maturity Model self-assessment.
- **Section 10 expanded with launch-blocking governance.** Named maintainers (pending), CoI policy, escalation ladder, Code of Conduct (Contributor Covenant 2.1), DCO, ORCID required, retraction propagation. Addresses policy Issue 3.
- **Section 11.1 — Federation and restricted-tier policy.** Three legal regimes enumerated; access-control venue chosen (repository-level); HBN deferred. Addresses policy Issue 2.
- **Section 11.2 — Sustainability.** Named institutional host (pending decision), funding source (pending decision), archive-transfer to Zenodo Community on sunset, cost cap, succession plan, DOI tombstoning. Addresses policy Issue 5.
- **Section 11.3 — NIH DMSP-readiness.** Maps AGI to NIH "Desirable Characteristics for Data Repositories"; positions AGI as overlay on OpenNeuro/DANDI; provides paste-able DMSP language. Addresses policy Issue 6.
- **Section 11.4 — Licensing.** SPDX, REUSE, default licenses (CC0 stimuli, CC-BY-4.0 annotations), license-composition rule, Zenodo Communities as DOI registrar. Addresses policy Issue 8.
- **Section 13.3 — Modality priority justification.** Leads with corpus density; collaborator availability is supporting reason. Addresses scientist Issue 7.
- **Cognitive-task track promoted from "fast follow" to parallel track.** Addresses scientist Issue 6.
- **Public reference URLs added** for `hed-task`, OpenNeuro, NEMAR, DANDI, NeuroScout, Cognitive Atlas, RDoC, BrainMap, CogPO, DataLad, Hugging Face Datasets, Zenodo Communities, BEP044. Addresses prior-art lesson 2.

### 15.4 Items flagged for follow-up rather than resolved in v1

- **White paper Section 1.2 / 8.1 strong-reading framing.** The scientist reviewer's Issue 1 critique applies to the white paper as well. v1 of this PRD calibrates Section 2 to the conservative reading; the white paper revision is a separate task.
- **Demonstrate citation rendering in three target-journal styles.** Specified as a v1 launch checklist item; the actual rendering is a separate deliverable.
- **Forthcoming governance manifesto.** Elaborates Section 10; drafts Q11 and Q14 procedures.
- **Forthcoming federation policy document.** Elaborates Section 11.1 with a fully-worked Data Use Agreement template (HBN movies as the worked example).
- **Forthcoming `tooling/` directory.** Specifies adapter conformance (Q10).
- **Cross-check terminology consistency.** Scientist Issue 14. To be done as a final pass before any external circulation.

### 16.5 User decisions resolved between v1 and v1.1

- **Institutional host:** UCSD via SCCN. Recorded in Section 11.2. AGI is and remains a SCCN project.
- **Co-leads:** Shirazi (UCSD/SCCN, contact lead) and Halchenko (Dartmouth, DataLad). Recorded in Section 10.1.
- **Advisory board:** Robbins, Delorme, Makeig, Hermes, Denissen. Recorded in Section 10.1; canonical roster maintained in `website/src/components/Team.tsx`.
- **Compute partners:** NSG and SDSC. Recorded in Section 4.
- **Funding target:** NIH BRAIN R24 RFA-MH-25-110. MPIs: Shirazi (contact), Halchenko, NSG/SDSC representative, Kay Robbins. Recorded in Section 11.2.
- **Code of Conduct:** BIDS-style, based on Contributor Covenant 2.1. Recorded in Section 10.1; specific enforcement contact still pending.
- **DOI registrar:** Inherited NEMAR pipeline (Zenodo Communities for community releases; UC California Digital Library DataCite for institutional-grade canonical releases). Recorded in Section 11.4.
- **Inherited NEMAR resources:** AWS Open Data hosting, `nemar-cli`, `nemar-tools`, `nemar-metadata`, `neuroschema`, `NEMAR-pipeline`, NSG REST API access. Recorded in Section 4 and throughout.

### 16.6 Major v1 → v1.1 additions

- **Section 12 — Annotation-driven analyses and compute integration.** New first-class capability commitment: per-annotation ERP / ERSP / grand-average / contrast computation via NSG REST API on SDSC compute. Canonical Phase 1 EEG / fMRI / iEEG recipes specified. Recipes are first-class identified objects with version, citation, and contributor list. Job receipts are themselves citable. NEMAR's existing NSG integration extended from "run pipelines against datasets" to "run recipes against annotations, joining whatever datasets back-point to them." This is the load-bearing capability for the BRAIN R24 application.
- **Section 4 SCCN / NEMAR / NSG / SDSC framing.** Position-relative-to-existing-work updated to record the inherited infrastructure stack (`nemar-cli`, `nemar-tools`, `nemar-metadata`, `neuroschema`, `NEMAR-pipeline`) and the architectural pattern (GitHub + AWS Open Data via S3 + Zenodo + UC California DataCite + Cloudflare D1). AGI is built on this stack rather than parallel to it.
- **Section 11.2 sustainability decisions resolved.** Institutional host (UCSD/SCCN), funding target (RFA-MH-25-110 R24, MPI structure), CI cost (rides existing NEMAR AWS Open Data hosting), archive transfer on sunset (Zenodo Community via `nemar-tools`), DOI tombstoning. Bridge funding posture explicit until R24 award.
- **Section 11.4 licensing decisions resolved.** DOI registrar specified as the dual NEMAR pipeline (Zenodo Communities + UC California Digital Library DataCite). The library-grade DOI is preferred for canonical annotation-perspective releases.
- **Section 10.1 governance roster filled.** Co-leads and advisory board named with affiliations and roles. Code of Conduct framed as BIDS-style.

### 16.7 User decisions resolved between v1.1 and v1.2

- **SDSC PI on R24 MPI team:** Amit Majumdar. Recorded in Section 11.2.
- **Ethical considerations adviser:** A UCSD philosophy department contact (specific name pending) advises on ethics; same contact is a candidate for Code of Conduct enforcement. Recorded in Section 10.1 and 11.3.
- **R24 mechanism specifics:** RFA-MH-25-110 full mechanism specifics integrated into Section 11.2 (June 24 2026 due date with LOI ~May 25 2026; $4M total per receipt date for 3-4 awards; five-year project period; sub-domain framing as stimulus annotations; non-responsiveness discipline; Christina Liu as NIMH Scientific Contact).

### 16.8 Major v1.1 → v1.2 changes

- **Section 11.2 — RFA-MH-25-110 specifics integrated.** Mechanism details, timing, MPI team with Amit Majumdar named, sub-domain framing, responsiveness discipline. The PRD now reads as a coherent project description aligned to a specific R24 application.
- **Section 12 — NOFO permitted-scope framing.** Annotation-driven analyses tightened from "first-class capability" wording to explicit alignment with the NOFO's "Analysis and Visualization Tools" Research Strategy sub-section: integrated capability of the archive, not a primary deliverable. The framing protects the application from non-responsive determination.
- **Section 11.3 — DMSP alignment grounded.** Added explicit reference to NOT-MH-19-010 (BRAIN data sharing), NOT-OD-22-198 (Genomic Data Sharing), NOT-MH-19-027 (clinical research data and safety monitoring), and the relationship between AGI as annotation overlay and the BRAIN-funded data flowing to peer archives.
- **Section 10.1 — Ethics-adviser line added.** UCSD philosophy contact serves the human-subjects-protections content of the R24 Research Strategy and is a candidate Code of Conduct enforcement contact.

### 16.9 User decisions still required

- Specific name of the UCSD philosophy ethics adviser (Section 10.1, 11.3).
- Code of Conduct enforcement contact (likely overlapping with the ethics adviser; final assignment pending).
- Initial members of the core archive-maintainers group beyond the co-leads (Section 10.1).
- Whether to merge or relegate the three direction papers per scientist Issue 12 (out of scope for the PRD itself; a documentation-architecture decision).
- LOI submission to NIMH for RFA-MH-25-110 (~May 25, 2026 deadline if targeting June 24, 2026 application date). The LOI is non-binding but signals intent and aids reviewer-pool planning.

---

*Document version: v1.2. Date: 2026-05-03. Author: Annotation Garden Initiative. Status: open for second-round review.*
