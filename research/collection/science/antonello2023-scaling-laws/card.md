---
slug: antonello2023-scaling-laws
type: paper
strand: science
year: 2023
authors: [Antonello, Vaidya, Huth]
venue: NeurIPS / arXiv
doi: 10.48550/arXiv.2305.11863
url: https://arxiv.org/abs/2305.11863
license: arXiv preprint
modalities: [fmri]
tags: [encoding-model, scaling-laws, language-model, sufficiency, naturalistic-language, theme-6]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

First systematic scaling-law study for language-encoding models in fMRI: encoding accuracy scales **log-linearly** with both training-data size and language-model parameter count over more than two orders of magnitude, with no clear saturation in current data regimes.

## Summary

Antonello and colleagues fit voxel-wise encoding models that predict BOLD activity from large-language-model (LLM) embeddings on the LeBel dataset. They sweep two axes: (i) the number of training stories (1–80, totaling tens of hours per subject) and (ii) the size of the language model (from 125M to 7B parameters). Encoding accuracy on held-out stories scales smoothly and log-linearly along both axes; a clear "scaling law" analogous to LLM perplexity scaling. The finding is that *more data* and *bigger models* keep yielding gains, with no asymptote in the explored regime. The paper is the first concrete answer to "how much annotation/data is enough?" for naturalistic language fMRI.

## Relevance to AGI

This is the canonical Theme 6 paper for the AGI commons. It shows that **scaling annotated stimuli is still paying off** for naturalistic fMRI encoding, which justifies the considerable investment AGI proposes to standardize and grow shared annotated stimulus corpora. The complementary scaling axis; annotation **richness** rather than **quantity**; is the natural extension AGI can pursue: do multilayer HED-annotated stimuli give the same scaling improvement as more data?

## Notable details

- Dataset: LeBel et al. 2023 natural-language fMRI (3 subjects, ~16 h each)
- Model sizes: 125M (GPT-2) to 7B (LLaMA, OPT)
- Data axis: 1 to 80 training stories
- Linear-encoding model with ridge regression
- Both axes scale log-linearly; no asymptote yet
- Layer selection within each LLM matters; mid-network layers dominate

## Open questions / limitations

- Fewer than 5 subjects; subject-level idiosyncratic ceilings are not characterized.
- Single language (English narrative); non-narrative or multilingual scaling unknown.
- Doesn't dissociate data quantity from annotation richness; what extra dimensions of annotation might help.
- Ridge regression as the encoder; non-linear encoders might shift the curves.
- Cortex-wide aggregate scaling; region-specific scaling laws (where do default-mode regions saturate first?) is open.
- Doesn't test whether HED-grounded explicit annotations augment LLM embeddings.
- Cross-modality scaling (does the same scaling appear in MEG or EEG with the same stimuli?) is open.
- Compute cost is large; AGI's commons could provide pre-computed embeddings to allow community replication without 7B-model inference.

## Citations

Primary BibTeX key: `antonello2023scaling`

Related works:
- LeBel et al. 2023; dataset used
- Huth et al. 2016; semantic-encoding foundational paper
- Tang & Huth 2023; semantic decoder built on these encoders
- Schrimpf et al. 2021; analogous behavior-prediction scaling for language
- Goldstein et al. 2022; LLM-brain alignment in narratives
