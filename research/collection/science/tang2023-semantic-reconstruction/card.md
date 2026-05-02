---
slug: tang2023-semantic-reconstruction
type: paper
strand: science
year: 2023
authors: [Tang, LeBel, Jain, Huth]
venue: Nature Neuroscience
doi: 10.1038/s41593-023-01304-9
url: https://www.nature.com/articles/s41593-023-01304-9
license: preprint-cc
modalities: [fmri]
tags: [decoding, language-decoder, gpt, llm, naturalistic-speech, semantic, theme-2]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Non-invasive semantic decoder that reconstructs continuous language from fMRI BOLD responses while subjects listen to or imagine narratives, using an encoding model with GPT-derived contextual embeddings plus a beam-search language-model prior.

## Summary

Tang and colleagues build a semantic decoder by training voxel-wise encoding models on hours of narrative-listening fMRI data with features from a GPT contextual language model. Decoding inverts the encoder via a beam-search procedure that uses the language model as a prior to generate plausible continuations. The decoder reconstructs perceived speech, imagined speech, and even silent video narratives at well-above-chance semantic similarity (BLEU, BERTScore). It generalizes across modalities (audio → silent video) and survives covert speech, implying the system reads conceptual content rather than just sensory features. Subject-specific models are required (no shared decoder), and adversarial counter-measures (deliberately distracting the listener) defeat decoding, which the authors highlight as an ethical safeguard.

## Relevance to AGI

This paper closes the loop on annotation-driven analysis: encoding models trained on naturalistic narrative stimuli can be inverted to read intent. AGI's commons feeds this loop in two ways: (i) shared narrative stimuli with versioned HED-tagged transcripts let many labs replicate and compare decoders; (ii) foundation-model-derived embeddings (Strand A tools; Whisper, GPT, CLIP) become standardized annotation layers that decoders can be conditioned on. The paper also demonstrates the importance of multi-modal annotation (the same decoder works for audio, imagination, and silent video); exactly the cross-modal generalization AGI targets.

## Notable details

- 3 subjects, ~16 hours each of narrative-listening fMRI training data
- Features: GPT-1 contextual embeddings (768-d) per word
- Beam search with the same GPT as language-model prior to disambiguate noisy fMRI predictions
- Validation: BLEU, BERTScore, BERTSimilarity on held-out narratives
- Generalizes to: imagined speech, silent video stories
- Cross-subject generalization fails (decoders are subject-specific)
- Adversarial defense: subjects can defeat the decoder by mental distraction

## Open questions / limitations

- Subject-specific only; population-level decoders or transferable adapters not yet demonstrated.
- 16 hours per subject is operationally infeasible for clinical translation; data-efficient variants (perhaps via foundation-model pretraining) untested.
- Pre-LLM-instruct GPT (small parameter count); whether modern LLM features improve or saturate is open.
- No HED tagging of stimulus; semantic structure is captured implicitly by GPT, which raises a question for AGI: would explicit HED-grounded annotation augment LLM features?
- Imagination and silent video work, but the **upper bound** of what mental content is decodable is not characterized; Theme 6 sufficiency questions.
- Doesn't address whether the same decoder works in healthy populations vs clinical (e.g., aphasia, locked-in).
- Whole-brain features used; selective lesion or distraction studies could clarify which networks are necessary.
- Privacy/ethics framework outlined informally; AGI commons distribution will need a formal opt-in/withdrawal mechanism.

## Citations

Primary BibTeX key: `tang2023semantic`

Related works:
- Huth et al. 2016; semantic encoding maps that this decoder inverts
- LeBel et al. 2022; natural-language fMRI dataset feeding this work
- Antonello et al. 2023; scaling laws for the encoders Tang uses
- de Heer et al. 2017; variance partitioning over hierarchical speech features
- Pereira et al. 2018; earlier word-decoding from fMRI
