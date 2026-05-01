Neuron

Article

Discovering Event Structure
in Continuous Narrative Perception and Memory
Christopher Baldassano,1,3,* Janice Chen,2 Asieh Zadbood,1 Jonathan W. Pillow,1 Uri Hasson,1 and Kenneth A. Norman1
1Princeton Neuroscience Institute and Department of Psychology, Princeton University, Princeton, NJ 08544, USA
2Department of Psychological and Brain Sciences, Johns Hopkins University, Baltimore, MD 21218, USA
3Lead Contact

*Correspondence: chrisb@princeton.edu
http://dx.doi.org/10.1016/j.neuron.2017.06.041



SUMMARY                                                                 dividual words, sentences, paragraphs, or chapters, and we may
                                                                        need to chunk information on different timescales depending on
During realistic, continuous perception, humans auto-                   our goals. Behavioral studies have shown that subjects can
matically segment experiences into discrete events.                     segment events into a nested hierarchy from coarse to fine time-
Using a novel model of cortical event dynamics, we                      scales (Kurby and Zacks, 2008; Zacks et al., 2001b) and flexibly
investigate how cortical structures generate event                      adjust their units of segmentation depending on their uncertainty
representations during narrative perception and how                     about ongoing events (Newtson, 1973). The neural basis of
                                                                        this segmentation behavior is unclear; event perception could
these events are stored to and retrieved from mem-
                                                                        rely on a single unified system, which segments the continuous
ory. Our data-driven approach allows us to detect
                                                                        perceptual stream at different granularities depending on the
event boundaries as shifts between stable patterns                      current task (Zacks et al., 2007), or may rely on multiple brain
of brain activity without relying on stimulus anno-                     areas that segment events at different timescales, as suggested
tations and reveals a nested hierarchy from short                       by the selective deficits for coarse segmentations exhibited by
events in sensory regions to long events in high-                       some patient populations (Zalla et al., 2003, 2004).
order areas (including angular gyrus and posterior                         A recent theory of cortical process-memory topography
medial cortex), which represent abstract, multimodal                    argues that information is integrated at different timescales
situation models. High-order event boundaries are                       throughout the cortex. Processing timescales increase from
coupled to increases in hippocampal activity, which                     tens of milliseconds in early sensory regions (e.g., for detecting
predict pattern reinstatement during later free recall.                 phonemes in early auditory areas), to a few seconds in mid-level
                                                                        sensory areas (e.g., for integrating words into sentences), up to
These areas also show evidence of anticipatory rein-
                                                                        hundreds of seconds in regions including the temporoparietal
statement as subjects listen to a familiar narrative.
                                                                        junction, angular gyrus, and posterior and frontal medial cortex
Based on these results, we propose that brain activity                  (e.g., for integrating information from entire paragraphs) (Chen
is naturally structured into nested events, which form                  et al., 2016; Hasson et al., 2015). The relationship between the
the basis of long-term memory representations.                          process-memory topography and event segmentation has not
                                                                        yet been investigated. On the one hand, it is possible that cortical
                                                                        representations are accumulated continuously, e.g., using a
INTRODUCTION                                                            sliding window approach, at each level of the processing hierar-
                                                                        chy (Stephens et al., 2013). On the other hand, a strong link
Typically, perception and memory are studied in the context of          between the timescale hierarchy and event segmentation
discrete pictures or words. Real-life experience, however, con-         theory would predict that each area chunks experience at its
sists of a continuous stream of perceptual stimuli. The brain           preferred timescale and integrates information within discretized
therefore needs to structure experience into units that can be un-      units (e.g., phonemes, words, sentences, paragraphs) before
derstood and remembered: ‘‘the meaningful segments of one’s             providing its output to the next processing level (Nelson et al.,
life, the coherent units of one’s personal history’’ (Beal and Weiss,   2017). In this view, ‘‘events’’ in low-level sensory cortex (e.g., a
2013). Although this question was first investigated decades ago        single phoneme; Giraud and Poeppel, 2012) are gradually inte-
(Newtson et al., 1977), a general ‘‘event segmentation theory’’         grated into minutes-long situation-level events, using a multi-
was proposed only recently (Zacks et al., 2007). These and other        stage nested temporal chunking. This chunking of continuous
authors have argued that humans implicitly generate event               experience at multiple timescales along the cortical processing
boundaries when consecutive stimuli have distinct temporal as-          hierarchy has not been previously demonstrated in the dynamics
sociations (Schapiro et al., 2013), when the causal structure of        of whole-brain neural activity.
the environment changes (Kurby and Zacks, 2008; Radvansky,                 A second critical question for understanding event perception
2012), or when our goals change (DuBrow and Davachi, 2016).             is how real-life experiences are encoded into long-term memory.
    At what timescale are experiences segmented into events?            Behavioral experiments and mathematical models have argued
When reading a story, we could chunk it into discrete units of in-      that long-term memory reflects event structure during encoding


                                                                            Neuron 95, 709–721, August 2, 2017 ª 2017 Elsevier Inc. 709
Figure 1. Theory of Event Segmentation and Memory
During perception, events are constructed at a hierarchy of timescales (1), with short events in primary sensory regions and long events in regions including the
angular gyrus and posterior medial cortex. These high-level regions have event boundaries that correspond most closely to putative boundaries identified by
human observers (2) and represent abstract narrative content that can be drawn from multiple input modalities (3). At the end of a high-level event, the situation
model is stored into long-term memory (4) (resulting in post-boundary encoding activity in the hippocampus), and can be reinstated during recall back into these
cortical regions (5). Prior event memories can also influence ongoing processing (6), facilitating prediction of upcoming events in related narratives. We test
each of these hypotheses using a data-driven event segmentation model, which can automatically identify transitions in brain activity patterns and detect
correspondences in activity patterns across datasets.



(Ezzyat and Davachi, 2011; Gershman et al., 2014; Sargent et al.,                 at its preferred timescale, beginning with short events in pri-
2013; Zacks et al., 2001b), suggesting that the event segments                    mary visual and auditory cortex and building to multimodal
generated during perception may serve as the ‘‘episodes’’ of                      situation models in long-timescale areas, including the angular
episodic memory. The hippocampus is thought to bind cortical                      gyrus and posterior medial cortex. This model of processing re-
representations into a memory trace (McClelland et al., 1995;                     quires that (1) all regions driven by audio-visual stimuli should
Moscovitch et al., 2005; Norman and O’Reilly, 2003), a process                    exhibit event-structured activity, with segmentation into short
that is typically studied using discrete memoranda (Danker                        events in early sensory areas and longer events in high-order
et al., 2016). However, given a continuous stream of information                  areas; (2) events throughout the hierarchy should have a nested
in a real-life context, it is not clear at what timescale memories                structure, with coarse event boundaries annotated by human
should be encoded and whether these memory traces should                          observers most strongly related to long events at the top of
be continuously updated or encoded only after an event has                        the hierarchy; and (3) event representations in long-timescale
completed. The hippocampus is connected to long-timescale                         regions, which build a coarse model of the situation, should
regions, including the angular gyrus and posterior medial cortex                  be invariant across different descriptions of the same situation
(Kravitz et al., 2011; Ranganath and Ritchey, 2012; Rugg and Vil-                 (e.g., when the same situation is described visually in a movie
berg, 2013), suggesting that the main inputs to long-term mem-                    or a verbally in a story). We also argue that event structure
ory come from these areas, which are thought to represent multi-                  is reflected in how experiences are stored into episodic mem-
modal, abstract representations of the features of the current                    ory. At event boundaries in long-timescale areas, the situation
event (‘‘situation models,’’ Johnson-Laird, 1983; Van Dijk and                    model is transmitted to the hippocampus, which can later
Kintsch, 1983; Zwaan et al., 1995; Zwaan and Radvansky,                           reinstate the situation model in long-timescale regions during
1998; or more generally, ‘‘event models,’’ Radvansky and Zacks,                   recall. This implies that (4) the end of an event in long-timescale
2011). Recent work has shown that hippocampal activity peaks                      cortical regions should trigger the hippocampus to encode
at the offset of video clips (Ben-Yakov and Dudai, 2011; Ben-Ya-                  information about the just-concluded event into episodic
kov et al., 2013), suggesting that the end of a long-timescale                    memory, and (5) stored event memories can be reinstated in
event triggers memory encoding processes that occur after the                     long-timescale cortical regions during recall, with stronger
event has ended.                                                                  reinstatement for more strongly encoded events. Finally, this
   Based on our experiments (described below), we propose                         process can come full circle, with prior event memories
that the full life cycle of an event can be described in a unified                influencing ongoing processing, such that (6) prior memory
theory, illustrated in Figure 1. During perception, each brain                    for a narrative should lead to anticipatory reinstatement in
region along the processing hierarchy segments information                        long-timescale regions.


710 Neuron 95, 709–721, August 2, 2017
Figure 2. Event Segmentation Model
(A) Given a set of (unlabeled) time courses from a region of interest, the goal of the event segmentation model is to temporally divide the data into ‘‘events’’ with
stable activity patterns, punctuated by ‘‘event boundaries’’ at which activity patterns rapidly transition to a new stable pattern. The number and locations of these
event boundaries can then be compared across brain regions or to stimulus annotations.
(B) The model can identify event correspondences between datasets (e.g., responses to movie and audio versions of the same narrative) that share the same
sequence of event activity patterns, even if the duration of the events is different.
(C) The model-identified boundaries can also be used to study processing evoked by event transitions, such as changes in hippocampal activity coupled to event
transitions in the cortex.
(D) The event segmentation model is implemented as a modified Hidden Markov Model (HMM) in which the latent state st for each time point denotes the event to
which that time point belongs, starting in event 1 and ending in event K. All datapoints during event K are assumed to be exhibit high similarity with an event-
specific pattern mk. See also Figures S1, S2, and S3.



   To test these hypotheses, we need the ability to identify how                    the model to multiple datasets evoked by the same narrative
different brain areas segment events (at different timescales),                     (e.g., during movie viewing and during later verbal recall), the
align events across different datasets with different timings                       model is constrained to find the same sequence of patterns
(e.g., to see whether the same situation model is being elicited                    (because the events are the same), but the timing of the transi-
by a movie versus a verbal narrative, or a movie versus recall),                    tions between the patterns can vary (e.g., since the spoken
and track differences in event segmentations in different ob-                       description of the events might not take as long as the original
servers of the same stimulus (e.g., depending on prior experi-                      events).
ence). Thus, to search for the neural correlates of event segmen-                      In prior studies, using human-based segmentation of coarse
tation, we have developed a new data-driven method that allows                      event structure, we demonstrated that event-related representa-
us to identify events directly from fMRI activity patterns across                   tions generalize across modalities and between encoding and
multiple timescales and datasets (Figure 2).                                        recall (thereby supporting hypotheses 3 and 5, Chen et al.,
   Our analysis approach (described in detail in STAR Methods)                      2017; Zadbood et al., 2016). In the current study, we extend
starts with two simple assumptions: that while processing a                         these findings by testing whether we can use the data-driven
narrative stimulus, observers progress through a sequence of                        HMM to detect stable and abstract event boundaries in high-
discrete event representations (hidden states), and that each                       order areas without relying on human annotations. This new
event has a distinct (observable) signature (a multi-voxel fMRI                     analysis approach also allows us to test for the first time whether
pattern) that is present throughout the event. We implement                         the brain segments information, hierarchically, at multiple time-
these assumptions using a data-driven event segmentation                            scales (hypotheses 1 and 2); how segmentation of information
model, based on a Hidden Markov Model (HMM). Fitting the                            interacts with the storage and retrieval of this information by
model to fMRI data (e.g., evoked by viewing a movie) entails esti-                  the hippocampus (hypothesis 4); and how prior exposure to a
mating the optimal number of events, the mean activity pattern                      sequence of events can later lead to anticipatory reinstatement
for each event, and when event transitions occur. When applying                     of those events (hypothesis 6). Taken together, our results


                                                                                                                  Neuron 95, 709–721, August 2, 2017 711
Figure 3. Event Segmentation Model for Movie-Watching Data Reveals Event Timescales
The event segmentation model identifies temporally clustered structure in movie-watching data throughout all regions of cortex with high intersubject correlation.
The optimal number of events varied by an order of magnitude across different regions, with a large number of short events in sensory cortex and a small number of
long events in high-level cortex. For example, the time point correlation matrix for a region in the precuneus exhibited coarse blocks of correlated patterns, leading
to model fits with a small number of events (white squares), while a region in visual cortex was best modeled with a larger number of short events (note that only
!3 min of the 50-min stimulus are shown and that the highlighted searchlights were selected post hoc for illustration). The searchlight was masked to include only
regions with intersubject correlation > 0.25 and voxelwise thresholded for greater within-than across-event similarity, q < 0.001. See also Figures S3, S4, and S8.


provide the first direct evidence that realistic experiences are                     our model (periods with stable event patterns punctuated by
discretely and hierarchically chunked at multiple timescales in                      shifts between events) and whether the timescales of these
the brain, with chunks at the top of the processing hierarchy                        events varied along the cortical hierarchy. We tested the model
playing a special role in cross-modal situation representation                       by fitting it to fMRI data collected while subjects watched a
and episodic memory.                                                                 50-min movie (Chen et al., 2017) and then assessing how well
                                                                                     the learned event structure explained the activity patterns of a
RESULTS                                                                              held-out subject. Note that previous analyses of this dataset
                                                                                     have shown that the evoked activity is similar across subjects,
All of our analyses are carried out using our new HMM-based                          justifying an across-subjects design (Chen et al., 2017). We found
event segmentation model (summarized above, and described                            that essentially all brain regions that responded consistently to
in detail in the Event Segmentation Model subsection in STAR                         the movie (across subjects) showed evidence for event-like
Methods), which can automatically discover the fMRI signatures                       structure, and that the optimal number of events varied across
of each event and its temporal boundaries in a particular dataset.                   the cortex (Figure 3). Sensory regions like visual and auditory cor-
We validated this model using both synthetic data (Figure S1)                        tex showed faster transitions between stable activity patterns,
and narrative data with clear event breaks between stories (Fig-                     while higher-level regions like the posterior medial cortex,
ure S2), confirming that we could accurately recover the number                      angular gyrus, and intraparietal sulcus had activity patterns that
of event boundaries and their locations (see STAR Methods). We                       often remained constant for over a minute before transitioning
then applied the model to test six predictions of our theory of                      to a new stable pattern (see Figure 3 insets and Figure S3). This
event perception and memory.                                                         topography of event timescales is broadly consistent with that
                                                                                     found in previous work (Hasson et al., 2015) measuring sensitivity
Timescales of Cortical Event Segmentation                                            to temporal scrambling of a movie stimulus (see Figure S8).
We first tested the hypothesis that all regions driven by audio-
visual stimuli should exhibit event-structured activity, with seg-                   Comparison of Event Boundaries across Regions and to
mentation into short events in early sensory areas and longer                        Human Annotations
events in high-order areas. We measured the extent to which                          The second implication of our theory is that events throughout
continuous stimuli evoked the event structure hypothesized by                        the hierarchy should have a nested structure, with coarse event


712 Neuron 95, 709–721, August 2, 2017
Figure 4. Cortical Event Boundaries Are Hierarchically Structured and Are Related to Human-Labeled Event Boundaries, Especially in
Posterior Medial Cortex
(A) An example of boundaries evoked by the movie over a 4-min period shows how the number of boundaries decreases as we proceed up the hierarchy, with
boundaries in posterior medial cortex most closely related to human annotations of event transitions.
(B) Event boundaries in higher regions are present in lower regions at above-chance levels (especially pairs of regions that are close in the hierarchy), suggesting
that event segmentation is in part hierarchical, with lower regions subdividing events in higher regions.
(C) All four levels of the hierarchy show an above-chance match to human annotations (the null distribution is shown in gray), but the match increases significantly
from lower to higher levels (yp = 0.058, *p < 0.05, **p < 0.01).


boundaries annotated by human observers most strongly related                      a significant amount of overlap, with an average pairwise Dice’s
to long events at the top of the hierarchy. To examine how                         coefficient of 0.63 and 20 event boundaries that were labeled
event boundaries changed throughout the cortical hierarchy,                        by all four raters. We constructed a ‘‘consensus’’ annotation con-
we created four regions of interest, each with 300 voxels,                         taining boundaries marked by at least two raters, which split the
centered on ROIs from prior work (see STAR Methods): early                         narrative into 54 events, similar to the mean timescale for individ-
visual cortex, late visual cortex, angular gyrus, and posterior                    ual annotators (49.5).We then measured, for each region, what
medial cortex. We identified the optimal timescale for each re-                    fraction of its fMRI-defined boundaries were close to (within three
gion as in the previous analysis and then fit the event segmenta-                  time points of) a consensus event boundary. As shown in Fig-
tion model at this optimal timescale, as illustrated in Figure 4A.                 ure 4C, all regions showed an above-chance match to human an-
We found that a significant portion of the boundaries in a given                   notations (early visual, p = 0.0135; late visual, p = 0.0065; angular
layer were also present in lower layers (Figure 4B), especially                    gyrus, p = 0.0011; posterior medial, p < 0.001), but this match
for adjacent layers in the hierarchy. This suggests that event                     increased across the layers of the hierarchy and was largest in
segmentation is at least partially hierarchical, with finer event                  angular gyrus and posterior medial cortex (angular gyrus > early
boundaries nested within coarser boundaries.                                       visual, p = 0.0580; posterior medial > early visual, p = 0.033).
   We asked four independent raters to divide the movie into
‘‘scenes’’ based on major shifts in the narrative (such as in loca-                Shared Event Structure across Modalities
tion, topic, or time). The number of event boundaries identified by                The third requirement of our theory is that activity patterns
the observers varied between 36 and 64, but the boundaries had                     in long-timescale regions should be invariant across different


                                                                                                                 Neuron 95, 709–721, August 2, 2017 713
                                                                                            Figure 5. Movie-Watching Model General-
                                                                                            izes to Audio Narration in High-Level Cortex
                                                                                            After identifying a series of event patterns in a
                                                                                            group of subjects who watched a movie, we tested
                                                                                            whether this same series of events occurred in a
                                                                                            separate group of subjects who heard an audio
                                                                                            narration of the same story. The movie and audio
                                                                                            stimuli were not synchronized and differed in their
                                                                                            duration. We restricted our searchlight to voxels
                                                                                            that responded to both the movie and audio stimuli
                                                                                            (having high intersubject correlation within each
                                                                                            group). Movie-watching event patterns in early
                                                                                            auditory cortex (dotted line) did not generalize to
                                                                                            the activity evoked by audio narration, while re-
                                                                                            gions including the angular gyrus, temporoparietal
                                                                                            junction, posterior medial cortex, and inferior
                                                                                            frontal cortex exhibited shared event structure
                                                                                            across the two stimulus modalities. This analysis,
                                                                                            conducted using our data-driven model, replicates
                                                                                            and extends the previous analysis of this dataset
                                                                                            (Zadbood et al., 2016) in which the event corre-
                                                                                            spondence between the movie and audio narration
                                                                                            was specified by hand. The searchlight is masked
                                                                                            to include only regions with intersubject correla-
                                                                                            tion > 0.1 in all conditions and voxelwise thresh-
                                                                                            olded for above-chance movie-audio fit, q < 10"5.
                                                                                            See also Figure S8.



descriptions of the same situation. This hypothesis is based on a    campus to encode information about the just-concluded event
prior study (Zadbood et al., 2016) in which one group of subjects    into episodic memory. Prior work has shown that the end of a
watched a 24-min movie while the other group listened to an          video clip is associated with increased hippocampal activity,
18-min audio narration describing the events that occurred in        and the magnitude of the activity predicts later memory (Ben-
the movie. The prior study used a hand-labeled event correspon-      Yakov and Dudai, 2011; Ben-Yakov et al., 2013). These experi-
dence between these two stimuli to show that activity patterns       ments, however, have used only isolated short video clips with
evoked by corresponding events in the movie and narration            clear transitions between events. Do neurally defined event
were correlated in a network of regions including angular gyrus,     boundaries in a continuous movie, evoked by subtler transitions
precuneus, retrosplenial cortex, posterior cingulate cortex, and     between related scenes, generate the same kind of hippocampal
mPFC (Zadbood et al., 2016). Here, we use this dataset to ask        signature? Using a searchlight procedure, we identified event
whether our event segmentation model can replicate these             boundaries with the HMM segmentation model for each cortical
results in a purely unsupervised manner, without using any prior     area across the timescale hierarchy, using the 50-min movie
event labeling.                                                      dataset (Chen et al., 2017). We then computed the average
   For each cortical searchlight, we first segmented the movie       hippocampal activity around the event boundaries of each
data into events and then tested whether this same sequence          cortical area to determine whether a cortical boundary tended
of events from the movie-watching subjects was present in the        to trigger a hippocampal response. We found that event bound-
audio-narration subjects. Regions including the angular gyrus,       aries in a distributed set of regions including angular gyrus, pos-
temporoparietal junction, posterior medial cortex, and inferior      terior medial cortex, and parahippocampal cortex all showed
frontal cortex showed a strongly significant correspondence          a strong relationship to hippocampal activity, with the hippocam-
between the two modalities (Figure 5), indicating that a similar     pal response typically peaking within several time points after the
sequence of event patterns was evoked by the movie and audio         event boundary (Figure 6). This network of regions closely over-
narration irrespective of the modality used to describe the          laps with the posterior medial memory system (Ranganath and
events. In contrast, though low-level auditory cortex was reliably   Ritchey, 2012). Note that both the event boundaries and the
activated by both of these stimuli, there was no above-chance        hippocampal response are hemodynamic signals, so there is
similarity between the series of activity patterns evoked by the     no hemodynamic offset between these two measures. The hip-
two stimuli (movie versus verbal description), presumably            pocampal response does start slightly before the event bound-
because the low-level auditory features of the two stimuli were      ary, which could be due to uncertainty in the model estimation
markedly different.                                                  of the exact boundary time point and/or anticipation that the
                                                                     event is about to end.
Relationship between Cortical Event Boundaries and
Hippocampal Encoding                                                 Reinstatement of Event Patterns during Free Recall
We tested a fourth hypothesis from our theory, that the end of an    Our theory further implies that stored event memories can be
event in long-timescale cortical regions should trigger the hippo-   reinstated in long-timescale cortical regions during recall, with


714 Neuron 95, 709–721, August 2, 2017
Figure 6. Hippocampal Activity Increases at Cortically Defined Event Boundaries
To determine whether event boundaries may be related to long-term memory encoding, we identify event boundaries based on a cortical region and then
measure hippocampal activity around those boundaries. In a set of regions including angular gyrus, posterior medial cortex, and parahippocampal cortex, we find
that event boundaries robustly predict increases in hippocampal activity, which tends to peak just after the event boundary (shaded region indicates 95%
confidence interval). The searchlight is masked to include only regions with intersubject correlation > 0.25 and voxelwise thresholded for post-boundary hip-
pocampal activity greater than pre-boundary activity, q < 0.001. See also Figures S5 and S8.



stronger reinstatement for more strongly encoded events. After                   (p = 0.015) and the angular gyrus (p = 0.002), but not in low-level
watching the movie, all subjects in this dataset were asked to                   auditory cortex (p = 0.277) (Figure 7B). This result demonstrates
retell the story they had just watched, without any cues or stim-                that we can identify shared temporal structure between percep-
ulus (see Chen et al., 2017 for full details). We focused our ana-               tion and recall without any human annotations. A similar pattern
lyses on the high-level regions that showed a strong relationship                of results can be found regardless of the number of latent events
with hippocampal activity in the previous analysis (posterior                    used (see Figure S6). The identified correspondences for each
cingulate and angular gyrus), as well as early auditory cortex                   subject (using both posterior cingulate and angular gyrus) were
for comparison.                                                                  also significantly similar to the human-labeled correspondences
   Using the event segmentation model, we first estimated the                    (probability mass inside annotations = 17.8%, significantly
(group-average) series of event-specific activity patterns evoked                greater than null model [11.9%], p < 0.001) (see Figure S6).
by the movie and then attempted to segment each subject’s                           We then assessed whether the hippocampal response evoked
recall data into corresponding events. When fitting the model                    by the end of an event during the encoding of the movie to
to the recall data, we assumed that the same event-specific ac-                  memory was predictive of the length of time for which the event
tivity patterns seen during the movie-viewing will be reinstated                 was strongly reactivated during recall. As shown in Figures 7C
during the spoken recall. Analyzing the spoken recall transcrip-                 and 7D, we found that encoding activity and event reactivation
tions revealed that subjects generally recalled the events in the                were positively correlated in both angular gyrus (r = 0.362,
same order as they appeared in the movie (see Table S1 in                        p = 0.002) and the posterior cingulate (r = 0.312, p = 0.042),
Chen et al., 2017). Therefore, the model was constrained to                      but not early auditory cortex (r = 0.080, p = 0.333). Note that there
use the same order of multi-voxel event patterns for recall that                 was no relationship between the hippocampal activity at the
it had learned from the movie-watching data. However, crucially,                 starting boundary of an event and that event’s later reinstate-
the model was allowed to learn different event timings for the                   ment in the angular gyrus (r = "0.119, p = 0.867; difference
recall data compared to the movie data—this allowed us to                        from ending boundary correlation p = 0.004) and only a weak,
accommodate the fact that event durations differed for free                      nonsignificant relationship in posterior cingulate (r = 0.189,
recall versus movie-watching.                                                    p = 0.113; difference from ending boundary correlation
   For each subject, the model attempted to find a sequence                      p = 0.274). The relationship between the average hippocampal
of latent event patterns that was shared between the movie                       activity throughout an event and later cortical reinstatement
and recall, as shown in the example with 25 events in Figure 7A                  was actually negative (angular gyrus, r = "0.247, p = 0.017; pos-
(see Figure S6 for examples from all subjects). Green shading                    terior cingulate, r = "0.092, p = 0.175), suggesting that encoding
indicates the probability that a movie and a recall time point                   is strongest when hippocampal activity is relatively low during an
belong to the same latent event (with darker shading indicating                  event and high at its offset.
higher probability), and boxes indicate segments of the movie
and recall that were labeled as corresponding to the same event                  Anticipatory Reinstatement for a Familiar Narrative
by human annotators. Compared to the null hypothesis that                        Finally, we tested a sixth hypothesis, that prior memory for
there was no shared event order between the movie and recall,                    a narrative should lead to anticipatory reinstatement in long-
we found significant model fits in both the posterior cingulate                  timescale regions. Our ongoing interpretation of events can be


                                                                                                              Neuron 95, 709–721, August 2, 2017 715
Figure 7. Movie-Watching Events Are Reactivated during Individual Free Recall, and Reactivation Is Related to Hippocampal Activation at
Encoding Event Boundaries
(A) We can obtain an estimated correspondence between movie-watching data and free-recall data in individual subjects by identifying a shared sequence of
event patterns, shown here for an example subject using data from posterior cingulate cortex.
(B) For each region of interest, we tested whether the movie and recall data shared an ordered sequence of latent events (relative to a null model in which the order
of events was shuffled between movie and recall). We found that both angular gyrus (blue) and posterior cingulate cortex (green) showed significant reactivation of
event patterns, while early auditory cortex (red) did not.
(C and D) Events whose offset drove a strong hippocampal response during encoding (movie-watching) were strongly reactivated for longer fractions of the recall
period, both in the angular gyrus and the posterior cingulate. Error bars for event points denote SEM across subjects, and error bars on the best-fit line indicate
95% confidence intervals from bootstrapped best-fit lines. See also Figure S6.



influenced by prior knowledge; specifically, if subjects listening                  sequence of event patterns across conditions. By analyzing
to the audio version of a narrative had already seen the movie                      which time points were assigned to the same event, we can
version, they may anticipate upcoming events compared to sub-                       generate a time point correspondence indicating—for each
jects experiencing the narrative for the first time. Detecting this                 time point during the audio narration datasets—which time
kind of anticipation has not been possible with previous ap-                        points of the movie are most strongly evoked (on average) in
proaches that rely on stimulus annotations, since the difference                    the mind of the listeners.
between the two groups is not in the stimulus (which is identical)                     We searched for cortical regions along the hierarchy of time-
but rather in the temporal dynamics of their cognitive processes.                   scale showing anticipation, in which this correspondence for
   Using data from Zadbood et al. (2016), we simultaneously fit                     the memory group was consistently ahead of the correspon-
our event segmentation model to three conditions—watching                           dence for the no-memory group (relative to chance). As shown
the movie, listening to the narration after watching the movie                      in Figure 8, we found anticipatory event reinstatement in the
(‘‘memory’’), and listening to the narration without having previ-                  angular gyrus, posterior medial cortex, and medial frontal cortex.
ously seen the movie (‘‘no memory’’)—looking for a shared                           Examining the movie-audio correspondences in these regions,


716 Neuron 95, 709–721, August 2, 2017
Figure 8. Prior Memory Shifts Movie-Audio Correspondence
The event segmentation model was fit simultaneously to data from a group watching the movie, the same group listening to the audio narration after having seen
the movie (‘‘memory’’), and a separate group listening to the audio narration for the first time (‘‘no memory’’). By examining which time points were estimated to fall
within the same latent event, we obtained a correspondence between time points in the audio data (for both groups) and time points in the movie data. We found
regions in which the correspondence in both groups was close to the human-labeled correspondence between the movie and audio stimuli (black boxes), but the
memory correspondence (orange) significantly led the non-memory correspondence (blue) (indicated by an upward shift on the correspondence plots; note that
the highlighted searchlights were selected post hoc for illustration). This suggests that cortical regions of the memory group were anticipating events in the
narration based on knowledge of the movie. The searchlight is masked to include only regions with intersubject correlation > 0.1 in all conditions and voxelwise
thresholded for above-chance differences between memory and no memory groups, q < 0.05. See also Figures S7 and S8.


the memory group was consistently ahead of the no-memory                             fMRI data of naturalistic narratives, without using specially con-
group, indicating that for a given time point of the audio narration                 structed stimuli or subjective labeling of where events should
the memory group had event representations that corresponded                         start and end. Previous work has shown that hand-labeled event
to later time points in the movie. A similar result can be obtained                  boundaries are associated with univariate activity increases in a
by directly aligning the two listening conditions without reference                  network of regions overlapping our high-level areas (Ezzyat and
to the movie-watching condition (see Figure S7).                                     Davachi, 2011; Speer et al., 2007; Swallow et al., 2011; Whitney
                                                                                     et al., 2009; Zacks et al., 2001a, 2010), but by modeling fine-
DISCUSSION                                                                           scale spatial activity patterns we were able to detect these event
                                                                                     changes without an external reference. This allowed us to iden-
We found that narrative stimuli evoke event-structured activity                      tify regions with temporal event structure at many different time-
throughout the cortex, with pattern dynamics consisting of                           scales, only some of which matched human-labeled boundaries.
relatively stable periods punctuated by rapid event transitions.                     Other analyses of these datasets also found reactivation during
Furthermore, the angular gyrus and posterior medial cortex                           recall (Chen et al., 2017) and shared event structure across
exhibit a set of overlapping properties associated with high-level                   modalities (Zadbood et al., 2016); however, because these
situation model representations: long event timescales, event                        other analyses defined events based on the narrative rather
boundaries closely related to human annotations, generalization                      than brain activity, they were unable to identify differences in
across modalities, hippocampal response at event boundaries,                         event segmentation across brain areas or across groups with
reactivation during free recall, and anticipatory coding for                         different prior knowledge.
familiar narratives. Identifying all of these properties was made
possible by using naturalistic stimuli with extended temporal                        Processing Timescales and Event Segmentation
structure, paired with a data-driven model for identifying activity                  The topography of event timescales revealed by our analysis
patterns shared across time points and across datasets.                              provides converging evidence for an emerging view of how
                                                                                     information is processed during real-life experience (Hasson
Event Segmentation Theory                                                            et al., 2015). The ‘‘process memory framework’’ argues that
Our results are the first to validate a number of key predictions                    perceptual stimuli are integrated across longer and longer time-
of event segmentation theory (Zacks et al., 2007) directly from                      scales along a hierarchy from early sensory regions to regions in


                                                                                                                   Neuron 95, 709–721, August 2, 2017 717
the default-mode network. Using a variety of experimental ap-         events (defined by pattern shifts in high-level regions), providing
proaches, including fMRI, electrocorticography (ECoG), and sin-       evidence that event boundaries trigger the storage of the current
gle-unit recording, this topography has previously been mapped        situation representation into long-term memory. We have also
either by temporally scrambling the stimulus at different time-       shown that this post-event hippocampal activity is related to
scales to see which regions’ responses are disrupted (Hasson          pattern reinstatement during recall, as has been recently demon-
et al., 2008; Honey et al., 2012; Lerner et al., 2011) or by exam-    strated for the encoding of discrete items (Danker et al., 2016),
ining the power spectrum of intrinsic dynamics within each re-        thereby supporting the view that events are the natural units of
gion (Honey et al., 2012; Murray et al., 2014; Stephens et al.,       episodic memory during everyday life. Changes in cortical activ-
2013). Our model and results yield a new perspective on these         ity patterns may drive encoding through a comparator operation
findings, suggesting that all processing regions can exhibit rapid    in the hippocampus (Lisman and Grace, 2005; Vinogradova,
activity shifts, but that these fast changes are much less frequent   2001), or the prediction error associated with event boundaries
in long-timescale regions. The power spectrum is therefore an         may potentiate the dopamine pathway (Zacks et al., 2011),
incomplete description of voxel dynamics, since the correlation       thereby leading to improved hippocampal encoding (Kempadoo
timescale changes dynamically, with faster changes at event           et al., 2016; Takeuchi et al., 2016). Notably, the positive relation-
boundaries and slower changes within boundaries (see also Fig-        ship between hippocampal activity and subsequent cortical rein-
ure S4B). We also found evidence for nested hierarchical struc-       statement was specific to hippocampal activity at the end of an
ture, suggesting that chunks of information are transmitted from      event; there was no significant relationship between hippocam-
lower to higher levels primarily at event boundaries, as in recent    pal activity at the start of an event and subsequent reinstate-
multiscale recurrent neural network models (Chung et al., 2017).      ment, and higher hippocampal activity during an event was
   The specific features encoded in the event representations         associated with worse reinstatement (a similar relationship was
of long-timescale regions like the angular gyrus and posterior        observed in parietal cortex by Lee et al., 2017). In this respect,
cingulate cortex during naturalistic perception are still an          our results differ from other results showing that the hippocam-
open question. These areas are involved in high-level, multi-         pal response to novel events drives memory for the novel events
modal scene processing tasks including memory and naviga-             themselves (for a review, see Ranganath and Rainer, 2003)—
tion (Baldassano et al., 2016; Kumar et al., 2017), are part of       here, we show that the hippocampal response to a new event
the ‘‘general recollection network’’ with strong anatomical and       is linked to subsequent memory for the previous event.
functional connectivity to the hippocampus (Rugg and Vilberg,            Most extant models of memory consolidation (McClelland
2013), and are the core components of the posterior medial            et al., 1995) and recall (Polyn et al., 2009) have been formulated
memory system (Ranganath and Ritchey, 2012), which is                 under the assumption that the input to the memory system is
thought to represent and update a high-level situation model          a series of discrete items to be remembered. Although this
(Johnson-Laird, 1983; Van Dijk and Kintsch, 1983; Zwaan               is true for experimental paradigms that use lists of words or
et al., 1995; Zwaan and Radvansky, 1998). Since event repre-          pictures, it was not clear how these models could function for
sentations in these regions generalized across modalities and         realistic autobiographical memory. Our model connects natural-
between perception and recall, our results provide further evi-       istic perception with theories about discrete memory traces, by
dence that they encode high-level situation descriptions. We          proposing that cortex chunks continuous experiences into
also found that event patterns could be partially predicted by        discrete events; these events are integrated along the process-
key characters and locations from the narrative (see Figure S4D,      ing hierarchy into meaningful, temporally extended, episodic
and Figure S6 in Chen et al., 2017), but future work (with richer     structures, to be later encoded into memory via interaction
descriptions of narrative events, Vodrahalli et al., 2017) will be    with the hippocampus. The fact that the hippocampus is coupled
required to understand how event patterns are evoked by se-           to both angular gyrus and posterior medial cortex, which have
mantic content.                                                       slightly different timescales, raises the interesting possibility
                                                                      that these event memories could be stored at multiple temporal
Events in Episodic Memory                                             resolutions.
Behavioral experiments have shown that long-term memory
reflects event structure during encoding (Ezzyat and Davachi,         Our Event Segmentation Model
2011; Sargent et al., 2013; Zacks et al., 2001b). Here, we were       Temporal latent variable models have been largely absent from
able to identify the reinstatement of events that were automati-      the field of human neuroscience, since the vast majority of exper-
cally discovered during perception, extending previous work           iments have a temporal structure that is defined ahead of time by
demonstrating reinstatement of individual items or scenes in          the experimenter. One notable exception is the recent work of
angular gyrus and posterior medial cortex (Chen et al., 2017;         Anderson and colleagues, which has used HMM-based models
Johnson et al., 2009; Kuhl and Chun, 2014; Ritchey et al.,            to discover temporal structure in brain activity responses during
2013; Wing et al., 2015) to continuous perception without any         mathematical problem solving (Anderson and Fincham, 2014;
stimulus annotations.                                                 Anderson et al., 2014, 2016). These models are used to segment
   We demonstrated that the hippocampal encoding activity pre-        problem-solving operations (performed in less than 30 s) into a
viously shown to be present at the end of movie clips (Ben-Yakov      small number of cognitively distinct stages such as encoding,
and Dudai, 2011; Ben-Yakov et al., 2013) and at abrupt switches       planning, solving, and responding. Our work is the first to show
between stimulus category and task (DuBrow and Davachi,               that (using a modified HMM and an annealed fitting procedure)
2016) also occurs at the much more subtle transitions between         this latent-state approach can be extended to much longer


718 Neuron 95, 709–721, August 2, 2017
experimental paradigms with a much larger number of latent                d METHOD DETAILS
states.                                                                       B Interleaved Stories dataset
   For finding correspondences between continuous datasets,                   B Sherlock Recall dataset
as in our analyses of shared structure between perception and                 B Sherlock Narrative dataset
recall or perception under different modalities, several other                B Event annotations by human observers
types of approaches (not based on HMMs) have been proposed                    B Event Segmentation Model
in psychology and machine learning. Dynamic time warping                      B Finding event structure in narratives
(Kang and Wheatley, 2015; Silbert et al., 2014) locally stretches             B Timescales of cortical event segmentation
or compresses two time series to find the best match, and                     B Comparison of event boundaries across regions and to
more complex methods such as conditional random fields (Zhu                       human annotations
et al., 2015) allow for parts of the match to be out of order. How-           B Shared event structure across modalities
ever, these methods do not explicitly model event boundaries.                 B Relationship between cortical event boundaries and
   Future work will be required to investigate what types of neural               hippocampal encoding
correspondences are well modeled by continuous warping                        B Reinstatement of event patterns during free recall
versus event-structured models. Logically, a strictly event-struc-            B Anticipatory reinstatement for a familiar narrative
tured model (with static event patterns) cannot be a complete             d QUANTIFICATION AND STATISTICAL ANALYSIS
description of brain activity during narrative perception, since              B Timescales of cortical event segmentation
subjects are actively accumulating information during each                    B Comparison of event boundaries across regions and to
event, and extensions of our model could additionally model                       human annotations
these within-event dynamics (see Figure S4B).                                 B Shared event structure across modalities
                                                                              B Relationship between cortical event boundaries and
Perception and Memory in the Wild                                                 hippocampal encoding
Our results provide a bridge between the large literature on long-            B Reinstatement of event patterns during free recall
term encoding of individual items (such as words or pictures) and             B Anticipatory reinstatement for a familiar narrative
studies of memory for real-life experience (Nielson et al., 2015;         d DATA AND SOFTWARE AVAILABILITY

Rissman et al., 2016). Since our approach does not require an
experimental design with rigid timing, it opens the possibility of     SUPPLEMENTAL INFORMATION
having subjects be more actively and realistically engaged in a
task, allowing for the study of events generated during virtual re-    Supplemental Information includes eight figures and can be found with this
                                                                       article online at http://dx.doi.org/10.1016/j.neuron.2017.06.041.
ality navigation (such as spatial boundaries, Horner et al., 2016)
or while holding dialogs with a simultaneously scanned subject
(Hasson et al., 2012). The model also is not fMRI specific and could   AUTHOR CONTRIBUTIONS
be applied to other types of neuroimaging time series such as
                                                                       Conceptualization: C.B., J.C., J.W.P., U.H., and K.A.N.; Methodology: C.B.,
ECoG, electroencephalography (EEG), or functional near-infrared
                                                                       J.W.P., U.H., and K.A.N.; Software: C.B.; Investigation: C.B., J.C., and A.Z.;
spectroscopy (fNIRS), including portable systems that could allow      Writing – Original Draft: C.B.; Writing – Review and Editing: C.B., J.C., A.Z.,
experiments to be run outside the lab (McKendrick et al., 2016).       J.W.P., U.H., K.A.N.; Supervision: U.H. and K.A.N.


Conclusion                                                             ACKNOWLEDGMENTS
Using a novel event segmentation model that can be fit directly
to neuroimaging data, we showed that cortical responses to             We thank M. Chow for assistance in collecting the Interleaved Stories data-
naturalistic stimuli are temporally organized into discrete events     set, M.C. Iordan for help in porting the model implementation to python, and
                                                                       the members of the Hasson and Norman labs for their comments and sup-
at varying timescales. In a network of high-level association
                                                                       port. This work was supported by a grant from Intel Labs (CAB), The
regions, we found that these events were related to subjective         National Institutes of Health (R01 MH112357-01 to U.H. and K.A.N.,
event annotations by human observers, predicted hippocampal            R01-MH094480 to U.H., and 2T32MH065214-11 to K.A.N.), the McKnight
encoding, generalized across modalities and between percep-            Foundation (J.W.P.), NSF CAREER Award IIS-1150186 (J.W.P.), and a grant
tion and recall, and showed anticipatory coding of familiar narra-     from the Simons Collaboration on the Global Brain (SCGB AWD1004351
tives. Our results provide a new framework for understanding           to J.W.P.).
how continuous experience is accumulated, stored, and recalled.
                                                                       Received: October 21, 2016
                                                                       Revised: May 8, 2017
STAR+METHODS                                                           Accepted: June 26, 2017
                                                                       Published: August 2, 2017
Detailed methods are provided in the online version of this paper
and include the following:                                             REFERENCES

   d KEY RESOURCES TABLE                                               Anderson, J.R., and Fincham, J.M. (2014). Discovering the sequential structure
   d CONTACT FOR REAGENT AND RESOURCE SHARING                          of thought. Cogn. Sci. 38, 322–352.
   d EXPERIMENTAL MODEL AND SUBJECT DETAILS                            Anderson, J.R., Lee, H.S., and Fincham, J.M. (2014). Discovering the structure
      B Interleaved Stories dataset                                    of mathematical problem solving. Neuroimage 97, 163–177.



                                                                                                    Neuron 95, 709–721, August 2, 2017 719
Anderson, J.R., Pyke, A.A., and Fincham, J.M. (2016). Hidden Stages of              Hasson, U., Chen, J., and Honey, C.J. (2015). Hierarchical process memory:
Cognition Revealed in Patterns of Brain Activation. Psychol. Sci. 27, 1215–         memory as an integral component of information processing. Trends Cogn.
1226.                                                                               Sci. 19, 304–313.
Baldassano, C., Esteva, A., Beck, D.M., and Fei-Fei, L. (2016). Two distinct        Honey, C.J., Thesen, T., Donner, T.H., Silbert, L.J., Carlson, C.E., Devinsky, O.,
scene processing networks connecting vision and memory. eNeuro 3, http://           Doyle, W.K., Rubin, N., Heeger, D.J., and Hasson, U. (2012). Slow cortical
dx.doi.org/10.1523/ENEURO.0178-16.2016.                                             dynamics and the accumulation of information over long timescales. Neuron
Beal, D.J., and Weiss, H.M. (2013). The Episodic Structure of Life at Work. In      76, 423–434.
A Day in the Life of a Happy Worker, A.B. Bakker and K. Daniels, eds.               Horner, A.J., Bisby, J.A., Wang, A., Bogus, K., and Burgess, N. (2016). The role
(Psychology Press), pp. 8–24.                                                       of spatial boundaries in shaping long-term event representations. Cognition
Ben-Yakov, A., and Dudai, Y. (2011). Constructing realistic engrams: poststim-      154, 151–164.
ulus activity of hippocampus and dorsal striatum predicts subsequent                Johnson, J.D., McDuff, S.G.R., Rugg, M.D., and Norman, K.A. (2009).
episodic memory. J. Neurosci. 31, 9032–9042.                                        Recollection, familiarity, and cortical reinstatement: a multivoxel pattern anal-
Ben-Yakov, A., Eshel, N., and Dudai, Y. (2013). Hippocampal immediate post-         ysis. Neuron 63, 697–708.
stimulus activity in the encoding of consecutive naturalistic episodes. J. Exp.     Johnson-Laird, P.N. (1983). Mental models: Towards a cognitive science of
Psychol. Gen. 142, 1255–1263.                                                       language, inference, and consciousness (Harvard University Press).
Chen, J., Chow, M., Norman, K.A., and Hasson, U. (2015a). Differentiation           Kang, O., and Wheatley, T. (2015). Pupil dilation patterns reflect the contents of
of neural representations during processing of multiple information streams         consciousness. Conscious. Cogn. 35, 128–135.
(Society for Neuroscience).
                                                                                    Kempadoo, K.A., Mosharov, E.V., Choi, S.J., Sulzer, D., and Kandel, E.R.
Chen, P.-H. (Cameron), Chen, J., Yeshurun, Y., Hasson, U., Haxby, J., and           (2016). Dopamine release from the locus coeruleus to the dorsal hippocampus
Ramadge, P.J. (2015b). A Reduced-Dimension fMRI Shared Response                     promotes spatial learning and memory. Proc. Natl. Acad. Sci. USA 113,
Model. In Advances in Neural Information Processing Systems 28 (NIPS                14835–14840.
2015). http://papers.nips.cc/paper/5855-a-reduced-dimension-fmri-shared-
                                                                                    Kravitz, D.J., Saleem, K.S., Baker, C.I., and Mishkin, M. (2011). A new neural
response-model.
                                                                                    framework for visuospatial processing. Nat. Rev. Neurosci. 12, 217–230.
Chen, J., Honey, C.J., Simony, E., Arcaro, M.J., Norman, K.A., and Hasson, U.
(2016). Accessing Real-Life Episodic Information from Minutes versus Hours          Kuhl, B.A., and Chun, M.M. (2014). Successful remembering elicits event-spe-
Earlier Modulates Hippocampal and High-Order Cortical Dynamics. Cereb.              cific activity patterns in lateral parietal cortex. J. Neurosci. 34, 8051–8060.
Cortex 26, 3428–3441.                                                               Kumar, M., Federmeier, K.D., Fei-Fei, L., and Beck, D.M. (2017). Evidence For
Chen, J., Leong, Y.C., Honey, C.J., Yong, C.H., Norman, K.A., and Hasson, U.        Similar Patterns of Neural Activity Elicted by Picture- and Word-based
(2017). Shared memories reveal shared structure in neural activity across indi-     Representations of Natural Scenes. Neuroimage. Published online March
viduals. Nat. Neurosci. 20, 115–125.                                                24, 2017. http://dx.doi.org/10.1016/j.neuroimage.2017.03.037.

Chung, J., Ahn, S., and Bengio, Y. (2017). Hierarchical Multiscale Recurrent        Kurby, C.A., and Zacks, J.M. (2008). Segmentation in the perception and
Neural Networks. In 5th International Conference on Learning Representations        memory of events. Trends Cogn. Sci. 12, 72–79.
(ICLR 2017).                                                                        Lee, H., Chun, M.M., and Kuhl, B.A. (2017). Lower Parietal Encoding Activation
Cox, R.W. (1996). AFNI: software for analysis and visualization of functional       Is Associated with Sharper Information and Better Memory. Cereb. Cortex 27,
magnetic resonance neuroimages. Comput. Biomed. Res. 29, 162–173.                   2486–2499.
http://www.ncbi.nlm.nih.gov/pubmed/8812068.                                         Lerner, Y., Honey, C.J., Silbert, L.J., and Hasson, U. (2011). Topographic
Danker, J.F., Tompary, A., and Davachi, L. (2016). Trial-by-Trial Hippocampal       mapping of a hierarchy of temporal receptive windows using a narrated story.
Encoding Activation Predicts the Fidelity of Cortical Reinstatement During          J. Neurosci. 31, 2906–2915.
Subsequent Retrieval. Cereb. Cortex. Published online June 10, 2016. http://        Lisman, J.E., and Grace, A.A. (2005). The hippocampal-VTA loop: controlling
dx.doi.org/10.1093/cercor/bhw146.                                                   the entry of information into long-term memory. Neuron 46, 703–713.
DuBrow, S., and Davachi, L. (2016). Temporal binding within and across              McClelland, J.L., McNaughton, B.L., and O’Reilly, R.C. (1995). Why there are
events. Neurobiol. Learn. Mem. 134 (Pt A), 107–114.                                 complementary learning systems in the hippocampus and neocortex: insights
Eickhoff, S.B., Stephan, K.E., Mohlberg, H., Grefkes, C., Fink, G.R., Amunts,       from the successes and failures of connectionist models of learning and mem-
K., and Zilles, K. (2005). A new SPM toolbox for combining probabilistic            ory. Psychol. Rev. 102, 419–457.
cytoarchitectonic maps and functional imaging data. Neuroimage 25, 1325–            McKendrick, R., Parasuraman, R., Murtza, R., Formwalt, A., Baccus, W.,
1335.                                                                               Paczynski, M., and Ayaz, H. (2016). Into the Wild: Neuroergonomic
Ezzyat, Y., and Davachi, L. (2011). What constitutes an episode in episodic         Differentiation of Hand-Held and Augmented Reality Wearable Displays during
memory? Psychol. Sci. 22, 243–252.                                                  Outdoor Navigation with Functional Near Infrared Spectroscopy. Front. Hum.
Gershman, S.J., Radulescu, A., Norman, K.A., and Niv, Y. (2014). Statistical        Neurosci. 10, 216.
computations underlying the dynamics of memory updating. PLoS Comput.               Moscovitch, M., Rosenbaum, R.S., Gilboa, A., Addis, D.R., Westmacott, R.,
Biol. 10, e1003939.                                                                 Grady, C., McAndrews, M.P., Levine, B., Black, S., Winocur, G., and Nadel,
Giraud, A.-L., and Poeppel, D. (2012). Cortical oscillations and speech pro-        L. (2005). Functional neuroanatomy of remote episodic, semantic and spatial
cessing: emerging computational principles and operations. Nat. Neurosci.           memory: a unified account based on multiple trace theory. J. Anat. 207, 35–66.
15, 511–517.                                                                        Murray, J.D., Bernacchia, A., Freedman, D.J., Romo, R., Wallis, J.D., Cai, X.,
Hasson, U., Nir, Y., Levy, I., Fuhrmann, G., and Malach, R. (2004). Intersubject    Padoa-Schioppa, C., Pasternak, T., Seo, H., Lee, D., and Wang, X.J. (2014).
synchronization of cortical activity during natural vision. Science 303, 1634–      A hierarchy of intrinsic timescales across primate cortex. Nat. Neurosci. 17,
1640.                                                                               1661–1663.
Hasson, U., Yang, E., Vallines, I., Heeger, D.J., and Rubin, N. (2008). A hierar-   Nelson, M.J., El Karoui, I., Giber, K., Yang, X., Cohen, L., Koopman, H., Cash,
chy of temporal receptive windows in human cortex. J. Neurosci. 28, 2539–           S.S., Naccache, L., Hale, J.T., Pallier, C., and Dehaene, S. (2017).
2550.                                                                               Neurophysiological dynamics of phrase-structure building during sentence
Hasson, U., Ghazanfar, A.A., Galantucci, B., Garrod, S., and Keysers, C.            processing. Proc. Natl. Acad. Sci. USA 114, E3669–E3678.
(2012). Brain-to-brain coupling: a mechanism for creating and sharing a social      Newtson, D. (1973). Attribution and the unit of perception of ongoing behavior.
world. Trends Cogn. Sci. 16, 114–121.                                               Journal of Personality and Social Psychology 28, 28–38.



720 Neuron 95, 709–721, August 2, 2017
Newtson, D., Engquist, G.A., and Bois, J. (1977). The objective basis of           Morris, R.G. (2016). Locus coeruleus and dopaminergic consolidation of
behavior units. Journal of Personality and Social Psychology 35, 847–862.          everyday memory. Nature 537, 357–362.
Nielson, D.M., Smith, T.A., Sreekumar, V., Dennis, S., and Sederberg, P.B.         Van Dijk, T.A., and Kintsch, W. (1983). Strategies of discourse comprehension
(2015). Human hippocampus represents space and time during retrieval of            (Academic Press).
real-world memories. Proc. Natl. Acad. Sci. USA 112, 11078–11083.
                                                                                   Vinogradova, O.S. (2001). Hippocampus as comparator: role of the two input
Norman, K.A., and O’Reilly, R.C. (2003). Modeling hippocampal and neocor-          and two output systems of the hippocampus in selection and registration of
tical contributions to recognition memory: a complementary-learning-systems        information. Hippocampus 11, 578–598.
approach. Psychol. Rev. 110, 611–646.
                                                                                   Vodrahalli, K., Chen, P.-H., Liang, Y., Baldassano, C., Chen, J., Yong, E.,
Polyn, S.M., Norman, K.A., and Kahana, M.J. (2009). A context maintenance
                                                                                   Honey, C., Hasson, U., Ramadge, P., Norman, K., and Arora, S. (2017).
and retrieval model of organizational processes in free recall. Psychol. Rev.
                                                                                   Mapping Between fMRI Responses to Movies and their Natural Language
116, 129–156.
                                                                                   Annotations. NeuroImage. Published online June 23, 2017. http://dx.doi.org/
Radvansky, G.A. (2012). Across the Event Horizon. Current Directions in            10.1016/j.neuroimage.2017.06.042.
Psychological Science 21, 269–272.
                                                                                   Wang, L., Mruczek, R.E., Arcaro, M.J., and Kastner, S. (2015). Probabilistic
Radvansky, G., and Zacks, J.M. (2011). Event Perception. Wiley Interdiscip.        Maps of Visual Topography in Human Cortex. Cereb. Cortex 25, 3911–3931.
Rev. Cogn. Sci. 2, 608–620.
                                                                                   Whitney, C., Huber, W., Klann, J., Weis, S., Krach, S., and Kircher, T. (2009).
Ranganath, C., and Rainer, G. (2003). Neural mechanisms for detecting and
                                                                                   Neural correlates of narrative shifts during auditory story comprehension.
remembering novel events. Nat. Rev. Neurosci. 4, 193–202.
                                                                                   Neuroimage 47, 360–366.
Ranganath, C., and Ritchey, M. (2012). Two cortical systems for memory-
guided behaviour. Nat. Rev. Neurosci. 13, 713–726.                                 Wing, E.A., Ritchey, M., and Cabeza, R. (2015). Reinstatement of individual
                                                                                   past events revealed by the similarity of distributed activation patterns during
Rissman, J., Chow, T.E., Reggente, N., and Wagner, A.D. (2016). Decoding
                                                                                   encoding and retrieval. J. Cogn. Neurosci. 27, 679–691.
fMRI Signatures of Real-world Autobiographical Memory Retrieval. J. Cogn.
Neurosci. 28, 604–620.                                                             Zacks, J.M., Braver, T.S., Sheridan, M.A., Donaldson, D.I., Snyder, A.Z.,
                                                                                   Ollinger, J.M., Buckner, R.L., and Raichle, M.E. (2001a). Human brain activity
Ritchey, M., Wing, E.A., LaBar, K.S., and Cabeza, R. (2013). Neural similarity
                                                                                   time-locked to perceptual event boundaries. Nat. Neurosci. 4, 651–655.
between encoding and retrieval is related to memory via hippocampal interac-
tions. Cereb. Cortex 23, 2818–2828.                                                Zacks, J.M., Tversky, B., and Iyer, G. (2001b). Perceiving, remembering, and
Rugg, M.D., and Vilberg, K.L. (2013). Brain networks underlying episodic mem-      communicating structure in events. J. Exp. Psychol. Gen. 130, 29–58.
ory retrieval. Curr. Opin. Neurobiol. 23, 255–260.                                 Zacks, J.M., Speer, N.K., Swallow, K.M., Braver, T.S., and Reynolds, J.R.
Sargent, J.Q., Zacks, J.M., Hambrick, D.Z., Zacks, R.T., Kurby, C.A., Bailey,      (2007). Event perception: a mind-brain perspective. Psychol. Bull. 133,
H.R., Eisenberg, M.L., and Beck, T.M. (2013). Event segmentation ability           273–293.
uniquely predicts event memory. Cognition 129, 241–255.                            Zacks, J.M., Speer, N.K., Swallow, K.M., and Maley, C.J. (2010). The
Schapiro, A.C., Rogers, T.T., Cordova, N.I., Turk-Browne, N.B., and Botvinick,     Brain’s Cutting-Room Floor: Segmentation of Narrative Cinema. Front. Hum.
M.M. (2013). Neural representations of events arise from temporal community        Neurosci. 4, 1–15.
structure. Nat. Neurosci. 16, 486–492.                                             Zacks, J.M., Kurby, C.A., Eisenberg, M.L., and Haroutunian, N. (2011).
Shirer, W.R., Ryali, S., Rykhlevskaia, E., Menon, V., and Greicius, M.D. (2012).   Prediction error associated with the perceptual segmentation of naturalistic
Decoding subject-driven cognitive states with whole-brain connectivity pat-        events. J. Cogn. Neurosci. 23, 4057–4066.
terns. Cereb. Cortex 22, 158–165.
                                                                                   Zadbood, A., Chen, J., Leong, Y.C., Norman, K.A., and Hasson, U. (2016). How
Silbert, L.J., Honey, C.J., Simony, E., Poeppel, D., and Hasson, U. (2014).        we transmit memories to other brains: constructing shared neural representa-
Coupled neural systems underlie the production and comprehension of natu-          tions via communication. bioRxiv. http://dx.doi.org/10.1101/081208.
ralistic narrative speech. Proc. Natl. Acad. Sci. USA 111, E4687–E4696.
                                                                                   Zalla, T., Pradat-Diehl, P., and Sirigu, A. (2003). Perception of action bound-
Simony, E., Honey, C.J., Chen, J., Lositsky, O., Yeshurun, Y., Wiesel, A., and
                                                                                   aries in patients with frontal lobe damage. Neuropsychologia 41, 1619–1627.
Hasson, U. (2016). Dynamic reconfiguration of the default mode network dur-
ing narrative comprehension. Nat. Commun. 7, 12141.                                Zalla, T., Verlut, I., Franck, N., Puzenat, D., and Sirigu, A. (2004). Perception of
                                                                                   dynamic action in patients with schizophrenia. Psychiatry Res. 128, 39–51.
Speer, N.K., Zacks, J.M., and Reynolds, J.R. (2007). Human brain activity time-
locked to narrative event boundaries. Psychol. Sci. 18, 449–455.                   Zhu, Y., Kiros, R., Zemel, R., Salakhutdinov, R., Urtasun, R., Torralba, A.,
Stephens, G.J., Honey, C.J., and Hasson, U. (2013). A place for time: the          and Fidler, S. (2015). Aligning Books and Movies: Towards Story-like
spatiotemporal structure of neural dynamics during natural audition.               Visual Explanations by Watching Movies and Reading Books. arXiv,
J. Neurophysiol. 110, 2019–2026.                                                   arXiv:1506.06724, https://arxiv.org/abs/1506.06724.

Swallow, K.M., Barch, D.M., Head, D., Maley, C.J., Holder, D., and Zacks, J.M.     Zwaan, R.A., and Radvansky, G.A. (1998). Situation models in language
(2011). Changes in events alter how people remember recent information.            comprehension and memory. Psychol. Bull. 123, 162–185.
J. Cogn. Neurosci. 23, 1052–1064.                                                  Zwaan, R.A., Langston, M.C., and Graesser, A.C. (1995). The Construction of
Takeuchi, T., Duszkiewicz, A.J., Sonneborn, A., Spooner, P.A., Yamasaki, M.,       Situation Models in Narrative Comprehension: An Event-Indexing Model.
Watanabe, M., Smith, C.C., Fernández, G., Deisseroth, K., Greene, R.W., and       Psychol. Sci. 6, 292–297.




                                                                                                                  Neuron 95, 709–721, August 2, 2017 721
STAR+METHODS

KEY RESOURCES TABLE



REAGENT or RESOURCE          SOURCE               IDENTIFIER
Software and Algorithms
Event Segmentation Model     Custom Software      https://github.com/intelpni/brainiak, https://github.com/cbaldassano/Event-Segmentation
MATLAB                       MathWorks            https://www.mathworks.com/products/matlab.html
Python                       Python               https://www.python.org/



CONTACT FOR REAGENT AND RESOURCE SHARING

Further information and requests for resources should be directed to and will be fulfilled by the Lead Contact, Christopher Baldas-
sano (chrisb@princeton.edu).

EXPERIMENTAL MODEL AND SUBJECT DETAILS

Interleaved Stories dataset
Twenty-two subjects (all native English speakers) were recruited from the Princeton community (9 male, 13 female, ages 18-26). All
subjects provided informed written consent prior to the start of the study in accordance with experimental procedures approved by
the Princeton University Institutional Review Board. The study was approximately 2 hr long and subjects received $20 per hour as
compensation for their time. Data from 3 subjects were discarded due to falling asleep during the scan, and 1 due to problems
with audio delivery.

METHOD DETAILS

Interleaved Stories dataset
To test our model in a dataset with clear, unambiguous event boundaries, we used data from subjects who listened to two unrelated
audio narratives (Chen et al, 2015a). We used data from 18 subjects who listened to the two audio narratives in an interleaved fashion,
with the audio stimulus switching between the two narratives approximately every 60 s at natural paragraph breaks. The total stim-
ulus length was approximately 29 min, during which there were 32 story switches. The audio was delivered via in-ear headphones.
   Imaging data were acquired on a 3T full-body scanner (Siemens Skyra) with a 20-channel head coil using a T2*-weighted echo
planar imaging (EPI) pulse sequence (TR 1500 ms, TE 28 ms, flip angle 64, whole-brain coverage 27 slices of 4 mm thickness, in-plane
resolution 3 3 3 mm, FOV 192 3 192 mm). Preprocessing was performed in FSL, including slice time correction, motion correction,
linear detrending, high-pass filtering (140 s cutoff), and coregistration and affine transformation of the functional volumes to a tem-
plate brain (MNI). Functional images were resampled to 3 mm isotropic voxels for all analyses.
   The analyses in this paper were carried out using data from a posterior cingulate region of interest, the posterior medial cluster in
the ‘‘dorsal default mode network’’ defined by whole-brain resting state connectivity clustering (Shirer et al., 2012).

Sherlock Recall dataset
Our primary dataset consisted of 17 subjects who watched the first 50 min of the first episode of BBC’s Sherlock, and were then
asked to freely recall the episode in the scanner without cues (Chen et al., 2017). Subjects varied in the length and richness of their
recall, with total recall times ranging from 11 min to 46 min (and a mean of 22 min). Imaging data was acquired using a T2*-weighted
echo planar imaging (EPI) pulse sequence (TR 1500 ms, TE 28 ms, flip angle 64, whole-brain coverage 27 slices of 4 mm thickness, in-
plane resolution 3 3 3 mm, FOV 192 3 192 mm). A standard preprocessing pipeline was performed using FSL, including motion
correction. Since acoustic output was not correlated across subjects (Chen et al., 2017), shared activity patterns at recall are unlikely
to be driven by correlated motion artifacts. All subjects were aligned to a common MNI template, and analyses were carried out in this
common volume space. We also conducted an alternate version of the segmentation analysis that does not rely on precise MNI align-
ment (Chen et al., 2015b) and obtained similar results (see Figure S4C).
   We restricted our searchlight analyses to voxels that were reliably driven by the stimuli, measured using intersubject correlation
(Hasson et al., 2004). Voxels with a correlation less than r = 0.25 during movie-watching were removed before running the searchlight
analysis.
   We defined five regions of interest based on prior work. In addition to the posterior cingulate region defined above, we defined the
angular gyrus as area PG (both PGa and PGp) using the maximum probability maps from a cytoarchitectonic atlas (Eickhoff et al.,



e1 Neuron 95, 709–721.e1–e5, August 2, 2017
2005), early auditory cortex as voxels within the Heschl’s gyrus region (Harvard-Oxford cortical atlas) with high intersubject correla-
tion during an audio narrative (‘‘Pieman,’’ Simony et al., 2016), early visual cortex as voxels near the calcarine sulcus with high
intersubject correlation during an audio-visual movie (‘‘The Twilight Zone,’’ Chen et al., 2016), and hV4 based on a group
maximum-probability atlas (Wang et al., 2015).

Sherlock Narrative dataset
To investigate cross-modal event representations and the impact of prior memory, we used a separate dataset in which subjects
experienced multiple versions of a narrative. One group of 17 subjects watched the first 24 min of the first episode of Sherlock
(a portion of the same episode used in the Sherlock Recall dataset), while another group of 17 subjects (who had never seen the
episode before) listened to an 18 min audio description of the events during this part of the episode (taken from the audio recording
of one subject’s recall in the Sherlock Recall dataset). The subjects who watched the episode then listened to the same 18 min audio
description. This yielded three sets of data, all based on the same story: watching a movie of the events, listening to an audio narration
of the events without prior memory, and listening to an audio narration of the events with prior memory. Imaging data was acquired
using the same sequence as in Sherlock Recall dataset; see Zadbood et al. (2016) for full acquisition and preprocessing details.
   As in the Sherlock Recall experiment, we removed all voxels that were not reliably driven by the stimuli. Only voxels with an inter-
subject correlation of at least r = 0.1 across all three conditions were included in searchlight analyses.

Event annotations by human observers
Four human observers were given the video file for the 50 min Sherlock stimulus, and given the following directions: ‘‘Write down the
times at which you feel like a new scene is starting; these are points in the movie when there is a major change in topic, location, time,
etc. Each ‘scene’ should be between 10 seconds and 3 minutes long. Also, give each scene a short title.’’ The similarity among ob-
servers was measured using Dice’s coefficient (number of matching boundaries divided by mean number of boundaries, considering
boundaries within three time points of one another to match).

Event Segmentation Model
Our model is built on two hypotheses: (1) while processing narrative stimuli, observers experience a sequence of discrete events, and
(2) each event has a distinct neural signature. Mathematically, the model assumes that a given subject (or averaged group of subjects)
starts in event s1 = 1 and ends in event sT = K, where T is the total number of time points and K is the total number of events. In each
time point the subject either remains in the same state or advances to the next state, i.e., st+1 ˛ {st, st+1} for all time points t. Each
event has a signature mean activity pattern mk across all V voxels in a region of interest, and the observed brain activity bt at any time
point t is assumed to be highly correlated with mk, as illustrated in Figure 2.
    Given the sequence of observed brain activities bt, our goal is to infer both the event signatures mk and the event structure st.
To accomplish this, we cast our model as a variant of a Hidden Markov Model (HMM). The latent states are the events st that evolve
according to a simple transition matrix, in which all elements are zero except for the diagonal (corresponding to st+1 = st)
and the adjacent         off-diagonal (corresponding to st+1 = st+1), and the observation model is an isotropic Gaussian
                   pﬃﬃﬃﬃﬃﬃﬃﬃﬃﬃ     2                2
pðbt jst = kÞ = ð1= 2ps2 Þe"ð1=2s Þkzðbt Þ"zðmk Þ k 2 , where zðxÞ denotes z-scoring an input vector x to have zero mean and unit variance.
Note that, due to this z-scoring, the log probability of observing brain state bt in an event with signature mk is simply proportional
to the Pearson correlation between bt and mk plus a constant offset.
    The HMM is fit to the fMRI data by using an annealed version of the Baum-Welch algorithm, which iterates between estimating the
fMRI signatures mk and the latent event structure st. Given the signature estimates mk, the distributions over latent events p(st = k) can
be computed using the forward-backward algorithm. Given the distributions p(st = k), the updated estimates for the signatures
                                                              P            P
mk can be computed as the weighted average mk = t pðst = kÞbt = t pðst = kÞ. To encourage convergence to a high-likelihood solu-
tion, we anneal the observation variance s2 as 4,0:98i where i is the number of loops of Baum-Welch completed so far. We stop the
fitting procedure when the log-likelihood begins to decrease, indicating that the observation variance has begun to drop below the
actual event activity variance. We can also fit the model simultaneously to multiple datasets; on each round of Baum-Welch, we run
the forward-backward algorithm on each dataset separately, and then average across all datasets to compute a single set of shared
signatures mk.
    The end state requirement of our model – that all states should be visited, and the end state should be symmetrical to all other
states – requires extending the traditional HMM by modifying the observation probabilities pðbt j st = kÞ. First, we enforce sT = K by
requiring that, on the final timestep, only the final state K could have generated the data, by setting pðbT j sT = kÞ = 0 for all ksK.
Equivalently, we can view this as a modification of the backward pass, by initializing the backward message bðsT = kÞ to 1 for
k = K and 0 otherwise. Second, we must modify the transition matrix to ensure that all valid event segmentations (which start at event 1
and end at event K, and proceed monotonically through all events) have the same prior probability. Formally, we introduce a dummy
absorbing state K+1 to which state K can transition, ensuring that the transition probabilities for state K are identical to those for pre-
vious states, and then set pðbt j st = K + 1Þ = 0 to ensure that this state is never actually used.
    Since we do not want to assume that events will have the same relative lengths across different datasets (such as a movie and
audio-narration version of the same narrative), we fix all states to have the same probability of staying in the same state (st+1 = st)
versus jumping to the next state (st+1 = st+1). Note that the shared probability of jumping to the next state can take any value between


                                                                                           Neuron 95, 709–721.e1–e5, August 2, 2017 e2
0 and 1 with no effect on the results (up to a normalization constant in the log-likelihood), since every valid event segmentation will
contain exactly the same number of jumps (K-1).
                                                                                                "       #
                                                                                                     T
   Our model induces a prior over the locations of the event boundaries. There are a total of              equally likely placements of the
                                                                                                   K"1
K-1 event boundaries, and the number of ways to have event boundary k fall on time point t is the number of ways that k-1 boundaries
can be placed in t-1 time points times the number of ways that (K-1)-(k-1)-1 boundaries can be placed in T-t time points. Therefore
                             "     #"            #$"         #
                               t"1       T"t             T
pðst = k & st + 1 = k + 1Þ =                                   . An example of this distribution is shown in Figure S1. During the anneal-
                               k"1    K"k"1            K"1
ing process, the distribution over boundary locations starts at this prior, and slowly adjusts to match the event structure of the data.
   After fitting the model on one set of data, we can then look for the same sequence of events in another dataset. Using the signatures
mk learned from the first dataset, we simply perform a single round of the forward-backward algorithm to obtain event estimates
p(st = k) on the second dataset. If we expect the datasets to have similar noise properties (e.g., both datasets are group-averaged
data from the same number of subjects), we set the observation variance to the final s2 obtained while fitting the first dataset. When
transferring events learned on group-averaged data to individual subjects, we estimate the variance for each event across the indi-
vidual subjects of the first dataset.
   The model implementation was first verified using simulated data. An event-structured dataset was constructed with V = 10 voxels,
K = 10 events, and T = 500 time points. The event structure was chosen to be either uniform (with 50 time points per event), or the
length of each event was sampled (from first to last) from N(1,0.25)*(time points remaining)/(events remaining). A mean pattern was
drawn for each event from a standard normal distribution, and the simulated data for each time point was the sum of the event pattern
for that time point plus randomly distributed noise with zero mean and varying standard deviation. The noisy data were then input to
the event segmentation model, and we measured the fraction of the event boundaries that were exactly recovered from the true un-
derlying event structure. As shown in Figure S1, were able to recover a majority of the event boundaries even when the noise level was
as large as the signature patterns themselves.

Finding event structure in narratives
To validate our event segmentation model on real fMRI data, we first fit the model to group-averaged PCC data from the Interleaved
Stories experiment. In this experiment, we expect that an event boundary should be generated every time the stimulus switches
stories, giving a ground truth against which to compare the model’s segmentations. As shown in Figure S2, our method was highly
effective at identifying events, with the majority of the identified boundaries falling close to a story switch.
   The following subsections describe how the model was used to obtain each of the experimental results, with subsection titles cor-
responding to subsections of the Results.

Timescales of cortical event segmentation
We applied the model in a searchlight to the whole-brain movie-watching data from the Sherlock Recall study. Cubical searchlights
were scanned throughout the volume at a step size of 3 voxels and with a side length of 7 voxels. For each searchlight, the event
segmentation model was applied to group-averaged data from all but one subject. We measured the robustness of the identified
boundaries by testing whether these boundaries explained the data in the held-out subject. We measured the spatial correlation be-
tween all pairs of time points that were separated by four time points, and then binned these correlations according to whether the
pair of time points fell within the same event or crossed over an event boundary. The average difference between the within- versus
across-event correlations was used as an index of how well the learned boundaries captured the temporal structure of the held-out
subject. The analysis was repeated for every possible held-out subject, and with a varying number of events from K = 10 to K = 120.
After averaging the results across subjects, the number of events with the best within- versus across-event correlations was chosen
as the optimal number of events for this searchlight.
  Since the topography of the results was similar to previous work on temporal receptive windows, we compared the map of the
optimal number of events with the short and medium/long timescale maps derived by measuring intersubject correlation for intact
versus scrambled movies (Chen et al., 2016). The histogram of the optimal number of events for voxels was computed within
each of the timescale maps.

Comparison of event boundaries across regions and to human annotations
We defined four equally-sized regions along the cortical hierarchy by taking the centers of mass of the early visual cortex, hV4,
angular gyrus and PCC ROIs in each hemisphere, and finding the nearest 150 voxels to these centers (yielding 300 bilateral voxels
for each region). For each region, we calculated its optimal number of events using the same within- versus across-event correlation
procedure described in the previous section, and then fit a final event segmentation model with the optimal number of events (using
the Sherlock Recall data). We measured the match between levels of the hierarchy by computing the fraction of boundaries in the
‘‘upper’’ (slower) level that were close to a boundary in the ‘‘lower’’ (faster) level. We defined ‘‘close to’’ as ‘‘within three time points,’’
since the typical uncertainty in the model about exactly where an event switch occurred was approximately three time points.




e3 Neuron 95, 709–721.e1–e5, August 2, 2017
  To measure similarity to the human annotations, we first constructed a ‘‘consensus’’ annotation from the four observers, consisting
of boundary locations that were within three time points of boundaries marked by at least two observers. We then measured the
match between the consensus boundaries and the boundaries from each region, treating the consensus boundaries as the ‘‘upper’’
level. To ensure that differences between regions were not driven by timescale differences, for this comparison we refit the event
segmentation model to each cortical region using the same number of events as in the consensus annotation (rather than using
each region’s optimal timescale).

Shared event structure across modalities
After fitting the event segmentation model to a searchlight of movie-watching data from the Sherlock Narration experiment, we took
the learned event signatures mk and used them to run the forward-backward algorithm on the audio narration data, to test whether
audio narration of a story elicited the same sequence of events as a movie of that story. Since both the movie and audio data were
averaged at the group level, they should have similar levels of noise, and therefore we simply used the fit movie variance s2 for the
observation variance.

Relationship between cortical event boundaries and hippocampal encoding
After applying the event segmentation model throughout the cortex to the Sherlock Recall study as described above, we measured
whether the data-driven event boundaries were related to activity in the hippocampus. For a given cortical searchlight, we extracted a
window of mean hippocampal activity around each of the searchlight’s event boundaries. We then averaged these windows together,
yielding a profile of boundary-triggered hippocampal response according to this region’s boundaries. To assess whether the hippo-
campus showed a significant increase in activity related to these event boundaries, we measured the mean hippocampal activity for
the 10 time points following the event boundary minus the mean activity for the 10 time points preceding the event boundary.

Reinstatement of event patterns during free recall
For each region of interest, we fit the event segmentation model as described above (on the group-averaged Sherlock Recall data).
We then took the learned sequence of event signatures mk and ran the forward-backward algorithm on each individual subject’s
recall data. We set the variance of each event’s observation model by computing the variance within each event in the movie-watch-
ing data of individual subjects, pooling across both time points and subjects. The analysis was run for 10 events to 60 events in
steps of 5.
                                                                    P
  We operationalized the overall reinstatement of an event k, as t pðst = kÞ; that is, the sum across all recall time points of the prob-
ability that the subject was recalling perceptual event k at that time point. We measured whether this per-event re-activation during
recall could be predicted during movie-watching, based on the hippocampal response at the end of the event. For each subject, we
computed the difference between hippocampal activity after versus before the event boundary as above. We then averaged the
event re-activation and hippocampal offset response across subjects, and measured their correlation. For comparison purposes,
we also performed the same analysis but with hippocampal differences at the beginning of each event, rather than the end, and
with the mean hippocampal activity throughout the event.

Anticipatory reinstatement for a familiar narrative
To determine whether memory changed the event correspondence between the movie and narration, we then fit the segmentation
model simultaneously to group-averaged data from the movie-watching condition, audio narration no-memory condition, and audio
narration with memory condition, yielding a sequence of events in each condition with the same activity signatures. We computed
the correspondence between the movie states sm,t and the audio no-memory states sanm,t as as pðsm;t1 = sanm;t2 Þ =
P
  k pðsm;t1 = kÞ,pðsanm;tP   2
                               = kÞ, and similarly for the audio memory states sam,t. We computed the differences between the group
                                 P
correspondences as t1 t2 ðpðsm;t1 = sanm;t2 Þ " pðsm;t1 = sam;t2 ÞÞ2 . For visualization, we also computed how far the memory corre-
spondence was ahead of the no-memory correspondence as the mean over t2 of the difference in the expected values
P                              P
  t1 t1 pðsm;t1 = sanm;t2 Þ "    t1 t1 pðsm;t1 = sam;t2 Þ. We also performed the same analysis but with only the two narration conditions,
computing the correspondence between the audio memory and audio no-memory states as pðsam;t1 = sanm;t2 Þ =
P
  k pðsam;t1 = kÞ,pðsanm;t2 = kÞ. Since deviation from a diagonal          correspondence
                                                                         P P            pﬃﬃﬃwould indicate anticipation in the memory group,
we measured the expected deviation from the diagonal as t1 t2 ðjt1 " t2 j = 2Þpðsam;t1 = sanm;t2 Þ, and for visualization calculated
                                        P
the amount of anticipation as t tpðsam;t1 = sanm;t2 Þ " T=2.

QUANTIFICATION AND STATISTICAL ANALYSIS

Permutation or resampling analyses were used to statistically evaluate all of the results. As above, the analyses for each subsection
are presented under a corresponding heading.

Timescales of cortical event segmentation
To generate a null distribution, the same analysis was performed except that the event boundaries were scrambled before computing
the within- versus across-event correlation. This scrambling was performed by reordering the events with their durations held


                                                                                           Neuron 95, 709–721.e1–e5, August 2, 2017 e4
constant, to ensure that the null events had the same distribution of event lengths as the real events. The within versus across
difference for the real events compared to 1000 null events was used to compute a z value, which was converted to a p value using
the normal distribution. The p values were Bonferroni corrected for the 12 choices of the number of events, and then the false
discovery rate q was computed using the same calculation as in AFNI (Cox, 1996).

Comparison of event boundaries across regions and to human annotations
For each pairwise comparison between regions or between a region and the human annotations, we scrambled the event boundaries
using the same duration-preserving procedure described above to produce 1000 null match values. The true match value was
compared to this distribution to compute a z value, which was converted to a p value. To assess whether two cortical regions
had significantly different matches to human annotations, we scrambled the boundaries from the regions (keeping the human
annotations intact), and computed the fraction of scrambles for which the difference in the match to human annotations was larger
in the null data than the original data.

Shared event structure across modalities
We compared the log-likelihood of the fit to the narration data against a null model in which the movie event signatures mk were
randomly re-ordered, and computed the z value of the true log-likelihood compared to 100 null shuffles, then converted to a p value.
This null hypothesis test therefore assessed whether the narration exhibited ordered reactivation of the events identified during
movie-watching.

Relationship between cortical event boundaries and hippocampal encoding
For each searchlight, we compared the difference in hippocampal activity for the 10 time points after an event boundary compared to
10 time points before an event boundary, both on the true boundaries and on shuffled event boundaries (using the duration-preser-
ving procedure described above). The z value for this difference was computed to a p value, and then transformed to a false discovery
rate q.

Reinstatement of event patterns during free recall
As in the movie-to-narration analysis, we compared the log-likelihood of the movie-recall fit to a null model in which the order of the
event signatures was shuffled before fitting to the recall data, which yielded a z value that was converted to a p value. When
measuring the match to human annotations, we compared to the same shuffled-event null models.
  To assess the robustness of the encoding activity versus reinstatement correlations, we performed a bootstrap test, in which we
resampled subjects (with replacement, yielding 17 subjects as in the original dataset) before taking the average and computing the
correlation. The p value was defined as the fraction of 1000 resamples that yielded correlations with a different sign from the true
correlation.

Anticipatory reinstatement for a familiar narrative
To determine if the correspondence with the movie was significantly different between the memory and no-memory conditions, we
created null groups by averaging together a random half of the no-memory subjects with a random half of memory subjects, and then
averaging together the remaining subjects from each group, yielding two group-averaged time courses whose correspondences
should differ only by chance. We calculated a z value based on the correspondence difference for real versus null groups, which
was converted to a p value and then corrected to a false discovery rate q. The analysis using only the narration conditions was per-
formed similarly, computing a z value based on the expected deviation from the diagonal in the real versus null groups.

DATA AND SOFTWARE AVAILABILITY

All of the primary data used in this study are drawn from other papers (Chen et al., 2017; Zadbood et al., 2016), and the ‘‘Interleaved
Stories’’ posterior cingulate cortex data are available on request. Implementations of our event segmentation model, along with simu-
lated data examples, are available on GitHub at https://github.com/intelpni/brainiak (python) and at https://github.com/cbaldassano/
Event-Segmentation (MATLAB).




e5 Neuron 95, 709–721.e1–e5, August 2, 2017
