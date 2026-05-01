# Natural speech reveals the semantic maps that tile human cerebral cortex

**Authors:** Alexander G. Huth, Wendy A. de Heer, Thomas L. Griffiths, Frédéric E. Theunissen, Jack L. Gallant

**Journal:** Nature, 532, 453–458 (2016)

**DOI:** 10.1038/nature17637

**PMCID:** PMC4852309

> Note: The publisher-formatted PDF is paywalled and not redistributable. This file
> contains the published abstract and key extracted facts; the underlying paper text
> is freely accessible at PMC4852309 for individual reading via NIH/Europe PMC.

## Abstract

The meaning of language is represented in regions of the cerebral cortex collectively known as the "semantic system". Previous studies have identified hundreds of discrete brain areas that selectively respond to specific semantic categories such as faces or places. However, these studies typically used controlled stimuli that probed only a few categories, leaving a comprehensive map of the semantic system unresolved. Here we systematically map semantic selectivity across the cortex using voxel-wise modelling of functional Magnetic Resonance Imaging (fMRI) data collected while subjects listened to hours of narrative stories. We show that the semantic system is organized into intricate patterns that seem to be consistent across individuals. We then use a novel generative model to create a detailed semantic atlas. Our results suggest that most areas within the semantic system represent information about specific semantic domains, or groups of related concepts, and our atlas shows which domains are represented in each area. This study demonstrates that data-driven methods, combined with naturalistic stimuli, offer a powerful approach for mapping functional representations in the brain.

## Key facts (extracted)

- **Subjects:** 7 healthy adults (3 women), 3 T fMRI
- **Stimuli:** narrative stories from "The Moth Radio Hour" totaling roughly two hours per subject, presented as audio
- **Feature space:** 985-dimensional word co-occurrence embedding derived from a ~10.4-billion-word corpus
- **Model:** voxel-wise ridge regression mapping word features (convolved with hemodynamic response) to BOLD response
- **Held-out validation:** prediction accuracy on a separate story; ~30% of cortex predicted significantly
- **Atlas construction:** four-component PCA across voxel weights yields a coordinate system shared across subjects; projected onto inflated and flattened cortical surfaces
- **Companion resource:** interactive viewer at gallantlab.org/huth2016
- **Coverage:** bilateral, includes lateral temporal, ventral temporal, lateral parietal, medial parietal, prefrontal regions

## Citation

Huth, A. G., de Heer, W. A., Griffiths, T. L., Theunissen, F. E., & Gallant, J. L. (2016). Natural speech reveals the semantic maps that tile human cerebral cortex. Nature, 532(7600), 453–458. https://doi.org/10.1038/nature17637
