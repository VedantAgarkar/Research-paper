# Phase 9: Final Research Roadmap

> **Project**: Real-Time CCTV-Based Elderly Fall Detection in Staircase / Common-Area Environments  
> **Phase**: Phase 9 — Research Plan, Architecture, and Experimental Design  
> **Source**: Gaps surviving Phase 8 adversarial stress test (GAP-01, 02, 03, 04)  
> **Distinction**: A = Research Contribution | B = Engineering Implementation | C = Experimental Contribution

---

## 1. Research Problem

Falls are the leading cause of injury-related death among the elderly globally. Staircase environments represent a disproportionately high-risk location: the combination of elevated surface, physical exertion, and reduced lighting creates a fall scenario with higher injury severity than flat-floor falls. Automated detection and rapid emergency response could significantly reduce response delay and harm.

Existing vision-based fall detection systems operate exclusively in flat-floor environments (living rooms, offices, hospital corridors). No published system — across 588 candidate papers reviewed by P12, and 87 papers reviewed by P07 — has experimentally evaluated fall detection in a staircase or multi-level corridor. Furthermore, no system implements a complete emergency response chain beyond single-shot alert transmission.

The result is a critical gap between published fall detection research and real-world elderly safety infrastructure.

---

## 2. Research Gap (Evidence-Backed)

**Primary gap (confirmed by two independent systematic reviews, P07 §5 and P12 §5.3)**:
> No published study has experimentally evaluated a vision-based CCTV fall detection system in a staircase environment, evaluated against staircase-specific confounding activities, validated in real-time on physical hardware, or integrated an alert acknowledgement and escalation mechanism.

This is a compound gap with four independently evidenced dimensions:
- **G1**: Zero staircase environment evaluations (0/12 papers; 0/87 surveyed papers in P07; 0/11 hardware-validated papers in P12)
- **G2**: Zero evaluation against staircase-specific ADL confounders (0/12 papers; confirmed by Phase 6 analysis)
- **G3**: Zero alert acknowledgement or escalation implementation (0/12 papers; confirmed by P07 and P12)
- **G4**: No hardware-validated staircase deployment (0/11 hardware-validated papers; P12)

---

## 3. Research Question

> **RQ**: Can a lightweight, real-time, CCTV-based fall detection system, specifically designed and evaluated for staircase environments, achieve clinically acceptable performance (sensitivity ≥ 85%, specificity ≥ 90%) against a staircase-specific activity set — including normal staircase activities that closely resemble falls — while integrating a complete alert acknowledgement and escalation pipeline on consumer-grade hardware?

**Sub-questions**:
- **SQ1**: What is the false-positive rate of an existing flat-floor-trained fall detection model when evaluated against staircase-specific activities (descent, bending on steps, stumble+recovery)?
- **SQ2**: Does fine-tuning on a staircase-specific dataset with staircase-ADL negatives significantly reduce the staircase false-positive rate?
- **SQ3**: What is the end-to-end latency from fall detection to local alarm activation and remote alert delivery on consumer-grade hardware?
- **SQ4**: What is the false-positive escalation rate (spurious escalations per hour) of the integrated system in a realistic staircase monitoring scenario?

---

## 4. Hypotheses

**H1 (Core Performance Hypothesis)**:
> A fall detection model fine-tuned on a staircase-specific dataset (including staircase-ADL negatives) will achieve significantly lower false-positive rate on staircase activities than the same model trained exclusively on public flat-floor datasets, when evaluated under identical staircase conditions.

**H2 (Real-Time Hypothesis)**:
> The complete integrated pipeline (YOLOv8-pose + ByteTrack + GRU + MQTT alert) will sustain ≥ 10 FPS on a consumer-grade laptop GPU (GTX 1650 / RTX 3050 mobile) under staircase deployment conditions.

**H3 (Alert Response Hypothesis)**:
> An acknowledgement-escalation protocol will reduce mean unresponsive-fall response delay (time from fall detection to human contact) to below 90 seconds in a simulated residential building scenario.

---

## 5. Objectives

**O1** — Build a staircase-specific fall detection dataset:
- Collect RGB video from 1–2 standard CCTV cameras in a real stairwell
- Record fall clips (staged) and staircase-ADL clips (non-fall)
- Annotate at frame level (pre-fall, fall-onset, impact, post-fall, normal)

**O2** — Develop and evaluate a staircase-adapted fall detection model:
- Baseline: existing architecture (YOLOv8-pose + GRU) trained on public datasets (Le2i, UR Fall)
- Fine-tune on staircase dataset with staircase-specific negatives
- Measure: sensitivity, specificity, F1, staircase-FPR before and after fine-tuning

**O3** — Integrate and evaluate the complete emergency response pipeline:
- Local alarm via ESP32 + buzzer
- Remote alert via MQTT broker → Telegram Bot / mobile notification
- Acknowledgement timeout → automatic escalation to secondary contact
- Measure: fall-to-alarm latency, false-positive escalation rate, acknowledgement response time

**O4** — Validate real-time performance on consumer hardware:
- Profile complete pipeline end-to-end (detection + pose + tracker + GRU + alert)
- Measure FPS under staircase conditions (single person, partial occlusion, dim light)
- Confirm ≥ 10 FPS biomechanical threshold (P12)

---

## 6. Proposed System Architecture

```
INPUT LAYER
┌───────────────────────────────────────────────────────┐
│  Standard RGB CCTV Camera (1–2 cameras)               │
│  Resolution: 720p / 1080p                             │
│  Mount: wall-mounted at staircase landing             │
│  Night mode: IR-illuminated grayscale (automatic)     │
└─────────────────────┬─────────────────────────────────┘
                      │ Video stream (RTSP / USB)
                      ▼
DETECTION & TRACKING LAYER (runs on laptop GPU)
┌───────────────────────────────────────────────────────┐
│  YOLOv8n-pose                                         │
│  • Detects persons + 17-point skeleton per frame      │
│  • ~30–80 FPS on GTX 1650 / RTX 3050m                │
│                                                       │
│  ByteTrack (multi-object tracker)                     │
│  • Assigns consistent person ID across frames         │
│  • Handles short occlusions (banister, frame edge)    │
└─────────────────────┬─────────────────────────────────┘
                      │ Per-person skeleton sequence
                      ▼
TEMPORAL REASONING LAYER
┌───────────────────────────────────────────────────────┐
│  GRU (or LSTM) Temporal Classifier                    │
│  • Input: sliding window of N frames (16–30 frames)   │
│  • Input features: joint angles, velocity, torso incl.│
│  • Output: fall probability score [0.0 – 1.0]         │
│                                                       │
│  Temporal Verification Gate                           │
│  • Requires M consecutive frames above threshold τ    │
│  • Prevents single-frame false positives              │
└─────────────────────┬─────────────────────────────────┘
                      │ Fall confirmed signal
                      ▼
ALERT PIPELINE (Engineering layer — B)
┌───────────────────────────────────────────────────────┐
│  LEVEL 1 — Local Alarm (< 1 second latency)           │
│  • MQTT message → ESP32 microcontroller               │
│  • ESP32 activates buzzer + LED indicator             │
│                                                       │
│  LEVEL 2 — Remote Alert (< 5 second latency)          │
│  • Telegram Bot API / WhatsApp notification           │
│  • Message: "⚠️ Fall Detected — Staircase Floor 2"    │
│  • Optional: Grad-CAM frame snapshot attached         │
│                                                       │
│  LEVEL 3 — Acknowledgement Window (30 seconds)        │
│  • Recipient presses acknowledge button               │
│  • If ACK received → alert resolved                   │
│                                                       │
│  LEVEL 4 — Escalation (if no ACK in 30s)             │
│  • Alert escalated to secondary contact list          │
│  • Repeat every 60 seconds until acknowledged         │
└───────────────────────────────────────────────────────┘
```

---

## 7. Novel Components

### A — Research Contributions (novel, supported by Phase 7–8 analysis)

**A1. First Staircase-Specific Fall Detection Dataset**
- A dataset of RGB video clips from a real stairwell environment
- Includes both fall events and staircase-ADL confounders
- The first dataset specifically designed for staircase fall detection evaluation
- *Evidence of novelty*: P07 §5, P12 §5.3 confirm zero prior staircase datasets

**A2. First Evaluation Against Staircase-ADL Confounder Set**
- Evaluation protocol specifically testing: stair descent, stair ascent, bending on steps, sitting on steps, stumble+recovery, carrying load on stairs
- Introduces "staircase-ADL false-positive rate" (S-FPR) as a reporting metric
- *Evidence of novelty*: Phase 6 confirms 0/12 papers test walking-down-stairs confusion; P12 calls for standardized evaluation protocols

**A3. First End-to-End Staircase Fall Safety System with Empirically Measured Alert Escalation**
- The only published system implementing: detection → local alarm → remote alert → acknowledgement → escalation
- Empirical measurement of: fall-to-alarm latency, false-positive escalation rate, acknowledgement response time
- *Evidence of novelty*: P07 §5 (1/22 vision studies had alarm transmission), P12 §5.3 (no acknowledgement or escalation in any paper)

### B — Engineering Implementation (not claimed as novel research)

- ESP32 firmware for buzzer/LED control via MQTT
- Telegram Bot integration for alert delivery
- MQTT broker setup (Mosquitto local or cloud)
- YOLOv8-pose + ByteTrack integration pipeline
- Sliding window GRU inference loop

### C — Experimental Contributions (novel measurements, not algorithmic novelty)

- Staircase-specific sensitivity/specificity/F1 measurement
- Pre vs. post fine-tuning false-positive rate comparison on staircase ADLs
- End-to-end latency profiling (detection → alarm → notification) on consumer GPU
- Ablation: temporal window size vs. false-positive rate trade-off in staircase context

---

## 8. Experimental Variables

| Variable | Values to Test | Purpose |
|---|---|---|
| Temporal window size (N frames) | 8, 16, 24, 32 | Optimize sensitivity vs. latency |
| Consecutive-frame threshold (M) | 2, 3, 5 | Optimize FP reduction |
| Fall probability threshold (τ) | 0.5, 0.6, 0.7, 0.8 | Precision-recall trade-off |
| Camera angle | ~30°, ~45°, ~60° from horizontal | Effect of staircase camera mounting |
| Lighting condition | Full light, dim (50% lux), IR night mode | Real staircase lighting variation |
| Training data | Flat-floor only vs. + staircase fine-tune | Core hypothesis test (H1) |
| Backbone | YOLOv8n-pose vs. YOLOv8s-pose | Speed vs. accuracy trade-off |

---

## 9. Baseline Systems

| Baseline | Description | Purpose |
|---|---|---|
| **Baseline-A** | MobileNetV2+GRU trained on Le2i (flat-floor) | Zero-shot staircase performance — measures H1 starting point |
| **Baseline-B** | YOLOv8-pose + GRU trained on UR Fall + Le2i | Our model without staircase fine-tuning |
| **Baseline-C** | Our model WITH staircase fine-tuning | Post fine-tuning improvement measurement |

> Note: There is no existing staircase fall detection system to compare against — our system IS the first. This must be explicitly stated in the paper, citing P07 and P12.

---

## 10. Dataset Strategy

### Public Datasets (Pre-training / Transfer Learning)
| Dataset | Purpose | Source |
|---|---|---|
| **Le2i** | Backbone + GRU pre-training | Public (University of Burgundy) |
| **UR Fall** | Additional fall class pre-training | Public (University of Rzeszów) |
| **CAUCAFall** | Validation of base model (following P11) | Public |

### Self-Collected Dataset (Staircase-Specific)
| Category | Target Clips | Description |
|---|---|---|
| **Fall events** | 30–40 clips | Forward, backward, sideward, stumble-to-fall, slow collapse, carrying-object fall |
| **Staircase ADL negatives** | 50–60 clips | Walking down, walking up, bending/picking up, sitting on step, stumble+recover, carrying load, slow descent, using phone |
| **Environmental variation** | Across all clips | Full light, dim, IR night mode; single person; 2+ people nearby |

### Data Collection Protocol
1. Location: real university/building stairwell (1–2 camera angles)
2. Subjects: 3–5 volunteers (young adults, explicitly acknowledged as limitation)
3. Falls: staged with safety mats below frame (falls happen at top of frame, mats out of view)
4. ADLs: natural performance of each activity without coaching for "realism"
5. Each clip: 10–15 seconds, padded before and after the event
6. Annotation: frame-level label at 1/5 FPS granularity (every 5th frame manually verified)

---

## 11. Training Strategy

```
STAGE 1: Pre-training (Transfer Learning)
  Dataset: Le2i + UR Fall (public, flat-floor)
  Architecture: YOLOv8n-pose → ByteTrack → [skeleton features] → GRU
  Goal: Learn general fall dynamics (standing → rapid descent → resting)
  Split: 80/20 train/val, subject-independent split where possible

STAGE 2: Fine-Tuning (Staircase Adaptation)  [core experiment]
  Dataset: Pre-trained model + staircase dataset (falls + staircase-ADLs)
  Goal: Adapt to staircase-specific fall postures and eliminate staircase-ADL FPs
  Split: 5-fold cross-validation (due to small dataset)
  Augmentation: horizontal flip, brightness/contrast jitter, Gaussian noise,
                simulated IR noise (for night evaluation)

STAGE 3: Ablation Training
  Vary: temporal window N, threshold M, threshold τ
  Goal: Characterize the sensitivity vs. FP trade-off curve for staircase context
```

---

## 12. Testing Strategy

```
TEST SET 1 — Public Benchmark (Reproducibility)
  Dataset: Le2i test split, UR Fall test split
  Purpose: Confirm our base model matches P11/P02 published performance
  Metric: Accuracy, Sensitivity, Specificity, F1

TEST SET 2 — Staircase Fall Performance (Primary)
  Dataset: Self-collected staircase fall clips (held-out test split)
  Purpose: Measure how well the model detects staircase falls
  Metric: Sensitivity, Specificity, F1, FPS

TEST SET 3 — Staircase ADL False-Positive Evaluation (Novel)
  Dataset: Self-collected staircase-ADL clips (ONLY non-fall activities)
  Purpose: Measure false-positive rate on staircase confounders
  Metric: S-FPR = (FP alerts / total ADL clips) × 100%
  Compare: Baseline-A vs. Baseline-B vs. Baseline-C (H1 test)

TEST SET 4 — Real-Time Hardware Benchmark
  Dataset: Live video stream from staircase camera
  Purpose: Validate ≥ 10 FPS end-to-end under realistic conditions
  Metric: FPS, fall-to-alarm latency (ms), CPU/GPU utilization

TEST SET 5 — Alert Pipeline Evaluation
  Scenario: Simulated fall events + simulated ADL false-positives
  Purpose: Measure alert system performance
  Metric: Fall-to-alarm latency, false-positive escalation rate, ACK response time
```

---

## 13. Scenarios to Test

### Fall Scenarios (Positive Class)
| Scenario | Description | Priority |
|---|---|---|
| Forward fall | Trips on step, falls forward | 🔴 Essential |
| Backward fall | Loses balance, falls backward | 🔴 Essential |
| Sideward fall | Twists at top of stairs | 🔴 Essential |
| Stumble-to-fall | Stumbles, cannot recover | 🔴 Essential |
| Slow collapse | Weakness, gradual descent to floor | 🟠 Important |
| Object-carrying fall | Falls while carrying bags | 🟡 Optional |

### Non-Fall Scenarios (Negative Class / Staircase-ADL Set)
| Scenario | Description | Priority | Why challenging |
|---|---|---|---|
| Walking down | Normal descent, standard pace | 🔴 Essential | Forward lean + height drop mimics fall |
| Walking up | Normal ascent | 🔴 Essential | Baseline control |
| Slow descent | Elderly-style cautious descent | 🔴 Essential | Slowness + forward lean → high FP risk |
| Bending / picking up | Crouches to pick up item on step | 🔴 Essential | Rapid height drop = fall-like |
| Sitting on step | Deliberately sits down on step | 🔴 Essential | Floor contact = ambiguous |
| Stumble + recover | Loses balance, grabs banister | 🔴 Essential | Near-fall with recovery |
| Carrying load | Descends with heavy bag | 🟠 Important | Altered posture, shifted CoM |
| Phone use | Distracted descent (head down) | 🟡 Optional | Head posture change |

---

## 14. Negative / Non-Fall Scenarios (Detailed)

The staircase-ADL set is the most important negative class — it is what distinguishes this evaluation from all prior work. Priority order:

1. **Slow staircase descent** — highest false-positive risk; directly mimics falling trajectory
2. **Bending on step** — rapid vertical descent below the step surface
3. **Stumble + banister recovery** — fall-onset posture without fall completion
4. **Sitting on step** — floor-contact posture without a fall event preceding it
5. **Fast staircase descent (jogging)** — rapid motion with bouncing trajectory
6. **Walking with large bags** — altered center-of-mass and arm position

---

## 15. Evaluation Metrics

### Primary Metrics
| Metric | Formula | Target |
|---|---|---|
| **Sensitivity (Recall)** | TP / (TP + FN) | ≥ 85% |
| **Specificity** | TN / (TN + FP) | ≥ 90% |
| **F1-Score** | 2 × (Prec × Rec) / (Prec + Rec) | ≥ 85% |
| **S-FPR** (Staircase-ADL False-Positive Rate) | FP alerts / total ADL clips | ≤ 15% |
| **FPS** (end-to-end pipeline) | Frames processed per second | ≥ 10 FPS |

### Secondary Metrics
| Metric | Description |
|---|---|
| **Fall-to-alarm latency** | Time from fall onset frame to local buzzer activation (ms) |
| **Fall-to-notification latency** | Time from fall onset to Telegram message delivered (ms) |
| **False-positive escalation rate** | Spurious escalations per simulated monitoring hour |
| **AUC-ROC** | Area under ROC curve (overall classifier quality) |
| **Precision** | TP / (TP + FP) |
| **Backbone inference time** | Following P11 methodology (ms per frame) |

---

## 16. Ablation Studies

| Ablation | What varies | What it measures |
|---|---|---|
| **ABL-1** | Flat-floor training vs. staircase fine-tuning | Core H1: does staircase-specific training reduce S-FPR? |
| **ABL-2** | Temporal window N = 8, 16, 24, 32 frames | Latency vs. accuracy trade-off |
| **ABL-3** | Consecutive threshold M = 2, 3, 5 | FP reduction vs. detection delay |
| **ABL-4** | YOLOv8n-pose vs. YOLOv8s-pose | Speed vs. skeleton quality trade-off |
| **ABL-5** | With vs. without temporal verification gate | Quantify FP reduction from gate alone |
| **ABL-6** | Camera angle 30° vs. 45° vs. 60° | Effect of mounting angle on detection quality |
| **ABL-7** | Full light vs. dim vs. IR night mode | Effect of lighting on pose estimation quality |

---

## 17. Real-Time Evaluation

**Protocol** (following P12's 10 FPS threshold and P11's profiling methodology):

```
1. Stream live video from CCTV to laptop GPU
2. Run complete pipeline: capture → YOLOv8-pose → ByteTrack → GRU → MQTT trigger
3. Measure FPS using rolling 30-frame average
4. Profile stage-wise timing (following P11's breakdown):
   - YOLOv8-pose inference time (ms/frame)
   - ByteTrack update time (ms/frame)
   - GRU inference time (ms/window)
   - MQTT publish time (ms)
   - Total pipeline latency (ms/frame)
5. Test under three conditions:
   - Single person, full light
   - Single person, dim light
   - Two people on stairs simultaneously
6. Report: mean FPS, min FPS (worst-case), and latency breakdown
```

**Hardware targets**:
- Primary: GTX 1650 laptop (user's own)
- Secondary: RTX 3050 mobile (collaborator's laptop)
- Minimum threshold: ≥ 10 FPS (P12 biomechanical justification)

---

## 18. False-Positive Evaluation

**S-FPR Protocol (novel — no prior paper has this)**:

```
1. Record 50+ staircase-ADL clips (negative class only)
2. Run inference on each clip with system running in monitoring mode
3. Record every alert triggered
4. S-FPR = (number of alert-triggering clips / total ADL clips) × 100%
5. Compare: Baseline-A (flat-floor trained) vs. Baseline-C (staircase fine-tuned)
6. Report S-FPR per activity category:
   - S-FPR (descent), S-FPR (bending), S-FPR (sitting), S-FPR (stumble+recover)
7. This becomes Table X in the paper — first staircase-ADL FPR breakdown in the literature
```

---

## 19. Staircase-Specific Evaluation Summary

This section is the methodological novelty of the paper:

> **Evaluation Protocol STA-EVAL-1** (proposed):
> A fall detection evaluation protocol for staircase environments comprising:  
> (a) a staircase-specific positive set (falls on stairs under varied conditions),  
> (b) a staircase-ADL negative set (6 categories of staircase activities resembling falls),  
> (c) staircase-ADL false-positive rate (S-FPR) as a reporting metric,  
> (d) camera-angle variation evaluation (30°/45°/60° mounting),  
> (e) lighting condition evaluation (full / dim / IR night mode).

This protocol can be adopted by future researchers to standardize staircase fall detection evaluation.

---

## 20. Hardware Architecture

```
[CCTV Camera 1]───────────────────────────────────────┐
                                                       │ USB / RTSP
[CCTV Camera 2]───────────────────────────────────────┤
                                                       ▼
                                          ┌─────────────────────┐
                                          │  Laptop (Main Unit) │
                                          │  GPU: GTX 1650 /    │
                                          │       RTX 3050m     │
                                          │  RAM: 8–16 GB       │
                                          │  OS: Ubuntu / Win   │
                                          │                     │
                                          │  ┌─────────────┐   │
                                          │  │ YOLOv8-pose │   │
                                          │  │ ByteTrack   │   │
                                          │  │ GRU model   │   │
                                          │  │ MQTT client │   │
                                          │  └──────┬──────┘   │
                                          └─────────┼───────────┘
                                                    │ MQTT
                               ┌────────────────────┼──────────────────┐
                               │                    │                  │
                               ▼                    ▼                  ▼
                    ┌─────────────────┐  ┌──────────────────┐  ┌──────────────┐
                    │ ESP32 + Buzzer  │  │ MQTT Broker      │  │ Telegram Bot │
                    │ (Local Alarm)   │  │ (Mosquitto)      │  │ (Remote App) │
                    │ < 1 second      │  │ Routes messages  │  │ < 5 seconds  │
                    └─────────────────┘  └──────────────────┘  └──────────────┘
```

**Component costs (prototype)**:
| Component | Cost (approx.) |
|---|---|
| CCTV camera (USB/RTSP) | ₹1,000–2,500 |
| ESP32 dev board | ₹300–500 |
| Buzzer + LED | ₹50–100 |
| Resistors / wiring | ₹50 |
| Total hardware | ₹1,500–3,500 |

---

## 21. Alert Architecture

```
FALL CONFIRMED
      │
      ├─[immediate]──► ESP32 → Buzzer (LEVEL 1 — Local Alarm)
      │
      ├─[< 5 sec]────► MQTT → Telegram Bot
      │                  Message: "⚠️ FALL DETECTED
      │                           Location: Staircase, Floor 2
      │                           Time: 20:42:15
      │                           Confidence: 94%"
      │                  Attachment: Grad-CAM frame (optional)
      │
      └─[wait 30 sec]─► If ACK received → RESOLVED, log event
                        If NO ACK ──────► ESCALATE
                                            │
                                            ├─► Alert secondary contact
                                            └─► Repeat every 60 sec
                                                until ACK received
```

---

## 22. Acknowledgement Mechanism

**Implementation (Engineering — B)**:
- Recipient receives Telegram message with inline "✅ Acknowledged" button
- Button press sends POST request to local MQTT broker (or direct webhook)
- Laptop receives ACK signal → stops escalation timer → logs event as resolved
- If ACK button not pressed within 30 seconds → escalation triggered

**Research measurement (Experimental — C)**:
- Log all acknowledgement events during testing
- Measure: time from alert delivery to ACK receipt (seconds)
- Measure: proportion of simulated falls acknowledged within 30 seconds vs. escalated

---

## 23. Escalation Mechanism

**Protocol**:
```
LEVEL 2: Primary contact (T+0s)   → Alert sent
LEVEL 3: Secondary contact (T+30s) → If no ACK: escalate to second contact
LEVEL 4: Tertiary / security (T+90s) → If still no ACK: escalate to building security
LEVEL 5: Persistent repeat (T+150s+) → Every 60 seconds until ACK
```

**Research measurement (Experimental — C)**:
- False-positive escalation rate: run staircase ADL set through complete pipeline
- Count how many non-fall events trigger escalation (most dangerous outcome)
- Report: false-positive escalation rate per hour of simulated monitoring

---

## 24. Privacy Considerations

| Concern | Our Approach |
|---|---|
| CCTV footage stored | Processed locally on laptop — no cloud upload of raw video |
| Skeleton-only processing | Only keypoints transmitted to alert broker, not raw frames |
| Alert evidence frame | Grad-CAM heatmap (blurred background) — not raw CCTV frame |
| GDPR / data ethics | Consent required from all subjects; data deleted after evaluation |
| Residential deployment | Alert only to pre-authorized contacts — not broadcast |

---

## 25. Expected Contributions

### A — Research Contributions (Novel, evidenced from Phase 7–8)

**RC1**: **First staircase-specific fall detection evaluation**
- Evidence of novelty: P07 (all 87 papers), P12 (all 11 hardware papers) — zero staircase evaluations
- Claim: "We present, to the best of our knowledge, the first experimental evaluation of a vision-based fall detection system in a staircase environment."

**RC2**: **First staircase-ADL false-positive evaluation and reporting protocol**
- Evidence of novelty: Phase 6 — 0/12 papers test walking-down-stairs confusion
- Claim: "We introduce the staircase-ADL evaluation protocol and the S-FPR metric for benchmarking fall detection systems in vertical environments."

**RC3**: **First integrated fall detection + alert acknowledgement + escalation system**
- Evidence of novelty: P07 (1/22 alarm), P12 (no ACK/escalation in any paper)
- Claim: "We present the first empirically evaluated end-to-end fall safety system integrating detection, local alarm, remote notification, acknowledgement, and multi-level escalation."

### B — Engineering Implementation (not claimed as novel research)

- YOLOv8-pose + ByteTrack + GRU pipeline integration
- ESP32 MQTT alarm circuit
- Telegram Bot escalation logic

### C — Experimental Contributions (Novel measurements)

- Staircase sensitivity/specificity baseline measurement
- Pre/post fine-tuning S-FPR comparison
- First hardware-profiled end-to-end staircase pipeline latency measurement
- False-positive escalation rate in residential monitoring scenario

---

## 26. Risks

| Risk | Probability | Severity | Mitigation |
|---|---|---|---|
| Baseline model already handles staircase ADLs well (S-FPR < 5%) | Medium | High (GAP-03 weakens) | Pre-test immediately; if low, pivot to GAP-01+02 only |
| Dataset too small for statistical significance | High | Medium | Use cross-validation; compare to published papers' dataset sizes (P06 had 1 subject) |
| Young subjects only — reviewer challenges generalizability | High | Medium | Acknowledge explicitly; cite P07 (95% of literature same limitation) |
| Alert pipeline latency too high (> 5 sec notification) | Low | Medium | Optimize MQTT; use local broker; Telegram API is < 1 sec typical |
| Ethics clearance delays data collection | Low | High | Apply early; use anonymous volunteers; no medical data |
| GPU not powerful enough for ≥ 10 FPS | Low | High | YOLOv8n-pose achieves ≥ 30 FPS on GTX 1650 per published benchmarks |
| Paper rejected as "system paper, not research paper" | Medium | High | Frame around H1 (quantitative FPR reduction) and RC1–RC3; submit to Applied Sciences, Sensors, IEEE Access |

---

## 27. Fallback Research Direction

If GAP-01 staircase data collection is not feasible (location access denied, ethics delays, etc.):

**Fallback A**: Simulation-based staircase evaluation
- Use Unreal Engine or Blender to generate synthetic staircase fall clips
- Less ecologically valid but still the first staircase evaluation
- Explicitly acknowledge as simulation-based; frame as "synthetic staircase benchmark"

**Fallback B**: Narrow to alert escalation + benchmark evaluation
- Take an existing trained model (P11's MobileNetV2+GRU, or re-train on Le2i)
- Focus on: implementing the complete alert pipeline + measuring its performance on the public Le2i dataset
- Research contribution shifts to: RC3 only (alert escalation, first empirical measurement)
- Still a novel contribution confirmed by P07 and P12

**Fallback C**: Evaluate existing models on staircase video (no training, only evaluation)
- Collect staircase test clips only (no training data required)
- Run P11-equivalent model on clips, measure FPR
- Research contribution: "First evaluation of existing flat-floor models on staircase environments — a zero-shot generalization study"
- Simpler to execute; still fills the staircase evaluation void

---

## 28. Contribution Classification Summary

```
┌─────────────────────────────────────────────────────────────────┐
│              CONTRIBUTION CLASSIFICATION MAP                     │
├───────────────────┬─────────────────────────────────────────────┤
│ A. RESEARCH       │ • First staircase evaluation (RC1)           │
│    CONTRIBUTION   │ • S-FPR metric + staircase ADL protocol (RC2)│
│    (Novel claims) │ • Alert escalation integration (RC3)         │
├───────────────────┼─────────────────────────────────────────────┤
│ B. ENGINEERING    │ • YOLOv8-pose + ByteTrack + GRU pipeline     │
│    IMPLEMENTATION │ • ESP32 buzzer circuit                       │
│    (Not novel)    │ • Telegram Bot alert logic                   │
│                   │ • MQTT broker setup                          │
├───────────────────┼─────────────────────────────────────────────┤
│ C. EXPERIMENTAL   │ • S-FPR before/after fine-tuning (H1 test)   │
│    CONTRIBUTION   │ • Pipeline latency profiling (H2 test)       │
│    (Novel data)   │ • Alert response time measurement (H3 test)  │
│                   │ • Camera-angle ablation                      │
│                   │ • Lighting condition ablation                │
└───────────────────┴─────────────────────────────────────────────┘
```

---

## 29. Target Journals / Venues

Based on scope, student-project feasibility, and gap strength:

| Venue | Type | Fit | Impact |
|---|---|---|---|
| **IEEE Access** | Open-access journal | ✅ Best fit — accepts applied systems papers; P01, P02 published here | IF ~3.4 |
| **MDPI Sensors** | Open-access journal | ✅ Excellent fit — P12 published here; covers embedded systems + CV | IF ~3.4 |
| **Applied Sciences (MDPI)** | Open-access journal | ✅ Good fit — multidisciplinary, accepts prototype systems | IF ~2.5 |
| **IEEE AVSS** | Conference | 🟡 Good — Video/surveillance focus; competitive | Tier B |
| **ICIP / ICCV Workshop** | Conference | 🟡 Stretch — stronger engineering component | Tier A |

**Recommendation**: Target **IEEE Access** or **MDPI Sensors** for first submission — both have published the papers in our literature set, accept applied system contributions with strong evaluation, and are peer-reviewed open access.

---

## 30. Timeline (Estimated — Prototype Phase)

```
Month 1 — Setup & Pre-Test
  ├── Week 1: Set up YOLOv8-pose + ByteTrack + GRU baseline
  ├── Week 2: Pre-test on staircase walking clips (validates GAP-03)
  ├── Week 3: Ethics clearance application + location scouting
  └── Week 4: Camera setup + initial data collection

Month 2 — Data Collection & Training
  ├── Week 1–2: Record staircase fall + ADL clips
  ├── Week 3: Annotate dataset (frame-level labels)
  └── Week 4: Fine-tuning on staircase dataset (Stage 2 training)

Month 3 — Evaluation & Alert Integration
  ├── Week 1: Run evaluation protocol (TEST 1–4)
  ├── Week 2: ESP32 + MQTT + Telegram Bot integration
  ├── Week 3: Alert pipeline evaluation (TEST 5)
  └── Week 4: Ablation studies (ABL-1 through ABL-5)

Month 4 — Writing & Submission
  ├── Week 1–2: Write paper (following Phase 1–9 structure)
  ├── Week 3: Internal review + revisions
  └── Week 4: Submit to IEEE Access / Sensors
```

---

*End of Phase 9 — Final Research Roadmap*  
*Literature analysis phases complete: Phase 1 through Phase 9.*  
*Next step: Research Gap Heatmap (as defined in user rules)*
