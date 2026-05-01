# BIDS-Validator

Source snapshot: https://github.com/bids-standard/bids-validator (commit-pinned 2026-04-30)

The BIDS-Validator is the reference implementation for checking that a dataset conforms to the Brain Imaging Data Structure (BIDS) specification. It is maintained by the BIDS community under the bids-standard GitHub organization and is distributed in two compatible forms:

1. A JavaScript / TypeScript implementation that runs both as a Node.js command-line tool (`bids-validator`) and as an in-browser validator embedded in https://bids-standard.github.io/bids-validator/.
2. A newer Python implementation (`bids-validator-deno` and the legacy `bids-validator` PyPI package) that wraps the same schema definitions.

Both implementations consume the canonical BIDS schema (https://github.com/bids-standard/bids-specification/tree/master/src/schema) so that any update to the specification immediately propagates to the validators.

The validator checks:

- File and folder naming conventions (entities, suffixes, extensions).
- Required and recommended sidecar JSON fields per modality.
- Cross-file consistency (events.tsv timing, channels.tsv length, scans.tsv coverage).
- Modality extensions: BIDS-MEG, BIDS-EEG, BIDS-iEEG, BIDS-PET, BIDS-MRS, Arterial Spin Labeling.
- Optional plugin-based checks for HED tag validity.

Common usage:

```
# Local CLI
bids-validator path/to/dataset

# Hosted web UI
https://bids-standard.github.io/bids-validator/
```

The validator emits structured JSON output suitable for ingestion by Continuous Integration pipelines, BIDS-Apps, and dataset archives such as OpenNeuro and NEMAR.

License: MIT.
