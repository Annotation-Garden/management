---
slug: naselaris2011-encoding-decoding-review
type: paper
strand: science
year: 2011
authors: [Naselaris, Kay, Nishimoto, Gallant]
venue: NeuroImage
doi: 10.1016/j.neuroimage.2010.07.073
url: https://doi.org/10.1016/j.neuroimage.2010.07.073
license: publisher-paywall
modalities: [fmri]
tags: [encoding-model, decoding, voxel-wise, review, ridge-regression, framework, theme-1]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

The canonical methodological review of voxel-wise encoding versus decoding analyses for functional Magnetic Resonance Imaging (fMRI), formalizing the four-stage pipeline (stimulus features → encoding model → decoding → predictions) that the field still uses today.

## Summary

Naselaris and colleagues review and unify the encoding-model and decoding-model paradigms in fMRI as two sides of the same statistical machinery. They argue that decoding (predicting stimulus class from BOLD activity) and encoding (predicting BOLD activity from stimulus features) are formally equivalent under different objectives and that encoding is the more powerful framework because it forces explicit, mechanistic feature-space hypotheses. The review walks through feature-space construction (Gabor banks, motion-energy, semantic categories), regularized regression (ridge, Lasso), validation on held-out stimuli, and Bayesian decoding via likelihood inversion. The paper sets methodological norms (cross-validated prediction accuracy on held-out stimuli, comparison of competing feature spaces, voxel-level granularity) that the rest of Theme 1 still follows.

## Relevance to AGI

Encoding models are only as good as their feature-space annotations. AGI's contribution is precisely to provide annotation layers (Hierarchical Event Descriptors (HED) Gen-3 sidecars, foundation-model embeddings, hand-curated semantic tags) that other labs can plug into the encoding pipeline without re-deriving them. This review's framework is the analytical engine; AGI's commons supplies the fuel (annotations) and lets the community version-control which feature space "best explains" cortical responses on shared stimuli.

## Notable details

- Cross-validated R^2 on held-out stimuli is the canonical evaluation metric
- Encoding models can be inverted into decoders via Bayesian decoding (Naselaris 2009, Nishimoto 2011)
- Nishimoto-style natural-movie reconstruction is presented as a flagship application
- Discusses the curse of dimensionality and ridge/Lasso regularization
- Pre-dates deep learning features; the framework is feature-agnostic

## Open questions / limitations

- Does not address how to compare and combine *multiple* annotation layers competing for variance (variance-partitioning came later: de Heer 2017).
- No discussion of single-trial estimation reliability; General Linear Model single-trial (GLMsingle, Prince 2022) was a decade away.
- Pre-foundation-model: doesn't anticipate that contextual embeddings (BERT, GPT, Contrastive Language-Image Pretraining (CLIP)) would dominate as feature spaces by 2023.
- Does not address cross-subject generalization or hyperalignment.
- Treats the stimulus as known and fully described; the practical bottleneck of *generating* annotations for naturalistic stimuli is out of scope (and is exactly AGI's gap).
- Does not discuss reliability ceilings (noise ceiling) for fairly comparing models.
- No formal treatment of how much data is needed to fit a useful encoding model, a question only recently approached (Antonello 2023, LeBel 2023).

## Citations

Primary BibTeX key: `naselaris2011encoding`

Related works:
- Kay et al. 2008; first natural-image identification from fMRI; foundational for encoding/decoding parity
- Naselaris et al. 2009; Bayesian image reconstruction
- Nishimoto et al. 2011; natural movie reconstruction from BOLD
- de Heer et al. 2017; variance partitioning across multiple feature spaces
- Prince et al. 2022; GLMsingle for trial-level encoding
