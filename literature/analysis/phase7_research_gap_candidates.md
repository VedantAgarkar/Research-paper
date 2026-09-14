# Phase 7: Research Gap Candidates

> **Project**: Real-Time CCTV-Based Elderly Fall Detection in Staircase / Common-Area Environments  
> **Phase**: Phase 7 — Evidence-Based Research Gap Discovery  
> **Evidence base**: Phases 1–6 (12 papers analyzed)  
> **Important**: Gaps here are CANDIDATES. They undergo adversarial stress-testing in Phase 8.

---

## Methodology

Each gap candidate is evaluated on:
- **Novelty (N)**: How original is the contribution? (1–5)
- **Importance (I)**: How critical is solving this? (1–5)
- **Feasibility (F)**: Can a student project realistically test this? (1–5)
- **Evidence Strength (E)**: How many papers support the existence of this gap? (1–5)

**Overall Priority** = N × I × F × E (normalized)

---

## GAP-01: Staircase-Specific Fall Detection

### Gap Statement
No published study has experimentally evaluated a vision-based fall detection pipeline in a real staircase or multi-level corridor environment. The entire body of literature — empirical and systematic — assumes flat floor environments.

### Existing State of Literature
| What exists | Papers | Limitation |
|---|---|---|
| Flat-floor indoor fall detection | P01–P11 | All assume flat horizontal plane |
| Surveys confirming staircase absence | P07, P12 | P07: explicitly absent from all 87 papers; P12: explicitly absent from all hardware-validated papers |
| "Staircase-adjacent" fall datasets | P02 (AI Hub — some stair clips?) | Not annotated or evaluated as staircase-specific |

### Evidence
- **P07 §5 (pp. 9000–9002)**: "No reviewed study evaluates fall detection specifically in staircase or multi-level environments."
- **P12 §5.3 (pp. 12–13)**: "No published hardware-tested vision system evaluates complex multi-level staircase environments."
- **P11 §5 (pp. 12–13)**: "Does not evaluate staircases or banister occlusion."
- **Implied by ALL empirical papers (P01–P11)**: None report staircase scenarios in their datasets.

### Papers Addressing This: 0 / 12 (0%)
### Papers NOT Addressing This: 12 / 12 (100%)

### Why This Gap Matters
The staircase is arguably the highest-risk location for elderly falls:
- **Biomechanics**: A fall on stairs causes more severe injury than a flat-floor fall (acceleration + multi-step impact)
- **Unique confounders that flat-floor systems cannot handle**:
  - Descending stairs mimics the forward-incline posture of a fall
  - Banister grip causes partial self-occlusion during descent
  - Vertical height-change is normal but resembles falling trajectory
  - Camera is typically wall-mounted at steep angles in stairwells
  - Multiple people can be on stairs at different heights simultaneously
- **No existing model was trained or validated on staircase data** — deploying any existing system on a staircase without staircase-specific training would produce unknown (likely high) false-positive rates

### Technical Difficulty
**HIGH** — Multiple interacting challenges:
1. Pose estimation accuracy degrades at steep camera angles (P07)
2. Banisters cause persistent partial occlusion
3. Normal descending gait has a distinctive "falling-like" angular trajectory
4. Multi-step environments have inconsistent backgrounds (each step creates a new visual region)
5. No public training data exists — dataset must be built from scratch

### Novelty Potential
**HIGH (5/5)** — Zero prior work. First paper to evaluate staircase fall detection with a CCTV-based system automatically claims "first staircase-specific evaluation" status.

### Feasibility (Student Project)
**MEDIUM-HIGH (4/5)**
- Accessible location: any university stairwell, building corridor
- Equipment: 1–2 standard CCTV cameras + laptop
- Data collection: 30–50 video clips (staged falls + normal stair activities)
- Can re-use existing backbone (YOLOv8-pose / MobileNetV2) and adapt for staircase context
- Main challenge: collecting enough data with sufficient variety

### Potential Experimental Design
1. Set up 2 CCTV cameras in a real stairwell (different angles)
2. Collect 30+ fall clips: forward falls, backward falls, sideward falls, tumbling, slow collapse
3. Collect 50+ non-fall clips: walking down/up stairs, bending to pick up items, sitting on steps, stumbling + recovering, using phone while descending
4. Train baseline model (MobileNetV2+GRU) on public datasets (Le2i + UR Fall)
5. Fine-tune on staircase dataset
6. Evaluate staircase-specific precision/recall and false-positive rate
7. Ablation: compare model performance with vs. without staircase fine-tuning
8. Compare detection accuracy at different camera angles

### Risks
- Ethical clearance required for human-subject video (usually straightforward for non-medical studies)
- Real falls cannot be used for safety reasons — staged falls introduce a domain gap
- Small dataset size — statistical power may be limited
- Staircase lighting varies significantly (often dim) — may need IR-capable camera

### What Could Invalidate This Gap
- If a paper exists that was not captured in our 12-paper set and evaluated staircase fall detection (possible — check Scopus)
- If a general model (e.g., YOLOv8-pose + GRU) generalizes perfectly to staircases without fine-tuning (unlikely given the pose angle distortion documented in P07)

### Scores
| Novelty | Importance | Feasibility | Evidence Strength |
|---|---|---|---|
| **5** | **5** | **4** | **5** |

**Overall Priority: VERY HIGH** ⭐⭐⭐⭐⭐

---

## GAP-02: Integrated Alert Acknowledgement and Escalation Pipeline

### Gap Statement
No published fall detection system implements an automated alert escalation mechanism — where an unacknowledged fall alert automatically escalates to a secondary contact or authority. Two independent systematic reviews confirm this is absent from the entire published literature.

### Existing State of Literature
| What exists | Papers | Limitation |
|---|---|---|
| Basic alarm / buzzer | P12 surveyed (rare) | Only 1/22 vision studies had real-time alarm transmission (P07) |
| SMS / Email alerts | P12 (mentioned in 2–3 papers) | Single-shot only — no acknowledgement loop |
| Grad-CAM visual evidence | P11 | Not transmitted — only visualized locally |
| Full escalation pipeline | **None** | 0/12 papers; confirmed absent by P07 and P12 |

### Evidence
- **P07 §5**: "Only 1 of 22 vision-based studies demonstrated real-time alarm transmission despite 40.9% claiming real-time performance."
- **P12 §5.3**: "Alert systems are rudimentary single-shot alerts without acknowledgement or escalation."
- **P11 §5 (pp. 12–13)**: "Does not implement automated alert escalation or local physical buzzer hardware."
- **P12 §5.3**: "No published hardware-tested vision system addresses acknowledgement or multi-level escalation."

### Papers Addressing Acknowledgement/Escalation: 0 / 12 (0%)
### Papers NOT Addressing This: 12 / 12 (100%)

### Why This Gap Matters
This is not a "nice-to-have" feature — it is the difference between:
- A fall detection **classifier** (what every existing paper builds)
- A fall detection **safety system** (what real-world deployment actually requires)

In a real scenario: an elderly person falls at 8:42 PM on a staircase. The model correctly detects the fall. Without acknowledgement and escalation:
- Alert is sent once → nearby contact is asleep / phone silenced → no response → person lies injured for hours
- This is the documented real-world failure mode of single-shot alert systems

A proper response loop: **Detection → Local Alarm → Remote Alert → [Wait X seconds] → If no ACK → Escalate to secondary contact / security desk → [Wait Y seconds] → Escalate again**

No published system implements this chain.

### Technical Difficulty
**MEDIUM (3/5)** — The CV pipeline is the hard part; the alert pipeline is engineering:
- MQTT / WebSocket broker for real-time alert transmission
- Simple timeout + callback logic
- WhatsApp API / Telegram Bot / SMS Gateway for notification
- ESP32 / Raspberry Pi for local buzzer hardware
- Acknowledgement button / mobile app interaction

### Novelty Potential
**MEDIUM-HIGH (4/5)** — The engineering is not novel on its own. The novelty is:
- First system to **integrate** fall detection with a full acknowledgement-escalation loop
- First **empirical evaluation** of false-positive alert rates in a real escalation chain
- Research question: "How does a structured escalation protocol affect response time and alert fatigue in a residential building scenario?"

### Feasibility (Student Project)
**HIGH (5/5)**
- Can be implemented in software (Python, MQTT, REST API)
- Hardware: ESP32 + buzzer (< ₹500)
- Notification: Telegram Bot API (free), WhatsApp Business API (low cost)
- No special ethics clearance needed for the engineering component
- Can be measured: response time, false-positive rate, escalation triggers

### Potential Experimental Design
1. Implement full pipeline: YOLOv8-pose → GRU → Fall trigger → MQTT broker → Local buzzer (ESP32) → Telegram alert → Wait 30s → If no ACK → Escalate
2. Measure in controlled scenario: alert latency, acknowledgement response time, escalation trigger accuracy
3. Simulate false-positive scenarios: walking down stairs, bending, sitting — measure how many generate spurious escalations
4. Evaluate fall-to-alert delay (from detection to buzzer activation, to notification received)
5. Compare: single-shot alert baseline vs. acknowledgement-escalation system — measure outcome scenarios

### Risks
- Notification APIs (WhatsApp/SMS) may have rate limits or costs
- Escalation logic is deterministic engineering — reviewers may challenge its "research" value
- Must frame as: "first empirical evaluation of escalation pipeline integration, with metrics"

### What Could Invalidate This Gap
- If the gap is purely engineering (no scientific hypothesis) — reviewers might reject it as a "system paper" not a "research paper"
  - **Mitigation**: Frame the research question as studying false-positive escalation rates and response time in a realistic fall monitoring scenario — this is empirical and measurable

### Scores
| Novelty | Importance | Feasibility | Evidence Strength |
|---|---|---|---|
| **4** | **5** | **5** | **5** |

**Overall Priority: VERY HIGH** ⭐⭐⭐⭐⭐

---

## GAP-03: False-Positive Discrimination in Staircase-Specific ADL Confounders

### Gap Statement
No published study evaluates fall detection against the specific set of normal staircase activities that closely resemble falls in temporal posture profiles: (a) walking down stairs, (b) bending to pick up a dropped item on a step, (c) sitting on a step to rest, (d) stumbling but recovering using the banister. These are the exact ADL confounders that will generate false positives in a staircase deployment.

### Existing State of Literature
| What tested | Papers | Limitation |
|---|---|---|
| Sitting confusion | P02, P04, P05, P10, P11 | Flat-floor sitting only — not sitting on stairs |
| Lying-down confusion | P02, P04, P05, P10, P11 | Flat-floor lying — not after a stair stumble |
| Bending confusion | P07 (noted), P10, P11 | Standing bending — not stair-step bending |
| Stumbling confusion | P07 (noted only) | No empirical evaluation anywhere |
| Walking-down-stairs confusion | **0/12** | **Not a single paper** |
| Banister-grip during descent | **0/12** | **Not mentioned anywhere** |

### Evidence
- **P06**: Only 2 non-fall scenarios evaluated — accuracy of 97.4% is meaningless with this few negatives
- **P07 §5**: "Slow falls and gradual postural changes remain unresolved sources of false positives in the literature"
- **P12 §5.3**: "No paper evaluates multi-person or complex multi-level staircase environments"
- **Phase 6 analysis**: Walking-down-stairs confusion = 0% coverage across all 12 papers

### Papers Addressing Staircase-Specific ADL Confounders: 0 / 12 (0%)

### Why This Gap Matters
A fall detection model trained only on flat-floor data will be systematically exposed to:
- Descent posture (forward lean, height-change per step) → triggers fall classifier
- Banister grip (arm raised, torso at angle) → appears like bracing-for-fall posture
- Step-by-step height reduction → mimics the downward trajectory of a fall

These are not edge cases — they are the **dominant activity** in a staircase environment. Without explicit negative training data for these activities, any existing model deployed on a staircase would have an unacceptably high false-positive rate.

This gap is closely linked to GAP-01 but is specifically about false-positive evaluation methodology, not just environmental coverage.

### Technical Difficulty
**MEDIUM (3/5)** — Requires:
- A dataset with staircase-specific negative activities (buildable with 50+ clips)
- An evaluation protocol that separates staircase-ADL false positives from general accuracy
- A metric: "Staircase-ADL false-positive rate" as a new reporting metric

### Novelty Potential
**HIGH (4/5)**  
- Proposes and evaluates a new category of ADL confounder specific to vertical environments
- Introduces a new evaluation protocol: staircase-specific negative activity set
- Produces the first empirical measurement of false-positive rates for this activity class

### Feasibility (Student Project)
**HIGH (5/5)**
- Same dataset as GAP-01 (shared collection effort)
- Requires 50 clips of staircase-specific normal activities
- Standard evaluation metrics (precision/recall/F1 + staircase-specific FPR)

### Potential Experimental Design
1. Define staircase-specific ADL set: (i) walking down, (ii) walking up, (iii) bending/picking up, (iv) sitting on step, (v) stumble + recover, (vi) carrying heavy load while descending
2. Collect 50+ clips of each (or as many as feasible)
3. Run existing model (MobileNetV2+GRU trained on Le2i) against this activity set
4. Record false-positive rate per activity class
5. Fine-tune with staircase-ADL negatives → re-evaluate FPR
6. Show: fine-tuning with staircase-specific negatives reduces FPR by X%

### Risks
- A general model might actually perform well on staircase ADLs (unlikely but possible)
- If FPR is already low without staircase-specific training, the gap is weaker than expected

### What Could Invalidate This Gap
- If a general model trained on rich flat-floor ADLs happens to generalize well to staircase ADLs
  - **Mitigation**: Pre-test this before committing to the research angle — if the baseline FPR is already low, pivot to another gap

### Scores
| Novelty | Importance | Feasibility | Evidence Strength |
|---|---|---|---|
| **4** | **5** | **5** | **4** |

**Overall Priority: HIGH** ⭐⭐⭐⭐

---

## GAP-04: Real-Time Validated Fall Detection on Laptop/Consumer GPU in Staircase Context

### Gap Statement
Only 1.87% of papers claiming real-time performance have validated on physical hardware (P12). Among those 11 papers, none deploy in a staircase context. The combination of real-time validation + staircase deployment has never been demonstrated.

### Existing State of Literature
| What exists | Papers | Limitation |
|---|---|---|
| Real-time claim without hardware | 98% of literature | P12 PRISMA: unvalidated |
| Hardware-validated (any scenario) | 11 papers (from P12 survey) | No staircase; controlled flat environments |
| Hardware-validated + staircase | **0 papers** | Confirmed void |
| Edge GPU deployment | P11 (MobileNetV2+GRU, ~32–93 FPS) | Le2i/CAUCA — no staircase |
| Backbone bottleneck analysis | P11 | MobileNetV2 = 96.8% of inference time |

### Evidence
- **P12 §4.1**: "Only 11 of 588 (1.87%) papers validated on physical hardware"
- **P11 §4**: MobileNetV2 backbone = 36.22ms; GRU = 0.93ms total per window → backbone dominates
- **P12 §5.1**: 10 FPS biomechanical minimum threshold established

### Papers Addressing Validated Real-Time Staircase: 0 / 12
### Papers Claiming Real-Time (Unvalidated): ~8 / 12

### Why This Gap Matters
"Works in a lab at 32 FPS" ≠ "Works in a staircase at 10+ FPS while also running the alert pipeline." No one has measured the overhead of: person tracking + pose estimation + temporal GRU + alert transmission simultaneously in a real environment.

### Technical Difficulty
**MEDIUM (3/5)** — Requires:
- Profiling the full pipeline end-to-end (detection → pose → GRU → alert) on a laptop GPU
- Measuring FPS drop under real staircase conditions (multi-person, partial occlusion, dim light)
- Applying at least one optimization (model quantization, TensorRT, or lighter backbone)

### Novelty Potential
**MEDIUM (3/5)**  
- Hardware benchmarking alone is not novel
- The novel contribution is: "first end-to-end latency measurement of a staircase fall detection + alert pipeline on consumer-grade hardware"

### Feasibility (Student Project)
**HIGH (5/5)**
- Direct hardware: the user's laptop (GTX 1650) or friend's (RTX 3050)
- Tools: PyTorch profiler, NVIDIA Nsight, simple FPS counter
- No additional data collection required beyond GAP-01/03

### Scores
| Novelty | Importance | Feasibility | Evidence Strength |
|---|---|---|---|
| **3** | **4** | **5** | **5** |

**Overall Priority: HIGH** ⭐⭐⭐⭐

---

## GAP-05: Multi-Person Tracking in Fall Detection Context

### Gap Statement
Multi-person tracking in fall detection is addressed by fewer than 10% of the broader literature (P07), and by only 1 paper (P08) in our 12-paper set — and P08 addresses tracking only, not fall classification. No paper demonstrates complete multi-person fall detection and tracking in a shared environment.

### Existing State of Literature
| What exists | Papers | Limitation |
|---|---|---|
| Single-person fall detection | All 11 empirical papers | Single-subject assumption |
| Multi-person detection (non-fall) | P08 (EfficientDet + DeepSORT) | Detection/tracking only, no fall classification |
| Multi-person fall detection | **0 papers** | Complete void |

### Why This Gap Matters
A shared building staircase will regularly have 2–3 people simultaneously. Existing systems would either:
- Fail to detect a fall if another person is nearby (identity confusion)
- Generate false positives when one person's motion overlaps another's skeleton
- Track the wrong person across frames after an occlusion event

### Technical Difficulty
**HIGH (4/5)** — Multi-person pose estimation + per-person temporal tracking is significantly more complex than single-person

### Novelty Potential
**MEDIUM (3/5)** — Multi-person tracking for activity recognition is studied; multi-person fall detection specifically is a gap

### Feasibility (Student Project)
**MEDIUM (3/5)** — Doubles the complexity; requires multi-person dataset collection with simultaneous falls

### Scores
| Novelty | Importance | Feasibility | Evidence Strength |
|---|---|---|---|
| **3** | **4** | **3** | **4** |

**Overall Priority: MEDIUM-HIGH** ⭐⭐⭐

---

## GAP-06: Night / Low-Light Fall Detection with Standard RGB CCTV

### Gap Statement
Only P05 systematically evaluates night/low-light fall detection — and it requires non-standard IR/depth hardware not available in standard CCTV. No paper evaluates fall detection using **standard RGB CCTV cameras in low-light or IR-illuminated conditions typical of building stairwells**.

### Existing State of Literature
| What exists | Papers | Limitation |
|---|---|---|
| Night evaluation with IR sensors | P05 | Requires Kinect/depth — not standard CCTV |
| Thermal/depth night evaluation | P10 | Requires non-CCTV hardware |
| Standard RGB night evaluation | **0 papers** | Confirmed absent |

### Why This Gap Matters
Our scenario occurs at 8:42 PM. Stairwell lighting is typically:
- Fluorescent overhead (inconsistent coverage)
- Motion-sensor activated (may be off when person first arrives)
- Standard CCTV with IR cut filter (switches to IR night mode)

When a CCTV camera switches to IR night mode:
- Image becomes grayscale
- Different noise characteristics than RGB
- Pose estimators trained on RGB may degrade

### Technical Difficulty
**MEDIUM (3/5)**
- Requires low-light or IR-mode camera footage
- Can be partially simulated with image brightness/contrast augmentation
- IR-mode footage from a CCTV camera is collectable in any dim stairwell at night

### Novelty Potential
**MEDIUM (3/5)** — Not fundamentally novel, but addresses a realistic gap in the context of our specific deployment

### Feasibility (Student Project)
**MEDIUM-HIGH (4/5)**
- A CCTV camera with IR night mode is sufficient
- Record staircase footage at night / in dim conditions
- Standard evaluation of model degradation in low-light

### Scores
| Novelty | Importance | Feasibility | Evidence Strength |
|---|---|---|---|
| **3** | **4** | **4** | **3** |

**Overall Priority: MEDIUM** ⭐⭐⭐

---

## GAP-07: Temporal Fall Verification vs. Instantaneous Detection

### Gap Statement
Most papers treat fall detection as a single-frame classification problem. Only P10 (fall score over time), P11 (GRU sliding window), and partially P02 (LSTM over skeleton sequence) implement temporal verification. The specific question of "how many consecutive high-confidence frames constitute a confirmed fall before triggering an alert" — and its effect on false-positive reduction — remains unstudied.

### Why This Gap Matters
In a staircase scenario, a single frame of a person bending or descending may look identical to a fall frame. Temporal verification (requiring N consecutive frames above threshold) is the primary false-positive reduction mechanism. Its optimal calibration in a staircase context is unknown.

### Technical Difficulty
**LOW-MEDIUM (2/5)** — Primarily a hyperparameter study + ablation

### Novelty Potential
**MEDIUM (3/5)** — Frame-level vs. temporal verification ablation is novel in a staircase context

### Feasibility
**VERY HIGH (5/5)** — Can be done entirely in software with existing models

### Scores
| Novelty | Importance | Feasibility | Evidence Strength |
|---|---|---|---|
| **3** | **4** | **5** | **3** |

**Overall Priority: MEDIUM** ⭐⭐⭐

---

## 7.1 Gap Priority Ranking Table

| Rank | Gap ID | Gap Description | N | I | F | E | Priority |
|---|---|---|---|---|---|---|---|
| **1** | GAP-01 | Staircase-specific fall detection pipeline | 5 | 5 | 4 | 5 | ⭐⭐⭐⭐⭐ VERY HIGH |
| **2** | GAP-02 | Alert acknowledgement + escalation pipeline | 4 | 5 | 5 | 5 | ⭐⭐⭐⭐⭐ VERY HIGH |
| **3** | GAP-03 | Staircase-specific ADL false-positive evaluation | 4 | 5 | 5 | 4 | ⭐⭐⭐⭐ HIGH |
| **4** | GAP-04 | Real-time validation on consumer GPU + staircase | 3 | 4 | 5 | 5 | ⭐⭐⭐⭐ HIGH |
| **5** | GAP-05 | Multi-person tracking in fall detection context | 3 | 4 | 3 | 4 | ⭐⭐⭐ MEDIUM-HIGH |
| **6** | GAP-06 | Night/low-light with standard RGB CCTV | 3 | 4 | 4 | 3 | ⭐⭐⭐ MEDIUM |
| **7** | GAP-07 | Temporal verification ablation in staircase context | 3 | 4 | 5 | 3 | ⭐⭐⭐ MEDIUM |

---

## 7.2 Gap Intersection Analysis

The most powerful research contributions emerge from the intersection of multiple gaps:

```
GAP-01 (Staircase)
    ├── + GAP-03 (Staircase ADL FP)     → Staircase fall detection WITH false-positive evaluation
    │       = "A staircase-specific fall detection dataset and evaluation protocol"
    │         (Novel dataset + novel evaluation methodology)
    │
    ├── + GAP-02 (Alert escalation)     → Staircase detection + full emergency response loop
    │       = "End-to-end CCTV staircase fall detection with alert escalation"
    │         (Novel deployment scenario + novel system completeness)
    │
    ├── + GAP-04 (Real-time validation) → Staircase + hardware-validated + profiled
    │       = "Real-time staircase fall detection: first hardware-validated evaluation"
    │         (Novel hardware benchmark in novel environment)
    │
    └── + GAP-01+02+03+04 combined      → THE STRONGEST POSSIBLE GAP
            = "A complete, real-time, hardware-validated staircase fall detection system
               with staircase-specific ADL evaluation and alert escalation pipeline"
              This is the proposed research direction.
```

---

## 7.3 Proposed Unified Research Gap Statement

> **Research Gap**: The existing fall detection literature, despite extensive study of indoor environments, has produced zero experimental evaluations of vision-based fall detection in staircase or multi-level corridor environments. This gap is compounded by three additional absent dimensions: (1) no system evaluates the staircase-specific activities that form the primary sources of false positives in this environment (stair descent, banister-assisted movement, step-level ADLs); (2) no system demonstrates real-time operation validated on consumer-grade hardware in this scenario; and (3) no published system implements an alert acknowledgement and escalation mechanism necessary for real-world elderly safety applications. The convergence of these four individually documented gaps defines a compound research void with direct implications for practical elderly fall safety in residential buildings.

---

## 7.4 Candidate Research Question

> **RQ**: Can a lightweight real-time CCTV-based fall detection system, specifically designed and evaluated for staircase environments, achieve clinically acceptable sensitivity (≥ 85%) and specificity (≥ 90%) against staircase-specific activities, while integrating a complete alert acknowledgement and escalation pipeline on consumer-grade hardware?

---

## 7.5 Candidate Hypothesis

> **H1**: A fall detection model fine-tuned on a staircase-specific dataset (including staircase-ADL negatives) will achieve significantly lower false-positive rates against staircase activities than a model trained exclusively on flat-floor datasets, when evaluated under equivalent conditions.

> **H2**: An integrated alert acknowledgement and escalation pipeline can reduce mean response delay from fall detection to confirmed human acknowledgement to below 60 seconds in a residential building scenario.

---

*End of Phase 7 — Research Gap Candidates*  
*Next: Phase 8 — Adversarial Stress Test (attempting to disprove each gap)*
