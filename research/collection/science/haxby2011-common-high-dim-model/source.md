                                                                                                                                 Neuron

                                                                                                                     Article

A Common, High-Dimensional Model
of the Representational Space
in Human Ventral Temporal Cortex
James V. Haxby,1,2,* J. Swaroop Guntupalli,1 Andrew C. Connolly,1 Yaroslav O. Halchenko,1 Bryan R. Conroy,3
M. Ida Gobbini,1,4 Michael Hanke,1 and Peter J. Ramadge3
1Department of Psychological and Brain Sciences, Dartmouth College, Hanover, NH 03755, USA
2Center for Mind/Brain Sciences, Universitá degli studi di Trento, Rovereto 38068, Italy
3Department of Electrical Engineering, Princeton University, Princeton, NJ 08544, USA
4Dipartimento di Psicologia, Universitá di Bologna, Bologna 40127, Italy

*Correspondence: james.v.haxby@dartmouth.edu
DOI 10.1016/j.neuron.2011.08.026




SUMMARY                                                                 feature in the distributed pattern. We refer to this response-
                                                                        pattern vector space as a representational space. Features can
We present a high-dimensional model of the repre-                       be single-neuron recordings, local field potentials, or imaging
sentational space in human ventral temporal (VT)                        measures of aggregate local neural activity, such as voxels in
cortex in which dimensions are response-tuning func-                    functional magnetic resonance imaging (fMRI). MVP analysis
tions that are common across individuals and patterns                   exploits variability in response-tuning profiles across these fea-
of response are modeled as weighted sums of basis                       tures to classify and characterize the distinctions among re-
                                                                        sponses to different stimuli (Norman et al., 2006; Haynes and
patterns associated with these response tunings.
                                                                        Rees, 2006; O’Toole et al., 2007; Kriegeskorte et al., 2008a).
We map response-pattern vectors, measured with                          Because establishing feature correspondence across brains is
fMRI, from individual subjects’ voxel spaces into this                  difficult, a new classifier model generally is built for each brain.
common model space using a new method, ‘‘hypera-                        Consequently, no general model of the representational space
lignment.’’ Hyperalignment parameters based on re-                      in VT cortex exists that uses a common set of response-tuning
sponses during one experiment—movie viewing—                            functions and can account for the fine-grained distinctions
identified 35 common response-tuning functions                          among neural representations in VT cortex for a wide range of
that captured fine-grained distinctions among a wide                    visual stimuli.
range of stimuli in the movie and in two category                          Representational distinctions among complex visual stimuli
perception experiments. Between-subject classifica-                     are embedded in topographies in VT cortex that have coarse-
tion (BSC, multivariate pattern classification based                    to-fine spatial scales. Large-scale topographic features that
                                                                        are fairly consistent across individuals reflect coarser categorical
on other subjects’ data) of response-pattern vectors
                                                                        distinctions, such as animate versus inanimate categories in
in common model space greatly exceeded BSC of
                                                                        lateral to medial VT cortex (Caramazza and Shelton, 1998; Chao
anatomically aligned responses and matched within-                      et al., 1999; Hanson et al., 2004; Kriegeskorte et al., 2008b;
subject classification. Results indicate that population                Mahon and Caramazza, 2009), faces versus objects and body
codes for complex visual stimuli in VT cortex are                       parts versus objects (the fusiform face and body-parts areas,
based on response-tuning functions that are common                      FFAs and FBAs, respectively; Kanwisher et al., 1997; Peelen
across individuals.                                                     and Downing, 2005; Kriegeskorte et al., 2008b), and places
                                                                        versus objects (the parahippocampal place area, PPA; Epstein
                                                                        and Kanwisher, 1998). Finer distinctions among animate cate-
INTRODUCTION                                                            gories, among mammalian faces, among buildings, and among
                                                                        objects appear to be carried by smaller-scale topographic fea-
Representations of complex visual stimuli in human ventral              tures, and an arrangement of these features that is consistent
temporal (VT) cortex are encoded in population responses that           across brains has not been reported (Haxby et al., 2001; Cox
can be decoded with multivariate pattern (MVP) classification           and Savoy, 2003; Brants et al., 2011). MVP analysis can detect
(Haxby et al., 2001; Spiridon and Kanwisher, 2002; Cox and              the features that underlie these representational distinctions at
Savoy, 2003; Tsao et al., 2003, 2006; Hanson et al., 2004;              both the coarse and fine spatial scales, whereas conventional
O’Toole et al., 2005; Hung et al., 2005; Kiani et al., 2007; Reddy      univariate analyses are sensitive only to the coarse spatial scale
and Kanwisher, 2007; Op de Beeck et al., 2010; Brants et al.,           topographies. Current models of the functional organization of
2011). Population responses are patterns of neural activity. For        VT cortex that are based on response-tuning functions defined
MVP analysis, patterns of activity are analyzed as vectors in           by simple contrasts, such as faces versus objects or scenes
a high-dimensional space in which each dimension is a local             versus objects, and on relatively large category-selective regions,


404 Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc.
Neuron
Common Model of Human Ventral Temporal Cortex




such as the FFA and PPA (Kanwisher et al., 1997; Epstein and          were needed to achieve this level of accuracy. Here we present
Kanwisher, 1998; Kanwisher, 2010; Lashkari et al., 2010), fail to     a common model space with 35 dimensions. Thus, the represen-
capture the fine-grained distinctions among responses to a            tational space in VT cortex can be modeled with response-tuning
wide range of stimuli and the fine spatial scale of the response      functions that are common across subjects. These response-
patterns that carry those distinctions.                               tuning functions are associated with cortical topographies that
   Here we present a high-dimensional model of the representa-        serve as basis patterns for modeling patterns of response to
tional space in VT cortex that is based on response-tuning func-      stimuli and can be examined in each individual’s VT cortex.
tions that are common across brains and is valid across a wide        The general validity of the model across the varied stimulus
range of complex visual stimuli. To construct this model, we          sets that we tested could be achieved only when hyperalignment
developed a method, hyperalignment, which aligns patterns of          was based on responses to the movie. Common models based
neural response across subjects into a common, high-dimen-            on responses to smaller, more controlled stimulus sets—still
sional space. We estimated the hyperalignment parameters              images of a limited number of categories—were valid only for
that transform an individual’s VT voxel space into this common        restricted stimulus domains, indicating that these models cap-
space based on responses obtained with fMRI while subjects            tured only a subspace of the substantially larger representational
watched a full-length action movie, Raiders of the Lost Ark. We       space in VT cortex.
reasoned that estimation of hyperalignment parameters that
are valid for a large domain of complex visual stimuli would          RESULTS
require sampling responses to a wide range of stimuli. Viewing
a natural movie evokes local brain responses that show syn-           In our first experiment, we collected functional brain images while
chrony across subjects in a large expanse of cortex, including        21 subjects watched a full-length action movie, Raiders of the
visual areas in the occipital, ventral temporal, and lateral          Lost Ark. In a second experiment, we measured brain activity
temporal cortices (Hasson et al., 2004; Bartels and Zeki, 2004;       while ten of these subjects, at Princeton University, looked at still
Sabuncu et al., 2010). In contrast to earlier univariate analyses     images of seven categories of faces and objects—male faces,
of local synchrony, we took a multivariate approach to analyze        female faces, monkey faces, dog faces, shoes, chairs, and
the time-varying patterns of response evoked by this rich,            houses. In a third experiment, we measured brain activity while
dynamic stimulus. We reasoned that in the brains of two individ-      the other 11 subjects, at Dartmouth College, looked at still
uals viewing the same dynamic visual stimulus, such as a full-        images of six animal species—ladybugs, luna moths, yellow-
length action movie, the trajectories of VT response-pattern          throated warblers, mallards, ring-tailed lemurs, and squirrel
vectors over time reflect similar visual information, but the coor-   monkeys.
dinate systems for their respective representational spaces, in          Hyperalignment uses the Procrustean transformation
which each dimension is one voxel, are poorly aligned. Hypera-        (Schönemann, 1966) to align individual subjects’ VT voxel
lignment uses Procrustean transformations (Schönemann, 1966)         spaces into a common space (Figure 1). Individual voxel spaces
iteratively over pairs of subjects to derive a group coordinate       and the common space are high dimensional, unlike the three-
system in which subjects’ vector trajectories are in optimal align-   dimensional anatomical spaces. The Procrustean transforma-
ment. The Procrustean transformation is an orthogonal transfor-       tion finds the optimal orthogonal matrix for a rigid rotation with
mation (rotations and reflections) that minimizes the Euclidean       reflections that minimizes Euclidean distances between two
distance between two sets of paired vectors. After hyperalign-        sets of labeled vectors. For hyperalignment, labeled vectors
ment, we reduced the dimensionality of the common space by            are patterns of response for time points in an fMRI experiment,
performing a principal components analysis (PCA) and deter-           and the Procrustean transformation rotates (with reflections)
mined the subspace that is sufficient to capture the full range       the high-dimensional coordinate axes for each subject to align
of response-pattern distinctions.                                     pattern vectors for matching time points. After rotation, coordi-
   We tested the validity of the common model by performing           nate axes, or dimensions, in the common space are no longer
between-subject MVP classification of responses to a wide             single voxels with discrete cortical locations but, rather, are
range of visual stimuli—time segments from the movie and still        distributed patterns across VT cortex (weighted sums of voxels).
images of seven categories of faces and objects and six animal        Minimizing the distance between subjects’ time-point response-
species. For between-subject classification (BSC), the response       pattern vectors also makes time-series responses for each
vectors for one subject were classified using a classifier model      common space dimension maximally similar across subjects
based on other subjects’ response vectors. We compared                (see Figure S2A available online). First, the voxel spaces for
BSC performance for response vectors that had been trans-             two subjects were brought into optimal alignment. We then
formed into the common model space to BSC for data that               brought a third subject’s voxel space into optimal alignment
were aligned across subjects based on anatomy and to within-          with the mean trajectory for the first two subjects and proceeded
subject classification (WSC), in which the response vectors for       by successively bringing each remaining subject’s voxel space
a subject were classified using an individually tailored classifier   into alignment with the mean trajectory of response vectors
model based on response vectors from the same subject.                from previous subjects. In a second iteration, we brought each
Results showed that BSC accuracies for response-pattern vec-          individual subject’s voxel space into alignment with the group
tors in common model space were markedly higher than BSC              mean trajectory from the first iteration and recalculated the
accuracies for anatomically aligned response-pattern vectors          group mean vector trajectory. In the third and final step, we re-
and equivalent to WSC accuracies. More than 20 dimensions             calculated the orthogonal matrix that brought each subject’s


                                                                        Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc. 405
                                                                                                                                             Neuron
                                                                                          Common Model of Human Ventral Temporal Cortex




                                                                                    of evoked patterns from short time segments in the other half
                                                                                    of the movie, as compared to other possible time segments of
                                                                                    the same length. The data used for BSC of time segments in
                                                                                    one half of the movie was not used for voxel selection or deriva-
                                                                                    tion of hyperalignment parameters (Kriegeskorte et al., 2009).
                                                                                    For the category perception experiments, we used the hypera-
                                                                                    lignment parameters derived from the entire movie data to trans-
                                                                                    form each subject’s VT responses to the category images into
                                                                                    the common space and tested whether BSC could identify the
                                                                                    stimulus category being viewed. As a basis for comparison, we
                                                                                    also performed BSC on data that had been aligned based on
                                                                                    anatomy, using normalization to the Talairach atlas (Talairach
                                                                                    and Tournoux, 1988). For the category perception experiments,
                                                                                    we also compared BSC to within-subject classification (WSC), in
                                                                                    which individually tailored classifiers were built for each subject.
                                                                                    Because each movie time segment was unique, WSC of movie
                                                                                    time segments was not possible. Voxel sets were selected
                                                                                    based on between-subject correlations of movie time series
                                                                                    (see Supplemental Experimental Procedures). BSC accuracies
                                                                                    were relatively stable across a wide range of voxel set sizes.
                                                                                    We present results for analyses of 1,000 voxels (500 per hemi-
Figure 1. Schematic of the Procedure for Building a High-Dimen-
                                                                                    sphere). See Figures S3A and S3B for results using other voxel
sional Common Model                                                                 set sizes.
The upper box shows the input data before any transformations—separate                 We used a one-nearest neighbor classifier based on vector
matrices of 500 voxels in the VT cortex of each hemisphere with time-series         correlations for BSC of 18 s segments of the movie (six time
data for each of 21 subjects. The middle box represents the data structures         points, TR = 3 s). An individual’s response vector to a specific
after hyperalignment. For each subject there is a matrix of time-series data that
                                                                                    time segment was correctly classified if the correlation of that
has been rotated (with reflections) into the common, 500-dimensional space
                                                                                    response vector with the group mean response vector (ex-
for the VT cortex of each hemisphere with an orthogonal matrix—the hyper-
alignment parameters—that specifies that transformation. The mean time-             cluding that individual) for the same time segment was higher
series data in the common spaces—2 matrices with 500 dimensions 3 2,205             than all correlations of that vector with group mean response
time points—are the targets for hyperalignment. The lower box represents the        vectors for more than 1,000 other time segments of equal length.
data structures after dimensionality reduction. PCA was performed on the            Other time segments were selected using a sliding time window,
mean time-series data from all 1,000 dimensions (right and left VT cortices),       and those that overlapped with the target time segment were
and the top 35 PCs were found to afford BSC that was equivalent to BSC of the
                                                                                    excluded from comparison. After hyperalignment, BSC identi-
1,000-dimensional hyperaligned data and to WSC. For each subject, there is
a matrix of time series for each PC (35 PCs 3 2,205 time points) and part of an     fied these segments correctly with 70.6% accuracy (SE =
orthogonal matrix (35 PCs 3 1,000 voxel weights) that can be used to trans-         2.6%, chance < 1%; Figure 2). After anatomical alignment, the
form any data from the same 1,000 VT voxels into the common model space.            same time segments could be classified with 32.0% accuracy
See also Figure S1.                                                                 (SE = 2.5%), a level of accuracy that was better than chance
                                                                                    but far lower than after hyperalignment (p < 0.001).
VT voxel space into optimal alignment with the final group mean                        We used a linear support vector machine (SVM) for BSC of
vector trajectory. The orthogonal matrix for each subject was                       both category perception experiments. After hyperalignment
then treated as that subject’s ‘‘hyperalignment parameters,’’                       using parameters derived from the movie data, BSC identified
which we used to transform data from independent experiments                        the seven face and object categories with 63.9% accuracy
into the common space.                                                              (SE = 2.2%, chance = 14.3%; Figure 2A). The confusion matrix
                                                                                    (Figure 2B) shows that the classifier distinguished human faces
Between-Subject Classification after Hyperalignment                                 from nonhuman animal faces and monkey faces from dog faces
Based on Responses to the Movie                                                     but could not distinguish human female from male faces. The
We calculated a common space for all 21 subjects based on                           classifier also could distinguish chairs, shoes, and houses. Con-
responses to the movie (Figure 1, middle). We performed BSC                         fusions between face and object categories were rare. WSC
of response patterns from all three data sets to test the validity                  accuracy (63.2% ± 2.1%) was equivalent to BSC of hyperaligned
of this space as a common model for the high-dimensional re-                        data with a similar pattern of confusions, but BSC of anatomi-
presentational space in VT cortex. With BSC, we tested whether                      cally aligned data (44.6% ± 1.4%) was significantly worse
a given subject’s response patterns could be classified using an                    (p < 0.001; Figure 2).
MVP classifier trained on other subjects’ patterns. For BSC of the                     After hyperalignment using parameters derived from the movie
movie data, we used hyperalignment parameters derived from                          data, BSC identified the six animal species with 68.0% accuracy
responses to one half of the movie to transform each subject’s                      (SE = 2.8%, chance = 16.7%; Figure 2A). The confusion matrix
VT responses to the other half of the movie into the common                         shows that the classifier could identify each individual species
space. We then tested whether BSC could identify sequences                          and that confusions were most often made within class, i.e.,


406 Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc.
Neuron
Common Model of Human Ventral Temporal Cortex




Figure 2. Results of MVP Classification Analyses of Data from Three Experiments
(A) Classification accuracies (means ± SE) for BSC of data that have been mapped into the 1,000-dimensional common space with hyperalignment, into the
35-dimensional common model space, and into Talairach atlas space (anatomically aligned), as well as for WSC of the category perception experiments. Dashed
lines indicate chance performance.
(B) Confusion matrices for the category perception experiments for the same MVP classifications. See also Figure S2.



between insects, between birds, or between primates. WSC                       varying numbers of top principal components (PCs). The results
accuracy (68.9% ± 2.8%) was equivalent to BSC of hyperaligned                  show that BSC accuracies for all three data sets continue to
data with a similar pattern of confusions. BSC of anatomically                 increase with more than 20 PCs (Figure 3A). We present results
aligned animal species data (37.4% ± 1.5%) showed an even                      for a common model space with 35 dimensions, which affords
larger decrement relative to BSC of hyperaligned data than                     BSC classification accuracies that are equivalent to BSC accu-
that found for the face and object perception data (p < 0.001).                racies using all 1,000 original dimensions (68.3% ± 2.6% versus
                                                                               70.6% ± 2.6% for movie time segments; 64.8% ± 2.3%
Reducing the Dimensionality of the Common Space                                versus 63.9% ± 2.2% for faces and objects; 67.6% ± 3.1%
We next asked how many dimensions are necessary to capture                     versus 68.0% ± 2.8% for animal species; Figure 2A). The effect
the information that enables these high levels of BSC accuracy                 of number of PCs on BSC was similar for models that were
(Figure 1). We performed a principal components analysis (PCA)                 based only on Princeton (n = 10) or Dartmouth (n = 11) data, sug-
of the mean responses to each movie time point in common                       gesting that this estimate of dimensionality is robust across
model space, averaging across subjects, then performed BSC                     differences in scanning hardware and scanning parameters
of the movie, face and object, and animal species data with                    (see Figure S3D).


                                                                                  Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc. 407
                                                                                                                                                      Neuron
                                                                                          Common Model of Human Ventral Temporal Cortex




                                                                                   Figure 4. Comparison of Common Models Based on Responses to
                                                                                   the Movie and on Responses to Still Images
                                                                                   We compared BSC accuracies (means ± SE) for data in the common model
                                                                                   space based on movie viewing relative to common model spaces based on
                                                                                   responses to the images in the category perception experiments. Note that
                                                                                   common models based on responses to the category images afford good BSC
                                                                                   for those experiments but do not generalize to BSC of responses to movie time
                                                                                   segments. Only the common model based on movie viewing generalizes to
                                                                                   high levels of BSC for stimuli from all three experiments. Dashed lines indicate
                                                                                   chance performance. See also Figure S4.



                                                                                   the movie time segments (49.5% ± 2.6%; Figure 3B). Thus,
                                                                                   the lower-dimensional representational spaces for the limited
                                                                                   number of stimulus categories in the face and object experiment
                                                                                   and in the animal species experiment are different from each
Figure 3. BSC Accuracies after Dimensionality Reduction                            other and are of less general validity than the higher-dimensional
Accuracies are shown as means ± SE.
                                                                                   movie-based common model space.
(A) BSC for 18 s movie time segments, the face and object categories, and the
animal species for different numbers of PCs.
(B) BSC for 35 PCs that were calculated based on responses during movie            Hyperalignment and Between-Subject Classification
viewing, for ten PCs that were calculated based on responses to the face and       within Experiments
object images, and for ten PCs that were calculated based on responses to the      We next asked whether a complex, natural stimulus, such as the
animal images. Note that only the 35 PCs based on responses to the movie           movie, is necessary to derive hyperalignment parameters that
afforded high levels of BSC for stimuli from all three experiments. Dashed lines
                                                                                   generate a common space with general validity across a wide
indicate chance performance. See also Figure S3.
                                                                                   range of complex visual stimuli. In principle, a common space
                                                                                   and hyperalignment parameters can be derived from any fMRI
   We next asked whether the information necessary for classifi-                   time series. We investigated whether hyperalignment of the
cation of stimuli in the two category perception experiments                       face and object data and hyperalignment of the animal species
could be captured in smaller subspaces and whether these                           data would afford high levels of BSC accuracy using only the
subspaces were similar. For each experiment, we performed                          data from those experiments. In each experiment, we derived
PCAs on mean category vectors for each run, averaged across                        a common space based on all runs but one. We transformed
subjects, in the common model space derived from the movie                         the data from all runs, including the left-out run, into this common
data, then used these PCs for BSC. Data folding, i.e., division                    space. We trained the classifier on those runs used for hypera-
of data into training and testing sets, ensured that generalization                lignment in all subjects but one and tested the classifier on the
testing was done on data that were not used for hyperalignment                     data from the left-out run in the left-out subject. Thus, the test
or classifier training (Kriegeskorte et al., 2009). BSC of the face                data for determining classifier accuracy played no role either in
and object categories reached a maximal level with the top 12                      hyperalignment or in classifier training (Kriegeskorte et al., 2009).
PCs from the PCA of the face and object data (67.7% ± 2.1%).                          BSC of face and object categories after hyperalignment based
BSC of the animal species reached a maximal level with the                         on data from that experiment was equivalent to BSC after movie-
top nine PCs from the PCA of the animal species data                               based hyperalignment (62.9% ± 2.9% versus 63.9% ± 2.2%,
(73.9% ± 3.0%). The top PCs from the face and object data,                         respectively; Figure 4). Surprisingly, BSC of the animal species
however, did not afford good classification of the animal species                  after hyperalignment based on data from that experiment was
(55.0% ± 3.4%) or the movie time segments (50.1% ± 2.7%), nor                      significantly better than BSC after movie-based hyperalignment
did the top PCs from the animal species data afford good clas-                     (76.2% ± 3.7% versus 68.0% ± 2.8%, respectively; p < 0.05;
sification of the face and object categories (54.2% ± 2.6%) or                     Figure 4). This result suggests that the validity for a model of


408 Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc.
Neuron
Common Model of Human Ventral Temporal Cortex




a specific subspace may be enhanced by designing a stimulus             place, and body-part selectivity that have dominated most
paradigm that samples the brain states in that subspace more            investigations into the functional organization of VT cortex.
extensively.                                                            Each dimension is associated with a response-tuning function
   We next asked whether hyperalignment based on these                  that is common across brains and with individual-specific cor-
simpler stimulus sets was sufficient to derive a common space           tical topographies. The dimensions have meaning in aggregate
with general validity across a wider array of complex stimuli.          as a computational framework that captures the distinctions
We applied the hyperalignment parameters derived from the               among VT representations for a diverse set of complex visual
face and object data to the movie data in the ten Princeton             stimuli, but their meaning in isolation is less clear. The coordinate
subjects and the hyperalignment parameters derived from the             axes for this space, however, can be rotated to search for dimen-
animal species data to the movie data in the 11 Dartmouth               sions that have clearer meaning, in terms of response-tuning
subjects. BSC of 18 s movie time segments after hyperalignment          function, and the cortical topographies for dimensions in a
based on category perception experiment data was markedly               rotated model space can be examined. Here we probe the
worse than BSC after hyperalignment based on movie data                 meaning of the common model space. First we examine the
(17.6% ± 1.3% versus 65.8% ± 2.7% for Princeton subjects;               response-tuning functions and cortical topographies for four of
28.3% ± 2.8% versus 74.9% ± 4.1% for Dartmouth subjects;                the top five PCs. In the next section, we illustrate how to derive
p < 0.001 in both cases; Figure 4). Thus, hyperalignment of             a dimension based on a simple stimulus contrast—faces versus
data using a set of stimuli that is less diverse than the movie is      objects—and examine the associated cortical topographies. We
effective, but the resultant common space has validity that is          show that the cortical topographies associated with well-known
limited to a small subspace of the representational space in VT         category selectivities are preserved in the 35-dimensional com-
cortex.                                                                 mon model space.
   We conducted further analyses to investigate the properties of          Individual VT voxel spaces can be transformed into the
responses to the movie that afford general validity across a wide       common model space with a single parameter matrix (the first
range of stimuli. We tested BSC of single time points in the movie      35 columns of an orthogonal matrix; Figure 1; Figure S1A).
and in the face and object perception experiment, in which we           Each common model space dimension is associated with a
carefully matched the probability of correct classifications for        time-series response for each experiment. A response-tuning
the two experiments. Single TRs in the movie experiment could           profile for an individual voxel is modeled as a weighted sum of
be classified with accuracies that were more than twice that            these 35 response-tuning functions (Figure S1E). Each dimen-
for single TRs in the category perception experiment (74.5% ±           sion is also associated with a topographic pattern in each indi-
2.5% versus 32.5% ± 1.8%; chance = 14%; Figure S4A). This               vidual subject’s VT voxel space (Figure S1C), and the response
result suggests that VT responses evoked by the cluttered,              pattern for a stimulus is modeled as a weighted sum of these
complex, and dynamic images in the movie are more distinctive           35 patterns (Figure S1D).
than are responses evoked by still images of single faces or               Figure 5A shows the response-tuning functions of four PCs—
objects.                                                                the first, second, third, and fifth PCs—for the face, object, and
   We also tested whether the general validity of the model space       animal species categories. These PCs are derived from time-
reflects responses to stimuli that are in both the movie and the        series responses to the movie, but within the model space they
category perception experiments or reflects stimulus properties         also are associated with distinct profiles of responses to stimuli
that are not specific to these stimuli. We recomputed the com-          in the category perception experiments (Figure S1B). The first
mon model after removing all movie time points in which a               and fifth PCs reflect stronger responses for faces as compared
monkey, a dog, an insect, or a bird appeared. We also removed           to objects. The first PC, however, is selective for human faces
time points for the 30 s that followed such episodes to factor out      with negative responses to all animal species, whereas the fifth
effects of delayed hemodynamic responses. BSC of the face and           PC has positive responses to both human and nonhuman animal
object and animal species categories, including distinctions            faces and positive responses to all animal species. The second
among monkeys, dogs, insects, and birds, was not affected by            and third PCs, by contrast, are associated with stronger
removing these time points from the movie data (65.0% ± 1.9%            responses to the objects than to faces. The second PC reflects
versus 64.8% ± 2.3% for faces and objects; 67.1% ± 3.0%                 a stronger response to houses than to small objects, whereas
versus 67.6% ± 3.1% for animal species; Figure S4B). This result        the third PC reflects a stronger response to small objects.
suggests that the movie-based hyperalignment parameters                    Figure 5B shows the VT topographies in two subjects for these
that afford generalization to these stimuli are not stimulus specific   four PCs. The locations of the individually defined FFA and PPA
but, rather, reflect stimulus properties that are more abstract and     (Kanwisher et al., 1997; Epstein and Kanwisher, 1998) are super-
of more general utility for object representations.                     imposed as white and black outlines, respectively, to provide an
                                                                        additional reference for functional topography. Each PC has
Common Model Dimensions: Response-Tuning                                a distinct topography, and these topographies are consistent,
Functions and Cortical Topographies                                     but not identical, across subjects, as evident in this pair of
The dimensions that define the common model space are                   subjects. The topographies of these PCs show only a rough
selected as those that most efficiently account for variance in         correspondence with the outlines of the FFA and PPA. For
patterns of response to the movie. The model space has a dimen-         example, the first PC, whose tuning profile showed positive
sionality that is much lower than that of the original voxel space      responses only for human faces, has positive weights only in
but much higher than the handful of binary contrasts for face,          small subregions of the FFA. The fifth PC, whose tuning profile


                                                                          Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc. 409
                                                                                                                                                   Neuron
                                                                                        Common Model of Human Ventral Temporal Cortex




Figure 5. Response-Tuning Profiles and Cortical Topographies for Common Model PCs
(A) Category response-tuning profiles for the first, second, third, and fifth PCs in the common model space. These PCs were derived to account for variance of
responses to the movie, but they also are associated with differential responses to the categories in the other two experiments. The scale for response-tuning
profiles is centered on zero, corresponding to the mean response to the movie, and scaled so that the maximum deviation from zero (positive or negative) is set
to one.
(B) The cortical topographies for the same PCs projected into the native voxel spaces of two subjects as the voxel weights for each PC in the matrix of
hyperalignment parameters for each subject. The outlines of individually defined face-selective (FFA) and house-selective (PPA) regions are shown for reference.
See also Figure S5.



showed positive responses to both human and nonhuman                             natural stimulus, did not correspond well with the category-
animal faces, has positive weights in most, but not all, of the                  selective regions, the FFA and PPA, that are identified based
FFA, including the same subregions that had positive weights                     on responses to still images of a limited variety of stimuli. We
for the first PC, as well as in more posterior VT regions outside                next asked whether the category selectivity that defines these
of the FFA. The second PC, which was associated with stronger                    regions is preserved in the 35-dimensional representational
responses to objects—especially houses—than faces, has only                      space of our model. First, we defined a dimension in the model
negative weights in the FFA and only positive weights in the                     space based on a linear discriminant that contrasts the mean
PPA, but the topography of positive responses extends into                       response vector to faces and the mean response vector to
a much larger region of medial VT cortex. By contrast, the third                 houses and objects. The mean response vectors were based
PC, which also was associated with stronger responses to                         on group data in the face and object perception experiment.
objects than faces but with a preference for small objects over                  We then plotted the voxel weights for this dimension in the native
houses, has a mixture of positive and negative weights in both                   anatomical spaces for individual subjects (Figure 6A; Figure S1F).
the FFA and PPA, with stronger positive weights in cortex                        Unlike the topographies for principal components, the voxel
between these regions and in the inferior temporal gyrus.                        weights for this faces-versus-objects dimension have a topog-
   Overall, these results show that the PCA-defined dimensions                   raphy that corresponds well with the boundaries of individually
capture a functional topography in VT cortex that has more                       defined FFAs. Thus, when the response-tuning profiles are
complexity and a finer spatial scale than that defined by large                  modeled with this single dimension, the face selectivity of FFA
category-selective regions such as the FFA and PPA.                              voxels is evident, but this dimension does not capture the fine-
                                                                                 scale topography in the FFA that is the basis for decoding finer
Category-Selective Dimensions and Regions                                        distinctions among faces or among nonface objects. By con-
in the Common Model                                                              trast, the dimensions in the common model do capture these
The topographies for the PCs in the common model that best                       distinctions. MVP analysis restricted to the FFA affords signifi-
capture the variance in responses to the movie, a complex                        cant classification of human faces versus animal faces, dog


410 Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc.
Neuron
Common Model of Human Ventral Temporal Cortex




                                                                                     Figure 6. Contrast-Defined Category-Selective
                                                                                     Profiles in the Common Model Space Projected
                                                                                     into the Native Voxel Spaces of Two Subjects
                                                                                     (A) The topography associated with the contrast between
                                                                                     mean response to faces as compared to the mean re-
                                                                                     sponse to nonface objects (houses, chairs, and shoes).
                                                                                     Note the tight correspondence of the regions with positive
                                                                                     weights and the outlines of individually defined FFAs.
                                                                                     (B) FFA and PPA regions defined by contrasts in group
                                                                                     data projected into the native voxel spaces of two sub-
                                                                                     jects. For each subject, that subject’s own data were
                                                                                     excluded from the calculation of face selectivity and house
                                                                                     selectivity, yielding category-selective regions that were
                                                                                     based exclusively on other subjects’ data. Each subject’s
                                                                                     individually defined FFAs and PPAs are shown as outlines
                                                                                     to illustrate the tight correspondence with model-defined
                                                                                     category-selective regions.




faces versus monkey faces, and even shoes versus chairs.            the representational space in VT cortex that is valid across
Moreover the topography within the FFA that enables decoding        brains.
these distinctions can be captured with common basis functions         We also investigated whether we could build a single model
when hyperalignment is restricted to individually defined FFA       that was not only valid across brains, but also valid across
voxels (Figure S2E).                                                a wide range of complex visual stimuli. To this end, we used
  We then asked whether the category-selective FFA and PPA          a complex and dynamic natural stimulus—a full-length action
could be identified reliably in the common model space. For         movie—to sample a diverse variety of representational states.
each subject, we projected all other subjects’ face and object      The results show that hyperalignment based on responses to
data in the 35-dimensional common model space into that             this stimulus affords a single model of VT cortex with general
subject’s 1,000 voxel native space. We then identified face-        validity across a broad range of stimuli, whereas hyperalignment
selective and house-selective regions in that subject’s VT cortex   based on responses to still images in more controlled, conven-
based solely on other subjects’ data. Figure 6B shows group-        tional experiments does not. Thus, by virtue of the rich diversity
defined FFAs and PPAs in two representative subjects. The           of a complex, natural stimulus, our model of the representational
outlines of the individually defined FFA and PPA are super-         space in VT cortex also has general validity across stimuli.
imposed on the group-defined regions to illustrate the close           Initially, the common space produced with hyperalignment
correspondence. Thus, the common model also captures the            has the same number of dimensions as the number of voxels
individual-specific anatomical locations of category-selective      in each individual’s native space. We asked how many distinct
regions within the VT cortex.                                       common response-tuning functions are needed to contain the
                                                                    information that affords the full range of fine-grained distinctions
DISCUSSION                                                          among complex, visual stimuli. We tested the sufficiency of
                                                                    lower-dimensional subspaces and found that BSC accuracies
The objective of this research project was to develop a model       continued to increase with more than 20 common response-
of the representational space in VT cortex that (1) is based on     tuning functions. We present a 35-dimensional common model
response-tuning functions that are common across brains and         space that afforded BSC for all three experiments at levels of
(2) captures the fine-scale distinctions among representations      accuracy that were equivalent to BSC with all 1,000 hyperaligned
of complex stimuli that, heretofore, have only been captured        dimensions or WSC with 1,000 voxels. Ten dimensions were
by within-subject analyses using MVP classification. To meet        sufficient within the limited stimulus domains of each category
this objective, we developed a method, hyperalignment, which        perception experiment, but these sets of ten dimensions did
maps data from individual subjects’ native voxel spaces into a      not afford high levels of BSC for the other experiment or for the
common, high-dimensional space. The dimensions in this com-         movie. Thus, these lower-dimensional models are subspaces
mon space are basis functions that are distinct response-tuning     of the full model and are valid only for more limited stimulus
functions defined by their commonality across brains. Model         domains.
dimensions also are associated with topographic patterns in
each subject’s native voxel space. Our results show that trans-     Modeling the Representational Space in VT Cortex
formation of response vectors into common space coordinates         with Common Basis Functions
affords between-subject MVP classification of subtle distinc-       Hyperalignment uses the Procrustean transformation to rotate
tions among complex visual stimuli at levels of accuracy that       and reflect the coordinate axes for an individual’s voxel space
far exceed BSC based on anatomically aligned voxels and are         into a common coordinate system in which the response vectors
equivalent to, and can even exceed, WSC. Hyperalignment             for the same stimuli or events are in optimal alignment across
thus makes it possible to build a high-dimensional model of         subjects. Principal components analysis is then used to rotate


                                                                      Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc. 411
                                                                                                                               Neuron
                                                                           Common Model of Human Ventral Temporal Cortex




the common space into a new coordinate system that is ordered        associated topographies, and the outlines of category-selective
by variance accounted for, and the common space is reduced to        regions are preserved in the common model and can be ex-
the top components that afford high levels of BSC. This pro-         tracted with high fidelity. Such category selectivities, however,
cedure produces a parameter matrix for each subject that trans-      do not account for a majority of the variance in VT responses
forms that subject’s data into model space coordinates (bottom       to natural, dynamic stimuli. Moreover, single dimensions that
square in Figure 1; Figure S1A).                                     define category-selective regions cannot model the fine-grained
   The parameter matrix for each subject can be applied to trans-    variations in response topographies within the FFA and PPA that
form a different set of response-pattern vectors, using the same     are modeled well by weighted sums of model dimensions and
voxels in that subject, into the common model space (Fig-            afford classification of responses to a wide range of stimulus
ure S1B). This step models the patterns of response to new stim-     distinctions (see Figure S2E).
ulus conditions as weighted sums of the same basis patterns             Single-neuron response-tuning profiles in monkey inferior
that model the responses to stimuli that were used to develop        temporal cortex (IT) reflect complex object features, and pat-
the common space. In our principal analysis, model dimensions        terns of responses over a population represent object categories
were defined by common differential responses to time points in      and identities (Logothetis and Sheinberg, 1996; Tanaka, 2003;
the movie. Rotating the response-pattern vectors for the cate-       Hung et al., 2005; Tsao et al., 2006; Freiwald et al., 2009; Serre
gory perception experiments into these dimensions afforded           et al., 2007; Kiani et al., 2007). IT response-tuning profiles
BSC of those categories at levels of accuracy that are equiva-       show a variety that appears open ended and, to our knowledge,
lent to WSC and allowed us to further characterize the               has not been modeled with response-tuning basis functions
response-tuning profiles for model dimensions in terms of differ-    (with the exception of Freiwald et al. [2009]’s investigation of
ential responses to specific categories of faces, objects, and       response-tuning basis functions for faces). The relationship
animals.                                                             between neuronal-tuning functions and model-basis functions
   The columns in each subject’s hyperalignment parameters           for voxel response profiles is unknown. Population responses
contain information about the topographic patterns for each          in monkey IT, as measured with multiple single-unit recording,
model dimension in the form of voxel weights that can be dis-        and fMRI response patterns in human VT cortex are related (Kiani
played as brain images (Figure 6B; Figure S1C). Patterns of re-      et al., 2007; Kriegeskorte et al., 2008b). Using our methods, the
sponse to single stimuli or time points are modeled as weighted      representational spaces for neuronal population responses and
sums of these patterns (Figure S1D). The topographic patterns        fMRI response patterns could be modeled, preferably with
for each model dimension show some consistency across indi-          data from the same animals, and the form of a transformation
vidual brains but are not identical. No single topography in a       that relates the basis functions for the neuronal space to the
canonical or average brain can capture the fine-scale topogra-       basis functions for the fMRI space could be investigated.
phies that are seen in individual subjects. The primary motivation
for the development of hyperalignment was to find such com-          Complex, Natural Stimuli for Sampling Representational
mon response-tuning functions that are associated with variable      State Spaces
cortical topographies.                                               The second goal of this project was to develop a single model
   The rows in a data matrix contain the model space coordinates     that was valid across stimuli that evoke distinct patterns of
of response-pattern vectors for time points or stimuli. The          response in VT cortex. To this end, we collected three data sets
response profile of a single voxel is modeled as a weighted          for deriving transformations into a common space and testing
sum of the response-tuning functions for dimensions (Fig-            general validity. All data sets could be used to derive the param-
ure S1E). Modeling voxel response profiles as weighted sums          eters for hyperalignment, and all data sets allowed BSC of
of response-tuning basis functions can capture an unlimited          responses to different stimuli.
variety of such profiles. Computational approaches that define          The central challenge was to estimate parameters in each
voxel response profiles as types (Lashkari et al., 2010), rather     subject for a high-dimensional transformation that captures the
than as mixtures of basis functions, cannot model this unlimited     full variety of response patterns in VT cortex. We reasoned that
variation, making them unsuited for modeling fine-grained struc-     achieving such general validity would require sampling a wide
ture in response topographies.                                       range of stimuli that reflect the statistics of normal visual experi-
   The full set of dimensions models topographies that are more      ence. The use of a limited number of stimuli—eight, 12, or even
fine grained than those of category-selective areas for faces        20 categories—constrains the number of dimensions that may
(FFAs) and houses (PPAs; Figure 5B; Figures S5A and S5B).            be derived. We chose the full-length action movie as a varied,
Category-selective areas are defined by simple contrasts, which      natural, and dynamic stimulus that can be viewed during an
are single dimensions in the model space. The single dimension       fMRI experiment (Hasson et al., 2004; Bartels and Zeki, 2004;
that is defined by the contrast between responses to faces           Sabuncu et al., 2010). Parameter estimates derived from
and objects produces individual topographies that correspond         responses to this stimulus produced a common model space
well with the outline of individually defined FFAs (Figure 6A).      that afforded highly accurate MVP classification for all three
Category-selective regions can be defined based on group             experiments. Supplemental analysis of the effect of the number
data that is projected into an individual’s native brain space.      of movie time points used for model derivation indicates that
Group-defined FFAs and PPAs in individual brain spaces corre-        maximal BSC required most of the movie (1,700 time points or
spond well with the regions defined by that subject’s own data       85 min; Figure S2D). This space has a dimensionality that cannot
(Figure 6B). Thus, category-selective response profiles, their       logically be derived from a more limited stimulus set.


412 Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc.
Neuron
Common Model of Human Ventral Temporal Cortex




   By contrast, the responses evoked by the stimuli in the cate-          Previous studies have shown that patterns of response to novel
gory perception experiments did not have these properties.             stimuli—complex natural images (Kay et al., 2008; Naselaris et al.,
We also derived common models based on responses to the                2009) and nouns (Mitchell et al., 2008)—can be predicted based
face and object categories in ten subjects and on responses to         on individually tailored models that predict the response of each
the pictures of animals in 11 subjects. These alternative common       voxel as a weighted sum of stimulus features from high-dimen-
models afforded high levels of accuracy for BSC of the stimulus        sional models of stimulus spaces. Our work presents a more
categories used to derive the common space but did not gener-          general model insofar as it is not limited to any particular stimulus
alize to BSC for the movie time segments. Thus, models based           space. Our model affords predictions of responses to any novel
on hyperalignment of responses to a limited number of stimulus         stimulus based on other subjects’ responses to that stimulus but
categories align only a small subspace within the representa-          cannot predict the response to a novel stimulus that was not pre-
tional space in VT cortex and are, therefore, inadequate as            sented to other subjects. A hybrid that integrates models of stim-
general models of that space. On the positive side, these results      ulus spaces with models of neural representational spaces could
also show that hyperalignment can be used for BSC of an fMRI           make a single prediction, based on neural data pooled across
experiment without data from movie viewing.                            subjects, of the response to a novel stimulus in the common
   Further analyses revealed other desirable properties of the         space, rather than make a new prediction for each subject.
movie as a stimulus for model derivation. The movie evoked
responses in VT cortex that were more distinctive than were            Conclusion
responses to the still images in the category perception experi-       The power and general utility of our model of the high-dimen-
ments. Moreover, the general validity of the model based on            sional representational space in VT cortex come from the deriva-
the responses to the movie is not dependent on responses to            tion of each individual subject’s hyperalignment parameters.
stimuli that are in both the movie and the category perception         These parameters allow new data response vectors in the
experiments but, rather, appears to rest on stimulus properties        same VT voxels to be transformed into the model space coordi-
that are more abstract and of more general utility.                    nate system. The advantage of such a transformation is that the
                                                                       model response-tuning functions are common across brains,
Relationship to Other Work                                             affording group MVP analysis of fMRI data and the potential to
Neural representational spaces also can be aligned across              archive data about the functional organization of an area at a level
brains after they are transformed into similarity structures—the       of detail that was not previously possible. For example, one
full set of pairwise similarities for a stimulus set (Abdi et al.,     could catalog the model coordinates of response vectors for
2009; Kriegeskorte et al., 2008a, 2008b; Connolly et al., in press).   an unlimited variety of stimuli that could be referenced relative
These methods, however, are not inductive in that, unlike hyper-       to new data for MVP classification or representational similarity
alignment, they provide a transformation only of the similarity        analysis (Kriegeskorte et al., 2008a).
spaces for the stimuli in the original experiment. By contrast,           In our results, BSC of hyperaligned data was equivalent to or
hyperalignment parameters provide a general transformation of          exceeded WSC, suggesting a high level of commonality of repre-
voxel spaces that is independent of the stimuli used to derive         sentational spaces across subjects. BSC of hyperaligned data
those parameters and can be applied to data from unrelated             potentially can be improved with an augmented stimulus and
experiments to map any response vector into the common                 by including more subjects in classifier training data (Figure S2C).
representational space.                                                WSC, however, also can be improved by collecting more data.
   Hyperalignment is fundamentally different from our previous         More detailed within-subject analysis should be able to detect
work on functional alignment of cortex (Sabuncu et al., 2010).         idiosyncrasies of individual representational spaces, but demon-
Functional alignment warps cortical topographies, using a              strating such idiosyncrasies and quantifying their role relative to
rubber-sheet warping that preserves topology. By contrast, hy-         factors that are common across individuals require further work.
peralignment rotates data into an abstract, high-dimensional           One also expects to find group differences in representational
space, not a three-dimensional anatomical space. After func-           spaces due to factors such as development, genetics, learn-
tional alignment, each cortical node is a single cortical location     ing, and clinical disorders. Our methods could be adapted to
with a time series that is simply interpolated from neighboring        study such group differences in terms of alterations of model
voxel time series from the original cortical space. In the high-       response-tuning functions.
dimensional common model space, each dimension is associ-
ated with a pattern of activity that is distributed across VT cortex   EXPERIMENTAL PROCEDURES
and with a time series response that is not typical of any single
voxel.                                                                 See Supplemental Experimental Procedures for details regarding subjects,
   Our results differ from previous demonstrations of between-         MRI scanning parameters, data preprocessing, region of interest definition,
subject MVP classification (Poldrack et al., 2009; Shinkareva          and voxel selection. All subjects gave written, informed consent to participate
                                                                       in the study, and all experimental procedures were approved by the appropriate
et al., 2008, 2011), which used only anatomy to align features
                                                                       Institutional Review Boards at Princeton University and Dartmouth College.
and performed MVP analysis on data from the whole brain rather
than restricting analysis to within-region patterns. Such analyses
                                                                       Stimuli and Tasks
mostly reflect coarse patterns of regional activations. By con-        Movie Stimulus
trast, our results demonstrate that BSC of anatomically aligned        For subjects at Princeton, movie viewing was divided into two sessions. In the
data from VT cortex is markedly worse than WSC.                        first session, subjects watched the first 55 min 3 s of the movie. After a short



                                                                          Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc. 413
                                                                                                                                                         Neuron
                                                                                            Common Model of Human Ventral Temporal Cortex




break, during which subjects were taken out of the scanner, the second 55 min        of the second pass, a new vector was calculated at each time point by aver-
36 s of the movie was shown. For subjects at Dartmouth, movie viewing was            aging all subjects’ vectors in the transformed space, which served as refer-
divided into eight parts due to scanner limitations. Each part was approxi-          ence for the next pass. In the final pass, we calculated Procrustean transfor-
mately 14 min 20 s with an overlap of 20 s between adjacent parts (overlapping       mations for each subject that aligned that subject’s voxel space to the
TRs were discarded from the beginning of the runs for analysis). Subjects were       reference space. This pair of transformations, one for each hemisphere of a
shown the first four parts in one session. After a short break, the second four      subject, served as the hyperalignment parameters for that subject.
parts were shown. Movie scenes at the end of fourth part and eighth part were           Procrustean transformation finds the optimal rotation matrix for two sets of
matched to the movie scenes at the end of the first session and the second           vectors that minimizes the sum of squared Euclidean distances between cor-
session of the Princeton movie study. Subjects were instructed simply to             responding vectors in those sets. The Procrustean transformation also derives
watch and listen to the movie and pay attention. The movie was projected             a translation vector, but we did not use this vector because the data for each
with an LCD projector onto a rear projection screen that the subject could           voxel were standardized.
view through a mirror. The soundtrack for the movie was played through               Principal Components Analysis
headphones.                                                                          Movie data from each subject’s left and right hemispheres were projected into
Face and Object Stimuli                                                              the hyperaligned common spaces, and a group mean time-point vector was
In the face and object study, subjects viewed static, grayscale pictures of four     computed for each time point of the movie. Mean movie data from both hemi-
categories of faces (human female, human male, monkeys, and dogs) and                spheres’ hyperaligned common spaces were concatenated, and PCA was
three categories of objects (houses, chairs, and shoes). Images were pre-            performed (princomp in MATLAB) on these data. This gave us 1,000 compo-
sented for 500 ms with 2 s interstimulus intervals. Sixteen images from one          nents, in descending order of their eigenvalues, corresponding to the 1,000
category were shown in each block, and subjects performed a one-back repe-           dimensions of the hyperaligned common space.
tition detection task. Repetitions were different pictures of the same face or       Mapping Pattern Vectors from an Individual’s Voxel Space into the
object. Blocks were separated by 12 s blank intervals. One block of each stim-       Common Model
ulus category was presented in each of eight runs.                                   Patterns of response from any experiment in the same VT voxels of an indi-
Animal Species Stimuli                                                               vidual can be mapped into the common model using that individual’s hypera-
In the animal species study, subjects viewed static, color pictures of six           lignment parameters by multiplying the rows of voxel responses for those time
animal species (ladybug beetles, luna moths, mallard ducks, yellow-throated          points or stimuli with the hyperalignment parameter matrix of that subject (Fig-
warblers, ring-tailed lemurs, and squirrel monkeys). Stimulus images showed          ure S1B). The resulting vectors were the mappings in the common model
full bodies of animals cropped out from the original background and overlaid         space.
on a uniform gray background. Images subtended approximately 10 of visual           Mapping Vectors from the Common Model into Individual Voxel
angle. These images were presented to subjects using a slow event-related            Spaces
design with a recognition memory task. In each event, three images of the            Mapping a vector in the common model space to individuals’ voxels was per-
same species were presented for 500 ms each in succession followed by                formed by applying the inverse transformations from the model space to each
4.5 s of fixation cross. Each trial consisted of six stimulus events for each        subject’s original voxel space using that subject’s hyperalignment parameter
species plus one 6 s blank event (fixation cross only) interspersed with the         matrix. This procedure was used for mapping PCs (Figure S1C), the activations
stimulus events. Each trial was followed by a probe event, and the subject           for a particular stimulus category (Figure S1D), and differential pattern vectors
indicated whether the probe event was identical to any of the events seen            (Figure S1F).
during the trial. Order of events was assigned pseudorandomly. Six trials            Differential Pattern Vectors
were presented in each of ten runs, giving 60 encoding events per species            Patterns of activation for individual stimulus blocks from the face and object
for each subject.                                                                    study were projected into the common model space. A Fisher’s linear discrim-
                                                                                     inant vector was computed over vectors from all subjects and all blocks of
Data Analysis                                                                        the two classes of interest. For the faces minus objects contrast vector, we
Data were preprocessed using AFNI (Cox, 1996; http://afni.nimh.nih.gov). All         combined the vectors of female faces, male faces, monkey faces, and dog
further analyses were performed using MATLAB (version 7.8, MathWorks)                faces into one class and the vectors of chairs, shoes, and houses into another.
and PyMVPA (Hanke et al., 2009; http://www.pymvpa.org). Software for                 Contrast vectors computed in the common model space were projected into
hyperalignment is available as part of PyMVPA (Hanke et al., 2009; http://           individual subjects’ anatomy using the method described above.
www.pymvpa.org), and data from these studies also can be downloaded                  Common Model Functional Localizers
from the PyMVPA website.                                                             Functional localizers based on the common model were computed using data
Hyperalignment                                                                       from face and object study. We excluded the data from the subject we were
Activation in a set of voxels at each time point can be considered as a vector in    computing the localizers for. Patterns of activation for all blocks and all
a high-dimensional Euclidean space with each voxel as one dimension. We call         subjects were projected into the common model space and then into the orig-
this a time-point vector and the space of voxels a voxel space. During movie         inal voxel space of the excluded subject. The common model FFA was defined
viewing, these activation patterns change over time, giving a sequence of            as all contiguous clusters of 20 or more voxels that responded more to faces
time-point vectors that trace a trajectory in the voxel space. Hyperalignment        than to objects at p < 10 10. The common model PPA was defined as all
uses Procrustean transformation to align individual subjects’ voxel spaces to        contiguous clusters of 20 or more voxels that responded more to houses
each other, time point by time point. This was done separately for each hemi-        than to faces at p < 10 10 and more to houses than to small objects at
sphere. A fixed number of top-ranking voxels (500 for main analyses) were            p < 5 3 10 10.
selected from each hemisphere of all subjects. A subject was chosen arbitrarily      Multivariate Pattern Classification
to serve as the reference. The reference subject’s time-point vectors during         Category Classification. For decoding category information from the fMRI
the movie study were taken as the initial group reference. In the first pass,        data, we used a multiclass linear support vector machine (Vapnik, 1995;
the nonreference subjects were iteratively chosen and their time-point vectors       Chang, C.C. and Lin, C.J., LIBSVM, a library for support vector machines,
were aligned to the time-point vectors of the current reference using the            http://www.csie.ntu.edu.tw/cjlin/libsvm; nu-SVC = 0.5, nu = 0.5, epsilon =
Procrustean transformation (procrustes as implemented in MATLAB). After              0.001). For the face and object perception study, fMRI data from the 11th to
each iteration, a new vector was calculated at each time point by averaging          the 26th TR after the beginning of each stimulus block was averaged to repre-
the vectors of the current reference and the current subject in the transformed      sent the response pattern for that category block. There were seven such
space. The final reference time-point vectors after iterating through all subjects   blocks, one for each category in each of the eight runs. For the animal species
in the first pass were the reference for the second pass. In the second pass, we     study, fMRI data from 4 s, 6 s, and 8 s after the stimulus onset was averaged in
computed Procrustean transformations to align each subject’s time-point              each presentation and the data from six presentations of a category in a run
vectors to the corresponding time-point vectors in this reference. At the end        was averaged to represent that category’s response pattern in that run.



414 Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc.
Neuron
Common Model of Human Ventral Temporal Cortex




    WSC of face and object categories was performed by training the SVM             using the Bootstrap and 3-way multidimensional scaling (DISTATIS).
model on the data from seven runs (7 runs 3 7 categories = 49 pattern vectors)      Neuroimage 45, 89–95.
and testing the model on the left-out eighth run (seven pattern vectors) in each    Bartels, A., and Zeki, S. (2004). Functional brain mapping during free viewing of
subject independently. WSC accuracy was computed as the average classifi-           natural scenes. Hum. Brain Mapp. 21, 75–85.
cation accuracy over eight run folds in each of the ten subjects (80 data folds).
                                                                                    Brants, M., Baeck, A., Wagemans, J., and de Beeck, H.P. (2011). Multiple
WSC of animal species categories was performed in the same way with ten run
                                                                                    scales of organization for object selectivity in ventral visual cortex.
folds in each of the 11 subjects (110 data folds).
                                                                                    Neuroimage 56, 1372–1381.
    For BSC of face and object categories, we trained the classifier on the cate-
gory patterns from seven runs in nine subjects (7 runs 3 7 categories 3 9           Caramazza, A., and Shelton, J.R. (1998). Domain-specific knowledge systems
subject = 441 pattern vectors) and then tested the model on the left-out            in the brain the animate-inanimate distinction. J. Cogn. Neurosci. 10, 1–34.
subject’s patterns in the left-out run (seven pattern vectors). We excluded         Chao, L.L., Haxby, J.V., and Martin, A. (1999). Attribute-based neural
the test run from each training data set to avoid any run-specific effects that     substrates in temporal cortex for perceiving and knowing about objects.
could not be included in WSC analyses. BSC accuracy was computed as                 Nat. Neurosci. 2, 913–919.
the averaged classification accuracy over eight run folds in each of the ten        Connolly, A.C., Gobbini, M.I., and Haxby, J.V. Three virtues of similarity-based
subjects (80 data folds). BSC of animal species categories was performed in         multi-voxel pattern analysis. In Understanding Visual Population Codes
the same way with ten run folds in each of the 11 subjects (110 data folds),        (UVPC) - Toward a Common Multivariate Framework for Cell Recording and
each with 540 pattern vectors in the training data (9 runs 3 6 categories 3         Functional Imaging, N. Kriegeskorte and G. Kreiman, eds. (Boston: MIT
10 subjects). We performed the BSC on data that were mapped into the                Press), in press.
common model space and on data that were aligned anatomically in Talairach
                                                                                    Cox, R.W. (1996). AFNI: software for analysis and visualization of functional
atlas space.
                                                                                    magnetic resonance neuroimages. Comput. Biomed. Res. 29, 162–173.
    Movie Time Segment Classification. For BSC of movie time segments, we
used a correlation-based one-nearest neighbor classifier. Voxel selection           Cox, D.D., and Savoy, R.L. (2003). Functional magnetic resonance imaging
and derivation of the common model space used data from one half of the             (fMRI) ‘‘brain reading’’: detecting and classifying distributed patterns of fMRI
movie. Data from the other half were mapped into the common model space             activity in human visual cortex. Neuroimage 19, 261–270.
and used for BSC. In each subject, response patterns for each TR during             Epstein, R., and Kanwisher, N. (1998). A cortical representation of the local
the test half of the movie and the five following TRs were concatenated for         visual environment. Nature 392, 598–601.
an 18 s time segment. BSC of these time segments was performed by calcu-            Freiwald, W.A., Tsao, D.Y., and Livingstone, M.S. (2009). A face feature space
lating the correlation between a test time segment in a test subject with the       in the macaque temporal lobe. Nat. Neurosci. 12, 1187–1196.
group mean response-pattern vector, excluding the test subject’s data, for          Hanke, M., Halchenko, Y.O., Sederberg, P.B., Hanson, S.J., Haxby, J.V., and
that time segment and other time segments. Other time segments were iden-           Pollmann, S. (2009). PyMVPA: A python toolbox for multivariate pattern anal-
tified using a sliding time window, and time segments that overlapped with the      ysis of fMRI data. Neuroinformatics 7, 37–53.
test time segment were not used. A test time segment was classified as the
                                                                                    Hanson, S.J., Matsuka, T., and Haxby, J.V. (2004). Combinatorial codes in
group mean time segment with which it had the maximum correlation. We per-
                                                                                    ventral temporal lobe for object recognition: Haxby (2001) revisited: is there
formed separate BSC analyses for subjects from each center to account for
                                                                                    a ‘‘face’’ area? Neuroimage 23, 156–166.
the differences in stimulus presentation. We repeated classification for all
n 1 versus 1 subject folds and two movie-half folds (42 folds). We estimated        Hasson, U., Nir, Y., Levy, I., Fuhrmann, G., and Malach, R. (2004). Intersubject
chance performance conservatively as <1%, assuming that even with tem-              synchronization of cortical activity during natural vision. Science 303, 1634–
poral autocorrelations time points separated by 30 s are independent. We per-       1640.
formed BSC of movie time segments on response patterns in Talairach space           Haxby, J.V., Gobbini, M.I., Furey, M.L., Ishai, A., Schouten, J.L., and Pietrini, P.
and in the common model spaces derived from the movie data and from the             (2001). Distributed and overlapping representations of faces and objects in
categorical-perception experiments. We used a correlation-based one-near-           ventral temporal cortex. Science 293, 2425–2430.
est neighbor classifier for this analysis because the number of different time      Haynes, J.-D., and Rees, G. (2006). Decoding mental states from brain activity
segments in each half of the movie, >1,000 using a sliding time window, makes       in humans. Nat. Rev. Neurosci. 7, 523–534.
a multiclass analysis based on pairwise binary classifications unwieldy.
                                                                                    Hung, C.P., Kreiman, G., Poggio, T., and DiCarlo, J.J. (2005). Fast readout of
                                                                                    object identity from macaque inferior temporal cortex. Science 310, 863–866.
SUPPLEMENTAL INFORMATION                                                            Kanwisher, N. (2010). Functional specificity in the human brain: a window into
                                                                                    the functional architecture of the mind. Proc. Natl. Acad. Sci. USA 107, 11163–
Supplemental Information includes five figures and Supplemental Experi-             11170.
mental Procedures and can be found with this article online at doi:10.1016/
                                                                                    Kanwisher, N., McDermott, J., and Chun, M.M. (1997). The fusiform face area:
j.neuron.2011.08.026.
                                                                                    a module in human extrastriate cortex specialized for face perception.
                                                                                    J. Neurosci. 17, 4302–4311.
ACKNOWLEDGMENTS                                                                     Kay, K.N., Naselaris, T., Prenger, R.J., and Gallant, J.L. (2008). Identifying
                                                                                    natural images from human brain activity. Nature 452, 352–355.
We would like to thank Jason Gors for assistance with data collection and
                                                                                    Kiani, R., Esteky, H., Mirpour, K., and Tanaka, K. (2007). Object category struc-
Courtney Rogers for administrative support. Funding was provided by National
                                                                                    ture in response patterns of neuronal population in monkey inferior temporal
Institutes of Mental Health grants, F32MH085433-01A1 (Connolly) and
                                                                                    cortex. J. Neurophysiol. 97, 4296–4309.
5R01MH075706 (Haxby), and by a graduate fellowship from the Neukom Insti-
tute for Computational Sciences at Dartmouth (Guntupalli).                          Kriegeskorte, N., Mur, M., and Bandettini, P. (2008a). Representational simi-
                                                                                    larity analysis - connecting the branches of systems neuroscience. Front
Accepted: August 30, 2011                                                           Syst Neurosci 2, 4.
Published: October 19, 2011                                                         Kriegeskorte, N., Mur, M., Ruff, D.A., Kiani, R., Bodurka, J., Esteky, H., Tanaka,
                                                                                    K., and Bandettini, P.A. (2008b). Matching categorical object representations
REFERENCES                                                                          in inferior temporal cortex of man and monkey. Neuron 60, 1126–1141.
                                                                                    Kriegeskorte, N., Simmons, W.K., Bellgowan, P.S., and Baker, C.I. (2009).
Abdi, H., Dunlop, J.P., and Williams, L.J. (2009). How to compute reliability       Circular analysis in systems neuroscience: the dangers of double dipping.
estimates and display confidence and tolerance intervals for pattern classifiers    Nat. Neurosci. 12, 535–540.



                                                                                       Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc. 415
                                                                                                                                                           Neuron
                                                                                           Common Model of Human Ventral Temporal Cortex




Lashkari, D., Vul, E., Kanwisher, N., and Golland, P. (2010). Discovering struc-    Reddy, L., and Kanwisher, N. (2007). Category selectivity in the ventral visual
ture in the space of fMRI selectivity profiles. Neuroimage 50, 1085–1098.           pathway confers robustness to clutter and diverted attention. Curr. Biol. 17,
                                                                                    2067–2072.
Logothetis, N.K., and Sheinberg, D.L. (1996). Visual object recognition. Annu.
Rev. Neurosci. 19, 577–621.                                                         Sabuncu, M.R., Singer, B.D., Conroy, B., Bryan, R.E., Ramadge, P.J., and
                                                                                    Haxby, J.V. (2010). Function-based intersubject alignment of human cortical
Mahon, B.Z., and Caramazza, A. (2009). Concepts and categories: a cognitive         anatomy. Cereb. Cortex 20, 130–140.
neuropsychological perspective. Annu. Rev. Psychol. 60, 27–51.
                                                                                    Schönemann, P. (1966). A generalized solution of the orthogonal procrustes
Mitchell, T.M., Shinkareva, S.V., Carlson, A., Chang, K.-M., Malave, V.L.,          problem. Psychometrika 31, 1–10.
Mason, R.A., and Just, M.A. (2008). Predicting human brain activity associated      Serre, T., Oliva, A., and Poggio, T. (2007). A feedforward architecture accounts
with the meanings of nouns. Science 320, 1191–1195.                                 for rapid categorization. Proc. Natl. Acad. Sci. USA 104, 6424–6429.
Naselaris, T., Prenger, R.J., Kay, K.N., Oliver, M., and Gallant, J.L. (2009).      Shinkareva, S.V., Mason, R.A., Malave, V.L., Wang, W., Mitchell, T.M., and
Bayesian reconstruction of natural images from human brain activity. Neuron         Just, M.A. (2008). Using FMRI brain activation to identify cognitive states
63, 902–915.                                                                        associated with perception of tools and dwellings. PLoS ONE 3, e1394.
Norman, K.A., Polyn, S.M., Detre, G.J., and Haxby, J.V. (2006). Beyond mind-        Shinkareva, S.V., Malave, V.L., Mason, R.A., Mitchell, T.M., and Just, M.A.
reading: multi-voxel pattern analysis of fMRI data. Trends Cogn. Sci. (Regul.       (2011). Commonality of neural representations of words and pictures.
Ed.) 10, 424–430.                                                                   Neuroimage 54, 2418–2425.

O’Toole, A.J., Jiang, F., Abdi, H., and Haxby, J.V. (2005). Partially distributed   Spiridon, M., and Kanwisher, N. (2002). How distributed is visual category
representations of objects and faces in ventral temporal cortex. J. Cogn.           information in human occipito-temporal cortex? An fMRI study. Neuron 35,
Neurosci. 17, 580–590.                                                              1157–1165.
                                                                                    Talairach, J., and Tournoux, P. (1988). Co-planar Stereotaxic Atlas of the
O’Toole, A.J., Jiang, F., Abdi, H., Pénard, N., Dunlop, J.P., and Parent, M.A.
                                                                                    Human Brain (Stuttgart, Germany: Georg Thieme).
(2007). Theoretical, statistical, and practical perspectives on pattern-based
classification approaches to the analysis of functional neuroimaging data.          Tanaka, K. (2003). Columns for complex visual object features in the inferotem-
J. Cogn. Neurosci. 19, 1735–1752.                                                   poral cortex: clustering of cells with similar but slightly different stimulus selec-
                                                                                    tivities. Cereb. Cortex 13, 90–99.
Op de Beeck, H.P., Brants, M., Baeck, A., and Wagemans, J. (2010).
                                                                                    Tsao, D.Y., Freiwald, W.A., Knutsen, T.A., Mandeville, J.B., and Tootell, R.B.H.
Distributed subordinate specificity for bodies, faces, and buildings in human
                                                                                    (2003). Faces and objects in macaque cerebral cortex. Nat. Neurosci. 6,
ventral visual cortex. Neuroimage 49, 3414–3425.
                                                                                    989–995.
Peelen, M.V., and Downing, P.E. (2005). Selectivity for the human body in the       Tsao, D.Y., Freiwald, W.A., Tootell, R.B.H., and Livingstone, M.S. (2006). A
fusiform gyrus. J. Neurophysiol. 93, 603–608.                                       cortical region consisting entirely of face-selective cells. Science 311,
Poldrack, R.A., Halchenko, Y.O., and Hanson, S.J. (2009). Decoding the large-       670–674.
scale structure of brain function by classifying mental States across individ-      Vapnik, V. (1995). The Nature of Statistical Learning Theory (New York:
uals. Psychol. Sci. 20, 1364–1372.                                                  Springer-Verlag).




416 Neuron 72, 404–416, October 20, 2011 ª2011 Elsevier Inc.
