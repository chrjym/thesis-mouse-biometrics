# Academic Style, Tone & Phraseology Guide

This reference provides concrete linguistic patterns, rhetorical structures, and stylistic standards for drafting and revising high-impact academic computer science and biometrics manuscripts.

---

## 1. Academic Register & Voice

### 1.1 Precision Over Hyperbole
Academic writing achieves authority through rigorous evidence and precise descriptions, not emphatic or promotional vocabulary.

| Avoid (Promotional / Vague) | Prefer (Precise / Scholarly) |
| :--- | :--- |
| "A revolutionary new approach" | "A closed-form geometric framework" |
| "Incredibly fast computation" | "Sub-millisecond per-trajectory processing latency" |
| "Achieves virtually perfect accuracy" | "Yields an Equal Error Rate (EER) of 2.14% on the benchmark dataset" |
| "Prior methods are completely useless for..." | "Prior methods exhibit computational degradation when applied to..." |
| "Obviously, the user trajectory shows..." | "Empirical observation indicates that the trajectory manifests..." |
| "A huge amount of data" | "An extensive corpus comprising 12,000 discrete stroke trajectories" |

### 1.2 The Active vs. Passive Voice Dynamic
- **Use active voice** when describing deliberate architectural, experimental, or analytical decisions made by the researchers:
  - *Yes:* "We formulate the trajectory curvature using the discrete Menger curvature of three consecutive coordinates."
  - *Avoid:* "The trajectory curvature is formulated by us..."
- **Use passive voice** when the focus is properly placed on the object, process, or phenomenon itself:
  - *Yes:* "Trajectories were sampled at a uniform polling frequency of 125 Hz."
  - *Yes:* "The calculated Fréchet distance is compared against an adaptive per-user threshold."
- **Avoid ambiguous agentless passives** where the reader cannot discern whether a claim originated in prior literature or in the current study:
  - *Ambiguous:* "It was shown that global bounding features fail under short strokes."
  - *Clear:* "Zhang et al. [14] demonstrated that global bounding features degrade when stroke duration drops below 500 ms." OR "In Section 4.2, we show that global bounding features fail under short strokes."

---

## 2. Epistemic Calibration (Hedging & Assertion)

Academic claims must be carefully calibrated to match the strength of the supporting empirical or theoretical evidence.

### 2.1 Hedged Interpretations (Findings & Inferences)
When interpreting empirical results, generalizations, or observed phenomena:
- "The results **indicate** that sub-movement chord deviation correlates with individual motor habit."
- "These observations **suggest** a heightened vulnerability to synthetic trajectory injection."
- "The performance **tends to degrade** under high DPI mouse configurations, likely attributable to..."
- "This behavior **may be explained by** the physiological constraints of fine motor coordination."

### 2.2 Strong Assertions (Mathematical & Factual Truths)
When stating mathematical definitions, experimental design facts, or proven theorems:
- "Equation (3) **defines** the circumradius of the triangle formed by points $p_{i-1}, p_i, p_{i+1}$."
- "The benchmark dataset **comprises** 45 participants recording across three distinct sessions."
- "Under Definition 2, the straightness ratio **is strictly bounded** within the interval $(0, 1]$."

### 2.3 Verb Spectrum for Literature Attribution
Vary attribution verbs according to the source's objective and rigor:

- **Neutral statement of finding:** *demonstrate, report, observe, determine, establish, evaluate.*
  - "Bhatt et al. [5] reported an EER of 4.8% using multi-scale trajectory velocity profiles."
- **Theoretical argument or hypothesis:** *propose, suggest, hypothesize, argue, posit.*
  - "Jain and Kumar [11] posited that continuous behavioral signals mitigate credential-replay attacks."
- **Critique or limitation:** *note, contend, identify, highlight, acknowledge.*
  - "While Smith et al. [8] highlighted the discriminative power of stroke curvature, they acknowledged high sensitivity to discrete sensor noise."

---

## 3. Cohesion & Discourse Flow: The Known-New Contract

Ensure that every paragraph advances logical argumentation by placing established/known information at the beginning of sentences (the topic position) and introducing new information toward the end (the stress position).

### 3.1 Signposting & Transition Taxonomy

| Purpose | Recommended Discourse Connectives |
| :--- | :--- |
| **Contrast / Conflict** | *In contrast, conversely, whereas, nevertheless, on the other hand, unlike prior formulations, notwithstanding* |
| **Causation / Consequence** | *Consequently, therefore, thus, as a result, hence, it follows that, yielding* |
| **Addition / Elaboration** | *Furthermore, moreover, in addition, additionally, specifically, along similar lines* |
| **Concession** | *Although, despite, while acknowledging that, even though, granted that* |
| **Exemplification / Focus** | *For instance, specifically, in particular, notably, to illustrate* |
| **Temporal / Sequential** | *Subsequently, thereafter, concurrently, simultaneously, prior to* |

### 3.2 Eliminating Nominalization Traps
Excessive nominalization (turning active verbs into heavy Latinate nouns) obscures clarity.

- *Wordy / Heavy:* "The implementation of an evaluation of the classification accuracy was performed by the algorithm."
- *Lean / Vigorous:* "The algorithm evaluated classification accuracy."
- *Wordy / Heavy:* "There was a realization of performance degradation during periods of user fatigue."
- *Lean / Vigorous:* "Performance degraded significantly during periods of user fatigue."

---

## 4. Academic Phrasebank for Research Sections

### 4.1 Stating the Gap / Problem
- "Despite recent advancements in [Topic], existing methodologies predominantly rely on..."
- "A critical limitation shared across prior studies [Refs] is the assumption that..."
- "However, this formulation introduces substantial computational overhead, rendering it ill-suited for real-time edge deployment."
- "To date, the literature lacks a comprehensive comparative analysis addressing..."

### 4.2 Introducing the Proposed Approach
- "To overcome these challenges, we introduce [Approach Name], a novel framework designed to..."
- "In contrast to black-box deep learning architectures, our approach formulates user mannerisms via closed-form geometric properties."
- "Specifically, we decouple trajectory dynamics into local differential geometry and global spatial containment."

### 4.3 Synthesizing and Contrasting Literature
- "While [Author A] and [Author B] both utilize trajectory angle histograms, their matching paradigms diverge: the former relies on support vector machines, whereas the latter employs one-class anomaly detection."
- "Although neural sequence models (e.g., LSTMs [Ref]) achieve competitive classification accuracy, their decision boundaries lack mathematical interpretability."

### 4.4 Reporting and Analyzing Metrics
- "As summarized in Table 3, the proposed feature set achieves an EER of 1.87%, outperforming the baseline by 3.42 percentage points."
- "The trade-off between decision latency and classification certainty is illustrated in the DET curve of Figure 4."
- "A paired-samples $t$-test indicates that the reduction in False Acceptance Rate is statistically significant ($p < 0.001$)."

### 4.5 Articulating Limitations & Threats to Validity
- "The empirical evaluation is subject to several constraints. First, the recording apparatus..."
- "Although our pipeline demonstrates resilience against moderate motor drift, its performance under adversarial playback remains an open question."
- "External validity is constrained by the demographic profile of the participant cohort, which primarily comprised university students."
