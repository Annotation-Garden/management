---
slug: hed-score
type: standard
strand: tools
year: 2025
authors: [Hermes, "Pal Attia", Beniczky, "Bosch-Bayard", Delorme, Lundstrom, Rogers, Rampp, Shirazi, Truong, "Valdés-Sosa", Worrell, Makeig, Robbins]
venue: Scientific Data (HED-SCORE library schema, arXiv:2310.15173)
doi: 10.48550/arXiv.2310.15173
url: https://arxiv.org/abs/2310.15173
license: CC-BY-4.0
modalities: [eeg, ieeg]
tags: [HED, SCORE, EEG, clinical, schema, library, ILAE, IFCN, BIDS]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

HED-SCORE is a Hierarchical Event Descriptors (HED) library schema that encodes the Standardized Computer-based Organized Reporting of Electroencephalography (SCORE) clinical vocabulary in a machine-readable form, letting EEG events be annotated with International League Against Epilepsy (ILAE) and International Federation of Clinical Neurophysiology (IFCN)-endorsed terms.

## Summary

The authors take the SCORE consensus terminology, originally a clinical reporting guideline for EEG graphoelements, ictal patterns, and artifacts, and recast it as a HED library schema. Each SCORE term is mapped to a hierarchical HED tag with attributes and relationships that a HED validator can enforce. The paper demonstrates end-to-end use: annotating events in a Brain Imaging Data Structure (BIDS)-formatted EEG dataset with HED-SCORE tags, validating those annotations, and querying across studies using shared vocabulary. The library schema mechanism preserves backward compatibility with the standard HED schema while letting clinical EEG terminology evolve independently. HED-SCORE was accepted in Scientific Data (2025) and is distributed alongside the HED standard schema at hedtags.org.

## Relevance to AGI

AGI's mission of capturing the semantics of stimuli and responses across labs requires controlled vocabularies; HED-SCORE shows how a domain-specific community (clinical EEG) extends HED without forking it. For AGI, the exact same library-schema mechanism is the path to vocabularies for stimulus categories that the standard schema does not yet cover (cinematic shot types, social interaction labels, infant directed speech features). HED-SCORE is also the only existing example of clinical-grade EEG terminology as a HED library, and AGI's flagship NEMAR-linked datasets (HBN-EEG, NeurIPS EEG Competition) will rely on it for any annotation that touches clinical artifact or ictal-state labels.

## Notable details

- Built as a HED library schema; activates with the `sc` namespace prefix.
- Captures graphoelements, artifacts, ictal patterns, and severity attributes.
- ILAE-Europe and IFCN endorsements bring clinical legitimacy.
- Demonstrated on BIDS-EEG datasets with the Python and JavaScript HED validators.
- Co-authored by maintainers of HED, EEGLAB, BIDS-EEG, and clinical EEG consortia.

## Open questions / limitations

- Coverage is biased toward epilepsy and routine EEG; sleep, brain-computer-interface, and developmental EEG vocabularies need separate libraries.
- Mapping between HED-SCORE and existing International Classification of Diseases (ICD) or SNOMED codes is incomplete.
- Inter-rater reliability of SCORE terms in non-specialist hands is not yet quantified inside HED-SCORE.
- Tooling support outside the EEGLAB plugin is still nascent.
- The schema does not yet model uncertainty or annotator disagreement explicitly.

## Citations

Primary: `hermes2023hedscore`. Related:
- `robbins2021hed` — base HED schema and tooling.
- `gorgolewski2016bids` — host data structure where HED-SCORE annotations live.
- `delorme2004eeglab` — primary EEG analysis tool with HED integration.
- `delorme2022nemar` — archive whose EEG datasets benefit from HED-SCORE.
- `wilkinson2016fair` — interoperability rationale that HED libraries fulfill.
