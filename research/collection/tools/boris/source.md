# BORIS: Behavioral Observation Research Interactive Software

Source snapshot: https://www.boris.unito.it/ and Friard & Gamba (2016) Methods in Ecology and Evolution 7(11): 1325-1330.

BORIS is a free, open-source desktop application for video and audio coding of behavioral observations, originally aimed at ethological and animal-behavior research and now widely used in human behavior labs, child development studies, infant research, and any project requiring time-aligned event coding from media files.

Key features:

- Multi-coder, multi-subject, multi-event coding of any number of synchronized video or audio files.
- State events (with start and stop) and point events (instantaneous).
- Configurable ethogram with categories, modifiers, and exclusion rules.
- Time budget analysis, transition matrices, inter-rater reliability statistics (Cohen's kappa, intraclass correlation coefficient).
- Export to CSV, TSV, XLSX, JWatcher, ELAN EAF, and a custom JSON-based BORIS project file.
- Live observation mode through webcam or microphone for real-time coding.

Cross-platform binary releases for Windows, macOS, and Linux. Distributed under the GPL-3.0 license. The reference paper:

Friard, O., & Gamba, M. (2016). BORIS: a free, versatile open-source event-logging software for video/audio coding and live observations. Methods in Ecology and Evolution, 7(11), 1325-1330. DOI: 10.1111/2041-210X.12584.

Project home and documentation:

- Web: https://www.boris.unito.it/
- Code: https://github.com/olivierfriard/BORIS

Common workflow:

1. Define an ethogram (set of behaviors with categories, modifiers, exclusions).
2. Load one or more media files; align if more than one camera angle.
3. Code events live or offline by pressing keyboard shortcuts mapped to behaviors.
4. Analyze: time budgets, transitions, reliability between coders.
5. Export to CSV / TSV / EAF for downstream analysis or for ingestion into BIDS events.tsv.
