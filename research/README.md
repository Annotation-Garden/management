# Annotation Garden — Research Corpus

Methodically collected literature, tools, and dataset metadata for the Annotation Garden Initiative.

## Layout

```
research/
├── README.md                    # this file
├── _briefs/                     # agent dispatch briefs (one per strand)
│   ├── strand-A-tools.md
│   ├── strand-B-data.md
│   └── strand-C-science.md
├── collection/                  # Phase 1 output — raw paper-cards
│   ├── _schema/paper-card.md    # shared template
│   ├── tools/                   # Strand A
│   │   ├── INDEX.md
│   │   ├── tools.bib
│   │   └── <slug>/              # one folder per artifact
│   │       ├── card.md
│   │       ├── source.pdf       # if redistributable
│   │       ├── source.md        # always
│   │       └── meta.json
│   ├── data/                    # Strand B (same per-entry folder layout)
│   └── science/                 # Strand C (same per-entry folder layout)
└── synthesis/                   # Phase 2 output (taxonomies, gap analysis)
```

## How to add an entry

1. Create a folder `collection/<strand>/<short-slug>/`
2. Inside it, write `card.md` from the schema in `collection/_schema/paper-card.md`
3. Use `opencite` to download the PDF (when redistributable) and produce `source.md`
4. Write `meta.json` with provenance (DOI, retrieved_at, license, sha256)
5. Append the BibTeX to the strand's `.bib` file
6. Append a one-line entry to the strand's `INDEX.md`

**License-aware archival:** open-access PDFs are committed; paywalled PDFs are NOT committed (set `pdf_status: not-redistributable` in card.md and document in meta.json). Markdown extractions are always stored.

## Provenance

Phase 1 collection seeded by the ANNOTATE R01 lit review at
`grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/`. Imported entries
note their source in the `imported_from` front-matter field.

## Phases

- **Phase 1 (issue #4):** populate `collection/` — three parallel strand agents
- **Phase 2 (issue #5):** synthesize into `synthesis/` taxonomies and gap analysis
- **Phase 3 (issue #6):** update `agi-white-paper.md` and draft direction documents

See [epic #3](https://github.com/Annotation-Garden/management/issues/3) for the full plan.
