# HED: Hierarchical Event Descriptors

Source snapshot: Robbins K. et al. (2021). Capturing the nature of events and event context using hierarchical event descriptors (HED). NeuroImage 245: 118766. DOI: 10.1016/j.neuroimage.2021.118766. Project home at https://www.hedtags.org and code at https://github.com/hed-standard.

Hierarchical Event Descriptors (HED) is a community-developed framework for annotating events in time series neuroscience data with formally defined, hierarchically organized terms. HED tags are comma-separated strings drawn from a published schema; each tag references a node in a hierarchy (for example, `Event/Sensory-event/Visual-presentation/Symbolic`).

Key components of the HED ecosystem:

- HED standard schema (XML / Markdown), versioned and published at hedtags.org.
- HED library schemas extending the standard schema for domain-specific vocabularies (HED-SCORE for clinical EEG, HED-LANG for linguistics, HED-MOVIE for cinematic stimuli).
- HED-Python validator (https://github.com/hed-standard/hed-python).
- HED-JS validator (https://github.com/hed-standard/hed-javascript).
- HEDTools EEGLAB plugin and direct integration with the BIDS-Validator.
- Schema browser and tagging assistant at https://www.hedtags.org/display_hed.html.

HED is integrated into the Brain Imaging Data Structure (BIDS) specification: events.json sidecars can declare a `HED` column whose values are HED tag strings, and the BIDS-Validator can be configured to invoke HED validation. HED tags are increasingly used as a discovery facet (NEMAR), as input to encoding-model regressors, and as the bridge between manual annotation tools and automated extractors.

License: standard schema and library schemas are CC-BY 4.0; tooling is BSD or MIT.

The reference paper:

Robbins, K. A., Truong, D., Appelhoff, S., Delorme, A., & Makeig, S. (2021). Capturing the nature of events and event context using hierarchical event descriptors (HED). NeuroImage, 245, 118766. DOI: 10.1016/j.neuroimage.2021.118766.
