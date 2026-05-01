---
slug: coco
type: dataset
strand: data
year: 2014
authors: [Lin, Maire, Belongie, Hays, Perona, Ramanan, Dollár, Zitnick]
venue: ECCV (European Conference on Computer Vision) / arXiv 1405.0312
doi: 10.1007/978-3-319-10602-1_48
url: https://cocodataset.org/
license: CC-BY-4.0 (annotations); Flickr image rights vary (mostly CC-BY)
modalities: [image, behavior]
tags: [naturalistic-images, captions, segmentation, stimulus-source, computer-vision]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Microsoft Common Objects in Context (COCO) image set, originally released as a computer-vision benchmark, is the upstream stimulus source for the Natural Scenes Dataset (NSD) and most modern naturalistic-image neuroimaging studies. It provides 328,000+ images with object segmentation masks, 80 thing categories, and 5 free-form English captions per image.

## Summary

Lin et al. (Microsoft / Cornell / Caltech / Brown) released COCO at the European Conference on Computer Vision (ECCV) 2014 as a computer vision benchmark for object detection, segmentation, and captioning. The dataset comprises 328,000 images (later expanded), 2.5 million object instance segmentations across 80 "thing" categories (person, animals, vehicles, household items) and 91 "stuff" categories. Each image carries 5 free-form English captions. COCO is the dominant stimulus source for naturalistic-image neuroscience: NSD (73,000 COCO images), Algonauts 2023, BOLD5000 (2,000 COCO images), Generic Object Decoding, and many language-grounding studies. The annotation set itself is the canonical example of community-driven naturalistic stimulus annotation at scale.

## Relevance to Annotation Garden Initiative (AGI)

COCO is the upstream "annotation source of truth" for visual-stimulus neuroscience. AGI's Stim-Brain Imaging Data Structure (BIDS) repositories should treat COCO image identifiers (`cocoId`) as a canonical key and map to/from COCO bounding boxes, masks, captions, and panoptic segmentation. AGI does not own COCO, but it should host crosswalks: from `cocoId` to NSD `nsdId`, BOLD5000 file paths, Algonauts scene IDs, and so on. This is exactly the kind of integrative cataloguing AGI is designed for.

## Notable details

- 328,000 images total (COCO 2017 split: 118k train, 5k val, 41k test, plus unlabeled).
- 1.5 million object instances across 80 things classes.
- 5 free-form English captions per image (CC-BY-4.0 licensed).
- Subsequent extensions: COCO-Stuff, COCO Panoptic, COCO Captions, RefCOCO (referring expressions).
- Image rights: Flickr-sourced; majority CC-BY 2.0; license per-image in Lookup tables.

## Open questions / limitations

- Cultural / geographic bias: predominantly North American / Western European scene composition.
- Caption distribution skewed toward agentive descriptions; lacks affective and aesthetic dimensions.
- No native Hierarchical Event Descriptors (HED) mapping; AGI must build it.

## Citations

- Primary: `Lin2014Microsoft` (ECCV 2014).
- Related: ImageNet (Deng 2009); Visual Genome (Krishna 2017); Open Images (Kuznetsova 2020).
