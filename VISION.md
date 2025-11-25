# Annotation Garden Initiative: Vision

## The Future We're Building

Imagine a world where every annotation of a naturalistic stimulus becomes a permanent contribution to scientific knowledge. Where a graduate student's careful scene boundary annotations of a movie clip accumulate with thousands of other perspectives across labs, forming a rich, multi-layered understanding that any researcher can build upon.

This is the Annotation Garden.

## Core Vision Statement

**Transform isolated annotation efforts into cumulative scientific knowledge through open, collaborative infrastructure.**

## The Problem

Modern neuroscience has embraced naturalistic stimuli. Researchers show participants movies, play audio stories, display complex natural images. This ecological validity comes at a cost: these stimuli require extensive annotation to be scientifically useful.

Currently:
- **Labs work in isolation**: The same Pixar movie gets annotated for scene boundaries in Boston, emotional content in Berlin, and semantic features in Beijing
- **Annotations are ephemeral**: When a postdoc leaves, their careful annotation work often disappears into supplementary materials
- **Formats are incompatible**: CSV files with custom column names, ELAN projects, lab-specific JSON schemas
- **Discovery is impossible**: There's no way to know if someone has already annotated the exact stimulus you're using

The result is thousands of hours of duplicated effort and missed opportunities for meta-analysis.

## Our Solution: Infrastructure, Not Just Tools

AGI is not another annotation tool. We're building **infrastructure**:

### 1. Stimulus Repositories as Commons

Each major naturalistic stimulus becomes a collaborative Git repository. Like Wikipedia for stimulus annotations:
- Multiple annotation "layers" coexist as branches
- Version control preserves the full history of annotations
- Pull requests enable quality review and discussion
- Issues provide forums for annotation philosophy debates

### 2. Branches as Annotation Layers

Different scientific perspectives on the same stimulus live as parallel branches:
```
main                    # Canonical/accepted annotations
├── scene-boundaries    # Shot cuts and scene structure
├── emotional-arcs      # Valence, arousal, emotion labels
├── semantic-content    # Objects, actions, relationships
├── auditory-features   # Music, speech, sound effects
└── lab-xyz-custom      # Lab-specific annotations
```

Branches can be merged, compared, and stacked. A researcher studying emotion can combine the `emotional-arcs` branch with `scene-boundaries` to analyze emotional changes at scene transitions.

### 3. Standards as Common Language

All annotations speak the same language:
- **BIDS** (Stim-BIDS / BEP044) for file organization
- **HED** for semantic annotation vocabulary
- **events.tsv** format for machine-readable storage

This standardization enables:
- Automated validation (is this annotation well-formed?)
- Cross-study comparison (these annotations mean the same thing)
- Tool interoperability (any HED-compatible tool can read AGI annotations)

### 4. Visualization as Understanding

A web interface at annotation.garden lets researchers:
- View annotations overlaid on stimuli
- Compare different annotation layers side-by-side
- Explore how annotations relate to neural data
- Contribute new annotations without command-line expertise

## What Success Looks Like

### For Individual Researchers
- Find existing annotations instead of creating them from scratch
- Build on others' work and get credit for contributions
- Access rich, multi-perspective annotations for analysis

### For the Field
- Meta-analyses across studies using the same stimuli
- Reproducible science with versioned annotation references
- Accumulated knowledge that grows over time

### For Science
- Understanding how brain responses relate to stimulus features
- Cross-modal, cross-population, cross-task comparisons
- Foundation for brain encoding models with rich stimulus descriptors

## Design Principles

### Open by Default
- All infrastructure is open source
- Annotations are openly licensed
- Governance is transparent

### Built for Collaboration
- GitHub-native workflow (Issues, PRs, branches)
- Clear contribution guidelines
- Credit attribution for all contributors

### Standards-First
- BIDS compliance from the start
- HED validation in CI/CD
- No proprietary formats

### Pragmatic Incremental Growth
- Start with what exists (studyforrest annotations)
- Add value to existing datasets
- Grow through demonstrated utility

## The Garden Metaphor

We chose "Annotation Garden" deliberately:
- **Gardens require cultivation**: Annotations need care, review, refinement
- **Gardens grow over time**: Each contribution enriches the soil
- **Gardens are shared spaces**: Multiple gardeners tend different plots
- **Gardens produce harvests**: The work enables future discoveries

As researchers cultivate this garden together, we grow not just annotations but understanding.

## Long-Term Vision

In 5-10 years, AGI could become the standard way neuroscience annotations are shared:
- New datasets published with AGI annotation repositories
- Grant applications referencing AGI infrastructure
- Papers citing specific annotation versions
- Cross-institutional working groups maintaining annotation layers
- AI models trained on AGI's rich annotation corpus

The annotation problem is an infrastructure problem. AGI provides that infrastructure.

---

*For the detailed technical implementation, see the [White Paper](agi-white-paper.md).*
