---
slug: hed-spec
type: standard
strand: tools
year: 2021
authors: [Robbins, Truong, Appelhoff, Delorme, Makeig]
venue: NeuroImage
doi: 10.1016/j.neuroimage.2021.118766
url: https://www.hedtags.org
license: CC-BY-4.0 (schema); BSD/MIT (tools)
modalities: [eeg, ieeg, meg, fmri, behavior, eyetrack]
tags: [HED, schema, hierarchical, annotation, BIDS, vocabulary, library-schema, ontology]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

Hierarchical Event Descriptors (HED) is a community-maintained framework for annotating events in time-series neuroscience data with formally defined, hierarchically organized tags drawn from a published schema and validated by HED-Python and HED-JS tools.

## Summary

HED defines a controlled vocabulary in which each tag is a path through a hierarchy (for example, `Event/Sensory-event/Visual-presentation/Symbolic`). Events are annotated with comma-separated HED strings stored in tabular events files; library schemas extend the standard schema for domain-specific needs (HED-SCORE for clinical Electroencephalography (EEG), prospective HED-LANG and HED-MOVIE libraries). HED is integrated into the Brain Imaging Data Structure (BIDS) via events.json sidecars and validated by HED-Python, HED-JS, and the EEGLAB HEDTools plugin. The 2021 NeuroImage paper formalizes HED 3.0, the version that introduced the library-schema mechanism and the strict node-attribute model.

## Relevance to AGI

HED is the semantic layer that makes AGI annotations interoperable across labs and tools. Without a controlled vocabulary, every lab invents its own column names and category labels; HED gives AGI a path-like tag structure that downstream tools (NEMAR search, EEGLAB plugins, MNE-Python decoders, Neuroscout regressors) can consume directly. AGI's per-stimulus annotation files store HED tags in events.json, the AGI image-annotation tool emits HED tags as primary output, and AGI's review process should require that any new annotation type have a HED-mapped vocabulary.

## Notable details

- Standard schema versioned at hedtags.org; semantic versioning.
- Library schema mechanism for domain-specific extensions (HED-SCORE first published example).
- Validators: HED-Python (Python), HED-JS (Node.js / browser), HEDTools (EEGLAB).
- Integrated into BIDS-Validator via plugin.
- Tag relationships: parent-child hierarchy, attributes, units, value placeholders.

## Open questions / limitations

- Coverage of cinematic / social / developmental vocabularies is incomplete; library schemas needed.
- Tooling for non-EEGLAB users (pure Python, browser-based annotators) lags.
- Inter-rater agreement on HED tags is rarely measured systematically.
- Schema evolution sometimes breaks downstream parsers; version pinning is mandatory.
- No automatic mapping between free-text descriptions and HED tags yet.

## Citations

Primary: `robbins2021hed`. Related:
- `hermes2023hedscore`, first HED library schema example.
- `gorgolewski2016bids`, host data structure.
- `delorme2004eeglab`, primary tool with HED integration.
- `delorme2022nemar`, archive that uses HED for search.
- `wilkinson2016fair`, interoperability principle that HED operationalizes.
