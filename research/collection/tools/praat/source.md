# Praat: Doing Phonetics by Computer

Source snapshot: https://www.fon.hum.uva.nl/praat/ (version 6.4, retrieved 2026-04-30).

Praat is the de facto standard tool for phonetic annotation, acoustic analysis, and synthesis in the linguistic sciences. It was created by Paul Boersma and David Weenink at the University of Amsterdam and has been continuously developed since 1992.

Capabilities:

- Spectrographic display, formant tracking, pitch extraction (autocorrelation, cross-correlation, sub-harmonic).
- Time-aligned annotation via TextGrids: multiple interval and point tiers with arbitrary labels.
- Statistical pattern analysis: linear discriminant, principal component, multidimensional scaling.
- Speech synthesis: source-filter, articulatory, formant, klatt-style, neural-net-based.
- Listening experiments and runtime experiment scripting (ExperimentMFC).
- Praat scripting language for batch processing and reproducible analyses.

The TextGrid format (.TextGrid) is the dominant exchange format for phonetic annotations and is supported by ELAN, Phon, EMU, and many BIDS conversion scripts.

License: GPL-3.0 (and later). Cross-platform binaries for Windows, macOS, Linux, FreeBSD, and Solaris.

Reference (citation form for the tool):

Boersma, P., & Weenink, D. (2024). Praat: doing phonetics by computer (version 6.4). Computer program. https://www.fon.hum.uva.nl/praat/.

Common workflow:

1. Open a sound file; visualize waveform plus spectrogram plus pitch plus formants.
2. Create a TextGrid with the desired tier structure (word, phoneme, syllable, prosody).
3. Annotate boundaries and labels with mouse plus keyboard shortcuts.
4. Save TextGrid for downstream consumption (BIDS events.tsv conversion, statistical pipelines, ELAN import).
5. Optionally script the entire pipeline with Praat scripting for reproducibility.
