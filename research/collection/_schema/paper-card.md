# Paper-Card Schema

Each entry lives in its own folder under the strand:

```
research/collection/<strand>/<slug>/
├── card.md         # this paper-card — required
├── source.pdf      # full PDF — when redistributable / open access
├── source.md       # markdown extraction of the paper — always required
└── meta.json       # provenance: source URL, retrieval date, license, hash
```

Rationale: we need offline-archival access to the underlying papers, not only summaries. Future
synthesis + drafting must be able to re-read the primary text.

## card.md template

```yaml
---
slug: <kebab-case-short-id>             # matches folder name
type: paper | dataset | tool | platform | standard
strand: tools | data | science
year: <YYYY>
authors: [<surname1>, <surname2>, ...]
venue: <journal / conference / org>
doi: <doi or null>
url: <canonical url or null>
license: <license or null>              # for datasets, tools, and PDF redistribution
modalities: [eeg, ieeg, fmri, meg, eyetrack, behavior, ...]
tags: [<5-12 short tags>]
agi_relevance: high | medium | low
imported_from: <relative path or null>
added: <YYYY-MM-DD>

# Archival fields
pdf_status: archived | not-redistributable | not-available | not-applicable
pdf_path: source.pdf | null
md_path: source.md | null
md_quality: clean | rough | partial | abstract-only
---
```

### Sections

**TL;DR** — one or two sentences.
**Summary** — 3-6 sentences covering core contribution, method, scope, key numbers.
**Relevance to AGI** — concrete connection to AGI's tooling / data / science / FAIR commons.
**Notable details** — bullet list of facts worth pulling forward.
**Open questions / limitations** — what this work doesn't answer.
**Citations** — primary BibTeX key + ≤5 related works as one-liners.

## meta.json template

```json
{
  "doi": "10.xxxx/xxxxx",
  "source_url": "https://...",
  "retrieved_at": "2026-04-30",
  "pdf_sha256": "<hash if archived, null otherwise>",
  "pdf_license": "CC-BY | CC-BY-NC | publisher-paywall | preprint-cc | unknown",
  "redistribution_ok": true | false,
  "notes": "<retrieval notes, e.g. 'arxiv preprint used; published version paywalled'>"
}
```

## Storage rules

- **Open-access PDFs** (CC-BY, CC0, arXiv preprints, bioRxiv, etc.): commit directly under `source.pdf`.
- **Paywalled / non-redistributable**: do NOT commit the PDF. Set `pdf_status: not-redistributable`. Still commit `source.md` (extracted text is generally fair use for research notes; flag if uncertain).
- **Datasets / tools without a paper**: `pdf_status: not-applicable`. Store the project README or canonical landing page as `source.md`.
- **Failed downloads**: `pdf_status: not-available`. Document the failure in `meta.json` notes.

## Tooling

Use `opencite:opencite` to:
1. Resolve DOI / canonical URL
2. Download PDF where licensing permits
3. Convert PDF → markdown (`source.md`)
4. Export BibTeX entry

For tools / platforms without papers, snapshot the canonical README as `source.md` and link the repo URL.
