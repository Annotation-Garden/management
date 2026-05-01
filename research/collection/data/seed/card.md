---
slug: seed
type: dataset
strand: data
year: 2015
authors: [Zheng, Lu]
venue: IEEE Transactions on Autonomous Mental Development
doi: 10.1109/TAMD.2015.2431497
url: https://bcmi.sjtu.edu.cn/home/seed/
license: data-use-agreement (Shanghai Jiao Tong University BCMI Lab)
modalities: [eeg, eyetrack, video, behavior]
tags: [hybrid, emotion-elicitation, film-clips, three-emotion-classes, n=15, adults, brain-computer-interface]
agi_relevance: low
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

The Shanghai Jiao Tong University Emotion EEG Dataset (SEED): 15 adults watching 15 emotional film clips (positive / neutral / negative) across three sessions while 62-channel scalp electroencephalography (EEG) is recorded; a frequent benchmark for emotion-classification brain-computer interface (BCI) studies.

## Summary

Zheng & Lu (Shanghai Jiao Tong University Brain-Computer Interface and Machine Intelligence Lab) released SEED in 2015 as an emotion-classification benchmark. 15 healthy adults watched 15 Chinese film clips (5 positive, 5 neutral, 5 negative) lasting roughly 4 minutes each, with three independent recording sessions per subject. 62-channel scalp EEG (using a 64-channel actiCAP, 1000 Hz sampling) was recorded throughout. Subsequent extensions (SEED-IV, SEED-VIG, SEED-V) cover additional emotion classes, drowsiness states, and multi-modal extensions. SEED has anchored hundreds of emotion-classification methodology papers.

## Relevance to Annotation Garden Initiative (AGI)

SEED is a pure stimulus-elicitation hybrid: short film clips selected for affective content, paired with high-density EEG. The film clips themselves are copyright; AGI's pointer architecture is a clean fit. Garden contribution opportunities: clip-level affect annotations beyond positive/neutral/negative (e.g., continuous valence/arousal), audio-feature extractions, scene-shot boundaries.

## Notable details

- N = 15 adults (Chinese university students).
- 15 film clips per session, 3 sessions per subject (with 1-week interval).
- Clips: roughly 4 minutes each, balanced positive / neutral / negative.
- 62-channel actiCAP EEG, 1000 Hz sampling.
- SEED extensions:
  - SEED-IV: 4 emotion classes, eye tracking added.
  - SEED-VIG: drowsiness states.
  - SEED-V: 5 emotion classes, peripheral physiology.
- License: DUA via SJTU BCMI Lab.

## Open questions / limitations

- Mandarin Chinese stimuli; cross-cultural generalization untested.
- Clips are copyright; redistribution prohibited.
- Adults only.

## Citations

- Primary: `Zheng2015InvestigatingCF`.
- Related: DEAP (`deap/`); SEED-IV; MAHNOB-HCI.
