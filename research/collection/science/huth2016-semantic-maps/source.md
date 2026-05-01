ARTICLE                                                                                                                                                                 doi:10.1038/nature17637




Natural speech reveals the semantic
maps that tile human cerebral cortex
Alexander G. Huth1, Wendy A. de Heer2, Thomas L. Griffiths1,2, Frédéric E. Theunissen1,2 & Jack L. Gallant1,2



      The meaning of language is represented in regions of the cerebral cortex collectively known as the ‘semantic system’.
      However, little of the semantic system has been mapped comprehensively, and the semantic selectivity of most regions
      is unknown. Here we systematically map semantic selectivity across the cortex using voxel-wise modelling of functional
      MRI (fMRI) data collected while subjects listened to hours of narrative stories. We show that the semantic system is
      organized into intricate patterns that seem to be consistent across individuals. We then use a novel generative model to
      create a detailed semantic atlas. Our results suggest that most areas within the semantic system represent information
      about specific semantic domains, or groups of related concepts, and our atlas shows which domains are represented in
      each area. This study demonstrates that data-driven methods—commonplace in studies of human neuroanatomy and
      functional connectivity—provide a powerful and efficient means for mapping functional representations in the brain.


Previous neuroimaging studies have identified a group of regions that                                   caused by low-level properties of the stimulus such as word rate
seem to represent information about the meaning of language. These                                      and phonemic content, additional regressors were included during
regions, collectively known as the semantic system, respond more to                                     voxel-wise model estimation and then discarded before further analysis.
words than non-words1, more to semantic tasks than phonological                                         We also included additional regressors to account for physiological and
tasks1, and more to natural speech than temporally scrambled speech2.                                   emotional factors, but these had no effect on the estimated semantic
Studies that have investigated specific types of representation in the                                  models (Supplementary Data 3).
semantic system have found areas selective for concrete or abstract                                        One advantage of voxel-wise modelling over conventional neuro­
words3–5, action verbs6, social narratives7 or other semantic features.                                 imaging approaches is that the fit models can be validated by
Others have found areas selective for specific semantic domains—                                        predicting BOLD responses to new natural stimuli that were not used
groups of related concepts such as living things, tools, food or                                        during model estimation. This makes it possible to compute effect size
shelter8–13. However, all previous studies tested only a handful of                                     by finding the fraction of response variance explained by the models.
stimulus conditions, so no study has yet produced a comprehensive                                       We tested how well the voxel-wise models predicted BOLD responses
survey of how semantic information is represented across the entire                                     elicited by a new 10-min Moth story (Fig. 1b) that had not been used for
semantic system.                                                                                        model estimation. We found good prediction performance for voxels
   We addressed this problem by using a data-driven approach14 to                                       located throughout the semantic system, including in the lateral tem-
model brain responses elicited by naturally spoken narrative stories                                    poral cortex (LTC) and ventral temporal cortex (VTC), lateral parietal
that contain many different semantic domains15. Seven subjects listened                                 cortex (LPC) and medial parietal cortex (MPC), and medial prefrontal
to more than two hours of stories from The Moth Radio Hour2 while                                       cortex, superior prefrontal cortex (SPFC) and inferior prefrontal cortex
whole-brain blood-oxygen-level-dependent (BOLD) responses were                                          (IPFC) (Fig. 1c and Extended Data Fig. 1). This suggests that much of
recorded by fMRI. We then used voxel-wise modelling, a highly effec-                                    the semantic system is domain selective.
tive approach for modelling responses to complex natural stimuli14–17,
to estimate the semantic selectivity of each voxel (Fig. 1a).                                           Mapping semantic representation across cortex
                                                                                                        By inspecting the fit models, we can determine which specific semantic
Voxel-wise model estimation and validation                                                              domains are represented in each voxel. In theory this could be done
In voxel-wise modelling, features of interest are first extracted from                                  by examining each voxel separately. However, our data consist of tens
the stimuli and then regression is used to determine how each feature                                   of thousands of voxels per subject, rendering this approach unfeasi-
modulates BOLD responses in each voxel. We used a word embedding                                        ble. A practical alternative is to project the models into a low-dimen-
space to identify semantic features of each word in the stories12,15,18–20.                             sional subspace that retains as much information as possible about the
The embedding space was constructed by computing the normalized                                         semantic tuning of the voxels10,14. We found such a space by applying
co-occurrence between each word and a set of 985 common English                                         principal components analysis to the estimated models aggregated
words (such as ‘above’, ‘worry’ and ‘mother’) across a large corpus                                     across subjects, producing 985 orthogonal semantic dimensions that
of English text. Words related to the same semantic domain tend to                                      are ordered by how much variance each explained across the voxels. It
occur in similar contexts, and so have similar co-occurrence values.                                    is likely that only some of these dimensions capture shared aspects of
For example, the words ‘month’ and ‘week’ are very similar (the corre-                                  semantic tuning across the subjects; the rest reflect individual differ-
lation between the two is 0.74), while the words ‘month’ and ‘tall’ are                                 ences, fMRI noise, or the statistical properties of the stories. To identify
not (correlation −​0.22).                                                                               the shared dimensions, we tested whether each explained more vari-
   Next we used regularized linear regression to estimate how the 985                                   ance across the models than expected by chance, which was defined
semantic features influenced BOLD responses in every cortical voxel                                     by the principal components of the stimulus matrix used for model
and in each individual subject (Fig. 1a). To account for responses                                      estimation14. At least four dimensions explained a significant amount
1
    Helen Wills Neuroscience Institute, University of California, Berkeley, California 94720, USA. 2Department of Psychology, University of California, Berkeley, California 94720, USA.


                                                                                                                                      2 8 A P R I L 2 0 1 6 | VO L 5 3 2 | NAT U R E | 4 5 3
                                                                      © 2016 Macmillan Publishers Limited. All rights reserved
 RESEARCH ARTICLE

  a     Voxel-wise model estimation                                                               b              Voxel-wise model validation
        Naturally spoken stories were played for 7 subjects                                                      A new story was then played for each subject




                                                                                                                              Estimated regression weights were
             Co-occurrence was found between each word                                                                        used to predict responses
             in the stories and 985 common words
                                         Regression                   BOLD                                                        Semantic                          Model                 New BOLD
              Semantic features           weights                   responses                                                     features                        predictions              responses
      ‘Above’                            2.8 –0.4 0.7                                                            ‘Above’                         2.8 –0.4   0.7
      ‘Dance’                           –1.5 –2.1 –3.2                                                           ‘Dance’                        –1.5 –2.1 –3.2
                                    ×                     =                                                        ‘Man’                    ×                     =
        ‘Man’                            0.1   0.1 –2.7                                                                                          0.1   0.1 –2.7                  Correlation
      ‘Seven’                            1.7 –0.8 –3.7                                                           ‘Seven’                         1.7 –0.8 –3.7

                       125 min                                          125 min                                                    11 min                             11 min     Prediction     11 min
                                                                                                                                                                                performance

  c                                                                           Prediction performance (r )
                                                                0   0.06 0.12 0.18 0.24 0.30 0.36 0.42 0.48 0.54 0.60




                                                                              05
                                                                                         10      10
                                                                                                            2       5    8    1
                                                                    S       0. 01                        10      10  10       –2
                                                                    N     0.
                                                                         0.
                                                                         0. 100             –7      –9      –1      –1  –1   10
                                                                           00
                                                                            1001–5

                                                                               P value (FDR corrected)
                                                          MPC                                                                          MPC


                                                                                                                                                                                      SPFC


                                                      LPC                                                                                       LPC
                SPFC




                             IPFC                                                                                                                                              IPFC

                                                                                                                                                         LTC
                                                          LTC                                                                        VTC
                                                                         VTC                                                                                                                   Superior
            Superior
                  LH                                                                                                                                                                       RH
 Anterior                                                                                                                                                                                                 Anterior



Figure 1 | Voxel-wise modelling. a, Seven subjects listened to over 2 h of                                 included during model estimation. Model prediction performance was
naturally spoken narrative stories while BOLD responses were measured                                      computed as the correlation between predicted responses to this story and
using fMRI. Each word in the stories was projected into a 985-dimensional                                  actual BOLD responses. c, Prediction performance of voxel-wise models
word embedding space constructed using word co-occurrence statistics                                       for one subject. Semantic models accurately predict BOLD responses in
from a large corpus of text. A finite impulse response (FIR) regression                                    many brain areas, including the LTC, VTC, LPC, MPC, SPFC and IPFC.
model was estimated individually for every voxel. The voxel-wise model                                     These regions have previously been identified as the semantic system in
weights describe how words appearing in the stories influence BOLD                                         the human brain. LH, left hemisphere; RH, right hemisphere.
signals. b, Models were tested using one 10-min story that was not

of variance (P <​ 0.001, Bonferroni-corrected bootstrap test) in all but                                      Next, we visualized where each of the 12 categories appeared in the
one subject; in the last subject only three dimensions were significant                                    shared semantic space (Fig. 2a). Each category label was also assigned
(Extended Data Fig. 2). This suggests that our fMRI data contain about                                     an RGB colour, where the red channel was determined by the first
four statistically significant semantic dimensions that are shared across                                  dimension, the green channel by the second, and the blue channel by
subjects.                                                                                                  the third. The first dimension is that which captured the most seman-
   The four shared semantic dimensions provide a way to summarize                                          tic variance across the voxel-wise models of all seven subjects. One
succinctly the semantic selectivity of a voxel. However, to interpret                                      end of this dimension favours categories related to humans and social
projections of the models onto these dimensions we need to under-                                          interaction, including ‘social’, ‘emotional’, ‘violent’ and ‘communal’. The
stand how semantic information is encoded in this four-dimensional                                         other end favours categories related to perceptual descriptions, quanti-
space. To visualize the semantic space, we projected the 10,470 words                                      tative descriptions and setting, including ‘tactile’, ‘locational’, ‘numeric’
in the stories from the word embedding space onto each dimension.                                          and ‘visual’. This is consistent with previous suggestions that humans
We then used k-means clustering to identify 12 distinct categories (see                                    comprise a particularly salient and strongly represented semantic
Supplementary Methods for details). Each category was inspected and                                        domain16,21. Subsequent dimensions of the semantic space captured
labelled by hand. The labels assigned to the 12 categories were ‘tactile’                                  less variance than the first and were also more difficult to interpret. The
(a cluster containing words such as ‘fingers’), ‘visual’ (words such as                                    second dimension seems to distinguish between perceptual categories,
‘yellow’), ‘numeric’ (‘four’), ‘locational’ (‘stadium’), ‘abstract’ (‘natural’),                           including ‘visual’ and ‘tactile’, and non-perceptual categories, including
‘temporal’ (‘minute’), ‘professional’ (‘meetings’), ‘violent’ (‘lethal’),                                  ‘mental’, ‘professional’ and ‘temporal’. The third and fourth dimensions
‘communal’ (‘schools’), ‘mental’ (‘asleep’), ‘emotional’ (‘despised’) and                                  are less clear.
‘social’ (‘child’). (See Supplementary Table 2 and Supplementary Data                                         Earlier studies identified the cortical regions comprising the seman-
5 for more detailed evaluations of each category.)                                                         tic system1,2, but could not comprehensively characterize their semantic

4 5 4 | NAT U R E | VO L 5 3 2 | 2 8 A P R I L 2 0 1 6
                                                            © 2016 Macmillan Publishers Limited. All rights reserved
                                                                                                                                                                                               ARTICLE RESEARCH

     a                    7*                                             7*                                                              7*                                                  7*




      7*                                                                                               7*                                                            7*
                                                   7*

                                                                                                       7*



                                  :4-(
                                                                                                                                                                                   :4-(
                           :,-
     b                           :4/(      4-               :-
                                                                                                                  7*
                                                                                   9:*
                                                                                               7*
                                                                                                                                                                       4-
                                                                                                                           9:*                             :-
                                                                                                                                                                                                      :,-
                                  -,-      4/                                                                                                   07:
                                                       :/         07:
                                                                                 =                                                  =                                  4/
                                 Z74]                                                                                                                            :/        -,-
                                         44                                          =)                                      =) 67(
                                                                                                                                                                                    Z74]
                                                 :4                      67(
                                      -6                                    =(                                                                                        :4
                                                                                                                                                                             44     74]O
                                                                                                                               =(                                                  -6
                                 )(
                                             :/                                                                                     ,)(
                                                                                 36                                            36
                                                                          ,)(          = =                                                                       :/                )(
                                             :-
           3/                                                              4;                 = =         =
                                                                                                                  =
                                                                                                                                     4;
                                                                                                                       = =
                                                         (*                                                                      6-(                         (*                                                 9/
               :\WLYPVY
                                                                                      6-(                                                                                                                   :\WLYPVY
    (U[LYPVY                                                                 --(
                                                                                                                                     --(                                                                           (U[LYPVY
                                                                                        77(                             77(




     c
                            :                                                                         :                                                                                 :




Figure 2 | Principal components of voxel-wise semantic models.                                           categories (tactile, locational) from human-related categories (social,
a–c, Principal components analysis of voxel-wise model weights reveals                                   emotional, violent). PC, principal component. b, Voxel-wise model
four important semantic dimensions in the brain (Extended Data Fig. 2).                                  weights were projected onto the semantic dimensions and then coloured
a, An RGB colourmap was used to colour both words and voxels based                                       using the same RGB colourmap (see Extended Data Fig. 3 for separate
on the first three dimensions of the semantic space. Words that best                                     dimensions). Projections for one subject (S2) are shown on that subject’s
match the four semantic dimensions were found and then collapsed into                                    cortical surface. Semantic information seems to be represented in intricate
12 categories using k-means clustering. Each category (Supplementary                                     patterns across much of the semantic system. c, Semantic principal
Table 2) was manually assigned a label. The 12 category labels (large                                    component flatmaps for three other subjects. Comparing these flatmaps,
words) and a selection of the 458 best words (small words) are plotted here                              many patterns appear to be shared across individuals. (See Extended Data
along four pairs of semantic dimensions. The largest axis of variation lies                              Fig. 3 for other subjects.) Abbreviations for regions of interest are listed in
roughly along the first dimension, and separates perceptual and physical                                 the Methods section.

selectivity. We were able to visualize the pattern of semantic-domain                                    Using PrAGMATiC to construct a semantic atlas
selectivity across the entire cortex by projecting voxel-wise models onto                                Given the apparent consistency in the patterns of semantic selectivity
the shared semantic dimensions. Figure 2b shows projections onto the                                     across individuals, we sought to create a single atlas that describes
first three dimensions for one subject, plotted together using the same                                  the distribution of semantically selective functional areas in human
RGB colour scheme as in Fig. 2a (Extended Data Fig. 3a shows each                                        cerebral cortex. To accomplish this, we developed a new Bayesian
dimension separately). Thus, for example, a green voxel produces                                         algorithm, PrAGMATiC, that produces a probabilistic and generative
greater BOLD responses to categories that are coloured green in the                                      model of areas tiling the cortex22. This algorithm models patterns of
semantic space, such as ‘visual’ and ‘numeric’. This visualization sug-                                  functional tuning recovered by voxel-wise modelling as a dense, tiled
gests that semantic information is represented in intricate patterns that                                map of functionally homogeneous brain areas (Fig. 3a), while respect-
cover the semantic system, including broad regions of the prefrontal                                     ing individual differences in anatomical and functional anatomy23,24.
cortex, LTC and MTC, and LPC and MPC. Furthermore, these patterns                                        The arrangement and selectivity of these areas are determined
appear to be relatively consistent across individuals (Fig. 2c; see also                                 by parameters learned from the fMRI data through a maximum-
Extended Data Fig. 3b).                                                                                  likelihood estimation technique similar to contrastive divergence25.

                                                                                                                                                       2 8 A P R I L 2 0 1 6 | VO L 5 3 2 | NAT U R E | 4 5 5
                                                                   © 2016 Macmillan Publishers Limited. All rights reserved
 RESEARCH ARTICLE

                               a               Arrangement model                                          Generated functional map                                           b
                                                                                                                                                                                                                            Left hemisphere
                                                                                                                                                                                                            0.1




                                                                                                                                                                         Average prediction performance
                                                                                                                                                                                                                       S1 S2 S3 S4 S5 S6 S7 Mean
                                                                                                                                                                                                           0.08

                                                                                                                                                                                                           0.06

                                                                                                                                                                                                           0.04
                                                                                                                                                                                                                                    n = 192
                                                                                                                                                                                                           0.02               Performance stops
                                                                                                                                                                                                                            significantly improving

                                                      Area centroid                                                                                                                                              0
                                                                                                             Functional map is
                                                      Landmark point                                         approximated as a
                                                      Spring                                                                                                                                              –0.02
                                                                                                             Voronoi tessellation of                                                                              8
                                                                                                                                                                                                                                  128   192      256      320     384
                                                                                                                                                                                                                 32
                                                                                                                                                                                                                 64
                                                                                                             the area centroids
                                       PrAGMATiC parameters                                                                                                                                                                        Total areas

                                       Shared across subjects                                       Unique to each subject
                                           L: ideal spring lengths                                   H: exact centroid locations                                                                                            Right hemisphere
                                                                                                                                                                                                            0.1




                                                                                                                                                                         Average prediction performance
                                           M: area functional means                                  V: functional values on cortex                                                                                    S1 S2 S3 S4 S5 S6 S7 Mean
                                                                                                                                                                                                           0.08
                                                            P(V,H;M,L) =                          P(H;L)                  P(V|H;M)
                                                                                                                                                                                                           0.06
                                                                                             Arrangement       Map
                                                 Total probability =                                      ×
                                                                                              probability   probability                                                                                    0.04

                                               P(H;L) ∝ e−E(H; L)                                         P(V|H;M) ∝ e−E(V|H; M)                                                                           0.02            n = 128
                                                                                                                                                                                                                         Performance stops
                                                                                                                                                                                                                       significantly improving
                                               E(H; L) =                  (dijs − Lij)2                   E(V|H; M) ∝               (MH(s,l) – Vls)2                                                             0
                                                                  i,j,s                                                       l,s

                                                                                                                                                                                                          –0.02
                                         Distance between centroids                                       Nearest centroid to point
                                                                                                                                                                                                                  8
                                                                                                                                                                                                                                  128   192     256    320        384
                                                                                                                                                                                                                 32
                                                                                                                                                                                                                 64
                                         i and j in subject s                                             l in subject s
                                                                                                                                                                                                                                  Total areas

                                                                                                                     visual
                         c                                            SMFA                                    tactile                PC2                                                                                           SMFA
                                                                                                                      abstract
                                                                                                                    numeric
                                                                           CgS                                                                                                                                              CgS
                                                                                                                                            violent
                                          SEF
                                                                  SMHA
                                                                                                                                                       PC1                                                                                                   SEF
                                                                                                                                                                                                                                                                        CgS
                                                                                                             locational                                                                                                             SMHA
                                   CgS                                                                                              communal                                                                                M1F
                                                                                                                                        emotional
                                                             FEF               M1F                                       temporal             social
                                                                                                                             professional                                                                                         M1H    FEF                SFS
                                                                      M1                                                                                                                                     S1F
                                                                        H                  S1F       CgS                           mental
                                         SFS
                                                           PreCeS                                                                                                                                                                                      sPMv
                                                                                  CeS                                                                         sbPS                                                     CeS
                                                                                                                                                                                                   PoCeS                                PreCeS
                                                 sPMv                                       PoCeS
                                                                                                                                                 RSC
                                                                                                             sbPS
                                                                               S1H                                                                                                                                   S1H
                                                      FO                                            IPS                   RSC                                                                                                 M1 M
                                                                                                                                                                     IPS                                                                              IFS
                                               IFS                M                                                                                                                                                           S1M
                                                              M1                           IPS                                                                                                             IPS                             FO
                                                                      S1M                                                                                                                                                                            BA
                                                BA                                                                                          POS         TOS
                                                                                                                          POS

                                                            CSI                                                                                                                                                                     S2F
                                                                                                                   TOS
                                                                      S2F
                                                                                                                                                        OPA                                                                                    CSI
                                                                                                            OPA                                                                                                             AC
                                                                          AC
                                                     SyF                             STS                      LOS
                                                                                             AOS                                                                                              AOS
                                                                                                                                                        LOS                                                                                    SyF
                                                                                                                                                                   EBA
                                                                                                     EBA
                    AC Known regions of                                                                     OFA
                       interest                                                                                                                                                                                             STS
                                                                                                                                                                     OFA
                                                                                                                                                                                                                                                                   Areas a ected by MRI
                                                                                                                                                       CoS                                                            ITS                                          signal dropout
                   SyF                                                                                                                     V1
                         Major sulci                                        ITS                              CoS
                                                                                                                              V1
                                                                                                                                                V2 V3                                                                                                              Areas explained well
                                                                                                                   V3                                        PPA                                                                                                   by low-level auditory
                                                                                                                         V2                                                 FFA
                                                                                                  FFA
                                                              Superior                                                                                                                                                      Superior                               models
                                                                                                             PPA                                                                       OTS
                                                                                            OTS
                                                Anterior                    LH                                                                                                                                       RH                   Anterior




Figure 3 | PrAGMATiC: a generative model for cortical maps.                                                                                was used to choose the number of areas in each hemisphere. PrAGMATiC
a–c, To create an atlas that describes the distribution of semantically                                                                    models were estimated on six subjects and then used to predict BOLD
selective functional areas in the human cerebral cortex we developed                                                                       responses for the seventh. Prediction performance improved significantly
PrAGMATiC, a probabilistic and generative model of areas tiling the                                                                        up to 192 total areas in the left hemisphere and 128 areas in the right.
cortex. a, PrAGMATiC has two parts: an arrangement model and an                                                                            c, A semantic atlas was estimated using data from all seven subjects. Areas
emission model. The arrangement model is analogous to a physical system                                                                    for which the semantic model did not predict better than models based
of springs joining neighbouring area centroids. To enforce similarity                                                                      on low-level features (that is, word rate, phonemes) were removed.
across subjects, springs also join areas to 19 regions of interest that were                                                               The remaining areas were plotted on one subject’s cortical surface using
localized separately. The emission model assigns the functional mean of                                                                    the same RGB colourmap as Fig. 2. Areas dominated by signal dropout are
the closest area centroid to each point on the cortex, forming a Voronoi                                                                   shown in black hatching, and areas where the low-level models performed
tessellation. Spring lengths and area means are shared across subjects                                                                     well are shown in white hatching. This atlas shows the functional
while exact area locations are unique to each subject. These parameters are                                                                organization of the semantic system that is common across subjects.
fit using maximum-likelihood estimation. b, A leave-one-out procedure


4 5 6 | NAT U R E | VO L 5 3 2 | 2 8 A P R I L 2 0 1 6
                                                                                        © 2016 Macmillan Publishers Limited. All rights reserved
                                                                                                                                        ARTICLE RESEARCH

Some parameters are shared; these describe properties of the cortical            and conscious thought26. One interesting possibility is that the seman-
map that are common across the group. Other parameters are unique                tic areas identified here represent the same semantic domains during
to each subject; these capture individual differences. Learning both             conscious thought. This suggests that the contents of thought, or inter-
shared and unique parameters simultaneously eliminates the usual                 nal speech, might be decoded using these voxel-wise models17. In the
requirement to perform anatomical or functional alignment of data                LTC (Extended Data Fig. 9), our atlas identifies fewer distinct semantic
across subjects.                                                                 areas than in the LPC, MPC or SPFC. This is surprising because the
   The PrAGMATiC algorithm has two components: an arrangement                    LTC has a key role in language comprehension1,27 and also belongs to
model that determines where functional areas appear on the cortical              the DMN. However, the quality of fMRI signals recorded in the anterior
sheet, and an emission model that determines how the cortical map                temporal lobe is poor, so the LTC probably contains other semantic areas
is produced from an arrangement of areas. The arrangement model                  that could not be recovered using our current approach. Detailed anal-
simulates a physical spring network that joins the centroid of each func-        yses of semantic representations in the LPC, MPC, SPFC and LTC, as
tional area to its neighbours. Equilibrium spring lengths are shared             well as the VTC (Extended Data Fig. 10), IPFC (Extended Data Fig. 11),
across subjects, but each spring can be stretched or compressed in any           and opercular and insular cortex (Extended Data Fig. 12) can be found
individual subject. Arrangements are also constrained by several func-           in Supplementary Information, along with discussion and comparisons
tional landmarks, which are known regions of interest identified in              to earlier neuroimaging and lesion results.
every subject using separate functional data. These constraints ensure
that the maps will be similar across subjects, but allow for substantial         Discussion
individual variability in the precise arrangement and size of the areas.         One striking aspect of our atlas is that the distribution of semantically
Using the arrangement model, the emission model creates homogene-                selective areas is relatively symmetrical across the two cerebral
ous functional areas by assigning each vertex on the cortical surface to         hemispheres. This finding is inconsistent with human lesion studies
the nearest area centroid. The functional value at each vertex is then           that support the idea that semantic representation is lateralized to the
drawn from a multivariate normal distribution. The mean functional               left hemisphere13. However, many fMRI studies of semantic representa-
value for each area is learned by the algorithm and is shared across             tion find only modest lateralization1 and one study that used narrative
subjects. We define the functional value as a four-dimensional vector            stories found highly bilateral results similar to ours2. This suggests
that reflects the projection of the estimated model for each voxel onto          that right hemisphere areas may respond more strongly to narrative
the four shared semantic dimensions.                                             stimuli than to the words and short phrases used in most studies. Still,
   One important hyperparameter is the total number of areas that                more research will be needed to determine what roles these left- and
PrAGMATiC uses to tile the cortex. We used a cross-validation                    right-hemisphere semantic areas have in language comprehension.
procedure to choose the total number of areas tiling each hemi-                     Another interesting aspect of these results is that the organization of
sphere and then tested whether each area is semantically selective.              semantically selective brain areas seems to be highly consistent across
PrAGMATiC models were estimated from data from six subjects and                  individuals. This might suggest that innate anatomical connectivity
then used to predict the semantic map in the seventh subject using               or cortical cytoarchitecture constrains the organization of high-level
only cortical anatomy and the locations of functional landmarks in that          semantic representations28,29. It is also possible that this is owing to
subject. Predicted BOLD responses based on this map were compared                common life experiences of the subjects, all of whom were raised and
to actual responses to determine how well the PrAGMATiC model gen-               educated in Western industrial societies. Future studies that include
eralizes across subjects. Prediction performance climbed quickly as the          subjects from more diverse backgrounds will be needed to determine
total number of areas rose from 8 to 128 and improved more gradually             how much of this organizational consistency reflects innate brain
thereafter (Fig. 3b). In the left hemisphere, prediction performance did         structure versus experience.
not improve significantly for models with 192 or more total areas (false            One limitation of PrAGMATiC as used here is that each area is
discovery rate (FDR) >​ 0.01, Tukey post-hoc test with subject-wise              assumed to be functionally homogeneous. This is a common assump-
random effects). In the right hemisphere, prediction performance                 tion in the design and analysis of many neuroimaging studies30.
did not improve significantly for models with 128 or more total areas.           However, many cortical maps, including semantic maps in visual
However, because PrAGMATiC tiles the entire cerebral cortex, these               cortex14, seem to contain smoothly changing gradients of representation.
numbers include both semantically selective and nonselective areas.              It should be possible to modify the PrAGMATiC algorithm to model
To identify the semantically selective areas and eliminate those that are        functional gradients explicitly. This will provide an objective tool for
nonselective, we tested whether the average voxel-wise semantic model            determining whether the semantic maps found here are best described
in each area predicted responses significantly better than the average           as homogeneous areas or as gradients.
model for low-level features such as word rate, phoneme rate, and pho-              Data-driven approaches are commonplace in studies of human
nemes. This excluded areas that were not selective for either semantic           neuroanatomy31 and resting state networks26,32, but are only beginning
or low-level features, such as motor and visual cortex. It also excluded         to be used in functional imaging14,15. Our study demonstrates the power
areas that were not uniquely selective for semantic features, such as            and efficiency of data-driven approaches for functional mapping of the
Broca’s area, which was desirable because of the increased uncertainty           human brain. Although our experiment used a simple design in which
of semantic model weights in those areas.                                        subjects only listened to stories, the data were rich enough to produce a
   Figure 3c shows the semantic atlas projected onto the cortical surface        comprehensive atlas of semantically selective areas. Furthermore, our
of one subject (see also Extended Data Figs 4 and 5). The left hemi-             data-driven framework is quite general. Other properties of language
sphere contains 77 semantic areas (FDR <​ 1/192, bootstrap test) and             can be mapped (even in this same data set) by using feature spaces
the right contains 63 semantic areas (FDR <​ 1/128, bootstrap test).             that reflect phonemes, syntax and so on. Complex semantic models
A diverse tiling of areas that represent different semantic domains              that incorporate information beyond word co-occurrence can be tested
appear in the LPC (Extended Data Fig. 6), MPC (Extended Data Fig. 7)             and compared quantitatively. The generalizability of these models
and SPFC (Extended Data Fig. 8). In the LPC and MPC, central areas               can also be tested by using stimuli beyond autobiographical stories.
(near the angular gyrus and subparietal sulci, respectively) are selective       It is sometimes difficult to synthesize the results of data-driven exper-
for social concepts, while surrounding areas are selective for numeric,          iments with those from hypothesis-driven experiments, but future
visual or tactile concepts. In the SPFC, medial areas are mainly selec-          methodological and theoretical developments should help to bridge
tive for social concepts, while dorsolateral areas are more diverse. The         this divide. We expect that the semantic atlas presented here will be
LPC, MPC and SPFC also all belong to the default mode network                    useful for many researchers investigating the neurobiological basis of
(DMN), which is thought to be involved in introspection, rumination              language. We also expect that this atlas can be refined and expanded

                                                                                                              2 8 A P R I L 2 0 1 6 | VO L 5 3 2 | NAT U R E | 4 5 7
                                                   © 2016 Macmillan Publishers Limited. All rights reserved
 RESEARCH ARTICLE

by incorporating results from future studies. To facilitate this, we have                19. Lund, K. & Burgess, C. Producing high-dimensional semantic spaces from
created a detailed interactive version of the semantic atlas that can be                     lexical co-occurrence. Behav. Res. Methods Instrum. Comput. 28, 203–208
                                                                                             (1996).
explored online at http://gallantlab.org/huth2016.                                       20. Turney, P. D. & Pantel, P. From frequency to meaning: vector space models
                                                                                             of semantics. J. Artif. Intell. Res. 37, 141–188 (2010).
Online Content Methods, along with any additional Extended Data display items and        21. Caramazza, A. & Mahon, B. Z. The organisation of conceptual knowledge in the
Source Data, are available in the online version of the paper; references unique to          brain: the future’s past and some future directions. Cogn. Neuropsychol. 23,
these sections appear only in the online paper.                                              13–38 (2006).
                                                                                         22. Huth, A. G., Griffiths, T. L., Theunissen, F. E. & Gallant, J. L. PrAGMATiC:
Received 8 January 2014; accepted 2 March 2016.                                              a probabilistic and generative model of areas tiling the cortex. Preprint at
                                                                                             http://arxiv.org/abs/1504.03622 (2015).
1.  Binder, J. R., Desai, R. H., Graves, W. W. & Conant, L. L. Where is the semantic     23. Amunts, K., Malikovic, A., Mohlberg, H., Schormann, T. & Zilles, K. Brodmann’s
    system? A critical review and meta-analysis of 120 functional neuroimaging               areas 17 and 18 brought into stereotaxic space—where and how variable?
    studies. Cereb. Cortex 19, 2767–2796 (2009).                                             Neuroimage 11, 66–84 (2000).
2. Lerner, Y., Honey, C. J., Silbert, L. J. & Hasson, U. Topographic mapping of a        24. Fedorenko, E., Hsieh, P.-J., Nieto-Castañón, A., Whitfield-Gabrieli, S. &
    hierarchy of temporal receptive windows using a narrated story. J. Neurosci.             Kanwisher, N. New method for fMRI investigations of language: defining ROIs
    31, 2906–2915 (2011).                                                                    functionally in individual subjects. J. Neurophysiol. 104, 1177–1194 (2010).
3. Friederici, A. D., Opitz, B. & von Cramon, D. Y. Segregating semantic and             25. Hinton, G. E. Training products of experts by minimizing contrastive
    syntactic aspects of processing in the human brain: an fMRI investigation of             divergence. Neural Comput. 14, 1771–1800 (2002).
    different word types. Cereb. Cortex 10, 698–705 (2000).                              26. Buckner, R. L., Andrews-Hanna, J. R. & Schacter, D. L. The brain’s default
4. Noppeney, U. & Price, C. J. Retrieval of abstract semantics. Neuroimage 22,               network: anatomy, function, and relevance to disease. Ann. NY Acad. Sci. 1124,
    164–170 (2004).                                                                          1–38 (2008).
5. Binder, J. R., Westbury, C. F., McKiernan, K. A., Possing, E. T. & Medler, D. A.      27. DeWitt, I. & Rauschecker, J. P. Phoneme and word recognition in the auditory
    Distinct brain systems for processing concrete and abstract concepts.                    ventral stream. Proc. Natl Acad. Sci. USA 109, E505–E514 (2012).
    J. Cogn. Neurosci. 17, 905–917 (2005).                                               28. Riesenhuber, M. Appearance isn’t everything: news on object representation
6. Bedny, M., Caramazza, A., Grossman, E., Pascual-Leone, A. & Saxe, R.                      in cortex. Neuron 55, 341–344 (2007).
    Concepts are more than percepts: the case of action verbs. J. Neurosci. 28,          29. Dehaene, S., Cohen, L., Sigman, M. & Vinckier, F. The neural code for written
    11347–11353 (2008).                                                                      words: a proposal. Trends Cogn. Sci. 9, 335–341 (2005).
7. Saxe, R. & Kanwisher, N. People thinking about thinking people. The role of the       30. Op de Beeck, H. P., Haushofer, J. & Kanwisher, N. G. Interpreting fMRI data:
    temporo-parietal junction in “theory of mind”. Neuroimage 19, 1835–1842                  maps, modules and dimensions. Nature Rev. Neurosci. 9, 123–135
    (2003).                                                                                  (2008).
8. Caramazza, A. & Shelton, J. R. Domain-specific knowledge systems in the               31. Caspers, S. et al. Organization of the human inferior parietal lobule based on
    brain the animate-inanimate distinction. J. Cogn. Neurosci. 10, 1–34                     receptor architectonics. Cereb. Cortex 23, 615–628 (2013).
    (1998).                                                                              32. Cohen, A. L. et al. Defining functional areas in individual human brains using
9. Mummery, C. J., Patterson, K., Hodges, J. R. & Price, C. J. Functional                    resting functional connectivity MRI. Neuroimage 41, 45–57 (2008).
    neuroanatomy of the semantic system: divisible by what? J. Cogn. Neurosci.
    10, 766–777 (1998).                                                                  Supplementary Information is available in the online version of the paper.
10. Just, M. A., Cherkassky, V. L., Aryal, S. & Mitchell, T. M. A neurosemantic theory
    of concrete noun representation based on the underlying brain codes.                 Acknowledgements This work was supported by grants from the National
    PLoS ONE 5, e8622 (2010).                                                            Science Foundation (NSF; IIS1208203), the National Eye Institute
11. Warrington, E. K. The selective impairment of semantic memory.                       (EY019684), and from the Center for Science of Information (CSoI), an NSF
    Q. J. Exp. Psychol. 27, 635–657 (1975).                                              Science and Technology Center, under grant agreement CCF-0939370.
12. Mitchell, T. M. et al. Predicting human brain activity associated with the           A.G.H. was also supported by the William Orr Dingwall Neurolinguistics
    meanings of nouns. Science 320, 1191–1195 (2008).                                    Fellowship. We thank J. Sohl-Dickstein and K. Crane for technical discussions
13. Damasio, H., Grabowski, T. J., Tranel, D., Hichwa, R. D. & Damasio, A. R.            about PrAGMATiC, J. Nguyen for assistance transcribing and aligning stimuli,
    A neural basis for lexical retrieval. Nature 380, 499–505 (1996).                    B. Griffin for segmenting and flattening cortical surfaces, and N. Bilenko,
14. Huth, A. G., Nishimoto, S., Vu, A. T. & Gallant, J. L. A continuous semantic space   J. Gao, M. Lescroart and A. Nunez-Elizalde for general comments and
    describes the representation of thousands of object and action categories            discussions.
    across the human brain. Neuron 76, 1210–1224 (2012).
15. Wehbe, L. et al. Simultaneously uncovering the patterns of brain regions             Author Contributions All authors helped conceive and design the experiment.
    involved in different story reading subprocesses. PLoS ONE 9, e112575                W.A.d.H. and A.G.H. selected and annotated stimuli and collected fMRI data.
    (2014).                                                                              A.G.H. analysed the data. A.G.H. and T.L.G. designed the PrAGMATiC generative
16. Naselaris, T., Prenger, R. J., Kay, K. N., Oliver, M. & Gallant, J. L. Bayesian      model. A.G.H. and J.L.G. wrote the paper. J.L.G. contributed to all aspects of the
    reconstruction of natural images from human brain activity. Neuron 63,               project.
    902–915 (2009).
17. Nishimoto, S. et al. Reconstructing visual experiences from brain activity           Author Information Reprints and permissions information is available at
    evoked by natural movies. Curr. Biol. 21, 1641–1646 (2011).                          www.nature.com/reprints. The authors declare no competing financial
18. Deerwester, S., Dumais, S. T., Furnas, G. W., Landauer, T. K. & Harshman, R.         interests. Readers are welcome to comment on the online version of the paper.
    Indexing by latent semantic analysis. J. Am. Soc. Inf. Sci. 41, 391–407              Correspondence and requests for materials should be addressed to
    (1990).                                                                              J.L.G. (gallant@berkeley.edu).




4 5 8 | NAT U R E | VO L 5 3 2 | 2 8 A P R I L 2 0 1 6
                                                            © 2016 Macmillan Publishers Limited. All rights reserved
                                                                                                                                                    ARTICLE RESEARCH

METHODS                                                                                       Next, we constructed a word co-occurrence matrix, M, with 985 rows and
MRI data collection. MRI data were collected on a 3T Siemens TIM Trio                     10,470 columns. Iterating through the text corpus, we added 1 to Mi,j each time
scanner at the UC Berkeley Brain Imaging Center using a 32-channel Siemens                word j appeared within 15 words of basis word i. A window size of 15 was selected
volume coil. Functional scans were collected using gradient echo EPI with                 to be large enough to suppress syntactic effects (that is, word order) but no larger.
repetition time (TR) =​ 2.0045 s, echo time (TE) =​ 31 ms, flip angle =​  70°, voxel      Once the word co-occurrence matrix was complete, we log-transformed the counts,
size =​  2.24 ×​  2.24 ×​ 4.1 mm (slice thickness =​ 3.5 mm with 18% slice gap), matrix   replacing Mi,j with log(1 +​  Mi,j). Next, each row of M was z-scored to correct for
size =​  100 ×​ 100, and field of view =​  224 ×​ 224 mm. Thirty axial slices were        differences in basis word frequency, and then each column of M was z-scored to
prescribed to cover the entire cortex and were scanned in interleaved order.              correct for word frequency. Each column of M is now a 985-dimensional semantic
A custom-modified bipolar water excitation radiofrequency (RF) pulse was used             vector representing one word in the lexicon.
to avoid signal from fat. Anatomical data were collected using a T1-weighted                  The matrix used for voxel-wise model estimation was then constructed from the
multi-echo MP-RAGE sequence on the same 3T scanner.                                       stories: for each word–time pair (w,t) in each story we selected the corresponding
Subjects. Functional data were collected from five male subjects and two female           column of M, creating a new list of semantic vector–time pairs, (Mw,t). These
subjects: S1 (male, age 26), S2 (male, age 32), S3 (female, age 31), S4 (male, age 31),   vectors were then resampled at times corresponding to the fMRI acquisitions using
S5 (male, age 26), S6 (female, age 25), and S7 (male, age 30). Two of the subjects        a 3-lobe Lanczos filter with the cut-off frequency set to the Nyquist frequency of
were authors (S1: A.G.H.; and S3: W.A.d.H.). All subjects were healthy and had            the fMRI acquisition (0.249 Hz).
normal hearing. The experimental protocol was approved by the Committee for               Voxel-wise model estimation and validation. A linearized finite impulse response
the Protection of Human Subjects at University of California, Berkeley. Written           (FIR) model14,17 consisting of four separate feature spaces was fit to every cortical
informed consent was obtained from all subjects. Voxel-wise models were esti-             voxel in each subject’s brain. These four feature spaces were word rate (1 feature),
mated and validated independently for each subject using separate data sets               phoneme rate (1 feature), phonemes (39 features), and semantics (985 features).
reserved for that purpose. Principal components and PrAGMATiC analyses used               The word rate, phoneme rate, and phoneme features were used to account for
leave-one-subject-out cross-validation to verify that the group models accurately         responses to low-level properties of the stories that could contaminate the seman-
predict the data recorded in each individual subject.                                     tic model weights (see Supplementary Methods for details of how these low-level
Natural story stimuli. The model estimation data set consisted of ten 10- to              models were constructed). A separate linear temporal filter with four delays
15-min stories taken from The Moth Radio Hour. In each story, a single speaker tells      (1, 2, 3, and 4 time points) was fit for each of these 1,026 features, yielding a total
an autobiographical story in front of a live audience. The ten selected stories cover     of 4,104 features. This was accomplished by concatenating feature vectors that had
a wide range of topics and are highly engaging. Each story was played during a            been delayed by 1, 2, 3, and 4 time points (2, 4, 6, and 8 s). Thus, in the concatenated
separate fMRI scan. The length of each scan was tailored to the story, and included       feature space one channel represents the word rate 2 s earlier, another 4 s earlier,
10 s of silence both before and after the story. These data were collected during two     and so on. Taking the dot product of this concatenated feature space with a set
2-h scanning sessions that were performed on different days. The model validation         of linear weights is functionally equivalent to convolving the original stimulus
data set consisted of one 10-min story, also taken from The Moth Radio Hour.              vectors with linear temporal kernels that have non-zero entries for 1-, 2-, 3-, and
This story was played twice for each subject (once during each scanning session),         4-time-point delays.
and then the two responses were averaged. For story synopses and details of story             Before doing regression, we first z-scored each feature channel within each
transcription and preprocessing procedures, see Supplementary Methods.                    story. This was done to match the features to the fMRI responses, which were also
    Stories were played over Sensimetrics S14 in-ear piezoelectric headphones.            z-scored within each story. However, this had little effect on the learned weights.
A Behringer Ultra-Curve Pro hardware parametric equalizer was used to flatten                 The 4,104 weights for each voxel were estimated using L2-regularized linear
the frequency response of the headphones based on calibration data provided               regression (also known as ridge regression). To keep the scale of the weights con-
by Sensimetrics. All stimuli were played at 44.1 kHz using the pygame library in          sistent and to prevent bias in subsequent analyses, a single value of the regulariza-
Python. All stimuli were normalized to have peak loudness of −1 dB relative to            tion coefficient was used for all voxels in all subjects. This regularization coefficient
maximum. However, the stories were performed by different speakers and were               was found by bootstrapping the regression procedure 50 times in each subject.
not uniformly mastered, so some differences in total loudness remain.                     In each bootstrap iteration, 800 time points (20 blocks of 40 consecutive time points
Story transcription and preprocessing. Each story was manually transcribed by             each) were removed from the model estimation data set and reserved for testing.
one listener, and then the transcript was checked by a second listener. Certain           Then the model weights were estimated on the remaining 2,937 time points for each
sounds (for example, laughter, lip-smacking and breathing) were also marked to            of 20 possible regularization coefficients (log spaced between 10 and 1,000). These
improve the accuracy of the automated alignment. The audio of each story was              weights were used to predict responses for the 800 reserved time points, and then the
downsampled to 11 kHz and the Penn Phonetics Lab Forced Aligner (P2FA33) was              correlation between actual and predicted responses was found. After the bootstr­
used to automatically align the audio to the transcript. The forced aligner uses a        apping was complete, a regularization–performance curve was obtained for each
phonetic hidden Markov model to find the temporal onset and offset of each word           subject by averaging the bootstrap sample correlations first across the 50 samples
and phoneme. The Carnegie Mellon University (CMU) pronouncing dictionary                  and then across all voxels. Next, the regularization–­performance curves were
was used to guess the pronunciation of each word. When necessary, words and               averaged across the seven subjects and the best overall value of the regularization
word fragments that appeared in the transcript but not in the dictionary were man-        parameter (183.3) was selected. The best overall regularization parameter value
ually added. After automatic alignment was complete, Praat34 was used to check            was also the best value in three individual subjects. For the other four subjects the
and correct each aligned transcript manually. The corrected aligned transcript was        best regularization parameter value was slightly higher (233.6).
then spot-checked for accuracy by a different listener.                                       To validate the voxel-wise models, estimated semantic feature weights were used
    Finally, the aligned transcripts were converted into separate word and phoneme        to predict responses to a separate story that had not been used for weight estimation.
representations. The phoneme representation of each story is a list of pairs (p,t),       Prediction performance was then estimated as the Pearson correlation between
where p is a phoneme and t is the time from the beginning of the story to the mid-        predicted and actual responses for each voxel over the 290 time points in the vali-
dle of the phoneme (that is, halfway between the start and end of the phoneme)            dation story. Statistical significance was computed by comparing estimated corre-
in seconds. Similarly the word representation of each story is a list of pairs (w,t),     lations to the null distribution of correlations between two independent Gaussian
where w is a word.                                                                        random vectors of the same length. Resulting P values were corrected for multiple
Semantic model construction. To account for response variance caused by the               comparisons within each subject using the false discovery rate (FDR) procedure35.
semantic content of the stories, we constructed a 985-dimensional semantic fea-               All model fitting and analysis was performed using custom software written in
ture space based on word co-occurrence statistics in a large corpus of text12,18,19.      Python, making heavy use of NumPy36, SciPy37, and pycortex38.
First, we constructed a 10,470-word lexicon from the union of the set of all words        Semantic principal components analysis. We used principal components analysis
appearing in the stories and the 10,000 most common words in the large text               (PCA) to recover a low-dimensional semantic space from the estimated semantic
corpus. We then selected 985 basis words from Wikipedia’s List of 1000 Basic Words        model weights. We first selected only the 10,000 best predicted voxels in each
(contrary to the title, this list contained only 985 unique words at the time it was      subject according to the average bootstrap correlation (for the selected regulariza-
accessed). This basis set was selected because it consists of common words that           tion parameter value) obtained during model estimation. This was done to avoid
span a very broad range of topics. The text corpus used to construct this feature         including noise from poorly modelled voxels. Then we removed temporal informa-
space includes the transcripts of 13 Moth stories (including the 10 used as stimuli       tion from the voxel-wise model weights by averaging across the four delays for each
in this experiment), 604 popular books, 2,405,569 Wikipedia pages, and 36,333,459         feature. The weights for the word frequency, phoneme frequency, and phoneme
user comments scraped from reddit.com. In total, the 10,470 words in our lexicon          features were then discarded, leaving only the 985 semantic model weights for each
appeared 1,548,774,960 times in this corpus.                                              voxel. Finally, we applied PCA to these weights, yielding 985 principal components



                                                            © 2016 Macmillan Publishers Limited. All rights reserved
 RESEARCH ARTICLE

(PCs). Partial scree plots showing the amount of variance accounted for by each          To train the generative model we derived maximum-likelihood estimation
PC are shown in Extended Data Fig. 2. See Supplementary Methods for details.          (MLE) update rules similar to the Boltzmann learning rule with contrastive
PrAGMATiC. The PrAGMATiC generative model22 has two components: an                    divergence25. We used these learning rules to iteratively update the spring lengths
arrangement model and an emission model. The arrangement model defines a              and semantic values, maximizing the probability of the observed maps and
probability distribution over possible arrangements of the functional areas. This     minimizing the probability of unobserved maps. For details see Supplementary
model assumes that the location of each area is defined by a single point called      Methods.
the area centroid. Each centroid is modelled as being joined to nearby centroids      Region of interest abbreviations. Fusiform face area (FFA), occipital face area
by springs. While exact centroid locations can vary from subject to subject, the      (OFA), parahippocampal place area (PPA), occipital place area (OPA), retros-
equilibrium length of each spring is assumed to be consistent across subjects. The    plenial cortex (RSC), extrastriate body area (EBA), visual areas (V1-V4, V3A,
probability distribution over possible locations of the centroids is defined using    V3B, V7), lateral occipital visual area (LO), middle temporal visual area (MT+),
the total potential energy of the spring system. This distribution assigns a high     intraparietal sulcus visual area (IPS), auditory cortex (AC), primary motor and
probability to low-energy arrangements of the centroids (that is, where the springs   somatosensory areas for feet (M1F, S1F), hands (M1H, S1H), and mouth (M1M,
are not stretched much and so store little potential energy) and low probability to   S1M), secondary somatosensory areas for feet (S2F), and hands (S2H), frontal eye
high-energy arrangements (where the springs are stretched a lot).                     fields (FEF), frontal opercular eye movement area (FO), supplementary motor
   The second component is the emission model, which defines a probability dis-       foot area (SMFA), and hand area (SMHA), supplementary eye fields (SEF), Broca’s
tribution over semantic maps given an arrangement of functional areas. In the         area (BA), superior premotor ventral speech area (sPMv), premotor ventral hand
emission model each area centroid is assigned a particular semantic value in the      area (PMvh).
four-dimensional common semantic space. This value determines what type of
semantic information is represented in that area. To generate a semantic map from
                                                                                      33. Yuan, J. & Liberman, M. Speaker identification on the SCOTUS corpus. Proc.
any particular arrangement, each point on the cortical surface is first assigned to       Acoust. Preprint at http://www.ling.upenn.edu/~jiahong/publications/c09.pdf
the closest area centroid (creating a Voronoi diagram). Then the semantic value           (2008).
for each point is sampled from a spherical Gaussian distribution in semantic space,   34. Boersma, P. & Weenink, D. Praat: doing phonetics by computer (University of
centred on the semantic value of the centroid.                                            Amsterdam, 2014).
   A consequence of modelling semantic maps using a Voronoi diagram is that           35. Benjamini, Y. & Hochberg, Y. Controlling the false discovery rate: a practical
every point on the cortex must be assigned to an area, while we know that many            and powerful approach to multiple testing. J. R. Statist. Soc. B 57, 289–300
                                                                                          (1995).
points on the cortex are not semantically selective. We distinguished between         36. Oliphant, T. E. Guide to NumPy (Brigham Young University, 2006).
semantically selective and non-selective areas by testing whether the mean seman-     37. Jones, E., Oliphant, T. E. & Peterson, P. SciPy: Open source scientific tools for
tic voxel-wise model in each area predicted responses significantly better on a           Python (SciPy, 2001).
held-out story than a baseline model that accounts for responses to phonemes          38. Gao, J. S., Huth, A. G., Lescroart, M. D. & Gallant, J. L. Pycortex: an interactive
and word rate.                                                                            surface visualizer for fMRI. Front. Neuroinform. 9, 23 (2015).




                                                         © 2016 Macmillan Publishers Limited. All rights reserved
                                                                                                                                  ARTICLE RESEARCH




Extended Data Figure 1 | Voxel-wise model prediction performance.               rather than 0–0.6 as in Fig. 1c to match the scale of the adjusted prediction
Cortical flatmaps showing prediction performance of voxel-wise semantic         performance maps. Right column, prediction performance corrected
models for all seven subjects, formatted similarly to Fig. 1c. Models           to account for different amounts of noise in the BOLD responses
were tested using one 10-min story that was not included during model           (see Supplementary Methods for details). The voxel-wise semantic models
estimation. Prediction performance was then computed as the correlation         predict BOLD responses in many brain areas, including SPFC, IPFC,
between predicted and measured BOLD responses. Left column, raw                 LTC, VTC, LPC and MPC. These same regions have been previously
prediction performance. Note that the colourmap here is scaled 0–1              identified as the semantic system in the human brain.




                                                  © 2016 Macmillan Publishers Limited. All rights reserved
RESEARCH ARTICLE




Extended Data Figure 2 | Amount of variance explained by individual               stories. (The Gale–Shapley stable marriage algorithm was used to
subject and group semantic dimensions. Principal components analysis              re-order the group and stimulus PCs to maximize their correlation
was used to discover the most important semantic dimensions from                  with the subject’s PCs.) Error bars indicate 99% confidence intervals.
voxel-wise semantic model weights in each subject. To reduce noise,               Confidence intervals for the subjects’ own PCs and group PCs are
we used only the 10,000 best voxels in each subject, determined by                very small. Hollow markers indicate subject or group PCs that explain
cross-validation within the model estimation data set. Here we show the           significantly more variance than the corresponding stimulus PCs
amount of variance explained in the semantic model weights by each of             (P <​ 0.001, bootstrap test). Six PCs explain significantly more variance
the 20 most important principal components (PCs). Orange lines show               in one out of seven subjects, five PCs in two subjects, four PCs in three
the amount of variance explained by each subject’s own PCs, blue lines            subjects, and three PCs in one subject. Thus, four PCs seem to comprise a
show the variance explained by the PCs of combined data from the other            semantic space that is common across most individuals.
six subjects, and grey lines show the variance explained by the PCs of the




                                                    © 2016 Macmillan Publishers Limited. All rights reserved
                                                                                                                                  ARTICLE RESEARCH




Extended Data Figure 3 | Separate cortical projections of semantic                dropout due to field inhomogeneity are shaded with black hatched lines.
dimensions 1–4 on subject S2 and combined cortical projections of                 b. Like Fig. 2b, c, this panel shows the result of projecting voxel-wise
dimensions 1–3 for subjects S1, S3 and S4. a, Voxel-wise semantic model           models onto the first three common semantic dimensions, and then
weights for subject S2 were projected onto each of the common semantic            colouring each voxel using an RGB colourmap. The red colour component
dimensions defined by PCs 1–4. Voxels for which model generalization              corresponds to the projection on the first PC, the green component to the
performance was not significantly greater than zero (q(FDR) >​  0.05) are         second, and the blue component to the third. Semantic information seems
shown in grey. Positive projections are shown in red, negative projections        to be represented in complex patterns distributed across the semantic
in blue and near-zero projections in white. Voxels with fMRI signal               system and the patterns seem to be largely conserved across individuals.




                                                    © 2016 Macmillan Publishers Limited. All rights reserved
 RESEARCH ARTICLE




Extended Data Figure 4 | PrAGMATiC atlas likelihood maps.                          areas where there are large semantic model weights (that is, the semantic
Comparison of actual semantic maps (Fig. 2, Extended Data Fig. 3) to               system) are much better explained by PrAGMATiC than by a null model
the maps generated from the PrAGMATiC atlas (Fig. 3). PrAGMATiC                    and thus appear red, while areas where the weights are small (that is,
atlases for the left and right hemispheres were fit using data from all            somatomotor cortex, visual cortex, and so on) are about equally well
seven subjects. The left hemisphere atlas has 192 total areas and the right        explained by both PrAGMATiC and the null model and thus appear white.
hemisphere has 128 (including non-semantic areas). Here we show the                Variance explained was computed by subtracting the PrAGMATiC atlas
actual semantic maps for four subjects (first column), the PrAGMATiC               from the actual semantic map (in the space of the four group semantic
atlas on each subject’s cortical surface (second column), the log likelihood       dimensions), squaring and summing the residuals and then dividing by
ratio of the actual semantic map under the PrAGMATiC atlas versus a                the sum of squares in the actual map. The variance explained maps show
null model (third column), and the fraction of variance in the semantic            that the PrAGMATiC atlas captures a large fraction of the variance in the
map that the PrAGMATiC atlas explains for each location on the cortical            semantic maps (37–47% in total).
surface (fourth column). The likelihood ratio maps show that most




                                                     © 2016 Macmillan Publishers Limited. All rights reserved
                                                                                                                                      ARTICLE RESEARCH




Extended Data Figure 5 | Comparison of PrAGMATiC models fit                        Some of these differences are due to statistical thresholding: a few areas
with different initial conditions. As with many clustering algorithms,             that were found to be significantly semantically selective in the best model
PrAGMATiC optimizes a non-convex objective function and so can                     are missing in the alternative model (see left medial prefrontal cortex),
find many potential locally optimal solutions. To reduce the effect of             and some significant areas in the alternate model are missing from the best
non-convexity on our results, we re-fit the model ten times (each time             model (left ventral occipital cortex). Other differences suggest alternative
with a different random initialization), and then selected the model fit that      parcellations for a few regions, where, for example, the same region of
yielded the best likelihood (that is, performance on the training set) as the      cortex is parcellated into three areas in the best model and four areas in the
PrAGMATiC atlas (Fig. 3). Here we show the PrAGMATiC atlas (top)                   alternative model. Yet it is clear that none of the differences between these
and the second best model out of the ten that were estimated (bottom).             two models are sufficient to change any of the interpretations given in the
The parcellations given by these two models are very similar. However,             main text.
there are a few differences, which illustrate uncertainty in the model.




                                                     © 2016 Macmillan Publishers Limited. All rights reserved
 RESEARCH ARTICLE




Extended Data Figure 6 | Semantic atlas for the LPC. The PrAGMATiC                 are marked with a plus) (bottom left and right). Bars show how completely
atlas divides the LPC into 15 areas in the left hemisphere and 13 areas in         this 12-category interpretation captures the average semantic model in
the right. Here we show the atlas for each hemisphere (top left and right),        each area. The LPC appears to be organized around the angular gyrus
three-dimensional brains indicating the location of the LPC (top middle),          (AG), with a core that is selective for social, emotional and mental
individual maps for two subjects in each hemisphere (bottom middle), and           concepts (L6, 7, 9, 11; R5, 7) and a periphery that is selective for visual,
the average predicted response of each area to the 12 semantic categories          tactile and numeric concepts (L2, 4, 5, 8, 10, 15; R6, 11).
identified earlier (responses consistently greater than zero across subjects




                                                     © 2016 Macmillan Publishers Limited. All rights reserved
                                                                                                                                      ARTICLE RESEARCH




Extended Data Figure 7 | Semantic atlas for the MPC. The PrAGMATiC                average semantic model in each area. Like the LPC, the MPC appears to
atlas divides the MPC into 14 areas in the left hemisphere and 10 areas           be organized around a core group of areas that are selective for social and
in the right. Here we show the atlas for each hemisphere (top left and            mental concepts (L6, 8, 10; R6, 7). Dorsolateral MPC areas (L2, 4; R1) are
right), three-dimensional brains indicating the location of the MPC               selective for visual and tactile concepts. Anterior dorsal areas (L5, 9; R4, 9)
(top middle), individual maps for two subjects in each hemisphere                 are selective for temporal concepts. Ventral areas (L11, 12, 14; R8) are
(bottom middle), and the average predicted response of each area to the           selective for professional, temporal and locational concepts. Just above the
12 semantic categories identified earlier (responses consistently greater         retrosplenial cortex one distinct area in each hemisphere is selective for
than zero across subjects are marked with a plus) (bottom left and right).        mental, professional and temporal concepts (L7; R3). Overall, the right
Bars show how completely the 12-category interpretation captures the              MPC responds more than the left MPC to mental concepts.




                                                    © 2016 Macmillan Publishers Limited. All rights reserved
 RESEARCH ARTICLE




Extended Data Figure 8 | Semantic atlas for the SPFC. The PrAGMATiC                the 12-category interpretation captures the average semantic model in
atlas divides the SPFC into 18 areas in the left hemisphere and 19 areas in        each area. The organization in the SPFC seems to follow the long
the right. Here we show the atlas for each hemisphere (top left and right),        rostro-caudal sulci and gyri of the dorsal frontal lobe. Posterior–lateral
three-dimensional brains indicating the location of the SPFC (top middle),         SPFC areas (L4, 6; R6, 9, 11) are selective for social, emotional, communal
individual maps for two subjects in each hemisphere (bottom middle), and           and violent concepts. Posterior superior frontal sulcus areas (L2, 3, 7, 8;
the average response of each area in the atlas to the 12 semantic categories       R1, 5, 7) are selective for visual, tactile and numeric concepts. The superior
identified earlier (responses consistently greater than zero across subjects       frontal gyrus contains a long strip of areas (L1, 5, 10, 12–15; R8, 12, 14–16)
are marked with a plus) (bottom left and right). Bars show how completely          selective for social, emotional, communal and violent concepts.




                                                     © 2016 Macmillan Publishers Limited. All rights reserved
                                                                                                                                  ARTICLE RESEARCH




Extended Data Figure 9 | Semantic atlas for the LTC. The PrAGMATiC               semantic categories identified earlier (responses consistently greater
atlas divides the LTC into eight areas in both the left and right                than zero across subjects are marked with a plus) (bottom left and right).
hemispheres. Here we show the atlas for each hemisphere (top left and            Bars show how completely the 12-category interpretation captures the
right), three-dimensional brains indicating the location of the LTC (top         average semantic model in each area. Anterior LTC areas (L4–8; R3–8) are
middle), individual maps for two subjects in each hemisphere (bottom             selective for social, emotional, mental and violent concepts. Posterior LTC
middle), and the average response of each area in the atlas to the 12            areas (L1–3; R1–2) are selective for numeric, tactile and visual concepts.




                                                   © 2016 Macmillan Publishers Limited. All rights reserved
 RESEARCH ARTICLE




Extended Data Figure 10 | Semantic atlas for the VTC. The PrAGMATiC              than zero across subjects are marked with a plus) (bottom left and right).
atlas divides the VTC into six areas in the left hemisphere and one area         Bars show how completely the 12-category interpretation captures the
in the right. Here we show the atlas for each hemisphere (top left and           average semantic model in each area. The VTC is relatively homogeneous:
right), three-dimensional brains indicating the location of the VTC              all areas are selective for numeric, tactile and visual concepts. Left VTC
(top middle), individual maps for two subjects in each hemisphere                areas close to the parahippocampal place area (PPA) are also selective for
(bottom middle), and the average response of each area in the atlas to the       locational concepts (L5–6).
12 semantic categories identified earlier (responses consistently greater




                                                   © 2016 Macmillan Publishers Limited. All rights reserved
                                                                                                                                    ARTICLE RESEARCH




Extended Data Figure 11 | Semantic atlas for the IPFC. The                       and right). Bars show how completely the 12-category interpretation
PrAGMATiC atlas divides the IPFC into 12 areas in the left hemisphere            captures the average semantic model in each area. Posterior IPFC areas
and 9 areas in the right. Here we show the atlas for each hemisphere             in the precentral sulcus (L1–3; R1, 2) are selective for visual, tactile and
(top left and right), three-dimensional brains indicating the location of        numeric concepts. Areas on the inferior frontal gyrus (L8; R4, 7) are
the IPFC (top middle), individual maps for two subjects in each hemisphere       selective for social and violent concepts. Areas in the inferior frontal sulcus
(bottom middle), and the average response of each area in the atlas to the       and anterior middle frontal gyrus (L4–7; R5–6) are selective for visual,
12 semantic categories identified earlier (responses consistently greater        tactile and numeric concepts. Areas in the orbitofrontal sulci (L10; R9) are
than zero across subjects are marked with a plus) (bottom left                   also selective for visual, tactile, numeric and locational concepts.




                                                   © 2016 Macmillan Publishers Limited. All rights reserved
 RESEARCH ARTICLE




Extended Data Figure 12 | Semantic atlas for the opercular and insular            categories identified earlier (responses consistently greater than
cortex. The PrAGMATiC atlas divides the opercular and insular cortex              zero across subjects are marked with a plus) (bottom left and right).
(OIC) into four areas in the left hemisphere and three areas in the right.        Bars show how completely the 12-category interpretation captures the
Here we show the atlas for each hemisphere (top left and right),                  average semantic model in each area. These areas are homogeneously
three-dimensional brains indicating the location of the OIC (top middle),         selective for abstract concepts, with more posterior and superior areas
individual maps for two subjects in each hemisphere (bottom middle),              also responding to emotional, communal and mental concepts.
and the average response of each area in the atlas to the 12 semantic




                                                    © 2016 Macmillan Publishers Limited. All rights reserved
