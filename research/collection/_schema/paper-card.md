# Paper-Card Schema

Each entry lives in its own folder under the strand:

```
research/collection/<strand>/<slug>/
├── card.md         this paper-card; required
├── source.pdf      full PDF; only when redistributable / open access
├── source.md       markdown extraction of the paper; always required
└── meta.json       provenance: source URL, retrieval date, license, hash
```

Rationale: we need offline-archival access to the underlying papers, not only summaries. Future
synthesis and drafting must be able to re-read the primary text.

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

### agi_relevance calibration anchors

To keep the field useful for downstream filtering, apply the following anchors:

- **high**: the entry is a direct dependency of AGI deliverables. Examples: BIDS, HED, Stim-BIDS BEP044, NSD (all modalities), HBN-EEG, StudyForrest, EEGLAB, OpenNeuro, NEMAR, NeuroScout, GLMsingle, HEDit-related work, papers that AGI infrastructure ships against.
- **medium**: standard tools / datasets / methods within scope but not a direct AGI dependency. Examples: HCP-task, ABCD, Whisper, CLIP, mTRF, encoding-model surveys, foundation-model papers in the broader landscape.
- **low**: tangential or background context. Examples: peripheral cognitive batteries (Cam-CAN, MyConnectome, dHCP), general-purpose annotators not specialized for neuroimaging (Praat, BORIS, Datavyu, Label-Studio), broad principles documents whose direct utility is reference-only.

If more than ~40% of entries land in `high`, the field has lost discriminative power; rebalance.

### Sections

- **TL;DR**: one or two sentences. Should capture the *thesis*, not duplicate the Summary opening.
- **Summary**: 3-6 sentences covering core contribution, method, scope, key numbers.
- **Relevance to AGI**: concrete connection to AGI's tooling, data, science, or FAIR commons. Cite specific mechanisms (HED, BIDS, events.tsv, Stim-BIDS, pointer architecture). Avoid generic prose.
- **Notable details**: bullet list of facts worth pulling forward to synthesis.
- **Open questions / limitations**: what this work doesn't answer. Paper-specific only; generic boilerplate is harmful because Phase 2 gap analysis depends on this.
- **Citations**: primary BibTeX key plus up to 5 related works as one-liners.

## meta.json template

```json
{
  "doi": "10.xxxx/xxxxx",
  "source_url": "https://...",
  "retrieved_at": "2026-04-30",
  "pdf_sha256": "<sha256 hex if archived; null otherwise>",
  "pdf_license": "<see vocabulary below>",
  "redistribution_ok": true | false,
  "notes": "<retrieval notes, e.g. 'arxiv preprint used; published version paywalled'>"
}
```

### pdf_license vocabulary

Common values used across the corpus:

- `CC-BY`, `CC-BY-2.0`, `CC-BY-3.0`, `CC-BY-4.0`, `CC-BY-NC`, `CC0`
- `preprint-cc-arxiv`, `preprint-cc-biorxiv`, `preprint-cc-osf`
- `author-accepted-manuscript` (institutional repository copy)
- `publisher-paywall`
- `not-applicable` (e.g. tool with only a README)
- `unknown`

Values may include a parenthetical qualifier when needed, e.g.
`publisher-paywall (NeuroImage); university repository copy archived`. Keep `redistribution_ok`
semantically aligned with the license: any `*-paywall` value implies `redistribution_ok: false`.

## Storage rules

- **Open-access PDFs** (CC-BY, CC0, arXiv, bioRxiv, OSF, institutional repository copies): commit directly under `source.pdf` and populate `pdf_sha256`.
- **Paywalled / non-redistributable**: do NOT commit the PDF. Set `pdf_status: not-redistributable`, `pdf_path: null`, `pdf_sha256: null`. Still commit `source.md` (extracted text is generally fair use for research notes; flag in `notes` if uncertain).
- **Datasets / tools without a paper**: set `pdf_status: not-applicable`. Store the project README or canonical landing page as `source.md`.
- **Failed downloads**: set `pdf_status: not-available`. Document the failure mode in `meta.json` notes (Cloudflare gate, reCAPTCHA, broken DOI, etc.).

The `redistribution_ok` field is the single source of truth for whether `source.pdf` may exist
in the repo. CI for this corpus should enforce: `redistribution_ok: false` implies no `source.pdf`
file in the entry folder.

## Tooling

Use `opencite:opencite` to:
1. Resolve DOI / canonical URL
2. Download PDF where licensing permits
3. Convert PDF to markdown (`source.md`)
4. Export BibTeX entry

For tools or platforms without papers, snapshot the canonical README as `source.md` and link the
repo URL.
