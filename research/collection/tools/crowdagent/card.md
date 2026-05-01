---
slug: crowdagent
type: tool
strand: tools
year: 2025
authors: [Qin, Zhu, Xia, Chen, Zhu, Lin, Zhao, Xu, Fan, Wu, Wang]
venue: arXiv preprint arXiv:2509.14030
doi: 10.48550/arXiv.2509.14030
url: https://arxiv.org/abs/2509.14030
license: code MIT (system); paper preprint
modalities: [text, image, multimodal]
tags: [multi-agent, annotation, LLM, SLM, human-in-the-loop, crowdsourcing, quality-assurance]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

CrowdAgent is a multi-agent annotation system that mirrors a human crowdsourcing company by orchestrating Large Language Models (LLMs), Small Language Models (SLMs), and human experts under explicit task-assignment, quality-assurance, and budget-tracking agents.

## Summary

The authors argue that prior hybrid human-plus-LLM annotation systems treat labeling as a single algorithmic step and ignore the operational layer (assignment, quality control, cost) that real crowdsourcing companies handle. CrowdAgent introduces four agents: Annotation Agents (multiple LLM prompts, noisy-label-trained SLMs, and human annotators on platforms like NetEase Youling), a Quality Assurance Agent that runs Bayesian label aggregation against a hidden golden set, a Financing Agent that tracks per-source cost-effectiveness, and a Scheduling Agent that dispatches each unlabeled sample to the most suitable annotator at each round. The system was evaluated on six multimodal classification tasks and consistently improved the quality-cost frontier compared to single-source baselines. Code is released at github.com/QMMMS/CrowdAgent.

## Relevance to AGI

AGI faces exactly the problem CrowdAgent targets: a single stimulus dataset (e.g. HBN movies) needs annotations from multiple sources (Vision-Language Models (VLMs), citizen scientists, expert raters) under varying budgets and quality requirements. The multi-agent pattern, with a separate Quality Assurance Agent computing inter-annotator agreement against a HED-tagged golden set and a Scheduling Agent that routes hard frames to humans while easy frames go to a VLM, is a direct template for AGI's annotation pipeline. The cost-tracking abstraction also maps cleanly onto credit allocation among lab contributors.

## Notable details

- Four-agent architecture: Annotation, Quality Assurance, Financing, Scheduling.
- Bayesian aggregation with a confusion matrix derived from a hidden golden set.
- LLM annotators instantiated through diverse prompt strategies (sequence swap, format change, confirmation bias).
- SLM annotators trained with noisy-label techniques as label purifiers.
- Six multimodal classification tasks used for evaluation; SLM training details in Appendix C.

## Open questions / limitations

- Tasks evaluated are classification only; the paper does not address span-level, spatial, or temporal annotation.
- Cost-effectiveness assumes priced human labor; volunteer / open-science contributors are not modeled.
- Bayesian aggregation requires a golden set that itself must be trustworthy; bootstrapping that set is not addressed.
- Privacy / consent for sensitive stimuli (clinical EEG, child-facing video) is out of scope.
- No discussion of provenance recording for downstream re-execution or auditing.

## Citations

Primary: `qin2025crowdagent`. Related:
- `mcnamara2017pliers`, alternative orchestration via static feature extraction.
- `zhang2024llavavideo`, example LLM annotator that could be plugged in.
- `radford2021clip`, embedding model for label space prior.
- `labelstudio2020`, manual annotation tool that complements multi-agent pipelines.
- `delavega2022neuroscout`, analogous orchestration for fMRI features.
