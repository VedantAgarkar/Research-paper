# Phase 5: Failure Modes & Limitations Analysis

> **Project**: Real-Time CCTV-Based Elderly Fall Detection in Staircase / Common-Area Environments  
> **Phase**: Phase 5 — Failure Modes, Limitations, and Edge Case Analysis  
> **Papers Analyzed**: 12 (PAPER_01 – PAPER_12)  
> **Classification System**: A = Demonstrated Failure | B = Explicitly Acknowledged | C = Implied by Design

---

## 5.1 Per-Paper Limitation Profiles

---

### PAPER_01 — BiMP Dataset (Dibble & Bazzocchi, 2025, IEEE Access)

| # | Limitation | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | No staircase testing — flat lab floor only | B | Section VII, p. 26576 | 🔴 Critical |
| L2 | Falls simulated by young healthy adults only — no elderly subjects | B | Section VII, p. 26576 | 🔴 Critical |
| L3 | Audio tested in acoustically controlled room — would degrade with staircase echo, ambient noise (TV, traffic, conversation) | C | Section III (setup) | 🔴 Critical |
| L4 | Multi-person not evaluated — single-subject only | C | Experimental design (no multi-person mention) | 🟠 High |
| L5 | No occlusion testing (banister, furniture, other persons) | C | Section VI (tested scenarios) | 🟠 High |
| L6 | No real-world deployment — zero alert/alarm/escalation pipeline | B | Section VII | 🟠 High |
| L7 | Night/low-light not tested (standard RGB cameras used) | C | Section II (hardware description) | 🟠 High |
| L8 | Audio microphones require physical installation — not available in standard CCTV | C | Section II (microphone hardware) | 🟡 Medium |

---

### PAPER_02 — AlphaPose+LSTM on AI Hub CCTV (Kim et al., 2024, IEEE Access)

| # | Limitation | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | AlphaPose achieves only ~3 FPS — **not real-time** by the 10 FPS biomechanical threshold (P12) | A | Section IV.B.1; Paper achieves 3 FPS on GPU | 🔴 Critical |
| L2 | Staircase-specific evaluation absent — diverse CCTV locations but no staircase annotation | B | Section IV.B.1 | 🔴 Critical |
| L3 | AlphaPose fails under dim indoor light and partial body occlusion — explicitly tested and noted | A | Section IV.B.1 | 🔴 Critical |
| L4 | AI Hub CCTV dataset is restricted-access / non-reproducible — results cannot be externally validated | B | Section V | 🟠 High |
| L5 | No elderly subjects — scripted falls by non-elderly volunteers | C | Section III.A (subject description) | 🟠 High |
| L6 | Single-person assumption — multi-person tracking not addressed | C | Experimental design | 🟠 High |
| L7 | SynADL (synthetic activities dataset) introduces domain gap — model exposed to synthetic non-falls | B | Section V | 🟡 Medium |
| L8 | No local alarm, remote alert, acknowledgement, or escalation | C | System architecture described — no alert component | 🟠 High |

---

### PAPER_03 — Custom CNN Pipeline (Private Dataset)

| # | Limitation | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | Private dataset — not reproducible by any external researcher | B | Section V | 🔴 Critical |
| L2 | Staircase not reported | C | Dataset description has no staircase mention | 🔴 Critical |
| L3 | Occlusion acknowledged as limitation — bounding box fails with back-to-camera or self-occlusion | B | Section V | 🟠 High |
| L4 | No elderly subjects, no age data reported | C | Subject description | 🟠 High |
| L5 | Varied indoor lighting acknowledged as limitation but not systematically tested | B | Section V | 🟠 High |
| L6 | No cross-subject evaluation protocol reported | C | Experimental design | 🟡 Medium |
| L7 | No alert, alarm, or escalation pipeline | C | System scope | 🟠 High |
| L8 | Subject count and video count not explicitly reported — cannot assess generalizability | C | Dataset description | 🟡 Medium |

---

### PAPER_04 — Floor Tile Pressure Sensor Array (Non-Vision)

| # | Limitation | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | **Fundamental incompatibility with staircase** — tile sensor physically requires flat floor installation | A | Section III (hardware constraints) | 🔴 Critical |
| L2 | **Non-vision** — incompatible with CCTV-based target system | A | Core methodology | 🔴 Critical |
| L3 | 6 young subjects aged 25–40 only — no elderly subjects | B | Section V.A | 🔴 Critical |
| L4 | Private dataset; single apartment environment; small sample size | B | Section VI | 🟠 High |
| L5 | Cannot handle multiple persons simultaneously — pressure readings are additive, not separable | C | System design | 🟠 High |
| L6 | No real-time performance benchmark | C | No FPS or latency reported | 🟠 High |
| L7 | Requires infrastructure modification — impractical for retrofitting existing buildings | B | Discussion | 🟡 Medium |

---

### PAPER_05 — Multimodal RGB+Depth+IR Night Dataset (Charfi et al., 2023)

| # | Limitation | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | Falls performed exclusively by young subjects — elderly only perform ADL activities, not falls | B | Section VI | 🔴 Critical |
| L2 | Staircase not reported — controlled flat-floor lab room | C | Dataset description | 🔴 Critical |
| L3 | Top-down ceiling cameras only — does not generalize to wall-mounted CCTV angles typical in staircase corridors | C | Section II.A (camera placement) | 🟠 High |
| L4 | Multi-person evaluation absent | C | Experimental design | 🟠 High |
| L5 | Controlled single-room lab setting — no environment variation | C | Dataset description | 🟠 High |
| L6 | Depth + IR sensors required — not available in standard CCTV infrastructure | B | Hardware requirements | 🟠 High |
| L7 | No alert, alarm, or escalation pipeline | C | System scope | 🟠 High |

*Note: L6 is critical for CCTV deployability — standard building cameras are RGB only.*

---

### PAPER_06 — Multiple Cameras Dataset (Martínez-Villaseñor et al., 2022)

| # | Limitation | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | **Extreme accuracy inflation** — 97.4% accuracy on only **22 fall videos + 2 non-fall videos** from **1 subject** | A | Section V (dataset description) | 🔴 Critical |
| L2 | Only 2 non-fall activity scenarios — model has almost no negative training data | A | Dataset description | 🔴 Critical |
| L3 | No staircase testing | C | Dataset description | 🔴 Critical |
| L4 | No elderly subjects | C | Subject description | 🟠 High |
| L5 | 1 single subject — zero generalizability across body types, clothing, or fall styles | A | Dataset description | 🔴 Critical |
| L6 | Confusion between slow falls / gradual lying-down not tested | C | Only 2 non-fall classes tested | 🟠 High |
| L7 | Multi-person evaluation absent | C | Single-subject dataset | 🟠 High |
| L8 | No alert, alarm, or escalation | C | System scope | 🟠 High |

---

### PAPER_07 — Survey (Islam et al., 2024, Artificial Intelligence Review)

| # | Limitation (of literature as surveyed) | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | **95% of all papers lack elderly subjects** — falling performed by young volunteers | A (Meta-finding) | Section 5 | 🔴 Critical |
| L2 | **Staircase environments explicitly absent** from all 87 analyzed papers | A (Meta-finding) | Section 5 | 🔴 Critical |
| L3 | Skeleton tracking breaks down under occlusion and steep camera angles — staircase directly implies this | B | Section 5 | 🔴 Critical |
| L4 | Night/low-light: depth cameras partially address but systematic testing is rare | B | Section 5 | 🟠 High |
| L5 | Multi-person: fewer than 10% of papers address multi-person tracking in fall detection context | B | Section 5 | 🟠 High |
| L6 | Privacy: 50% of papers lack any privacy consideration | B | Section 5 | 🟡 Medium |
| L7 | Generalization: most models trained and tested on same controlled dataset — cross-environment never validated | A (Meta-finding) | Section 5 | 🟠 High |
| L8 | Alert/communication: only 1 of 22 vision-based studies demonstrated a real-time alarm transmission | A (Meta-finding) | Section 5 | 🔴 Critical |
| L9 | Slow / gradual falls (sitting, kneeling, bending) cause persistent false positives — no paper fully resolves | B | Section 5 | 🟠 High |

---

### PAPER_08 — EfficientDet Multi-Person Detector (Puig-Davi et al., 2021)

| # | Limitation | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | **Only addresses person detection/tracking — no fall classification pipeline** | A | Abstract; system scope | 🟠 High |
| L2 | Neither dataset (Penn-Fudan, MOT17) is a fall detection dataset — no fall events | A | Dataset description | 🟠 High |
| L3 | No elderly subjects; no fall classification; no staircase | C | Experimental design | 🔴 Critical |
| L4 | Multi-person tracking loses ID under dense occlusion (crowded corridor) | B | Section V | 🔴 Critical |
| L5 | No alert, alarm, or escalation pipeline | C | System scope | 🟠 High |
| L6 | GPU required for EfficientDet real-time performance — CPU-only deployment would be sub-real-time | C | Hardware benchmarks | 🟡 Medium |

---

### PAPER_09 — GAN Temporal Reasoning (Generative Adversarial Approach)

| # | Limitation | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | Staircase not reported — flat indoor room only | C | Dataset description | 🔴 Critical |
| L2 | No elderly subjects | C | Subject description | 🟠 High |
| L3 | No occlusion testing | C | Tested scenarios | 🟠 High |
| L4 | No night/low-light systematic testing | C | Dataset setup | 🟠 High |
| L5 | GAN training instability — convergence not guaranteed across domain shifts | C | GAN methodology | 🟡 Medium |
| L6 | No cross-subject evaluation protocol reported | C | Experimental design | 🟡 Medium |
| L7 | No alert, alarm, or escalation | C | System scope | 🟠 High |
| L8 | No real-time hardware benchmark | C | No FPS reported | 🟠 High |

---

### PAPER_10 — DCLSTMAE Depth/Thermal Autoencoder (Li et al., 2022)

| # | Limitation | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | **Requires depth or thermal sensors** — incompatible with standard CCTV infrastructure | B | Section 4, p. 739 | 🔴 Critical |
| L2 | Staircase not reported — flat controlled environments only | C | Dataset description | 🔴 Critical |
| L3 | Reconstruction threshold sensitive to sudden camera movement or novel non-fall activities | B | Section 4, p. 739 | 🟠 High |
| L4 | Kinect depth holes acknowledged — partial depth hole-filling applied but not fully resolved | B | Section 2, 3.1 | 🟡 Medium |
| L5 | Datasets extremely small (UR = 70 videos; Thermal = 44 videos) — poor generalizability | B | Section 3.1 | 🔴 Critical |
| L6 | No elderly subjects; no staircase; no multi-person | C | Experimental design | 🟠 High |
| L7 | No alarm, escalation, or edge benchmarking | B | Section 4, p. 739 | 🟠 High |
| L8 | Unsupervised approach cannot distinguish slow sit-down or controlled crouch from novel fall pattern — false positives likely | C | Methodology (unsupervised reconstruction error) | 🟠 High |

---

### PAPER_11 — MobileNetV2+GRU (Trustworthy/Responsible AI, 2024, Springer)

| # | Limitation | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | Falls tested on simulated falls by volunteers — not real elderly subjects | B | Section 5, pp. 12–13 | 🔴 Critical |
| L2 | No staircase evaluation — banister occlusion not tested | B | Section 5, pp. 12–13 | 🔴 Critical |
| L3 | Multi-person identity swap under occlusion not evaluated | B | Section 5, pp. 12–13 | 🟠 High |
| L4 | Federated learning communication overhead increases under unstable network connections | B | Section 5, pp. 12–13 | 🟡 Medium |
| L5 | No local physical buzzer or alert hardware | B | Section 5, pp. 12–13 | 🔴 Critical (for our system) |
| L6 | No automated alert escalation pipeline | B | Section 5, pp. 12–13 | 🔴 Critical (for our system) |
| L7 | **MobileNetV2 backbone = 96.8% of inference time** (36.22ms) vs. GRU = 0.93ms — backbone is the bottleneck, not temporal model | A | Section 4 (Performance breakdown table) | 🟠 High |
| L8 | Evaluated on Le2i and CAUCAFall — not a staircase or real elderly dataset | C | Dataset section | 🟠 High |

---

### PAPER_12 — Systematic Review: Real-Time FPS on Hardware (Nabizade et al., 2026, MDPI Sensors)

| # | Limitation (of literature as reviewed) | Type | Evidence | Relevance to Target |
|---|---|---|---|---|
| L1 | **Only 11 of 588 (1.87%) papers validated real-time on physical hardware** | A (Meta-finding) | Section 4.1, Table 1, pp. 6–8 | 🔴 Critical |
| L2 | **No published hardware-tested system evaluates staircase** | A (Meta-finding) | Section 5.3, pp. 12–13 | 🔴 Critical |
| L3 | **Alert systems are rudimentary single-shot only** — no acknowledgement, timeout, or escalation in any analyzed system | A (Meta-finding) | Section 5.3, pp. 12–13 | 🔴 Critical |
| L4 | Multi-person tracking absent from all hardware-tested papers | A (Meta-finding) | Section 5.3, pp. 12–13 | 🟠 High |
| L5 | Thermal throttling on edge devices causes FPS degradation over time — not modeled in most papers | B | Section 5.1 | 🟡 Medium |
| L6 | Privacy: camera systems in corridors create legal/ethical barriers to real elderly subject data collection | B | Section 5.2 | 🟡 Medium |
| L7 | Poor handling of multi-person and occlusion scenarios, limited privacy, weak security measures | A (Meta-finding, citing multiple sub-reviews) | Section 2 | 🟠 High |
| L8 | Dataset fragmentation — no common benchmark for real-time evaluation | A (Meta-finding) | Section 5.4 | 🟡 Medium |

---

## 5.2 Cross-Paper Limitation Frequency Matrix

For each limitation category, how many papers exhibit it (directly or by implication):

| # | Limitation Category | Papers Affected | Count | Classification |
|---|---|---|---|---|
| **L-A** | **Staircase absent** | P01,P02,P03,P04,P05,P06,P07(meta),P08,P09,P10,P11,P12(meta) | **12/12** | 🔴 Universal |
| **L-B** | **No elderly subjects for falls** | P01,P02,P03,P04,P05,P06,P07(meta),P08,P09,P10,P11,P12(meta) | **12/12** | 🔴 Universal |
| **L-C** | **No alert/alarm/escalation pipeline** | P01,P02,P03,P04,P05,P06,P08,P09,P10,P11 | **10/12** | 🔴 Near-universal |
| **L-D** | **Multi-person tracking not addressed** | P01,P02,P03,P05,P06,P07(meta),P08,P09,P10,P11 | **10/12** | 🔴 Near-universal |
| **L-E** | **No real-time hardware validation** | P01,P02,P03,P04,P05,P06,P07(meta),P09,P10,P12(meta) | **10/12** | 🔴 Near-universal |
| **L-F** | **Occlusion not systematically handled** | P01,P02,P03,P05,P07(meta),P08,P09,P10,P11 | **9/12** | 🔴 Major |
| **L-G** | **Night/low-light not tested** | P01,P02,P03,P06,P07(meta),P08,P09,P10,P11 | **9/12** | 🔴 Major |
| **L-H** | **Dataset too small / non-reproducible** | P01,P03,P06,P07(meta),P09,P10,P12(meta) | **7/12** | 🟠 Common |
| **L-I** | **False-positive reduction insufficient** | P02,P03,P07(meta),P06,P09,P10,P11 | **7/12** | 🟠 Common |
| **L-J** | **Slow falls / ADL confusion** | P07(meta),P10,P11,P06,P09 | **5/12** | 🟠 Common |
| **L-K** | **Privacy / data collection barriers** | P07,P10,P11,P12 | **4/12** | 🟡 Moderate |
| **L-L** | **Non-standard CCTV hardware required** | P04,P05,P10 | **3/12** | 🟡 Moderate |
| **L-M** | **Camera-angle generalization not tested** | P01,P05,P07(meta) | **3/12** | 🟡 Moderate |

---

## 5.3 Severity-Ranked Master Limitation List

Ranked by combined frequency × severity × relevance to our target system:

### 🔴 SEVERITY 1 — Critical (present across literature AND critical for our system)

**LIMIT-01: Staircase Environments — 12/12 Papers (100%)**
- **Status**: Zero published papers evaluate a complete fall detection pipeline in a real staircase environment
- **Why critical**: Our entire system is designed for staircase deployment. This is not just a gap — it is a void.
- **Type**: C (Implied by experimental design) across all empirical papers; A+B (Meta-confirmed) by P07 and P12
- **Confounders specific to staircases**: 
  - Person naturally inclines forward — mimics fall posture
  - Banister causes repeated partial occlusion
  - Person moves vertically (step descent) — mimics falling trajectory
  - Multiple people on stairs simultaneously
  - Steep camera angles distort pose keypoints
  - Staircase echoes disrupt audio-based methods

---

**LIMIT-02: No Elderly Subjects for Fall Data — 12/12 Papers (100%)**
- **Status**: 95% of the broader literature (P07 survey) confirmed; all 12 empirical papers confirmed.
- **Why critical**: Elderly falls have distinct biomechanics — slower velocity, asymmetric balance loss, use of banister for support during fall. Young-subject data may not generalize.
- **Type**: B across empirical papers; A (meta-finding, P07)
- **Evidence**: P07 §5; P12 §5.1 — "none include older adults: all falls are simulated by young volunteers"

---

**LIMIT-03: No Alert / Escalation Pipeline — 10/12 Papers (83%)**
- **Status**: Only 1 of 22 vision studies (P07 survey) demonstrated real-time alarm transmission. No paper implements acknowledgement or escalation.
- **Why critical**: Our system's unique contribution is the complete emergency response loop: local buzzer → remote alert → acknowledgement → escalation. This is confirmed absent by two independent systematic reviews.
- **Type**: A (meta-confirmed by P07 and P12); C (implied in empirical papers P01-P11)
- **Evidence**: P07 §5; P12 §5.3 — "alert systems are rudimentary single-shot alerts without acknowledgement or escalation"

---

**LIMIT-04: Real-Time Hardware Gap — 10/12 Papers (83%)**
- **Status**: 98.13% of 588 papers claiming real-time capability were never validated on physical hardware (P12)
- **Why critical**: Our system must run on a laptop GPU in real-time. This is currently essentially unvalidated in the staircase context.
- **Type**: A (P12 PRISMA meta-finding); B (explicit acknowledgement in P07)
- **Evidence**: P12 §4.1 — "only 11 of 588 (1.87%) papers validated on physical hardware"

---

**LIMIT-05: Multi-Person Tracking Failure — 10/12 Papers (83%)**
- **Status**: Multi-person detection/tracking essentially absent from fall detection literature. Only P08 addresses multi-person tracking but not fall classification.
- **Why critical**: Common-area staircases regularly have 2–3 persons simultaneously. Standard trackers lose identity under occlusion in this scenario.
- **Type**: A (confirmed by P07 and P12 meta-findings); C (implied by single-subject experimental designs)
- **Evidence**: P07 §5; P12 §5.3; P08 §V (partial multi-person only)

---

### 🟠 SEVERITY 2 — High (affects multiple papers, significant for target system)

**LIMIT-06: Occlusion Handling — 9/12 Papers**
- Partial body occlusion from banister, furniture, or other persons degrades pose keypoint accuracy
- Skeleton tracking explicitly breaks under steep camera angles (P07 §5)
- P02: AlphaPose demonstrably fails under dim indoor light and partial occlusion (A)
- P08: Multi-person tracking loses ID under dense occlusion (B)

**LIMIT-07: Night/Low-Light Conditions — 9/12 Papers**
- Standard RGB cameras degrade severely in low-light (relevant: 8:42 PM target scenario)
- P05 is the only paper addressing night with IR sensors — but IR is not standard CCTV
- P07: night/low-light rarely systematically tested in literature
- Only P05 explicitly evaluates night; 8 others simply ignore it

**LIMIT-08: False-Positive Reduction / ADL Confusion — 7/12 Papers**
- Slow falls, kneeling, bending, sitting, stumbling frequently confused with real falls
- P06: only 2 non-fall scenarios — virtually guarantees inflated accuracy
- P10 (DCLSTMAE): unsupervised reconstruction error cannot cleanly distinguish slow crouch from fall (C)
- P07 explicitly states no paper fully resolves false-positive discrimination for ADLs

**LIMIT-09: Dataset Smallness / Non-Reproducibility — 7/12 Papers**
- UR Dataset (used by P10, P06): only 70 videos, single room
- P06 Multiple Cameras: 1 subject, 22 falls, 2 non-falls
- P03: private, non-reproducible dataset
- P02 (AI Hub): restricted access — not reproducible

---

### 🟡 SEVERITY 3 — Moderate (present in literature, relevant but less critical)

**LIMIT-10: Non-Standard Hardware Requirements — 3/12 Papers**
- P04: pressure tiles, P05: IR/Depth sensors, P10: Depth/Thermal sensors
- None of these are available in standard CCTV infrastructure
- This limitation directly justifies our RGB-only CCTV approach

**LIMIT-11: Camera-Angle Generalization — 3/12 Papers**
- P05 uses only ceiling top-down cameras
- P07: steep camera angles distort pose keypoints
- Staircase cameras typically wall-mounted at ~45° angle — rarely tested

**LIMIT-12: Backbone Computational Bottleneck — 1 paper explicitly, implied broadly**
- P11 (MobileNetV2): backbone = 96.8% of inference time (36.22ms) vs GRU = 0.93ms
- This is an architectural finding, not a hardware limitation
- Implication: optimize backbone selection → bigger gains than temporal model optimization

---

## 5.4 Limitation Classification Summary Table

| Limitation | Type A (Demonstrated) | Type B (Acknowledged) | Type C (Implied) | Total Papers |
|---|---|---|---|---|
| Staircase absent | P07(meta), P12(meta) | P01,P02,P03,P10,P11 | P04,P05,P06,P08,P09 | 12 |
| No elderly falls | P07(meta), P12(meta) | P01,P03,P05,P11 | P02,P04,P06,P08,P09 | 12 |
| No alert/escalation | P07(meta), P12(meta) | P10,P11 | P01,P02,P03,P05,P06,P08,P09 | 12 |
| Real-time hardware gap | P12(meta) | P07(meta) | P01,P02,P03,P06,P09,P10 | 8 |
| Multi-person absent | P07(meta), P12(meta) | P08 | P01,P02,P03,P05,P06,P09,P11 | 10 |
| Occlusion insufficient | P02 | P03,P07,P08,P10 | P01,P05,P09,P11 | 9 |
| Night/low-light absent | — | P07 | P01,P02,P03,P06,P08,P09,P11 | 9 |
| False-positive insufficient | P06 | P07,P10 | P02,P03,P09,P11 | 7 |
| Dataset smallness | P06(1 subject) | P03,P07,P10,P12 | P01,P09 | 7 |
| Backbone bottleneck | P11 | — | P02,P03,P09 | 4 |
| Non-standard hardware | P04(tiles) | P05,P10 | — | 3 |
| Camera-angle generalization | — | P05,P07 | P01 | 3 |

---

## 5.5 Limitations Ranked by Research Priority

| Rank | Limitation | Frequency | Severity | Target Relevance | Research Priority |
|---|---|---|---|---|---|
| 1 | Staircase environments | 12/12 | 🔴 Critical | Maximum | **VERY HIGH** |
| 2 | No alert / escalation pipeline | 10/12 | 🔴 Critical | Maximum | **VERY HIGH** |
| 3 | No real-time hardware validation | 10/12 | 🔴 Critical | Very High | **VERY HIGH** |
| 4 | Multi-person tracking | 10/12 | 🔴 Critical | Very High | **HIGH** |
| 5 | No elderly subjects | 12/12 | 🔴 Critical | High | **HIGH** |
| 6 | Occlusion handling | 9/12 | 🟠 High | Very High | **HIGH** |
| 7 | Night / low-light | 9/12 | 🟠 High | High (8:42 PM scenario) | **HIGH** |
| 8 | False-positive / ADL confusion | 7/12 | 🟠 High | Very High | **HIGH** |
| 9 | Non-reproducible small datasets | 7/12 | 🟠 High | Medium | **MEDIUM** |
| 10 | Backbone computational bottleneck | 4/12 | 🟡 Med | Medium | **MEDIUM** |
| 11 | Non-standard hardware | 3/12 | 🟡 Med | Medium (justifies CCTV-only) | **MEDIUM** |
| 12 | Camera-angle generalization | 3/12 | 🟡 Med | Medium | **LOW-MEDIUM** |

---

## 5.6 Key Observations for Research Gap Extraction

1. **The staircase void is total**: Not a single paper in the literature — empirical or survey — has experimentally evaluated a complete fall detection pipeline in a staircase environment. This is a **confirmed void**, not just a gap.

2. **The alert void is total and independently confirmed by two systematic reviews (P07, P12)**: Only 1 of 22 vision-based studies demonstrated real-time alarm transmission. No paper implements acknowledgement or timeout-escalation. This is a **confirmed void**, not just a gap.

3. **Real-time claim vs. reality**: The P12 meta-finding (1.87% hardware validation rate) means the vast majority of "high accuracy" papers (including P01=97.4%, P06=97.4%, P10=97.1%) have unknown real-time performance. **High accuracy ≠ real-time deployable system**.

4. **The backbone finding (P11)** has direct design implications: spending effort optimizing the temporal classifier (GRU) yields only 3% improvement potential; switching backbone architectures (e.g., MobileNetV2 → EfficientNet-Lite or MobileNetV3) yields up to 97% improvement potential in inference time. This is an **actionable design choice** for our system.

5. **ADL confusion is persistent and unresolved**: Every method that reports high accuracy does so with either (a) very few non-fall scenarios (P06 has 2), (b) easy-to-classify non-falls (lying in bed, walking), or (c) no slow/gradual falls. The staircase context adds new hard confounders: walking down stairs, bending to pick something up on stairs, sitting on steps.

6. **Night/low-light is relevant but addressable**: Our target scenario (8:42 PM) specifically involves evening/night conditions. Standard RGB CCTV with infrared illumination (very common in building security cameras) partially resolves this. This is worth noting in our system architecture.

---

## 5.7 Evidence Traceability for Top Limitations

| Limitation | Paper | Page/Section | Evidence Type | Supports/Contradicts Gap |
|---|---|---|---|---|
| Staircase absent from all papers | P07 | §5, pp. 9000–9002 | Meta-finding | Supports |
| Staircase absent from all papers | P12 | §5.3, pp. 12–13 | Meta-finding | Supports |
| Staircase absent (banister occlusion specific) | P11 | §5, pp. 12–13 | Explicit limitation | Supports |
| No elderly subjects (95% of literature) | P07 | §5 | Meta-finding | Supports |
| No alert escalation in any system | P07 | §5 | 1/22 alert-capable | Supports |
| No alert escalation in any system | P12 | §5.3, pp. 12–13 | PRISMA meta-finding | Supports |
| Real-time hardware gap (1.87%) | P12 | §4.1, Table 1 | PRISMA meta-finding | Supports |
| Multi-person tracking absent | P12 | §5.3, pp. 12–13 | PRISMA meta-finding | Supports |
| Multi-person not evaluated | P07 | §5 | Survey finding | Supports |
| Occlusion breaks skeleton tracking | P07 | §5 | Survey finding | Supports |
| AlphaPose fails under occlusion/dark | P02 | §IV.B.1 | Demonstrated failure | Supports |
| False-positive rate insufficient | P06 | Dataset description | Only 2 non-fall classes | Supports |
| Backbone bottleneck (96.8% of time) | P11 | §4, performance table | Quantitative finding | Informs design |
| Night/low-light not systematically tested | P05 | Only paper testing (IR-only) | Single-paper finding | Supports |
| No staircase — physical incompatibility | P04 | §III | Physical constraint | Supports |

---

*End of Phase 5 — Failure Modes & Limitations Analysis*  
*Next: Phase 6 — System-Level Analysis (YES/NO/PARTIAL/NOT REPORTED matrix)*
