# fMRIPrep

Source snapshot: Esteban O. et al. (2019). fMRIPrep: a robust preprocessing pipeline for functional MRI. Nature Methods 16(1): 111-116. DOI: 10.1038/s41592-018-0235-4. Companion documentation at https://fmriprep.org and code at https://github.com/nipreps/fmriprep.

fMRIPrep is a Brain Imaging Data Structure (BIDS) App that preprocesses functional Magnetic Resonance Imaging (fMRI) data in a robust, generalizable, and largely automatic way. It is the flagship tool of the Nipreps (NeuroImaging PREProcessing tools) project and is the most widely adopted preprocessing pipeline for naturalistic and traditional fMRI studies as of 2026.

Pipeline highlights:

- Anatomical workflow: skull-stripping (ANTs), bias-field correction (N4), tissue segmentation (FAST), spatial normalization to standard templates via ANTs, FreeSurfer reconstruction (optional).
- Functional workflow: head-motion correction, susceptibility distortion correction (fieldmap-based or fieldmap-less SyN), boundary-based registration to anatomical space (FreeSurfer bbregister), spatial normalization to MNI152 / fsaverage, slice timing correction.
- Confound regressors: 6 motion parameters and derivatives, framewise displacement, DVARS, anatomical and temporal CompCor, global signal, AROMA components, white-matter and cerebrospinal-fluid signals.
- Quality control: per-subject HTML report with mosaic views and registration checks.

Containerized via Docker, Singularity, and Apptainer; runs as a self-contained BIDS App on any HPC, cloud, or local workstation. Outputs follow the BIDS-Derivatives specification.

License: Apache-2.0. Reference paper:

Esteban, O., Markiewicz, C. J., Blair, R. W., Moodie, C. A., Isik, A. I., Erramuzpe, A., Kent, J. D., Goncalves, M., DuPre, E., Snyder, M., Oya, H., Ghosh, S. S., Wright, J., Durnez, J., Poldrack, R. A., & Gorgolewski, K. J. (2019). fMRIPrep: a robust preprocessing pipeline for functional MRI. Nature Methods, 16(1), 111-116. DOI: 10.1038/s41592-018-0235-4.
