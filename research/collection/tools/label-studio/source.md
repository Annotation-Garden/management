# Label Studio

Source snapshot: https://github.com/HumanSignal/label-studio (commit-pinned 2026-04-30) and https://labelstud.io.

Label Studio is a free, open-source, web-based data labeling platform created by HumanSignal (formerly Heartex). It supports a wide range of annotation types across modalities and is one of the most widely adopted general-purpose annotators in industry and academic research.

Supported annotation types:

- Text: classification, named-entity recognition, span labeling, relation extraction, summarization.
- Images: classification, bounding boxes, polygons, semantic segmentation, key points, OCR transcription.
- Audio: transcription, speaker diarization, segment classification.
- Video: temporal segmentation, frame-level classification, object tracking.
- Time series: peak detection, segment classification, anomaly labeling.
- Multimodal: arbitrary combinations through XML-defined labeling configurations.

Architecture:

- Django plus React web application.
- PostgreSQL or SQLite backend.
- Pluggable Machine Learning (ML) backend interface so model predictions can pre-fill annotations and humans correct them.
- Programmatic Software Development Kit (SDK) in Python for batch import, export, and project management.

License: Apache-2.0 for the open-source community edition. Commercial Label Studio Enterprise adds team management, single sign-on, and audit logging.

Reference:

Tkachenko, M., Malyuk, M., Holmanyuk, A., & Liubimov, N. (2020-2024). Label Studio: Data labeling software. Open source. https://github.com/HumanSignal/label-studio.

Documentation: https://labelstud.io/guide/.
