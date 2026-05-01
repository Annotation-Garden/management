---
slug: studyforrest-eyegaze
type: dataset
strand: data
year: 2016
authors: [Hanke, Adelhöfer, Kottke, Iacovella, Sengupta, Kaule, Nigbur, Waite, Baumgartner, Stadler]
venue: Scientific Data
doi: 10.1038/sdata.2016.92
url: https://studyforrest.org/data.html
license: CC0 / PDDL (data); paper CC-BY
modalities: [fmri-7t, eyetrack, behavior]
tags: [naturalistic-video, forrest-gump, eye-tracking, simultaneous-fmri-eyegaze, adults, n=15]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

A studyforrest extension providing simultaneous 7T functional Magnetic Resonance Imaging (fMRI) and high-speed eye tracking during 2-hour audiovisual viewing of Forrest Gump, plus a comparison sample with eye tracking outside the scanner.

## Summary

This Scientific Data extension adds an eye-tracking layer to the studyforrest paradigm. 15 subjects watched the audiovisual feature film Forrest Gump in a 7T scanner with simultaneous EyeLink 1000 eye tracking at 1000 Hz. A separate cohort of 15 subjects performed the same viewing outside the scanner with eye tracking. The release adds gaze position, saccade events, fixation events, and pupil size as additional naturalistic-stimulus annotation layers. It is the canonical example of "annotation by behavior": gaze position is itself a continuous attentional annotation that co-evolves with the stimulus. The dataset has supported studies of inter-subject gaze synchronization, saliency-driven encoding models, and pupil-coupled arousal dynamics.

## Relevance to Annotation Garden Initiative (AGI)

Eye-gaze is one of the highest-value annotation layers AGI can host: it is participant-derived, time-locked to frames, and immediately comparable across subjects. AGI's pointer-architecture for copyright-protected stimuli (where stimulus media stays with rights holders) is naturally enabled by gaze annotations because they are scene-relative coordinates rather than image content. The studyforrest-eyegaze release is the proof of concept.

## Notable details

- 15 subjects audiovisual 7T fMRI + eye tracking; 15 subjects behavior-only.
- EyeLink 1000 1000 Hz eye tracking; gaze in display coordinates.
- 8 movie segments (mean roughly 15 minutes each).
- Brain Imaging Data Structure (BIDS)-compatible release; hosted via DataLad.
- License: data public-domain dedication / Open Data Commons (PDDL); paper CC-BY.

## Open questions / limitations

- Gaze data only meaningful relative to the displayed movie frame; without the movie, gaze is unanchored.
- Movie is copyright; redistribution of stimuli prohibited.

## Citations

- Primary: `Hanke2016AS`.
- Related: studyforrest base (Hanke 2014); Naturalistic Neuroimaging Database (Aliko 2020).
