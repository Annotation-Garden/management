# DANDI: Distributed Archives for Neurophysiology Data Integration

Source snapshot: https://dandiarchive.org and https://github.com/dandi/dandi-archive (commit-pinned 2026-04-30).

DANDI is a publicly available archive for cellular neurophysiology data, funded primarily by the U.S. National Institutes of Health (NIH) BRAIN Initiative. It provides versioned storage, programmatic access, and Web-based browsing for datasets formatted according to the Neurodata Without Borders (NWB) and Brain Imaging Data Structure (BIDS) standards.

Key features:

- Versioned dataset hosting with stable Digital Object Identifiers (DOIs) per published version.
- Native NWB ingestion plus growing support for BIDS-iEEG and BIDS-microscopy.
- Python (`dandi`), Web, and Application Programming Interface (API) access patterns.
- Per-dataset metadata cards including species, brain region, recording technique, and assay type.
- Integration with the JupyterHub-based DANDI Hub for in-browser analysis without download.
- Free-tier storage funded by the BRAIN Initiative; institutional uploads typically require asset metadata review.

The archive is operated by the LINC Brain Project (Laboratory for the Imaging of Neural Circuits) and partner institutions (Lawrence Berkeley National Laboratory, Catalyst Neuro, Kavli Foundation collaborators). As of 2026, DANDI hosts hundreds of datasets covering single-unit electrophysiology, two-photon imaging, voltage imaging, optogenetics, and intracranial human EEG.

Useful entry points:

- Web UI: https://dandiarchive.org/
- Python client: https://github.com/dandi/dandi-cli
- DANDI Hub: https://hub.dandiarchive.org/
- Documentation: https://docs.dandiarchive.org/

License: dataset licenses are set per-asset by the contributor (commonly CC-BY or CC0). The DANDI software stack is BSD-3-Clause.
