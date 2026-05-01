---
slug: nwb
type: standard
strand: tools
year: 2022
authors: [Rübel, Tritt, Ly, Dichter, Ghosh, Niu, Baker, Soltesz, Ng, Svoboda, Frank, Bouchard]
venue: eLife
doi: 10.7554/eLife.78362
url: https://www.nwb.org
license: BSD-3-Clause
modalities: [ephys, ophys, behavior]
tags: [NWB, neurophysiology, HDF5, data-language, FAIR, BRAIN-Initiative, schema]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Neurodata Without Borders (NWB) is an extensible data language for neurophysiology, defined through a hierarchical schema and serialized in Hierarchical Data Format 5 (HDF5) or Zarr, that unifies single-cell ephys, optical imaging, behavior, and stimulus metadata across species and labs.

## Summary

The 2022 eLife paper articulates NWB's core design: separate the schema specification language (NWB:N specification language and HDMF) from the data model (Neurodata types), and from storage backends (HDF5 today, Zarr in pipeline). This separation lets the schema evolve while preserving on-disk compatibility. NWB defines extension points (neurodata extensions) so labs can add custom metadata without forking the standard. The ecosystem includes PyNWB, MatNWB, NWB Inspector for validation, NWB GUIDE for conversion, and DANDI for archiving. NWB has been adopted across the BRAIN Initiative, Allen Institute, Janelia, IBL, and many smaller labs, and is the canonical data language for cellular and circuit-level neurophysiology.

## Relevance to AGI

NWB sits adjacent to AGI rather than at its center. AGI's primary scope is human stimulus annotation, where Brain Imaging Data Structure (BIDS) is the dominant standard. However, when AGI stimuli are paired with non-human or invasive recordings (rodent two-photon viewing of natural images, primate ephys to movies, intracranial human responses on the DANDI archive), NWB becomes the format on the response side. AGI annotations will need a bridge that exposes events.tsv and HED tags as NWB TimeIntervals or stimulus tables, so the same annotation can travel with both BIDS and NWB recordings. The neurodata-extension mechanism is also a useful template for AGI's own annotation-side schema extensions.

## Notable details

- Schema language: NWB:N specification format, implemented through HDMF.
- Storage: HDF5 today, Zarr support emerging.
- Reference libraries: PyNWB, MatNWB; conversion via NeuroConv and NWB GUIDE.
- DANDI archive is the canonical NWB repository.
- Includes data types for spike trains, calcium imaging, behavioral video, optogenetic stimuli.

## Open questions / limitations

- HDF5 file size and partial-read performance can be limiting for cloud workflows.
- Naming and metadata conventions for stimulus alignment with BIDS-style annotations are not yet harmonized.
- Tooling for human imaging (fMRI, scalp EEG) is intentionally minimal; that lives in BIDS.
- Conversion barrier for legacy data is real, despite NeuroConv's improvements.
- Long-term stewardship depends on continued BRAIN Initiative funding.

## Citations

Primary: `rubel2022nwb`. Related:
- `gorgolewski2016bids` — sister standard for human imaging.
- `dandi2024` — archive built on NWB.
- `wilkinson2016fair` — guiding principles NWB operationalizes.
- `halchenko2021datalad` — alternative versioned distribution.
- `markiewicz2021openneuro` — peer archive on the BIDS side.
