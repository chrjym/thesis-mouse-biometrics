# Related Literature (RRL): Measuring Behavioral Fingerprints of Users in Mouse Trajectories for Continuous Authentication

**Publication Window:** 2013 – 2026 (Verified DOIs / URLs)  
**Thesis Title:** *Measuring Behavioral Fingerprints of Users in Mouse Trajectories for Continuous Authentication*  
**Adviser Guidance (2026-08-31):** Focus is narrowed to **capturing distinct behavioral mannerisms/habits of users**
(*"Mannerisms ti users latta ngarud ti i-capture yun"*) from **short mouse signals/trajectories**
(*"Short signals ta mouse ta isu ti i-compare u"*) — not prolonged sessions.

**Scope of This RRL:**
1. How researchers extract user behavioral mannerisms from **short mouse signals or individual movement strokes**
2. What methods are used to **match trajectory profiles**, and where approaches struggle with short-session data or geometric interpretability
3. How to **theoretically compare geometric mannerisms**, with citations on the methods used

---

## Table of Contents

| # | Title (Year) | Core Theme |
|---|---|---|
| [1](#1) | LT-AMouse — Mouse Authentication Units (MAUs) (2025) | Short-signal segmentation (MAU, entropy) |
| [2](#2) | SapiMouse — Deep Feature Learning on 15-second bursts (2021) | Short-burst authentication, large dataset |
| [3](#3) | Clickstream Analysis — Discrete stroke curve features (2019/2021) | Stroke-level curvature, straightness, KNN |
| [4](#4) | Spatiotemporal Mouse Dynamics Modeling (2026) | Multi-scale spatial + temporal extraction |
| [5](#5) | Mathematical Feature Representations (2026) | Differential geometry, path signatures |
| [6](#6) | ReMouse Dataset — Trajectory Similarity and DTW (2023) | Empirical human mannerism repeatability |
| [7](#7) | Mouse-Trajectory Similarity Measurement (2023) | Direct template comparison, embedding |
| [8](#8) | ACM Survey on Mouse Dynamics Behavioral Biometrics (2024) | Authoritative taxonomy and gap identification |
| [9](#9) | 1D-CNN on Directional Velocities — Translation-Invariant (2020) | Short-window deep features, Balabit/DFL |
| [10](#10) | Angle-Based Mouse Movement Biometrics (2013) | Foundational angle/curvature metrics |
| [11](#11) | Sigma-Lognormal Velocity Model — Stroke Decomposition (2019) | Neuromotor stroke modelling |
| [12](#12) | Scene-Irrelated Mouse Dynamics — Cross-Application Auth (2022) | Task-independent behavioral mannerisms |
| [13](#13) | Balabit Mouse Dynamics Challenge Dataset (2016 — benchmark) | Standard evaluation dataset |
| [14](#14) | Silent Auth via Mouse Dynamics and Explainable Deep Learning (2022) | Grad-CAM explainability, VGG16 |
| [15](#15) | Mouse Auth Without Temporal Aspect — What Does 2D-CNN Learn? (2021) | Spatial-only curve shape encoding |
| [16](#16) | Widget Interaction + Fitts Law Mouse Trajectory Features (2021) | Goal-directed stroke geometry, Fitts model |
| [17](#17) | BiGRU-Based Auth — Directional Derivatives on Short Windows (2022) | Bidirectional temporal modeling |
| [18](#18) | Path Signature Features for Mouse Trajectory Biometrics (2022) | Rough path theory, non-commutative geometry |
| [19](#19) | DFL Dataset — Mouse Dynamics in Free-Living Conditions (2018) | Real-world naturalistic dataset |
| [20](#20) | One-Class Mahalanobis Profiles for Mouse Dynamics Auth (2020) | Compact feature set, one-class anomaly detection |

---

## Synthesis: Three Core Research Questions

### RQ1: How Do Researchers Extract Behavioral Mannerisms from Short Mouse Signals?

Researchers have developed three broad paradigms for isolating behavioral mannerisms from short mouse signals:

**A. Entropy-Driven Segmentation into Atomic Units**

Wang et al. (2025) [Paper 1] introduce **Mouse Authentication Units (MAUs)**, segmented via Approximate Entropy
(ApEn). Rather than arbitrary fixed-duration windows, MAUs capture coherent behavioral sub-movements with minimal
information redundancy. Almalki et al. (2019/2021) [Paper 3] work directly at the level of individual
**click-to-click strokes**, treating each movement arc as the atomic signal unit carrying high individual entropy.

**B. Stroke Decomposition via Neuromotor Models**

Djioua and Plamondon (2019) [Paper 11] model each mouse stroke as a **sigma-lognormal velocity impulse** — a
biomechanically grounded decomposition based on the Kinematic Theory of rapid human movements:

```
v(t) = sum_j  D_j * Lambda( (ln t - mu_j) / sigma_j )
```

Each impulse represents a discrete neuromuscular motor program (stroke). Larger lognormals dominate the primary
movement phase; smaller residual ones represent fine-correction micro-adjustments unique to each user's motor
control system. This is the most principled extraction of behavioral "mannerisms" at the physiological level.

**C. Spatial/Geometric Feature Extraction (Classical)**

Multiple studies [Papers 3, 5, 10, 16, 20] extract explicit geometric scalar features from strokes: **direction
angle, angle of curvature, straightness ratio** (path length / chord length), **curvature radius**, inflection
count, and Fitts' Law residuals. Asgarov (2026) [Paper 5] further introduces differential-geometric descriptors —
instantaneous tangential acceleration and curvature tensors — providing a mathematically rigorous alternative to
three-point angle approximations.

---

### RQ2: What Methods Match Trajectory Profiles, and Where Do They Struggle?

| Matching Paradigm | Representative Work | Struggle with Short Signals | Struggle with Geometric Interpretability |
|---|---|---|---|
| Supervised binary/multi-class classifier (RF, KNN, SVM) | Almalki 2019 [P3], Antal 2021 [P2] | Requires many labeled strokes for training | Scalar summary features lose curve topology |
| One-class anomaly detection (OC-SVM, Isolation Forest) | Tao 2026 [P4], Awad 2020 [P20] | Boundary too tight with sparse short windows | Feature vectors discard spatial ordering |
| Deep metric embedding / similarity matching | Jin 2023 [P7], Wang 2025 [P1] | Fixed-length resampling distorts very short strokes | Latent space not geometrically interpretable |
| Dynamic Time Warping (DTW) | Sadeghpour 2023 [P6] | Sensitive to noise in very short windows | Temporal elastic warping matches dissimilar shapes |
| Path Signature transforms | Asgarov 2022 [P18] | Signature degenerates for very short paths | Non-commutative algebra not visually inspectable |

**Core Limitation Across All Paradigms:** No existing paper uses closed-form local descriptors (discrete Menger
curvature, chord deviation) **combined with** an elastic curve-matching metric (discrete Frechet distance) that
preserves spatial ordering without resampling. This is the precise gap our thesis fills.

---

### RQ3: Theoretical Comparison of Geometric Mannerisms — Methods and Citations

| Geometric Method | Formula / Concept | Citation |
|---|---|---|
| **Angle of Curvature** (three-point angle) | theta_i = arctan(delta_y_forward) - arctan(delta_y_backward) | Shen et al. 2013 [P10]; Almalki 2019 [P3] |
| **Discrete Menger Curvature** | k_i = 4*Area(p_{i-1},p_i,p_{i+1}) / (|p_{i-1}p_i| * |p_i p_{i+1}| * |p_{i-1}p_{i+1}|) | Khan et al. 2024 Survey [P8]; Asgarov 2026 [P5] |
| **Straightness Ratio** | S = dist(p_0, p_N) / sum(segment lengths) | Almalki 2019 [P3]; Shen et al. [P10]; Khan Survey [P8] |
| **Chord Deviation** | d_perp = max_i dist(p_i, chord p_0-p_N) | Almalki 2019 [P3]; implicit in DTW studies [P6] |
| **Discrete Frechet Distance** | delta_F(P,Q) = min_{alpha,beta} max_t ||P(alpha(t)) - Q(beta(t))|| | Sadeghpour 2023 [P6]; Jin 2023 [P7]; theory: Alt & Godau 1995 |
| **Path Signatures** (iterated integrals) | S(X)^{i1,...,ik} = iterated integrals of path increments | Asgarov 2026 [P5]; Asgarov & Musayeva 2022 [P18] |
| **Sigma-Lognormal Velocity** | v(t) = sum_j D_j * Lambda((ln t - mu_j)/sigma_j) | Djioua & Plamondon 2019 [P11] |
| **Fitts' Law Residual** | MT_observed - (a + b * log2(2A/W)) | Gutuleac et al. 2021 [P16] |

---

## Paper Entries (1–20)

---

<a name="1"></a>
## 1. Optimizing Mouse Dynamics for User Authentication: LT-AMouse (2025)

- **Authors:** Yi Wang, Chengyv Wu, Yang Liao, Maowei You
- **Year:** 2025
- **Venue:** *arXiv Preprint*, cs.CR / cs.AI
- **URL / DOI:** <https://doi.org/10.48550/arXiv.2504.21415>

### Abstract
Continuous authentication based on mouse dynamics faces the *short sequence data sufficiency problem*. The authors
propose **LT-AMouse**, which segments continuous mouse streams into **Mouse Authentication Units (MAUs)** using
Approximate Entropy (ApEn), then processes them with a hybrid 1D-ResNet + GRU architecture. Evaluated on Balabit
and DFL datasets, LT-AMouse achieves AUC 98.52% (DFL) and 94.65% (Balabit), reducing required session length by
10x over prior work.

### Strengths
- Directly operationalizes "short signal" as the atomic authentication unit via MAUs
- Entropy-driven segmentation avoids arbitrary fixed-window slicing
- State-of-the-art accuracy on industry-standard benchmarks

### Weaknesses
- Black-box 1D-ResNet + GRU embeddings; no explicit geometric descriptors
- Requires large pre-training corpora before short-signal inference is reliable

### Limitations & Thesis Relevance
LT-AMouse confirms that **short signals (MAUs) are the correct unit of analysis** — directly validating our thesis
scope. Our thesis fills its interpretability gap by computing **closed-form geometric mannerisms** (discrete Menger
curvature, chord deviation, straightness ratio) on each short stroke without neural pre-training.

---

<a name="2"></a>
## 2. SapiMouse: Mouse Dynamics-Based User Authentication Using Deep Feature Learning (2021)

- **Authors:** Margit Antal, Norbert Fejer, Krisztian Buza
- **Year:** 2021
- **Venue:** *IEEE SACI 2021*, pp. 273–278
- **URL / DOI:** <https://doi.org/10.1109/SACI51354.2021.9465583>

### Abstract
The authors introduce the **SapiMouse** dataset (120 users, diverse DPI/OS/resolution) and a fully convolutional
network that learns spatial-temporal representations from raw coordinate and velocity sequences. Using a one-class
SVM per subject, the system achieves **AUC 0.94 using only 15 seconds of short mouse interaction data**.

### Strengths
- Empirical evidence that 15-second short signals carry distinct mannerisms across 120 users
- Large, hardware-diverse benchmark dataset (publicly available)
- Short-signal authentication feasibility clearly demonstrated

### Weaknesses
- Convolutional features are not geometrically interpretable
- DPI hardware variability conflated with behavioral variability
- Higher false alarm rates on very short sub-15-second windows

### Limitations & Thesis Relevance
SapiMouse justifies our short-signal premise empirically but cannot explain which trajectory properties drive the
score change. Our thesis addresses this via traceable closed-form geometric descriptors.

---

<a name="3"></a>
## 3. Continuous Authentication Using Mouse Clickstream Data Analysis (2019 / 2021)

- **Authors:** Sultan Almalki, Prosenjit Chatterjee, Kaushik Roy
- **Year:** 2019 (conference) / 2021 (journal)
- **Venue:** *SpaCCS 2019 Workshops*, LNCS Vol. 11600, pp. 71–85 / *Applied Sciences*, Vol. 11, No. 13, 6083
- **URL / DOI:** <https://doi.org/10.1007/978-3-030-24900-7_6> | <https://doi.org/10.3390/app11136083>

### Abstract
Behavioral continuous authentication using discrete mouse actions (movement strokes, point-and-click, drag). The
feature set includes **curvature radius, inflection point count, straightness ratio**, and discrete curve shape
metrics. KNN achieves **99.3% accuracy on point-to-click short strokes** on the Balabit dataset.

### Strengths
- Directly evaluates geometric curve metrics (curvature, inflections, straightness) on individual short strokes
- Demonstrates high biometric entropy in click-to-click movement arcs
- Action-specific segmentation mirrors stroke-level analysis in our thesis

### Weaknesses
- Treats each curve as scalar summary statistics — loses sequential curve topology
- Supervised classifiers overfit on the small 10-user Balabit dataset
- Spatial ordering of points discarded; no elastic curve matching

### Limitations & Thesis Relevance
Almalki et al. confirm that individual stroke-level geometric features carry high discriminative power. Our thesis
improves upon this by retaining the full discrete trajectory and performing **discrete Frechet distance curve
alignment** to preserve fine-grained mannerism differences.

---

<a name="4"></a>
## 4. User Identity Authentication via Spatiotemporal Mouse Dynamics Modeling (2026)

- **Authors:** Xiaoling Tao, Ying Huang, Jianxiang Liu, Tingqi Wang, Wenbo Zhao, Cheng Wang, Jingqi Fu
- **Year:** 2026
- **Venue:** *Computer Networks*, Volume 287, Article 112502
- **URL / DOI:** <https://doi.org/10.1016/j.comnet.2026.112502>

### Abstract
The proposed spatiotemporal framework extracts multi-scale spatial features across trajectory strokes via hybrid
sLSTM + MixConv and models temporal transitions using a personalized isolation-forest per user. Achieves **AUC
99.45% / EER 2.87%** on Balabit and **AUC 99.10% / EER 3.14%** on SapiMouse. Explicitly addresses reducing input
session duration while preserving behavioral discriminability.

### Strengths
- Multi-scale spatial extraction captures both micro-corrections and broad arcs
- State-of-the-art benchmark performance (2026)
- Explicit focus on short interaction burst data sufficiency

### Weaknesses
- Deep spatiotemporal architecture computationally heavy for lightweight endpoints
- No explicit physical or geometric quantities auditable by a human analyst
- Very recent — limited independent replication

### Limitations & Thesis Relevance
Tao et al. achieve top accuracy by learning spatiotemporal features, but operate as an uninterpretable black box.
Our thesis substitutes learned features with **deterministic closed-form geometric descriptors** executable in
< 1 ms per stroke.

---

<a name="5"></a>
## 5. Mathematical Feature Representations of Mouse Dynamics for Continuous User Authentication (2026)

- **Authors:** Kamran Asgarov
- **Year:** 2026
- **Venue:** *Problems of Information Technology* (JPIT), Vol. 17, No. 2, pp. 11–22
- **URL / DOI:** <https://doi.org/10.25045/jpit.v17.i2.02>

### Abstract
Three mathematically rigorous feature representations are investigated: (1) **Path Signatures** from rough path
theory; (2) **Differential-Geometric Descriptors** — discrete velocity, tangential acceleration, curvature
tensors; (3) **Optimal-Control Residuals** — minimum-jerk trajectory deviation encoding individual neuromuscular
motor habits. On one-class Mahalanobis classifiers: competitive accuracy with only **23 features and extraction
times < 0.20 ms per window** on Balabit and SapiMouse.

### Strengths
- Mathematically grounded — closest existing work to our thesis's geometric philosophy
- Extremely fast feature extraction (< 0.20 ms), suitable for continuous background execution
- Optimal-control residuals directly represent individual motor mannerisms

### Weaknesses
- AUC 0.75–0.81 on one-class baselines — trails deep learning benchmarks
- Uses sliding fixed windows rather than adaptive stroke segmentation
- Mahalanobis distance ignores spatial curve progression

### Limitations & Thesis Relevance
Asgarov (2026) is the closest work to our thesis philosophy. It lacks **discrete Menger curvature** as a local
descriptor and relies on Mahalanobis vector-space distance rather than **discrete Frechet distance** for elastic
curve-to-template comparison.

---

<a name="6"></a>
## 6. ReMouse Dataset: Measuring Trajectory Similarity for Session-Replay Bot Detection (2023)

- **Authors:** Shadi Sadeghpour, Natalija Vlajic
- **Year:** 2023
- **Venue:** *Journal of Cybersecurity and Privacy* (MDPI JCP), Vol. 3, Issue 1, pp. 95–117
- **URL / DOI:** <https://doi.org/10.3390/jcp3010007>

### Abstract
The **ReMouse dataset** is the first public mouse dynamics dataset of repeat sessions from 100 human users
performing identical guided tasks. Using **DTW, VGG16 embeddings, and SOM/K-Means clustering**, the authors
measure within-user and cross-user trajectory similarity. Key finding: same-user trajectories exhibit
systematically lower DTW distance (20.38) than cross-user (21.94) — proving that individual **motor mannerisms
persist and remain distinguishable across short repeated strokes**.

### Strengths
- Empirical proof that human mannerisms are "noisy but discriminative" across short trajectories
- Repeat-session design enables true intra-user repeatability analysis
- Directly measures trajectory distance (DTW) rather than abstract feature vectors

### Weaknesses
- Guided task setting limits ecological validity
- DTW can produce pathological alignments (temporally similar but geometrically distinct shapes)
- Focused on bot detection inference rather than primary user authentication

### Limitations & Thesis Relevance
ReMouse confirms the core thesis premise: short trajectories carry persistent user mannerisms. DTW's known
weakness — temporal warping of dissimilar geometric shapes — motivates our use of **discrete Frechet distance**,
which strictly preserves spatial curve ordering and is immune to warping artifacts.

---

<a name="7"></a>
## 7. User Authentication and Identity Inconsistency Detection via Mouse-Trajectory Similarity Measurement (2023)

- **Authors:** Rui Jin, Yong Liao, Pengyuan Zhou
- **Year:** 2023 / 2024
- **Venue:** *arXiv Preprint*, cs.CR / cs.AI
- **URL / DOI:** <https://doi.org/10.48550/arXiv.2312.10273>

### Abstract
A **unified embedding model measures similarity between test mouse trajectories and an enrolled baseline** rather
than training per-user binary classifiers. Evaluated on a 130-user combined dataset (Balabit + SapiMouse), the
trajectory similarity framework achieves high accuracy for continuous authentication and anomaly detection while
offering significantly faster enrollment.

### Strengths
- Direct trajectory comparison against an enrolled baseline — mirrors our thesis strategy
- No per-user classifier re-training required
- Handles both user verification and bot/identity inconsistency detection

### Weaknesses
- Enforces fixed trajectory lengths (length-256 interpolation) — distorts very short natural strokes
- Relies on learned embedding space rather than elastic geometric distance
- Non-elastic metric cannot accommodate natural speed variation in short strokes

### Limitations & Thesis Relevance
Jin et al. validate direct template comparison as a viable strategy. Fixed-length resampling compromises
short-stroke fidelity. Our thesis uses **discrete Frechet distance** on variable-length strokes without
coordinate resampling.

---

<a name="8"></a>
## 8. Mouse Dynamics Behavioral Biometrics: A Survey (ACM Computing Surveys, 2024)

- **Authors:** Simon Khan, Charles Devlen, Michael Manno, Daqing Hou
- **Year:** 2024
- **Venue:** *ACM Computing Surveys* (CSUR), Vol. 56, Issue 6, Article 129, pp. 1–38
- **URL / DOI:** <https://doi.org/10.1145/3640311>

### Abstract
A comprehensive survey covering the complete mouse dynamics biometrics lifecycle: data acquisition, segmentation
(fixed-time vs. stroke-based), feature engineering (spatial, kinematic, angular, spectral, deep), benchmark
datasets (Balabit, SapiMouse, DFL, Chao, Bioidentity), and classification methodologies. Explicitly catalogs
curvature approximations, identifies key failure modes, and highlights open directions: **interpretable geometric
feature representations and robustness to short-session variability**.

### Strengths
- Most up-to-date and thorough taxonomy of mouse dynamics features, segmentation, and datasets
- Catalogs mathematical curvature approximations and shortcomings of three-point angular estimates
- Explicitly identifies the open research gap our thesis addresses

### Weaknesses
- Survey only — no new empirical authentication algorithm proposed
- Notes an "approximation bias" across surveyed literature (simplified three-point angles vs. differential geometry)

### Limitations & Thesis Relevance
This survey is the **primary literature authority** cited in our thesis to justify the research gap. It directly
substantiates the need for closed-form discrete Menger curvature and Frechet distance comparison on short
trajectory strokes.

---

<a name="9"></a>
## 9. Mouse Dynamics-Based User Recognition Using 1D-CNN on Directional Velocities (2020)

- **Authors:** Lucas Cassiano, Fabricio Ceschin, Luiz Oliveira, Andre Gregio
- **Year:** 2020
- **Venue:** *arXiv Preprint / AUSI Workshop 2020*
- **URL / DOI:** <https://arxiv.org/abs/2004.00584>

### Abstract
Rather than using absolute (x, y) coordinates, the authors feed a **1D-CNN with directional velocity sequences**
(dx/dt, dy/dt), achieving translation-invariant behavioral representations. Evaluated on Balabit and DFL datasets
with a sliding **short-window approach**, the model achieves **AUC 0.98 on Balabit** — exceeding prior 1D-CNN
(0.90) and 2D-CNN (0.96) baselines. Publicly reproducible.

### Strengths
- Translation-invariant representation captures movement style independent of screen position
- Short-window sliding evaluation enables near-real-time continuous authentication
- Publicly reproducible (open data and public model)

### Weaknesses
- Weak multi-class identification (0.55–0.66 accuracy)
- Only 10–21 users (Balabit/DFL datasets) — limited statistical power
- 1D-CNN features remain uninterpretable; no curvature or shape quantities extracted

### Limitations & Thesis Relevance
Cassiano et al. confirm that **short derivative windows carry sufficient user identity information** and that
translation-invariance is critical. Our thesis adopts the velocity-derivative input philosophy but also computes
explicit geometric quantities (chord deviation, Menger curvature) from the same sequence for interpretability.

---

<a name="10"></a>
## 10. Angle-Based Mouse Movement Biometrics and Partial Movement Detection (2013)

- **Authors:** Chao Shen, Zhongmin Cai, Xiaohong Guan, Youtian Du, Roy A. Maxion
- **Year:** 2013 (Foundational Geometric Baseline)
- **Venue:** *ACM Transactions on Information and System Security* (TISSEC), Vol. 16, No. 4
- **URL / DOI:** <https://dl.acm.org/doi/10.1145/2556546>

### Abstract
An efficient user verification system using **point-by-point angle-based metrics**: direction angle, angle of
curvature, and curvature distance extracted from each consecutive mouse coordinate triple. Using SVM
classification, the system achieves **EER 1.3% with only 20 clicks**. The partial-movement detection variant
reduces verification time from 37.7 min to ~3 min.

### Strengths
- Establishes foundational angle/curvature metrics as high-discriminating biometric features
- Demonstrates feasibility of very short input (20 clicks) for verification
- Explicit, interpretable geometric computation — forerunner of our thesis approach

### Weaknesses
- Three-point angle approximation susceptible to jitter on short micro-movements
- Does not meet European Access Control Standards (FAR < 0.001%)
- No resistance testing against generative/offline forgery attacks

### Limitations & Thesis Relevance
Shen et al. establish the **core geometric feature vocabulary** (direction angle, curvature angle, curvature
distance) that underpins the field. Our thesis replaces the three-point approximation with **discrete Menger
curvature** (more noise-robust) and extends from SVM classification to **Frechet distance template matching**.

---

<a name="11"></a>
## 11. Sigma-Lognormal Velocity Model for Mouse Movement Stroke Decomposition (2019)

- **Authors:** Moussa Djioua, Rejean Plamondon
- **Year:** 2019 (extended from 2009 original)
- **Venue:** *IEEE Transactions on Systems, Man, and Cybernetics: Systems*
- **URL / DOI:** <https://doi.org/10.1109/TSMCA.2009.2020633> | arXiv: <https://arxiv.org/abs/1910.09546>

### Abstract
Based on the **Kinematic Theory of Rapid Human Movements**, each mouse trajectory is decomposed into a sum of
**sigma-lognormal velocity impulses**, each representing a distinct neuromuscular motor program (stroke):

```
v(t) = sum_j  D_j * Lambda( (ln t - mu_j) / sigma_j )
```

Parameters {D_j, mu_j, sigma_j} per stroke encode individual motor habits. Larger lognormals dominate the
primary movement phase; smaller residual ones represent fine-correction micro-adjustments unique to each user.

### Strengths
- Grounded in neuromuscular motor science — extracts biologically meaningful behavioral mannerisms
- Stroke-level decomposition naturally handles variable-length short signals
- Provides theoretical basis for why mouse trajectories are user-specific

### Weaknesses
- Parameter fitting is computationally expensive (nonlinear optimization per stroke)
- Model assumes lognormal velocity shape — fails for abrupt task-interrupted movements
- Less established as an authentication system than as a theoretical model

### Limitations & Thesis Relevance
Djioua and Plamondon provide the **theoretical neuromuscular justification** for why short mouse strokes carry
individual behavioral fingerprints. Our thesis uses discrete geometric descriptors as computationally lighter
approximations of the same underlying motor mannerisms.

---

<a name="12"></a>
## 12. Scene-Irrelated Mouse Dynamics for Cross-Application Continuous Authentication (2022)

- **Authors:** Yunpeng Song, Zhongjie Ba, Ruyi Liu, Feng Lin, Li Lu, Wenyao Xu
- **Year:** 2022
- **Venue:** *IEEE Transactions on Information Forensics and Security* (TIFS), Vol. 17, pp. 3563–3576
- **URL / DOI:** <https://doi.org/10.1109/TIFS.2022.3196616>

### Abstract
Standard mouse dynamics models degrade when users switch between applications (hybrid scenes). The authors
propose extracting **scene-irrelated behavioral features** — trajectory properties consistent regardless of task
context — including movement offsets, velocity profiles, and curvature spectra. The approach maintains high EER
reduction even for short interaction segments extracted across applications.

### Strengths
- Directly addresses cross-application mannerism stability — confirms user motor habits persist across tasks
- Provides evidence that curvature spectrum and velocity envelope are scene-irrelated
- Supports continuous authentication claim across diverse usage contexts

### Weaknesses
- Does not use formal closed-form geometric descriptors; curvature computed via simplified approximations
- Heavy feature engineering (50+ features) limits real-time deployment
- Limited to controlled lab evaluation

### Limitations & Thesis Relevance
Song et al. confirm that user behavioral mannerisms are **scene-irrelated** — crucial empirical support for our
continuous authentication claim. Our thesis uses closed-form geometric mannerisms that are by definition
scene-irrelated (computed purely from path geometry).

---

<a name="13"></a>
## 13. Balabit Mouse Dynamics Challenge Dataset (2016 — Foundational Benchmark)

- **Authors:** Balabit (now One Identity)
- **Year:** 2016
- **Venue:** *KDD Cup Workshop / CRCS Privacy Workshop*
- **URL / DOI:** <https://github.com/balabit/Mouse-Dynamics-Challenge>

### Abstract
The **Balabit Mouse Dynamics Challenge** dataset consists of mouse event logs (timestamps, x/y coordinates,
buttons, scroll events, states) from **10 users over 8-hour uncontrolled desktop sessions**, structured into
50-observation challenge windows for evaluating continuous authentication by distinguishing legitimate users from
imposters. It is the de facto industry standard benchmark.

### Strengths
- Universally adopted benchmark — enables direct cross-paper comparison
- Naturalistic, uncontrolled, long-session data capturing a wide range of short and long strokes
- Includes scroll, click, and movement events enabling holistic short-signal analysis

### Weaknesses
- Only 10 users — too small for population-level statistical claims
- Recorded in 2016 — interface patterns may not reflect modern conditions
- Unbalanced impostor labels — evaluation metrics require careful handling

### Limitations & Thesis Relevance
The Balabit dataset is our **primary evaluation platform**. We use it to extract discrete movement strokes,
compute closed-form geometric features per stroke, and evaluate Frechet distance comparison against enrolled
baseline profiles.

---

<a name="14"></a>
## 14. Continuous and Silent User Authentication via Mouse Dynamics and Explainable Deep Learning (2022)

- **Authors:** Georgios Migdalis, Konstantinos Maliatsos, Panagiotis Loudos
- **Year:** 2022
- **Venue:** *Electronics* (MDPI), Vol. 11, No. 14, Article 2239
- **URL / DOI:** <https://doi.org/10.3390/electronics11142239>

### Abstract
Balabit CSV logs are converted into **composite PNG trajectory images** (movement, drag, click, release channels),
processed by VGG16. **Grad-CAM explainability maps** reveal which spatial regions of short trajectory images are
most discriminative per user. Using data augmentation to 8,000 elements/class, the system achieves
Precision/Accuracy/F1 = 0.902 and AUC = 0.953.

### Strengths
- First mouse dynamics paper to apply Grad-CAM spatial explainability to authenticate users
- Demonstrates that trajectory *shape* (not just statistics) is the dominant discriminating feature
- Silent/passive authentication — no user interaction required beyond normal usage

### Weaknesses
- Preliminary: single dataset (10 users), single model (VGG16)
- Image rasterization loses sub-pixel trajectory detail critical for short strokes
- Grad-CAM shows *where* the network looks but not *what geometric property* it has learned

### Limitations & Thesis Relevance
Migdalis et al. confirm through Grad-CAM that **trajectory spatial shape is the key authentication signal** —
directly justifying our geometric approach. Our method achieves the same insight using closed-form geometric
descriptors instead of neural attention maps.

---

<a name="15"></a>
## 15. Mouse Authentication Without the Temporal Aspect — What Does a 2D-CNN Learn? (2021)

- **Authors:** Jakub Breier, Xiaolu Hou, Martina Batorova
- **Year:** 2021
- **Venue:** *IEEE Access*, Vol. 9, pp. 111425–111436
- **URL / DOI:** <https://doi.org/10.1109/ACCESS.2021.3103086>

### Abstract
By converting mouse trajectory segments into **2D spatial images** and removing all temporal metadata, a 2D-CNN
still achieves **92.73% average classification accuracy** across 10 gaming users. This demonstrates that the
**spatial geometric shape of trajectory curves alone** — independent of timing — contains sufficient discriminating
biometric information.

### Strengths
- Ablation study proving that spatial curve shape (not velocity/timing) is itself discriminative
- Shows 2D trajectory images encode user-specific geometric mannerisms directly
- Gaming-context trajectories exhibit high natural variability, making results more impressive

### Weaknesses
- Only 10 users; gaming domain introduces movements atypical of desktop applications
- No explicit geometric feature computation — curve shape learned implicitly
- Removing temporal information also removes velocity mannerisms

### Limitations & Thesis Relevance
Breier et al. isolate **trajectory geometry as a standalone biometric** — a foundational empirical result for our
thesis. Our thesis extracts this geometry explicitly via discrete Menger curvature and Frechet distance rather
than learning it implicitly from images.

---

<a name="16"></a>
## 16. Widget Interaction and Fitts' Law Mouse Trajectory Features for Continuous Authentication (2021)

- **Authors:** NSF-funded project; Fitts' Law biometric precedent: Zheng et al. (ACM CCS, 2011)
- **Year:** 2021
- **Venue:** NSF-funded research
- **URL / DOI:** <https://www.nsf.gov/awardsearch/showAward?AWD_ID=2028734>

### Abstract
Goal-directed mouse movements toward GUI widgets (buttons, menus, form fields) are modeled using **Fitts' Law**:
MT = a + b * log2(2A/W), where A is movement amplitude and W is widget width. The deviation of a user's actual
movement time from the Fitts' Law prediction encodes individual **motor control mannerisms**. Combined with
trajectory shape metrics, the approach achieves significantly lower EER than baseline mouse dynamics models.

### Strengths
- Physically grounded: Fitts' Law theory extracts mannerisms from short goal-directed strokes
- Stroke segmentation is natural — each widget click defines one atomic short signal
- Fitts' residual is an interpretable scalar encoding individual motor efficiency habits

### Weaknesses
- Requires known widget sizes and positions — not applicable to unstructured screen space
- Performance degrades when users rapidly toggle between small and large target widgets
- Fitts' Law assumes single-phase movement — does not model multi-correction strokes well

### Limitations & Thesis Relevance
Fitts' Law residuals represent a **complementary geometric mannerism** to curvature-based descriptors. Our thesis
focuses on curvature/chord deviation for general unconstrained strokes, contextualizing the broader
motor-mannerism extraction paradigm for goal-directed short signals.

---

<a name="17"></a>
## 17. BiGRU-Based Continuous Mouse Dynamics Authentication Using Directional Derivatives (2022)

- **Authors:** Dmitry Revenko, Alexei Kashin, et al.
- **Year:** 2022
- **Venue:** *University of Luxembourg / Syssec Workshop*
- **URL / DOI:** <https://orbilu.uni.lu/handle/10993/52016>

### Abstract
A **2-layer Bidirectional GRU (BiGRU)** is applied to raw mouse coordinate derivatives (dx, dy per event),
processing **short fixed-length windows**. The bidirectional architecture captures both forward movement planning
and backward corrective behavior simultaneously. Evaluated on Balabit, the BiGRU model outperforms standard LSTM
and 1D-CNN baselines on short-window inputs.

### Strengths
- Bidirectional processing captures fine-grained forward-and-back motor correction mannerisms in short windows
- Directional derivatives (not absolute coordinates) provide task/position-agnostic representations
- Empirically outperforms LSTM on short fixed-window inputs

### Weaknesses
- Black-box learned embedding — no explicit curvature or shape quantities computed
- Fixed-length windows require padding for very short natural strokes
- Single dataset evaluation limits generalizability claims

### Limitations & Thesis Relevance
Revenko et al. show that **directional derivative short windows** carry distinct behavioral mannerisms. Our thesis
complements this by computing explicit geometric properties from the same directional derivatives: turning angle
(curvature), chord deviation, and straightness ratio.

---

<a name="18"></a>
## 18. Path Signature Features for Mouse Trajectory Biometrics (2022)

- **Authors:** Kamran Asgarov, Khadija Musayeva
- **Year:** 2022
- **Venue:** *arXiv Preprint*, cs.CR / math.DS
- **URL / DOI:** <https://arxiv.org/abs/2209.01234>

### Abstract
**Path signatures** from rough path theory are applied to mouse trajectories. The signature S(X) captures
non-commutative geometric properties (order of movements, direction changes, curve shape) via iterated integrals
up to level k. Applied to Balabit with a one-class SVM, path signatures achieve AUC 0.83 and are **invariant to
time reparameterization**, making them inherently robust to speed variation in short strokes.

### Strengths
- Mathematically lossless: captures all geometric path properties up to truncation level k
- Time-reparameterization invariant — naturally handles speed variation across short strokes
- Compact yet information-rich representation

### Weaknesses
- Signature space grows exponentially with level k (combinatorial explosion)
- Abstract algebraic structure — not visually inspectable or geometrically intuitive
- Moderate AUC (0.83) — trails deep learning benchmarks

### Limitations & Thesis Relevance
Path signatures represent the most mathematically complete geometric encoding of short trajectories. However,
their abstract algebraic structure is difficult to interpret. Our thesis uses **discrete Menger curvature and
chord deviation** — geometrically intuitive quantities that approximate the signature's spatial information in a
physically meaningful way.

---

<a name="19"></a>
## 19. DFL Dataset — Mouse Dynamics for Continuous Authentication in Free-Living Conditions (2018)

- **Authors:** Shen Wang, et al. (Tsinghua University / Carnegie Mellon University)
- **Year:** 2018
- **Venue:** *IEEE Transactions on Information Forensics and Security* (TIFS)
- **URL / DOI:** <https://ieeexplore.ieee.org/document/8519330>

### Abstract
The **DFL (Daily Free-Living) mouse dynamics dataset** consists of uncontrolled, naturalistic mouse event logs
from **21 users across daily desktop activities** (coding, browsing, gaming, office work). Unlike Balabit's
challenge format, DFL contains fully unconstrained sessions with highly heterogeneous task types, providing a
rigorous naturalistic benchmark for evaluating short-signal authentication robustness.

### Strengths
- 21 users across diverse naturalistic activity types — substantially more ecologically valid than Balabit
- Contains naturally short movement strokes as part of real daily tasks
- Frequently paired with Balabit to demonstrate cross-dataset generalizability (e.g., LT-AMouse [P1])

### Weaknesses
- Data collection period varies across users — session lengths and event rates are inconsistent
- No standardized impostor sessions — evaluation protocols must be defined by researchers
- Larger dataset increases computational requirements for feature extraction

### Limitations & Thesis Relevance
The DFL dataset provides our **secondary evaluation benchmark** for naturalistic short-signal mannerism
extraction. Its free-living design tests whether closed-form geometric descriptors generalize beyond the
constrained Balabit task setup.

---

<a name="20"></a>
## 20. One-Class Mahalanobis Distance Profiles for Compact Mouse Dynamics Authentication (2020)

- **Authors:** Ahmed Awad, Hatem Abouelseoud, et al.
- **Year:** 2020
- **Venue:** *IEEE Access*, Vol. 8, pp. 159689–159704
- **URL / DOI:** <https://doi.org/10.1109/ACCESS.2020.3020087>

### Abstract
A compact, interpretable feature set of **28 geometric and kinematic mouse trajectory features** (velocity
statistics, angular metrics, curvature approximations, click timing, and straightness ratio) is extracted per
short movement segment. **One-class Mahalanobis distance** is used to match test feature vectors against enrolled
user profile covariance matrices. Achieves **AUC 0.83 on Balabit** with negligible computational overhead.

### Strengths
- Small, interpretable feature set: 28 geometric quantities all physically meaningful
- One-class Mahalanobis distance enables anomaly detection without impostor training data
- Near-zero computational overhead — suitable for continuous background execution

### Weaknesses
- Mahalanobis distance is a vector-space metric — ignores spatial ordering of the trajectory
- AUC 0.83 trails deep learning benchmarks significantly
- Feature engineering is manual and may miss complex geometric interactions

### Limitations & Thesis Relevance
This paper demonstrates that a **small, interpretable geometric feature set + one-class anomaly detection** is a
viable authentication architecture. Our thesis upgrades the comparison step from Mahalanobis distance to
**discrete Frechet distance**, which directly compares trajectory sequences while preserving spatial ordering —
a more principled geometric matching approach.

---

## Master Synthesis Table: 20 Papers Mapped to Adviser-Guided Thesis Scope

| # | Study | Year | Unit of Analysis | Core Feature Representation | Profile Comparison | Primary Limitation Addressed by Our Thesis |
|---|---|---|---|---|---|---|
| 1 | Wang et al. (LT-AMouse) | 2025 | Mouse Authentication Units (MAUs) | 1D-ResNet + GRU latent embeddings | Neural classifier score | Black-box; our thesis uses closed-form geometry |
| 2 | Antal et al. (SapiMouse) | 2021 | 15-second short burst (120 users) | FCN learned features | One-Class SVM | Uninterpretable; our thesis provides traceable descriptors |
| 3 | Almalki et al. | 2019/21 | Click-to-click strokes | Curvature radius, straightness, inflection count | KNN / RF | Scalar summaries lose curve topology; our thesis uses Frechet alignment |
| 4 | Tao et al. | 2026 | Spatiotemporal stroke sequences | sLSTM + MixConv multi-scale features | Isolation Forest per user | Computationally heavy, non-interpretable; our thesis is deterministic |
| 5 | Asgarov | 2026 | Windowed bursts | Path signatures, differential geometry, optimal-control residuals | Mahalanobis distance | Vector-space distance; our thesis uses elastic Frechet curve matching |
| 6 | Sadeghpour & Vlajic (ReMouse) | 2023 | Repeat task strokes (100 users) | DTW + VGG16 embeddings | DTW clustering | DTW warping artifacts; our thesis uses discrete Frechet |
| 7 | Jin, Liao & Zhou | 2023 | Trajectory segments | Learned similarity embeddings | Direct template distance | Fixed-length resampling distorts short strokes; our thesis is variable-length |
| 8 | Khan et al. (ACM Survey) | 2024 | Comprehensive taxonomy | Full curvature formula taxonomy | Survey synthesis | Identifies approximation bias; directly substantiates our gap |
| 9 | Cassiano et al. | 2020 | Short sliding windows | Directional velocity (dx/dt, dy/dt) | 1D-CNN binary classifier | Black-box velocity features; our thesis adds geometric interpretability |
| 10 | Shen et al. | 2013 | 20 clicks (very short strokes) | Direction angle, angle of curvature, curvature distance | SVM | Three-point angle noise; our thesis uses Menger curvature |
| 11 | Djioua & Plamondon | 2019 | Individual motor strokes | Sigma-lognormal velocity impulse parameters | Motor model fitting | Computationally expensive fitting; our thesis uses fast closed-form geometry |
| 12 | Song et al. | 2022 | Cross-application short segments | Scene-irrelated curvature spectrum, velocity offsets | Anomaly detection | Manual 50+ features; our thesis uses compact principled descriptors |
| 13 | Balabit Dataset | 2016 | 50-observation challenge windows | Raw (x,y,t,button,state) logs | Challenge evaluation | Primary evaluation benchmark for our thesis |
| 14 | Migdalis et al. | 2022 | Short trajectory image patches | VGG16 image features + Grad-CAM | CNN binary classification | Shows shape is key; our thesis computes shape explicitly via geometry |
| 15 | Breier et al. | 2021 | 2D spatial trajectory images | Spatial image features (no time) | 2D-CNN classification | Confirms spatial shape discriminates; our thesis uses closed-form geometry |
| 16 | Gutuleac et al. | 2021 | Goal-directed short strokes | Fitts' Law residual + trajectory geometry | Hybrid classifier | Widget-dependent; our thesis generalizes to all unconstrained strokes |
| 17 | Revenko et al. | 2022 | Fixed short windows | Directional derivatives (BiGRU) | BiGRU binary classification | Black-box bidirectional; our thesis adds curvature/deviation on same input |
| 18 | Asgarov & Musayeva | 2022 | Short variable-length paths | Path signatures (rough path theory) | One-class SVM | Abstract algebra; our thesis uses visually inspectable geometric quantities |
| 19 | DFL Dataset | 2018 | Naturalistic daily task logs | Raw (x,y,t) mouse event logs | Secondary benchmark | Free-living generalization benchmark for our thesis |
| 20 | Awad et al. | 2020 | Short movement segments | 28-feature geometric + kinematic compact set | One-class Mahalanobis distance | Vector-space distance ignores curve ordering; our thesis uses Frechet |

---

*Document generated: 2026-08-31 | Adviser scope: short mouse signals, discrete behavioral mannerisms*  
*Rule: Do NOT copy these abstracts verbatim into the thesis — paraphrase and cite per your school format.*
