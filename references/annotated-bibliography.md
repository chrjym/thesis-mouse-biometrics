# Annotated Bibliography — Mouse Dynamics Behavioral Biometrics for Continuous Authentication

Source: `Literature_Review_Mouse_Biometrics.xlsx` (compiled by the thesis group, 4 members, ~46 entries).
Each entry: title, one-line summary, source link, strengths, and limitations/gaps, as logged by the group.

## Table of Contents
1. [Fundamentals & Angle/Curvature-Based Methods](#1-fundamentals--anglecurvature-based-methods)
2. [Deep Learning Approaches](#2-deep-learning-approaches)
3. [Multimodal & Fusion Approaches](#3-multimodal--fusion-approaches)
4. [Evaluation Methodology, Metrics & Surveys](#4-evaluation-methodology-metrics--surveys)
5. [Adversarial Robustness, Spoofing & Bot Detection](#5-adversarial-robustness-spoofing--bot-detection)
6. [Alternative Modalities & Novel Capture Methods](#6-alternative-modalities--novel-capture-methods)
7. [Randomness, Static Auth & Practical Deployment Constraints](#7-randomness-static-auth--practical-deployment-constraints)
8. [Geometric/Spatial Feature-Focused (Member 2's angle — curvature, Fréchet distance)](#8-geometricspatial-feature-focused)

Use this file for citation-checking, gap-spotting, and drafting RRL sections. Don't reproduce
abstracts verbatim in the actual thesis — paraphrase and cite properly per your school's format.

---

## 1. Fundamentals & Angle/Curvature-Based Methods

**An Efficient User Verification System Using Angle-Based Mouse Movement Biometrics**
(dl.acm.org/doi/10.1145/2893185, also reprinted as "An Efficient User Verification System via Mouse Movements")
- Point-by-point angle-based metrics (direction angle, angle of curvature, curvature distance), SVM classification, platform-independent.
- EER of 1.3% with 20 clicks; partial-movement detection cuts verification time from ~37.7 min to ~3 min but raises EER to 1.9%.
- Gap: doesn't meet European Standard for Access Control (FAR<0.001%, FRR<1%); no resistance testing against offline/generative forgery.

**Insights from Curve Fitting Models in Mouse Dynamics Authentication Systems** (Tan, Binder, Boshmaf)
- Point-by-point angle/curvature metric + SVM/AR curve-fitting, 53-user uncontrolled dataset, AUC 0.86.
- Gap: uses curve-fitting/AR rather than closed-form geometric curvature (e.g., Menger curvature); moderate AUC vs. later deep learning.

**Dynamic User Authentication Based on Mouse Movement Curves** (two entries, DCU / Springer versions)
- Curves traced by consecutive mouse positions carry discriminative info; back-propagation neural network classifier; 10 participants, Mac OS.
- Best EER 5.3% at 300 curves/session (vs. Schulz's 16.6%). Nine curve features designed for translation/scale/rotation invariance.
- Gaps: small N, single-platform; sessions take 5.6–18.7 min (impractical for real-time); consistency over time not evaluated; fatigue effects; internal inconsistency in one write-up (Manhattan vs. Euclidean reported as best in different sections).

**A Study on Mouse Movement Features to Identify User**
- Survey/categorization of features used across mouse-dynamics literature.
- Gap: inconsistent feature naming/calculation across researchers; some features depend on click events or keyboard patterns, reducing mouse-only applicability.

## 2. Deep Learning Approaches

**Mouse dynamics based user recognition using deep learning** (two related entries — ausi-2020 and a 2020 ResearchGate version)
- 1D-CNN on raw sequences using directional velocities (dx/dt, dy/dt) instead of absolute coordinates (translation-invariant); tested on Balabit + DFL, transfer learning explored.
- 0.98 AUC on Balabit, beating prior 1D-CNN (0.90) and 2D-CNN (0.96); fully reproducible (public data + code).
- Gaps: only 10 users (Balabit)/21 (DFL); weak multi-class identification (0.55–0.66 acc); transfer-learning gains modest/overstated in abstract vs. body.

**SapiMouse: Mouse Dynamics-based User Authentication Using Deep Feature Learning**
- Introduces SapiMouse dataset (120 users, heterogeneous hardware/DPI); fully convolutional network learns features directly from raw trajectories; one-class SVM per subject.
- 0.94 AUC using only 15 seconds of data; larger/more diverse dataset than Balabit — relevant if studying hardware/DPI variability.
- Gap: end-to-end learning sacrifices interpretability of explicit geometric descriptors; DPI variability is natural, not systematically controlled.

**User Authentication Based on Mouse Dynamics Using an Efficient-Net Model**
- Lightweight EfficientNet-inspired model on SapiMouse (120 users); CGAN generates 120 synthetic "Unknown" profiles → 240-class problem.
- 99.24% accuracy, F1 0.991, inference 0.233s/sample — exceeds prior mouse-dynamics benchmarks.
- Gap: CGAN "Unknown" class may not capture real impostor complexity; extreme emotional/physical states degrade accuracy; 50-event session splitting may miss longer-term patterns.

**Machine and Deep Learning Applications to Mouse Dynamics for Continuous User Authentication**
- 40-user dataset; 3 ML + 3 DL algorithms; 1D-CNN peak 85.73% (top-10 users, binary); ANN peak 92.48% (multi-class).
- Gap: small dataset (40 users); primary challenge remains silent/continuous verification without invasive sensors.

**Mouse Authentication Without the Temporal Aspect – What Does a 2D-CNN Learn?**
- Converts trajectories to 2D images, 2D-CNN + joint multi-label learning, isolates spatial (non-temporal) structure; gaming context, 92.73% avg accuracy.
- Gap: only 10 users; gaming introduces confounds (camera-look movements) atypical of desktop use.

**User identity authentication via spatiotemporal mouse dynamics modeling**
- Hybrid sLSTM + MixConv, personalized isolation-forest per user, evaluated on Balabit + SapiMouse.
- State-of-the-art: AUC 99.45%/EER 2.87% (Balabit), AUC 99.10%/EER 3.14% (SapiMouse).
- Gap: very recent, little independent replication yet; spatial features learned via convolution, not closed-form geometry — limited interpretability for a geometry-focused thesis.

**A Proposal for Continuous and Silent User Authentication Through Mouse Dynamics and Explainable Deep Learning**
- Converts Balabit CSV logs into composite PNG images (movement/drag/click/release); VGG16 + Grad-CAM for explainability.
- Precision/accuracy/F1 = 0.902, AUC = 0.953 after augmentation to 8,000 elements/class.
- Gap: preliminary, single dataset (10 users), single model (VGG16), dataset from 2016 may not reflect modern interaction patterns.

**User Authentication Based on Mouse Dynamics Using Deep Neural Networks: A Comprehensive Study**
- Compares 1D-CNN, 2D-CNN, LSTM, hybrid CNN-RNN, and transfer-learning 2D-CNN against classical handcrafted-feature ML baseline.
- Transfer-learning 2D-CNN outperformed all others including classical ML baseline; frequently cited IEEE TIFS benchmark.
- Gap: implicit feature extraction — no explicit curvature/Fréchet-distance quantities reported; performance dataset-dependent, degrades with small-dataset random init.

## 3. Multimodal & Fusion Approaches

**Hand in Motion: Enhanced Authentication Through Wrist and Mouse Movement**
- Combines device-independent angle-based mouse features + wrist motion (smartwatch/wristband); Random Forest Ensemble Classifier + Sequential Sampling Analysis.
- FAR 1.46% (impostors)/4.69% (intruders), FRR 0%; decision within 9–12 clicks (up to 49% faster than geometry-only methods).
- Gap: requires wearable hardware; 26 subjects, all right-handed; hand physical characteristics affect wrist patterns; early-stage, needs integration with other modalities.

**Wrist in Motion: A Seamless Context-aware Continuous Authentication Framework Using Your Clickings and Typings**
- Context-aware keystroke latency + angle-based mouse metrics + wrist motion; one-vs-all RFEC; Sequential Sampling Analysis + Dynamic Trust Model.
- 44 subjects: FRR 0.92% (genuine), FAR 0% (attackers), identification within 35 mixed actions.
- Gap: early-stage; cross-platform testing raises FRR; needs further modality fusion (touch, posture); proposes deep learning (RNN/LSTM) as future work.

**A study on continuous authentication using a combination of keystroke and mouse biometrics**
- Multimodal fusion of keystroke + mouse dynamics; argues fusion improves robustness/time-to-detection vs. single modality.
- Gap: requires simultaneous keystroke+mouse activity (unavailable during mouse-only periods like browsing/gaming); harder to attribute gains to mouse dynamics alone; keystroke logging raises more privacy concerns than mouse logging.

**Design and Implementation of Continuous Authentication Mechanism Based on Multimodal Fusion Mechanism (MFCA)**
- Fuses keystroke (decision tree), mouse (linear SVM), and application usage (statistical modeling) with a time-variant trust model.
- 22 participants; illegal users caught after ~430 feature inputs on average, legitimate users undisturbed for ~7,341 inputs.
- Gap: hand-set trust thresholds; privacy risk from model attacks (mitigations only proposed, not implemented); small sample (22); PC-centric scope.

**A Comprehensive Review on Secure Biometric-Based Continuous Authentication and User Profiling**
- 2024 survey spanning physiological, behavioral, multimodal, and context-aware CAS approaches.
- Identifies gaps: lack of comparative analysis across biometric pairings; usability/security/scalability under-studied vs. accuracy (FAR/FRR/EER).
- Gap: review only, no new empirical data; mouse dynamics is only one slice of a broad survey.

**Mitigating insider threat by profiling users based on mouse usage pattern: ensemble learning and frequency domain analysis**
- Legality score per action aggregated into session-level legality probability; frequency-domain (Lomb-Scargle) features combined with time-domain.
- Balabit (10 users, extended to 20): EER 7.46%, AUC 96.47%; faster than deep learning (<2ms/action, ~5x speedup).
- Gap: ignores inter-action sequence relationships (can't capture higher-level patterns like DL); small dataset; one user (user21) underperformed.

## 4. Evaluation Methodology, Metrics & Surveys

**Evaluating Behavioral Biometrics for Continuous Authentication: Challenges and Metrics**
- Analyzes 16 biometric datasets; shows mean FAR/FRR hides systematic vs. random error distribution; proposes Gini Coefficient (GC) as additional metric.
- Finding: 13/25 papers reviewed either included impostor data in negative-class training or randomly sampled training data — leading to 63–81% underestimation of error rates.
- Gap: meta-study, doesn't propose a new authentication algorithm; 16 datasets may not include newest mouse-specific sets (e.g., SapiMouse); adopting GC requires field-wide reporting-norm change.

**Mouse Dynamics Behavioral Biometrics: A Survey** (ACM Computing Surveys, covers 1897–2023)
- Comprehensive review: data collection protocols, raw-attribute taxonomy, mathematical feature definitions (including curvature), public datasets, ML/DL methods.
- Directly usable as a methodological reference for curvature computation from discrete trajectory points; identifies open research gaps.
- Gap: synthesizes rather than generates new results; some cited curvature formulas are simplified approximations, not rigorous differential geometry (no explicit Menger curvature discussion).

**MATHEMATICAL FEATURE REPRESENTATIONS OF MOUSE DYNAMICS FOR CONTINUOUS USER AUTHENTICATION** (two related versions — jpit.az and doi.org/10.25045/jpit.v17.i2.02)
- Three feature families: path signatures (rough path theory), differential-geometric cursor descriptors, optimal-control residuals (motor-control models). Evaluated on Balabit + SapiMouse vs. a 142-feature reference bank, one-class Mahalanobis protocol.
- Key result: optimal-control (OC) features give best compact representation — AUC 0.749 (Balabit)/0.709 (SapiMouse) with only 23 features, cheapest to extract (0.17ms/window); combined features reach AUC 0.815, F1 0.774.
- Gap: Balabit only 10 users (flagged by authors as too small); best 7-feature OC subset lacks mathematical justification for generalization; only tested with one detector (Mahalanobis) — deep-learning detectors left as future work.

**Analyzing spatial data from mouse tracker methodology: An entropic approach (EMOT)**
- Proposes entropy-based trajectory analysis (EMOT) vs. traditional descriptive geometric approach (DGA, e.g., max deviation, area under curve); models trajectories as fast movement + motor pauses.
- Relevant for critiquing simple geometric-summary approaches as ignoring motor pauses / trajectory noise.

**Intrusion Detection Using Mouse Dynamics**
- Descriptive/exploratory paper detailing Balabit dataset structure and reviewing prior authentication, monitoring, and stress-detection applications of mouse dynamics.
- Gap: primarily descriptive, no new feature-extraction technique; compares to older baselines.

**Mouse Biometric Authentication** (review paper referencing U. Washington / San Jose State studies)
- Reviews trajectory-point/velocity/angle logging methods; introduces a "Bubble Click Application" for controlled data capture.
- Concludes mouse dynamics work best as a complementary layer, not standalone — due to long collection times, hardware/workflow variability, and remote-desktop/input-technology shifts.

## 5. Adversarial Robustness, Spoofing & Bot Detection

**Adversarial Attacks on Remote User Authentication Using Behavioural Mouse Dynamics**
- Realistic threat model: attacker has compromised client data but no access to remote server/model. Three attack types: statistics-based, imitation-based (GRU-RNN), surrogate-based.
- Surrogate attacks reach up to 92.1% success (SVM target) / 81.7% (1D-CNN target) if architecture is correctly guessed.
- Gap: fills a real gap (little prior adversarial work on mouse dynamics vs. image domain), but architecture-guessing assumption may not always hold in practice.

**SapiAgent: A Bot Based on Deep Learning to Generate Human-Like Mouse Trajectories**
- Deep-autoencoder bot generating human-like trajectories to support bot-detection research; trained/evaluated on SapiMouse.
- Gap: focused on generation/evasion, not authentication accuracy; fidelity assessed at system level, not via explicit geometric metrics.

**ReMouse Dataset: On the Efficacy of Measuring the Similarity of Human-Generated Trajectories for the Detection of Session-Replay Bots**
- First public dataset with repeat sessions from same users (100 MTurk users); DTW + VGG16 (transfer learning) + unsupervised clustering (SOM, K-means, agglomerative).
- Establishes: no two human sessions are identical (even same-user repeats); cross-user sessions remain distinguishable after behavior stabilizes. Closest cross-user DTW distance (21.94) > closest same-user distance (20.38).
- Gap: MTurk sample bias; small scale (100 users, ~5 min each); artificial guided task; no actual bot data (detection claim inferred, not tested); no formal significance testing.

**User Authentication and Identity Inconsistency Detection via Mouse-trajectory Similarity Measurement**
- Single embedding model for both authentication and CAPTCHA-farm/identity-inconsistency detection (one classifier for all users, not per-user).
- 130-user hybrid dataset (SapiMouse+Balabit): 94.3% AUC (inconsistency detection), 97.7% AUC (authentication); 7–10x faster training than InceptionTime/Hydra+MultiROCKET/HIVE-COTEv2.
- Gap: requires long trajectory segments (length-256 cap); doesn't explicitly use Fréchet distance (other similarity measures used).

**Optimizing Mouse Dynamics for User Authentication by Machine Learning: Addressing Data Sufficiency, Accuracy-Practicality Trade-off, and Model Performance Challenges (LT-AMouse)**
- Investigates environmental interference (surface friction, hardware sensitivity), minimal-input scenarios, adversarial trajectory forgery; evaluated on Balabit + DFL.
- Directly relevant to hardware-sensitivity/degradation angle of geometry-focused theses.
- Gap: focuses on adversarial forgery/defense, not systematic controlled degradation (e.g., polling-rate downsampling); doesn't isolate curvature/Fréchet-distance fidelity explicitly.

## 6. Alternative Modalities & Novel Capture Methods

**Fine-grained continuous user authentication via mouse grip pressure biometrics**
- Flexible film resistive pressure sensors at 5 grip locations; hierarchical model segments movement into 12 directional domains.
- 12 participants: accuracy >99% (KNN), FAR <0.1%, FRR <0.4%; robust to counterfeiting/imitation attacks (FAR stays <0.2% under attack).
- Gap: small/narrow pool (12 right-handed users, 18–40); sensor drift from temperature/humidity; explicit enrollment burden (10 circular movements); no multimodal fusion or deep learning tested yet.

**A Behavioral Biometric Authentication System Based on Memory Game**
- 24-tile memory game captures mouse movement; AR modeling extracts X/Y features; Euclidean/Manhattan/Mahalanobis distance classifiers compared.
- 50 volunteers, 10 sessions: Euclidean EER 2.1% (best), accuracy 88.03%; outperforms maze-navigation/poker-based systems.
- Gap: AR model excludes past noise/process model; Euclidean performs poorly in high dimensions; user fatigue from repeated sessions; touchpad users found the game harder.

**A Real-Time Authentication Method Based on Cursor-hidden Scene**
- Hides cursor on suspicious activity, assuming anxious/instinctive reactions; builds behavioral model from those reaction traces.
- 2.6% FAR, 3.3% FRR; only ~2 min training data needed, authentication in seconds (vs. 17–37 min for prior methods).
- Gap: feasibility shown with only 2 users, 150 records total; assumes user doesn't swap mouse hardware when a malicious user takes over; emotion-driven errors acknowledged as not fully ruled out.

**From Clicks to Security: Investigating Continuous Authentication via Mouse Dynamics**
- Compares GRU, LSTM, Decision Tree, Random Forest across two gaming scenarios (high-intensity "Team Fortress" vs. low-intensity "Poly Bridge").
- GRU AUC 0.96, LSTM 0.92, Random Forest F1 0.95 — competitive with/exceeding prior studies (Antal et al. 0.95, Salman & Hameed 0.981).
- Gap: Decision Tree/Random Forest show notable train-test variance (overfitting risk); all models decline slightly in the high-intensity environment.

## 7. Randomness, Static Auth & Practical Deployment Constraints

**Randomized Mouse Movement for Behavioral Biometric Identification**
- Random-button-following task to capture unpredictable, real-life mouse behavior; 5 users, 46.67% matching accuracy.
- Gap: very small cohort, low accuracy; screen resolution/pointer-speed differences historically degrade performance without standardization.

**Mouse Movement Behavioral Biometric For Static User Authentication**
- Static (login-time) authentication via mouse movement; data capture → feature extraction → classifier pipeline; 10 participants, 44% authenticate rate.
- Gap: limited data available at login; short decision window trades off length vs. accuracy.

**Secure System of Continuous User Authentication Using Mouse Dynamics**
- Open-scenario (no prior registration) continuous authentication; one-class SVM detects deviation from recorded pattern.
- Gap: weak accuracy — EER 50% (authors admit "not up to the mark"); of 23 participants over 4 weeks, only 8 yielded usable data; narrow population (engineering students).

**Continuous Authentication Using Mouse Clickstream Data Analysis** (two related entries)
- 39 features from Balabit; Decision Tree, KNN, Random Forest classifiers across 3 mouse actions (move, click, drag).
- 100% accuracy in verification mode; best authentication result: KNN on point-and-click, 99.3% ACC / 99.9% AUC.
- Gap: high false rejection in some configs (RF FRR 0.473); anomalous KNN FAR/EER of 8.444 in one report; field "not yet reached an acceptable level of accuracy" per the authors.

**Performance and Security Evaluation of Behavioral Biometric Systems** (PhD thesis)
- Generic framework for behavioral biometrics (keystroke + physical activity, not mouse-specific) using classical ML + deep learning; reversible signal-to-image transform for 2D CNNs; TimeGAN used to synthesize spoofing attacks.
- Gap: focuses on keystroke/activity, not mouse dynamics — applicability to mouse-based CA is indirect; single-author thesis limited to lab/benchmark testing.

## 8. Geometric/Spatial Feature-Focused

*(Entries most directly relevant if your thesis centers on curvature/Fréchet-distance-style geometric descriptors — cross-referenced from sections above.)*

- **Mathematical Feature Representations of Mouse Dynamics** — closest existing work to explicit geometric feature engineering (path signatures, differential geometry, optimal-control residuals).
- **Mouse Dynamics Behavioral Biometrics: A Survey** — best available mathematical reference for curvature formulas from discrete trajectory points.
- **ReMouse Dataset** — DTW as a Fréchet-distance-adjacent similarity metric; strong empirical support that geometric trajectory features are "noisy but discriminative," never perfectly repeatable.
- **User Authentication and Identity Inconsistency Detection via Mouse-trajectory Similarity Measurement** — trajectory-similarity as the authentication mechanism itself, though not explicitly Fréchet distance.
- **Continuous Authentication Using Mouse Clickstream Data Analysis (arXiv:2312.00802 version)** — reproduces Schulz's (2006) curvature/inflection/straightness features; useful prior art and EER-vs-sample-size framing (24.3% at 60 curves → 11.2% at 3,600 curves).
- **Optimizing Mouse Dynamics... (LT-AMouse)** — most relevant existing work on hardware-sensitivity/environmental interference, if the thesis simulates hardware degradation.
- **SapiMouse** — most relevant dataset if hardware/DPI heterogeneity is part of the thesis's evaluation design.

---

## 9. Literature Evolution & Identified Gap (thesis framing, as presented to adviser)

**Four-phase evolution of mouse-dynamics authentication literature:**

| Phase | Era | Dominant Representations | Key Algorithms & Technologies | Primary Bottlenecks & Limitations |
|---|---|---|---|---|
| 1: Early Feasibility Studies | 2003–2004 | Mouse gestures, strokes, coordinates | Distance measures, statistical analysis, neural networks | Small samples; controlled or task-specific interaction |
| 2: Classical Mouse-Dynamics Biometrics | 2007–2011 | Movement distance, speed, direction, click behavior | Statistical signatures, feature engineering, SVM, fuzzy classification | Large data requirements; device and task sensitivity |
| 3: Continuous Authentication & Geometric Features | 2012–2014 | Curves, curvature, inflection, straightness, action sequences | Geometric descriptors, histograms, Euclidean distance, pattern growth, anomaly detection | Authentication delay; limited public datasets; variable real-world conditions |
| 4: Machine Learning & Deep Learning | 2018–2022 | Raw sequences, directional velocities, images, temporal streams | Random Forest, k-NN, CNN, 1D-CNN, CNN-LSTM, one-class SVM | Training cost, model complexity, interpretability and robustness concerns |

**Identified gap — no work stays in the "middle" to measure shape directly and rigorously:**

| Gap | Summary | Source |
|---|---|---|
| Local geometry | Curvature/shape formulas used in the literature are approximations rather than rigorous differential-geometry treatments — no explicit discrete Menger curvature. | Ahmed et al., 2024 survey, *Mouse Dynamics Behavioral Biometrics* |
| Curve modeling | Relies on curve-fitting / autoregressive models instead of measuring geometry directly. | Tan et al., curve-fitting model paper |
| Shape similarity | Uses other similarity measures instead of Fréchet distance for comparing whole paths. | Fang et al., mouse-trajectory similarity paper |
| Global geometry | Area-based descriptors (e.g., area under the curve) are noisy/irregular and ignore motor pauses. | EMOT paper (Member 3, RRL entry #12) |
| Deep learning | Sacrifices interpretability in favor of learned embeddings. | SapiMouse, Antal & Egyed-Zsigmond, 2021 |

**Resulting thesis framing (as presented to the adviser, 2026-08-28):** the thesis measures the
shape of a single mouse movement from a defined start point to a defined end point, using
closed-form local descriptors — chord deviation, discrete Menger curvature, and straightness
ratio — plus a supplementary global descriptor (convex hull), each computed with explicit
safeguards against its own documented mathematical failure mode. The resulting shape profile is
compared against an enrolled baseline using Fréchet distance, producing a continuous, per-action
trust score traceable to a specific geometric property. See `adviser-log.md` for the adviser's
response and the resulting next deliverable (a full measurement-vs-comparison-method survey).

---

*Compiled from the group's shared spreadsheet (Members 1–4) and subsequent gap-analysis slides
presented to the adviser. When citing in the actual thesis manuscript, go back to the primary
source (DOI/URL given) rather than citing this summary, and follow your university's citation
style.*