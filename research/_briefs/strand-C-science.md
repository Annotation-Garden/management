# Strand C, Science of Annotation-Driven Brain Dynamics (Phase 1 brief)

**Goal:** populate `research/collection/science/` with at least 25 paper-cards on the methods and findings that link rich stimulus annotations to neural responses.

## Scope

Cover seven themes. This strand explicitly extends, does NOT duplicate, the ANNOTATE R01 lit review. Focus on what is sparse there.

### 1. Annotation-driven encoding models
- Voxel-wise encoding (Kay 2008, Naselaris 2011)
- Hierarchical linguistic encoding (Huth 2016)
- Visual ventral stream models (Yamins 2014, Conwell 2024)
- Multi-perspective / variance partitioning (de Heer 2017, LeBel 2023)
- HRF estimation per voxel: GLMsingle (Prince 2022)
- Population receptive field models (Wandell, Dumoulin 2008; Guest 2025 pulvinar)

### 2. Annotation-driven decoding
- Visual reconstruction (Takagi & Nishimoto 2023, Ozcelik 2023, Scotti et al. NSD MindEye 1/2)
- Semantic decoding from cortex (Tang & Huth 2023, language decoder)
- Cross-subject decoding & alignment

### 3. Inter-subject correlations & hyperalignment
- ISC foundations: Hasson 2004, Lerner 2011
- Searchlight ISC and hyperalignment (Haxby 2011, Guntupalli 2016)
- Idiosynchrony (Finn 2020)
- Movie-watching connectivity (Vanderwal 2019)

### 4. Event segmentation / boundaries
- Event Segmentation Theory (Zacks)
- Neural event boundaries (Baldassano 2017 schemas; Geerligs 2022)
- Hippocampal "event cells" in Bang You're Dead (Zheng 2022 type work)
- Visual cuts vs semantic novelty (Cohen, Chen, Hasson)

### 5. Foundation models with annotation supervision
- DIVER-1 (Han 2025), large EEG foundation model
- NeuroSwift (Zhang 2025)
- LaBraM (Jiang 2024), large EEG transformer
- BIOT, Brant, EEGPT
- xiong2025eegfmbench, systematic review showing foundation models often don't beat baselines
- Lahner 2025 MOSAIC, multi-dataset training
- CLIP-style annotation conditioning analogs in neuroimaging
- NeurIPS 2025 EEG Foundation Challenge (Aristimunha 2025)

### 6. Annotation-response curves & sufficiency studies
- Learning-curve / data-scaling work in fMRI encoding (where exists)
- Naspi 2021, perceptual vs taxonomic granularity
- Memory encoding and feature granularity (Naspi, Cooper)
- Anything on "how much annotation is enough?", likely scarce (this is the gap ANNOTATE addresses)

### 7. Cross-modal & cross-dataset generalization
- iEEG-fMRI alignment (Hermes 2017, 2019; Berezutskaya 2022)
- EEG-fMRI RSA (Cichy 2016)
- Cross-modality on shared stimuli (THINGS multimodal, Hebart 2023)
- Wagner 2019 OHBM Forrest Gump empirical contrasts (referenced in ANNOTATE preliminary studies)

## Per-entry deliverable

Same folder pattern: `research/collection/science/<slug>/{card.md, source.pdf?, source.md, meta.json}`.

`type: paper`, `strand: science`. Tags should capture the methodological theme + dataset(s) used + modality. Markdown extraction (`source.md`) is required even when the PDF is paywalled, it's our offline reference for synthesis and drafting.

## Per-card "Open questions" emphasis

Strand C cards must emphasize the **Open questions / limitations** section. These feed Phase 2's gap analysis and Phase 3's direction documents.

## Seed material

The ANNOTATE lit review covers themes 1, 2, 5, 7 well. Strand C's distinctive contribution: **deeper coverage of themes 3, 4, and 6**, plus surfacing where event annotations and cognitive task annotations have been used together (rare).

## Skills to use

- `opencite:opencite`
- `manuscript:manuscript-writing` for prose
- `opencite:literature-review` knowledge for organizing themes (but DO NOT write a synthesis, that's Phase 2)

## Acceptance criteria

- [ ] ≥25 entries
- [ ] All 7 themes covered with ≥2 entries each
- [ ] Every entry folder has `card.md`, `source.md`, and `meta.json`
- [ ] `source.pdf` archived for ≥50% of entries (mix of OA and paywalled in this strand)
- [ ] Strong emphasis on `Open questions / limitations` in every card
- [ ] BibTeX in science.bib
- [ ] INDEX.md categorized by theme

## Out of scope

- Writing synthesis prose (Phase 2)
- Drafting the white paper (Phase 3)
- Tool / dataset descriptions beyond what is needed to characterize each paper's method
