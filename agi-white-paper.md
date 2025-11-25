# The Annotation Garden Initiative: FAIR Annotation Platform for Brain-Behavior Research

## Executive Summary

The Annotation Garden Initiative (AGI) establishes an open infrastructure for collaborative, multi-layered annotation of stimuli used in neuroscience research. Building on emerging standards including Stim-BIDS (BEP044) and HED specifications, AGI addresses the critical gap between increasingly complex naturalistic stimuli and the need for standardized, reusable annotations. Through GitHub-based version control and modern web interfaces, AGI enables researchers to share, refine, and build upon stimulus annotations across studies, transforming how we document and analyze brain responses to complex sensory experiences.

## The Fragmentation Problem

Modern neuroscience increasingly employs naturalistic stimuli—from the 73,000 COCO images prepared for the Natural Scenes Dataset (Allen et al. 2021) to the 2-hour audiovisual experience of Forrest Gump (Hanke et al. 2014) and the diverse movie-watching paradigms in the Child Mind Institute's Healthy Brain Network (Alexander et al. 2017), which now powers the NeurIPS 2025 EEG Foundation Challenge (eeg2025.github.io). Each dataset represents thousands of hours of wasted researcher time as labs independently annotate the same stimuli: scene boundaries, emotional valence, semantic content, acoustic features, narrative structure. Yet these annotations remain siloed within individual studies, limiting reproducibility and preventing the field from building cumulative knowledge about brain-behavior relationships.

Current approaches fragment across tools (ELAN, Praat, custom scripts), formats (CSV, JSON, proprietary), and storage (lab servers, supplementary materials, forgotten hard drives). When researchers analyze the same Pixar movie shown to children in HBN-EEG studies (Shirazi et al. 2024) or the Forrest Gump stimulus used across multiple sites, they repeatedly annotate the same features—wasting effort and introducing inconsistencies that confound meta-analyses. AGI transforms this fragmentation into collaborative growth.

## Architecture for Collaboration

AGI implements a hub-and-spoke architecture where each stimulus becomes a collaborative repository, with Git branches serving as annotation layers. This "branches as layers" model enables independent development of different annotation perspectives—scene boundaries, emotional arcs, object detection that can be stacked, compared, and merged through standard Git workflows. Researchers fork repositories to create their own annotation perspectives, then contribute back through pull requests, enabling the community to cultivate shared understanding while preserving individual viewpoints.

We begin with three flagship datasets that exemplify the platform's value:

**Natural Scenes Dataset (NSD)**: 73,000 COCO images were prepared for this dataset, with each of 8 subjects viewing approximately 10,000 distinct images (9,000 unique per subject plus 1,000 shared across all subjects) during 7T fMRI scanning. AGI hosts a single repository (github.com/annotation-garden/nsd-stimuli) containing the stimulus identifiers and accumulating annotation layers: object detection, scene categorization, emotional ratings, visual saliency maps. Each annotation type exists as a versioned directory following stimuli-BIDS specifications, with standardized events.tsv files and accompanying JSON sidecars defining the annotation schema.

**Forrest Gump (studyforrest.org)**: The 2-hour movie stimulus already boasts an impressive collection of published annotations developed over years of collaborative effort: 870 shot boundaries with location and temporal progression metadata, 2,500+ spoken sentences with speaker identification and syntactic parsing, emotion characterizations with arousal/valence ratings, semantic conflict episodes (lies, irony, sarcasm), body contact events, eye movement classifications, music soundtrack timing, and frame-wise perceptual features. AGI's role is to unify these valuable existing layers into HED-compatible formats, visualize them together for the first time, and enable the community to build additional perspectives through the same collaborative infrastructure. The repository structure accommodates both discrete events and continuous annotations, supporting the full complexity of naturalistic viewing experiences.

**HBN Movies**: The diverse movie collection from the Child Mind Institute (Despicable Me, The Present, Pixar shorts) presents unique challenges with varying durations and copyright considerations. The HBN-EEG dataset, comprising EEG recordings from over 3,000 participants aged 5-21 across six cognitive tasks including movie watching, serves as the foundation for the NeurIPS 2025 EEG Foundation Challenge (eeg2025.github.io)—highlighting the hunger for well-annotated naturalistic stimuli in the machine learning community. AGI handles the copyright complexities through pointer-based architecture—storing unique identifiers and timestamps while annotations reference publicly available versions.

## Technical Implementation

Each stimulus repository follows a consistent structure aligned with stimuli-BIDS:
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

Version control through Git enables sophisticated collaboration patterns. Researchers propose new annotations via pull requests, with automated HED validation ensuring compatibility. GitHub Issues become discussion threads for annotation decisions—"Should character emotion be annotated continuously or at scene changes?"—creating transparent documentation of annotation philosophy. The GitHub API powers a modern web frontend at annotation.garden, where researchers can:

- **Visualize annotation layers**: See different branches (perspectives) overlaid on stimuli, understanding how scene boundaries, emotional arcs, and object detection align or diverge
- **Connect to brain dynamics**: Link annotations with neuroimaging data to explore how stimulus features map to neural responses across time
- **Compare across dimensions**: Analyze how annotations relate to brain activity across different modalities (fMRI, EEG, MEG), populations (adults, children, clinical groups), tasks, and environmental contexts

This integrated visualization transforms AGI from a data repository into an analysis platform, enabling discoveries that span the boundary between stimulus, annotation, and neural response.

Multi-agent AI assistants accelerate annotation through automated tools: Whisper for dialogue transcription, CLIP for scene description, emotion detection models for affective ratings. These computational annotations serve as initial drafts, refined through community review. Quality metrics track inter-annotator agreement, annotation completeness, and usage statistics, incentivizing high-quality contributions through transparent impact metrics.

## Integration with Existing Infrastructure

AGI synthesizes rather than replaces existing tools. HED provides the semantic framework for annotations, ensuring machine-readable, hierarchical event descriptions. The Stim-BIDS specification (BEP044), currently in final review for BIDS version 1.11.0, standardizes how annotations integrate with neuroimaging datasets. OpenNeuro datasets can reference AGI annotations through unique identifiers, enabling researchers to combine neural data with rich stimulus descriptions without duplication.

The platform bridges tool-specific formats through import pipelines: ELAN projects convert to BIDS events, Praat TextGrids map to continuous annotations, existing lab-specific formats transform into standardized structures. Export functionality reverses this process, ensuring researchers can work with familiar tools while contributing to the commons.

## Enabling New Science: Cross-Modal Comparative Analysis

AGI's collaborative annotation infrastructure enables previously infeasible cross-modal comparative analyses. By standardizing how annotations describe stimulus features, researchers can compare brain responses across multiple dimensions:

- **Across modalities**: How do fMRI, EEG, and MEG responses to the same scene boundary differ in timing and localization?
- **Across populations**: Do children and adults show different neural signatures for emotional peaks in the same movie?
- **Across tasks**: How does directed attention vs. passive viewing change neural encoding of annotated features?
- **Across environments**: Do lab-based and naturalistic viewing conditions produce different brain-behavior relationships?

Cross-dataset mega-analyses can align neural responses using shared stimulus features rather than experimental conditions. The NSD's scene categories can be mapped onto specific frames in Forrest Gump, enabling researchers to identify category-selective responses across static and dynamic viewing. HBN's developmental trajectories can be analyzed through the lens of increasing sensitivity to narrative complexity across age groups.

Machine learning approaches benefit from dense, multi-perspective annotations. The HBN-EEG dataset's role in powering the NeurIPS 2025 EEG Foundation Challenge (eeg2025.github.io) demonstrates the appetite for richly annotated naturalistic neuroimaging data. The competition's success hinges on annotation quality—teams need detailed stimulus descriptors to build meaningful brain-behavior models. AGI amplifies this impact by enabling the community to collaboratively refine annotations, ensuring that future competitions and research can build on increasingly sophisticated stimulus characterizations. Rather than training encoding models on single annotation types, researchers can explore how different annotation layers explain unique variance in neural responses. The platform's version control enables reproducible science—papers can cite specific annotation versions, ensuring analyses remain reproducible even as annotations improve.

## Implementation Roadmap

**Phase 1 (Months 1-3)**: Launch with NSD static image annotations, establishing core infrastructure and validation pipelines. The existing dashboard (neuromechanist.github.io/image-annotation) provides the initial interface, expanded with version control integration.

**Phase 2 (Months 4-6)**: Integrate Forrest Gump temporal annotations, developing continuous annotation tools and playback synchronization. Establish working groups for annotation standards in each modality.

**Phase 3 (Months 7-12)**: Expand to HBN movies and beyond, implementing federation protocols for distributed hosting of copyright-protected stimuli. Launch annotation challenges to incentivize community contributions.

## Conclusion

The Annotation Garden Initiative transforms stimulus annotation from a preparatory step into a scientific contribution. By providing infrastructure for collaborative, versioned, validated annotations, AGI enables the neuroscience community to build cumulative knowledge about how brains process complex, naturalistic stimuli. The success of the HBN-EEG dataset in driving the NeurIPS 2025 EEG Foundation Challenge (eeg2025.github.io) demonstrates the transformative potential when neuroscience data meets machine learning—and crucially, how high-quality annotations catalyze this interdisciplinary collaboration. AGI amplifies this impact by ensuring every dataset can achieve similar annotation richness through community contribution. As researchers cultivate this garden together, we grow not just annotations but understanding—each contribution enriching the soil from which future discoveries emerge.

## References

Alexander, L. M., et al. (2017). An open resource for transdiagnostic research in pediatric mental health and learning disorders. Scientific Data, 4, 170181.

Allen, E. J., et al. (2021). A massive 7T fMRI dataset to bridge cognitive neuroscience and artificial intelligence. Nature Neuroscience, 25(1), 116-126. https://doi.org/10.1038/s41593-021-00962-x

EEG 2025 Foundation Challenge. (2025). From Cross-Task to Cross-Subject EEG Decoding. NeurIPS 2025 Competition Track. https://eeg2025.github.io

Hanke, M., et al. (2014). A high-resolution 7-Tesla fMRI dataset from complex natural stimulation with an audio movie. Scientific Data, 1, 140003.

Shirazi, S. Y., et al. (2024). HBN-EEG: The FAIR implementation of the Healthy Brain Network electroencephalography dataset. bioRxiv. https://doi.org/10.1101/2024.10.03.615261
