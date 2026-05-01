# Strand B — Data Landscape (Phase 1 brief)

**Goal:** populate `research/collection/data/` with at least 25 paper-cards spanning naturalistic stimuli and cognitive task datasets, with an organizing hierarchy.

## Scope

Cover six categories. The naturalistic ↔ cognitive-task spectrum is the throughline.

### 1. Naturalistic — static images
- Natural Scenes Dataset (NSD): fMRI, ECoG/iEEG, EEG, MEG variants
  - NSD-fMRI (Allen 2022), NSD-iEEG (Huang 2024), NSD-EEG (Xu 2024 alljoined / Brotherwood 2024), NSD macaque unit (Li 2025 triplen)
- THINGS initiative (Hebart 2023): fMRI, MEG, EEG with shared image set
- BOLD5000
- COCO + free-form captions (used for AI-supervised stimulus features)

### 2. Naturalistic — video / film
- StudyForrest (Hanke 2014, Hausler 2021); Forrest Gump 7T fMRI + 3T variants + MEG (ds003633) + eye-gaze (Hanke 2016)
- HBN Movies: Despicable Me, The Present, Pixar shorts (Alexander 2017; Shirazi 2024 HBN-EEG)
- "Bang! You're Dead" — Hitchcock — ds003688 / ds004798 (single-unit + iEEG + fMRI) (Aly et al.)
- Sherlock fMRI (Chen et al.)
- 7T-clip set / "Naturalistic Neuroimaging Database" (Aliko 2020)
- Pixar / Inscapes (Vanderwal 2015 — passive viewing inscapes)

### 3. Naturalistic — audio / narrative
- Pieman (Yeshurun 2017) and Pieman fMRI / EEG
- Moth Radio Hour stories (Huth 2016)
- Podcast / Lectures (LePelley)
- Music: NaturalSounds-fMRI (Norman-Haignere 2015), MusicNet
- Spoken book / narrative datasets (Brennan, Hale)

### 4. Cognitive task batteries (sporadic but rich)
- HBN cognitive task suite: Surround Suppression, Contrast Change Detection, Symbol Search, Sequence Learning, etc. (Shirazi 2024)
- ds00*-style OpenNeuro single-task collections (sample; survey for diversity)
- AOMIC (Snoek 2021)
- MATCH / Cam-CAN cognitive battery (Shafto 2014)
- ABCD task fMRI tasks (high-N developmental)
- HCP task fMRI (Barch 2013)
- MyConnectome (Poldrack et al.)

### 5. Hybrid / mixed paradigms
- HCP / dHCP — resting + task + diffusion
- HBN-EEG combined (movies + tasks + resting)
- LEMON (Babayan 2019) — resting + tasks
- DEAP / SEED — emotion-elicitation video + EEG

### 6. Single-stimulus benchmark sets
- Localizer batteries (FFA / PPA localizers, motion / language localizers)
- Open iEEG-fMRI shared stimulus sets (Berezutskaya 2022)
- DECCO / ds002338 / ds002550 type micro-datasets used as cross-validation

## Per-entry deliverable

Same folder pattern as Strand A: `research/collection/data/<slug>/{card.md, source.pdf?, source.md, meta.json}`.

`type: dataset` (or `paper` for benchmark/methods papers). `strand: data`. Required front-matter must include:
- `modalities` list — be precise
- `license` — copyright matters for HBN movies, Forrest Gump, etc.
- `tags` — at minimum: stimulus type (image/video/audio/task), age range, N

For datasets, `source.pdf` is the dataset's primary descriptor paper. `source.md` should additionally summarize key dataset README / data dictionary contents (BIDS structure, modalities, sample size, access conditions).

## Hierarchy capture

Beyond per-entry cards, fill `research/collection/data/INDEX.md` with the dataset hierarchy: each entry placed under the right category, with one-liners noting:
- Modality coverage
- Approximate N
- Annotation density (none / minimal / moderate / rich)
- AGI hook (why a Garden contributor would care)

## Seed material

Heavy reuse from `grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md` Table 2.5 + sections 2.1–2.4. Mark `imported_from`.

## Skills to use

- `opencite:opencite` for DOIs and citation pulls
- `neuroinformatics:bids-conversion` skill knowledge (if needed) to verify dataset structure claims

## Acceptance criteria

- [ ] ≥25 entries
- [ ] All 6 categories have ≥2 entries
- [ ] Every entry folder has `card.md`, `source.md`, and `meta.json`
- [ ] `source.pdf` archived for ≥70% of entries (dataset descriptor papers are mostly OA)
- [ ] INDEX.md captures the naturalistic ↔ cognitive-task hierarchy explicitly
- [ ] Every card has `modalities`, `license`, `tags` populated
- [ ] BibTeX in data.bib

## Out of scope

- Tool descriptions (those go in Strand A)
- Encoding/decoding methodology (Strand C)
- Synthesis / hierarchy taxonomy beyond INDEX.md categorization (Phase 2)
