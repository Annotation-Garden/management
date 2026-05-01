---
slug: deap
type: dataset
strand: data
year: 2012
authors: [Koelstra, Mühl, Soleymani, Lee, Yazdani, Ebrahimi, Pun, Nijholt, Patras]
venue: IEEE Transactions on Affective Computing
doi: 10.1109/T-AFFC.2011.15
url: https://www.eecs.qmul.ac.uk/mmv/datasets/deap/
license: data-use-agreement (Queen Mary University of London)
modalities: [eeg, peripheral-physio, video, behavior]
tags: [hybrid, emotion-elicitation, music-videos, valence-arousal, n=32, adults, affective-computing]
agi_relevance: medium
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

A Database for Emotion Analysis using Physiological Signals (DEAP): 32 adults watching 40 1-minute music videos while 32-channel scalp electroencephalography (EEG), peripheral physiology, and frontal video are recorded; participants rate each video on valence, arousal, dominance, and liking.

## Summary

Koelstra and colleagues (Queen Mary University of London / EPFL) released DEAP in 2012 as a benchmark for affective computing. 32 adults each watched 40 carefully selected 1-minute music videos chosen to span a balanced range of emotional valence and arousal. During each video, 32-channel BioSemi scalp EEG, peripheral physiology (galvanic skin response, respiration, blood volume pulse, electromyography (EMG)), and frontal-face video were recorded. Participants self-rated each video on a 9-point valence / arousal / dominance / liking scale. DEAP is among the most cited datasets in affective neuroscience and brain-computer interfaces (BCI), but its mixed modalities and explicit emotion-elicitation paradigm place it on the hybrid spectrum between naturalistic video and structured task.

## Relevance to Annotation Garden Initiative (AGI)

DEAP is an exemplar dataset for AGI's hybrid category: short-form naturalistic videos (music videos) coupled with rich behavioural ratings. The 40 music videos themselves are external (YouTube IDs released, but content is copyright); annotations (per-second arousal / valence per video, music feature vectors, scene-cut times) can be hosted in AGI as pointer-architecture layers. The dataset's EEG protocol is also a useful baseline for naturalistic-EEG community comparisons.

## Notable details

- N = 32 adults.
- 40 music videos, 1 minute each (selection from 120 candidates).
- 32-channel BioSemi EEG, peripheral physiology, frontal face video.
- Ratings: valence, arousal, dominance, liking on 9-point Self-Assessment Manikin scale.
- Also released: 22 of 32 subjects with extended EEG-only viewing of additional videos (DEAP+).
- License: DUA via Queen Mary University of London.

## Open questions / limitations

- Stimuli are copyright; only YouTube IDs and timing distributed.
- No standardized BIDS deposit; access via custom DUA portal.
- Adult sample, mostly Western European.

## Citations

- Primary: `Koelstra2012DEAPAD`.
- Related: SEED (Zheng & Lu 2015, `seed/`); MAHNOB-HCI (Soleymani 2012); EmoForest (Hu 2019).
