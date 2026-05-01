# Pliers: A Comprehensive Framework for Multimodal Feature Extraction

Source snapshot: McNamara Q., de la Vega A., Yarkoni T. (2017). Developing a Comprehensive Framework for Multimodal Feature Extraction. In Proceedings of the 23rd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining (KDD '17), 1567-1574. DOI: 10.1145/3097983.3098075. Code at https://github.com/PsychoinformaticsLab/pliers.

Pliers is a Python framework that wraps disparate feature extraction tools behind a unified Application Programming Interface (API), letting researchers compose multi-stage pipelines that take heterogeneous stimulus inputs (image, audio, video, text) and emit time-aligned feature columns. The framework is the multimodal-annotation backbone of Neuroscout and is used in many naturalistic-fMRI studies.

Architecture:

- Stim hierarchy: ImageStim, AudioStim, VideoStim, TextStim, ComplexTextStim, with Iterators for breaking media into frames or segments.
- Extractor hierarchy: low-level ImageExtractor, AudioExtractor, etc., with concrete subclasses wrapping individual tools (Google Vision, Microsoft Cognitive Services, IBM Watson, OpenCV, FaceRecognition, librosa, NLTK, spaCy, TensorFlow, PyTorch).
- Filter / Converter mechanisms allow pipelines like "VideoStim -> FrameSamplingFilter -> ImageStim -> CLIPExtractor -> ExtractorResult."
- ExtractorResult objects contain a pandas DataFrame of features over time, ready for ingestion into a General Linear Model (GLM) or any downstream analysis.

Cloud-based extractor wrappers historically required API keys (Google Vision, Microsoft Cognitive); a growing collection of local extractors (OpenCV, librosa, transformers via Hugging Face) avoid that dependency. Pliers also handles caching of extractor outputs so re-running a pipeline is fast.

License: BSD-3-Clause.

The reference paper:

McNamara, Q., de la Vega, A., & Yarkoni, T. (2017). Developing a Comprehensive Framework for Multimodal Feature Extraction. KDD '17, 1567-1574. DOI: 10.1145/3097983.3098075.
