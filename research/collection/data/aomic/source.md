# The Amsterdam Open MRI Collection, a set of multimodal MRI datasets for individual difference analyses

# The Amsterdam Open MRI Collection, a set of multimodal MRI datasets for individual difference analyses

Lukas Snoek, Maite M. van der Miesen, Tinka Beemsterboer, Andries van der Leij, Annemarie Eigenhuis, H. Steven Scholte

## Abstract

We present the Amsterdam Open MRI Collection (AOMIC): three datasets with multimodal (3T) MRI data including structural (T1-weighted), diffusion-weighted, and (resting-state and task-based) functional BOLD MRI data, as well as detailed demographics and psychometric variables from a large set of healthy participants (N = 928, N = 226, and N = 216). Notably, task-based fMRI was collected during various robust paradigms (targeting naturalistic vision, emotion perception, working memory, face perception, cognitive conflict and control, and response inhibition) for which extensively annotated event-files are available. For each dataset and data modality, we provide the data in both raw and preprocessed form (both compliant with the Brain Imaging Data Structure), which were subjected to extensive (automated and manual) quality control. All data is publicly available from the OpenNeuro data sharing platform.

## Keywords

Neuroscience, Neuroscience

## Background & Summary

It is becoming increasingly clear that robust effects in neuroimaging studies require very large sample sizes^{1,2}, especially when investigating between-subject effects^{3}. With this in mind, we have run several large-scale “population imaging” MRI projects over the past decade at the University of Amsterdam, with the aim to reliably estimate the (absence of) structural and functional correlates of human behavior and mental processes. After publishing several articles using these datasets^{4--8}, we believe that making the data from these projects publicly available will benefit the neuroimaging community most. To this end, we present the Amsterdam Open MRI Collection (AOMIC) — three large-scale datasets with high-quality, multimodal 3 T MRI data and detailed demographic and psychometric data, which are publicly available from the OpenNeuro data sharing platform. In this article, we describe the characteristics and contents of these three datasets in a manner that complies with the guidelines of the COBIDAS MRI reporting framework^{9}.

We believe that AOMIC represents a useful contribution to the growing collection of publicly available population imaging MRI datasets^{10--13}. AOMIC contains a large representative dataset of the general population, “ID1000” (N = 928), and two large datasets with data from university students, “PIOP1” (N = 216) and “PIOP2” (N = 226; Population Imaging of Psychology). Each dataset contains MRI data from multiple modalities (structural, diffusion, and functional MRI), concurrently measured physiological (respiratory and cardiac) data, and a variety of well-annotated demographics (age, sex, handedness, educational level, etc.), psychometric measures (intelligence, personality), and behavioral information related to the task-based fMRI runs (see Fig. 1 and Table 1 for an overview). Furthermore, AOMIC offers, in addition to the raw data, also preprocessed data from well-established preprocessing and quality control pipelines, all consistently formatted according to the Brain Imaging Data Structure^{14}. As such, researchers can quickly and easily prototype and implement novel secondary analyses without having to worry about quality control and preprocessing themselves.

---

www.nature.com/scientificdata/

![img-0.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-1.jpg)
Fig. 1 General overview of AOMIC's contents. Each dataset (ID1000, PIOP1, PIOP2) contains multimodal MRI data, physiology (concurrent with fMRI acquisition), demographic and psychometric data, as well as a large set of "derivatives", i.e., data derived from the original "raw" data through state-of-the-art preprocessing pipelines.

|  | ID1000 | PIOP1 |  |  |  |  |  | PIOP2 |  |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| N subj. | 928 | 216 |  |  |  |  |  | 226 |  |  |  |
| T1w | 928 | 216 |  |  |  |  |  | 226 |  |  |  |
| DWI | 925 | 211 |  |  |  |  |  | 226 |  |  |  |
| Fieldmap | n/a | n/a |  |  |  |  |  | 226 |  |  |  |
|  | Mov | RSNO | Emo | G-str | FPNO | WM | Antic | RS | Emo | WM | Stop |
| fMRI | 881 | 210 | 208 | 208 | 203 | 207 | 203 | 214 | 222 | 224 | 226 |
| Physiology | 790 | 198 | 194 | 194 | 189 | 194 | 188 | 216 | 216 | 211 | 217 |

Table 1. Overview of the number of subjects per dataset and tasks. Mov: movie watching, RS: resting-state, Emo: emotion matching, G-str: gender-stroop, FP: face perception, WM: working memory, Antic: anticipation, Stop: stop-signal. MB subscript indicates that multiband acceleration (also known as simultaneous slice excitation) was used. Tasks without this subscript were acquired without multiband acceleration (i.e., "sequential" acquisition).

Due to the size and variety of the data in AOMIC, there are many ways in which it can be used for secondary analysis. One promising direction is to use the data for the development of generative and discriminative machine learning-based algorithms, which often need large datasets to train models on. Another, but related, use of AOMIC's data is to use it as a validation dataset (rather than train-set) for already developed (machine learning) algorithms to assess the algorithm's ability to generalize to different acquisition sites or protocols. Lastly, due to the rich set of confound variables shipped with each dataset (including physiology-derived noise regressors), AOMIC can be used to develop, test, or validate (novel) denoising methods.

# Methods

In this section, we describe the details of the data acquisition for each dataset in AOMIC. We start with a common description of the MRI scanner used to collect the data. The next two sections describe the participant characteristics, data collection protocols, experimental paradigms (for functional MRI), and previous analyses separately for the ID1000 study and the PIOP studies. Then, two sections describe the recorded subject-specific variables (such as educational level, background socio-economic status, age, etc.) and psychometric measures from questionnaires and tasks (such as intelligence and personality). Finally, we describe how we standardized and preprocessed the data, yielding an extensive set of "derivatives" (i.e., data derived from the original raw data).

Scanner details and general scanning protocol (all datasets). Data from all three datasets were acquired on the same Philips 3T scanner (Philips, Best, the Netherlands), but underwent several upgrades in between the three studies. The ID1000 dataset was scanned on the "Intera" version, after which the scanner was

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

upgraded to the “Achieva” version (converting a part of the signal acquisition pathway from analog to digital) on which the PIOP1 dataset was scanned. After finishing the PIOP1 study, the scanner was upgraded to the “Achieva dStream” version (with even earlier digitalization of the MR signal resulting in less noise interference), on which the PIOP2 study was scanned. All studies were scanned with a 32-channel head coil (though the head coil was upgraded at the same time as the dStream upgrade). Although not part of AOMIC, a separate dataset (dStreamUpgrade) with raw and preprocessed data (DWI, T1-weighted, and both resting-state and task-based functional MRI scans) acquired before and after the dStream upgrade using the same sequences and participants in both sessions is available on OpenNeuro^{15}. In addition, unthresholded group-level temporal signal-to-noise ratio (tSNR) maps and group-level GLM maps (for both the pre-upgrade and post-upgrade data as well as the post-pre difference) are available on NeuroVault^{16}.

At the start of each scan session, a low resolution survey scan was made, which was used to determine the location of the field-of-view. For all structural (T1-weighted), fieldmap (phase-difference based B0 map), and diffusion (DWI) scans, the slice stack was not angled. This was also the case for the functional MRI scans of ID1000 and PIOP1, but for PIOP2 the slice stack for functional MRI scans was angled such that the eyes were excluded as much as possible in order to reduce signal dropout in the orbitofrontal cortex. While the set of scans acquired for each study is relatively consistent (i.e. at least one T1-weighted anatomical scan, at least one diffusion-weighted scan, and at least one functional BOLD MRI scan), the parameters for a given scan vary slightly between the three studies. Notably, the functional MRI data from the resting-state and faces tasks from PIOP1 were acquired with multi-slice acceleration (factor 3; referred to in the current article as “multiband” acquisition), while all other functional MRI scans, including those from ID1000 and PIOP2, were acquired without multi-slice acceleration (referred to in the current article as “sequential” acquisition). The reason for reverting to sequential (instead of multiband) acquisition of the resting-state scan in PIOP2 is that we did not think the reduction in tSNR observed in multiband scans outweighs the increase in number of volumes. In Online-only Table 1, the parameters for the different types of scans across all three studies are listed.

During functional MRI scans, additional physiological data was recorded. Respiratory traces were recorded using a respiratory belt (air filled cushion) bound on top of the subject's diaphragm using a velcro band. Cardiac traces were recorded using a plethysmograph attached to the subject's left ring finger. Data was transferred to the scanner PC as plain-text files (Philips “SCANPHYSLOG” files) using a wireless recorder with a sampling frequency of 496 Hz.

Experimental paradigms for the functional MRI runs were shown on a 61 × 36 cm screen using a DLP projector with a 60 Hz refresh rate (ID1000 and PIOP1) or on a Cambridge Electronics BOLDscreen 32 IPS LCD screen with a 120 Hz refresh rate (PIOP2), both placed at 113 cm distance from the mirror mounted on top of the head coil. Sound was presented via a MRConfon sound system. Experimental tasks were programmed using Neurobs Presentation (Neurobehavioral Systems Inc, Berkeley, U.S.A.) and run on a Windows computer with a dedicated graphics card. To allow subject responses in experimental tasks (PIOP1 and PIOP2 only), participants used MRI-compatible fibre optic response pads with four buttons for each hand (Cambridge Research Systems, Rochester, United Kingdom).

### ID1000 specifics

In this section, we describe the subject recruitment, subject characteristics, data collection protocol, functional MRI paradigm, and previous analyses of the ID1000 study.

### Subjects

The data from the ID1000 sample was collected between 2010 and 2012. The faculty's ethical committee approved this study before data collection started (EC number: 2010-BC-1345). Potential subjects were a priori excluded from participation if they did not pass a safety checklist with MRI contraindications. We recorded data from 992 subjects of which 928 are included in the dataset (see “Technical validation” for details on the post-hoc exclusion procedure). Subjects were recruited through a recruitment agency (Motivaction International B.V.) in an effort to get a sample that was representative of the general Dutch population in terms of educational level (as defined by the Dutch government^{17}), but drawn from only a limited age range (19 to 26). We chose this limited age range to minimize the effect of aging on any brain-related covariates. A more detailed description of educational level and other demographic variables can be found in the section “Subject variables”.

### Data collection protocol

Prior to the experiment, subjects were informed about the goal and scope of the research, the MRI procedure, safety measures, general experimental procedures, privacy and data sharing concerns, and voluntary nature of the project (i.e. subjects were told that they could stop with the experiment at any time, without giving a reason for it). Before coming to the scan center, subjects also completed a questionnaire on background information (to determine educational level, which was used to draw a representative sample). If participants were invited they provided informed consent and completed an MRI screening checklist. Subjects then completed an extensive set of questionnaires and tests, including a general demographics questionnaire, the Intelligence Structure Test^{18,19}, the “trait” part of the State-Trait Anxiety Inventory (STAI)^{20}, a behavioral avoidance/inhibition questionnaire (BIS/BAS)^{21,22}, multiple personality questionnaires — amongst them the MPQ^{23} and the NEO-FFI^{24,25} and several behavioral tasks. The psychometric variables of the tests included in the current dataset are described in the section “Psychometric variables”.

Testing took place from 9 AM until 4 PM and on each day two subjects were tested. One subject began with the IST intelligence test, while the other subject started with the imaging part of the experiment. For the MRI part, we recorded three T1-weighted scans, three diffusion-weighted scans, and one functional (BOLD) MRI scan (in that order). The scanning session lasted approximately 60 minutes. Afterwards, the subjects switched and completed the other part. After these initial tasks, the subjects participated in additional experimental tasks, some of which have been reported in other publications^{26,27} and are not included in this dataset.

---

### Functional MRI paradigm

During functional MRI acquisition, subjects viewed a movie clip consisting of a (continuous) compilation of 22 natural scenes taken from the movie Koyaanisqatsi^{28} with music composed by Philip Glass. The scenes were selected because they broadly sample a set of visual parameters (textures and objects with different sizes and different rates of movement). Importantly, the focus on variation of visual parameters means, in this case, that the movie lacks a narrative and thus may be inappropriate to investigate semantic or other high-level processes.

The scenes varied in length from approximately 5 to 40 seconds with “cross dissolve” transitions between scenes. The movie clip extended 16 degrees visual angle (resolution 720 × 576, movie frame rate of 25 Hz). The onset of the movie clip was triggered by the first volume of the fMRI acquisition and had a duration of 11 minutes (which is slightly longer than the fMRI scan, i.e. 10 minutes and 38 seconds). The movie clip is available in the “stimuli” subdirectory of the ID1000 dataset (with the filename task-moviewatching_desc-koyaanisqatsi_movie.mp4).

### Previous analyses

The MRI data of ID1000 has been analyzed previously by two studies. One study^{4} analyzed the functional MRI data of a subset of 20 subjects by relating features from computational models applied to the movie data to the voxelwise time series using representational similarity analysis. Another study^{5} analyzed the relationship between autistic traits and voxel-based morphometry (VBM, derived from the T1-weighted scans) as well as fractional anisotropy (FA, derived from the DWI scans) in a subset of 508 subjects.

### PIOP1 and PIOP2 specifics

In this section, we describe the subject recruitment, subject characteristics, data collection protocol, functional MRI paradigms, and previous analyses of the PIOP1 and PIOP2 studies. These two studies are described in a common section because their data collection protocols were very similar. Information provided in this section (including sample characteristics, sample procedure, data acquisition procedure and scan sequences) can be assumed to apply to both PIOP1 and PIOP2, unless explicitly stated otherwise. As such, these datasets can be used as train/test (or validation) partitions. The last subsection (Differences between PIOP1 and PIOP2) describes the main differences between the two PIOP datasets.

### Subjects

Data from the PIOP1 dataset were collected between May 2015 and April 2016 and data from the PIOP2 dataset between March 2017 and July 2017. The faculty's ethical committee approved these studies before data collection started (PIOP1 EC number: 2015-EXT-4366, PIOP2 EC number: 2017-EXT-7568). Potential subjects were a priori excluded from participation if they did not pass a safety checklist with MRI contraindications. Data was recorded from 248 subjects (PIOP1) and 242 subjects (PIOP2), of which 216 (PIOP1) and 226 (PIOP2) are included in AOMIC (see “Technical validation” for details on the post-hoc exclusion procedure). Subjects from both PIOP1 and PIOP2 were all university students (from the Amsterdam University of Applied Sciences or the University of Amsterdam) recruited through the University websites, posters placed around the university grounds, and Facebook. A description of demographic and other subject-specific variables can be found in the section “Subject variables”.

### Data collection protocol

Prior to the research, subjects were informed about the goal of the study, the MRI procedure and safety, general experimental procedure, privacy and data sharing issues, and the voluntary nature of participation through an information letter. Each testing day (which took place from 8.30 AM until 1 PM), four subjects were tested. First, all subjects filled in an informed consent form and completed an MRI screening checklist. Then, two subjects started with the MRI part of the experiment, while the other two completed the demographic and psychometric questionnaires (described below) as well as several tasks that are not included in AOMIC.

The MRI session included a survey scan, followed by a T1-weighted anatomical scan. Then, several functional MRI runs (described below) and a single diffusion-weighted scan were recorded. Details about the scan parameters can be found in Online-only Table 1. The scan session lasted approximately 60 minutes. The scans were always recorded in the same order. For PIOP1, this was the following: faces (fMRI), gender-stroop (fMRI), T1-weighted scan, emotion matching (fMRI), resting-state (fMRI), phase-difference fieldmap (B0) scan, DWI scan, working memory (fMRI), emotion anticipation (fMRI). For PIOP2, this was the following: T1-weighted scan, working memory (fMRI), resting-state (fMRI), DWI scan, stop signal (fMRI), emotion matching (fMRI).

### Functional MRI paradigms

In this section, we will describe the experimental paradigms used during fMRI acquisition. See Fig. 2 for a visual representation of each paradigm. None of the designs were optimized for efficiency, except for the emotion anticipation task (which was optimized for efficiency to estimate the effect of each condition). All paradigms during functional MRI were started and synced to the functional MRI acquisition using a transistor-transistor logic (TTL) pulse sent to the stimulus presentation computer.

Emotion matching (PIOP1 + 2). The goal of the “emotion matching” task is to measure processes related to (facial) emotion processing. The paradigm we used was based on ref.^{29}. Trials were presented using a blocked design. In each trial, subjects were presented with either color images of an emotional target face (top) and two emotional probe faces (bottom left and bottom right; “emotion” condition) or a target oval (top) and two probe ovals (bottom left and bottom right; “control” condition) on top of a gray background (RGB: 248, 248, 248) and were instructed to either match the emotional expression of the target face (“emotion” condition) or the orientation or the target oval (“control” condition) as quickly as possible by pushing a button with the index finger of their left or right hand. The target and probes disappeared when the subject responded (or after 4.8 seconds). A new trial always appeared 5 seconds after the onset of each trial. In between the subject's response and the new trial, a blank screen was shown. Trials were presented in alternating “control” and “emotion” blocks consisting of six stimuli of 5 seconds each (four blocks each, i.e. 48 stimuli in total). Stimuli always belonged to the same block,

---

www.nature.com/scientificdata/

![img-1.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-2.jpg)
Emotion matching

![img-2.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-3.jpg)
Gender-stroop

![img-3.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-4.jpg)
Working memory

![img-4.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-5.jpg)

![img-5.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-6.jpg)
Fig. 2 A visual representation of all experimental paradigms during task-based fMRI. ISI: inter-stimulus interval.

but the order of stimuli within blocks was randomized across participants. The task took 270 seconds in total (i.e., 135 volumes with a 2 second TR).

The faces always displayed either stereotypical anger or fear. Within trials, always exactly two faces portrayed the same expression. Both male and female faces and white, black, and Asian faces were used, but within a single trial, faces were always of the same sex and ethnicity category (white or Asian/black). Face pictures were derived from the NimStim Face Stimulus set $^{30}$ . The oval stimuli were created by pixelating the face stimuli and were approximately the same area as the face stimuli (making them color and size matched to the face stimuli) and were either presented horizontally (i.e., the long side was horizontally aligned) or vertically (i.e., the long side was vertically aligned). Within trials, always exactly two ovals were aligned in the same way.

The fMRI "event files" (with the identifier_events) associated with this task contain information of the trial onset (the moment the faces/ovals appeared on screen, in seconds), duration (how long the faces/ovals were presented, in seconds), trial type (either "control" or "emotion"), response time (how long it took the subject to respond, logged "n/a" in case of no response), response hand (either "left", "right", or "n/a" in case of no response), response accuracy (either "correct", "incorrect", or "miss"), orientation to match (either "horizontal", "vertical", or "n/a" in case of emotion trials), emotion match (either "fear", "anger", or "n/a" in case of control trials), gender

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

of the faces (either “male”, “female”, of “n/a” in case of control trials), and ethnicity of the target and probe faces (either “caucasian”, “asian”, “black”, or “n/a” in case of control trials).

Working memory task (PIOP1 + 2). The goal of the working memory task was to measure processes related to visual working memory. The paradigm we used was based on ref.^{31}. Trials were presented using a fixed event-related design, in which trial order was the same for each subject. Trials belonged to one of three conditions: “active (change)”, “active (no change)”, or “passive”. Each trial consisted of six phases: an alert phase (1 second), an encoding phase (1 second), a retention phase (2 seconds), a test phase (1 second), a response phase (1 second), and an inter-stimulus interval (0--4 seconds). Subjects were instructed to keep focusing on the fixation target, which was shown throughout the entire trial, and completed a set of practice trials before the start of the actual task. The task took 324 seconds in total (i.e. 162 volumes with a 2 second TR).

In all trial types, trials started with an alert phase: a change of color of the fixation sign (a white plus sign changing to green, RGB [0, 255, 0]), lasting for 1 second. In the encoding phase, for “active” trials, an array of six white bars with a size of 2 degrees visual angle with a random orientation (either 0, 45, 90, or 135 degrees) arranged in a circle was presented for 1 second. This phase of the trial coincided with a change in background luminance from black (RGB: [0, 0, 0]) to gray (RGB: [120, 120, 120]). For “passive” trials, only the background luminance changed (but no bars appeared) in the encoding phase. In the subsequent retention phase, for all trial types, a fixation cross was shown and the background changed back to black, lasting 2 seconds. In the test phase, one single randomly chosen bar appeared (at one of the six locations from the encoding phase) which either matched the original orientation (for “active (no change)” trials) or did not match the original orientation (for “active (change)” trials), lasting for 1 second on a gray background. For “passive” trials, the background luminance changed and, instead of a bar, the cue “respond left” or “respond right” was shown in the test phase. In the response phase, lasting 1 second, the background changed back to black and, for “active” trials, subjects had to respond whether the array changed (button press with right index finger) or did not change (button press with left index finger). For “passive” trials, subjects had to respond with the hand that was cued in the test phase. In the inter-stimulus interval (which varied from 0 to 4 seconds), only a black background with a fixation sign was shown.

In total, there were 8 “passive” trials, 16 “active (change)” and “active (no change)” trials, in addition to 20 “null” trials of 6 seconds (which are equivalent to an additional inter-stimulus interval of 6 seconds). The sequence trials was, in terms of conditions (active, passive, null) exactly the same for all participations in both PIOP1 and PIOP2, but which bar or cue was shown in the test phase was chosen randomly.

The fMRI event files associated with this task contain information of the trial onset (the moment when the alert phase started, in seconds), duration (from the alert phase up to and including the response phase, i.e. always 6 seconds), trial type (either “active (change)”, “active (no change)”, or “passive”; “null” trials were not logged), response time (how long it took the subject to respond, “n/a” in case of no response), response hand (either “left”, “right”, or “n/a” in case of no response), and response accuracy (either “correct”, “incorrect”, or “miss”). Note that, in order to model the response to one or more phases of the trial, the onsets and durations should be adjusted accordingly (e.g. to model the response to the retention phase, add 2 seconds to all onsets and change the duration to 2 seconds).

Resting state (PIOP1 + 2). During the resting state scans, participants were instructed to keep their gaze fixated on a fixation cross in the middle of the screen with a gray background (RGB: [150, 150, 150]) and to let their thoughts run freely. Eyetracking data was recorded during this scan but is not included in this dataset. The resting state scans lasted 6 minutes (PIOP1; i.e. 480 volumes with a 0.75 second TR) and 8 minutes (PIOP2; i.e. 240 volumes with a 2 second TR).

Face perception (PIOP1). The face perception task was included to measure processes related to (emotional) facial expression perception. Trials were presented using an event-related design, in which trial order was randomized per subject. In each trial, subjects passively viewed dynamic facial expressions (i.e. short video clips) taken from the Amsterdam Facial Expression Set (ADFES)^{32}, which displayed either anger, contempt, joy, or pride, or no expression (“neutral”). Each clip depicted a facial movement from rest to a full expression corresponding to one of the four emotions, except for “neutral” faces, which depicted no facial movement. All clips lasted 2 seconds and contained either North-European or Mediterranean models, all of whom were female. After each video, a fixed inter-stimulus interval of 5 seconds followed. Each emotional facial expression (including “neutral”) was shown 6 times (with different people showing the expression each time), except for one, which was shown 9 times. Which emotional expression (or “neutral”) was shown an extra three times was determined randomly for each subject. Importantly, the three extra presentations always contained the same actor and were always presented as the first three trials. This was done in order to make it possible to evaluate the possible effects of stimulus repetition. The task took 247.5 seconds in total (i.e. 330 volumes with a 0.75 second TR).

The fMRI event files associated with this task contain information of the trial onset (the moment when the clip appeared on screen, in seconds), duration (of the clip, i.e. always 2 seconds), trial type (either “anger”, “joy”, “contempt”, “pride”, or “neutral”), sex of the model (all “female”), ethnicity of the model (either “North-European” or “Mediterranean”), and the ADFES ID of the model.

Gender-stroop task (PIOP1 only). The goal of the gender-stroop task was to measure processes related to cognitive conflict and control^{33} (see also ref.^{8} for an investigation of these processes using the PIOP1 gender-stroop data). We used the face-gender variant of the Stroop task (which was adapted from ref.^{34}), often referred to as the “gender-stroop” task. In this task, pictures of twelve different male and twelve different female faces are paired with the corresponding (i.e. congruent) or opposite (i.e. incongruent) label. For the labels, we used the Dut

---

words for “man”, “sir”, “woman”, and “lady” using either lower or upper case letters. The labels were located just above the head of the face. Trials were presented using an event-related design, in which trial order was randomized per subject. The task took 490 seconds in total (i.e. 245 volumes with a 2 second TR).

On each trial, subjects were shown a face-label composite on top of a gray background (RGB: [105, 105, 105]) for 0.5 seconds, which was either “congruent” (same face and label gender) or “incongruent” (different face and label gender). Stimulus presentation was followed by an inter-stimulus interval ranging between 4 and 6 seconds (in steps of 0.5 seconds). Subjects were always instructed to respond to the gender of the pictured face, ignoring the distractor word, as fast as possible using their left index finger (for male faces) or right index finger (for female faces). There were 48 stimuli for each condition (“congruent” and “incongruent”).

The fMRI event files associated with this task contain information of the trial onset (the moment when the face-label composite appeared on screen, in seconds), duration (of the face-label composite, i.e. always 0.5 seconds), trial type (either “incongruent” or “congruent”), gender of the face (either “male or “female”), gender of the word (either “male” or “female”), response time (in seconds), response hand (either “left”, “right”, or “n/a” in case of no response), response accuracy (either “correct”, “incorrect”, or “miss”).

Emotion anticipation task (PIOP1 only). We included the emotion anticipation task to measure processes related to (emotional) anticipation and curiosity. The paradigm was based on paradigms previously used to investigate (morbid) curiosity^{35,36}. Trials were presented using an event-related design, in which trial order was randomized per subject. In this task, subjects viewed a series of trials containing a cue and an image. The cue could either signal an 80% chance of being followed by a negatively valenced image (and a 20% chance of a neutral image) or an 80% chance of being followed by a neutral image (and a 20% change of a negatively valenced image). The cue was shown on top of a black background for 2 seconds, followed by a fixed interval of 3 seconds. After this interval, either a negative or neutral image was shown for 3 seconds, with a frequency that corresponds to the previously shown cue. In other words, for all trials with, for example, a cue signalling an 80% chance of being followed by a neutral image, it was in fact followed by a neutral image in 80% of the times. After the image, a fixed inter-stimulus interval of five seconds followed. In total, 15 unique negative images and 15 unique neutral images were shown, of which 80% (i.e. 12 trials) was preceded by a “valid” cue. Which stimuli were paired with valid or invalid cues was determined randomly for each subject. The order of the trials, given the four possible combinations (valid cue + negative image, invalid cue + negative image, valid cue + neutral image, invalid cue + neutral image), was drawn randomly from one of four possible sequences, which were generated using OptSeq (https://surfer.nmr.mgh.harvard.edu/optseq/) to optimize the chance of finding a significant interaction between cue type and image valence. The task took 400 seconds in total (i.e. 200 volumes with a 2 second TR).

The cue was implemented as a pie chart with the probability of a neutral image in blue and the probability of the negative image in red with the corresponding labels and probabilities (e.g. “negative 20%”) superimposed for clarity. The images were selected from the IAPS database^{37} and contained images of mutilation, violence, and death (negative condition) and of people in neutral situations (neutral condition).

The fMRI event files associated with this task contain information on the trial onset (the moment when either the cue or image appeared on the screen, in seconds), duration (of either the cue or image), and trial type. Trial type was logged separately for the cues (“negative”, indicating 80% probability of a negative image, and “neutral”, indicating 80% probability of a neutral image) and images (“negative” or “neutral”).

Stop-signal task (PIOP2 only). The stop-signal task was included to measure processes related to response inhibition. This specific implementation of the stop-signal paradigm was based on ref.^{38}. Trials were presented using an event-related design, in which trial order was randomized per subject. Subjects were presented with trials (n = 100) in which an image of either a female or male face (chosen from 9 exemplars) was shown for 500 ms on a black background. Subjects had to respond whether the face was female (right index finger) or male (left index finger) as quickly and accurately as possible, except when an auditory stop signal (a tone at 450 Hz for 0.5 seconds) was presented (on average 33% of the trials). The delay in presentation of the stop signal (i.e. the “stop signal delay”) was at start of the experiment 250 milliseconds, but was shortened with 50 ms if stop performance, up to that point, was better than 50% accuracy and shortened with 50 ms if it was worse. Each trial had a duration of 4000 ms and was preceded by a jitter interval (0, 500, 1000 or 1500 ms). If subjects responded too slow, or failed to respond an additional feedback trial of 2000 ms was presented. Additionally 10% (on average) null trials with a duration of 4000 ms were presented randomly. Note that due to this additional feedback trial and the fact that subjects differed in how many feedback trials they received, the fMRI runs associated with this task differ in length across subjects (i.e. the scan was manually stopped after 100 trials; minimum: 210 volumes, maximum: 250 volumes, median: 224 volumes, corresponding to a duration of 448 seconds with a 2 second TR).

The fMRI event files associated with this task contain information on the trial onset (the moment when a face was presented, in seconds), duration (always 0.5083 seconds), trial type (go, succesful_stop, unsuccesful_stop), if and when a stop signal was given (in seconds after stimulus onset), if and when a response time was given (in seconds after stimulus onset), response of the subject (left, right), and the sex of the image (male, female).

### Previous analyses

The PIOP1 data has been previously analyzed by three studies. One methodological study^{6} used the T1-weighted data (VBM, specifically) and DWI data (tract-based spatial statistics, TBSS, specifically) and the self-reported biological sex of subjects to empirically test an approach to correct for confounds in decoding analyses of neuroimaging data. Two other studies analyzed the participants' religiosity scores. One study^{7} performed a voxelwise VBM analysis on the religiosity scores while the other study^{8} related the religiosity data to the incongruent - congruent activity differences from the gender-stroop functional MRI data. Notably, both studies were pre-registered. There have been no (published) analyses on the PIOP2 data.

---

www.nature.com/scientificdata/

|  | % by biological sex | Mean age (sd; range) | % per education level/category |
| --- | --- | --- | --- |
| ID1000 | M: 47%, F: 52% | 22.85 (1.71; 19–26) | Low: 10%, Medium: 43%, High: 43% |
| PIOP1 | M: 41.2%, F: 55.6% | 22.18 (1.80; 18.25–26.25) | Applied: 56.5%, Academic: 43.5% |
| PIOP2 | M: 42.5%, F: 57.0% | 21.96 (1.79; 18.25–25.75) | Applied: 53%, Academic: 46% |

Table 2. Descriptive statistics for biological sex, age, and education level for all three datasets.

Differences between PIOP1 and PIOP2. One important difference between PIOP1 and PIOP2 is that they are not the same in terms of task-based functional MRI they acquired. Specifically, the "emotion anticipation", "faces", and "gender stroop" tasks were only acquired in PIOP1 and the "stop signal" task was only acquired in PIOP2 (see Table 1). In terms of scan sequences, the only notable difference between PIOP1 and PIOP2 is that the resting-state functional MRI scan in PIOP1 was acquired with multiband factor 3 (resulting in a TR of  $750~\mathrm{ms}$ ) while the resting-state functional MRI scan in PIOP2 was acquired without multiband (i.e., with a sequential acquisition, resulting in a TR of  $2000~\mathrm{ms}$ ; see Online-only Table 1). Additionally, because PIOP1 was acquired before the dStream upgrade and PIOP2 after the upgrade, the PIOP1 data generally has a lower tSNR but this does not seem to lead to substantial differences in effects (see "Technical Validation").

Subject variables (all datasets). In AOMIC, several demographic and other subject-specific variables are included per dataset. Below, we describe all variables in turn. Importantly, all subject variables and psychometric variables are stored in the participants.tsv file in each study's data repository. Note that missing data in this file is coded as "n/a". In Online-only Table 2, all variables and associated descriptions are listed for convenience.

Age. We asked subjects for their date of birth at the time they participated. From this, we computed their age rounded to the nearest quartile (for privacy reasons). See Table 2 for descriptive statistics of this variable.

Biological sex and gender identity. In all three studies, we asked subjects for their biological sex (of which the options were either male or female). For the ID1000 dataset, after the first 400 subjects, we additionally asked to what degree subjects felt male and to what degree they felt female (i.e., gender identity; separate questions, 7 point likert scale,  $1 = \text{not at all}$ ,  $7 = \text{strong}$ ). The exact question in Dutch was: 'ik voel mij een man', 'ik voel mij een vrouw'. This resulted in  $0.3\%$  of subjects scoring opposite on gender identity compared to their biological sex and  $92\%$  of females and  $90\%$  of males scoring conformable with their sex.

Sexual orientation. For the ID1000 dataset, after the first 400 subjects, we additionally asked to what degree subjects were attracted to men and women (both on a 7 point likert scale,  $1 = \text{not at all}$ ,  $7 = \text{strong}$ ). The exact question in Dutch was: 'ik val op mannen' and 'ik val op vrouwen'.

Of the 278 subjects with a male sex  $7.6\%$  indicated to be attracted to men (score of 4 or higher), of the 276 subjects with a female sex  $7.2\%$  indicated to be attracted to women (score of 4 or higher). Of the 554 subjects who completed these questions  $0.4\%$  indicated not be attracted to either men or women and  $0.9\%$  indicated to be strongly attracted to both men and women.

BMI. Subjects were asked for (PIOP1 and PIOP2) or we measured (ID1000) subjects' height and weight on the day of testing, from which we calculated their body-mass-index (BMI), which we rounded to the nearest integer. Note that height and weight are not included in AOMIC (for privacy reasons), but BMI is.

Handedness. Subjects were asked for their dominant hand. In ID1000, the options were "left" and "right" (left: 102, right: 826). For PIOP1 and PIOP2 we also included the option "both" (PIOP1, left: 24, right: 180, ambidextrous: 5, n/a: 7; PIOP2, left: 22, right: 201, ambidextrous: 1, n/a: 2).

Educational level/category. Information about subjects' educational background is recorded differently for ID1000 and the PIOP datasets, so they are discussed separately. Importantly, while we included data on educational level for the ID1000 dataset, we only include data on educational category for the PIOP datasets because they contain little variance in terms of educational level.

Educational level (ID1000). As mentioned, for the ID1000 dataset we selected subjects based on their educational level in order to achieve a representative sample of the Dutch population (on that variable). We did this by asking for their highest completed educational level. In AOMIC, however, we report the educational level (three point scale: low, medium, high) on the basis of the completed or current level of education (which included the scenario in which the subject was still a student), which we believe reflects educational level for our relatively young (19-26 year old) population better. Note that this difference in criterion causes a substantial skew towards a higher educational level in our sample relative to the distribution of educational level in the Dutch population (see Table 3).

Educational category (PIOP1 + 2). Relative to ID1000, there is much less variance in educational level within the PIOP datasets as these datasets only contain data from university students. As such, we only report whether subjects were, at the time of testing, studying at the Amsterdam University of Applied Sciences (category: "applied") or at the University of Amsterdam (category: "academic").

Background socio-economic status (SES). In addition to reporting their own educational level, subjects also reported the educational level (see Table 3) of their parents and the family income in their primary household.

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

www.nature.com/scientificdata/

| Educational level | Population | Subjects | Father | Mother |
| --- | --- | --- | --- | --- |
| Low | 35% | 10% | 36% | 32% |
| Medium | 39% | 43% | 27% | 24% |
| High | 26% | 47% | 37% | 44% |

Table 3. Distribution of educational level in the Dutch population (in 2010) and in our ID1000 sample. The data from the education level of subjects' parents was used to compute background socio-economic status.

| Background SES | % of subjects |
| --- | --- |
| 2-3 | 16% |
| 3-4 | 26% |
| 4-5 | 28% |
| 5-6 | 19% |
| >6 | 11% |

Table 4. Distribution of background SES.

Based on this information, we determined subjects' background social economical status (SES) by adding the household income — defined on a three point scale (below modal income,  $25\%$ : 1, between modal and  $2 \times$  modal income,  $57\%$ : 2, above  $2 \times$  modal income,  $18\%$ : 3) — with the average educational level of the parents — defined on a three point scale (low: 1, medium: 2, high: 3). This revealed that, while the educational level of the subjects is somewhat skewed towards "high", SES is well distributed across the entire spectrum (see Table 4).

Religion (PIOP1 and ID1000 only). For both the PIOP1 and ID1000 datasets, we asked subjects whether they considered themselves religious, which we include as a variable for these datasets (recoded into the levels "yes" and "no"). Of the subjects that participated in the PIOP1 study  $18.0\%$  indicated to be religious, for the subjects in the ID1000 projects this was  $21.2\%$ . For the ID1000 dataset we also asked subjects if they were raised religiously  $(N = 319, 34.1\%)$  and to what degree religion played a daily role in their lives (in Dutch, "Ik ben dagelijks met mijn geloof bezig", 5 point likert scale,  $1 = \text{not at all applicable}$ ,  $5 = \text{very applicable}$ ).

Psychometric variables (all datasets). BIS/BAS (ID1000 only). The BIS/BAS scales are based on the idea that there are two general motivational systems underlying behavior and affect: a behavioral activation system (BAS) and a behavioral inhibition system (BIS). The scales of the BIS/BAS attempt to measure these systems[21]. The BAS is believed to measure a system that generates positive feedback while the BIS is activated by conditioned stimuli associated with punishment.

The BIS/BAS questionnaire consists of 20 items (4 point scale). The BIS scale consists of 7 items. The BAS scale consists of 13 items and contains three subscales, related to impulsivity (BAS-Fun, 4 items), reward responsiveness (BAS-Reward, 5 items) and the pursuit of rewarding goals (BAS-Drive, 4 items).

STAI-T (ID1000). We used the STAI $^{20,25}$  to measure trait anxiety (STAI-T). The questionnaire consists of two scales (20 questions each) that aim to measure the degree to which anxiety and fear are a trait and part of the current state of the subject; subjects only completed the trait part of the questionnaire, which we include in the ID1000 dataset.

NEO-FFI (all datasets). The NEO-FFI is a Big 5 personality questionnaire that consists of 60 items (12 per scale)[24,39]. It measures neuroticism ("NEO-N"), extraversion ("NEO-E"), openness to experience ("NEO-O"), agreeableness ("NEO-A"), and conscientiousness ("NEO-C"). Neuroticism is the opposite of emotional stability, central to this construct is nervousness and negative emotionality. Extraversion is the opposite of introversion, central to this construct is sociability — the enjoyment of others' company. Openness to experience is defined by having original, broad interests, and being open to ideas and values. Agreeableness is the opposite of antagonism. Central to this construct are trust, cooperation and dominance. Conscientiousness is the opposite of un-directedness. Adjectives associated with this construct are thorough, hard-working and energetic.

IST (ID1000 only). The Intelligence Structure Test (IST) $^{18,19}$  is an intelligence test measuring crystallized intelligence, fluid intelligence, and memory, through tests using verbal, numerical, and figural information. The test consists of 590 items. The three measures (crystallized intelligence, fluid intelligence, and memory) are strongly positively correlated (between  $r = 0.58$  and  $r = 0.68$ ) and the sum score of these values form the variable "total intelligence".

Raven's matrices (PIOP1+2). As a proxy for intelligence, subjects performed the 36 item version (set II) of the Raven's Advanced Progressive Matrices Test $^{40,41}$ . We included the sum-score (with a maximum score of 36) in the PIOP datasets.

Data standardization, preprocessing, and derivatives. In this section, we describe the data curation and standardization process as well as the preprocessing applied to the standardized data and the resulting

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

www.nature.com/scientificdata/

![img-6.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-7.jpg)
Fig. 3 Overview of the types of data and "derivatives" included in AOMIC and the software packages used to preprocess and analyze them.

"derivatives" (see Fig. 3 for a schematic overview). This section does not describe this process separately for each dataset, because they are largely identically standardized and (pre)processed. Exceptions to this will be explicitly mentioned. In this standardization process, we adhered to the guidelines outlined in the Brain Imaging Data Structure (BIDS, v1.2.2) $^{14}$ , both for the "raw" data as well as the derivatives (whenever BIDS guidelines exist for that data or derivative modality).

Raw data standardization. Before subjecting the data to any preprocessing pipeline, we converted the data to BIDS using the in-house developed package bidsify (see "Code availability" section for more details about the software used in the standardization process). The "BIDSification" process includes renaming of files according to BIDS convention, conversion from Philips PAR/REC format to compressed nifti, removal of facial characteristics from anatomical scans ("defacing"), and extraction of relevant metadata into JSON files.

The results from the standardization process were checked using the bids-validator software package, which revealed no validation errors. However, the validation process raised several warnings about possible issues with the datasets (as shown in the "BIDS validation" section in their OpenNeuro repositories), which we explain in turn.

First, all three datasets contain subjects with incomplete data (i.e., missing MRI or physiology data), which causes the "Not all subjects contain the same files" warning. Second, the bids-validator issues a warning that "[n] ot all subjects/sessions/runs have the same scanning parameters". One cause for this warning (in PIOP1 and PIOP2) is that the time to repetition (TR) parameter of some DWI scans varies slightly (PIOP1: min = 7382 ms, max = 7700, median = 7390; PIOP2: min = 7382, max = 7519, median = 7387), which is caused by acquiring the DWI data with the shortest possible TR (i.e., TR = "shortest" setting on Philips scanners; see Online-only Table 1). Because the shortest possible TR depends on the exact angle of the slice box, the actual TR varies slightly from scan to scan. Notably, this warning is absent for the ID1000 dataset, because the TR value in the nifti file header is incorrect (i.e., it is set to 1 for each scan). Like the DWI scans in PIOP1 and PIOP2, the DWI scans from ID1000 were acquired with the shortest possible TR, resulting in slightly different TRs from scan to scan (min = 6307, max = 6838, median = 6312). The correct TR values in seconds for each DWI scan in ID1000 was added to the dataset's participants.tsv file (with the column names "DWI_TR_run1", "DWI_TR_run2", and "DWI_TR_run3").

In addition, the functional MRI scans from ID1000 were cropped in the axial and coronal direction by conservatively removing axial slices with low signal intensity in order to save disk space, causing slightly different dimensions across participants. Finally, in PIOP2, the functional MRI scans from the stop-signal task differ in the exact number of volumes (min = 210, max = 250, median = 224) because the scan was stopped manually after the participant completed the task (which depended on their response times).

Anatomical and functional MRI preprocessing. Results included in this manuscript come from preprocessing performed using Fmriprep version 1.4.1 (RRID:SCR_{016216}) $^{42,43}$ , a Nipype based tool (RRID:SCR_{002502}) $^{44,45}$ . Each T1w (T1-weighted) volume was corrected for INU (intensity non-uniformity) using N4BiasFieldCorrection v2.1.0 $^{46}$  and skull-stripped using antsBrainExtraction.sh v2.1.0 (using the OASIS template). Brain surfaces were reconstructed using recon-all from FreeSurfer v6.0.1 (RRID:SCR_{001847}) $^{47}$ , and the brain mask estimated previously was refined with a custom variation of the method to reconcile ANTs-derived and FreeSurfer-derived segmentations of the cortical gray-matter of Mindboggle (RRID:SCR_{002438}) $^{48}$ . Spatial normalization to the ICBM 152 Nonlinear Asymmetrical template version 2009c (RRID:SCR_{008796}) $^{49}$  was performed through nonlinear registration with the antsRegistration tool of ANTs v2.1.0 (RRID:SCR_{004757}) $^{50}$ , using brain-extracted versions

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

of both T1w volume and template. Brain tissue segmentation of cerebrospinal fluid (CSF), white-matter (WM) and gray-matter (GM) was performed on the brain-extracted T1w using fast (FSL v5.0.9, RRID:SCR_{002823})^{31}.

Functional data was not slice-time corrected. Functional data was motion corrected using mcflirt (FSL v5.0.9)^{32} using the average volume after a first-pass motion correction procedure as the reference volume and normalized correlation as the image similarity cost function. “Fieldmap-less” distortion correction was performed by co-registering the functional image to the same-subject T1w image with intensity inverted^{53,54} constrained with an average fieldmap template^{55}, implemented with antsRegistration (ANTs). Note that this fieldmap-less method was used even for PIOP2, which contained a phase-difference (B0) fieldmap, because we observed that Fmriprep's fieldmap-based method led to notably less accurate unwarping than its fieldmap-less method.

Distortion-correction was followed by co-registration to the corresponding T1w using boundary-based registration^{56} with 6 degrees of freedom, using bbregister (FreeSurfer v6.0.1). Motion correcting transformations, field distortion correcting warp, BOLD-to-T1w transformation and T1w-to-template (MNI) warp were concatenated and applied in a single step using antsApplyTransforms (ANTs v2.1.0) using Lanczos interpolation.

Physiological noise regressors were extracted by applying CompCor^{57}. Principal components were estimated for the two CompCor variants: temporal (tCompCor) and anatomical (aCompCor). A mask to exclude signal with cortical origin was obtained by eroding the brain mask, ensuring it only contained subcortical structures. Six tCompCor components were then calculated including only the top 5% variable voxels within that subcortical mask. For aCompCor, six components were calculated within the intersection of the subcortical mask and the union of CSF and WM masks calculated in T1w space, after their projection to the native space of each functional run. Framewise displacement^{58} was calculated for each functional run using the implementation of Nipype.

Many internal operations of Fmriprep use Nilearn (RRID:SCR_{001362})^{59}, principally within the BOLD-processing workflow. For more details of the pipeline see https://fmriprep.readthedocs.io/en/1.4.1/workflows.html.

### Diffusion MRI (pre)processing

DWI scans were preprocessed using a custom pipeline combining tools from MRtrix3^{60} and FSL. Because we acquired multiple DWI scans per participant in the ID1000 study (but not in PIOP1 and PIOP2), we concatenated these files as well as the diffusion gradient table (bvecs) and b-value information (bvals) prior to preprocessing. Using MRtrix3, we denoised the diffusion-weighted data using dwidenoise^{61,62}, removed Gibbs ringing artifacts using mrdegibbs^{63}, and performed eddy current and motion correction using dwipreproc. Notably, dwipreproc is a wrapper around the GPU-accelerated (CUDA v9.1) FSL tool eddy^{64}. Within eddy, we used a quadratic first-level (-flm = quadratic) and linear second-level model (-slm = linear) and outlier replacement^{65} with default parameters (-repol). Then, we performed bias correction using dwibiascorrect (which is based on ANTs; v2.3.1), extracted a brain mask using dwi2mask^{66}, and corrected possible issues with the diffusion gradient table using dwigradcheck^{67}.

After preprocessing, using MRtrix3 tools, we fit a diffusion tensor model on the preprocessed diffusion-weighted data using weighted linear least squares (with 2 iterations) as implemented in dwi2tensor^{68}. From the estimated tensor image, a fractional anisotropy (FA) image was computed and a map with the first eigenvectors was extracted using tensor2metric. Finally, a population FA template was computed using population_template (using an affine and an additional non-linear registration).

The following files are included in the DWI derivatives: a binary brain mask, the preprocessed DWI data as well as preprocessed gradient table (bvec) and b-value (bval) files, outputs from the eddy correction procedure (for quality control purposes; see Technical validation section), the estimated parameters from the diffusion tensor model, the eigenvectors from the diffusion tensor model, and a fractional anisotropy scalar map computed from the eigenvectors. All files are named according to BIDS Extension Proposal 16 (BEP016: diffusion weighted imaging derivatives).

### Freesurfer morphological statistics

In addition to the complete Freesurfer directories containing the full surface reconstruction per participant, we provide a set of tab-separated values (TSV) files per participant with several morphological statistics per brain region for four different anatomical parcellations/segmentations. For cortical brain regions, we used two atlases shipped with Freesurfer: the Desikan-Killiany (aparc in Freesurfer terms)^{69} and Destrieux (aparc.a2009 in Freesurfer terms)^{70} atlases. For these parcellations, the included morphological statistics are volume in mm^{3}, area in mm^{2}, thickness in mm, and integrated rectified mean curvature in mm^{-1}. For subcortical and white matter brain regions, we used the results from the subcortical segmentation (aseg in Freesurfer terms) and white matter segmentation (wmparc in Freesurfer terms) done by Freesurfer. For these parcellations, the included morphological statistics are volume in mm^{3} and average signal intensity (arbitrary units). The statistics were extracted from the Freesurfer output directories using the Freesufer functions asegstats2table and aparcstats2table and further formatted using custom Python code. The TSV files (and accompanying JSON metadata files) are formatted according to BIDS Extension Proposal 11 (BEP011: structural preprocessing derivatives).

### Voxel-based morphology (VBM)

In addition to the Fmriprep-preprocessed anatomical T1-weighted scans, we also provide voxelwise gray matter volume maps estimated using voxel-based morphometry (VBM). We used a modified version of the FSL VBM pipeline (http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSLVBM)^{71}, an optimised VBM protocol^{72} carried out with FSL tools^{73}. We skipped the initial brain-extraction stage (fslvbm_{1}_bet) and segmentation stage (first part of fslvbm_{3}_proc) and instead used the probabilistic gray matter segmentation file (in native space) from Fmriprep (i.e. *label-GM_probseg.nii.gz files) directly. These files were registered to the MNI152 standard space using non-linear registration^{74}. The resulting images were averaged and flipped along the x-axis to create a left-right symmetric, study-specific grey matter template. Second, all native grey matter images were

---

www.nature.com/scientificdata/

|  | ID1000 | PIOP1 | PIOP2 |
| --- | --- | --- | --- |
| OpenNeuro URL | https://openneuro.org/datasets/ds003097 | https://openneuro.org/datasets/ds002785 | https://openneuro.org/datasets/ds002790 |
| Neurovault URL | https://neurovault.org/collections/7105/ | https://neurovault.org/collections/7103/ | https://neurovault.org/collections/7104/ |

Table 5. Data repositories for subject data (OpenNeuro) and group-level data (NeuroVault).

![img-7.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-8.jpg)
Fig. 4 Quality control metrics related to the T1-weighted scans. CNR: contrast-to-noise ratio;  $^{101}$  CJV: coefficient of joint variation  $^{102}$ , an index reflecting head motion and spatial inhomogeneity; EFC: entropy-focused criterion  $^{103}$ , an index reflecting head motion and ghosting; INU: intensity non-uniformity, an index of spatial inhomogeneity; WM2MAX: ratio of median white-matter intensity to the  $95\%$  percentile of all signal intensities; low values may lead to problems with tissue segmentation.

![img-8.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-9.jpg)
Fig. 5 Quality control metrics related to the functional (BOLD) MRI scans. SNR: signal-to-noise ratio, an index of signal quality; FD: framewise displacement $^{104}$ , an index of overall movement; GCOR: global correlation, an index of the presence of global signals $^{105}$ ; GSR: ghost-to-signal ratio, an index of ghosting along the phase-encoding axis.

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

www.nature.com/scientificdata/

![img-9.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-10.jpg)
Fig. 6 Average (across subjects and runs) temporal signal-to-noise (tSNR) maps of each type of functional (BOLD) MRI scan in each dataset. Unthresholded whole-brain tSNR maps are available on NeuroVault.

non-linearly registered to this study-specific template and "modulated" to correct for local expansion (or contraction) due to the non-linear component of the spatial transformation.

Physiological noise processing. Physiology files were converted to BIDS-compatible compressed TSV files using the scanphyslog2bids package (see Code availability). Each TSV file contains three columns: the first contains the cardiac trace, the second contains the respiratory trace, and the third contains the volume onset triggers (binary, where 1 represents a volume onset). Each TSV file is accompanied by a JSON metadata file with the same name, which contains information about the start time of the physiology recording relative to the onset of the first volume. Because the physiology recording always starts before the fMRI scan starts, the start time is always negative (e.g., a start time of  $-42.01$  means that the physiology recording started 42.01 seconds before the onset of the first volume). After conversion to BIDS, the estimated volume triggers and physiology traces were plotted, visually inspected for quality, and excluded if either of the physiology traces had missing data for more than ten seconds or if the volume triggers could not be estimated.

The physiology data was subsequently used to estimate fMRI-appropriate nuisance regressors using the TAPAS PhysIO package $^{74}$  (see Code availability). Using this package, we specifically estimated 18 "RETROICOR" regressors $^{76}$  based on a Fourier expansion of cardiac (order: 2) and respiratory (order: 3) phase and their first-order multiplicative terms (as defined in ref.  $^{77}$ ). In addition, we estimated a heart-rate variability (HRV) regressor by convolving the cardiac trace with a cardiac response function $^{78}$  and a respiratory volume by time (RVT) regressor by convolving the respiratory trace with a respiration response function $^{79}$ .

# Data Records

Data formats and types. In AOMIC, the majority of the data is stored in one of four formats. First, all volumetric (i.e., 3D or 4D) MRI data is stored in compressed "NIfTI" files (NIfTI-1 version; extension:.nii.gz). NIfTI files contain both the data and metadata (stored in the header) and can be loaded into all major neuroimaging analysis packages and programming languages using, e.g., the nibabel package for Python (https://nipy.org/nibabel), the oro.nifti package in R (https://cran.r-project.org/web/packages/oro.nifti), and natively in Matlab (version R2017b and higher). Second, surface (i.e., vertex-wise) MRI data is stored in "Gifti" files (https://www.nitrc.org/projects/gifti; extension:.gii). Like NIfTI files, Gifti files contain both data and metadata and can be loaded in several major neuroimaging software packages (including Freesurfer, FSL, AFNI, SPM, and Brain Voyager) and programming languages using, e.g., the nibabel package for Python and the gifti package for R (https://cran.rstudio.com/web/packages/gifti).

Third, data organized as tables (i.e., observations in rows and properties in columns), such as physiological data and task-fMRI event log files, are stored in tab-separated values (TSV) files, which contain column names as the first row. TSV files can be opened using spreadsheet software (such as Microsoft Excel or Libreoffice Calc)

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

www.nature.com/scientificdata/

# PIOP1

![img-10.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-11.jpg)
Emo. matching: emotion &gt; control

![img-11.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-12.jpg)
PIOP2

![img-12.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-13.jpg)
Working memory: active &gt; passive

![img-13.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-14.jpg)
Working memory: active &gt; passive

![img-14.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-15.jpg)
Gender-stroop: incorrect &gt; correct

![img-15.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-16.jpg)
Stop-signal: failed stop &gt; go

![img-16.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-17.jpg)
Anticipation: negative &gt; neutral

![img-17.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-18.jpg)

![img-18.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-19.jpg)
Faces: expressive &gt; neutral
Fig. 7 Results from task-specific group-level analyses. Brain maps show uncorrected effects  $(p &lt; 0.00001$ , two-sided) and were linearly interpolated for visualization in FSLeyes. Unthresholded whole-brain  $z$ -value maps are available on NeuroVault. Unthresholded whole-brain  $z$ -value maps are available on NeuroVault.

and read using most major programming languages. Fourth, (additional) metadata is stored as key-value pairs in plain-text JSON files. A small minority of data in AOMIC is stored using different file formats (such as hdf5 for composite transforms of MRI data and some Freesurfer files), but these are unlikely to be relevant for most users.

Apart from data formats, we can distinguish different data types within AOMIC. Following BIDS convention, data types are distinguished based on an "identifier" at the end of the file name (before the extension). For example, T1-weighted files (e.g., sub-0001_T1w.nit.gz) are distinguished by the _T1w identifier and event log files for task-based functional MRI data (e.g., sub-001_task-workingmemory_acq-seq_events.tsv) are distinguished by the _events identifier. All data types and associated identifiers within AOMIC are listed in Online-only Table 3.

Data repositories used. Data from AOMIC can be subdivided into two broad categories. The first category encompasses all subject-level data, both raw data and derivatives. The second category encompasses group-level aggregates of data, such as an average (across subjects) tSNR map or group-level task fMRI activation maps. Data from these two categories are stored in separate, dedicated repositories: subject-level data is stored on OpenNeuro (https://openneuro.org) $^{35}$  and the subject-aggregated data is stored on NeuroVault (https://neurovault.org) $^{36}$ . Data from each dataset — PIOP1, PIOP2, and ID1000 — are stored in separate repositories on OpenNeuro $^{40-42}$  and NeuroVault $^{43-45}$ . URLs to these repositories for all datasets can be found in Table 5. Apart from the option to download data using a web browser, we provide instructions to download the data programmatically on https://nilab-uva.github.io/AOMIC.github.io.

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

www.nature.com/scientificdata/

![img-19.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-20.jpg)
Fig. 8 Group-level dual regression results for the first four components of Smith and colleagues $^{30}$ . Unthresholded  $z$ -value maps are available on NeuroVault. Unthresholded whole-brain  $z$ -value maps are available on NeuroVault.

![img-20.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-21.jpg)
Fig. 9 Results from the voxelwise ISC analysis, arbitrarily thresholded at 0.1. An unthresholded whole-brain ISC map is available on NeuroVault.

Data anonymization. In curating this collection, we took several steps in ensuring the anonymity of participants. All measures were discussed with the data protection officer of the University of Amsterdam and the data steward of the department of psychology, who deemed the anonymized data to be in accordance with the European General Data Protection Regulation (GDPR).

First, all personally identifiable information (such as subjects' name, date of birth, and contact information) in all datasets were irreversibly destroyed. Second, using the pydeface software package $^{30}$ , we removed facial characteristics (mouth and nose) from all anatomical scans, i.e., the T1-weighted anatomical scans and (in PIOP2) magnitude and phase-difference images from the B0 fieldmap. The resulting defaced images were checked visually to confirm that the defacing succeeded. Third, the data files were checked for timestamps and removed when present. Lastly, we randomized the subject identifiers (sub-xxxx) for all files. In case participants might have remembered their subject number, they will not be able to look up their own data within our collection.

# Technical Validation

In this section, we describe the measures taken for quality control of the data. This is described per data type (e.g., anatomical T1-weighted images, DWI images, physiology, etc.), rather than per dataset, as the procedure for quality control per data type was largely identical across the datasets. Importantly, we take a conservative approach towards exclusion of data, i.e., we generally did not exclude data unless (1) it was corrupted by scanner-related incorrigible artifacts, such as reconstruction errors, (2) when preprocessing fails due to insufficient data quality (e.g., in case of strong spatial inhomogeneity of structural T1-weighted scans, preventing accurate segmentation), (3) an absence of a usable T1-weighted scan (which is necessary for most preprocessing pipelines), or (4) incidental findings. This way, the data from AOMIC can also be used to evaluate artifact-correction methods and other preprocessing techniques aimed to post-hoc improve data quality and, importantly, this places the responsibility for inclusion and exclusion of data in the hands of the users of the datasets.

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

www.nature.com/scientificdata/

![img-21.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-22.jpg)
Fig. 10 Quality control metrics related to the diffusion-weighted scans. FD: framewise displacement, Std EC: standard deviation of the linear terms of the eddy current distortions in  $\mathrm{Hz / mm}$ .

![img-22.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-23.jpg)

Researchers not interested in using AOMIC data for artifact-correction or preprocessing techniques may still want to exclude data that do not meet their quality standards. As such, we include, for each modality (T1-weighted, BOLD, and DWI) separately, a file with several quality control metrics across subjects. The quality control metrics for the T1-weighted and functional (BOLD) MRI scans were computed by the Mriqc package $^{47}$  and are stored in the group_T1w.tsv and group_T1w.tsv files in the mriqc derivative folder. The quality control metrics for the DWI scans were derived from the output of FSIs eddy algorithm and are stored in the group_dwi.tsv file in the dwipreproc derivative folder. Using these precomputed quality control metrics, researchers can decide which data to include based on their own quality criteria.

T1-weighted scans. All T1-weighted scans were run through the Mriqc pipeline, which outputs several quality control metrics as well as a report with visualizations of different aspects of the data. All individual subject reports were visually checked for artifacts including reconstruction errors, failure of defacing, normalization issues, and segmentation issues (and the corresponding data excluded when appropriate). In Fig. 4, we visualize several quality control metrics related to the T1-weighted scans across all three datasets. In general, data quality appears to increase over time (with ID1000 being the oldest dataset, followed by PIOP1 and PIOP2), presumably due to improvements in hardware (see "Scanner details and general scanning protocol"). All quality control metrics related to the T1-weighted scans, including those visualized in Fig. 4, are stored in the group_T1w.tsv file in the mriqc derivatives folder.

Functional (BOLD) scans. Like the T1-weighted images, the functional (BOLD) scans were run through the Mriqc pipeline. The resulting reports were visually checked for artifacts including reconstruction errors, registration issues, and incorrect brain masks.

In Fig. 5, we visualize several quality control metrics related to the functional scans across all three datasets. Similar to the T1-weighted quality control metrics, the functional quality control metrics indicate an improvement of quality over time. Also note the clear decrease in temporal signal-to-noise ratio (tSNR) for multiband-accelerated scans (consistent with ref.  $^{88}$ ). All quality control metrics related to the functional MRI scans, including those visualized in Fig. 5, are stored in the group bold.tsv file in the mriqc derivatives folder.

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

www.nature.com/scientificdata/

![img-23.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-24.jpg)
Fig. 11 Diffusion-encoded color images of the FA-modulated median DTI eigenvectors across subjects. Red colors denote preferential diffusion along the sagittal axis (left-right), green colors denote preferential diffusion along the coronal axis (anterior-posterior), and blue colors denote preferential diffusion along the axial axis (inferior-superior). Brighter colors denote stronger preferential diffusion.

In addition to global quality control metrics, we also computed whole-brain (voxelwise) tSNR maps, computed by dividing the average signal (across time) by the standard deviation of the signal (across time) of the motion-corrected and spatially normalized data. This is done for each subject and fMRI scan separately, which are subsequently averaged across subjects and scans (but separately for sequential and multiband-accelerated scans in PIOP1 to highlight the tSNR cost of multiband-acceleration).

In Fig. 6, we visualize these tSNR maps for each dataset (and separately for the sequential and multiband scans of PIOP1). Again, there appears to be an increase in tSNR across time. Corresponding whole-brain tSNR maps can be viewed and downloaded from NeuroVault (i.e., files with the _tsnr identifier).

For the fMRI data with an explicit task (i.e., all fMRI data except for the PIOP resting-state fMRI scans and the ID1000 movie watching fMRI scan), we additionally computed group-level whole-brain statistics maps. To do so, using the nistats Python package, we ran mass-univariate first-level GLS models (using an AR1 noise model) based on a design matrix including task-regressors based on the events convolved with a canonical HRF function as well as a discrete cosine basis set functioning as a high-pass filter of 128 seconds and six motion regressors and computed first-level contrast maps for each subject which were subsequently analyzed in a random effects group-level (intercept) model, resulting in whole-brain  $z$ -value maps. The data was never spatially smoothed. In Fig. 7, we show the (uncorrected) whole-brain group-level results for each task. Note that we chose these specific contrasts to demonstrate that the tasks elicit to-be expected effects (e.g., amygdala activity in the emotion matching task and cingulate cortex activity in the gender-stroop task). Different, and more sophisticated analyses, including analysis of between-subject factors, are possible with this data and the associated event files.

To validate the quality of the resting-state functional MRI scans in PIOP1 and PIOP2, we ran dual regression analyses $^{89}$  using the spatial ICA maps from Smith and colleagues (10-component version) $^{90}$ . Prior to the dual regression analyses, the data was cleaned and high-pass filtered (using a 128 second cutoff) by regressing out a discrete cosine basis set and six motion parameter estimates and spatially smoothed with a Gaussian kernel with a  $5\mathrm{mm}$  FWHM. Figure 8 shows the group-level dual regression results from both PIOP1 and PIOP2 for the first four components next to the original ICA map from Smith and colleagues $^{90}$ .

Finally, to assess the quality of the ID1000 functional MRI data, we performed a voxelwise whole-brain "inter-subject correlation" (ISC) analysis $^{91}$ , using the BrainIAK software package $^{92}$  on data from a subset of 100 participants (randomly drawn from the ID1000 dataset). Before computing the inter-subject correlations, the data were masked by an intersection of a functional brain mask and a grey matter mask (probability  $&gt;0.1$ ). Low-frequency drift (with a cutoff of 128 seconds), the mean signal within the cerebrospinal fluid, global (whole-brain average) signal, and six motion parameters were regressed out before computing the ISCs. The average (across subjects) voxelwise ISCs are visualized in Fig. 9, which shows the expected inter-subject synchrony in the ventral and dorsal visual stream. The emphasis on variance in visual parameters rather than narrative when composing the movie stimulus likely caused the high ISC values to be largely restricted to visual brain areas.

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

www.nature.com/scientificdata/

![img-24.jpeg](source_images/the-amsterdam-open-mri-collection-a-set-of-multimo-4f6760-fig-25.jpg)
ID1000
Fig. 12 Results from group-level physiology analyses. Brain maps show uncorrected effects (thresholded arbitrarily at  $z &gt; 6$ ) and were linearly interpolated for visualization in FSLeyes. Unthresholded whole-brain  $z$ -value maps are available on NeuroVault.

| IST (N = 926) | IST Int | IST Crystal | IST Memory | IST Fluid | Background SES | Education |
| --- | --- | --- | --- | --- | --- | --- |
| IST Int | 1 | 0.82** | 0.79** | 0.96** | 0.35** | 0.46** |
| IST Crystallized |  | 1 | 0.58** | 0.68** | 0.37** | 0.44** |
| IST Memory |  |  | 1 | 0.65** | 0.25** | 0.39** |
| IST Fluid |  |  |  | 1 | 0.31** | 0.41** |
| Background SES |  |  |  |  | 1 | 0.38** |
| Education |  |  |  |  |  | 1 |

Table 6. Correlations between total score, and subscales of the IST and relevant external variables (background SES and educational level). IST: Intelligence Structure Test, Int: Total Intelligence, SES: background social-economic status. ** indicates  $p &lt; {0.01}$  .

Diffusion-weighted scans. Before preprocessing, the  $b = 0$  volume from each DWI scan was extracted and visually checked for severe artifacts and reconstruction errors (in which case the data was excluded). After preprocessing and DTI model fitting, we furthermore visualized each estimated fractional anisotropy (FA) map and the color-coded FA-modulated (absolute) eigenvectors for issues with the gradient directions. These images are included in the DWI derivatives.

Furthermore, we extracted quality control metrics based on outputs from the eddy correction/motion correction procedure in the DWI preprocessing pipeline as implemented in FSL's eddy algorithm (based on the procedure outlined in ref. 93). Specifically, we computed the mean framewise displacement across volumes based on the realignment parameters from motion correction, the percentage of "outlier slices" (as determined by FSL eddy)

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

www.nature.com/scientificdata/

| ID1000 (n = 927) | Neuroticism | Extraversion | Openness | Agreeableness | Conscientiousness |
| --- | --- | --- | --- | --- | --- |
| Neuroticism | 1 | -0.30** | 0.15** | -0.08* | -0.43** |
| Extraversion |  | 1 | 0.20** | -0.13** | 0.12** |
| Openness |  |  | 1 | -0.06 | -0.19** |
| Agreeableness |  |  |  | 1 | 0.16** |
| Conscientiousness |  |  |  |  | 1 |
| PIOP1 (N = 216) | Neuroticism | Extraversion | Openness | Agreeableness | Conscientiousness |
| Neuroticism | 1 | -0.29** | 0.18** | 0.00 | -0.25** |
| Extraversion |  | 1 | -0.05 | 0.20** | 0.14* |
| Openness |  |  | 1 | 0.08 | -0.18** |
| Agreeableness |  |  |  | 1 | 0.20** |
| Conscientiousness |  |  |  |  | 1 |
| PIOP2 (N = 226) | Neuroticism | Extraversion | Openness | Agreeableness | Conscientiousness |
| Neuroticism | 1 | -0.38** | 0.12 | -0.07 | -0.24** |
| Extraversion |  | 1 | 0.11 | 0.26** | 0.25** |
| Openness |  |  | 1 | 0.02 | -0.04 |
| Agreeableness |  |  |  | 1 | 0.15* |
| Conscientiousness |  |  |  |  | 1 |

Table 7. Cross-correlations for the subscales of the NEO-FFI for the ID1000, PIOP1 and PIOP2 samples. With the exception of the correlation between agreeableness and extraversion the cross-correlation patterns are very similar across samples. *indicates p &lt; 0.05. **indicates p &lt; 0.01.

| BIS/BAS (N=928) | BAS drive | BAS fun | BAS reward | BIS |
| --- | --- | --- | --- | --- |
| BAS drive | 1 | 0.45** | 0.34** | -0.19** |
| BAS fun |  | 1 | 0.39** | -0.13** |
| BAS reward |  |  | 1 | 0.19** |
| BIS |  |  |  | 1 |

Table 8. Cross-correlations for the subscales of the BIS/BAS for the ID1000 sample. The pattern of correlations is consistent with that reported in literature.

in total and per volume, and the standard deviation of the estimated linear eddy current distortions across volumes. These metrics are visualized in Fig. 10. Note that the y-axis for the standard deviation of the eddy currents for ID1000 has a larger range than for PIOP1 and PIOP2 to show the scans with particularly strong eddy current fluctuations.

Finally, for each dataset, we transformed all preprocessed DTI eigenvectors to a population template estimated on all FA images using MRTrix' population_template (using a linear followed by a non-linear registration procedure) and computed the voxelwise median across subjects. The median eigenvector images are visualized in Fig. 11 as "diffusion-encoded color" (DEC) images, in which values are modulated by the associated FA values.

Physiological data. After conversion to BIDS, physiological data was visually checked for quality by plotting the scanner triggers (i.e., volume onsets) and the cardiac and respiratory traces. Files missing a substantial window of data ( $&gt;10$  seconds) were excluded as well as files for which the scanner triggers could not be estimated reliably. Figures of the physiology traces and scanner triggers for each file are included in the physiology derivatives. Additionally, using the same approach as described for the task-based technical validation analyses, we fit first-level (subject-specific) and subsequently group-level (subject-average) models using the physiology regressors (all 18 RETROICOR regressors, one HRV, and one RVT regressor) for each dataset. In Fig. 12, we visualize the effects of the different RETROICOR components (respiratory, cardiac, and interaction regressors; an  $F$ -test, but converted to and visualized as  $z$ -scores) and the HRV and RVT regressors (a  $t$ -test, but converted to and visualized as  $z$ -scores). Unthresholded whole-brain maps are available from NeuroVault.

Psychometric data. The patterns of correlations within the scales of the questionnaires are consistent with those reported in literature, indicating that this data is overall reliable. The pattern of correlations between scales of different questionnaires and external variables is also consistent with those reported in literature and what would be expected on theoretical grounds.

Intelligence Structure Test (IST). The subscales of the IST (fluid and crystallized intelligence and memory) are strongly correlated with each other. The validity of the measure data is supported by the correlation with relevant external variables like educational level,  $r(926) = 0.46$  and background SES,  $r(926) = 0.35$  (see Table 6).

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

### Personality: NEO-FFI

The cross-correlation patterns of the 5 NEO-FFI scales are depicted in Table 7. Significant correlations exist between the scales, and the correlation pattern is overall consistent with the reported norm data for this test^{24}. The correlation between cross-correlation patterns of the three datasets is very consistent (r = 0.88 between PIOP1 and PIOP2, and on average r = 0.74 between ID1000 and PIOP), with as a notable outlier a negative correlation, r(928) = -0.13, p < 0.001, between extraversion and agreeableness in the ID1000 dataset and a positive correlation for these scales in the PIOP1, r(216) = 0.20, p < 0.005, and PIOP2, r(226) = 0.26, p < 0.001. A source for this discrepancy could be the difference in population sample between the PIOP1 and PIOP2 studies and the ID1000 study.

In terms of external validity we note that openness to experience has a positive correlation with intelligence in all three samples (ID1000: r(925) = 0.22, p < 0.001, PIOP1: r(216) = 0.25, p = 0.000196), PIOP2: r(225) = 0.24, p = 0.000276).

### BIS/BAS

The cross-correlation patterns of the BIS/BAS scales are depicted in Table 8. The cross-correlation between the scales are similar to the one reported by Franken and colleagues^{22} and contrary to what Carver & White^{21} predicted, with a positive correlation between the three different BAS-scales, but also between BIS and BAS-Reward, r(927) = 0.194.

### STAI-T

The STAI-T scale measures trait anxiety. Because this instrument only consists of one scale we evaluate its reliability on the degree in which it shows correlations with other questionnaire scales that also have a pretension of measuring negative emotionality. Because we observe positive correlations with both Neuroticisms, r(927) = 0.77, p < 0.001) and BIS, r(927) = 0.514, p < 0.001) we conclude that the reported scales are reliable and consistent.

## Code availability

All code used for curating, annotating, and (pre)processing AOMIC are version-controlled using git and can be found in project-specific Github repositories within the NILAB-UvA Github organization: https://github.com/orgs/NILAB-UvA. Many pre and postprocessing steps were identical across datasets, so the code for these procedures is stored in a single repository: https://github.com/NILAB-UvA/AOMIC-common-scripts. Possible parameters are all hard-coded within the scripts, except for a single positional parameter pointing to the directory to be processed. For custom Python-based scripts, we used Python version 3.7. All code was developed on a Linux system with 56 CPUs (Intel Xeon E5-2680 v4, 2.40 GHz) and 126GB RAM running Ubuntu 16.04. All curation, preprocessing, and analyses were run on said Linux system, apart from the Fmriprep, MRIQC, and Freesurfer analyses, which were run in a Docker container provided by those software packages. Custom code was parallelized to run on multiple CPUs concurrently using the Python package joblib (https://joblib.readthedocs.io).

For curation, preprocessing, and analysis of the datasets, we used a combination of existing packages and custom scripts (written in Python or bash). To convert the data to the Brain Imaging Data Structure (BIDS), we used the in-house developed, publicly available software package bidsify (v0.3; https://github.com/NILAB-UvA/bidsify), which in turn uses the dcm2niix (v1.0.20181125)^{94} to convert the Philips PAR/REC files to compressed nifti files. In contrast to the data from PIOP1 and PIOP2 (which were converted to nifti using dcm2niix), r2aGUI (v2.7.0; http://r2agui.sourceforge.net/) was used to convert the data from ID1000. Because r2aGUI does not correct the gradient table of DWI scans for slice angulation, we used the angulation_correction_Achieva Matlab script (version December 29, 2007) from Jonathan Farrell to do so (available for posterity at https://github.com/NILAB-UvA/ID1000/blob/master/code/bidsify/DTI_gradient_table_ID1000.m). To remove facial characteristics from anatomical scans, we used the pydeface package (v.1.1.0)^{96}. Finally, to convert the raw physiology files (i.e. Philips “SCANPHYSLOG” files) to BIDS, we used the in-house developed, publicly available Python package scanphyslog2bids (v0.1; https://github.com/lukassnoek/scanphyslog2bids). The outputs from the BIDS-conversion pipeline were checked using the bids-validator software package (v1.4.3).

Anatomical and functional MRI preprocessing were done using Fmriprep (v1.4.1; see the Derivatives section for extensive information about Fmriprep's preprocessing pipeline)^{42}. For our DWI preprocessing pipeline, we used tools from the MRtrix3 package (www.mrtrix.org; v3.0_RC3)^{40} and FSL (v6.0.1)^{95}. For the VBM and dual regression pipelines, we used FSL (v6.0.1)^{71--73}. To create the files with Freesurfer-based metrics across all participants, we used Freesurfer version 6.0.0^{96}. Physiological nuisance regressors (RETROICOR and HRV/RVT regressors) were estimated using the TAPAS PhysIO Matlab package (v3.2.0)^{75}.

First-level functional MRI analyses for technical validation were implemented using the Python package nistats (v0.0.1b2)^{59} and nilearn (v0.6.2)^{59,97}. For the inter-subject correlation analysis the Brain Imaging Analysis Kit was used (BrainIAK, http://brainiak.org, v0.10; RRID:SCR_{014824})^{92}. Plotting brain images was done using FSLeyes (v0.32)^{98} and plotting statistical plots was done using the Python packages seaborn^{99} and Matplotlib^{100}.

Received: 4 December 2020; Accepted: 18 February 2021;Published online: 19 March 2021

---

www.nature.com/scientificdata/

5. Koolschijn, P. C. M. P., Geurts, H. M., van der Leij, A. R. &amp; Scholte, H. S. Are Autistic Traits in the General Population Related to Global and Regional Brain Differences? J. Autism Dev. Disord. 45, 2779-2791 (2015).
6. Snoek, L., Miletic, S. &amp; Scholte, H. S. How to control for confounds in decoding analyses of neuroimaging data. Neuroimage 184, 741-760 (2019).
7. van Elk, M. &amp; Snoek, L. The relationship between individual differences in gray matter volume and religiosity and mystical experiences: A preregistered voxel-based morphometry study. Eur. J. Neurosci. 51, 850-865 (2020).
8. Hoogeveen, S., Snoek, L. &amp; van Elk, M. Religious belief and cognitive conflict sensitivity: A preregistered fMRI study. Cortex 129, 247-265 (2020).
9. Nichols, T. E. et al. Best practices in data analysis and sharing in neuroimaging using MRI. Nat. Neurosci. 20, 299-303 (2017).
10. Miller, K. L. et al. Multimodal population brain imaging in the UK Biobank prospective epidemiological study. Nat. Neurosci. 19, 1523-1536 (2016).
11. Van Essen, D. C. et al. The WU-Minn Human Connectome Project: an overview. Neuroimage 80, 62-79 (2013).
12. Mendes, N. et al. A functional connectome phenotyping dataset including cognitive state and personality measures. Sci Data 6, 180307 (2019).
13. Babayan, A. et al. A mind-brain-body dataset of MRI, EEG, cognition, emotion, and peripheral physiology in young and old adults. Sci Data 6, 180308 (2019).
14. Gorgolewski, K. J. et al. The brain imaging data structure, a format for organizing and describing outputs of neuroimaging experiments. Sci Data 3, 160044 (2016).
15. Gorgolewski, K., Esteban, O., Schaefer, G., Wandell, B. &amp; Poldrack, R. OpenNeuro—a free online platform for sharing and analysis of neuroimaging data. Organization for Human Brain Mapping. Vancouver, Canada 1677 (2017).
16. Gorgolewski, K. J. et al. NeuroVault.org: a web-based repository for collecting and sharing unthresholded statistical maps of the human brain. Front. Neuroinform. 9, 8 (2015).
17. Onderwijsindeling, S. Standard Educational Classification. Den Haag/Heerlen, Netherlands: Centraal Bureau voor de Statistiek [Statistics Netherlands] (2016).
18. Vorst, H. Intelligentie Structuur Test (IST). (Hogrefe, 2010).
19. Amthauer, R., Brocke, B., Liepmann, D. &amp; Beauducel, A. Intelligenz-Struktur-Test 2000 R. vol. 2 (Hogrefe, 2001).
20. Spielberger, C. D., Gorsuch, R. L. &amp; Lushene, R. E. STAI Manual for the State-Trait Anxiety Inventory. (1970).
21. Carver, C. S. &amp; White, T. L. Behavioral inhibition, behavioral activation, and affective responses to impending reward and punishment: The BIS/BAS Scales. J. Pers. Soc. Psychol. 67, 319-333 (1994).
22. Franken, I. H. A., Muris, P. &amp; Rassin, E. Psychometric properties of the dutch BIS/BAS scales. J. Psychopathol. Behav. Assess. 27, 25-30 (2005).
23. Eigenhuis, A., Kamphuis, J. H. &amp; Noordhof, A. Development and validation of the Dutch brief form of the Multidimensional Personality Questionnaire (MPQ-BF-NL). Assessment 20, 565-575 (2013).
24. Hoekstra, H. A., Ormel, H. &amp; De Fruyt, F. Persoonlijkheidsvragenlijsten: NEO-PI-R &amp; NEO-FFI. (Swets &amp; Zeitlinger, 1996).
25. Van der Ploeg, H. M. Validity of the Zelf-Beordelings-Vragenlijst (A Dutch version of the Spielberger State-Trait Anxiety Inventory). Ned. Tijdschr. Psychol. 35, 243-249 (1980).
26. Gazendam, F. J. et al. Personality Predicts Individual Variation in Fear Learning: A Multilevel Growth Modeling Approach. Clin. Psychol. Sci. 3, 175-188 (2015).
27. Pinto, Y., van der Leij, A. R., Sligte, I. G., Lamme, V. A. F. &amp; Scholte, H. S. Bottom-up and top-down attention are independent. J. Vis. 13, 16 (2013).
28. Reggio, G. Koyaanisqatsi. (Institute for Regional Education/American Zoetrope, 1982).
29. Hariri, A. R., Bookheimer, S. Y. &amp; Mazziotta, J. C. Modulating emotional responses: effects of a neocortical network on the limbic system. Neuroreport 11, 43-48 (2000).
30. Tottenham, N. et al. The NimStim set of facial expressions: judgments from untrained research participants. *Psychiatry Res.* **168**, 242–249 (2009).
31. Pessoa, L., Gutierrez, E., Bandettini, P. &amp; Ungerleider, L. Neural correlates of visual working memory: fMRI amplitude predicts task performance. Neuron 35, 975-987 (2002).
32. van der Schalk, J., Hawk, S. T., Fischer, A. H. &amp; Doosje, B. Moving faces, looking places: validation of the Amsterdam Dynamic Facial Expression Set (ADFES). Emotion 11, 907-920 (2011).
33. Milham, M. P., Banich, M. T. &amp; Barad, V. Competition for priority in processing increases prefrontal cortex's involvement in top-down control: an event-related fMRI study of the stroop task. *Brain Res. Cogn. Brain Res.* 17, 212-222 (2003).
34. Egner, T., Ely, S. &amp; Grinband, J. Going, going, gone: characterizing the time-course of congruency sequence effects. Front. Psychol. 1, 154 (2010).
35. Oosterwijk, S. Choosing the negative: A behavioral demonstration of morbid curiosity. PLoS One 12, e0178399 (2017).
36. Oosterwijk, S., Snoek, L., Tekoppele, J., Engelbert, L. H. &amp; Scholte, H. S. Choosing to view morbid information involves reward circuitry. Sci. Rep. 10, 15291 (2020).
37. Lang, P. J., Bradley, M. M. &amp; Cuthbert, B. N. &amp; Others. International affective picture system (IAPS): Technical manual and affective ratings. NIMH Center for the Study of Emotion and Attention 1, 39-58 (1997).
38. Jahfari, S., Waldorp, L., Ridderinkhof, K. R. &amp; Scholte, H. S. Visual information shapes the dynamics of corticobasal ganglia pathways during response selection and inhibition. J. Cogn. Neurosci. 27, 1344-1359 (2015).
39. McCrae, R. R. &amp; Costa, P. T. Jr. Validation of the five-factor model of personality across instruments and observers. J. Pers. Soc. Psychol. 52, 81-90 (1987).
40. Raven, J., Court, J. H. &amp; Raven, J. C. Manual for Raven's progressive matrices and vocabulary scales. (1998).
41. Raven, J. The Raven's progressive matrices: change and stability over culture and time. Cogn. Psychol. 41, 1-48 (2000).
42. Esteban, O. et al. fMRIPrep: a robust preprocessing pipeline for functional MRI. Nat. Methods 16, 111-116 (2019).
43. Esteban, O. et al. Analysis of task-based functional MRI data preprocessed with fMRIPrep. Nat. Protoc. 15, 2186-2202 (2020).
44. Gorgolewski, K. J. et al. Nipype: a flexible, lightweight and extensible neuroimaging data processing framework in Python. 0.13.1. Zenodo https://doi.org/10.5281/zenodo.581704 (2017).
45. Gorgolewski, K. et al. Nipype: a flexible, lightweight and extensible neuroimaging data processing framework in python. Front. Neuroinform. 5, 13 (2011).
46. Tustison, N. J. et al. N4ITK: improved N3 bias correction. IEEE Trans. Med. Imaging 29, 1310-1320 (2010).
47. Dale, A. M., Fischl, B. &amp; Sereno, M. I. Cortical surface-based analysis. I. Segmentation and surface reconstruction. Neuroimage 9, 179-194 (1999).
48. Klein, A. et al. Mindboggling morphometry of human brains. PLoS Comput. Biol. 13, e1005350 (2017).
49. Fonov, V. S., Evans, A. C., McKinstry, R. C., Almli, C. R. &amp; Collins, D. L. Unbiased nonlinear average age-appropriate brain templates from birth to adulthood. Neuroimage Supplement 1, S102 (2009).
50. Avants, B. B., Epstein, C. L., Grossman, M. &amp; Gee, J. C. Symmetric diffeomorphic image registration with cross-correlation: evaluating automated labeling of elderly and neurodegenerative brain. Med. Image Anal. 12, 26-41 (2008).
51. Zhang, Y., Brady, M. &amp; Smith, S. Segmentation of brain MR images through a hidden Markov random field model and the expectation-maximization algorithm. IEEE Trans. Med. Imaging 20, 45-57 (2001).

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

www.nature.com/scientificdata/

52. Jenkinson, M., Bannister, P., Brady, M. &amp; Smith, S. Improved optimization for the robust and accurate linear registration and motion correction of brain images. Neuroimage 17, 825-841 (2002).
53. Huntenburg, J. M. Evaluating nonlinear coregistration of BOLD EPI and T1w images. (Freie Universität Berlin, 2014).
54. Wang, S. et al. Evaluation of Field Map and Nonlinear Registration Methods for Correction of Susceptibility Artifacts in Diffusion MRI. Front. Neuroinform. 11, 17 (2017).
55. Treiber, J. M. et al. Characterization and Correction of Geometric Distortions in 814 Diffusion Weighted Images. PLoS One 11, e0152472 (2016).
56. Greve, D. N. &amp; Fischl, B. Accurate and robust brain image alignment using boundary-based registration. Neuroimage 48, 63-72 (2009).
57. Behzadi, Y., Restom, K., Liau, J. &amp; Liu, T. T. A component based noise correction method (CompCor) for BOLD and perfusion based fMRI. Neuroimage 37, 90-101 (2007).
58. Power, J. D. et al. Methods to detect, characterize, and remove motion artifact in resting state fMRI. Neuroimage 84, 320-341 (2014).
59. Abraham, A. et al. Machine learning for neuroimaging with scikit-learn. Front. Neuroinform. 8, 14 (2014).
60. Tournier, J.-D. et al. MRIrix3: A fast, flexible and open software framework for medical image processing and visualisation. Neuroimage 202, 116137 (2019).
61. Veraart, J., Fieremans, E., Novikov, D. S. &amp; Diffusion, M. R. I. noise mapping using random matrix theory. Magn. Reson. Med. 76, 1582-1593 (2016).
62. Veraart, J. et al. Denoising of diffusion MRI using random matrix theory. Neuroimage 142, 394-406 (2016).
63. Kellner, E., Dhital, B., Kiselev, V. G. &amp; Reisert, M. Gibbs-ringing artifact removal based on local subvoxel-shifts. Magn. Reson. Med. 76, 1574-1581 (2016).
64. Andersson, J. L. R. &amp; Sotiropoulos, S. N. An integrated approach to correction for off-resonance effects and subject movement in diffusion MR imaging. Neuroimage 125, 1063-1078 (2016).
65. Andersson, J. L. R., Graham, M. S., Zsoldos, E. &amp; Sotiropoulos, S. N. Incorporating outlier detection and replacement into a nonparametric framework for movement and distortion correction of diffusion MR images. Neuroimage 141, 556-572 (2016).
66. Dhollander, T., Raffelt, D. &amp; Connolly, A. Unsupervised 3-tissue response function estimation from single-shell or multi-shell diffusion MR data without a co-registered T1 image. in ISMRM Workshop on Breaking the Barriers of Diffusion MRI vol. 5 5 (researchgate.net, 2016).
67. Jeurissen, B., Leemans, A. &amp; Sijbers, J. Automated correction of improperly rotated diffusion gradient orientations in diffusion weighted MRI. Med. Image Anal. 18, 953-962 (2014).
68. Veraart, J., Sijbers, J., Sunaert, S., Leemans, A. &amp; Jeurissen, B. Weighted linear least squares estimation of diffusion MRI parameters: strengths, limitations, and pitfalls. Neuroimage 81, 335-346 (2013).
69. Desikan, R. S. et al. An automated labeling system for subdividing the human cerebral cortex on MRI scans into gyral based regions of interest. Neuroimage 31, 968-980 (2006).
70. Destrieux, C., Fischl, B., Dale, A. &amp; Halgren, E. Automatic parcellation of human cortical gyri and sulci using standard anatomical nomenclature. Neuroimage 53, 1-15 (2010).
71. Douaud, G. et al. Anatomically related grey and white matter abnormalities in adolescent-onset schizophrenia. Brain 130, 2375-2386 (2007).
72. Good, C. D. et al. A voxel-based morphometric study of ageing in 465 normal adult human brains. Neuroimage 14, 21-36 (2001).
73. Smith, S. M. et al. Advances in functional and structural MR image analysis and implementation as FSL. Neuroimage 23(Suppl 1), S208-19 (2004).
74. Andersson, J. L. R., Jenkinson, M. &amp; Smith, S. &amp; Others. Non-linear registration, aka Spatial normalisation FMRIB technical report TR07JA2. FMRIB Analysis Group of the University of Oxford 2, e21 (2007).
75. Kasper, L. et al. The PhysIO Toolbox for Modeling Physiological Noise in fMRI Data. J. Neurosci. Methods 276, 56-72 (2017).
76. Glover, G. H., Li, T.-Q. &amp; Ress, D. Image-based method for retrospective correction of physiological motion effects in fMRI: RETROICOR. Magnetic Resonance in Medicine: An Official Journal of the International Society for Magnetic Resonance in Medicine 44, 162-167 (2000).
77. Harvey, A. K. et al. Brainstem functional magnetic resonance imaging: disentangling signal from physiological noise. J. Magn. Reson. Imaging 28, 1337-1344 (2008).
78. Chang, C., Cunningham, J. P. &amp; Glover, G. H. Influence of heart rate on the BOLD signal: the cardiac response function. Neuroimage 44, 857-869 (2009).
79. Birn, R. M., Smith, M. A., Jones, T. B. &amp; Bandettini, P. A. The respiration response function: the temporal dynamics of fMRI signal fluctuations related to changes in respiration. Neuroimage 40, 644-654 (2008).
80. Snoek, L. et al. AOMIC-ID1000. OpenNeuro https://doi.org/10.18112/openneuro.d003097.v1.2.0 (2020).
81. Snoek, L. et al. AOMIC-PIOP1. OpenNeuro https://doi.org/10.18112/openneuro.d002785.v2.0.0 (2020).
82. Snoek, L. et al. AOMIC-PIOP2. OpenNeuro https://doi.org/10.18112/openneuro.d002790.v2.0.0 (2020).
83. Snoek, L. et al. AOMIC-ID1000. NeuroVault https://identifiers.org/neurovault.collection:7105 (2020).
84. Snoek, L. et al. AOMIC-PIOP1. NeuroVault https://identifiers.org/neurovault.collection:7103 (2020).
85. Snoek, L. et al. AOMIC-PIOP2. NeuroVault https://identifiers.org/neurovault.collection:7104 (2020).
86. Gulban, O. F. et al. poldracklab/pydeface: v2.0.0. Zenodo https://doi.org/10.5281/zenodo.3524401 (2019).
87. Esteban, O. et al. MRIQC: Advancing the automatic prediction of image quality in MRI from unseen sites. PLoS One 12, e0184661 (2017).
88. Demetriou, L. et al. A comprehensive evaluation of increasing temporal resolution with multiband-accelerated protocols and effects on statistical outcome measures in fMRI. Neuroimage 176, 404-416 (2018).
89. Beckmann, C. F., Mackay, C. E., Filippini, N. &amp; Smith, S. M. Group comparison of resting-state FMRI data using multi-subject ICA and dual regression. Neuroimage 47, S148 (2009).
90. Smith, S. M. et al. Correspondence of the brain's functional architecture during activation and rest. Proc. Natl. Acad. Sci. USA 106, 13040-13045 (2009).
91. Hasson, U., Nir, Y., Levy, I., Fuhrmann, G. &amp; Malach, R. Intersubject synchronization of cortical activity during natural vision. Science 303, 1634-1640 (2004).
92. Kumar, M. et al. BrainIAK tutorials: User-friendly learning materials for advanced fMRI analysis. PLoS Comput. Biol. 16, e1007549 (2020).
93. Bastiani, M. et al. Automated quality control for within and between studies diffusion MRI data using a non-parametric framework for movement and distortion correction. Neuroimage 184, 801-812 (2019).
94. Li, X., Morgan, P. S., Ashburner, J., Smith, J. &amp; Rorden, C. The first step for neuroimaging data analysis: DICOM to NIfTI conversion. J. Neurosci. Methods 264, 47-56 (2016).
95. Jenkinson, M., Beckmann, C. F., Behrens, T. E. J., Woolrich, M. W. &amp; Smith, S. M. FSL. Neuroimage 62, 782-790 (2012).
96. Fischl, B. FreeSurfer. Neuroimage 62, 774-781 (2012).
97. Pedregosa, F. et al. Scikit-learn: Machine Learning in Python. J. Mach. Learn. Res. 12, 2825-2830 (2011).
98. McCarthy, P. FSLeyes. Zenodo https://doi.org/10.5281/zenodo.3530921 (2019).
99. Waskom, M. et al. mwaskom/seaborn: v0.10.0 (January 2020). Zenodo https://doi.org/10.5281/zenodo.3629446 (2020).

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6

---

www.nature.com/scientificdata/

100. Hunter. Matplotlib. A 2D Graphics Environment. IEEE Ann. Hist. Comput. 9, 90-95 (2007).
101. Magnotta, V. A., Friedman, L. &amp; FIRST BIRN. Measurement of Signal-to-Noise and Contrast-to-Noise in the fBIRN Multicenter Imaging Study. J. Digit. Imaging 19, 140-147 (2006).
102. Ganzetti, M., Wenderoth, N. &amp; Mantini, D. Intensity Inhomogeneity Correction of Structural MR Images: A Data-Driven Approach to Define Input Algorithm Parameters. Front. Neuroinform. 10, 10 (2016).
103. Atkinson, D., Hill, D. L., Stoyle, P. N., Summers, P. E. &amp; Keevil, S. F. Automatic correction of motion artifacts in magnetic resonance images using an entropy focus criterion. IEEE Trans. Med. Imaging 16, 903-910 (1997).
104. Power, J. D., Barnes, K. A., Snyder, A. Z., Schlaggar, B. L. &amp; Petersen, S. E. Spurious but systematic correlations in functional connectivity MRI networks arise from subject motion. Neuroimage 59, 2142-2154 (2012).
105. Saad, Z. S. et al. Correcting brain-wide correlation differences in resting-state FMRI. Brain Connect. 3, 339-352 (2013).

## Acknowledgements

We thank all research assistants and students who helped collecting the data of the three projects, Jasper Wijnen and Marco Teunisse for advice and guidance with respect to anonymization and GDPR-related concerns, Jos Bloemers, Sennay Ghebreab, Adriaan Tuiten, Joram van Driel, Christian Olivers, Ilja Sligte, Sara Jahfari, Guido van Wingen, and Suzanne Oosterwijk for help with designing the paradigms, Marcus Spaan for technical support, and Franklin Feingold and Joe Wexler for help with uploading the datasets to OpenNeuro. The acquisition of the ID1000 dataset was funded by a grant from the Alan Turing Institute (Almere, The Netherlands).

## Author contributions

L.S. curated the datasets, did visual quality control, preprocessed and analyzed the data, and wrote the article. M.v.d.M. did visual quality control, analyzed the data, and wrote the article. T.B. designed the data acquisition protocol of PIOP1 and PIOP2, was responsible for subject recruitment of PIOP1 and PIOP2, collected the data, and did visual quality control for PIOP1 and PIOP2. A.v.d.L. designed the data acquisition protocol, collected data, and did visual quality control for ID1000. A.E. designed and implemented the questionnaires in ID1000, PIOP1 and PIOP2 and managed questionnaire data from ID1000. H.S.S. was principal investigator of the ID1000, PIOP1, and PIOP2 studies, designed the data acquisition protocol of PIOP1, PIOP2, and ID1000, and wrote the article.

## Competing interests

The authors declare no competing interests.

## Additional information

Correspondence and requests for materials should be addressed to L.S.

Reprints and permissions information is available at www.nature.com/reprints.

Publisher's note Springer Nature remains neutral with regard to jurisdictional claims in published maps and institutional affiliations.

Open Access This article is licensed under a Creative Commons Attribution 4.0 International License, which permits use, sharing, adaptation, distribution and reproduction in any medium or format, as long as you give appropriate credit to the original author(s) and the source, provide a link to the Creative Commons license, and indicate if changes were made. The images or other third party material in this article are included in the article's Creative Commons license, unless indicated otherwise in a credit line to the material. If material is not included in the article's Creative Commons license and your intended use is not permitted by statutory regulation or exceeds the permitted use, you will need to obtain permission directly from the copyright holder. To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/.

The Creative Commons Public Domain Dedication waiver http://creativecommons.org/publicdomain/zero/1.0/ applies to the metadata files associated with this article.

© The Author(s) 2021

SCIENTIFIC DATA (2021) 8:85 | https://doi.org/10.1038/s41597-021-00870-6
