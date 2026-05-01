# DIVER-1: Deep Integration of Vast Electrophysiological Recordings at Scale

# DIVER-1: Deep Integration of Vast Electrophysiological Recordings at Scale

Danny Dongyeop Han^{∗,†,1} Yonghyeon Gwon^{∗,1} Ahhyun Lucy Lee^{∗,1} Taeyang Lee^{∗,1}
Seong Jin Lee^{1} Jubin Choi^{1} Sebin Lee^{1} Jihyun Bang^{1} Seungju Lee^{1}
David Keetae Park^{2} Shinjae Yoo^{2} Chun Kee Chung^{†,1} Jiook Cha^{†,1}
^{1} Seoul National University, Seoul, Republic of Korea
^{2} Brookhaven National Laboratory, New York, United States
^{∗} These authors contributed equally.
^{†} Correspondence to:
dyhan316@snu.ac.kr, chungc@snu.ac.kr, connectome@snu.ac.kr

###### Abstract

Unifying the vast heterogeneity of brain signals into a single foundation model is a longstanding challenge in neuroscience. Yet, even as large-scale pretraining becomes feasible, the field lacks principled guidance on how to scale EFMs under realistic data and compute constraints. We present the first systematic scaling law analysis spanning both EEG and iEEG and uncover a distinct “data-constrained” characteristic: unlike in language modeling, performance in electrophysiology is dominated first by data scale, followed by training duration (epochs), with model parameter count playing a subordinate role under fixed compute budgets. This challenges the prevailing “bigger is better” heuristic derived from LLMs. Building on these insights, we introduce DIVER-1, a family of models trained on the largest and most diverse corpus to date—59.3k hours (54k EEG + 5.3k iEEG) across 1.6M channel-hours from 17.7k+ subjects—scaling up to 1.82B parameters. By prioritizing data diversity and training horizons over mere parameter expansion, DIVER-1 achieves state-of-the-art performance across established benchmarks. Our work provides both a powerful generalist model and actionable guidelines for efficient development of future neuro-AI systems.

## 1 Introduction

Brain electrophysiology—scalp electroencephalography (EEG) and intracranial EEG (iEEG)—provides direct, millisecond-scale access to neural dynamics, enabling the study of rapid neural processes inaccessible to slower neuroimaging modalities *(Luck, 2014; Cohen, 2014)*. It supports applications spanning neuroscience, brain–computer interfaces, and clinical monitoring, leveraging EEG/iEEG as both a research instrument and a clinical-grade measurement*(Wolpaw et al., 2002; Tatum et al., 2022)*. However, electrophysiology is highly heterogeneous: signals vary across subjects, sessions, and brain states, and the sensing geometry itself changes across montages, channel counts, and electrode types. This heterogeneity is a primary barrier to transferable representations, and much recent electrophysiology foundation model (EFM) work has focused on objectives and architectures that explicitly cope with it rather than assuming a fixed sensor layout *(Wang et al., 2024c; Zhang et al., 2023; Chau et al., 2025)*.

A natural hypothesis is that scaling—in data, compute, and model capacity—can help absorb electrophysiological heterogeneity into a single reusable backbone. Indeed, a small but growing set of EFMs has begun to probe “scaling,” typically through coarse ablations over model capacity and/or pretraining corpus size, and reports additional downstream gains with increased scale *(Jiang et al., 2024; Wang et al., 2024b, c, 2023)*. However, it remains difficult to translate these findings into actionable guidance: explored regimes are still limited, and studies do not conduct compute-matched sweeps across multiple scaling axes (especially training duration). Moreover, it is unclear whether

---

these trends hold consistently across both EEG and iEEG. This stands in contrast to language modeling, where scaling laws provide concrete guidance for trading off model size and data under a fixed compute budget to achieve strong performance (Kaplan et al., 2020; Hoffmann et al., 2022).

This gap is critical as most EFMs are developed with limited compute, where the cost of turning the wrong scaling knob is high. Additionally, ephys introduces domain-specific knobs beyond model and dataset size. In particular, training duration (number of epochs) becomes a first-class knob because ephys corpora are far from internet-scale, making repeated passes over the same recordings largely unavoidable. For iEEG, subject diversity introduces yet another knob, reflecting a trade-off between collecting data from more subjects versus collecting more recordings per subject. As a result, "how to scale" in electrophysiology is not a single decision but a knob-setting problem: how to allocate a fixed compute budget across model size, training duration, and data scale and composition to maximize transfer.

![img-0.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-1.jpg)
Figure 1: Overview of DIVER-1 architecture and pretraining. DIVER-1 is pretrained on a large EEG and iEEG data corpus. After preprocessing, input patches are randomly masked and enhanced by adding modality, spectral, and CNN-based patch embeddings, along with STCPE. The enhanced patches are processed through MOIRAI blocks and trained to reconstruct missing patches across multiple signal domains (time series, spectrum, spectrogram). The pretrained model is then applied to diverse downstream tasks.

To provide principled guidance for this problem, we run controlled experiments that sweep multiple scaling axes while pushing into regimes large enough to test whether scaling behavior holds at much larger data/model scales. Specifically, we conduct the first systematic quantitative study that jointly varies dataset scale, model size, and training epochs, and validate conclusions across both modalities—scalp EEG and iEEG—to ensure the resulting guidance is not modality-specific. Concretely, we pretrain DIVER-1 on substantially larger corpora than prior work—over  $77 \times$  more iEEG data than the previous iEEG state-of-the-art model of Chau et al. (2025), and about  $10 \times$  more EEG data than Wang et al. (2024c)—and we evaluate models ranging from 13M to 1.82B parameters (up to  $3 \times$  larger than the largest open-source iEEG EFM) (Zhang et al., 2023).

---

These experiments reveals an actionable set of scaling knob settings: (i) turn the data knob as far as possible by acquiring more pretraining recordings, and (ii) under fixed data and compute budgets, turn the training-duration knob up—prioritizing longer training of smaller models over briefly training very large models (e.g., a 51M-parameter model trained for 32 epochs outperforms a 1.8B-parameter model trained for 8 epochs while using *less* compute). Importantly, these knob settings need not be chosen heuristically: the data-constrained scaling framework *(Muennighoff et al., 2023)* quantitatively predicts the compute-efficient allocation across model size, and epochs given fixed dataset size and compute. Guided by these insights, we introduce DIVER-1, a family of EEG and iEEG EFMs that achieves state-of-the-art performance with an architecture shaped by neuroscientifically motivated inductive priors; together with our scaling analysis, DIVER-1 provides a quantitative, modality-spanning scaling playbook for future EFM development.

The contributions of this work are threefold:

- A quantitative scaling playbook for EFMs: We provide actionable guidance for compute-limited Ephys pretraining: (i) increasing data scale yields the largest gains, and (ii) under fixed data and compute, allocating more budget to epochs can be more beneficial than pushing to $\geq$1B-parameter models. We further show these trade-offs are precisely captured by data-constrained scaling laws *(Muennighoff et al., 2023)*, which generalize classical Kaplan/Chinchilla-style scaling to the multi-epoch Ephys regime.
- A modality-spanning scaling study at unprecedented scale: We scale EFM pretraining to previously unattained regimes—$77\times$ more iEEG and $10\times$ more EEG data than prior work, and models up to 1.82B parameters—and show that the same data-constrained scaling behavior continues to hold at these scales across both scalp EEG and iEEG.
- DIVER-1 model family with flexible electrode embeddings: We introduce DIVER-1 and achieve state-of-the-art performance across EEG and iEEG benchmarks using ephystailored components that better embed diverse electrode sets and make the encoder flexible to varying channel layouts.

## 2 DIVER-1 Architecture

Motivated by the central challenge of electrophysiology—robust generalization under heterogeneous and variable electrode configurations—we design DIVER-1 (Deep Integration of Vast Electrophysiological Recordings) around a single goal: flexible, informative embeddings for diverse electrode sets. DIVER-1 uses an architecture custom-designed for EEG and iEEG that supports effective self-supervised pretraining via masked patch reconstruction (Figure 1). The architecture consists of four components: (1) *patch encoding*, (2) *embedding enhancements* to inject modality- and channel-aware inductive priors, (3) a stack of *MOIRAI blocks* *(Woo et al., 2024)* to process variable-channel inputs, and (4) *multi-output projection* for multi-domain reconstruction. During pretraining, we randomly mask 50% of input patches and train the model to reconstruct the missing content across multiple signal domains through the projection layer. The details of pretraining and architectural hyperparameters can be found in Appendix B.6.

### 2.1 Patch Encoding

We convert the raw signal into patch representations and extracts temporal features. Given an input time series $\mathbf{Y}\in\mathbb{R}^{C\times T}$, where $C$ is the number of channels (variables) and $T$ is the sequence length, we patchify $\mathbf{Y}$ into 1 or 0.1 second patches, each containing $P\in\{500,50\}$ timepoints (at 500Hz sampling rate). During pretraining, $50\%$ of the patches are randomly masked with zero, and the remaining patches are passed through a three layer patch-wise convolutional neural network (CNN) to extract temporal features. This results in a basic representation $\mathbf{Y}_{\text{CNN}}\in\mathbb{R}^{C\times N\times d_{\text{model}}}$, where $N = T/P$ is the number of patches and $d_{\text{model}}$ is the embedding dimension.

### 2.2 Embedding Enhancements

This section introduces three sub-modules developed for improved learning over heterogeneous signal and channel information.

---

#### Spectral embedding ($\mathbf{E}_{\text{spectral}}$).

$\mathbf{E}_{\text{spectral}}$ injects patch-wise frequency information by applying FFT to each patch and projecting the features to $d_{\text{model}}$ dimensions via a learnable linear layer.

#### Channel position and modality embeddings.

Both spatial electrode locations and electrode modality are jointly embedded to handle heterogeneous recording setups. While EEG follows standardized montages, iEEG channels are implanted in specific brain regions based on individual clinical needs. To address this heterogeneity, we encode both channel position embeddings $\mathbf{E}_{\text{position}}$ using the 3D spatial coordinates (registered to MNI space) and modality embeddings $\mathbf{E}_{\text{modality}}$ to distinguish between different electrode types. We then define the combined position–modality embedding term as:

$\left[\mathbf{E}_{\text{position}},\mathbf{E}_{\text{modality}}\right]=\left[\left(PE^{(d)}(d)\right)_{d\in\{x,y,z\}},\;\mathbf{E}_{\text{modality}}\right],$ (1)

where electrode coordinates $(x,y,z)$ are in mm and:

$PE^{(j)}_{2i}=\sin\!\left(\tfrac{j/256}{2000^{2l/2_{j}}}\right),\quad PE^{(j)}_{2i+1}=\cos\!\left(\tfrac{j/256}{2000^{2l/2_{j}}}\right)$ (2)

for $j\in\{x,y,z\}$ and $d_{x}=d_{y}=d_{z}=d_{\text{model}}/4$, following PopT *(Chau et al., 2025)*. If the coordinates x,y,z for a given channel are not available, the positional embedding for that channel is set to zero. The modality embedding $\mathbf{E}_{\text{modality}}$ is computed as $\mathbf{E}^{\text{type}}_{\text{modality}}+\mathbf{E}^{\text{subtype}}_{\text{modality}}$, where $\mathbf{E}^{\text{type}}_{\text{modality}}$ distinguishes between EEG and iEEG channels, and $\mathbf{E}^{\text{subtype}}_{\text{modality}}$ encodes electrode subtypes (grid, strip, or depth for iEEG electrodes) through learnable embedding vectors shared across all patches within the same category.

#### Spatio-Temporal Conditional Positional Embedding (STCPE).

STCPE addresses the need for positional encodings that remain valid under heterogeneous and variable electrode configurations. Transformers require positional information because self-attention is inherently permutation-invariant. In vision, this is often handled with fixed positional encodings; in contrast, *Conditional Positional Encoding* (CPE) *(Chu et al., 2021)* injects position via lightweight convolutions over local neighborhoods, allowing the encoding to adapt to the structure of each input. Building on this idea, *Asymmetric Conditional Positional Encoding* (ACPE) *(Wang et al., 2024c)* applies asymmetric convolutions across channels and time for EEG. However, ACPE’s channel-wise convolutions are defined along a fixed channel axis and therefore do not preserve channel permutation equivariance: the learned spatial relationships depend on the training-time channel order. This is a critical limitation for electrophysiology, where robust transfer requires invariance to arbitrary electrode re-orderings and flexibility across montages, recording systems, and channel counts.

To address this, *STCPE* replaces convolution with a sliding-window MOIRAI transformer block that computes channel-permutation-equivariant positional encodings. After patch encoding, embeddings are first projected to a reduced dimension using $P_{b}:\mathbb{R}^{d_{\text{model}}}\rightarrow\mathbb{R}^{d_{\text{model}}/8}$ for computational efficiency. A temporal window of width $w$ (stride 1) is then applied to the projected sequence. Let $m=(w - 1)/2$. For each window centered at index $t^{\prime}$, MOIRAI receives the spatiotemporal slice $\mathbf{X}_{[:,\,t^{\prime}-m:t^{\prime}+m,:]}\in\mathbb{R}^{C\times w\times(d_{\text{model}}/8)}$ and produces $w$ outputs—one per relative temporal offset:

$\mathbf{H}_{t^{\prime}}=\text{MOIRAI}\!\left(\mathbf{X}_{[:,\,t^{\prime}-m:t^{\prime}+m,:]}\right)\in\mathbb{R}^{C\times w\times(d_{\text{model}}/8)}.$

The STCPE embedding at absolute time $t$ aggregates contributions from all overlapping windows, and the original dimension is restored with $P_{7}$, yielding the final STCPE embedding:

$\mathbf{E}_{\text{STCPE}}[:,t,:]$ $=P_{7}\!\left(\sum_{{k=-m}}^{{m}}\mathbf{H}_{t+k}[:,\,k + m,:]\right)$ (3)
$\in\mathbb{R}^{C\times w\times(d_{\text{model}})},$ $t = 1,\ldots,N.$

STCPE thus provides input-dependent positional information while maintaining both temporal translation equivariance (via temporal sliding windows) and channel permutation equivariance (via MOIRAI blocks)—properties that ACPE lacks.

---

Overall inputs.

The final transformer input is computed as:

$\mathbf{X}=\mathbf{Y}_{\text{CNN}}+\mathbf{E}_{\text{spectral}}+\left[\mathbf{E}_{\text{position}},\mathbf{E}_{\text{modality}}\right]+\mathbf{E}_{\text{STCPE}}$ (4)

where $[\cdot,\cdot]$ denotes concatenation, and each embedding component $\mathbf{E}_{\cdot}\in\mathbb{R}^{C\times N\times d_{\text{model}}}$ maintains the same dimensional structure to ensure consistent element-wise addition.

### 2.3 MOIRAI Block

Any-variate attention. Unlike vanilla attention mechanisms that rely solely on input embeddings to differentiate between tokens and model their relationships, any-variate attention *(Woo et al., 2024)* enables adaptive spatial modeling across heterogeneous electrode configurations by directly embedding spatio-temporal information into the attention computation itself through two main components: Rotary Position Embedding (RoPE) *(Su et al., 2024)* and binary attention bias.

Given input $\mathbf{X}\in\mathbb{R}^{C\times N\times d_{\text{model}}}$, the attention score between the $(i,m)$-th query (where $i$ denotes the patch index and $m$ denotes the channel index) and the $(j,n)$-th key is computed as $A_{ij,mn}=\frac{\exp\{E_{ij,mn}\}}{\sum_{k,n}\exp\{E_{ik,mc}\}}$, where $E_{ik,mc}$ is computed as (we omit layer and attention head indices as well as scaling factors for clarity):

$$
 \begin{split}E_{ij,mn}=&(\mathbf{W}^{Q}\bm{x}_{i,m})^{T}\mathbf{R}_{i-j}(\mathbf{W}^{K}\bm{x}_{j,n})\\
&+u^{1}\cdot\mathbbm{1}_{\{m=n\}}+u^{2}\cdot\mathbbm{1}_{\{m\neq n\}}\end{split}
$$
 (5)

where $\mathbf{W}^{Q}\bm{x}_{i,m},\mathbf{W}^{K}\bm{x}_{j,n}\in\mathbb{R}^{d_{h}}$ are the query and key vectors, $\mathbf{R}_{i-j}\in\mathbb{R}^{d_{h}\times d_{h}}$ is the rotary projection matrix encoding temporal relationships, $u^{1},u^{2}\in\mathbb{R}$ are learnable scalars that can differ across attention heads, and $\mathbbm{1}_{\{cond\}}=1$ if the condition is true and $0$ otherwise.

Spatio - temporal register tokens. Following register tokens in vision transformers *Darcet et al. (2023)*, we augment the $C\times N$ token grid with learnable registers for channel, temporal, and joint spatio - temporal information. This transforms input token grid shape from $C\times N\times d_{\text{model}}$ to $(C+1)\times(N+1)\times d_{\text{model}}$. These registers provide dedicated workspace for auxiliary computations without perturbing the primary Ephys representations.

### 2.4 Multi - Output Projection

We perform reconstruction across multiple signal domains during pretraining. Refined spatio - temporal representations are linearly projected to reconstruct patches in three complementary domains: raw time series, FFT, and STFT. This multi - domain reconstruction objective encourages comprehensive learning of temporal and spectral properties.

## 3 Training and Experimental Setup

### 3.1 Pretraining

DIVER - 1 employs self - supervised pretraining based on masked patch reconstruction.

Multi - domain reconstruction objective. Rather than reconstructing only raw time series, DIVER - 1 utilizes a multi - output projection architecture that maps each learned patch representation $\mathbf{h}_{c,n}\in\mathbb{R}^{d_{\text{model}}}$ to three complementary signal domains through parallel linear transformations. For each patch $(c,n)$, the representation is projected to: (1) raw time series $\hat{\mathbf{y}}^{\text{raw}}_{c,n}\in\mathbb{R}^{P}$ to reconstruct temporal dynamics, (2) FFT coefficients $\hat{\mathbf{y}}^{\text{FFT}}_{c,n}\in\mathbb{R}^{P/2+1}$ to capture frequency domain characteristics, and (3) STFT spectrogram $\hat{\mathbf{y}}^{\text{STFT}}_{c,n}\in\mathbb{R}^{F\times T_{r}}$ to model time - frequency relationships, with specific FFT and STFT parameters detailed in Appendix B.5.

The total pretraining loss aggregates reconstruction errors across all masked patches and all signal domains:

$\mathcal{L}_{\text{total}}=\sum_{(c,n)\in\mathcal{M}}\sum_{k\in\mathcal{K}}\lambda_{k}\,\mathcal{L}_{\text{MSE}}\!\left(\mathbf{y}^{(k)}_{c,n},\hat{\mathbf{y}}^{(k)}_{c,n}\right)$ (6)

## #

---

$\mathcal{K}=\{\mathrm{raw},\mathrm{FFT},\mathrm{STFT}\}$ denotes the set of signal domains, $\lambda_{k}$ is the corresponding loss weight for domain $k$ and $\mathcal{M}$ denotes the set of masked patch indices. We used $(\lambda_{k})_{k\in\mathcal{K}}=(1,0.1,1)$ for 1 s patches model and $(1,1,0)$ for 0.1 s patches.

Input resampling. To train the model to handle heterogeneous channel layouts and variable sequence lengths, we feed only a randomly resampled subset of each 30 s training segment. A 30 s window yields $N{=}30$ patches for 1 s granularity and $N{=}300$ for 0.1 s. We then sample $C^{\prime}\leq\min(C,32)$ channels and $N^{\prime}\leq 30$ temporal patches, with both $C^{\prime}$ and $N^{\prime}$ drawn from a scaled $\mathrm{Beta}(3,1)$ distribution that favors larger subsets. Capping $N^{\prime}$ at 30 prevents the 0.1 s model from processing the full 300-patch sequence, keeping its effective context comparable to the 1 s model and avoiding excessive compute. This stochastic subsampling exposes the model to diverse channel sets and window lengths across epochs.

Pretraining dataset. DIVER was pretrained on, to our knowledge, the largest and most diverse collection of Ephys datasets compared to previous EFMs. Our pretraining data encompasses diverse recording conditions including task-based experiments, resting-state recordings, and sleep studies, ensuring robust representation learning across different brain states. The pretraining datasets are summarized in Table 3 with further details in Appendix F.1. All data underwent QAQC, minimal preprocessing, and resampling with the goal of preserving as much of the original signal as possible. Please refer to Appendix F.3 for more details.

Scaling. As DIVER-1 extends the scale of EFMs, we require methods to transfer optimal hyperparameters across different model sizes. In standard parameterizations, optimal hyperparameters are highly dependent on model width. Maximal Update Parametrization ($\mu P$) *(Yang et al., 2022)*, by carefully scaling initializations and learning rates, ensures consistent weight update magnitudes as model width increases. This enables $\mu$Transfer, where optimal hyperparameters from small models can be directly transferred to large models, precluding expensive hyperparameter tuning.

Training details. DIVER-1 was pretrained on either 128, 48, 32 NVIDIA A100 GPUs or 32, 24, 16 H200 GPUs, depending on the experimental configuration. We tested models varying in number of parameters, from 12.72M to 1.83B as in Table 2. Additional training details are provided in Appendix section B.4. We conducted comprehensive scaling law experiments across four dimensions: compute (training epochs 1-64), model size (varying width), dataset size (1-100% of available data), and subject diversity (2-16 subjects with fixed dataset size). Detailed experimental settings and scaling behaviors are provided in the Appendix.

### 3.2 Finetuning

Benchmark datasets. For iEEG downstream evaluation, we use Neuroprobe *(Zahorodnii et al., 2025)*, which provides 15 auditory, visual, and language decoding tasks from naturalistic movie-watching iEEG, and MAYO dataset *(Bbrinkm and Cukierski, 2014)*(seizure detection). For EEG, we use: FACED *(Chen et al., 2023)* (emotion decoding), PhysioNet-MI *(Goldberger et al., 2000)* (motor-imagery decoding), and MentalArithmetic *(Zyma et al., 2019)* (cognitive-workload decoding). Refer to Appendix F.2 for more details.

Baseline models. We evaluate DIVER-1 against state-of-the-art foundation models across both modalities: LaBraM *(Jiang et al., 2024)* and CBraMod *(Wang et al., 2024c)* for EEG, and BrainBERT *(Wang et al., 2023)*, Population Transformer (PopT) *(Chau et al., 2025)* and Brant *(Zhang et al., 2023)* for iEEG. These transformer-based models employ self-supervised pretraining strategies; LaBraM, CBraMod, BrainBERT, and Brant use masked patch reconstruction objectives while PopT applies discriminative self-supervised learning on BrainBERT embeddings.

Finetuning methods. For iEEG downstream tasks, we evaluate both linear probing and full finetuning using a linear classifier head on the flattened token representations. Linear probing freezes the encoder and trains only the classifier, providing a clean measure of representation quality. Full finetuning updates all encoder parameters together with the linear head. Details are in Appendix B.8. For EEG downstream tasks, we follow CBraMod’s finetuning protocol *(Wang et al., 2024c)*, jointly training the encoder and a three-layer MLP classifier. This MLP generally outperforms a linear head on EEG benchmarks, and depth-dependent results are provided in Appendix Table 23.

---

![img-1.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-2.jpg)
Figure 2: Contrasting scaling laws between DIVER-1 and LLMs. Each colored region shows how much each factor should be scaled (assuming compute optimal scaling) (multiplicative contribution) when total compute increases (with epoch fixed to two). Both DIVER-1 variants (left (iEEG) and middle (EEG)) demonstrates that data is the critical bottleneck for EFMs, requiring proportionally much larger increases in dataset size relative to model size. In contrast, LLM training (right) (adapted from Kaplan et al. (2020)) optimally allocates increased compute primarily to model size with minimal data growth, indicating that EFM are fundamentally more data-limited than LLMs.

# 4 RESULTS AND DISCUSSION

# 4.1 SCALING LAW

We systematically investigate multi-dimensional scaling laws to understand how EFMs scale with computational resources and data. Our analysis primarily uses (1) pretext-task loss (reconstruction loss during self-supervised pretraining) and (2) downstream-task performance across diverse Ephys benchmarks. We vary both traditional scaling axes (compute budget, dataset size, model size) and EFM-specific factors (training epochs, subject diversity).

Overall scaling law validation. Both iEEG and EEG EFMs exhibit neural scaling behaviors that aligns with the established Kaplan scaling laws (Kaplan et al., 2020), as shown in Figure 3 (a-c, e-g). Our empirical studies further show they also follow the more general data-constrained scaling law framework (Muennighoff et al., 2023):

$$
L (N, D) = \frac{A}{\left(N ^ {\prime}\right) ^ {\alpha}} + \frac{B}{\left(D ^ {\prime}\right) ^ {\beta}} + E \tag {7}
$$

where  $N^{\prime}$  and  $D^{\prime}$  are diminishing returns with more epochs:

$$
D ^ {\prime} = U _ {D} + U _ {D} R _ {D} ^ {*} \left(1 - e ^ {- \frac {R _ {D}}{R _ {D} ^ {*}}}\right), \tag {8}
$$

$$
N ^ {\prime} = U _ {N} + U _ {N} R _ {N} ^ {*} \left(1 - e ^ {- \frac {R _ {N}}{R _ {N} ^ {*}}}\right).
$$

where  $U_{D}$ ,  $R_{D}$ , and  $R_{D}^{*}$  corresponds to unique data tokens, repetitions (epochs - 1), and the "half - life" of repeated data, respectively (see Appendix A.2 and C.3 for details). This set - up provides quantitative evidence that scaling EFMs across compute, dataset size, model parameters, and training epochs - a dimension largely unexplored in EFM scaling - predictably and logarithmically improves performance. The scaling relationships derived with DIVER - 1 exhibit strong log - log fits in iEEG EFMs, with  $R^{2}$  values of 0.8152 for patch size 1 second models and 0.7718 for patch size 0.1 second models (Appendix Table 8), confirming the validity of the power-law scaling framework (additional results in Appendix C.5). Standard scaling axes (model, data, compute): We observe in Figure 3 (a-c, e-g) the expected power-law relationships across standard dimensions. Model size, dataset size, and compute budget scaling logarithmically reduces loss, following Kaplan et al. (2020), though Ephys data limitations necessitate data-constrained formulation. EFM-specific scaling axes (epoch, subject number): Beyond the traditional dimensions of model size, dataset size, and compute budget, we identify two novel scaling dimensions relevant to Ephys.

---

Finding 1. *Epoch scaling* in Figure 3 (d,h) shows increasing epochs improves performance across all model sizes, and larger models achieve lower loss when given sufficient repetitions. However, overly large models (e.g., XXL in Figure 3 (d) and Large in Figure 3 (h)) perform worse at very small epoch counts, only surpassing smaller models after many more epochs—consistent with the data-constrained scaling law, where repeated passes increase the effective dataset size $D^{\prime}$ required for large-capacity models.

Finding 2. *Subject diversity scaling* in Figure 3 (i) shows that under fixed training data volume, there exists an optimal balance between the number of subjects and data per subject.

Finding 3. While increases in model size and training epochs both improve performance, they also raise compute level, making it necessary to balance the two. To study this trade-off under fixed compute, we use the empirical IsoLoss landscape with IsoCompute curves (Figure 3(p), left), which map parameter–epoch pairs to equal FLOPs. The contours reveal a clear trend: at any fixed compute level, smaller and mid-sized models achieve lower loss than larger models. Thus, within realistic compute budgets, allocating resources toward training smaller models longer is more effective than briefly training very large models. We revisit this in the Practical Implications section using predicted IsoLoss contours (Figure 3(p), right).

Finding 4. Our fitted data-constrained scaling law parameters reveal important domain-specific characteristics (Appendix Table 8). Most notably, EFMs exhibit smaller $R_{N}^{*}$ values (3.39 for 1s patch sizes and 0.72 for 1s) compared to language models (5.30) *(Muennighoff et al., 2023)*. This indicates that increasing model parameters yields diminishing returns more rapidly in Ephys modeling than in language modeling, consistent with our observations that smaller models often suffice for EFM tasks.

Finding 5. The $R_{D}^{*}$ values exhibit interesting patch-size dependence: 8.91 for 1s patches versus 20.09 for 0.1s patches, compared to 15.38 for language models. This suggests that while 1s models experience faster diminishing returns from repeated epochs than language models, 0.1s models retain efficacy from additional epochs for longer durations. This behavior aligns with our data sampling strategy—0.1s models sample up to 3s context windows from original 30s segments, creating genuine ”multiple views” of the underlying data compared to 1s models.

#### Downstream performance.

Downstream performance scaling roughly mirrors pretraining behavior. Scaling with dataset size yields consistent gains, whereas scaling model size produces mixed effects (Figure 3(j,k,m,n)), similar to *Anonymous (2026)*. In iEEG tasks, larger models perform comparably to smaller ones, while in EEG tasks performance continues to improve up to 813M parameters. Across training duration, performance generally improves up to 32 epochs for both iEEG and EEG tasks, although iEEG exhibits a slight decline at 64 epochs (Figure 3(i,o)). The stronger benefit of dataset scaling relative to model scaling may be explained by the much larger reductions in test loss achieved via data scaling, as seen by comparing Figures 3(c,g) with Figures 3(b,f), and quantified in Figure 2. The weak sensitivity to model size in iEEG may reflect the smaller effective sample size available in iEEG pretraining.

#### Practical Takeaway.

These findings have direct relevances for resource allocation in EFM. Because the domain is data-constrained, the optimal compute strategy differs from that of language or vision: smaller models trained for more epochs outperform larger models trained briefly under fixed compute budgets. The IsoLoss and IsoCompute structure in Figure 3(p, left) indicates that large models are compute-inefficient at realistic epoch counts. Building on this observation, Figure 3(p, right) defines a clear “compute-optimal frontier” that specifies the most efficient combinations of model size and training duration. Prior EFMs tend to fall outside this frontier, often emphasizing increased model size over additional training repetitions (Appendix G). Our scaling framework provides a principled insight for selecting compute-optimal points before launching expensive pretraining. However, when the goal is to achieve the highest possible performance for a given model size, training beyond the compute-optimal frontier is still beneficial. This was the case for our Small iEEG model, and also applied to CBraMod *(Wang et al., 2024c)* and BIOT *(Yang et al., 2023)*, when trained substantially past their compute-optimal points.

---

# 4.2 DECODING PERFORMANCE

As shown in Figure 3(q)-(t), DIVER-1 achieves state-of-the-art decoding performance across iEEG and EEG benchmarks. On the iEEG downstream dataset, our 13M-parameter model surpasses nearly all prior approaches—including BrainBERT (43M) (Wang et al., 2023), PopT (63M)(Chau et al., 2025), and Brant (506M) (Zhang et al., 2023)—across almost all 15 tasks in Neuroprobe binary-label tasks and by a large margin in MAYO. For Neuroprobe Multi-label tasks, our model still outperforms the linear STFT laplacian which surpasses other models. On EEG downstream tasks, DIVER-1 also establishes new SOTA results, outperforming C BraMod (Wang et al., 2024c) and LaBraM (Jiang et al., 2024) on FACED emotion recognition (Chen et al., 2023), PhysioNet-MI motor imagery (Goldberger et al., 2000), and MentalArithmetic workload decoding (Zyma et al., 2019). Full task-level values for all benchmark results are provided in Appendix Section D.1. We also evaluated DIVER-1 on additional EEG downstream tasks, where we identified a methodological (reproduction) problem. To ensure fair comparison and facilitate replicability, we conducted a controlled investigation by standardizing the finetuning method across models and comparing performance over seven different methods. We find that under controlled finetuning settings, DIVER-1 also achieves comparable or superior performance to the other baseline models (Appendix Table 25). Linear probing analysis further demonstrates that DIVER learns high-quality representations (Appendix Section E.5). Detailed experimental procedures and results are provided in Appendix Section E.

The strong performances over NeuroProbe are particularly notable given the pretraining-finetuning distribution shift under which DIVER-1 was trained. Unlike PopT or BrainBERT, DIVER-1 was pretrained on different datasets than those used for finetuning, on adult data rather than pediatrics, and using both ECoG and SEEG modalities rather than exclusively SEEG data. Moreover, DIVER-1 is much smaller (13M) than the other models (BrainBERT: 43M, PopT: 63M). This highlights the robustness of our representations across dataset shifts and recording modalities.

# 4.3 ABLATION STUDIES

To disentangle architectural contributions to performance from the pretraining data-scale, we evaluate all models pretrained on the same dataset (BrainTreebank; Table 1). Under this controlled setting, DIVER still outperforms BrainBERT and PopT on downstream tasks, indicating that the gains are not solely attributable to larger pretraining corpora.

Table 1: Controlled comparison using BrainTreebank (BTB). Models are pretrained on the same BTB corpus to isolate architectural effects. Results are mean AUROC ± SEM across subjects, trials, and folds (DIVER: 32 pretraining epochs).

| Model | speech | onset |
| --- | --- | --- |
| BrainBERT (frozen)* | 0.611 ± 0.022 | 0.757 ± 0.027 |
| PopT* | 0.677 ± 0.044 | 0.689 ± 0.050 |
| DIVERDay&0.1s (frozen) | 0.770 ± 0.028 | 0.859 ± 0.018 |

* results from Neuroprobe (Zahorodnis et al., 2025)

Architecture ablations (Appendix Tables 18, 19) indicate most components are contributing to the final performance, including any-variate attention, RoPE, STCPE, and the multi-domain reconstruction objectives. The main exception was the iEEG absolute channel-position embedding, whose ablation improved performance. We hypothesize this reflects a pretraining-downstream distribution shift: pretraining uses adult population data, whereas Neuroprobe consists only of child/adolescent subjects, so age-related differences in brain size/geometry and electrode localization may miscalibrate absolute 3D positional embeddings, reducing their transferability and decreasing performance.

---

![img-2.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-3.jpg)
Figure 3: Scaling laws and downstream performance of DIVER-1. (a-h) Scaling law validation: DIVER-1 follows data-constrained scaling laws across four dimensions for iEEG (a-d) and EEG (e-h) modalities. Loss decreases predictably with increased (a,e) compute (training FLOPs), (b,f) dataset size (number of tokens), (c,g) model size (parameters), and (d,h) training epochs, with strong log-log fits. iEEG experiments (a-d) used  $100\%$  of the dataset, while EEG experiments used  $20\%$  of the dataset for (e,h) and  $100\%$  for (f,g). (q-t) Downstream performance: Performance for iEEG (i-l) and EEG (m-o) across increasing (i) number of subjects while keeping dataset size identical, (j,m) dataset size (k,n) model sizes and (l,o) epochs. (p) Compute-Optimal Frontier (IsoLoss analysis): Comparison between empirical isolation loss contours and predicted isolation loss contours, with model configurations plotted to show the relationship between training epochs and model parameters under fixed compute budgets. (q) Neuroprobe benchmark results Comprehensive performance (AUROC) comparison across multiple neural decoding tasks, with  $\mathrm{DIVER}_{\mathrm{Tiny} / \mathrm{I} / 0.1s}$  achieving state-of-the-art or competitive results on most tasks.  $\mathrm{DIVER}_{\mathrm{Tiny} / \mathrm{I} / 0.1s}$  with  $d_{\mathrm{model}} = 256$  and patch size 0.1s was pretrained on iEEG dataset for 32 epochs, past the compute optimal frontier for best performance. Performance with linear probing (red) and full finetuning (black) are shown. (r, s) iEEG downstream performance (r) Neuroprobe multi-label classification results using  $\mathrm{DIVER}_{\mathrm{Small} / \mathrm{I} / 0.1s}$ . (s) MAYO(seizure detection task) results using  $\mathrm{DIVER}_{\mathrm{Small} / \mathrm{I} / 1s}$  (t). EEG downstream performance: DIVER-1 showed competitive performance compared to other EEG foundation models (C BraMod and LaBraM-base) on the FACED, PhysioNet-MI, and MentalArithmetic datasets. Results shown are obtained using full finetuning. The DIVER model refers to  $\mathrm{DIVER}_{\mathrm{Small} / \mathrm{IE} / 1s}$  with  $d_{\mathrm{model}} = 512$  and patch size 1s pretrained on iEEG and EEG datasets for 16 epochs. Other baseline results are replicated using their official code. Performance values for C BraMod and LaBraM are reported from their original publications.

---

5 Conclusion

This work presents the first systematic investigation of scaling laws for Ephys foundation models (EFMs), across both scalp-EEG and iEEG modalities. We introduce DIVER-1, a family of EEG/iEEG foundation models ranging from 13M to 1.82B parameters, designed with electrophysiology-specific inductive priors. Our analysis shows that EFMs operate in a data-constrained regime with scaling behavior that fundamentally differs from language models. Through unprecedented scaling across data, model size, and compute, DIVER-1 achieves state-of-the-art performance across various iEEG and EEG tasks.

Our findings underscore that data, not model capacity, is the critical bottleneck for EFM progress. Substantial quantities of ephys data remain untapped in laboratories worldwide. We therefore advocate for open science and community-driven efforts to curate large-scale public datasets. Importantly, our scaling analysis shows that competitive EFMs can be trained even under limited computational budgets by prioritizing longer training durations with small models, lowering the barrier to foundation model development for academic groups with modest GPU resources.

Looking ahead, these findings establish the foundation for a new generation of EFM development by demonstrating that Ephys requires tailored scaling strategies, rather than direct application of scaling laws from other domains. While the precise scaling law parameters and optimal ratios we derived are tied to our particular architecture and pretraining objective, the central insight—that data-constrained regimes favor extended training over increased model size—constitutes a broadly applicable principle for future EFM development.

## 6 Impact Statement

This work presents controlled scaling experiments across compute, data, and model capacity for electrophysiology foundation models (EFMs) in both scalp EEG and intracranial EEG (iEEG). We identify a data-constrained regime in which compute-efficient performance is achieved by balancing model size with extended multi-epoch training, rather than by increasing parameter count alone. These findings provide practical guidance for allocating limited computational resources when training EFMs.

We plan to release our pretrained models under an open-science framework to support reuse in brain–computer interface and clinical applications. Our conclusions are specific to EEG and iEEG under the modeling and training settings studied here, and scaling behavior may differ for other modalities such as MEG or fMRI.

## 7 Acknowledgement

This work was supported by the National Research Foundation of Korea (NRF) grant funded by the Korea government (MSIT) (No. 2021R1C1C1006503, RS-2023-00266787, RS-2023-00265406, RS-202400421203, RS-2024-00421268, RS-2024-00342301, RS-2024-00435727, RS-2025-25457239, RS-2021-NR061370, NRF-2021M3E5D2A01022515, and NRF-2021S1A3A2A02090597), Alchemist Brain to X (B2X) Project funded by the Ministry of Trade, Industry and Energy (No.20012355, NTIS:1415181023) and by the Researchers Program through Seoul National University (No. 200-20250071, 200-20250049, 200-20250116, 200-20250115, 200-20250113). Additional support was provided by the Institute of Information & Communications Technology Planning & Evaluation (IITP) grant funded by the Korea government (MSIT) [No. RS-2021-II211343, Artificial Intelligence Graduate School Program, Seoul National University] and by the Global Research Support Program in the Digital Field (RS-2024-00421268). This work was also supported by the Artificial Intelligence Industrial Convergence Cluster Development Project funded by the Ministry of Science and ICT and Gwangju Metropolitan City, by the Korea Brain Research Institute (KBRI) basic research program (25-BR-05-01), by the Korea Health Industry Development Institute (KHIDI) and the Ministry of Health and Welfare, Republic of Korea (HR22C1605), and by the Korea Basic Science Institute (National Research Facilities and Equipment Center) grant funded by the Ministry of Education (RS-2024-00435727). We acknowledge the National Supercomputing Center for providing supercomputing resources and technical support (KSC-2023-CRE-0568).

# #

---

An award for computer time was provided by the U.S. Department of Energy’s (DOE) ASCR Leadership Computing Challenge (ALCC). This research used resources of the National Energy Research Scientific Computing Center (NERSC), a DOE Office of Science User Facility, under ALCC award m4750-2024, and supporting resources at the Argonne and Oak Ridge Leadership Computing Facilities, U.S. DOE Office of Science user facilities at Argonne National Laboratory and Oak Ridge National Laboratory.

The BNL team was supported by the U.S. Department of Energy (DOE), Office of Science (SC), Advanced Scientific Computing Research program under award DE-SC-0012704 and used resources of the National Energy Research Scientific Computing Center, a DOE Office of Science User Facility using NERSC award DDR-ERCAP0033558.

## References

- Abnar and Zuidema [2020] Samira Abnar and Willem Zuidema. Quantifying attention flow in transformers. *arXiv preprint* arXiv:2005.00928, 2020.
- Akiba et al. [2019] Takuya Akiba, Shotaro Sano, Toshihiko Yanase, Takeru Ohta, and Masanori Koyama. Optuna: A next-generation hyperparameter optimization framework. *CoRR*, abs/1907.10902, 2019. URL http://arxiv.org/abs/1907.10902.
- Chou et al. [2026] Anonymous. Are EEG foundation models worth it? comparative evaluation with traditional decoders in diverse BCI tasks. In *The Fourteenth International Conference on Learning Representations*, 2026. URL https://openreview.net/forum?id=5Xwm8e6vbh.
- Bärnkm and Cukierski [2014] S Bärnkm and W Cukierski. Upenn and mayo clinic’s seizure detection challenge, 2014.
- Chen et al. [2023] Geeling Chau, Christopher Wang, Sabera Talukder, Vighnesh Subramaniam, Saraswati Soedarmadji, Yisong Yue, Boris Katz, and Andrei Barbu. Population transformer: Learning population-level representations of neural activity. *ArXiv*, pp. arXiv–2406, 2025.
- Chen et al. [2020] Jingjing Chen, Xiaobin Wang, Chen Huang, Xin Hu, Xinke Shen, and Dan Zhang. A large finer-grained affective computing eeg dataset. *Scientific Data*, 10(1):740, 2023.
- Chen et al. [2024] Ting Chen, Simon Kornblith, Mohammad Norouzi, and Geoffrey Hinton. A simple framework for contrastive learning of visual representations. In *International conference on machine learning*, pp. 1597–1607. PmLR, 2020.
- Chen et al. [2021] Yuqi Chen, Kan Ren, Kaitao Song, Yansen Wang, Yifan Wang, Dongsheng Li, and Lili Qiu. Eegformer: Towards transferable and interpretable large-scale eeg foundation model. *arXiv preprint* arXiv:2401.10278, 2024.
- Chu et al. [2024] Xiangxiang Chu, Zhi Tian, Bo Zhang, Xinlong Wang, and Chunhua Shen. Conditional positional encodings for vision transformers. *arXiv preprint* arXiv:2102.10882, 2021.
- Cohen et al. [2014] Mike X. Cohen. Analyzing Neural Time Series Data: Theory and Practice. MIT Press, 2014. URL https://direct.mit.edu/books/monograph/4013/analyzing-neural-time-series-datatheory-and.
- Cui et al. [2024] Wenhui Cui, Woojae Jeong, Philipp Thölke, Takfarinas Medani, Karim Jerbi, Anand A Joshi, and Richard M Leahy. Neuro-gpt: Towards a foundation model for eeg. In *2024 IEEE International Symposium on Biomedical Imaging (ISBI)*, pp. 1–5. IEEE, 2024.
- Darcet et al. [2023] Timothée Darcet, Maxime Oquab, Julien Mairal, and Piotr Bojanowski. Vision transformers need registers. *arXiv preprint* arXiv:2309.16588, 2023.
- Dehaene and Cohen [2011] Stanislas Dehaene and Laurent Cohen. The unique role of the visual word form area in reading. *Trends in cognitive sciences*, 15(6):254–262, 2011.
- Dehene and Fiederici [2011] Angela D Fiederici. The brain basis of language processing: from structure to function. *Physiological reviews*, 91(4):1357–1392, 2011.

---

Ary L Goldberger, Luis AN Amaral, Leon Glass, Jeffrey M Hausdorff, Plamen Ch Ivanov, Roger G Mark, Joseph E Mietus, George B Moody, Chung-Kang Peng, and H Eugene Stanley. Physiobank, physiotoolkit, and physionet: components of a new research resource for complex physiologic signals. circulation, 101(23):e215–e220, 2000.

Gregory Hickok and David Poeppel. The cortical organization of speech processing. Nature reviews neuroscience, 8(5):393–402, 2007.

Jordan Hoffmann, Sebastian Borgeaud, Arthur Mensch, Elena Buchatskaya, Trevor Cai, Eliza Rutherford, Diego de Las Casas, Lisa Anne Hendricks, Johannes Welbl, Aidan Clark, Tom Hennigan, Eric Noland, Katie Millican, George van den Driessche, Bogdan Damoc, Aurelia Guy, Simon Osindero, Karen Simonyan, Erich Elsen, Jack W. Rae, Oriol Vinyals, and Laurent Sifre. Training compute-optimal large language models, 2022. URL https://arxiv.org/abs/2203.15556.

Wei-Bang Jiang, Li-Ming Zhao, and Bao-Liang Lu. Large brain model for learning generic representations with tremendous eeg data in bci. arXiv preprint arXiv:2405.18765, 2024.

Michael J. Kahana, Joseph H. Rudoler, Lynn J. Lohnas, Karl Healey, Ada Aka, Adam Broitman, Elizabeth Crutchley, Patrick Crutchley, Kylie H. Alm, Brandon S. Katerman, Nicole E. Miller, Joel R. Kuhn, Yuxuan Li, Nicole M. Long, Jonathan Miller, Madison D. Paron, Jesse K. Pazdera, Isaac Pedisich, and Christoph T. Weidemann. Penn electrophysiology of encoding and retrieval study (PEERS). Dataset, 2023. URL https://doi.org/10.18112/openneuro.ds004395.v2.0.0.

Jared Kaplan, Sam McCandlish, Tom Henighan, Tom B Brown, Benjamin Chess, Rewon Child, Scott Gray, Alec Radford, Jeffrey Wu, and Dario Amodei. Scaling laws for neural language models. arXiv preprint arXiv:2001.08361, 2020.

Demetres Kostas, Stephane Aroca-Ouellette, and Frank Rudzicz. Bendr: Using transformers and a contrastive self-supervised learning task to learn from massive amounts of eeg data. Frontiers in Human Neuroscience, 15:653659, 2021.

Harlin Lee, Boyue Li, Shelly DeForte, Mark L Splaingard, Yungui Huang, Yuejie Chi, and Simon L Linwood. A large collection of real-world pediatric sleep studies. Scientific Data, 9(1):421, 2022.

Steven J. Luck. An Introduction to the Event-Related Potential Technique. MIT Press, 2 edition, 2014. URL https://mitpress.mit.edu/9780262525855/an-introduction-to-the-event-related-potential-technique/.

Leland McInnes, John Healy, and James Melville. Umap: Uniform manifold approximation and projection for dimension reduction. arXiv preprint arXiv:1802.03426, 2018.

Nima Mesgarani, Connie Cheung, Keith Johnson, and Edward F Chang. Phonetic feature encoding in human superior temporal gyrus. Science, 2014.

Niklas Muennighoff, Alexander Rush, Boaz Barak, Teven Le Scao, Nouamane Tazi, Aleksandra Piktus, Sampo Pyysalo, Thomas Wolf, and Colin A Raffel. Scaling data-constrained language models. Advances in Neural Information Processing Systems, 36:50358–50376, 2023.

Wajid Mumtaz. MDD patients and healthy controls EEG data (new). Dataset, 2016. URL https://doi.org/10.6084/m9.figshare.4244171.v2.

Iyad Obeid and Joseph Picone. The temple university hospital eeg data corpus. Frontiers in neuroscience, 10:196, 2016.

Steven M Peterson, Satpreet H Singh, Benjamin Dichter, Michael Scheid, Rajesh PN Rao, and Bingni W Brunton. Ajile12: Long-term naturalistic human intracranial neural recordings and pose. Scientific data, 9(1):184, 2022.

Alec Radford, Jong Wook Kim, Chris Hallacy, Aditya Ramesh, Gabriel Goh, Sandhini Agarwal, Girish Sastry, Amanda Askell, Pamela Mishkin, Jack Clark, et al. Learning transferable visual models from natural language supervision. In International conference on machine learning, pp. 8748–8763. PmLR, 2021.

---

Jeff Rasley, Samyam Rajbhandari, Olatunji Ruwase, and Yuxiong He. Deepspeed: System optimizations enable training deep learning models with over 100 billion parameters. In Proceedings of the 26th ACM SIGKDD international conference on knowledge discovery & data mining, pp. 3505–3506, 2020.
- Schalk et al. (2019) Josef P Rauschecker and Sophie K Scott. Maps and streams in the auditory cortex: nonhuman primates illuminate human speech processing. Nature neuroscience, 12(6):718–724, 2009.
- Schalk et al. (2022) Gerwin Schalk, Dennis J McFarland, Thilo Hinterberger, Niels Birbaumer, and Jonathan R Wolpaw. Bci2000: a general-purpose brain-computer interface (bci) system. IEEE Transactions on biomedical engineering, 51(6):1034–1043, 2004.
- Sharma and Kaplan (2024) Utkarsh Sharma and Jared Kaplan. Scaling laws from the data manifold dimension. Journal of Machine Learning Research, 23(9):1–34, 2022. URL http://jmlr.org/papers/v23/20-1111.html.
- Shirazi et al. (2024) Seyed Yahya Shirazi, Alexandre Franco, Maurício Scopel Hoffmann, Nathalia B Esper, Dung Truong, Arnaud Delorme, Michael P Milham, and Scott Makeig. Hbn-eeg: The fair implementation of the healthy brain network (hbn) electroencephalography dataset. bioRxiv, pp. 2024–10, 2024.
- Su et al. (2023) Jianlin Su, Murtadha Ahmed, Yu Lu, Shengfeng Pan, Wen Bo, and Yunfeng Liu. Roformer: Enhanced transformer with rotary position embedding. Neurocomputing, 568:127063, 2024.
- Wang et al. (2023) William O. Tatum, Jayanti Mani, Kazutaka Jin, Jonathan J. Halford, David Gloss, Firas Fahoum, Louis Maillard, Ian Mothersill, and Sandor Beniczky. Minimum standards for inpatient long-term video-​eeg monitoring: A clinical practice guideline of the international league against epilepsy and international federation of clinical neurophysiology. Clinical Neurophysiology, 134:111–128, 2022. doi: 10.1016/j.clinph.2021.07.016. URL https://www.sciencedirect.com/science/article/pii/S1388245721006672.
- Wang et al. (2024) Christopher Wang, Vighnesh Subramaniam, Adam Uri Yaari, Gabriel Kreiman, Boris Katz, Ignacio Cases, and Andrei Barbu. Brainbert: Self-supervised representation learning for intracranial recordings. arXiv preprint arXiv:2302.14367, 2023.
- Wang et al. (2024a) Christopher Wang, Adam Yaari, Aaditya Singh, Vighnesh Subramaniam, Dana Rosenfarb, Jan DeWitt, Pranav Misra, Joseph Madsen, Scellig Stone, Gabriel Kreiman, et al. Brain treebank: Large-scale intracranial recordings from naturalistic language stimuli. Advances in Neural Information Processing Systems, 37:96505–96540, 2024a.
- Wang et al. (2024b) Guangyu Wang, Wenchao Liu, Yuhong He, Cong Xu, Lin Ma, and Haifeng Li. Eegpt: Pre-trained transformer for universal and reliable representation of eeg signals. Advances in Neural Information Processing Systems, 37:39249–39280, 2024b.
- Wang et al. (2024c) Jiquan Wang, Sha Zhao, Zhiling Luo, Yangxuan Zhou, Haiteng Jiang, Shijian Li, Tao Li, and Gang Pan. Cbramod: A criss-cross brain foundation model for eeg decoding. arXiv preprint arXiv:2412.07236, 2024c.
- Wang et al. (2025) Xujia Wang, Xuhui Liu, Xi Liu, Qian Si, Zhaoliang Xu, Yang Li, and Xiantong Zhen. Eeg-dino: Learning eeg foundation models via hierarchical self-distillation. In International Conference on Medical Image Computing and Computer-Assisted Intervention, pp. 196–205. Springer, 2025.
- R. Wolpaw, Niels Birbaumer, Dennis J. McFarland, Gert Pfurtscheller, and Theresa M. Vaughan. Brain–computer interfaces for communication and control. Clinical Neurophysiology, 113(6):767–791, 2002. doi: 10.1016/S1388-2457(02)00057-3. URL https://www.sciencedirect.com/science/article/pii/S1388245702000573.
- Woo et al. (2024) Gerald Woo, Chenghao Liu, Akshat Kumar, Caiming Xiong, Silvio Savarese, and Doyen Sahoo. Unified training of universal time series forecasting transformers. International Conference on Machine Learning, 2024.
- Yang et al. (2023) Chaoqi Yang, M Westover, and Jimeng Sun. Biot: Biosignal transformer for cross-data learning in the wild. Advances in Neural Information Processing Systems, 36:78240–78260, 2023.

---

Greg Yang, Edward J Hu, Igor Babuschkin, Szymon Sidor, Xiaodong Liu, David Farhi, Nick Ryder, Jakub Pachocki, Weizhu Chen, and Jianfeng Gao. Tensor programs v: Tuning large neural networks via zero-shot hyperparameter transfer. arXiv preprint arXiv:2203.03466, 2022.
- Andrii Zahorodnii, Bennett Stankovits, Christopher Wang, Charikleia Moraitaki, Geeling Chau, Ila R Fiete, Boris Katz, and Andrei Barbu. Neuroprobe: Evaluating intracranial brain responses to naturalistic stimuli, 2025. URL TBD.
- Daoze Zhang, Zhizhang Yuan, Yang Yang, Junru Chen, Jingjing Wang, and Yafeng Li. Brant: Foundation model for intracranial neural signal. Advances in Neural Information Processing Systems, 36:26304–26321, 2023.
- Igor Zyma, Sergii Tukaev, Ivan Seleznov, Ken Kiyono, Anton Popov, Mariia Chernykh, and Oleksii Shpenkov. Electroencephalograms during mental arithmetic task performance. Data, 4(1):14, 2019.

---

APPENDIX TABLE OF CONTENTS

A Related Works 17
A.1 Ephys Data Foundation Models 17
A.2 Neural Scaling Law 17

B Experimental Setup Details 18
B.1 Tested Models 18
B.2 Pretraining Dataset. 18
B.3 Downstream Task and Dataset Overview. 19
B.4 Pretraining Setup and Model Scaling 19
B.5 DIVER Architecture and Pretext Task Hyperparameter Setting 20
B.6 Pretraining Hyperparameter Search using $\mu$-Parameterization ($\mu$P) and $\mu$Transfer 20
B.7 $\mu$-parameterization ($\mu P$) 22
B.8 Finetuning Setup 23

C Scaling Law 23
C.1 Scaling Law Experiment Details. 23
C.2 Extended Kaplan (Kaplan et al., 2020) Scaling Law Results for iEEG 26
C.3 Data-Constrained Scaling Law Fitting Results for iEEG. 26
C.4 Extended Kaplan (Kaplan et al., 2020) Scaling Law Results for EEG 30
C.5 Data-Constrained Scaling Law Fitting Results for EEG 30
C.6 Extended EEG Downstream Scaling Results 33

D Extended Results 36
D.1 Comprehensive DIVER Downstream Task Results 36
D.2 Performance Evaluation across DIVER-1 Model configurations 37
D.3 Ablations 38
D.4 Analysis of Joint Modality (intracranial/scalp-EEG) Pretraining 41
D.5 Interpretation Results 43

E Exploration of Finetuning Method 45
E.1 Overview: Impact of Finetuning Methodology on EEG Downstream Task Performance 45
E.2 Impact of MLP Classifier Depth on DIVER Performance 45
E.3 Challenges in Reproducing C BraMod Baseline Performance 45
E.4 Task-Specific Optimal Finetuning Configurations for C BraMod and DIVER. 45
E.5 Linear Probing Analysis: Evidence of High-Quality Learned Representations 47

F Data Details 48
F.1 Pretraining Dataset Description 48
F.2 Finetuning Dataset Description 49
F.3 QAQC and preprocessing 50

G Comparison With Existing EEG/iEEG Foundation Models 51

---

A Related Works

### A.1 Ephys Data Foundation Models

Ephys decoding has progressed from pipelines that coupled hand-crafted features with classical classifiers to end-to-end deep architectures that learn task-relevant representations directly from raw signals. Early EEG studies relied on feature engineering (e.g., band-power, CSP) paired with SVMs or LDA; subsequent work introduced convolutional backbones and sequence models that absorb spectral–temporal patterns with minimal preprocessing. Building on advances in self-supervised learning (SSL) and “foundation” paradigms, recent efforts pretrain large models on heterogeneous, weakly labeled or unlabeled EEG/iEEG corpora and adapt them to diverse downstream tasks (e.g., event detection, cognitive state decoding, BCI control). Representative lines include large-scale EEG transformers and montage-aware encoders *(e.g., EEGFormer(Chen et al., 2024)*, NEURO-GPT*(Cui et al., 2024)*, LaBraM*(Jiang et al., 2024)*), intracranial representation learners *(e.g., BrainBERT(Wang et al., 2023)*, foundation models for intracranial neural signals), and broader neuro-sequence backbones emphasizing transfer and robustness *(e.g., CBraMod(Wang et al., 2024c))*.

### A.2 Neural Scaling Law

Kaplan *(Kaplan et al., 2020)* scaling law provides a principled framework for predicting model performance as a function of model size and dataset size for large language models. They demonstrated that language model cross-entropy loss follows smooth power-law relationships with respect to model parameters ($N$) and training data ($D$). Concretely, they proposed a relation of the form

$L(N,D)=\frac{A}{N^{\alpha}}+\frac{B}{D^{\beta}}+E$ (9)

where $A,B,E$ are constants, and $\alpha,\beta>0$ are scaling exponents. This formulation implies that increasing the number of parameters or training data yields a predictable reduction in loss, enabling systematic optimization of compute allocation across model size and training duration.

Data-constrained scaling law. In scientific domains, including Ephys, unique high-quality data are inherently limited. To address this, *Muennighoff et al. (2023)* extended the scaling framework to data-constrained regimes, where models must repeatedly train on the same corpus for multiple epochs. They proposed a modified law

$L(N,D)=\frac{A}{(N^{\prime})^{\alpha}}+\frac{B}{(D^{\prime})^{\beta}}+E$ (10)

where the effective number of parameters $N^{\prime}$ and effective tokens $D^{\prime}$ account for diminishing returns: repeated tokens are progressively less valuable, and excessively large models are less sample-efficient. They further define

$D^{\prime}$ $=U_{D}+U_{D}R_{D}^{*}\Big{(}1 - e^{-\frac{R_{D}}{R_{D}^{*}}}\Big{)}$ (11)
$N^{\prime}$ $=U_{N}+U_{N}R_{N}^{*}\Big{(}1 - e^{-\frac{R_{N}}{R_{N}^{*}}}\Big{)}$ (12)

where $U_{D}$ is the number of unique tokens, $R_{D}$ is the number of repetitions (epochs $-1$), and $R_{D}^{*}$ is a learned constant describing the “half-life” of repeated data. Analogously, $U_{N}$ is the compute-optimal parameter count for $U_{D}$, and $R_{N}^{*}$ governs diminishing returns beyond that point. Empirical results suggest that up to $\sim$4 epochs, repeated data is almost as useful as new data, but returns decrease sharply thereafter.

Compared to the Chinchilla law *(Hoffmann et al., 2022)*, which assumes abundant data and one training epoch, this formulation makes epoch count itself a central axis of scaling. This perspective is crucial for domains constrained by limited samples, such as EEG and iEEG, and it guides how compute should be allocated between model size and additional training passes.

Finally, the data-constrained scaling law also connects scaling analysis to more fundamental theory. Recent work has suggested that the exponents governing power-law scaling, such as $\alpha$ and $\beta$, are intimately connected to the intrinsic dimension of the underlying data manifold *(Sharma and Kaplan,

---

2022)*. In particular, it has been argued that the data exponent $\beta$ can be interpreted in terms of an effective dimension $d$ via an approximate inverse relation of the form:

$\beta\ \approx\ \frac{2}{d}.$ (13)

From this view, estimating $\beta$ provides not only a measure of how data volume translates into performance but also an insight into the intrinsic dimensionality of Ephys signals, where scarcity and structural complexity are defining features.

## Appendix B EXPERIMENTAL SETUP DETAILS

### B.1 Tested Models

We adopt a systematic naming convention for all DIVER model variants: DIVER_{Size/Modality/Granularity}. The Size component indicates model size (Tiny: 256, Small: 512, Base: 768, Large: 1024, XL: 2048, XXL: 3072 hidden dimensions). The Modality specifies input data types (I: iEEG-only, IE: iEEG+EEG). The Granularity indicates temporal resolution (0.1s or 1s window). For example, DIVER_{Base/I/1s} represents a base-sized model trained on iEEG-only data with 1s temporal windows.

Table 2: Model configurations with measured parameters and total FLOPs per epoch.

| Models | # Parameters | Modality | Granularity | Hidden Dimension ($d_{\text{model}}$) | total FLOPs / epoch |
| --- | --- | --- | --- | --- | --- |
| DIVER_{Tiny/I/0.1s} | 12.72M | iEEG | 0.1s | 256 | 76.34P |
| DIVER_{Small/I/0.1s} | 50.75M | iEEG | 0.1s | 512 | 253.96P |
| DIVER_{Base/I/0.1s} | 114.07M | iEEG | 0.1s | 768 | 532.77P |
| DIVER_{Large/I/0.1s} | 202.70M | iEEG | 0.1s | 1024 | 912.83P |
| DIVER_{XL/I/0.1s} | 810.19M | iEEG | 0.1s | 2048 | 3.40E |
| DIVER_{XXL/I/0.1s} | 1.82B | iEEG | 0.1s | 3072 | 7.50E |
| DIVER_{Tiny/I/1s} | 13.03M | iEEG | 1s | 256 | 77.52P |
| DIVER_{Small/I/1s} | 51.36M | iEEG | 1s | 512 | 256.44P |
| DIVER_{Base/I/1s} | 115.00M | iEEG | 1s | 768 | 536.82P |
| DIVER_{Large/I/1s} | 203.95M | iEEG | 1s | 1024 | 918.56P |
| DIVER_{XL/I/1s} | 812.85M | iEEG | 1s | 2048 | 3.46E |
| DIVER_{XXL/I/1s} | 1.83B | iEEG | 1s | 3072 | 7.64E |
| DIVER_{Tiny/E/1s} | 13.03M | EEG | 1s | 256 | 238.83P |
| DIVER_{Small/E/1s} | 51.36M | EEG | 1s | 512 | 790.01P |
| DIVER_{Base/E/1s} | 115.00M | EEG | 1s | 768 | 1.65E |
| DIVER_{Large/E/1s} | 203.95M | EEG | 1s | 1024 | 2.83E |
| DIVER_{XL/E/1s} | 812.85M | EEG | 1s | 2048 | 10.65E |
| DIVER_{Tiny/IE/1s} | 13.03M | iEEG+EEG | 1s | 256 | 316.35P |
| DIVER_{Small/IE/1s} | 51.36M | iEEG+EEG | 1s | 512 | 1.05E |
| DIVER_{Large/IE/1s} | 203.95M | iEEG+EEG | 1s | 1024 | 2.19E |
| DIVER_{XL/IE/1s} | 812.85M | iEEG+EEG | 1s | 2048 | 3.75E |

### B.2 Pretraining Dataset

DIVER-1 was pretrained on the largest and most diverse Ephys corpus to date, with DIVER_{-/I/-} trained on 352k channel-hours from 37 subjects using iEEG data (ECoG/sEEG), DIVER_{-/IE/-} trained on 1.66M channel-hours from 17,718 subjects combining both iEEG and EEG modalities across multiple datasets. Pretraining dataset description is given in Table 3.

---

Table 3: Summary of DIVER-1 pretraining datasets. The datasets are categorized by modality: iEEG (including ECoG and sEEG) and EEG.  $\mathrm{DIVER_I}$  was pretrained on iEEG,  $\mathrm{DIVER_E}$  on EEG, and  $\mathrm{DIVER_{IE}}$  utilized both. Note that for the self-collected iEEG dataset in  $\mathrm{DIVER_{IE}}$ , we applied stricter QAQC criteria (3.33% threshold) compared to  $\mathrm{DIVER_I}$  (50% threshold) for consistency with EEG criteria.

| Datasets | Data Type | # Subj. | Volume (channel-hours) | Duration (hours) | Sampling Rate (Hz) |
| --- | --- | --- | --- | --- | --- |
| iEEG (Used in DIVERI & DIVERIE) |  |  |  |  |  |
| AJILE12 (Peterson et al., 2022) | ECoG | 12 | 124,423 | 1,282 | 1,000 |
| Self-collected iEEG (DIVERI) | ECoG/sEEG | 25 | 227,612 | 4,028 | 2,000 |
| Self-collected iEEG (DIVERIE) | ECoG/sEEG | 25 | 144,634 | 2,844 | 2,000 |
| EEG (Used in DIVERE & DIVERIE) |  |  |  |  |  |
| TUEG (Obeid & Picone, 2016) | EEG | 10,874 | 422,036 | 23,178 | 250–512 |
| HBN (Shirazi et al., 2024) | EEG | 2,782 | 61,703 | 572 | 500 |
| NCHSDB (Lee et al., 2022) | EEG | 3,673 | 163,146 | 26,055 | 256–512 |
| PEERS (Kahana et al., 2023) | EEG | 364 | 870,447 | 6,964 | 500 |
| Total (DIVERI) | iEEG | 37 | 352,035 | 5,310 | — |
| Total (DIVERE) | EEG | 17,693 | 1,517,332 | 56,769 | — |
| Total (DIVERIE) | iEEG + EEG | 17,718 | 1,661,966 | 59,613 | — |

# B.3 DOWNSTREAM TASK AND DATASET OVERVIEW

Table 4 provides a comprehensive overview of all downstream tasks and datasets used in our evaluation. Our evaluation spans two modalities (iEEG and EEG) and covers diverse neural decoding objectives across visual, auditory, and language domains.

iEEG tasks. We evaluated on 15 tasks from the Neuroprobe (LITE) benchmark (Zahorodnii et al., 2025), including visual perception (frame brightness, optical flow, face detection), auditory processing (volume, pitch, delta volume), and language processing (speech decoding, word prediction, onset detection, part-of-speech tagging). The Neuroprobe dataset contains depth electrode recordings from 6 subjects with 109-120 channels per subject, originally sampled at  $2048\mathrm{Hz}$  and was resampled to  $500\mathrm{Hz}$  to match our pretraining configuration. There are both binary-label and multi-label task options for Neuroprobe. In the multi-label configuration, the speech, onset, and head word position tasks remain binary, the part-of-speech task uses 6 labels, and the remaining tasks use 3 labels. Throughout this paper, unless explicitly stated otherwise as multi-label, all reported Neuroprobe results correspond to the binary-label setting. Also, we evaluated on the seizure detection test on MAYO dataset (modified the dataset in kaggle challenge (Bbrinkm &amp; Cukierski, 2014)). The original dataset consists of 1 s samples, but to match the minimum patch length of Brant, one of the baseline models, we concatenated samples in temporal order to create 6 s samples. We evaluated the model separately for each of the 8 participants. To address the issue of having more test data than training data, we swapped the train and test sets for each participant.

EEG tasks. We evaluated on three EEG benchmarks: FACED (emotion recognition from 32-channel EEG, 9-class classification, 123 subjects)(Chen et al., 2023), PhysioNet-MI (motor imagery with 64 channels, 4-class classification, 109 subjects)(Goldberger et al., 2000), and MentalArithmetic (mental stress detection with 20 channels reduced to 19, 2-class classification, 36 subjects)(Zyma et al., 2019). Sampling rates were standardized to  $500\mathrm{Hz}$  across all datasets to ensure consistency with our pretraining setup.

# B.4 PRETRAINING SETUP AND MODEL SCALING

Training experiments were conducted across two high-performance computing configurations. The primary server consisted of nodes each equipped with a single 2.8 GHz AMD EPYC Milan 7543P 32-core CPU and four NVIDIA A100 GPUs, which was more heavily utilized throughout the training process. For large model variants, we additionally employed a secondary server equipped with dual Intel Xeon Platinum 8480+ processors (112 cores total) and eight NVIDIA H200 GPUs with 144GB memory each. Training experiments were conducted using either 128, 32, 8 A100 GPUs or 32, 24, 16 H200 GPUs depending on the experimental configuration. We maintained a fixed global

---

Table 4: Overview of downstream tasks and datasets. Sampling rates were adjusted to  $500\mathrm{Hz}$  across all datasets to match the pretraining configuration. Arrows  $(\rightarrow)$  indicate resampling or channel selection from the original dataset.

| Modality | Task Name | Datasets | Sampling Rate | # Ch. | # Subj. | Label |
| --- | --- | --- | --- | --- | --- | --- |
| iEEG | frame_brightness (visual) |  |  |  |  |  |
|  | global_flow (visual) |  |  |  |  |  |
|  | local_flow (visual) |  |  |  |  |  |
|  | face_num (visual) |  |  |  |  |  |
|  | volume (auditory) |  |  |  |  |  |
|  | pitch (auditory) |  |  |  |  |  |
|  | delta_volume (auditory) |  |  |  |  |  |
|  | speech (language) | Neuroprobe (LITE) | 2048 → 500Hz | Var. (109–120) | 6 | 2-class (2-6 in mulilabel) |
|  | onset (language) |  |  |  |  |  |
|  | gpt2_surprisal (language) |  |  |  |  |  |
|  | word_length (language) |  |  |  |  |  |
|  | word_gap (language) |  |  |  |  |  |
| word_index (language) |  |  |  |  |  |  |
| word_head_pos (language) |  |  |  |  |  |  |
| word_part_speech (language) |  |  |  |  |  |  |
|  | Seizure Detection | MAYO | 5000 → 500Hz | Var.(16–72) | 8 | 2-class |
| EEG | Emotion Recognition | FACED | 250 → 500Hz | 32 | 123 | 9-class |
|  | Motor Imagery | PhysioNet-MI | 160 → 500Hz | 64 | 109 | 4-class |
|  | Mental Stress Detection | MentalArithmetic | 500Hz | 20 → 19 | 36 | 2-class |

batch size of 192 across all training runs, with the per-GPU batch size adjusted dynamically based on the number of nodes employed.

We varied the model size by modifying the hidden dimension of the transformer, resulting in sizes of 13M, 51M, 115M, 203M, 813M, 1.83B parameters, while keeping the depth fixed at 12 layers. This capacity adjustment leverages the benefits of  $\mu$  parameterization for stable training across different model sizes. DIVER-1 was implemented on the Python 3.12.3 and Pytorch 2.6.0 + CUDA version 12.4. To enhance training efficiency, we employed DeepSpeed ZeRO Stage 2, BF16 precision. Optimization was performed using a custom implementation of the DeepSpeed's MuAdam optimizer (Yang et al., 2022) with utilizing DeepSpeed's FusedAdam backend (Rasley et al., 2020) for computational efficiency and learning rate calibration. A cosine annealing learning rate scheduler with warm-up restarts was applied, with cycle length matching the total training steps and minimum learning rate set to  $0.01\times$  the initial rate.

# B.5 DIVER ARCHITECTURE AND PRETEXT TASK HYPERPARAMETER SETTING

Architecture setting Table 5 lists the detailed architectural hyperparameter settings used for DIVER-1 pretraining.

FFT, STFT setting For the FFT, we used a window size of 500 time points with a sampling frequency of  $500\mathrm{Hz}$ . A cutoff frequency of  $200\mathrm{Hz}$  was applied, and the FFT amplitudes were converted to absolute values, normalized, and then compressed using a  $\log (1 + x)$  transform. For the STFT, we employed a multi-resolution approach with window sizes of 200 and 100 time points, respectively. Each window was shifted with  $50\%$  overlap and tapered with a Hann window function. Consistent with the FFT settings, a cutoff frequency of  $200\mathrm{Hz}$  was applied, and the STFT amplitudes were converted to absolute values, normalized, and compressed using the  $\log (1 + x)$  transform.

# B.6 PRETRAINING HYPERPARAMETER SEARCH USING  $\mu$ -PARAMETERIZATION ( $\mu$ P) AND  $\mu$ TRANSFER

We employed a two-stage hyperparameter optimization approach to determine optimal learning rate (lr) and weight decay (wd) values; grid search followed by optuna optimization. The search was conducted using a 50M parameter model, a 12-layer architecture with 512-dimensional attention layers trained for different modalities: iEEG, EEG, and TUEG and iEEG; DIVERSmall/I/1s, DIVERSmall/E/1s, DIVERSmall/IE/1s. All hyperparameter searches were performed over 2 epochs to balance computational efficiency with reliable performance estimation.

---

Table 5: Hyperparameters for DIVER-1 pretraining. Two model variants were trained for inputs with 1s and 0.1s patch size respectively. The 1s and 0.1s models share all settings except for patch size, patchwise CNN embedding settings, and SSL weights. Some hyperparameters are defined as a function of  $d_{\mathrm{model}}$ , which we vary across {256, 512, 768, 1024, 2048, 3072}.

|  | Hyperparameters | Settings |
| --- | --- | --- |
| Input & Masking | Patch size | 500 (1s) |
| 50 (0.1s) |
| Mask ratio | 0.5 |
| Masking type | Patch random |
| Patch Encoder (CNN) | Intermediate channel (Cinter) | dmodel/8 (1s) |
| Input dimension | dmodel/16 (0.1s) |
| Output dimension | {1, Cinter, Cinter} |
| Stride | {Cinter, Cinter, Cinter} |
|  | {64, 3, 3} (1s) |
| Kernel size | {63, 3, 3} |
| Padding | {31, 1, 1} |
| Depth | 3 |
| Patch Encoder (Spectral) | Spectral FFT size | dmodel/2 + 1 |
| Spectral dropout | 0.1 |
| STCPE | STCPE dimension | dmodel/8 |
| STCPE layers | 1 |
| STCPE heads | dmodel/256 |
| STCPE dff | dmodel/2 |
| Time window size | 7 |
| Positional Embedding | Channel type dimension | dmodel/4 |
| Embedding style | CPE (Learnable) |
| Temperature | 2000 |
| Scale | 1/256 |
| Transformer | Model dimension | dmodel |
| Layers | 12 |
| Heads | dmodel/32 |
| Feed-forward dimension | 4 * dmodel |
| Activation | SiLU |
| Attention type | Flash attention |
| Dropout | 0.1 |
| SSL Head | Domain | Time, FFT, STFT |
| Loss weight (λTime) | 1.0 |
| Loss weight (λFFT) | 0.1 (1s) / 1.0 (0.1s) |
| Loss weight (λSTFT) | 1.0 (1s) / 0.0 (0.1s) |
| Training | Parameterization | μP |

Stage1: Grid search We conducted an extensive grid search across learning rate and weight decay combinations, systematically exploring the hyperparameter space.

- a) Initial Learning Rate Exploration (wd=1e-2): Learning rates: 1e-5, 1e-4, 1e-3, 1e-2
- b) Weight Decay Exploration (lr=1e-3): Weight decay values: 1e-7, 1e-6, 1e-5, 1e-4, 1e-3, 1e-2, 1e-1
- c) Refined Learning Rate Search: Based on initial results, we refined the learning rate search between 1e-4 and 1e-2, testing: 2e-4, 3e-4, 5e-4, 8e-4, 2e-3, 3e-3, 5e-3, 6e-3, 8e-3
- e) Cross-combinations: Additional combinations around promising regions, including lr=6e-3 with various weight decay values: 1e-6, 1e-5, 1e-4, 1e-3, 1e-1

---

Table 6: Stage 1: Grid search hyperparameter exploration.

| Search Step | Hyperparameter Values |
| --- | --- |
| Initial Learning Rate Exploration | Learning rate: {1e-5, 1e-4, 1e-3, 1e-2} (wd=1e-2) |
| Weight Decay Exploration | Weight decay: {1e-7, 1e-6, 1e-5, 1e-4, 1e-3, 1e-2, 1e-1} (lr=1e-3) |
| Refined Learning Rate Search | Learning rate: {2e-4, 3e-4, 5e-4, 8e-4, 2e-3, 3e-3, 5e-3, 6e-3, 8e-3} |
| Cross-combinations | lr=6e-3 with wd: {1e-6, 1e-5, 1e-4, 1e-3, 1e-1} |

The grid search evaluated 30 distinct learning rate and weight decay combinations, revealing optimal configurations of  $\mathrm{lr} = 6.0\mathrm{e - }03$  with  $\mathrm{wd} = 1.0\mathrm{e - }06$  for  $\mathrm{DIVER}_{\mathrm{Small / I / 1s}}$  and  $\mathrm{lr} = 1.0\mathrm{e - }03$  with  $\mathrm{wd} = 2.0\mathrm{e - }01$  for  $\mathrm{DIVER}_{\mathrm{Small / IE / 1s}}$  when pretrained on the TUEG dataset (our largest EEG dataset).

For subsequent Optuna optimization of  $\mathrm{DIVER}_{\mathrm{Small} / \mathrm{IE} / 1s}$ , we used the geometric mean between the  $\mathrm{DIVER}_{\mathrm{Small} / \mathrm{I} / 1s}$  Optuna results (lr=2.30e-03, wd=2.17e-07) and the TUEG-pretrained model's grid search results (lr=1.0e-03, wd=2.0e-01) as the starting point, yielding lr=1.51e-03 and wd=2.09e-04.

Stage2: Optuna Optimization We further refined the hyperparameters using Optuna(Akiba et al., 2019) or bayesian hyperparameter optimization. The search space was defined as  $\pm 1$  order of magnitude around the best grid search configurations (range:  $\times 0.1$  to  $\times 10$ ), with 50 trials conducted to systematically explore this refined hyperparameter space. The optimal hyperparameter settings identified through Optuna optimization are presented in Table 7.

Table 7: Optimal learning rate and weight decay by model configuration.

| Models | Modality | Granularity | Learning Rate | Weight Decay |
| --- | --- | --- | --- | --- |
| DIVER$ _{Small/I/1s} $ | iEEG | 1s | 2.30e-03 | 2.17e-07 |
| DIVER$ _{Small/I/0.1s} $ | iEEG | 0.1s | 4.91e-03 | 3.75e-06 |
| DIVER$ _{Small/E/1s} $ | EEG | 1s | 7.70e-03 | 2.14e-07 |
| DIVER$ _{Small/IE/1s} $ | iEEG+TUEG | 1s | 2.61e-03 | 1.36e-03 |

![img-3.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-4.jpg)
B.7  $\mu$ -PARAMETERIZATION  $(\mu P)$
Figure 4: Verification of the  $\mu P$  implementation. The L1 norm of activation vectors (y-axis) is plotted against model width (x-axis) for five training timesteps ( $t = 1$  to  $t = 5$ ) across four different widths (256, 512, 768, 1024). (Top Row) With standard parameterization, activation norms are unstable and diverge as model width increases. (Bottom Row) In contrast, our  $\mu P$  implementation yields stable activation norms that are independent of model width. This confirms the model is correctly parameterized, a critical prerequisite for successful hyperparameter transfer via  $\mu$  Transfer.

The stable initialization shown in the Figure 4 translates directly to stable training dynamics. We confirmed this by tracking the training loss while varying the model width across the same four configurations. With  $\mu P$  enabled, the training loss remained low and stable for all model sizes. In stark contrast, training without  $\mu P$  led to severe instability; the loss diverged rapidly as the model grew, with values exploding to over 100 for the largest width. This empirical result demonstrates that our use of  $\mu P$  was essential for reliably training larger models in our scaling experiments.

---

B.8 Finetuning Setup

For Neuroprobe (iEEG task), DIVER-1 was finetuned at lr = 2e-3 and wd = 1e-2, batch size 32, with AdamW for both frozen and full-finetuning. For the MAYO (iEEG) task, frozen models were finetuned using the same learning rate and weight decay as above, whereas full fine-tuning employed separate hyperparameters for each model size (lr = 1.19e-3, wd = 6.18e-1 for 256; lr = 4.19e-3, wd = 1.45e-2 for 512; lr = 7.14e-4, wd = 2.84e-1 for 768; lr = 1.40e-4, wd = 3.44e-2 for 1024; lr = 8.65e-4, wd = 9.90e-2 for 2048; selected via a learning-rate and weight-decay search based on the validation set of subject 1, fold 1).

Unlike Neuroprobe, for which PopT and BrainBERT baselines are provided as benchmarks *(Zahorodnii et al., 2025)*, the MAYO seizure dataset is an extended dataset that we constructed to match Brant’s minimum input length, and therefore required training on the baseline models.BrainBERT was set at lr = 1e-3 for the classifier with AdamW, as in the original paper *(Wang et al., 2023)*, with batch size 32. The features in time [l-5:l+5] were concatenated along the channel dimension. Brant was set at lr = 1e-4 for the classifier and 1e-7 for encoder layers, with betas=(0.9, 0.999), eps=1e-8, batch size 4 and Adam, same as their publicly released code. We could not evaluate PopT on MAYO because LPI coordinates are not available. Brant was pretrained with a 6 s patch and a total of 15 patches (90 s), so we were therefore unable to evaluate it on the neuroprobe (1 s), and there is a mismatch with the original pretrained context in MAYO (6 s).

All models were trained for 40 epochs with a CosineAnnealing scheduler. The same validation splits were applied to the training set for each model, and we early-stopped if the validation AUROC did not increase for 10 epochs.

For all EEG downstream tasks, we use the same optimizer (AdamW) and learning rate scheduler (cosine annealing) as described in the iEEG finetuning configuration. The base learning rate is set to 2.00e-4, weight decay to 3.00e-1, and batch size to 64. We perform full finetuning without employing multi-lr strategies, applying the same learning rate to both the backbone and classifier. The classifier consists of a 3-layer MLP with ELU activation functions, where the first hidden layer has width $T\times 200$ ($T$ is the sample duration in seconds), the second hidden layer has width 200, and the output layer dimension matches the number of classes. Dropout rate is set to 0.1, label smoothing to 0.1, and gradient clipping value to 1.0. All models are trained for 50 epochs without early stopping. For model selection, we use the epoch that achieves the best validation performance (AUROC for binary classification, F1 score for multi-class classification), which is then evaluated on the test set. All results are reported as mean $\pm$ standard deviation across 5 random seeds (41, 42, 43, 44, 45). For the one-to-one comparison experiments with CBraMod (Table 25), we use task-specific hyperparameters to match CBraMod’s training conditions: on Mumtaz2016*(Mumtaz, 2016)*, linear probing uses learning rate 5.00e-6 and weight decay 6.25e-6, while multi-lr and linear classifier configurations use learning rate 6.25e-5 and weight decay 6.25e-6.

## Appendix C Scaling Law

### C.1 Scaling Law Experiment Details

Pretraining loss curves for the trained models are presented in Figure 5 for the $\textsc{DIVER}_{\cdot/\text{I}/1s}$ model family, Figure 6 for the $\textsc{DIVER}_{\cdot/\text{I}/0.1s}$ model family and Figure 7 for the $\textsc{DIVER}_{\cdot/\text{E}/1s}$ model family. For the iEEG models, we trained separate instances for each epoch to obtain the corresponding loss curves. In contrast, for EEG models, we trained all models with a fixed maximum of 32 epochs and extracted test loss values at the relevant epoch checkpoints for scaling analysis. This difference in training procedure was necessitated by computational constraints, as EEG model training requires substantially longer wall-clock time. Consequently, the iEEG plots display epoch-specific loss curves(5 and 6), while the EEG plot presents all scaling curves within a single figure(Figure 7). Importantly, this methodological difference affects the learning rate schedule: we employed cosine annealing with warmup, where the decay schedule depends on the total number of training epochs. Therefore, extracting the loss at epoch 2 from a model trained for 32 epochs differs from the loss at epoch 2 of a model trained for only 2 epochs, as the learning rate trajectories diverge under these configurations.

---

![img-4.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-5.jpg)
Figure 5: Loss curves of the DIVER $_{/1/1s}$  model family. Test loss across epochs is shown.

![img-5.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-6.jpg)
Figure 6: Loss curves of the DIVER $_{/1/0.1s}$  model family. Test loss across epochs is shown.

---

![img-6.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-7.jpg)
Figure 7: Loss curves of the DIVER $_{-/E/1s}$  model family for each dataset size. Test loss across epochs is shown. Unlike the iEEG experiments, where separate models were trained for each epoch, all EEG models were trained for a fixed 32-epoch schedule. Early-epoch losses were extracted from intermediate checkpoints of these longer runs. Consequently, each dataset size yields five loss curves, one for each model scale trained within the 32-epoch run.

Unique number of tokens First of all, the estimated total number of unique tokens is  $U_{D} =$  number of data sample  $\times$  number of tokens per sample. The number of tokens per sample can be expressed as number of channels  $\times$  number of timestamps  $\times$  proportion of unmasked patches.

For iEEG, the total number of data samples is 636,480. Since we randomly sampled from a 32 channel x 30 timestamp token grid using Beta(3,1) distribution for both axis, we estimate the number of tokens per sample as  $32 \times 30 \times 0.75 \times 0.75 = 540$  tokens. Thus, we get  $U_{D} = 636,480 \times 540$  for iEEG.

In the case of EEG, the approximated total number of data samples is 1,960,800, and the number of tokens per sample is same as iEEG. Therefore, the  $U_{D} = 1,960,800 \times 540$  for EEG.

Compute To investigate compute scaling properties, we conducted systematic pretraining experiments across different epoch counts for the 1-second granularity models. For shorter training regimes (1, 2, 4, and 8 epochs), we pretrained all six model variants:  $\mathrm{DIVER}_{\mathrm{Tiny} / 1 / 1s}$ ,  $\mathrm{DIVER}_{\mathrm{Small} / 1 / 1s}$ ,  $\mathrm{DIVER}_{\mathrm{Base} / 1 / 1s}$ ,  $\mathrm{DIVER}_{\mathrm{Large} / 1 / 1s}$ ,  $\mathrm{DIVER}_{\mathrm{XL} / 1 / 1s}$ , and  $\mathrm{DIVER}_{\mathrm{XXL} / 1 / 1s}$ . For longer training regimes (16, 32, and 64 epochs), computational constraints limited our experiments to the four smaller model variants:  $\mathrm{DIVER}_{\mathrm{Tiny} / 1 / 1s}$ ,  $\mathrm{DIVER}_{\mathrm{Small} / 1 / 1s}$ ,  $\mathrm{DIVER}_{\mathrm{Base} / 1 / 1s}$ , and  $\mathrm{DIVER}_{\mathrm{Large} / 1 / 1s}$ .

For the DIVER $_{-/1/0.1s}$  model family with 0.1-second granularity models, we followed a similar training protocol. We trained six model variant for epochs 2, 8 and five model variants for epochs 32, excluding DIVER $_{\text{Base}/1/0.1s}$  and three model variants for epochs 64, excluding DIVER $_{\text{Base}/1/0.1s}$ , DIVER $_{\text{Large}/1/0.1s}$  and DIVER $_{\text{XXL}/1/0.1s}$ .

For the DIVER $_{-/E/1s}$  model family on EEG data, we adopted a different training approach due to the substantially longer training time required for EEG models. We trained all model variants with a fixed maximum of 32 epochs and extracted test loss values at epochs 2, 4, 8, 16, and 32 for scaling analysis. We conducted experiments on  $10\%$  and  $20\%$  of the EEG dataset. For the  $10\%$  subset, we trained five model variants up to 32 epochs, while for the  $20\%$  subset, computational constraints allowed us to train four variants:  $\mathrm{DIVER}_{\mathrm{Tiny/E/1s}}$ ,  $\mathrm{DIVER}_{\mathrm{Small/E/1s}}$ ,  $\mathrm{DIVER}_{\mathrm{Base/E/1s}}$ ,  $\mathrm{DIVER}_{\mathrm{Large/E/1s}}$ ,  $\mathrm{DIVER}_{\mathrm{XL/E/1s}}$  was trained up to 16 epochs in  $20\%$  data and  $\mathrm{DIVER}_{\mathrm{XXL/E/1s}}$  was trained up to 4 epochs in both  $10\%$  and  $20\%$  dataset setting.

Data Size For iEEG, data size scaling was done in 1, 3, 9, 24, 50, 90,  $100\%$  of data on  $\mathrm{DIVER}_{\mathrm{Small} / 1 / 1s}$  for 2 epochs with hyperparameters fixed as  $lr = 6.0e - 03,wd = 1.0e - 06$ . For EEG, data size scaling was done in 1, 3, 9, 10, 24, 50,  $100\%$  of data on  $\mathrm{DIVER}_{\mathrm{Small} / E / 1s}$  for 2 epochs with hyperparameters fixed as  $lr = 7.70\times 10^{-3},wd = 2.14\times 10^{-7}$ . Number of token  $=$  number of data sample  $\times$  number of tokens per sample, while the total number of data samples was

---

636,480 for iEEG and 1,960,800 for EEG. Number of tokens per sample estimated as 540, given that we randomly sampled from a  $32 \times 30$  token grid using Beta(3,1) distribution. A detailed explanation can be found in the aforementioned Unique number of tokens section.

Model Size We fixed the number of epochs to 2. The models varied by their width, number of layers, and patch size. The detailed experiment conditions are on table 2. We observed that the models with different number of layers or patch size show different scaling behavior, so we fitted them separately.

Number of Subjects Subject scaling experiments were done only for iEEG, with datasets containing 2, 4, 5, 8, 10, 15, 16 subjects respectively, while maintaining a constant dataset size.  $\mathrm{DIVER}_{\mathrm{Small} / 1 / 0.1s}$  trained for 2 epochs, due to compute constraint.

Data-constrained Scaling Law We trained a total of 31 models with varying parameter counts and numbers of training epochs, while keeping the dataset fixed. The hidden dimension was fixed to 12 layers. Since different granularity led to different scaling behavior, we experimented on two granularity conditions and fitted them separately. The empirical isoLoss contours in Figure 3(j) show less smoothness compared to the original scaling law paper(Muennighoff et al., 2023), primarily due to sampling density. While the original study used 93 model configurations with dense sampling across all loss ranges, we evaluated 30 configurations. Despite this visual difference, our empirical isoLoss contours (Figure 3(j) and Figure 8, left panel) align well with the predicted contours (Figure 3(j) and Figure 8, right panel), demonstrating that data-constrained scaling laws generalize to neural data.

# C.2 EXTENDED KAPLAN (KAPLAN ET AL., 2020) SCALING LAW RESULTS FOR IEEG

We tested models at the 1-second and 0.1-second granularity. For 1-second granularity models, all six models listed in Table 2 as  $\mathrm{DIVER}_{-/1/1s}$  were tested for epochs 2, 4, 8. At epochs 16, 32, and 64, evaluation was conducted on the following four models:  $\mathrm{DIVER}_{\mathrm{Tiny}/1/1s}$ ,  $\mathrm{DIVER}_{\mathrm{Small}/1/1s}$ ,  $\mathrm{DIVER}_{\mathrm{Base}/1/1s}$ , and  $\mathrm{DIVER}_{\mathrm{Large}/1/1s}$ . At earlier epochs (2, 4, and 8), the general trend showed decreasing loss as model size increased. However, as observed in  $\mathrm{DIVER}_{\mathrm{XXL}/1/1s}$ , larger models exhibited substantially higher loss when trained with only a few epochs. This confirms what was also suggested by the data-constrained scaling isoplets: training very large models with insufficient updates is ineffective. Another possibility is that the aspect ratio of  $\mathrm{DIVER}_{\mathrm{XXL}/1/1s}$  (256) places it outside the region where loss remains stable. Future work should therefore evaluate larger models within the aspect-ratio regime where stable loss behavior is maintained.

# C.3 DATA-CONSTRAINED SCALING LAW FITTING RESULTS FOR IEEG

Table 8: Fitted data-constrained scaling law parameters for DIVER.  $\frac{1}{1}$  s and DIVER.  $\frac{1}{0.1}$  s model families.

|  | DIVER. /1/1s | DIVER. /1/0.1s |
| --- | --- | --- |
| A | 19.217 | 101.52 |
| B | 57.065 | 1.1550 |
| E | 0.0092 | 0.0030 |
| α | 0.3773 | 0.5248 |
| β | 0.3504 | 0.1246 |
| R*D | 9.5372 | 19.705 |
| R*X | 3.3850 | 0.7191 |
| R2 (linear) | 0.7858 | 0.7575 |
| R2 (log) | 0.8152 | 0.7718 |

Table 8 shows fitted data-constrained scaling law parameters.  $A$  and  $B$  describe the relative influence of parameters and dataset size on loss. In our setting, we obtain larger  $A$  than  $B$  in both granularity, suggesting that model size plays a more critical role than dataset size. In particular, the 0.1s patch model yields a comparatively small value of  $B$  (0.3925), suggesting that variations in dataset size exert only a minor effect on the loss in this setting.

The exponents  $\alpha$  and  $\beta$  govern the marginal benefit of scaling parameters and data, respectively. Our values  $(\alpha = 0.377, \beta = 0.350)$  indicate that increasing model size and adding data yield comparable

---

![img-7.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-8.jpg)
Data-constrained scaling laws efficient frontier Models trained

![img-8.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-9.jpg)
Figure 8: IsoLoss contours for  $\mathbf{DIVER}_{-/1/0.1s}$  model family: (Left) Twenty models with 0.1s patches were trained across varying epochs and parameter counts. Iso-loss contours are obtained by linear interpolation between measured data points. (Right) Corresponding contours predicted by the fitted scaling law. The fading line denotes the minimum-loss configuration for each compute budget.

contributions to overall performance improvements. Compared to prior results in language domain  $(\alpha = 0.348, \beta = 0.366$ ; (Hoffmann et al., 2022)), our fitted exponents show similar values.

Importantly, the characteristic half-lives  $R_{D}^{\star} = 8.9$  and  $R_{N}^{\star} = 3.3$  quantify diminishing returns under repeated data and excessive parameters. The relatively larger  $R_{D}^{\star}$  implies that repeated data remains useful for many epochs before saturation, whereas the smaller  $R_{N}^{\star}$  suggests that the benefit of adding parameters decays more quickly. Together, these results suggest that gains are most effectively pursued by scaling model size while maintaining moderate dataset repetition, rather than prioritizing further data collection.

---

![img-9.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-10.jpg)
Figure 9: Scaling law extended results for the DIVER $_{-1/1s}$  family. Compute scaling and model size scaling plots are given for models trained for 2, 4, 8, 16, 32, and 64 epochs.(a) Compute scaling and (b) model size scaling plots are given for models trained for 2, 8, 32, and 64 epochs. (c) Epoch scaling plot of the models reported in Fig. 3 (d). The same training runs are reused, with losses re-plotted against parameters and dataset size in log-log scale.

---

![img-10.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-11.jpg)

![img-11.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-12.jpg)
Figure 10: Scaling law extended results for the DIVER.  $/1/0.1s$  family. (a) Compute scaling and (b) model size scaling plots are given for models trained for 2, 8, 32, and 64 epochs. (c) Epoch scaling plot of the models reported in Fig. 8. The same training runs are reused, with losses re-plotted against parameters and dataset size in log-log scale.

![img-12.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-13.jpg)

---

# C.4 EXTENDED KAPLAN (KAPLAN ET AL., 2020) SCALING LAW RESULTS FOR EEG

We tested DIVER. $_{/E/1s}$  model family trained on  $10\%$  and  $20\%$  of the EEG dataset. Use of partial dataset was due to computational constraints. Overall, the scaling behavior across compute and model size demonstrates reasonable fit to the power law. However, notable deviations were observed for the  $10\%$  data subset at epochs 16 and 32, where the power law fit was inadequate. This is primarily attributable to instabilities in  $\mathrm{DIVER}_{\mathrm{XL/E/1s}}$ , whose loss curve exhibits sudden upward spikes and irregular behavior (Figure 7). Furthermore, when trained for shorter durations, larger models exhibit overfitting tendencies; consequently, fitting the power law across all model sizes fails to capture the expected scaling behavior in these regimes. For cases where the fitted slope approached zero, we omit the fitted line from the visualization. Additionally, it is important to note that the suboptimal learning rate schedule—arising from our use of a single training instance with fixed maximum epoch as 32 for EEG models—may contribute to these deviations from ideal scaling behavior.

# C.5 DATA-CONSTRAINED SCALING LAW FITTING RESULTS FOR EEG

We included models trained on  $10\%$  and  $20\%$  of the full dataset, as in the Kaplan scaling law experiment setup in C.4.

Table 9: Fitted data-constrained scaling law parameters for DIVER.  ${}_{/E/{1s}}$  model family.

|  | DIVER. /E/1s |
| --- | --- |
| A | 0.5983 |
| B | 2.0633 |
| E | 0.0004 |
| α | 3.4480 |
| β | 0.2059 |
| RD | 23.860 |
| RN | 3.2903 |
| R2 (linear) | 0.5019 |
| R2 (log) | 0.6012 |

The most notable difference in the EEG scaling results appears in the model-size exponent. For EEG, we obtain an unusually large  $\alpha = 3.29$ , whereas the iEEG experiments produced a much smaller and value of  $\alpha = 0.3773$ . Such a steep exponent suggests that, within the range of model sizes we explored, performance changed very little with additional capacity. A plausible explanation is the behavior of the XXL model: its loss is higher than that of the smaller models, probably due to overfitting. Similar behavior has been reported in very large models trained on fixed data in the Data-constrained scaling law literature(Muennighoff et al., 2023). In addition, we observed that losses often rise around epochs 4-8; because our analysis used the midpoint checkpoint of the 32-epoch runs, this choice may also have distorted the fit.

This instability is also reflected in the overall goodness-of-fit. The EEG scaling law yields an  $R^{2}$  of 0.5019, substantially lower than the 0.8152 observed for iEEG, indicating that EEG does not follow the expected power-law pattern nearly as well. Some of this gap may arise from fundamental differences between EEG and iEEG: EEG has lower signal quality and greater trial-to-trial variability, which can obscure systematic trends. At the same time, aspects of our experimental design may also have contributed. In particular, training all models for a fixed 32 epochs and sampling intermediate losses, rather than evaluating models at comparable levels of convergence, may have introduced additional noise into the fit.

This interpretation is reinforced by the estimate of the irreducible-loss term  $E$ , which drops to an unusually small value ( $E = 0.0004$ ) for EEG, far below the iEEG estimate of  $E = 0.0092$ . Such a low value is difficult to justify on theoretical grounds and likely reflects a compensatory effect of the fitting procedure rather than a meaningful property of the data. Even so, the EEG models follow the general direction of the expected scaling behavior, albeit in a much noisier and less stable form than iEEG.

---

![img-13.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-14.jpg)
10% Data

![img-14.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-15.jpg)
Figure 11: Scaling law extended results for the DIVER $_{-/E/1+}$  family on  $10\%$  of EEG dataset. (a) Compute scaling and (b) model size scaling plots are given for test loss values extracted at epochs 2, 4, 8, 16, and 32 from models trained with a maximum of 32 epochs. For epochs 16 and 32, the fitted slope was effectively zero, so the corresponding fitted lines were omitted from the visualization. (c) Epoch scaling plot of the models in log-log scale.

![img-15.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-16.jpg)

---

![img-16.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-17.jpg)

![img-17.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-18.jpg)
Figure 12: Scaling law extended results for the DIVER $_{-/E/1s}$  family on  $20\%$  of EEG dataset. (a) Compute scaling and (b) model size scaling plots are given for test loss values extracted at epochs 2, 4, 8, 16, and 32 from models trained with a maximum of 32 epochs. (c) Epoch scaling plot of the models reported in reported in Fig. 3(h). The same training runs are reused, with losses re-plotted against parameters and dataset size in log-log scale.

---

C.6 Extended EEG Downstream Scaling Results

Data size scaling (Table 10). We evaluate how pretraining data size affects downstream performance by training $\text{DIVER}_{\text{Small}/E/1s}$ with $d_{\text{model}}=512$ for 2 epochs on varying fractions of the EEG pretraining dataset (1%, 3%, 9%, 24%, 50%, and 100%). Performance generally improves as more pretraining data is used for FACED dataset. While the performance peaked at 24% of the pretraining dataset for PhysioNet-MI, this difference is not significant when considering the standard deviation; performance at 100% is comparable. Overall, larger pretraining datasets lead to better downstream task performance. The improvements are most pronounced when scaling from small fractions (1-10%) to larger portions of the dataset, with diminishing but still positive returns at the largest scales.

Model size scaling (Table 11). We examine the effect of model capacity by evaluating the $\text{DIVER}_{-/E/1s}$ model family with varying hidden dimensions: $d_{\text{model}}\in\{256,512,768,1024,2048\}$ (corresponding to 12M, 48M, 114M, 204M, and 813M parameters respectively). All models were pretrained for 2 epochs on the full EEG dataset. Performance generally improves with model size, though not always monotonically. The $\text{DIVER}_{XL/E/1s}(d_{model}=2048)$ achieves the best performance for PhysioNet-MI dataset while $\text{DIVER}_{Small/E/1s}$ ($d_{model}=512$) achieved best performance for FACED dataset. This could be possible due to the limited number of epochs used to pretrain the model, but further work is needed to clarify this.

Epoch scaling (Table 12). We investigate how pretraining epochs affects downstream performance by training models across different sizes ($d_{\text{model}}\in\{256,512,768,1024,2048\}$) for varying numbers of epochs (2, 4, 8, 16, 32). All models were pretrained on 10% of the EEG dataset due to computational constraints. Performance generally improves with more training epochs, though the optimal number of epochs varies by model size. Larger models tend to benefit more from extended training, while smaller models may plateau earlier. These results demonstrate that both model size and training duration are important factors in achieving optimal downstream performance.

Together, these scaling experiments demonstrate that EEG foundation model performance improves predictably across multiple dimensions—data size, model size, and training duration—providing practical guidance for efficient model development.

---

Table 10: Data size scaling on EEG downstream tasks. DIVER $_{Small/E/1s}$  with  $d_{\mathrm{model}} = 512$  was trained for 2 epochs on a different fraction (1%, 3%, 9%, ..., 100%) of the EEG pretraining dataset.

| Pretraining Fraction | FACED |  |  | PhysioNet-MI |  |  |
| --- | --- | --- | --- | --- | --- | --- |
|  | ACC | kappa | F1 | ACC | kappa | F1 |
| 1% | 0.111 ± 0.000 | 0.000 ± 0.000 | 0.036 ± 0.000 | 0.581 ± 0.007 | 0.441 ± 0.009 | 0.582 ± 0.006 |
| 3% | 0.467 ± 0.012 | 0.400 ± 0.013 | 0.474 ± 0.012 | 0.624 ± 0.005 | 0.498 ± 0.007 | 0.626 ± 0.005 |
| 9% | 0.451 ± 0.017 | 0.380 ± 0.020 | 0.456 ± 0.017 | 0.600 ± 0.005 | 0.467 ± 0.007 | 0.601 ± 0.005 |
| 10% | 0.509 ± 0.013 | 0.448 ± 0.014 | 0.520 ± 0.012 | 0.640 ± 0.006 | 0.519 ± 0.009 | 0.641 ± 0.006 |
| 24% | 0.525 ± 0.007 | 0.464 ± 0.008 | 0.529 ± 0.006 | 0.650 ± 0.004 | 0.533 ± 0.005 | 0.651 ± 0.004 |
| 50% | 0.493 ± 0.007 | 0.426 ± 0.007 | 0.491 ± 0.006 | 0.628 ± 0.006 | 0.504 ± 0.008 | 0.628 ± 0.006 |
| 100% | 0.568 ± 0.011 | 0.513 ± 0.013 | 0.579 ± 0.009 | 0.647 ± 0.006 | 0.529 ± 0.008 | 0.649 ± 0.006 |
| Pretraining Fraction | MentalArithmetic |  |  |
| --- | --- | --- | --- |
|  | ACC | AUC-PR | AUROC |
| 1% | 0.500 ± 0.000 | 0.625 ± 0.000 | 0.500 ± 0.000 |
| 3% | 0.597 ± 0.090 | 0.350 ± 0.053 | 0.611 ± 0.069 |
| 9% | 0.626 ± 0.058 | 0.520 ± 0.087 | 0.690 ± 0.065 |
| 10% | 0.635 ± 0.041 | 0.547 ± 0.045 | 0.765 ± 0.020 |
| 24% | 0.617 ± 0.067 | 0.370 ± 0.054 | 0.701 ± 0.033 |
| 50% | 0.572 ± 0.088 | 0.563 ± 0.234 | 0.752 ± 0.115 |
| 100% | 0.619 ± 0.046 | 0.490 ± 0.069 | 0.765 ± 0.049 |

Table 11: Model size scaling on EEG downstream tasks. DIVER $_{- / E / 1s}$  model family across different model sizes were evaluated. All models were pretrained for 2 epochs using the EEG dataset.

| dmodel (Params) | FACED |  |  | PhysioNet-MI |  |  |
| --- | --- | --- | --- | --- | --- | --- |
|  | ACC | kappa | F1 | ACC | kappa | F1 |
| 256 (13M) | 0.488 ± 0.006 | 0.421 ± 0.006 | 0.485 ± 0.005 | 0.630 ± 0.006 | 0.506 ± 0.008 | 0.631 ± 0.007 |
| 512 (51M) | 0.568 ± 0.011 | 0.513 ± 0.013 | 0.579 ± 0.009 | 0.647 ± 0.006 | 0.529 ± 0.008 | 0.649 ± 0.006 |
| 768 (114M) | 0.477 ± 0.006 | 0.411 ± 0.006 | 0.477 ± 0.006 | 0.659 ± 0.005 | 0.546 ± 0.007 | 0.660 ± 0.005 |
| 1024 (204M) | 0.524 ± 0.005 | 0.462 ± 0.005 | 0.523 ± 0.005 | 0.691 ± 0.006 | 0.588 ± 0.008 | 0.692 ± 0.006 |
| 2048 (813M) | 0.525 ± 0.012 | 0.462 ± 0.012 | 0.524 ± 0.010 | 0.669 ± 0.011 | 0.560 ± 0.014 | 0.672 ± 0.010 |
| dmodel (Params) | MentalArithmetic |  |  |
| --- | --- | --- | --- |
|  | ACC | AUC-PR | AUROC |
| 256 (13M) | 0.626 ± 0.032 | 0.480 ± 0.072 | 0.751 ± 0.036 |
| 512 (51M) | 0.619 ± 0.046 | 0.490 ± 0.069 | 0.765 ± 0.049 |
| 768 (114M) | 0.697 ± 0.012 | 0.631 ± 0.045 | 0.800 ± 0.029 |
| 1024 (204M) | 0.722 ± 0.028 | 0.657 ± 0.063 | 0.806 ± 0.033 |
| 2048 (813M) | 0.674 ± 0.031 | 0.601 ± 0.053 | 0.780 ± 0.031 |

---

Table 12: Epoch scaling on EEG downstream tasks. We evaluate the DIVER  $- / E / 1s$  model family across different model sizes, each pretrained for varying numbers of epochs. All models were pretrained using  $10\%$  of the EEG dataset.

| dmodel | Epochs | FACED |  |  | PhysioNet-MI |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- |
|  |  | ACC | kappa | F1 | ACC | kappa | F1 |
| 256 | 2 | 0.153 ± 0.007 | 0.050 ± 0.007 | 0.103 ± 0.015 | 0.580 ± 0.006 | 0.440 ± 0.007 | 0.582 ± 0.006 |
|  | 4 | 0.463 ± 0.013 | 0.392 ± 0.015 | 0.461 ± 0.014 | 0.604 ± 0.008 | 0.472 ± 0.011 | 0.605 ± 0.008 |
|  | 8 | 0.484 ± 0.005 | 0.417 ± 0.006 | 0.484 ± 0.006 | 0.614 ± 0.003 | 0.485 ± 0.004 | 0.614 ± 0.003 |
|  | 16 | 0.447 ± 0.003 | 0.375 ± 0.003 | 0.443 ± 0.002 | 0.609 ± 0.004 | 0.479 ± 0.005 | 0.610 ± 0.004 |
|  | 32 | 0.488 ± 0.006 | 0.421 ± 0.006 | 0.485 ± 0.005 | 0.615 ± 0.003 | 0.487 ± 0.005 | 0.615 ± 0.004 |
| 512 | 2 | 0.510 ± 0.012 | 0.448 ± 0.013 | 0.517 ± 0.012 | 0.624 ± 0.005 | 0.498 ± 0.007 | 0.625 ± 0.005 |
|  | 4 | 0.539 ± 0.012 | 0.479 ± 0.013 | 0.543 ± 0.010 | 0.654 ± 0.005 | 0.538 ± 0.007 | 0.655 ± 0.005 |
|  | 8 | 0.445 ± 0.008 | 0.373 ± 0.008 | 0.444 ± 0.008 | 0.619 ± 0.004 | 0.491 ± 0.005 | 0.619 ± 0.004 |
|  | 16 | 0.476 ± 0.004 | 0.410 ± 0.004 | 0.477 ± 0.004 | 0.668 ± 0.002 | 0.557 ± 0.003 | 0.669 ± 0.002 |
|  | 32 | 0.493 ± 0.005 | 0.429 ± 0.005 | 0.495 ± 0.005 | 0.680 ± 0.004 | 0.573 ± 0.006 | 0.681 ± 0.004 |
| 768 | 2 | 0.387 ± 0.024 | 0.309 ± 0.027 | 0.386 ± 0.025 | 0.605 ± 0.004 | 0.473 ± 0.005 | 0.606 ± 0.003 |
|  | 4 | 0.511 ± 0.009 | 0.448 ± 0.010 | 0.516 ± 0.010 | 0.636 ± 0.005 | 0.515 ± 0.006 | 0.638 ± 0.005 |
|  | 8 | 0.531 ± 0.004 | 0.470 ± 0.005 | 0.534 ± 0.005 | 0.663 ± 0.004 | 0.550 ± 0.006 | 0.664 ± 0.004 |
|  | 16 | 0.519 ± 0.011 | 0.458 ± 0.012 | 0.518 ± 0.012 | 0.682 ± 0.004 | 0.576 ± 0.005 | 0.683 ± 0.004 |
|  | 32 | 0.526 ± 0.005 | 0.467 ± 0.006 | 0.527 ± 0.005 | 0.690 ± 0.002 | 0.587 ± 0.002 | 0.691 ± 0.002 |
| 1024 | 2 | 0.510 ± 0.010 | 0.449 ± 0.010 | 0.518 ± 0.008 | 0.638 ± 0.005 | 0.518 ± 0.007 | 0.640 ± 0.005 |
|  | 4 | 0.544 ± 0.011 | 0.486 ± 0.013 | 0.554 ± 0.010 | 0.656 ± 0.004 | 0.542 ± 0.005 | 0.658 ± 0.004 |
|  | 8 | 0.462 ± 0.012 | 0.393 ± 0.013 | 0.464 ± 0.012 | 0.591 ± 0.006 | 0.454 ± 0.008 | 0.592 ± 0.007 |
|  | 16 | 0.461 ± 0.007 | 0.390 ± 0.008 | 0.458 ± 0.007 | 0.630 ± 0.008 | 0.507 ± 0.011 | 0.632 ± 0.008 |
|  | 32 | 0.451 ± 0.030 | 0.380 ± 0.033 | 0.449 ± 0.030 | 0.644 ± 0.016 | 0.526 ± 0.022 | 0.646 ± 0.016 |
| 2048 | 2 | 0.380 ± 0.220 | 0.301 ± 0.246 | 0.355 ± 0.261 | 0.620 ± 0.016 | 0.495 ± 0.014 | 0.624 ± 0.009 |
|  | 4 | 0.111 ± 0.000 | 0.000 ± 0.000 | 0.036 ± 0.000 | 0.512 ± 0.131 | 0.351 ± 0.176 | 0.485 ± 0.193 |
|  | 8 | 0.450 ± 0.018 | 0.379 ± 0.021 | 0.450 ± 0.019 | 0.620 ± 0.006 | 0.495 ± 0.007 | 0.623 ± 0.005 |
|  | 16 | 0.514 ± 0.008 | 0.449 ± 0.008 | 0.512 ± 0.007 | 0.658 ± 0.004 | 0.547 ± 0.005 | 0.662 ± 0.004 |
|  | 32 | 0.531 ± 0.014 | 0.470 ± 0.015 | 0.514 ± 0.013 | 0.661 ± 0.009 | 0.550 ± 0.012 | 0.665 ± 0.009 |
| dmodel | Epochs | MentalArithmetic |  |  |
| --- | --- | --- | --- | --- |
|  |  | ACC | AUC-PR | AUROC |
| 256 | 2 | 0.530 ± 0.071 | 0.325 ± 0.079 | 0.625 ± 0.078 |
|  | 4 | 0.537 ± 0.066 | 0.333 ± 0.051 | 0.620 ± 0.046 |
|  | 8 | 0.710 ± 0.086 | 0.620 ± 0.103 | 0.811 ± 0.054 |
|  | 16 | 0.567 ± 0.063 | 0.516 ± 0.102 | 0.767 ± 0.042 |
|  | 32 | 0.647 ± 0.025 | 0.504 ± 0.069 | 0.734 ± 0.033 |
| 512 | 2 | 0.586 ± 0.051 | 0.457 ± 0.069 | 0.700 ± 0.042 |
|  | 4 | 0.623 ± 0.043 | 0.505 ± 0.061 | 0.766 ± 0.022 |
|  | 8 | 0.639 ± 0.057 | 0.466 ± 0.149 | 0.728 ± 0.074 |
|  | 16 | 0.712 ± 0.014 | 0.643 ± 0.049 | 0.803 ± 0.019 |
|  | 32 | 0.728 ± 0.030 | 0.672 ± 0.030 | 0.805 ± 0.028 |
| 768 | 2 | 0.569 ± 0.033 | 0.367 ± 0.067 | 0.610 ± 0.044 |
|  | 4 | 0.577 ± 0.063 | 0.433 ± 0.052 | 0.693 ± 0.032 |
|  | 8 | 0.738 ± 0.034 | 0.615 ± 0.046 | 0.811 ± 0.027 |
|  | 16 | 0.692 ± 0.033 | 0.709 ± 0.025 | 0.819 ± 0.019 |
|  | 32 | 0.710 ± 0.025 | 0.705 ± 0.040 | 0.824 ± 0.029 |
| 1024 | 2 | 0.576 ± 0.032 | 0.393 ± 0.065 | 0.648 ± 0.053 |
|  | 4 | 0.704 ± 0.044 | 0.601 ± 0.064 | 0.800 ± 0.031 |
|  | 8 | 0.574 ± 0.016 | 0.395 ± 0.017 | 0.660 ± 0.020 |
|  | 16 | 0.626 ± 0.032 | 0.470 ± 0.066 | 0.770 ± 0.050 |
|  | 32 | 0.693 ± 0.020 | 0.561 ± 0.034 | 0.792 ± 0.015 |
| 2048 | 2 | 0.630 ± 0.076 | 0.610 ± 0.073 | 0.848 ± 0.028 |
|  | 4 | 0.500 ± 0.000 | 0.596 ± 0.065 | 0.501 ± 0.003 |
|  | 8 | 0.554 ± 0.008 | 0.352 ± 0.057 | 0.621 ± 0.047 |
|  | 16 | 0.717 ± 0.038 | 0.618 ± 0.073 | 0.816 ± 0.028 |
|  | 32 | 0.690 ± 0.025 | 0.644 ± 0.059 | 0.795 ± 0.028 |

---

# D EXTENDED RESULTS

# D.1 COMPREHENSIVE DIVER DOWNSTREAM TASK RESULTS

We present the detailed numerical values. The EEG performance table is provided in Table 15. The iEEG performance table is provided in Table 13 and Table 14. For Neuroprobe binary-label (iEEG task), we evaluated  $\mathrm{DIVER}_{Tiny / I / 0.1s}$  (with  $d_{\mathrm{model}} = 256$  and patch size 0.1s, pretrained on iEEG for 32 epochs) in both frozen (linear probing, red) and fine-tuned (black) configurations against Linear Laplacian STFT, BrainBERT and PopT baselines on Figure 3. Table 14 presents comprehensive results comparing DIVER with baseline models across all 15 Neuroprobe tasks. For Neuroprobe multi-label, our model are still overperform the linear baseline. Results are reported as mean AUROC  $\pm$  SEM across subjects, trials, and cross-validation folds. DIVER consistently outperformed baseline models across the majority of tasks in both evaluation settings. The model demonstrated particularly strong performance on language-related tasks (speech decoding, word prediction, onset detection) and auditory tasks (volume, pitch), with finetuning providing additional gains over frozen features. These results validate that self-supervised pretraining on iEEG data produces representations that transfer effectively to diverse downstream neural decoding tasks. In the multi-label setting, DIVER again outperformed the linear baseline for both frozen and fully fine-tuned models. $^3$

For MAYO (iEEG task), we evaluated  $\mathrm{DIVER}_{Tiny / I / 1s}$  (with  $d_{\mathrm{model}} = 256$  and 1 s patch size, pretrained on iEEG for 32 epochs) in both frozen (linear probing) and full-finetuning settings. We could not evaluate PopT because the dataset does not contain any coordinates. By contrast, although our model is trained with 3D positional embeddings, it can handle missing position information by replacing the positional embedding with a zero vector for electrodes with unknown location. Among the different baselines (BrainBERT frozen, Brant frozen, and Brant full-finetuning),  $\mathrm{DIVER}_{Tiny / I / 1s}$  achieved the best performance. Brant exhibited a substantial performance drop under full finetuning, likely because we deviated from its original pretraining configuration by using only a single patch, which can impair optimization when updating all parameters with original context windows (90s), whereas the frozen setting simply uses the fixed embedding.

Table 13: Comparison of the DIVER-1 iEEG model with other baseline models. We evaluated  $\mathrm{DIVER}_{Tiny / I}$  models that were pretrained for 32 epochs on  $100\%$  of the iEEG pretraining dataset. For Neuroprobe (1 s), we compare  $\mathrm{DIVER}_{Tiny / I / 0.1}$  with other baselines using an overall score defined as the mean AUROC averaged over all 15 tasks, subjects, trials, and folds. For MAYO (6 s), we compare  $\mathrm{DIVER}_{Tiny / I / 1s}$  with Brant and BrainBERT; scores are reported as mean AUROC  $\pm$  SEM across 8 subjects and 3 folds.

|  | Neuroprobe (overall) |  | MAYO |
| --- | --- | --- | --- |
|  | binary-label | multi-label |  |
| linear (stft-laplacian) | 0.660 ± 0.005 | 0.617 ± 0.007 | - |
| PopT | 0.545 ± 0.006 | - | - |
| BrainBERT (frozen) | 0.586 ± 0.004 | - | 0.748 ± 0.038 |
| Brant | - | - | 0.551 ± 0.023 |
| Brant (frozen) | - | - | 0.757 ± 0.042 |
| DIVER_Tiny/I/0.1or1s | 0.662 ± 0.008 | 0.621 ± 0.007 | 0.961 ± 0.011 |
| DIVER_Tiny/I/0.1or1s (frozen) | 0.676 ± 0.007 | 0.631 ± 0.007 | 0.935 ± 0.012 |

---

Table 14: Downstream performance of each task in Neuroprobe. We compare DIVER with existing models on comprehensive iEEG downstream tasks. We evaluated both the fine-tuned and frozen configurations of  $\mathrm{DIVER}_{Tiny / I / 0.1s}$  (pretrained on iEEG for 32 epochs) against Linear Laplacian STFT, BrainBERT, and popT. Results are reported as mean AUROC  $\pm$  SEM across subjects, trials, and folds. Overall, DIVER consistently outperformed baselines across the majority of tasks.

| Models | Overall | Sentence Onset | Speech | Volume |
| --- | --- | --- | --- | --- |
| Linear Laplacian STFT | 0.660 ± 0.005 | 0.891 ± 0.018 | 0.883 ± 0.018 | 0.717 ± 0.032 |
| BrainBERT (frozen) | 0.586 ± 0.004 | 0.757 ± 0.027 | 0.611 ± 0.022 | 0.583 ± 0.010 |
| PopT | 0.545 ± 0.006 | 0.689 ± 0.050 | 0.677 ± 0.044 | 0.576 ± 0.018 |
| DIVER$T_{iny}/I/0.1s$ | 0.662 ± 0.008 | 0.924 ± 0.009 | 0.900 ± 0.011 | 0.699 ± 0.020 |
| DIVER$T_{iny}/I/0.1s$ (frozen) | 0.676 ± 0.007 | 0.930 ± 0.008 | 0.896 ± 0.012 | 0.717 ± 0.018 |
| Models | Delta Volume | Voice Pitch | Word position | Inter-word Gap |
| Linear Laplacian STFT | 0.762 ± 0.026 | 0.578 ± 0.016 | 0.740 ± 0.028 | 0.612 ± 0.014 |
| BrainBERT (frozen) | 0.706 ± 0.021 | 0.524 ± 0.007 | 0.685 ± 0.027 | 0.584 ± 0.017 |
| PopT | 0.628 ± 0.025 | 0.509 ± 0.008 | 0.519 ± 0.023 | 0.509 ± 0.009 |
| DIVER$T_{iny}/I/0.1s$ | 0.812 ± 0.017 | 0.563 ± 0.007 | 0.777 ± 0.016 | 0.623 ± 0.014 |
| DIVER$T_{iny}/I/0.1s$ (frozen) | 0.809 ± 0.016 | 0.589 ± 0.007 | 0.791 ± 0.014 | 0.628 ± 0.011 |
| Models | GPT-2 Surprisal | Head Word Pos | Part of Speech | Word Length |
| Linear Laplacian STFT | 0.613 ± 0.017 | 0.602 ± 0.012 | 0.605 ± 0.012 | 0.618 ± 0.015 |
| BrainBERT (frozen) | 0.580 ± 0.015 | 0.585 ± 0.013 | 0.556 ± 0.012 | 0.571 ± 0.012 |
| PopT | 0.523 ± 0.014 | 0.519 ± 0.008 | 0.513 ± 0.004 | 0.505 ± 0.005 |
| DIVER$T_{iny}/I/0.1s$ | 0.617 ± 0.009 | 0.613 ± 0.009 | 0.597 ± 0.011 | 0.638 ± 0.011 |
| DIVER$T_{iny}/I/0.1s$ (frozen) | 0.628 ± 0.009 | 0.622 ± 0.009 | 0.624 ± 0.011 | 0.642 ± 0.013 |
| Models | Global Flow | Local Flow | Frame Brightness | Num of Faces |
| Linear Laplacian STFT | 0.625 ± 0.054 | 0.607 ± 0.017 | 0.521 ± 0.025 | 0.530 ± 0.014 |
| BrainBERT (frozen) | 0.521 ± 0.006 | 0.525 ± 0.003 | 0.508 ± 0.012 | 0.503 ± 0.007 |
| PopT | 0.509 ± 0.008 | 0.508 ± 0.014 | 0.499 ± 0.019 | 0.492 ± 0.010 |
| DIVER$T_{iny}/I/0.1s$ | 0.587 ± 0.010 | 0.586 ± 0.012 | 0.492 ± 0.015 | 0.509 ± 0.007 |
| DIVER$T_{iny}/I/0.1s$ (frozen) | 0.620 ± 0.009 | 0.614 ± 0.012 | 0.502 ± 0.012 | 0.523 ± 0.010 |

Table 15: Comparison of DIVER-1 EEG model with other baseline models. We compare DIVER with existing state-of-the-art models on three EEG downstream tasks using their reported values from the original papers. DIVER consistently outperformed baseline models across all metrics.

| Models | FACED (9-class) |  |  |
| --- | --- | --- | --- |
|  | ACC | kappa | F1 |
| LaBraM | 0.527 ± 0.011 | 0.470 ± 0.019 | 0.529 ± 0.010 |
| CBraMod | 0.551 ± 0.009 | 0.504 ± 0.012 | 0.562 ± 0.009 |
| DIVER (Ours) | 0.601 ± 0.008 | 0.550 ± 0.009 | 0.607 ± 0.009 |
| Models | PhysioNet-MI (4-class) |  |  |
|  | ACC | kappa | F1 |
| LaBraM | 0.617 ± 0.012 | 0.491 ± 0.019 | 0.618 ± 0.014 |
| CBraMod | 0.642 ± 0.009 | 0.522 ± 0.017 | 0.643 ± 0.010 |
| DIVER (Ours) | 0.676 ± 0.003 | 0.567 ± 0.004 | 0.678 ± 0.004 |
| Models | MentalArithmetic (2-class) |  |  |
|  | ACC | AUC-PR | AUROC |
| LaBraM | 0.691 ± 0.013 | 0.600 ± 0.016 | 0.772 ± 0.009 |
| CBraMod | 0.726 ± 0.013 | 0.627 ± 0.010 | 0.791 ± 0.007 |
| DIVER (Ours) | 0.727 ± 0.018 | 0.676 ± 0.046 | 0.814 ± 0.026 |

# D.2 PERFORMANCE EVALUATION ACROSS DIVER-1 MODEL CONFIGURATIONS

We first evaluated  $\mathrm{DIVER}_{Tiny / I / }$  's performance in Neuroprobe, based on different model configurations including the patch size, Laplacian re-referencing and training settings. The 0.1s model outperformed the 1s model (Table 16) in 4 tasks in Neuroprobe. Considering that the Neuroprobe

---

dataset consists of 1-second samples and its tasks require classifying short-timescale features such as speech and onset, the effectiveness of 0.1s model may be explained. Additionally, the model without Laplacian re-referencing generally showed degraded performance, indicating the effectiveness of the pre-processing method. Further, we examined the effect of pretraining by comparing the performance of  $\mathrm{DIVER}_{Tiny / I / 0.1s}$  with diverse training settings. The model trained from scratch showed significantly degraded performance than the full-finetuned and backbone-frozen models. Such results indicate the efficacy of pretraining. Specifically, the model with a frozen backbone showed the highest performance, except for the speech task.

Table 16: Performance evaluation between various DIVER model configurations in Neuroprobe (iEEG tasks). We first compare  $\mathrm{DIVER}_{Tiny/I}$  models by patch size, Laplacian re-referencing, and training settings. The model from scratch was trained on only four tasks (speech, onset, volume, pitch) due to computational constraints, consequently; model evaluation is limited to these four tasks. For the backbone-frozen models, 0.1s variants with different sizes were trained on four tasks, whereas the tiny model was trained on all Neuroprobe tasks. The results are reported as mean AUROC ± SEM across multiple subjects, trials, and folds. All models, except the one trained from scratch, were pretrained for 32 epochs on 100% of the iEEG pretraining dataset.

|  | speech | onset | volume | pitch | neuroprobe total |
| --- | --- | --- | --- | --- | --- |
| Tiny/I/1s | 0.828 ± 0.016 | 0.885 ± 0.012 | 0.634 ± 0.018 | 0.551 ± 0.009 | 0.645 ± 0.007 |
| Tiny/I/0.1s | 0.900 ± 0.011 | 0.924 ± 0.009 | 0.699 ± 0.020 | 0.563 ± 0.007 | 0.662 ± 0.008 |
| Tiny/I/0.1s (w.o. laplacian) | 0.862 ± 0.018 | 0.901 ± 0.013 | 0.662 ± 0.018 | 0.533 ± 0.004 | 0.642 ± 0.007 |
| Tiny/I/0.1s (from scratch) | 0.832 ± 0.014 | 0.872 ± 0.010 | 0.622 ± 0.016 | 0.554 ± 0.006 | - |
| Tiny/I/0.1s (frozen) | 0.896 ± 0.012 | 0.930 ± 0.008 | 0.717 ± 0.018 | 0.589 ± 0.007 | 0.676 ± 0.007 |
| Small/I/0.1s (frozen) | 0.888 ± 0.012 | 0.926 ± 0.009 | 0.705 ± 0.016 | 0.578 ± 0.006 | - |
| Large/I/0.1s (frozen) | 0.890 ± 0.0126 | 0.928 ± 0.009 | 0.710 ± 0.017 | 0.581 ± 0.007 | - |
| XL/I/0.1s (frozen) | 0.893 ± 0.012 | 0.930 ± 0.009 | 0.713 ± 0.017 | 0.582 ± 0.007 | - |

And for MAYO (seizure detection), we chose only 1 sec model, because MAYO has 6 s window that is too long for 0.1 s model's context. We compared the frozen and full finetuning model in each model size in Table 17. In contrast to the Neuroprobe results, we found that full fine-tuning outperformed the frozen for the Tiny, Small and XL model, even though it was slightly worse for the Large and Base models. Since our preprocessing clips signal amplitudes above a certain threshold  $(200\mu \mathrm{V})$ , so pretrained-dataset's distribution can differ from seizure data, which contains spikes with much larger amplitudes; under this distribution shift, fully fine-tuned models may therefore tend to achieve better performance. For the linear baseline, the highest performance was obtained with the Large model, whereas under full-finetuning the Tiny model achieved the best performance.

Table 17: Performance evaluation between various DIVER model configurations in MAYO (iEEG task). DIVER 1 s models were trained for each model size, and we compared the frozen and full fine-tuning variants. The results are reported as mean AUROC ± SEM across multiple subjects and folds. All models, except were pretrained for 32 epochs on 100% of the iEEG pretraining dataset.

|  | Tiny | Small | Base | Large | XL |
| --- | --- | --- | --- | --- | --- |
| frozen | 0.935 ± 0.012 | 0.904 ± 0.019 | 0.911 ± 0.017 | 0.937 ± 0.015 | 0.914 ± 0.018 |
| full-finetuned | 0.961 ± 0.011 | 0.927 ± 0.020 | 0.905 ± 0.026 | 0.934 ± 0.014 | 0.947 ± 0.019 |

# D.3 ABLATIONS

Input ablations Previously in Table16 we confirmed that the iEEG models' downstream performance improve when Laplacian re-referencing is used. PopT and BrainBERT were pretrained on Laplacian re-referenced signals, and their downstream performances were also derived under that setting. Even though our model was trained on raw signals (not referenced), it was better with Laplacian referencing (Table 16). Therefore, we use Laplacian re-referencing as the default setting for finetuning on iEEG downstream tasks.

Architecture ablations To assess whether encoder components (RoPE and any variate attention), embedding components, and multi-domain reconstruction task are effective, we removed each ele

---

Table 18: Architecture ablation for iEEG downstream tasks. Tasks include speech decoding, onset detection, volume prediction, and pitch estimation tasks.  $\mathrm{DIVER}_{Tiny / I / 0.1s}$  (bottom row) represents the full model with all components. Each row indicates the model's performance when removing a specific component. All models use 12 layers with  $d_{\mathrm{model}} = 256$  and were pretrained for 8 epochs. Results are reported as mean AUROC  $\pm$  SEM across multiple subjects, trials and folds.

|  | speech | onset | volume | pitch |
| --- | --- | --- | --- | --- |
| w.o. RoPE | 0.886 ± 0.013 | 0.916 ± 0.011 | 0.693 ± 0.019 | 0.579 ± 0.008 |
| w.o anyV attention | 0.889 ± 0.013 | 0.919 ± 0.009 | 0.699 ± 0.018 | 0.579 ± 0.007 |
| w.o RoPE and anyV attention | 0.870 ± 0.014 | 0.898 ± 0.012 | 0.669 ± 0.018 | 0.560 ± 0.006 |
| w.o. STCPE | 0.879 ± 0.014 | 0.911 ± 0.013 | 0.686 ± 0.019 | 0.572 ± 0.007 |
| w.o Channel modality + subtype emb. | 0.892 ± 0.011 | 0.919 ± 0.009 | 0.690 ± 0.017 | 0.577 ± 0.006 |
| w.o Channel 3d position emb. | 0.900 ± 0.011 | 0.927 ± 0.009 | 0.710 ± 0.018 | 0.584 ± 0.009 |
| w.o Spectral feature emb. | 0.885 ± 0.013 | 0.919 ± 0.010 | 0.694 ± 0.019 | 0.571 ± 0.010 |
| w.o Multi-domain reconstruction (only raw) | 0.875 ± 0.014 | 0.916 ± 0.010 | 0.680 ± 0.017 | 0.569 ± 0.006 |
| DIVERTiny/I/0.1s | 0.890 ± 0.013 | 0.922 ± 0.009 | 0.698 ± 0.018 | 0.572 ± 0.008 |

ment and evaluated the corresponding performance. Ablation studies on iEEG were conducted on  $\mathrm{DIVER}_{Tiny / I / 0.1s}$  trained for 8 epochs with full pretraining dataset, and for EEG,  $\mathrm{DIVER}_{Tiny / E / 1s}$  trained for 2 epochs with  $10\%$  of the data were used, due to computational constraints and time limitations. Architecture ablation results for iEEG are given in Table 18. When each encoder component was removed individually, the performance varied across tasks, but dropped noticeably when both were excluded. An ablation of STCPE and multi-domain reconstruction task each induced performance degradation, whereas the ablation of other embedding components did not yield significant changes. Since the Neuroprobe dataset includes only depth electrodes (SEEG), the effect of channel modality and subtype embedding may be minimal. Moreover, as the dataset utilizes only child and adolescent subjects, whose brain volumes differ by age, the effect of the channel 3D positional embedding may be attenuated.

For EEG downstream tasks, detailed results are described in Table 19. The ablation of encoder components yielded a significant performance decline in both EEG tasks, indicating that the encoder components are crucial contributors to overall performance. Removing the multi-domain reconstruction task, STCPE and spectral feature embedding resulted in a notable performance degradation as well. Ablation of the channel-wise patch embedding components led to inconsistent effects across tasks: performance dropped on FACED, whereas performance on PhysioNet-MI did not degrade meaningfully.

Incorporating encoder components and multi-domain reconstruction task significantly improved the model's performance in both iEEG and EEG downstream tasks. Specifically, in multi-domain reconstruction, removing each component for STFT and FFT also degrades performance, which shows that each element of multi-domain reconstruction is important. Channel-wise embedding components however differed in their effects depending on the modality and the type of downstream tasks. Since informative features in Ephys signals can vary across modalities and tasks, holding these various components may help improve generalization across a range of tasks.

Dataset ablations and dataset size-based comparisons The other iEEG models (PopT (Chau et al., 2025) and BrainBERT (Wang et al., 2023)) are pretrained on the BrainTreebank (BTB) (Wang et al., 2024a) datasets—the precursor to Neuroprobe. Therefore, we compare downstream performance when we use BTB exclusively (Figure 13). We trained  $\mathrm{DIVER}_{Tiny / I / 0.1s}$  models with BTB and size-variations of our self-collected iEEG datasets. For the model trained on our self-collected data of the same size as BTB, the linear-probing results were lower than those trained with BTB only. However, when we increased the size of the self-collected dataset (approximately  $\times 16$  and  $\times 64$  size of BTB), performance surpassed the BTB-only setting. This shows that, with sufficient data, it is possible to achieve higher performance even if the distribution of the pretraining dataset differs from that of the downstream tasks.

Comparison of DIVER-1 iEEG model with other baseline models on a shared dataset Since the pretraining dataset between iEEG baseline models and our model differentiated, we additionally trained the DIVER model on the pretraining dataset of the baseline models. The corresponding results are shown in Table 1. The model trained under our own early-stopping strategy is denoted

---

Table 19: Architecture ablation for EEG downstream tasks. Tasks include FACED and PhysioNet-MI dataset.  $\mathrm{DIVER}_{Tiny / E / 1s}$  represents the full model with all components. Each row shows performance when removing a specific component. All models use 12 layers with  $d_{\mathrm{model}} = 256$  and were pretrained for 2 epochs. Results are reported as mean  $\pm$  standard deviation across 5 random seeds.

|  | FACED (9-class) |  |  |
| --- | --- | --- | --- |
|  | ACC | kappa | F1 |
| w.o. RoPE | 0.408 ± 0.025 | 0.333 ± 0.027 | 0.414 ± 0.024 |
| w.o anyV attention | 0.414 ± 0.012 | 0.339 ± 0.014 | 0.417 ± 0.012 |
| w.o RoPE and anyV attention | 0.446 ± 0.007 | 0.376 ± 0.007 | 0.450 ± 0.005 |
| w.o. STCPE | 0.463 ± 0.024 | 0.395 ± 0.027 | 0.471 ± 0.026 |
| w.o Channel modality + subtype emb. | 0.474 ± 0.018 | 0.406 ± 0.021 | 0.482 ± 0.019 |
| w.o Channel 3d position emb. | 0.481 ± 0.016 | 0.415 ± 0.018 | 0.487 ± 0.016 |
| w.o Spectral feature emb. | 0.454 ± 0.015 | 0.386 ± 0.016 | 0.462 ± 0.013 |
| w.o Multi-domain reconstruction (only raw) | 0.435 ± 0.008 | 0.364 ± 0.009 | 0.437 ± 0.006 |
| w.o FFT reconstruction (raw and stft) | 0.468 ± 0.007 | 0.401 ± 0.008 | 0.479 ± 0.008 |
| w.o STFT reconstruction (raw and fft) | 0.485 ± 0.014 | 0.418 ± 0.015 | 0.487 ± 0.013 |
| DIVERTiny/E/1s | 0.491 ± 0.023 | 0.428 ± 0.025 | 0.502 ± 0.023 |
|  | PhysioNet-MI (4-class) |  |  |
|  | ACC | kappa | F1 |
| w.o. RoPE | 0.614 ± 0.005 | 0.485 ± 0.006 | 0.615 ± 0.005 |
| w.o anyV attention | 0.611 ± 0.003 | 0.481 ± 0.004 | 0.612 ± 0.004 |
| w.o RoPE and anyV attention | 0.591 ± 0.005 | 0.454 ± 0.006 | 0.593 ± 0.005 |
| w.o. STCPE | 0.626 ± 0.006 | 0.502 ± 0.008 | 0.627 ± 0.006 |
| w.o Channel modality + subtype emb. | 0.629 ± 0.006 | 0.505 ± 0.007 | 0.632 ± 0.005 |
| w.o Channel 3d position emb. | 0.629 ± 0.008 | 0.506 ± 0.010 | 0.631 ± 0.007 |
| w.o Spectral feature emb. | 0.626 ± 0.005 | 0.501 ± 0.006 | 0.627 ± 0.004 |
| w.o Multi-domain reconstruction (only raw) | 0.614 ± 0.005 | 0.485 ± 0.006 | 0.616 ± 0.004 |
| w.o FFT reconstruction (raw and stft) | 0.626 ± 0.006 | 0.502 ± 0.008 | 0.628 ± 0.006 |
| w.o STFT reconstruction (raw and fft) | 0.615 ± 0.005 | 0.487 ± 0.007 | 0.617 ± 0.005 |
| DIVERTiny/E/1s | 0.628 ± 0.005 | 0.504 ± 0.007 | 0.630 ± 0.005 |

---

![img-18.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-19.jpg)
Figure 13: Pretraining dataset and size effects on performance: BrainTreebank vs. Self-Collected

as "ours." Given the same pretraining dataset, the DIVER model achieved the highest performance compared to the two baseline models.

# D.4 ANALYSIS OF JOINT MODALITY (INTRACRANIAL/SCALP-EEG) PRETRAINING

We examined the effects of joint training on both iEEG and EEG downstream tasks, with detailed results presented in Table 20. Joint training showed contrasting effects on the two modalities: it decreased performance on iEEG benchmarks but improved performance on EEG tasks.

This difference may stem from the signal quality disparity between the two modalities. Since EEG signals are inherently noisier than iEEG signals, incorporating EEG data during joint training may introduce noise that degrades the model's ability to process high-quality iEEG signals. Conversely, for EEG tasks, joint training provides EEG specific information that iEEG cannot provide. Additionally, the data imbalance between modalities may contribute to these results. Since EEG data outnumber iEEG data, the model may become biased toward EEG-specific patterns during joint training. As detailed in Table 20, training exclusively on curated EEG datasets achieves the best performance on EEG downstream tasks, outperforming models that include iEEG data.

To further analyze how the composition of pretraining data influences EEG downstream performance, we conducted ablation studies across different EEG and iEEG dataset combinations, as shown in Table 21. With only two pretraining epochs, models pretrained exclusively on curated EEG datasets consistently outperformed those incorporating iEEG data across both FACED and PhysioNet-MI benchmarks. Even within the EEG modality, combining multiple datasets outperformed using the largest single dataset alone (TUEG-only), highlighting the benefits of dataset diversity.

This trend, however, reverses with extended pretraining. As shown in Table 22, while EEG-only pretraining yields superior performance in epoch2 and epoch8, models jointly pretrained on EEG and iEEG eventually outperform EEG-only counterparts given sufficient training time(epoch16). This suggests that modality heterogeneity acts as an initial impediment that the model gradually overcomes, ultimately enabling it to leverage complementary information across modalities. Based on these findings, we selected the EEG+iEEG jointly pretrained model as our final configuration for all subsequent EEG downstream evaluations.

---

Table 20: Joint pretraining results on downstream tasks. Performance compared between  $\mathrm{DIVER}_{Ting / I / 1s}$  (trained on iEEG only) and  $\mathrm{DIVER}_{Ting / IE / 1s}$  (trained on iEEG and EEG), both with  $d_{model} = 256$ . Performance across iEEG tasks (speech and onset, measured by AUROC) and EEG task (FACED, measured by ACC) are shown. Joint training with EEG data improves performance on EEG tasks but slightly decreases performance on iEEG tasks.

|  | speech (iEEG, AUROC) | onset (iEEG, AUROC) | FACED (EEG, ACC) |
| --- | --- | --- | --- |
| Ting/I/1s (frozen) | 0.854 ± 0.011 | 0.906 ± 0.008 | 0.328 ± 0.003 |
| Ting/IE/1s (frozen) | 0.817 ± 0.018 | 0.891 ± 0.012 | 0.359 ± 0.004 |

Table 21: Ablation on pretraining data composition for EEG downstream tasks. We evaluated how different pretraining dataset combinations affect performance on EEG downstream tasks. We compared models pretrained on: TUEG (Obeid &amp; Picone, 2016)-only (largest single EEG dataset), TUEG+iEEG, all EEG datasets, and EEG+iEEG (all available data). All models use  $\mathrm{DIVER}_{Small / E / 1s}$  architecture with  $d_{\mathrm{model}} = 512$ , pretrained for 2 epochs. The model trained exclusively on curated EEG datasets achieves the best performance, outperforming models that include iEEG data.

| Pretraining Data | FACED (9-class) |  |  | PhysioNet-MI (4-class) |  |  |
| --- | --- | --- | --- | --- | --- | --- |
|  | ACC | kappa | F1 | ACC | kappa | F1 |
| TUEG-only | 0.519 ± 0.004 | 0.456 ± 0.005 | 0.518 ± 0.005 | 0.623 ± 0.010 | 0.497 ± 0.013 | 0.625 ± 0.009 |
| TUEG + iEEG | 0.461 ± 0.011 | 0.394 ± 0.013 | 0.471 ± 0.012 | 0.599 ± 0.008 | 0.465 ± 0.010 | 0.600 ± 0.008 |
| EEG + iEEG | 0.540 ± 0.013 | 0.482 ± 0.015 | 0.550 ± 0.014 | 0.638 ± 0.005 | 0.517 ± 0.006 | 0.639 ± 0.004 |
| EEG | 0.570 ± 0.009 | 0.515 ± 0.010 | 0.579 ± 0.008 | 0.644 ± 0.005 | 0.526 ± 0.006 | 0.646 ± 0.005 |

Table 22: Ablation on pretraining data composition across pretraining epochs. We compare EEG-only vs EEG+iEEG pretraining at different pretraining epochs. All models use  $\mathrm{DIVER}_{Small / E / 1s}$  architecture with  $d_{\mathrm{model}} = 512$ . Notably, with longer pretraining, EEG+iEEG consistently outperforms EEG-only across downstream tasks.

| Epochs | Pretraining Data | FACED (9-class) |  |  | PhysioNet-MI (4-class) |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- |
|  |  | ACC | kappa | F1 | ACC | kappa | F1 |
| 2 | EEG-only | 0.570 ± 0.009 | 0.515 ± 0.010 | 0.579 ± 0.008 | 0.644 ± 0.005 | 0.526 ± 0.006 | 0.646 ± 0.005 |
|  | EEG + iEEG | 0.540 ± 0.013 | 0.482 ± 0.015 | 0.550 ± 0.014 | 0.638 ± 0.005 | 0.517 ± 0.006 | 0.639 ± 0.004 |
| 8 | EEG-only | 0.594 ± 0.016 | 0.542 ± 0.017 | 0.604 ± 0.013 | 0.658 ± 0.019 | 0.544 ± 0.026 | 0.660 ± 0.019 |
|  | EEG + iEEG | 0.514 ± 0.110 | 0.453 ± 0.123 | 0.521 ± 0.116 | 0.651 ± 0.013 | 0.534 ± 0.017 | 0.653 ± 0.013 |
| 16 | EEG-only | 0.541 ± 0.048 | 0.485 ± 0.054 | 0.551 ± 0.051 | 0.662 ± 0.012 | 0.549 ± 0.017 | 0.664 ± 0.012 |
|  | EEG + iEEG | 0.601 ± 0.008 | 0.550 ± 0.009 | 0.607 ± 0.009 | 0.676 ± 0.003 | 0.567 ± 0.004 | 0.678 ± 0.004 |

---

Table 23: Comparison of finetuning architectures in EEG downstream tasks. Deeper heads generally improve performance up to 3-4 layers.

| Head Depth | FACED (9-class) |  |  | PhysioNet-MI (4-class) |  |  |
| --- | --- | --- | --- | --- | --- | --- |
|  | ACC | kappa | F1 | ACC | kappa | F1 |
| Linear | 0.523 ± 0.018 | 0.461 ± 0.020 | 0.521 ± 0.018 | 0.653 ± 0.013 | 0.538 ± 0.017 | 0.654 ± 0.013 |
| 2-Layer | 0.584 ± 0.005 | 0.530 ± 0.005 | 0.584 ± 0.005 | 0.674 ± 0.003 | 0.565 ± 0.004 | 0.676 ± 0.003 |
| 3-Layer | 0.601 ± 0.008 | 0.550 ± 0.009 | 0.607 ± 0.009 | 0.676 ± 0.003 | 0.567 ± 0.004 | 0.678 ± 0.004 |
| 4-Layer | 0.603 ± 0.007 | 0.552 ± 0.008 | 0.609 ± 0.007 | 0.672 ± 0.008 | 0.573 ± 0.011 | 0.674 ± 0.008 |
| 5-Layer | 0.594 ± 0.021 | 0.543 ± 0.023 | 0.601 ± 0.019 | 0.660 ± 0.007 | 0.547 ± 0.009 | 0.662 ± 0.006 |

# D.5 INTERPRETATION RESULTS

![img-19.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-20.jpg)
Figure 14 shows a visualization of representation analysis on downstream datasets using UMAP (McInnes et al., 2018). We examine the embeddings obtained from the pretrained  $\mathrm{DIVER}_{\mathrm{Tiny} / 1 / 0.1s}$  model on the test set of speech, onset, and volume tasks in neuroprobe dataset without any finetuning. The results indicate that DIVER learned meaningful iEEG representations from pretraining, thereby capturing label-relevant structure in downstream datasets even in the absence of finetuning.

![img-20.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-21.jpg)
Figure 14: Visualizations of representations on neuroprobe downstream tasks. Each plot shows test set embeddings from one fold of a single trial from a single subject.

![img-21.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-22.jpg)

To obtain an interpretable salience measure of the model, we applied attention rollout (Abnar &amp; Zuidema, 2020), which aggregates attention weights across all attention layers. Although DIVER's any-variate attention produces a high-dimensional matrix, the attention rollout yielded a rank-1 matrix across all subjects and sessions. We therefore used a single representative row, reflecting a uniform attention distribution across keys independent of query. Figure 15 shows task-dependent temporal and cortical attribution patterns derived from the attention rollout of  $\mathrm{DIVER}_{\mathrm{Tiny} / 1 / 0.1s}$ . Attention rollout weights were computed on test sets for four high AUROC scored Neuroprobe tasks (volume, pitch, GPT-2 surprisal, and word head position). We follow PopT's method of mapping attention weights onto the cortical surface, normalizing within each subject and scaling by the test AUROC (Chau et al., 2025). The resulting weights were averaged across subjects, trials, and folds.

Across both auditory (volume, pitch) and language (GPT-2 surprisal, word head position) tasks, attention rollout exhibits two temporal peaks: an early window  $(0 - 300\mathrm{ms})$  and a late window  $(800 - 1000\mathrm{ms})$ . The early peak coincides with word onset of each sample and engages core speech-language regions, including inferior temporal gyrus and Broca's and Wernicke's areas (Mesgarani et al., 2014). The late peak shows task-specific spatial patterns. For auditory tasks, attribution remains concentrated in primary auditory cortex (Heschl's gyrus and superior temporal gyrus). This is consistent with the possible continued auditory processing of subsequent words within the 1s window. In contrast, language tasks show increased engagement of temporal-frontal regions in the later window. This aligns with the known post-auditory latency of higher language networks (Hickok &amp; Poeppel, 2007; Rauschecker &amp; Scott, 2009). Overall, these results indicate that DIVER attends to tokens in a temporally structured manner with task-relevant spatial attribution. Notably, the right middle occipital gyrus remains consistently salient for GPT-2 surprisal, suggesting a contribution of

---

visual-context representations to surprisal estimation (Friederici, 2011; Dehaene &amp; Cohen, 2011). Collectively, DIVER's task-dependent attributions are consistent with established neural models of auditory and language processing (Hickok &amp; Poeppel, 2007).

![img-22.jpeg](source_images/diver-1-deep-integration-of-vast-electrophysiologi-29d0b5-fig-23.jpg)
Figure 15: Scaled attention rollout weights mapped onto the cortical surface for four Neuroprobe downstream tasks. Each panel shows  $\mathrm{DIVER}_{\mathrm{Time} / 1 / 0.1s}$  scaled attention weights extracted via attention rollout and aggregated in  $100~\mathrm{ms}$  bins from  $0\mathrm{ms}$  to  $1\mathrm{s}$  relative to stimulus onset. For each task, the top row shows the left hemisphere and the bottom row shows the right hemisphere; brighter colors indicate larger scaled attention weights, which we interpret as greater model salience on the corresponding channel-temporal token for each task.

---

E Exploration of Finetuning Method

### E.1 Overview: Impact of Finetuning Methodology on EEG Downstream Task Performance

We conduct comprehensive experiments to investigate the impact of different finetuning methods on downstream task performance. Our analysis includes: (1) systematic exploration of MLP classifier depth for DIVER(appendix subsection E.2), (2) reproduction of CBraMod *(Wang et al., 2024c)* performance using publicly available code and weights(appendix subsection E.3), and (3) comparative analysis of various finetuning configurations across both models E.4. These experiments reveal that finetuning methodology significantly affects model performance, and optimal configurations vary across tasks and models. Importantly, when comparing DIVER and CBraMod under identical finetuning configurations (one-to-one comparison), DIVER demonstrates competitive or superior performance to CBraMod across multiple tasks, achieving overall state-of-the-art results despite CBraMod’s higher reported in-paper performance on some tasks.

### E.2 Impact of MLP Classifier Depth on DIVER Performance

Initially, we employed a linear classifier head for finetuning but observed suboptimal performance. Upon examining the publicly available code of CBraMod *(Wang et al., 2024c)*, the previous state-of-the-art model, we found that it uses an MLP classifier head. To ensure fair comparison, we replaced the linear head with an MLP classifier, which resulted in substantial performance improvements for DIVER-1. This motivated us to conduct systematic experiments investigating how MLP depth affects performance. Table 23 compares the performance across the depths of MLP classifier for downstream EEG tasks. The original 3-layer MLP classifier is varied between 1 to 5 layers. For both FACED and PhysioNet-MI tasks, performance improved with the increase of MLP depth, achieving peak performance at 4-layer for FACED (balanced accuracy of 0.603) and 3-layer for PhysioNet-MI (balanced accuracy of 0.676). Beyond the optimal depth, we observed performance saturation or slight degradation, particularly notable in the 5-layer MLP for both datasets. These results indicate that a moderate depth (3-4 layers) suffices model’s effectiveness across different EEG downstream tasks.

### E.3 Challenges in Reproducing CBraMod Baseline Performance

While we found that finetuning method significantly impacts downstream task performance, the CBraMod paper does not specify which finetuning methods were used for each downstream task. Therefore, we conducted experiments to reproduce CBraMod’s performance using the default configuration from their publicly released code and weights. To ensure faithful reproduction, we used CBraMod’s preprocessing pipeline, pretrained weights, and finetuning code without modification.

The experimental results revealed substantial performance gaps on several tasks (Table 24). On MentalArithmetic*(Zyma et al., 2019)*, reproduced accuracy (0.619) fell short of reported performance (0.726); on TUEV*(Obeid and Picone, 2016)*, accuracy decreased from 0.667 to 0.605; on Mumtaz2016*(Zyma et al., 2019)*, from 0.956 to 0.882. Only FACED*(Chen et al., 2023)* and PhysioNet-MI*(Goldberger et al., 2000; Schalk et al., 2004)* showed relatively successful reproduction. Notably, similar reproduction difficulties with CBraMod have been reported in recent work *(Wang et al., 2025)*, which also observed performance gaps between reported and reproduced results on certain tasks.

These reproduction challenges highlight the sensitivity of EEG foundation models to finetuning configurations. When comparing DIVER to the reproduced CBraMod baselines, the performance gaps narrow considerably: on TUEV, DIVER achieves 0.630 compared to reproduced CBraMod’s 0.605; on MentalArithmetic, 0.727 vs 0.619. This underscores the importance of transparent reporting of finetuning protocols for fair model comparison.

### E.4 Task-Specific Optimal Finetuning Configurations for CBraMod and DIVER

As mentioned above, the default configuration from CBraMod’s public code was insufficient to fully reproduce their reported performance. To maximize performance recovery, we experimented with

---

Table 24: Comparison of DIVER-1 EEG model with CBraMod. CBraMod (in paper) refers to the performance reported in the original CBraMod paper, while CBraMod (reproduction) represents our reproduction using the default configuration from their publicly released code and weights. We conduct systematic finetuning method experiments to ensure fair comparison, with detailed results provided in Table 25.

| Models | FACED (9-class) |  |  |
| --- | --- | --- | --- |
|  | ACC | kappa | F1 |
| CBraMod(in paper) | 0.551 ± 0.009 | 0.504 ± 0.012 | 0.562 ± 0.009 |
| CBraMod(reproduction) | 0.570 ± 0.005 | 0.514 ± 0.006 | 0.574 ± 0.006 |
| DIVER (Ours) | 0.601 ± 0.008 | 0.550 ± 0.009 | 0.607 ± 0.009 |
| Models | PhysioNet-MI (4-class) |  |  |
|  | ACC | kappa | F1 |
| CBraMod(in paper) | 0.642 ± 0.009 | 0.522 ± 0.017 | 0.643 ± 0.010 |
| CBraMod(reproduction) | 0.621 ± 0.002 | 0.495 ± 0.003 | 0.622 ± 0.003 |
| DIVER (Ours) | 0.676 ± 0.003 | 0.567 ± 0.004 | 0.678 ± 0.004 |
| Models | MentalArithmetic (2-class) |  |  |
|  | ACC | AUC-PR | AUROC |
| CBraMod(in paper) | 0.726 ± 0.013 | 0.627 ± 0.010 | 0.791 ± 0.007 |
| CBraMod(reproduction) | 0.619 ± 0.035 | 0.533 ± 0.064 | 0.749 ± 0.031 |
| DIVER (Ours) | 0.727 ± 0.018 | 0.676 ± 0.046 | 0.814 ± 0.026 |
| Models | Mumtaz2016 (2-class) |  |  |
|  | ACC | AUC-PR | AUROC |
| CBraMod(in paper) | 0.956 ± 0.006 | 0.992 ± 0.003 | 0.992 ± 0.003 |
| CBraMod(reproduction) | 0.882 ± 0.019 | 0.976 ± 0.007 | 0.974 ± 0.009 |
| DIVER (Ours) | 0.894 ± 0.006 | 0.971 ± 0.003 | 0.968 ± 0.005 |
| Models | TUEV (6-class) |  |  |
|  | ACC | kappa | F1 |
| CBraMod(in paper) | 0.667 ± 0.011 | 0.677 ± 0.010 | 0.834 ± 0.006 |
| CBraMod(reproduction) | 0.605 ± 0.024 | 0.623 ± 0.016 | 0.802 ± 0.009 |
| DIVER (Ours) | 0.630 ± 0.029 | 0.527 ± 0.039 | 0.747 ± 0.019 |

various finetuning methods available in their codebase. We systematically explored five different configurations: (1) no multi lr: using a single learning rate for both backbone and head, (2) multi lr multiplier  $3/7$ : setting the head learning rate to  $3 \times$  or  $7 \times$  the backbone learning rate, (3) linear classifier: full finetuning with a 1-layer linear head, (4) linear probing: freezing the backbone while training only a 1-layer linear head, and (5) CBraMod finetuning method: using a 3-layer MLP head with  $5 \times$  learning rate multiplier as the default configuration.

As shown in Table 25, the optimal finetuning method for CBraMod varied across tasks. Specifically, for Mumtaz2016, the "no multi lr" configuration achieved the best performance (ACC: 0.920), while for TUEV, the "linear classifier" method performed best (ACC: 0.635). For MentalArithmetic, both "no multi lr" and the default CBraMod method showed comparable performance.

Interestingly, when applying the same finetuning methods to DIVER, different configurations yielded superior performance compared to what worked best for CBraMod. For instance, on Mumtaz2016, DIVER achieved its best performance with "linear probing" (ACC: 0.944), which performed poorly for CBraMod (ACC: 0.515). On TUEV, DIVER performed best with "multi lr multiplier 3" (ACC: 0.649), whereas CBraMod favored the "linear classifier" approach.

Crucially, when comparing both models under identical finetuning configurations (one-to-one comparison), DIVER demonstrates competitive performance across tasks. DIVER achieves superior performance on multiple configurations for Mumtaz2016 and TUEV, and shows strong results on MentalArithmetic. This head-to-head comparison under controlled conditions reveals that DIVER

---

Table 25: One-to-One Comparison between C Bra Mod and DIVER using fixed finetuning method. Both models evaluated with identical finetuning configurations. C Bra Mod uses publicly released weights and code. DIVER model uses 12 layers with  $d_{\mathrm{model}} = 512$  and were pretrained for 16 epochs. Results are reported as mean ± standard deviation across 5 random seeds.

| Mumtaz2016(2-class) | DIVER |  |  | C Bra Mod |  |  |
| --- | --- | --- | --- | --- | --- | --- |
|  | ACC | AUC-PR | AUROC | ACC | AUC-PR | AUROC |
| no multi lr | 0.894 ± 0.006 | 0.971 ± 0.003 | 0.968 ± 0.005 | 0.920 ± 0.027 | 0.985 ± 0.010 | 0.984 ± 0.012 |
| multi lr multiplier 3 | 0.896 ± 0.003 | 0.980 ± 0.001 | 0.979 ± 0.002 | 0.892 ± 0.010 | 0.977 ± 0.006 | 0.974 ± 0.008 |
| multi lr multiplier 7 | 0.882 ± 0.044 | 0.981 ± 0.008 | 0.980 ± 0.007 | 0.888 ± 0.012 | 0.977 ± 0.007 | 0.975 ± 0.008 |
| linear classifier | 0.902 ± 0.004 | 0.986 ± 0.005 | 0.985 ± 0.006 | 0.872 ± 0.059 | 0.975 ± 0.012 | 0.973 ± 0.014 |
| linear probing | 0.944 ± 0.003 | 0.990 ± 0.000 | 0.990 ± 0.000 | 0.515 ± 0.003 | 0.962 ± 0.003 | 0.972 ± 0.001 |
| C Bra Mod finetuning method* | 0.901 ± 0.011 | 0.985 ± 0.006 | 0.985 ± 0.006 | 0.882 ± 0.019 | 0.976 ± 0.007 | 0.974 ± 0.009 |
| TUEV(6-class) | DIVER |  |  | C Bra Mod |  |  |
|  | ACC | kappa | F1 | ACC | kappa | F1 |
| no multi lr | 0.630 ± 0.029 | 0.527 ± 0.039 | 0.747 ± 0.019 | 0.609 ± 0.021 | 0.618 ± 0.023 | 0.801 ± 0.012 |
| multi lr multiplier 3 | 0.649 ± 0.030 | 0.563 ± 0.026 | 0.765 ± 0.018 | 0.611 ± 0.021 | 0.628 ± 0.027 | 0.805 ± 0.013 |
| multi lr multiplier 7 | 0.648 ± 0.036 | 0.555 ± 0.050 | 0.761 ± 0.025 | 0.602 ± 0.057 | 0.624 ± 0.031 | 0.802 ± 0.017 |
| linear classifier | 0.611 ± 0.024 | 0.524 ± 0.031 | 0.753 ± 0.016 | 0.635 ± 0.024 | 0.625 ± 0.047 | 0.804 ± 0.024 |
| linear probing | 0.559 ± 0.025 | 0.397 ± 0.037 | 0.624 ± 0.041 | 0.314 ± 0.011 | 0.307 ± 0.014 | 0.574 ± 0.012 |
| C Bra Mod finetuning method* | 0.612 ± 0.014 | 0.414 ± 0.021 | 0.644 ± 0.017 | 0.605 ± 0.024 | 0.623 ± 0.016 | 0.802 ± 0.009 |
| MentalArithmetic(2-class) | DIVER |  |  | C Bra Mod |  |  |
|  | ACC | AUC-PR | AUROC | ACC | AUC-PR | AUROC |
| no multi lr | 0.727 ± 0.018 | 0.676 ± 0.046 | 0.814 ± 0.026 | 0.637 ± 0.038 | 0.494 ± 0.022 | 0.747 ± 0.031 |
| multi lr multiplier 3 | 0.654 ± 0.091 | 0.666 ± 0.070 | 0.815 ± 0.027 | 0.629 ± 0.035 | 0.493 ± 0.042 | 0.734 ± 0.025 |
| multi lr multiplier 7 | 0.669 ± 0.120 | 0.710 ± 0.113 | 0.852 ± 0.052 | 0.584 ± 0.030 | 0.459 ± 0.051 | 0.704 ± 0.033 |
| linear classifier | 0.724 ± 0.040 | 0.705 ± 0.035 | 0.855 ± 0.021 | 0.621 ± 0.084 | 0.453 ± 0.079 | 0.720 ± 0.072 |
| linear probing | 0.608 ± 0.037 | 0.667 ± 0.021 | 0.791 ± 0.011 | 0.515 ± 0.008 | 0.522 ± 0.017 | 0.668 ± 0.008 |
| C Bra Mod finetuning method* | 0.735 ± 0.045 | 0.707 ± 0.069 | 0.839 ± 0.022 | 0.619 ± 0.035 | 0.533 ± 0.064 | 0.749 ± 0.031 |

* Finetuning methods: (1) no multi lr: single LR for backbone and head (2) multi lr multiplier X: head LR = X × backbone LR (3) linear classifier: full finetuning with 1-layer head (4) linear probing: frozen backbone, trainable 1-layer head (5) C Bra Mod finetuning method: 3-layer MLP head, multi lr multiplier 5.

achieves overall state-of-the-art performance when evaluation methodology is held constant, even though C Bra Mod's reported in-paper results appear higher on some tasks.

These findings underscore that finetuning methodology is critical for evaluating EFMs, and optimal configurations can be model-dependent. Given this importance, we provide detailed specifications of the finetuning methods used for DIVER (Appendix B.8) to promote transparency and reproducibility in the EFM research community. We hope this contributes positively to establishing standardized evaluation protocols for electrophysiology foundation models.

# E.5 LINEAR PROBING ANALYSIS: EVIDENCE OF HIGH-QUALITY LEARNED REPRESENTATIONS

Linear probing provides a controlled method to evaluate the intrinsic quality of learned representations by eliminating confounding effects of different finetuning configurations (Radford et al., 2021; Chen et al., 2020). Recent electrophysiology foundation model research has similarly employed linear probing to assess representation quality (Anonymous, 2026). Given that optimal finetuning configurations vary across models and tasks (Section E.4), we conduct additional analysis using linear probing to assess the intrinsic quality of DIVER's learned representations. Table 26 presents linear probing results across five downstream tasks, comparing DIVER against C BraMod (Wang et al., 2024c) and EEGPT (Wang et al., 2024b).

---

Table 26: Linear Probing Performance Comparison. DIVER demonstrates superior linear probing performance on 4 out of 5 tasks, indicating high-quality learned representations. Bold indicates best performance; underline indicates second-best. Results are reported as mean ± standard deviation across 5 random seeds.

| Models | FACED (9-class) |  |  |
| --- | --- | --- | --- |
|  | ACC | kappa | F1 |
| CBAMod | 0.257 ± 0.010 | 0.160 ± 0.011 | 0.216 ± 0.012 |
| EEGPT | 0.186 ± 0.011 | 0.084 ± 0.012 | 0.183 ± 0.016 |
| DIVER (Ours) | 0.355 ± 0.005 | 0.272 ± 0.005 | 0.352 ± 0.004 |
| Models | PhysioNet-MI (4-class) |  |  |
|  | ACC | kappa | F1 |
| CBAMod | 0.545 ± 0.011 | 0.393 ± 0.015 | 0.546 ± 0.014 |
| EEGPT | 0.486 ± 0.010 | 0.290 ± 0.014 | 0.468 ± 0.009 |
| DIVER (Ours) | 0.530 ± 0.011 | 0.373 ± 0.015 | 0.531 ± 0.011 |
| Models | MentalArithmetic (2-class) |  |  |
|  | ACC | AUC-PR | AUROC |
| CBAMod | 0.515 ± 0.008 | 0.522 ± 0.017 | 0.668 ± 0.008 |
| EEGPT | 0.535 ± 0.028 | 0.335 ± 0.042 | 0.590 ± 0.045 |
| DIVER (Ours) | 0.608 ± 0.037 | 0.667 ± 0.021 | 0.791 ± 0.011 |
| Models | Mumtaz2016 (2-class) |  |  |
|  | ACC | AUC-PR | AUROC |
| CBAMod | 0.515 ± 0.003 | 0.962 ± 0.003 | 0.972 ± 0.002 |
| EEGPT | 0.897 ± 0.014 | 0.970 ± 0.006 | 0.968 ± 0.006 |
| DIVER (Ours) | 0.944 ± 0.003 | 0.990 ± 0.000 | 0.990 ± 0.000 |
| Models | TUEV (6-class) |  |  |
|  | ACC | kappa | F1 |
| CBAMod | 0.314 ± 0.011 | 0.307 ± 0.014 | 0.574 ± 0.012 |
| EEGPT | 0.446 ± 0.055 | 0.431 ± 0.059 | 0.710 ± 0.029 |
| DIVER (Ours) | 0.559 ± 0.025 | 0.397 ± 0.037 | 0.624 ± 0.041 |

DIVER demonstrates strong linear probing performance across all tasks. On FACED, MentalArithmetic, and Mumtaz2016, DIVER achieves the best performance across all metrics. On TUEV, DIVER achieves the highest accuracy (0.559), while EEGPT shows stronger performance on kappa and F1 scores. On PhysioNet-MI, CBAMod achieves the best performance, though DIVER remains competitive as the second-best model.

These linear probing results indicate that DIVER learns high-quality embeddings that effectively capture task-relevant information even without tuning the backbone. This suggests that DIVER's pretraining approach successfully learns generalizable representations of electrophysiological signals across diverse downstream applications.

# F DATA DETAILS

# F.1 PRETRAINING DATASET DESCRIPTION

The following datasets were utilized for the pretraining of our DIVER models. The total pretraining time for the  $\mathrm{DIVER_I}$  dataset is 5,310 hours, and for the  $\mathrm{DIVER_{IE}}$  dataset, it is 59,613 hours.

- AJILE12 (Anotated Joints in Long-term Electrocorticography) (Peterson et al., 2022): An ECoG dataset from 12 epilepsy patients, recorded semi-continuously over 55 days. Signals were collected from  $\geq 64$  electrodes at  $1\mathrm{kHz}$  sampling rate and paired

---

with synchronized video-vased 3D human pose estimation and annotated wrist-movement events.
- Self-collected iEEG dataset: An intracranial EEG dataset from 25 drug-resistant epilepsy patients ($\sim$7 days, $\sim$168 h per subject) with long-term ECoG and sEEG recordings (mean 56.4 $\pm$ 3.38 channels, sampled at 2 kHz) during naturalistic hospital behaviors.
- TUEG (Temple University Hospital EEG Corpus) *(Obeid and Picone, 2016)*: A large-scale clinical EEG dataset comprising 16,986 recording sessions from 10,874 subjects with heterogeneous diagnoses. EEG signals were recorded using 20–31+ channels, predominantly at sampling rate between 250–512 Hz, and are linked with de-identified clinical reports.
- HBN-EEG (Healthy Brain Network) *(Shirazi et al., 2024)*: An developmental EEG dataset from 2,782 participants aged 5–21. Each participant underwent approximately 60 minutes of high-density (128-channel) EEG and eye-tracking recordings across six distinct tasks, including resting-state and movie watching.
- NCHSDB (Nationwide Children’s Hospital Sleep DataBank) *(Lee et al., 2022)*: An pediatric sleep EEG dataset of 3,673 patients. Each record includes 8–12 hours of EEG data (26–29 channels, sampled at 256–512 Hz) manually scored for sleep stages and events. While the dataset contains multimodal PSG signals (EOG, EMG, ECG, respiration, etc.), we used only the EEG channels.
- PEERS (Penn Electrophysiology of Encoding and Retrieval Study) *(Kahana et al., 2023)*: An EEG dataset from 364 subjects who participated in multiple sessions of free recall, recognitionm and distractor tasks. EEG signals were recorded with 125 channels at 500 Hz sampling rate.

### F.2 Finetuning Dataset Description

The following datasets were utilized for the downstream evaluation of our DIVER models, comprising a comprehensive set of benchmarks across both iEEG and EEG modalities. An overview of the dataset specifications and task definitions is provided in Table 4.

Neuroprobe Neuroprobe *(Zahorodnii et al., 2025)* is a large scale iEEG benchmarks with naturalistic labels during movie watching. 10 subjects watch 25 movies, age from 6 to 19. There are 3 types of evaluation in neuroprobe; single subject-single movie (WithinSession) (splits within the movies), single subject-different movie(CrossSession) (splits within subjects), different subject-different movie(CrossSubject). We evaluated the model in WithinSession. Additionally, Neuroprobe provides an option to subset subjects and trials. We used the LITE option (default configuration), which includes two movies per subject and a total of six subjects. Detailed description of each task is provided below (adapted from *(Zahorodnii et al., 2025)*:

1. frame_brightness (visual): The mean brightness computed as the average HSV value over all pixels. Low (percentiles 0%-25%) vs High (75%-100%)
2. global_flow (visual): A camera motion proxy. The maximal average dense optical flow vector magnitude. Same as above.
3. local_flow (visual): A large displacement proxy. The maximal optical flow vector magnitude. Same as above.
4. face_num (visual): The maximum number of faces per frame during the word. 0, or $\geq$ 1.
5. volume (auditory): Average root mean squared watts of the audio. Low (0%-25%) vs High (75%-100%).
6. pitch (auditory): Average pitch of the audio. Same as above.
7. delta_volume (auditory): The difference in average RMS of the 500 ms windows pre- and post-word onset. Same as above.

---

8. speech (language): Whether any speech is present in the given time interval.
9. onset (language): Whether a new sentence starts in the interval, or there is no speech at all.
10. gpt2_surprisal (language): Negative-log transformed GPT-2 word probability (given preceding 20s of language context). Low (0%-25%) vs High (75%-100%).
11. word_length (language): Word length (ms). Same as above.
12. word_gap (language): Difference between previous word offset and current word onset (ms). Same as above.
13. word_index (language): The word index in its context sentence. The first word in the sentence (0), or other (1).
14. word_head_pos (language): The relative position (left/right) of the word’s dependency tree head.
15. word_part_speech (language): The word Universal Part-of-Speech (UPOS) tag. Verb (0), or other (1).

EEG tasks We evaluate our model on five publicly available EEG datasets spanning emotion recognition, motor imagery, mental workload tasks and mental disorder diagnosis and event type classification. We adopted the preprocessing procedure from CBraMod with minimal modifications; specifically, the resampling rate was adjusted to 500 Hz while all other steps remained consistent with the original pipeline. Detailed description of each dataset is provided below:

1. FACED *(Chen et al., 2023)*: A large-scale EEG corpus for emotion recognition. It contains recordings from 123 subjects with 32-channel EEG while watching 28 emotion-eliciting video clips. Emotions are categorized into 9 discrete classes: amusement, inspiration, joy, tenderness, anger, fear, disgust, sadness, and neutral. We evaluated the model with the 9-class emotion classification task.
2. PhysioNet-MI *(Goldberger et al., 2000; Schalk et al., 2004)*: An EEG dataset for motor imagery–based BCI tasks. It includes recordings from 109 subjects using a 64-channel 10–20 montage and contains four motor imagery classes: left fist, right fist, both fists, and both feet.
3. MentalArithmetic *(Zyma et al., 2019)*: An EEG dataset for mental stress detection. It contains recordings from 36 subjects using 20 channels. We used 19 channels in total, excluding 1 reference channel. The dataset consists of recordings during mental arithmetic tasks under two conditions: with mental stress and without mental stress.
4. Mumtaz2016 *(Mumtaz, 2016)*: A clinical EEG dataset designed to distinguish major depressive disorder patients from healthy individuals. This dataset comprises 64 subjects (34 with MDD, 30 healthy controls), with signals acquired from 19 scalp locations following the standard 10-20 electrode placement system. We employed the resting-state conditions for binary MDD classification.
5. TUEV *(Obeid and Picone, 2016)*: An EEG dataset for event type classification in clinical neurophysiology. This corpus provides annotated EEG segments categorized into six classes: spike and sharp wave (SPSW), generalized periodic epileptiform discharges (GPED), periodic lateralized epileptiform discharges (PLED), eye movement (EYEM), artifact (ARTF), and background (BCKG). We evaluated the model on this 6-class event classification task.

### F.3 QAQC and preprocessing

All data underwent quality assessment and control (QAQC) and preprocessing with a philosophy of minimal intervention to retain as much original signal information as possible. For QAQC, we normalized signals by dividing EEG by 100 µV and iEEG by 200 µV (the latter accounting for larger amplitudes in intracranial recordings). While *Jiang et al. (2024)* applied normalization without QAQC and *Wang et al. (2024c)* removed entire segments if even one timepoint exceeded 100 µV, we adopted a more conservative clipping approach to prevent data loss. We clipped amplitude values exceeding these normalization thresholds, only discarding electrodes when more than 3.33% of samples required clipping and removing whole segments when more than 50% of channels were

---

compromised. This conservative strategy enabled us to preserve substantially more usable data: whereas CBRaMod's preprocessing yielded approximately 174.7k channel-hours of pretraining data on the same TUEG dataset (refer to Appendix Table 28), our QAQC pipeline retained 422k channel-hours, a  $2.4 \times$  increase.

For preprocessing, we applied minimal filtering: a high-pass filter (0.5 Hz for private iEEG, 0.3 Hz for other datasets) to remove low-frequency drift, a 60 Hz notch filter for power line noise suppression, and no low-pass filtering to preserve high-frequency components. All datasets were resampled to 500 Hz and segmented into 30-second non-overlapping windows.

# G COMPARISON WITH EXISTING EEG/EEG FOUNDATION MODELS

A direct comparison of training epochs for prior EEG/iEEG foundation models is misleading due to varying dataset sizes (Table 27). To enable a fair assessment, we introduce the "Scaled Epochs on Our Data" metric. This normalizes the total data processed during training (channel-hours  $\times$  epochs) into an equivalent number of epochs on our dataset, allowing for a direct comparison of training epochs across all prior models and our own. For entries in Table 27 that use estimated values (marked with *), the corresponding estimation procedures are documented in Table 28.

Table 27: Comparison of prior EEG/iEEG foundation models

| Models | Modality | Model Size (Parameters) | Volume (Channel-hours) | Training Epochs | Scaled Epochs on Our Dataa |
| --- | --- | --- | --- | --- | --- |
| BENDR (Kostas et al., 2021) | EEG | 155M* | N/A | 1 | N/A |
| BrainBERT (Wang et al., 2023) | SEEG | 43M* | 4.5k | 39* | 0.5 |
| Brant (Zhang et al., 2023) | SEEG | 505.68M | 281k | 32* | 25.6 |
| BIOT (Yang et al., 2023) | EEG | 3.3M | 312k | 100 | 88.6 |
| Neuro-GPT (Cui et al., 2024) | EEG | 90M* | 541k | 135 | 207.6 |
| LaBraM (Jiang et al., 2024) | EEG | 5.8M, 46M, 369M 0.4M, 0.5M, 1.6M, | 76.8–83.7k | 50 | 11.4 |
| EEGPT (Wang et al., 2024b) | EEG | 6.4M, 19M, 25M, 76M, 101M 0.1M, 0.4M, 0.8M, | 11.1k* | 200 | 6.8 |
| CBraMod (Wang et al., 2024c) | EEG | 1.2M, 1.5M, 2M, 3M, 4M | 175.7k* | 40 | 20 |
| Ours (DIVERI) | ECoG+SEEG | 12.72M–1.83B | 352k | 64 |  |
| Ours (DIVERIE) | ECoG+SEEG+EEG | 13.03–812.85M | 1,662k | 1 |  |

a This metric normalizes the total training compute across studies to represent the equivalent number of training compute on our dataset. It is calculated as: Scaled Epochs = Source Dataset (channel-hours) × Source Epochs where our iEEG dataset = 352,035 channel-hours. Our Dataset (channel-hours)  ${}^{ * }$  Values marked with an asterisk are our estimates,as they were not explicitly stated in the source paper; the estimation methods are summarized in Table 28.

---

Table 28: Estimation of model and training specifications. We detail the assumptions and calculations used to derive model size, training epochs, and data volume (channel-hours) for prior models. Bold values represent the final estimates derived from the reported configurations.

| Models | Parameters | Est. Value | Justification / Method |
| --- | --- | --- | --- |
| BENDR | Model Size | 155M | Assume d=1536, r=3076, L=8. Decompose P = Pconv + Ppos + Pin + LPt. Here Pconv = (3·20·512+512) + 5(2·512·512+512) + 6(2·512), Ppos = 25·(512/16)·512 + 512, Pin = 512·1536 + 1536, and Pt ≈ 4d2+2dr+r+9d. Numerically ≈ 155M. |
| BrainBERT | Model Size | 43M | Assume d=768, r=4d=3072, L=6. Per layer Pf ≈ 4d2+2dr+r+9d ≈ 7.08M. Transformer total LPt ≈ 42.5M. Add 2-layer head 768→768→40: Phead ≈ 0.6M. Hence P ≈ 42.5+0.6 ≈ 43M. |
|  | Training Epochs | 39 | Total hours H=4,551, segment τ=5s. Nsamp = B-9800 = 4551g1600 = 3,276,720. Steps/epoch ≈ Nsamp/256 ≈ 12,800. With U=500,000 updates: epochs ≈ U/12,800 ≈ 39. |
| Brant | Training Epochs | 32 | Use epochs = U(B·A)/Nsamp. Reported U=750,000, B=16, A=4 ⇒ 48M sample-passes. Dataset size Nsamp ≈ 1.5M ⇒ epochs ≈ 48/1.5 ≈ 32. |
| Neuro-GPT | Model Size | 90M | Assume GPT-2-like decoder with d=1024, r=4096, L=6. Per layer Pf ≈ 12.6M ⇒ PGPT = LPt ≈ 75.6M. Adding EEG encoder and a linear projector (P0) yields P = P0 + PGPT ≈ 90M (projector ~ 1.1M; remainder in encoder). |
| EEGPT | Channel-hours | 11.1k | Apply ch-hr = (# trials) (#ch) (ε)/3600 per dataset and sum: PhysioMI ≈ 107, HGD ≈ 1,991, TSU ≈ 597, SEED ≈ 116, M3CV ≈ 8,267 ⇒ total ≈ 11,078 ch-hr. |
| CBAMod | Channel-hours | 175.7k | Common channels ε=19, non-overlapping segment τ=30s, kept segments N=1,109,545: ch-hr = C-B-ε/3600 = P0 + 109,545·30/3600 ≈ 175.7k. |

Conventions. Hidden size  $d$ , FFN expansion  $r$ , layers  $L$ , per-layer parameters  $P_{\ell}$ , total parameters  $P$ , segment length  $\tau$  (seconds), minibatch  $B$ , gradient accumulation  $A$ , updates  $U$ , number of samples  $N_{\mathrm{samp}}$ . Transformer block (per layer):  $P_{\ell} = \underbrace{4d^{2}}_{\mathrm{Q,K,V,Out}} + \underbrace{2dr + r}_{\mathrm{FFN}} + \underbrace{9d}_{\mathrm{FPN}} \approx 4d^{2} + 2dr + r + 9d$ . Total params:  $P = P_{0} + L P_{\ell}$  (non-Transformer parts  $P_{0}$  separated when needed). Epochs: epochs =  $\frac{U(B \cdot A)}{N_{\mathrm{samp}}}$ , with  $N_{\mathrm{samp}} = \frac{(\mathrm{hours} \cdot 3600)}{\tau}$ . Channel-hours: ch-hr =  $\sum \frac{(\# \mathrm{trials}) \cdot (\# \mathrm{channels}) \cdot (\mathrm{sounds})}{3600}$ .
