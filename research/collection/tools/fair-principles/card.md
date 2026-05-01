---
slug: fair-principles
type: standard
strand: tools
year: 2016
authors: [Wilkinson, Dumontier, Aalbersberg, Appleton, Axton, Baak, Blomberg, Boiten, "da Silva Santos", Bourne]
venue: Scientific Data
doi: 10.1038/sdata.2016.18
url: https://www.nature.com/articles/sdata201618
license: CC-BY-4.0
modalities: [all]
tags: [FAIR, data-stewardship, findability, accessibility, interoperability, reusability, open-science]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Findable, Accessible, Interoperable, Reusable (FAIR) Guiding Principles articulate fifteen criteria for scholarly data and metadata management aimed at supporting both human and machine reuse of digital research objects.

## Summary

The FAIR paper, the formal first publication of principles drafted at the 2014 Leiden "Jointly Designing a Data Fairport" workshop, argues that good data stewardship requires datasets, algorithms, tools, and workflows that are discoverable through globally unique persistent identifiers (Findable), retrievable via standardized open protocols including authentication when needed (Accessible), described with formal vocabularies that interoperate with shared ontologies (Interoperable), and licensed and provenance-tracked sufficiently for reuse (Reusable). Each principle has sub-clauses (F1-F4, A1-A2, I1-I3, R1) that turn the abstract goals into actionable checks. FAIR has since become the policy lingua franca for funders (National Institutes of Health (NIH), European Commission), repositories, and journals.

## Relevance to AGI

FAIR is AGI's architectural ethic. Each AGI stimulus repository must satisfy: globally unique stimulus IDs (F), open Hyper Text Transfer Protocol Secure (HTTPS) and Git access (A), HED-tagged events plus BIDS schemas for shared semantics (I), and open licenses with provenance via DataLad (R). The 2016 paper is the citation AGI's white paper, governance, and review checklist will lean on whenever a repository or annotation campaign is reviewed for compliance. FAIR also provides the rationale for layering HED on top of BIDS: human-readable annotations alone are not Interoperable until they reference a formal vocabulary.

## Notable details

- Fifteen principles grouped under four pillars: F (1-4), A (1-2 with sub-clauses), I (1-3), R (1 with sub-clauses).
- Emphasizes machine-actionability: metadata must be processable by software agents.
- Distinguishes data from metadata; metadata can stay accessible even if the data become restricted.
- Cited by NIH 2023 Data Management and Sharing policy and European Open Science Cloud.
- Enabled subsequent extensions: TRUST principles for repositories, CARE principles for Indigenous data.

## Open questions / limitations

- Principles are intentionally not standards; concrete implementations vary widely.
- "Accessible" does not require "open"; restricted data can be FAIR, which causes downstream confusion.
- No quantitative compliance metric; FAIR maturity assessments differ across organizations.
- Costs of FAIRification fall on data producers without a clear funding model.
- Sensor-level neuroscience (EEG, eye-tracking) needs additional vocabularies beyond what FAIR mandates.

## Citations

Primary: `wilkinson2016fair`. Related:
- `gorgolewski2016bids`, domain-specific operationalization of FAIR for neuroimaging.
- `markiewicz2021openneuro`, repository explicitly built on FAIR.
- `halchenko2021datalad`, FAIR-compatible distribution of code plus data.
- `rubel2022nwb`, FAIR data language for neurophysiology.
- `nichols2017cobidas`, community best-practice document layered on FAIR.
