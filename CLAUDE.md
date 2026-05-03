# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository serves as the management and planning hub for the Annotation Garden Initiative (AGI), an open infrastructure for collaborative, multi-layered annotation of stimuli used in neuroscience research. The initiative is part of the GitHub organization: https://github.com/Annotation-Garden

### Mission
AGI addresses the fragmentation problem in neuroscience research where researchers repeatedly annotate the same naturalistic stimuli (images, videos, audio) in isolation. By building on stimuli-BIDS (BEP042) and HED specifications, AGI enables researchers to share, refine, and build upon stimulus annotations collaboratively through GitHub-based version control.

### Key Components to Be Developed

1. **Management Repository** (annotation-garden): Central coordination and documentation
2. **Assets Repository**: AGI logo, templates, color themes, design guidelines
3. **Website** (annotation-garden.github.io → annotation.garden): Modern platform inspired by datalad.org
4. **Image Annotation Tool**: Forked from https://github.com/neuromechanist/image-annotation with AGI branding and HED integration

### Flagship Datasets
- Natural Scenes Dataset (NSD): 73,000 COCO images with 7T fMRI
- Forrest Gump (studyforrest.org): 2-hour movie with temporal annotations
- HBN Movies: Child Mind Institute collection (Despicable Me, The Present, Pixar shorts)

## Repository Structure

This repository contains:
- `agi-white-paper.md`: Comprehensive project vision and implementation roadmap
- `AGI-square.png/svg/af`: Logo files (Affinity Designer source)
- `apple_open_letter.md`: Advocacy document for open science principles
- Design assets and planning documents

## Design Philosophy

### AGI Branding
- Logo: AGI-square.* files contain the official logo
- Positioning: Logo should appear top-left in all AGI applications
- Theme: Consistent color scheme and visual identity across all repositories

### Standards Integration
- **BIDS**: Brain Imaging Data Structure, particularly stimuli-BIDS (finalizing end of 2025)
- **HED**: Hierarchical Event Descriptors (hedtags.org) for semantic annotation framework
- **GitHub-based**: Version control for annotations, PRs for contributions, Issues for discussions

## Development Guidelines

### Stimulus Repository Structure
When creating new stimulus repositories, follow this structure aligned with stimuli-BIDS:
```
stimulus-name/
├── stimuli/
│   └── [stimulus files or pointers]
├── annotations/
│   ├── visual-saliency/
│   │   ├── events.tsv
│   │   └── events.json
│   ├── emotional-ratings/
│   └── scene-boundaries/
├── README.md
└── LICENSE
```

### Version Control Approach
- Atomic commits for all changes
- Create branches for non-minor edits
- Make PRs after testing
- Commit messages should be concise and descriptive (no emojis, no Claude co-authorship)

### GitHub Organization Management
- Organization URL: https://github.com/Annotation-Garden
- Repositories should follow naming convention: lowercase with hyphens
- Each repository should have clear README with AGI context

## Implementation Phases

**Phase 1 (Months 1-3)**: NSD static image annotations, core infrastructure
**Phase 2 (Months 4-6)**: Forrest Gump temporal annotations, continuous annotation tools
**Phase 3 (Months 7-12)**: HBN movies, federation protocols for copyright-protected stimuli

## Key References

- White paper: `agi-white-paper.md`
- HED specifications: https://hedtags.org
- Stimuli-BIDS: https://github.com/bids-standard/bids-specification/pull/2022
- NeurIPS EEG Competition: https://eeg2025.github.io
- Existing image annotation dashboard: https://neuromechanist.github.io/image-annotation

## Related Documents

When planning or researching, check for these files if they exist:
- `plan.md`: Implementation plans and next steps
- `ideas.md`: Feature ideas and enhancements
- `scratch_notes.md`: Working notes and temporary thoughts
- `research.md`: Background research and literature notes

All planning documents should be added to .gitignore to keep the repository focused on deliverables.
