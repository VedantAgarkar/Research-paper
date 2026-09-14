# Phase 6: Master Cross-Paper Comparison Matrix

> **Project**: Real-Time CCTV-Based Elderly Fall Detection in Staircase / Common-Area Environments  
> **Phase**: Phase 6 — System-Level YES / NO / PARTIAL / NOT REPORTED Matrix  
> **Papers**: 12 (PAPER_01 – PAPER_12)  
> **Source data**: Phases 1–5 analyses  

---

## Legend

| Symbol | Meaning |
|---|---|
| ✅ YES | Explicitly evaluated / implemented / validated |
| ⚠️ PARTIAL | Addressed but incompletely or under limited conditions |
| ❌ NO | Explicitly stated as not done / out of scope |
| — | NOT REPORTED — paper does not address this; cannot infer either way |

> ⚠️ **NOT REPORTED ≠ NO**. A paper not mentioning a dimension may simply be out of scope, not a denial of capability.

---

## 6.1 Master Comparison Matrix

*(Scroll horizontally — 12 papers × 42 dimensions)*

### BLOCK A — Core Computer Vision Pipeline

| Dimension | P01 BiMP | P02 AlphaPose+LSTM | P03 Custom CNN | P04 Floor Tiles | P05 Multimodal | P06 MultiCam | P07 Survey | P08 EfficientDet | P09 GAN Temporal | P10 DCLSTMAE | P11 MobileNetV2+GRU | P12 RT-Review |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **Person detection** | ✅ | ✅ | ✅ | ❌ (non-vision) | ✅ | ✅ | ✅ (literature) | ✅ | ✅ | ✅ | ✅ | ✅ (literature) |
| **Person tracking** | — | ✅ AlphaPose | ⚠️ basic BB | ❌ | ⚠️ | ⚠️ | ✅ (literature) | ✅ Multi-track | — | — | ⚠️ sliding window | ✅ (literature) |
| **Pose estimation** | ✅ GoogLeNet feats | ✅ AlphaPose skeleton | — | ❌ | ✅ RGB+D+IR | — | ✅ (literature) | — | — | — | ✅ MobileNetV2 | ✅ (literature) |
| **Skeleton / keypoint repr.** | — | ✅ 17-keypoint | — | ❌ | ✅ | — | ✅ (literature) | — | — | — | — | — |
| **Spatial feature extraction** | ✅ GoogLeNet CNN | ✅ AlphaPose | ✅ CNN | ❌ pressure | ✅ multimodal | ✅ CNN | ✅ (literature) | ✅ EfficientDet | ✅ GAN | ✅ Dilated Conv | ✅ MobileNetV2 | ✅ (literature) |
| **Motion / optical flow features** | — | ⚠️ skeleton motion | — | — | ⚠️ temporal diff | — | ✅ (literature) | — | ✅ | ✅ conv-LSTM diff | — | — |
| **Temporal modelling** | ✅ LSTM | ✅ LSTM | — | — | ✅ | — | ✅ (literature) | — | ✅ GAN discriminator | ✅ ConvLSTM | ✅ GRU sliding window | ✅ (literature) |
| **Fall classification** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ (literature) | ❌ (detection only) | ✅ | ✅ | ✅ | ✅ (literature) |
| **Fall verification / confidence threshold** | — | — | — | — | ✅ fall score | — | ⚠️ mentioned | — | — | ✅ reconstruction score | ✅ fall probability | — |

---

### BLOCK B — Environmental Robustness

| Dimension | P01 | P02 | P03 | P04 | P05 | P06 | P07 | P08 | P09 | P10 | P11 | P12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **Multiple-person detection** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ <10% of lit | ✅ (detection only) | ❌ | ❌ | ❌ | — |
| **Multiple-person tracking** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ (absent from hardware papers) |
| **Occlusion handling** | ❌ | ⚠️ tested; fails | ⚠️ acknowledged | — | — | — | ⚠️ noted as failure | ⚠️ partial in crowd | — | ⚠️ depth hole-fill | ❌ not evaluated | ⚠️ noted as gap |
| **Lighting variation (daytime)** | — | ✅ AI Hub varied | ✅ 5 indoor scenes | — | ✅ day sessions | — | ⚠️ varies | — | — | — | ⚠️ varied environments | — |
| **Night / low-light conditions** | ❌ | ⚠️ dim indoor only | ❌ | — | ✅ IR night sessions | ❌ | ⚠️ rarely in lit | ❌ | ❌ | ⚠️ thermal (not night per se) | ❌ | — |
| **Camera-angle variation** | ✅ 4 angles | ✅ varied CCTV | ⚠️ 5 rooms | — | ❌ top-down only | ✅ multiple cameras | ⚠️ mentioned gap | — | — | — | ✅ multiple angles | — |
| **Staircase evaluation** | ❌ | ❌ | ❌ | ❌ (incompatible) | ❌ | ❌ | ❌ (explicit: absent from all 87) | ❌ | ❌ | ❌ | ❌ | ❌ (explicit: absent) |
| **Distance from camera** | — | — | — | — | — | ✅ varied | — | — | — | — | — | — |
| **Partial visibility / frame exit** | — | — | — | — | — | — | ⚠️ noted as issue | — | — | — | — | — |

---

### BLOCK C — Real-World Validation

| Dimension | P01 | P02 | P03 | P04 | P05 | P06 | P07 | P08 | P09 | P10 | P11 | P12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **Real CCTV footage used** | ❌ lab cameras | ✅ AI Hub CCTV | ❌ lab setup | ❌ | ❌ ceiling RGB+D | ❌ | ⚠️ <10% of lit | — | ❌ | ❌ | ⚠️ Le2i is surveillance-like | — |
| **Real (unscripted) falls** | ❌ staged | ❌ staged | ❌ staged | ❌ | ❌ staged | ❌ staged | ❌ (none in lit) | — | ❌ staged | ❌ staged | ❌ staged | ❌ (explicit: none in lit) |
| **Elderly subjects for falls** | ❌ | ❌ | ❌ | ❌ | ❌ (ADL only) | ❌ | ❌ (95% of lit) | ❌ | ❌ | ❌ | ❌ | ❌ (explicit: none) |
| **Uncontrolled / natural environment** | ❌ | ⚠️ AI Hub diverse | ❌ | ❌ | ❌ | ❌ | ⚠️ rare in lit | ❌ | ❌ | ❌ | ⚠️ Le2i/CAUCA multi-room | — |
| **Cross-environment generalization** | ❌ | ⚠️ AI Hub multi-loc | ❌ | ❌ | ❌ | ❌ | ❌ | — | ❌ | ❌ | ✅ Le2i + CAUCAFall | — |
| **Cross-camera generalization** | ✅ 4 cameras | ✅ varied CCTV | — | — | ❌ single rig | ✅ multi-camera | — | — | — | — | ⚠️ 2 datasets | — |
| **Realistic ADL negative activities** | ⚠️ few ADLs | ✅ varied activities | ⚠️ limited | ✅ pressure-based ADL | ✅ varied | ❌ only 2 non-falls | ⚠️ rarely rich | — | ⚠️ some | ✅ ADL-trained | ✅ bending/sitting | — |

---

### BLOCK D — Non-Fall Activity Discrimination

| Dimension | P01 | P02 | P03 | P04 | P05 | P06 | P07 | P08 | P09 | P10 | P11 | P12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **Sitting confusion tested** | — | ✅ | — | ✅ | ✅ | — | ⚠️ noted | — | — | ✅ | ✅ | — |
| **Lying-down confusion tested** | — | ✅ | — | ✅ | ✅ | — | ⚠️ noted | — | — | ✅ | ✅ | — |
| **Bending confusion tested** | — | ✅ | — | ✅ | — | — | ⚠️ noted | — | — | — | ✅ | — |
| **Kneeling confusion tested** | — | — | — | — | — | — | ⚠️ noted | — | — | — | — | — |
| **Stumbling / near-fall tested** | — | — | — | — | — | — | ⚠️ noted | — | — | — | — | — |
| **Walking-down-stairs confusion** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Slow fall tested** | — | — | — | — | — | — | ⚠️ noted as FP risk | — | — | — | — | — |
| **Fast fall tested** | — | ✅ | — | — | — | — | — | — | — | — | — | — |

---

### BLOCK E — Computation & Real-Time Deployment

| Dimension | P01 | P02 | P03 | P04 | P05 | P06 | P07 | P08 | P09 | P10 | P11 | P12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **Real-time implementation** | — | ❌ (~3 FPS) | — | — | — | — | ⚠️ <15% of lit | ✅ stated | — | — | ✅ 32 FPS GPU | ✅ (audits this) |
| **FPS reported** | — | ✅ ~3 FPS | — | — | — | — | ⚠️ rarely in lit | ✅ | — | — | ✅ ~93 FPS (reported) | ✅ (11 papers) |
| **Hardware specified** | ✅ lab PC | ✅ GPU server | — | ✅ MCU tiles | ✅ lab PC | — | ⚠️ varied | ✅ GPU | — | — | ✅ edge-tier GPU | ✅ extensive |
| **Edge / local processing** | — | — | — | — | — | — | ⚠️ growing trend | ⚠️ GPU required | — | — | ✅ federated/local | ✅ core focus |
| **Resource efficiency** | — | — | — | — | — | — | ⚠️ rarely optimized | — | — | — | ✅ MobileNetV2 | ✅ central topic |
| **Inference latency reported** | — | — | — | — | — | — | — | — | — | — | ✅ 36.22ms backbone | ✅ per paper |
| **Privacy-preserving processing** | — | — | — | ✅ no video | ✅ depth/thermal | — | ⚠️ 50% lack it | — | — | ✅ depth/thermal | ✅ federated | ⚠️ noted concern |

---

### BLOCK F — Emergency Response System

| Dimension | P01 | P02 | P03 | P04 | P05 | P06 | P07 | P08 | P09 | P10 | P11 | P12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **Local alarm / buzzer** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ 1/22 vision | ❌ | ❌ | ❌ | ❌ | ✅ (surveyed, rare) |
| **Remote notification** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ rare in lit | ❌ | ❌ | ❌ | ❌ | ⚠️ SMS/email noted |
| **Security / multi-recipient alert** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Image / clip evidence transmission** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ Grad-CAM heatmap | ❌ |
| **Human acknowledgement mechanism** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Alert timeout** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Alert escalation** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **End-to-end emergency response** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |

---

## 6.2 Dimension Coverage Summary

How many of the 12 papers address each dimension (YES or PARTIAL only):

### BLOCK A — Core CV Pipeline

| Dimension | YES | PARTIAL | NOT REPORTED | NO | Coverage % | Status |
|---|---|---|---|---|---|---|
| Person detection | 10 | — | — | 2 | 83% | ✅ **Saturated** |
| Person tracking | 5 | 4 | 2 | 1 | 75% | ✅ **Well explored** |
| Pose estimation | 6 | — | 4 | 2 | 50% | 🟡 **Moderately explored** |
| Skeleton / keypoint repr. | 3 | — | 7 | 2 | 25% | 🟠 **Underexplored** |
| Spatial feature extraction | 10 | — | — | 2 | 83% | ✅ **Saturated** |
| Motion / optical flow features | 3 | 4 | 5 | — | 58% | 🟡 **Moderately explored** |
| Temporal modelling | 7 | — | 3 | 2 | 58% | 🟡 **Moderately explored** |
| Fall classification | 10 | — | — | 2 | 83% | ✅ **Saturated** |
| Fall verification / threshold | 3 | 1 | 8 | — | 33% | 🟠 **Underexplored** |

### BLOCK B — Environmental Robustness

| Dimension | YES | PARTIAL | NOT REPORTED | NO | Coverage % | Status |
|---|---|---|---|---|---|---|
| Multiple-person detection | 1 | 1 | — | 10 | 17% | 🔴 **Almost unexplored** |
| Multiple-person tracking | 1 | — | — | 11 | 8% | 🔴 **Almost unexplored** |
| Occlusion handling | — | 6 | 2 | 4 | 50% | 🟡 **Moderate (but always PARTIAL)** |
| Lighting variation (day) | 3 | 4 | 5 | — | 58% | 🟡 **Moderately explored** |
| Night / low-light | 1 | 2 | — | 9 | 25% | 🟠 **Underexplored** |
| Camera-angle variation | 5 | 2 | 3 | 2 | 58% | 🟡 **Moderately explored** |
| **Staircase evaluation** | **0** | **0** | **0** | **12** | **0%** | 🔴 **COMPLETELY ABSENT** |
| Distance from camera | 1 | — | 11 | — | 8% | 🔴 **Almost unexplored** |
| Partial visibility / frame exit | — | 1 | 9 | 2 | 8% | 🔴 **Almost unexplored** |

### BLOCK C — Real-World Validation

| Dimension | YES | PARTIAL | NOT Reported | NO | Coverage % | Status |
|---|---|---|---|---|---|---|
| Real CCTV footage | 1 | 2 | — | 9 | 25% | 🟠 **Underexplored** |
| Real (unscripted) falls | 0 | 0 | 0 | 12 | 0% | 🔴 **COMPLETELY ABSENT** |
| Elderly subjects for falls | 0 | 0 | 0 | 12 | 0% | 🔴 **COMPLETELY ABSENT** |
| Uncontrolled / natural env. | — | 3 | — | 9 | 25% | 🟠 **Underexplored** |
| Cross-environment generalization | 1 | 2 | 4 | 5 | 25% | 🟠 **Underexplored** |
| Cross-camera generalization | 3 | 2 | 6 | 1 | 42% | 🟡 **Moderate** |
| Realistic ADL negatives | 2 | 6 | 1 | 3 | 67% | 🟡 **Moderately explored** |

### BLOCK D — Non-Fall Activity Discrimination

| Dimension | YES | PARTIAL | Not Reported | NO | Coverage % | Status |
|---|---|---|---|---|---|---|
| Sitting confusion tested | 4 | 2 | 6 | — | 50% | 🟡 **Moderate** |
| Lying-down confusion tested | 4 | 2 | 6 | — | 50% | 🟡 **Moderate** |
| Bending confusion tested | 3 | 1 | 8 | — | 33% | 🟠 **Underexplored** |
| Kneeling confusion tested | — | 1 | 11 | — | 8% | 🔴 **Almost unexplored** |
| Stumbling / near-fall tested | — | 1 | 11 | — | 8% | 🔴 **Almost unexplored** |
| **Walking-down-stairs confusion** | **0** | **0** | **0** | **12** | **0%** | 🔴 **COMPLETELY ABSENT** |
| Slow fall tested | — | 1 | 11 | — | 8% | 🔴 **Almost unexplored** |
| Fast fall tested | 1 | — | 11 | — | 8% | 🔴 **Almost unexplored** |

### BLOCK E — Computation & Deployment

| Dimension | YES | PARTIAL | Not Reported | NO | Coverage % | Status |
|---|---|---|---|---|---|---|
| Real-time implementation | 3 | 2 | 3 | 4 | 42% | 🟡 **Moderate (claim vs. reality gap)** |
| FPS reported | 4 | 2 | 5 | 1 | 50% | 🟡 **Moderate** |
| Hardware specified | 6 | 2 | 4 | — | 67% | 🟡 **Moderately explored** |
| Edge / local processing | 2 | 2 | 7 | 1 | 33% | 🟠 **Underexplored** |
| Resource efficiency | 2 | 1 | 9 | — | 25% | 🟠 **Underexplored** |
| Inference latency reported | 2 | — | 10 | — | 17% | 🟠 **Underexplored** |
| Privacy-preserving processing | 3 | 3 | 4 | 2 | 50% | 🟡 **Moderate** |

### BLOCK F — Emergency Response

| Dimension | YES | PARTIAL | Not Reported | NO | Coverage % | Status |
|---|---|---|---|---|---|---|
| Local alarm / buzzer | 0 | 1 | — | 11 | 8% | 🔴 **Almost unexplored** |
| Remote notification | 0 | 1 | — | 11 | 8% | 🔴 **Almost unexplored** |
| Security / multi-recipient alert | 0 | 0 | — | 12 | 0% | 🔴 **COMPLETELY ABSENT** |
| Image / clip evidence | 0 | 1 | — | 11 | 8% | 🔴 **Almost unexplored** |
| **Human acknowledgement** | **0** | **0** | **0** | **12** | **0%** | 🔴 **COMPLETELY ABSENT** |
| **Alert timeout** | **0** | **0** | **0** | **12** | **0%** | 🔴 **COMPLETELY ABSENT** |
| **Alert escalation** | **0** | **0** | **0** | **12** | **0%** | 🔴 **COMPLETELY ABSENT** |
| **End-to-end emergency response** | **0** | **0** | **0** | **12** | **0%** | 🔴 **COMPLETELY ABSENT** |

---

## 6.3 Ranked Dimension Coverage List

### 🔴 COMPLETELY ABSENT (0% coverage — confirmed ❌ across all 12 papers)

| Rank | Dimension | Evidence | Research Importance |
|---|---|---|---|
| 1 | **Staircase evaluation** | P07 §5 (all 87 papers), P12 §5.3 | Maximum — core target scenario |
| 2 | **Real (unscripted) falls** | P12 §5.1 confirmed across literature | Maximum — ecological validity |
| 3 | **Elderly subjects performing falls** | P07 §5 (95% of literature), P12 | Maximum — target demographic |
| 4 | **Walking-down-stairs confusion** | No paper even mentions this ADL | Maximum — core false-positive risk |
| 5 | **Human acknowledgement** | P12 §5.3 | Very High — system completeness |
| 6 | **Alert timeout** | P12 §5.3 | Very High — system completeness |
| 7 | **Alert escalation** | P07 §5, P12 §5.3 | Very High — system completeness |
| 8 | **End-to-end emergency response** | Confirmed absent from all papers | Very High — system completeness |
| 9 | **Security / multi-recipient alert** | No paper implements this | High |

---

### 🔴 ALMOST UNEXPLORED (< 17% coverage)

| Rank | Dimension | Coverage | Key Paper(s) | Research Importance |
|---|---|---|---|---|
| 10 | **Multiple-person tracking** | 8% (1/12) | P08 (detection only, not fall) | Very High |
| 11 | **Multiple-person detection (fall context)** | 17% (2/12) | P08 | Very High |
| 12 | **Distance from camera** | 8% (1/12) | P06 | Medium |
| 13 | **Partial visibility / frame exit** | 8% (1/12) | P07 noted | High |
| 14 | **Kneeling confusion** | 8% (1/12) | P07 noted | High |
| 15 | **Stumbling / near-fall** | 8% (1/12) | P07 noted | Very High (FP risk) |
| 16 | **Slow fall** | 8% (1/12) | P07 noted | Very High (FP risk) |
| 17 | **Fast fall** | 8% (1/12) | P02 | Medium |
| 18 | **Local alarm / buzzer** | 8% (1/12) | P12 surveyed | Very High |
| 19 | **Remote notification** | 8% (1/12) | P12 (SMS/email noted) | Very High |
| 20 | **Image / clip evidence** | 8% (1/12) | P11 (Grad-CAM only) | High |

---

### 🟠 UNDEREXPLORED (17–40% coverage)

| Rank | Dimension | Coverage | Key Paper(s) | Research Importance |
|---|---|---|---|---|
| 21 | **Night / low-light** | 25% (3/12) | P05 (IR only) | Very High (8:42 PM) |
| 22 | **Real CCTV footage** | 25% (3/12) | P02 (AI Hub) | Very High |
| 23 | **Cross-environment generalization** | 25% (3/12) | P11 (2 datasets) | High |
| 24 | **Uncontrolled / natural environments** | 25% (3/12) | P02 partial | High |
| 25 | **Elderly subjects (ADL only — not falls)** | 25% (3/12) | P05, P07 noted | High |
| 26 | **Skeleton / keypoint representation** | 25% (3/12) | P02, P05, P07 | Medium |
| 27 | **Fall verification / threshold** | 33% (4/12) | P05, P10, P11 | Very High |
| 28 | **Edge / local processing** | 33% (4/12) | P11, P12 | High |
| 29 | **Bending confusion tested** | 33% (4/12) | P10, P11, P07 | High |
| 30 | **Resource efficiency** | 25% (3/12) | P11, P12 | High |
| 31 | **Inference latency reported** | 17% (2/12) | P11, P12 | Very High |

---

### 🟡 MODERATELY EXPLORED (40–60% coverage)

| Rank | Dimension | Coverage | Key Paper(s) | Research Importance |
|---|---|---|---|---|
| 32 | **Temporal modelling** | 58% (7/12) | P01,P02,P05,P09,P10,P11,P07 | Very High |
| 33 | **Pose estimation** | 50% (6/12) | P01,P02,P04,P05,P11,P07 | High |
| 34 | **Motion / optical flow** | 58% (7/12) | Multiple | Medium |
| 35 | **Camera-angle variation** | 58% (7/12) | P01,P02,P03,P05,P06,P07 | High |
| 36 | **Lighting variation (daytime)** | 58% (7/12) | P02,P03,P05,P07,P11 | Medium |
| 37 | **Occlusion handling** | 50% (6/12, all PARTIAL) | Multiple | Very High |
| 38 | **Sitting confusion** | 50% (6/12) | P02,P04,P05,P10,P11,P07 | High |
| 39 | **Lying-down confusion** | 50% (6/12) | P02,P04,P05,P10,P11,P07 | High |
| 40 | **Real-time implementation** | 42% (5/12) | P02,P08,P11,P12 | Very High |
| 41 | **Privacy-preserving processing** | 50% (6/12) | P04,P05,P10,P11,P12,P07 | Medium |
| 42 | **Realistic ADL negatives** | 67% (8/12) | Multiple | High |

---

### ✅ SATURATED / WELL EXPLORED (> 70% coverage)

| Rank | Dimension | Coverage | Notes |
|---|---|---|---|
| 43 | **Person detection** | 83% | Basic — mature technology |
| 44 | **Spatial feature extraction** | 83% | CNN backbone — well established |
| 45 | **Fall classification** | 83% | Core task — heavily studied |
| 46 | **Person tracking** | 75% | Mature, various trackers |
| 47 | **Hardware specified** | 67% | Moderate reporting |
| 48 | **Realistic ADL negatives** | 67% | Present but quality varies |

---

## 6.4 System-Level Completeness: Our Target Requirements vs. Literature

How many papers cover each component of our target system end-to-end:

| System Component (Our Target) | Papers Addressing | Coverage | Gap Level |
|---|---|---|---|
| Continuous CCTV input | P02, P11 (partially) | 2/12 (17%) | 🟠 High gap |
| Person detection | 10/12 | 83% | ✅ Low gap |
| Person tracking | 5 YES + 4 PARTIAL | 75% | ✅ Low gap |
| Pose estimation | 6/12 | 50% | 🟡 Medium gap |
| Temporal fall reasoning | 7/12 | 58% | 🟡 Medium gap |
| Fall vs. ADL discrimination | 5 well / 5 partial | ~42% robust | 🟡 Medium gap |
| **Staircase scenario** | **0/12** | **0%** | 🔴 **VOID** |
| **Real elderly subjects (falls)** | **0/12** | **0%** | 🔴 **VOID** |
| Real-time inference validated | 3 rigorous / 2 partial | 25% | 🟠 High gap |
| Local alarm / buzzer | 0 empirical / 1 survey | <8% | 🔴 Near-void |
| Remote alert | 0 empirical | 0% empirical | 🔴 Near-void |
| **Human acknowledgement** | **0/12** | **0%** | 🔴 **VOID** |
| **Alert timeout** | **0/12** | **0%** | 🔴 **VOID** |
| **Alert escalation** | **0/12** | **0%** | 🔴 **VOID** |
| Privacy preservation | 3 YES / 3 PARTIAL | 50% | 🟡 Medium gap |
| Visual evidence (clip/frame) | P11 Grad-CAM partial | <8% | 🔴 Near-void |

---

## 6.5 Key Observations for Phase 8 (Gap Discovery)

1. **Five confirmed absolute voids in the literature (0% coverage, all 12 confirmed NO)**:
   - Staircase evaluation
   - Real / unscripted falls
   - Elderly subjects performing falls
   - Walking-down-stairs confusion testing
   - Human acknowledgement + timeout + escalation (three linked voids)

2. **The emergency response block is a complete void**: Every single paper stops at fall detection. None build the notification → acknowledgement → escalation loop that our target system requires. Two independent systematic reviews (P07, P12) confirm this explicitly.

3. **The real-time claim vs. reality gap is enormous**: 98.13% of "real-time" claims were never validated on hardware (P12). Among the 11 that were, none tested staircase scenarios.

4. **Occlusion is the most consistently partial dimension**: Every paper that addresses occlusion at all only partially handles it — no paper demonstrates robust occlusion-resistant fall detection. This is a persistent open problem.

5. **Night / low-light is addressed only by P05 — and it requires non-standard hardware** (IR sensors, not available in CCTV). No paper addresses night fall detection using standard RGB CCTV cameras.

6. **The intersection of staircase + multi-person + night + CCTV + real-time + alert escalation = absolute zero**: Not a single paper in 12 addresses even 4 of these 6 dimensions simultaneously. Our system aims to address all 6.

---

*End of Phase 6 — Master Cross-Paper Comparison Matrix*  
*Next: Phase 7 — Research Coverage Analysis (dimension-by-dimension deep dive with coverage scores)*
