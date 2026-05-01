# Strand A — Tools Landscape (Phase 1 brief)

**Goal:** populate `research/collection/tools/` with at least 25 paper-cards covering the annotation-driven research toolchain.

## Scope

Cover five categories. Aim for breadth first, depth where it matters for AGI.

### 1. Annotation tools (manual + semi-automatic)
- ELAN, Praat, Anvil, Datavyu, BORIS
- HED tools: HED-Python validator, HED-JS, HED schema browser, hed-curation
- HEDit (annotation.garden/hedit) — internal, but card it for reference
- Pliers (https://github.com/PsychoinformaticsLab/pliers) — multimodal feature extraction
- ELAN-to-BIDS, TextGrid-to-BIDS converters
- Bidsannotator, OpenNeuro annotation viewers
- LabelStudio, CVAT, Prodigy (general-purpose annotators researchers repurpose)

### 2. Analysis pipelines / encoding-model libraries
- EEGLAB (incl. plugins: ICLabel, DIPFIT, AMICA, Unfold) — Delorme et al.
- MNE-Python
- fMRIPrep, MRIQC, sMRIPrep
- GLMsingle (Prince et al.)
- Unfold toolbox (Ehinger & Dimigen) — regression-based deconvolution
- Voxelwise / encoding-model packages: pycortex, voxelwise_tutorials, himalaya, naplib
- mTRF Toolbox (Crosse et al.)
- BIDS-Apps ecosystem (https://bids-apps.neuroimaging.io)

### 3. AI-assisted annotators (incl. video / multimodal)
- CLIP / OpenCLIP — text-image alignment for stimulus features
- Whisper / WhisperX — speech-to-text + alignment
- Video-language models: Qwen-Omni / VideoLLaMA / VideoLLM-online (Fong 2025), LLaVA-Video
- Multi-agent annotation: CrowdAgent (Qin 2025), neuro-symbolic temporal consistency (Choi 2024)
- Pliers as orchestration; HEDit multi-agent architecture; Detoxify, GroundingDINO for object grounding
- Subtitle / scene-cut: PySceneDetect, ffmpeg scene change

### 4. Infrastructure / sharing platforms
- OpenNeuro (Markiewicz et al. 2021)
- NEMAR (Delorme lab — EEG focus)
- DataLad (Halchenko et al. 2021)
- OSF, Zenodo, FigShare
- HuggingFace (for foundation-model weights / datasets)
- NeuroScout (de la Vega et al. 2022)
- DANDI archive, BIDS-Apps registry, ReproNim containers (`///repronim/containers`)
- BIDS-Validator (CLI + web), HED-validator integration
- GitHub-based annotation patterns (e.g., Pliers + Neuroscout pipelines)

### 5. Standards / specifications
- BIDS core (Gorgolewski et al. 2016) and BEPs:
  - BEP044 / Stim-BIDS
  - BEP010 (PET), BEP020 (eye-tracking), BEP021 (Common Electrophys Derivatives), BEP037 (HED)
- HED schema and HED-SCORE (Robbins et al. 2021, Scientific Data 2025)
- COBIDAS (Nichols 2017) — fMRI rigor
- DataLad YODA principles
- FAIR principles (Wilkinson 2016)
- DICOM / NIfTI / EDF / .set / NWB (Neurodata Without Borders)

## Per-entry deliverable

Create folder `research/collection/tools/<slug>/` containing:
- `card.md` from the schema (`type` ∈ {tool, platform, standard, paper}; `strand: tools`)
- `source.pdf` — for tools, this is the tool's primary methods paper if redistributable. For tools without a paper, omit and set `pdf_status: not-applicable`.
- `source.md` — always required. For papers, markdown extraction. For tools without a paper, snapshot of the canonical README / docs landing page.
- `meta.json` with provenance (DOI / source URL, retrieval date, license, sha256 if PDF archived)
- BibTeX entry appended to `research/collection/tools/tools.bib`
- One-line entry appended to `research/collection/tools/INDEX.md` under the right category heading

Use `opencite` for DOI lookup, PDF retrieval (where licensing permits), and PDF→markdown conversion.

## Seed material

Skim `grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md` and `submission/research-strategy.tex` — many tools are cited there. Import where useful, mark `imported_from: grant-proposals/...`.

## Skills to use

- `opencite:opencite` for paper retrieval, DOI lookup, BibTeX export
- `manuscript:manuscript-writing` for prose discipline (no em-dashes, define abbreviations on first use)

## Acceptance criteria

- [ ] ≥25 entries across all 5 categories
- [ ] Each category has ≥3 entries
- [ ] Every entry folder has `card.md`, `source.md`, and `meta.json`
- [ ] `source.pdf` archived for ≥60% of entries that have a redistributable paper
- [ ] All entries have BibTeX in tools.bib
- [ ] INDEX.md fully populated with categorized one-liners
- [ ] No prose synthesis — that's Phase 2

## Out of scope

- Tools unrelated to annotation, neuroimaging, or large-scale event-structured data
- Drafting the white paper or direction documents
- Comparing or ranking tools — collection only
