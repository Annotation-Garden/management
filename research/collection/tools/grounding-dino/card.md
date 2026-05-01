---
slug: grounding-dino
type: tool
strand: tools
year: 2024
authors: [Liu, Zeng, Ren, Li, Zhang, Yang, Li, Yang, Su, Zhu, Zhang]
venue: ECCV 2024
doi: 10.48550/arXiv.2303.05499
url: https://arxiv.org/abs/2303.05499
license: Apache-2.0
modalities: [image, text]
tags: [object-detection, open-set, vision-language, DINO, grounding, REC, zero-shot]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Grounding DINO marries the DEtection TRansformer (DINO) with grounded language pre-training to detect arbitrary objects specified by natural-language prompts, achieving 52.5 Average Precision (AP) on Common Objects in Context (COCO) zero-shot.

## Summary

The authors observe that classical detectors are hard to retrofit with language because their feature pipelines are not transformer-native. They take DINO, a transformer detector, and inject language at three stages: a feature enhancer that runs cross-attention between vision and text tokens in the neck, a language-guided query selection module that initializes detection queries from text-relevant regions, and a cross-modality decoder for the head. They pre-train on a mixture of detection, grounding, and caption data and evaluate on COCO, LVIS, ODinW, and RefCOCO/+/g. Grounding DINO achieves 52.5 AP zero-shot on COCO and a record 26.1 mean AP on ODinW. Code and checkpoints are released under Apache 2.0 at github.com/IDEA-Research/GroundingDINO.

## Relevance to AGI

For AGI's static-image stimulus repositories (Natural Scenes Dataset, COCO derivatives, Pixar still frames), Grounding DINO is the natural way to convert HED-style category prompts into spatial bounding boxes without training. Combined with Segment Anything Model (SAM), it produces a HED-tag-to-mask pipeline that AGI can run as a batch annotator and store as JSON sidecars next to the stimulus. The open-set capability matches the open-vocabulary nature of HED itself: any tag in the schema can be queried as a phrase.

## Notable details

- Three-phase fusion: neck feature enhancer, language-guided query selection, cross-modality decoder.
- Sub-sentence text feature trick reduces cross-category attention contamination.
- Trained on Objects365, GoldG, and Cap4M for grounding; evaluated zero-shot on COCO, LVIS.
- 52.5 AP on COCO zero-shot; 26.1 mean AP on Objects in the Wild (ODinW).
- Powers downstream tools like Grounded-SAM, Autodistill, and many automated labeling pipelines.

## Open questions / limitations

- Inference is slow relative to closed-set detectors; batch-throughput cost is real for large stimulus sets.
- Failure modes on small or rare object categories not represented in training data.
- Grounding accuracy degrades for compositional referring expressions ("the small red ball next to the blue cup").
- License of the training datasets (especially scraped caption data) is not fully clarified.
- No native temporal extension; video annotation requires per-frame application plus tracking.

## Citations

Primary: `liu2024groundingdino`. Related:
- `radford2021clip` — language-vision backbone many open-set detectors build on.
- `zhang2024llavavideo` — video-language alternative for high-level descriptions.
- `mcnamara2017pliers` — orchestration tool that wraps detectors.
- `labelstudio2020` — manual review interface for detector output.
- `qin2025crowdagent` — multi-agent system that could route detector outputs to human review.
