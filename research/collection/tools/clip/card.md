---
slug: clip
type: tool
strand: tools
year: 2021
authors: [Radford, Kim, Hallacy, Ramesh, Goh, Agarwal, Sastry, Askell, Mishkin, Clark, Krueger, Sutskever]
venue: ICML 2021
doi: 10.48550/arXiv.2103.00020
url: https://arxiv.org/abs/2103.00020
license: MIT (code); custom acceptable-use (released model checkpoints)
modalities: [image, text, video]
tags: [vision-language, contrastive, zero-shot, foundation-model, embedding, OpenAI, multimodal]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Contrastive Language-Image Pre-training (CLIP) jointly learns image and text encoders on 400 million internet image-text pairs, producing a shared embedding space that supports zero-shot transfer to diverse vision tasks via natural language prompts.

## Summary

CLIP trains an image encoder and a text encoder so the cosine similarity of paired (image, text) embeddings is maximized while non-pairs are pushed apart, using a symmetric cross-entropy loss across batches. The authors collected WebImageText (WIT), a 400-million-pair dataset, and trained a series of ResNet and Vision Transformer (ViT) variants. The resulting models match the original ResNet-50 on ImageNet zero-shot and transfer non-trivially to over 30 benchmarks spanning Optical Character Recognition (OCR), action recognition in videos, geo-localization, and fine-grained classification. CLIP weights and inference code are released under MIT license, and the embeddings became the de facto multimodal retrieval and similarity backbone for downstream open-source projects.

## Relevance to AGI

CLIP is the dominant zero-shot annotator for the kinds of stimuli AGI hosts: still images (Natural Scenes Dataset (NSD), Common Objects in Context (COCO)), film frames (Forrest Gump, Healthy Brain Network (HBN) movies), and Pixar shorts. A single forward pass produces an embedding that can be projected against a HED-derived label vocabulary to score scene-level concepts at zero training cost. AGI's image-annotation tool already uses CLIP-derived features, and the Stim-BIDS events.tsv format is well suited to record CLIP scores per stimulus or per video frame as continuous predictors that downstream encoding models (Voxelwise, Neuroscout) can pick up directly.

## Notable details

- 400 million (image, text) pairs collected from public web sources.
- Eight model scales spanning roughly two orders of magnitude of compute.
- Released checkpoints: ResNet-50 / 101 / 50x4 / 50x16 / 50x64 and ViT-B/32, ViT-B/16, ViT-L/14.
- Zero-shot ImageNet top-1 accuracy of 76.2 percent for ViT-L/14@336.
- Key downstream forks: OpenCLIP (LAION), SigLIP, MetaCLIP, EVA-CLIP.

## Open questions / limitations

- Training data is not redistributable, so reproductions rely on LAION-style approximations.
- Strong demographic, geographic, and lexical biases inherited from web text; documented in the original Section 7.
- Image and text encoders are frozen at training time; fine-grained spatial grounding (boxes, masks) requires extensions like GroundingDINO or SAM.
- Performance on naturalistic video remains weak without temporal aggregation.
- License of derived embeddings is not formally clarified for commercial reuse.

## Citations

Primary: `radford2021clip`. Related:
- `radford2023whisper`, companion audio model from the same group.
- `liu2024groundingdino`, uses CLIP-style features for open-set detection.
- `mcnamara2017pliers`, orchestration layer that wraps CLIP-style extractors.
- `delavega2022neuroscout`, uses Pliers + CLIP for fMRI feature timelines.
- `zhang2024llavavideo`, vision-language model that builds on CLIP visual encoders.
