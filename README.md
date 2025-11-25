<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Annotation-Garden/assets/main/AGI-square-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/Annotation-Garden/assets/main/AGI-square.svg">
  <img alt="Annotation Garden Initiative" src="https://raw.githubusercontent.com/Annotation-Garden/assets/main/AGI-square.svg" width="120" align="right">
</picture>

# Annotation Garden Initiative

**Open infrastructure for collaborative annotation of neuroscience stimuli**

[![Website](https://img.shields.io/badge/website-annotation.garden-teal)](https://annotation.garden)
[![License](https://img.shields.io/badge/license-CC--BY--4.0-green)](LICENSE)

---

## Vision

Transform isolated annotation efforts into cumulative scientific knowledge. Every lab annotating the same stimulus should contribute to a shared resource that grows richer over time.

## Mission

Build open infrastructure that enables researchers to share, refine, and build upon stimulus annotations through GitHub-based collaboration, BIDS/HED standards compliance, and modern visualization tools.

---

## The Problem We Solve

Labs repeatedly annotate the same naturalistic stimuli in isolation:

- The same movies, images, and audio get re-annotated for each study
- Annotations remain siloed in supplementary materials or lab servers
- Incompatible formats confound meta-analyses
- Years of annotation work are lost when researchers move on

**The Annotation Garden Initiative transforms this fragmentation into collaborative growth.**

---

## Our Approach

| Principle | Implementation |
|-----------|----------------|
| **Branches as Layers** | Different annotation perspectives (scenes, emotions, objects) live as Git branches that stack and merge |
| **Standards-Based** | Built on BIDS and HED specifications for machine-readable, interoperable annotations |
| **AI-Accelerated** | VLMs provide initial drafts; humans refine and validate |
| **Cross-Modal** | Compare annotations across modalities, populations, tasks, and environments |

---

## Flagship Datasets

| Dataset | Status | Description |
|---------|--------|-------------|
| **[Natural Scenes Dataset](https://naturalscenesdataset.org)** | Active | 73,000 COCO images from 7T fMRI study |
| **[Forrest Gump](https://studyforrest.org)** | Coming | 2-hour movie with rich temporal annotations |
| **[HBN Movies](https://eeg2025.github.io)** | Planned | Child Mind Institute developmental EEG collection |

---

## Repository Structure

This management repository contains governance and coordination documents for the AGI organization:

| Document | Purpose |
|----------|---------|
| [White Paper](agi-white-paper.md) | Technical vision and implementation roadmap |
| [Vision](VISION.md) | Comprehensive vision and design philosophy |
| [Contributing](CONTRIBUTING.md) | Guidelines for contributing to AGI |
| [Governance](GOVERNANCE.md) | Decision-making and organizational structure |

### Related Repositories

| Repository | Purpose |
|------------|---------|
| [website](https://github.com/Annotation-Garden/annotation-garden.github.io) | Landing page at annotation.garden |
| [image-annotation](https://github.com/Annotation-Garden/image-annotation) | VLM-powered annotation tool |
| [assets](https://github.com/Annotation-Garden/assets) | Logos, design guidelines |

---

## Standards Integration

AGI builds on established neuroscience standards:

- **[BIDS](https://bids.neuroimaging.io/)**: Brain Imaging Data Structure, particularly [Stim-BIDS (BEP044)](https://github.com/bids-standard/bids-specification/pull/2022)
- **[HED](https://hedtags.org)**: Hierarchical Event Descriptors for semantic annotation vocabulary
- **[OpenNeuro](https://openneuro.org)**: Integration with existing neuroimaging data archives

### Stimulus Repository Structure

```
stimulus-name/
├── stimuli/              # Files or pointers
├── annotations/
│   ├── <annotation-type>/
│   │   ├── events.tsv
│   │   └── events.json
├── README.md
└── LICENSE
```

---

## Get Involved

- **Try the tool**: [annotation-garden.github.io/image-annotation](https://annotation-garden.github.io/image-annotation/)
- **Read the vision**: [White Paper](agi-white-paper.md) | [Vision Document](VISION.md)
- **Contribute**: See our [Contributing Guide](CONTRIBUTING.md)
- **Discuss**: Open an issue in this repository

---

## Implementation Roadmap

**Phase 1 (Q4 2025 - Q1 2026)**: NSD static image annotations, core infrastructure
**Phase 2 (Q2 2026)**: Forrest Gump temporal annotations, continuous annotation tools
**Phase 3 (Q3-Q4 2026)**: HBN movies, federation protocols for copyright-protected stimuli

---

<p align="center">
  <i>Cultivating knowledge together</i><br>
  <a href="https://annotation.garden">annotation.garden</a>
</p>
