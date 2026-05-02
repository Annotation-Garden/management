---
slug: fedorenko-language-localizer
type: paper
strand: data
year: 2010
authors: [Fedorenko, Hsieh, Nieto-Castañón, Whitfield-Gabrieli, Kanwisher]
venue: Journal of Neurophysiology
doi: 10.1152/jn.00032.2010
url: https://evlab.mit.edu/funcloc/
license: paper publisher (American Physiological Society); stimuli openly released
modalities: [fmri, behavior]
tags: [single-stimulus-benchmark, language-localizer, sentences-vs-nonwords, individual-functional-rois, adults, n=49]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

The Fedorenko language localizer: a 5-minute functional Magnetic Resonance Imaging (fMRI) paradigm that contrasts intact sentences with phonotactically legal nonword sequences to identify language-selective regions in individual subjects, used as a canonical "single-stimulus benchmark" across hundreds of cohorts.

## Summary

Fedorenko, Hsieh, Nieto-Castañón, Whitfield-Gabrieli, Kanwisher (Massachusetts Institute of Technology / Stanford / Harvard) introduced a short, robust functional Magnetic Resonance Imaging (fMRI) localizer for language-selective cortex using a sentences vs nonword-lists block design. The 5-minute paradigm reliably activates a left-lateralized fronto-temporal language network in 95+% of typical adults, and is the canonical reference for language-selective regions of interest (ROIs). Stimulus materials, presentation scripts, and analysis code are openly released by the EvLab. The paradigm has been applied across thousands of subjects and is the de facto cross-cohort comparator for language-network research.

## Relevance to Annotation Garden Initiative (AGI)

The Fedorenko localizer is the textbook "single-stimulus benchmark" entry: a stable, well-annotated, openly distributed paradigm used to anchor cohort-level analyses. Garden contribution opportunities: standardized HED-Lang sidecar JSON, multilingual variants (currently English, Spanish, Mandarin community translations exist), and cross-walks from the localizer ROIs to naturalistic-language datasets like Narratives or Moth Radio Hour.

## Notable details

- 5-minute task; 12 blocks (6 sentences, 6 nonword lists) of 18 seconds each.
- 12 sentences per block, 8 words each; 12 nonword sequences per block, 8 nonwords each.
- Visual presentation (rapid serial visual presentation, RSVP, 350 ms per word).
- Materials and analysis code openly distributed at evlab.mit.edu/funcloc.
- License: paper publisher; stimuli openly released.

## Open questions / limitations

- Original validation cohort small (N = 49); replications in larger samples.
- Visual RSVP presentation; auditory variants exist but are less standardized.

## Citations

- Primary: `Fedorenko2010NewMF`.
- Related: HCP Language task (`hcp-task/`); Pinel localizer (Pinel 2007, `pinel-localizer/`); Narratives (`narratives-pieman/`).
