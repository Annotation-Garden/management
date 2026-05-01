---
slug: natural-sounds-fmri
type: dataset
strand: data
year: 2015
authors: [Norman-Haignere, Kanwisher, McDermott]
venue: Neuron
doi: 10.1016/j.neuron.2015.11.035
url: https://github.com/snormanhaignere/natural-sound-encoding-2015
license: paper publisher (Cell Press); data CC-BY (deposit)
modalities: [fmri-3t, audio-stimulus, behavior]
tags: [naturalistic-audio, environmental-sounds, music, speech, auditory-cortex, adults, n=20+]
agi_relevance: low
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

3 Tesla functional Magnetic Resonance Imaging (fMRI) of more than 20 adults listening to a 165-sound naturalistic auditory benchmark spanning music, speech, environmental sounds, and animal vocalizations, used to discover music- and speech-selective auditory cortical regions.

## Summary

Norman-Haignere, Kanwisher, McDermott (Massachusetts Institute of Technology) collected 3T fMRI from more than 20 adults listening to a curated set of 165 two-second natural sound clips covering music, speech, mechanical sounds, animal vocalizations, and environmental scenes. Using non-negative matrix factorization on voxel response patterns, the authors discovered that human auditory cortex contains regions selective for music and speech beyond what can be explained by acoustic features alone. The stimulus set has become a community benchmark for auditory-cortex encoding studies.

## Relevance to Annotation Garden Initiative (AGI)

This is the canonical "natural sounds" stimulus set. The 165 clips have rich acoustic feature annotations (modulation power spectra, spectro-temporal modulation features); category labels are present but coarse. AGI Garden contribution opportunities include hierarchical semantic tags, source-of-sound (musical instrument identification, speech-language tags), and emotional valence/arousal ratings.

## Notable details

- N = 20+ adults per cohort (multiple cohorts for replication).
- 165 sound clips, each 2 seconds.
- Categories: music, speech (English), mechanical, environmental, animal, etc.
- 3 Tesla Siemens; 2-second TR.
- Stimulus set distributed openly via the McDermott / Norman-Haignere lab GitHub.
- Companion analyses on intracranial EEG and electrocorticography (ECoG).

## Open questions / limitations

- Western-music-centric stimulus selection.
- 2-second clips remove temporal context; not a "long-form" naturalistic stimulus.
- Paper paywalled.

## Citations

- Primary: `NormanHaignere2015DistinctCM`.
- Related: NaturalSounds2 stimulus set (subsequent extensions); SoundNet (Aytar 2016); HEAR audio benchmark (Turian 2022).
