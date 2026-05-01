# Datavyu

Source snapshot: https://datavyu.org and https://github.com/databrary/datavyu (commit-pinned 2026-04-30).

Datavyu is a free, open-source video coding tool maintained by the Databrary Project at New York University. It is the descendant of the older MacSHAPA / OpenSHAPA tradition and has been widely adopted in developmental psychology, child language acquisition, infant action research, and other fields where naturalistic video coding is central.

Key features:

- Sheet-based annotation interface where each row is an event with start time, stop time, and arbitrary user-defined columns.
- Multiple synchronized video and audio panels with frame-level navigation.
- Codes can be hierarchical via passes (named annotation tracks); each pass can have its own code dictionary.
- Ruby-based scripting interface for batch operations, transformations, and inter-coder reliability.
- Companion Databrary repository (https://databrary.org) for sharing video plus annotations under managed-access agreements.

Datavyu emphasizes:

- Reproducibility: every code is timestamped and the project file is plain-text-friendly XML.
- Reliability: explicit support for double-coding workflows and reliability statistics.
- Sharing: designed to feed Databrary, which honors institutional review board (IRB) constraints around child-subject video.

License: GPL-3.0. Cross-platform binaries for macOS, Windows, and Linux.

The tool does not have a single canonical paper; the closest reference is the Databrary white paper (Adolph et al. 2017) and the project documentation. The BibTeX entry uses `datavyu2014` as the placeholder key for the tool itself.
