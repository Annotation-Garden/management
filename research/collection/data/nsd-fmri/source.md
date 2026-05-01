# Source notes: NSD descriptor (Allen 2022)

> Paywalled at Nature Neuroscience (DOI 10.1038/s41593-021-00962-x); PDF not redistributed.
> This is a structured summary of the descriptor paper plus dataset README content, supplemented from the open-access landing page (https://naturalscenesdataset.org).

## Citation

Allen EJ, St-Yves G, Wu Y, Breedlove JL, Prince JS, Dowdle LT, Nau M, Caron B, Pestilli F, Charest I, Hutchinson JB, Naselaris T, Kay K. **A massive 7T fMRI dataset to bridge cognitive neuroscience and artificial intelligence.** *Nature Neuroscience* 25, 116 to 126 (2022). DOI: 10.1038/s41593-021-00962-x. PMID: 34916659.

## Cohort

- N = 8 healthy adults (NSD subjects 1 to 8). Age range 19 to 32; mixed sex.
- Each subject completed 30 to 40 task scan sessions (varies per subject) plus one prfStim session and one fLoc session.

## Acquisition

- 7T Siemens Magnetom passively shielded scanner (University of Minnesota Center for Magnetic Resonance Research, CMRR).
- 1.8-mm isotropic gradient-echo echo-planar imaging (EPI), repetition time (TR) = 1.6 s, multi-band acceleration factor 5.
- Whole brain coverage with field-mapping correction.
- Eye tracking (when permitted by participant) and physiological logging.
- Anatomical: T1-weighted (T1w), T2-weighted (T2w) at 0.8-mm isotropic; diffusion-weighted imaging (DWI) at 1.5-mm with multi-shell b-values.

## Stimulus design

- 73,000 unique COCO images (Lin et al. 2014). Square cropped to 8.4 deg visual angle.
- Each subject viewed 9,000 to 10,000 unique COCO images plus a shared 1,000 image subset across subjects.
- Each image shown 3 times across the experiment (with 6 repeats for the shared subset).
- Continuous recognition memory task: "Have you seen this image before in any session?" Yes/No button response.
- Trial timing: 3 s on / 1 s off (4 s trial duration, 62 trials per run, 12 runs per session).

## Outputs released

- Raw Digital Imaging and Communications in Medicine (DICOM) and Brain Imaging Data Structure (BIDS)-Neuroimaging Informatics Technology Initiative (NIfTI) functional and anatomical data.
- Pre-processed surface-space data (FreeSurfer fsaverage and native).
- Single-trial beta weights (GLMsingle, three versions: betas_assumeHRF, betas_fithrf, betas_fithrf_GLMdenoise_RR).
- Behavioral logs, eye tracking, ROI atlases (Kastner, HCP-MMP, Glasser), category-selective masks (face, body, place, word), retinotopic angle/eccentricity maps.
- COCO image stimuli with cross-references to COCO instance/keypoint/caption annotations.

## Data dictionary (high level)

- `sub-{01..08}/ses-nsd{01..40}/func/sub-XX_ses-nsdYY_task-nsdcore_run-ZZ_bold.nii.gz`
- `derivatives/glmsingle/sub-XX/...`
- `stimuli/nsd_stimuli.hdf5` (single HDF5 archive with 73,000 RGB 425x425 images keyed by `nsdId`).
- `stimuli/nsd_stim_info_merged.csv` (mapping `nsdId` to `cocoId`, COCO split, shared1000 flag, repetition counts).

## Access conditions

- Hosted on Amazon Web Services (AWS) Simple Storage Service (S3) `s3://natural-scenes-dataset/`.
- Download: requires data-use agreement; registration at https://naturalscenesdataset.org.
- License: CC-BY 4.0 for derived data products; COCO image rights inherit Flickr terms (mostly CC-BY).

## Ecosystem

- NSD-iEEG (Huang et al. 2024, Vision Sciences Society / jov.arvojournals.org/article.aspx?articleid=2801527): 12 epilepsy patients, 1,000 NSD subset, broadband gamma activity.
- NOD-EEG / NOD-MEG (Zhang et al. 2025, Scientific Data 10.1038/s41597-025-05174-7): cross-modal extension on similar object-image set.
- alljoined / NSD-EEG (Xu et al. 2024, arxiv:2401.10023): scalp EEG to NSD images, public stimulus set.
- BrainScore-NSD: encoding model leaderboard.
- Algonauts 2023: fMRI encoding challenge built on NSD.

## Annotation hooks for AGI

| Layer | State | Garden opportunity |
|-------|-------|--------------------|
| COCO segmentation | provided | Already in COCO; pull-through to BIDS sidecars. |
| COCO captions | provided | Five free-form captions per image (English). |
| HED tags per object | absent | Map COCO categories to HED `Item/Object/...` tree. |
| Visual saliency | partial (Itti, GBVS, DeepGaze pre-computed by community) | Aggregate predictions into a saliency layer. |
| Scene-level affect | absent | International Affective Picture System (IAPS)-style valence/arousal ratings would be additive. |
| Aesthetic / memorability | partial (LaMem, AVA scores available externally) | Stim-BIDS-formatted aggregation. |
