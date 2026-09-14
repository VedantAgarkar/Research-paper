# Phase 4: Performance Analysis — Quantitative Results & Comparability Assessment

> **Project**: Real-Time CCTV-Based Elderly Fall Detection in Staircase / Common-Area Environments  
> **Phase**: Phase 4 — Performance Analysis  
> **Status**: Completed  
> **Papers Analyzed**: 12 (PAPER_01 – PAPER_12)  
> **Governed by**: [phase4.md](file:///home/endurance/Desktop/Research%20paper/.agents/workflows/phase4.md)

> [!IMPORTANT]
> **Cross-Paper Comparability Warning**: Metrics from different papers are evaluated on different datasets, with different train/test splits, different subject pools, and different evaluation protocols. Direct numerical comparisons between papers are frequently misleading and must be interpreted with caution. This document explicitly flags non-comparable comparisons.

---

## A. Individual Paper Performance Records

---

### PAPER_01 — BiMP Dataset (Dibble & Bazzocchi, 2025, IEEE Access)

| Metric | Value | Dataset | Notes |
|---|---|---|---|
| **Accuracy (GoogLeNet)** | Not explicitly reported as %; classification results per fall type | BiMP (custom lab, 22 subjects) | Table-level results in §V.A |
| **Accuracy (GoogLeNet+LSTM)** | Improved over GoogLeNet alone (percentage not extracted from mid-section) | BiMP | §V.B |
| **Precision** | Not reported | — | — |
| **Recall** | Not reported | — | — |
| **F1-score** | Not reported | — | — |
| **AUC** | Not reported | — | — |
| **FPS** | Not reported (offline evaluation only) | — | — |
| **Inference latency** | Not reported | — | — |
| **Baseline methods** | GoogLeNet (CNN only) vs. GoogLeNet+LSTM | BiMP | §V |
| **Ablation** | CNN-only vs. CNN+LSTM; Audio-only vs. Video-only vs. Combined | §V | Explicit |
| **Statistical significance** | Not reported | — | — |
| **Subject-independent eval** | Not reported | — | — |
| **Environment-independent eval** | No (single lab environment) | — | — |

**Performance Summary**: Primary contribution is the dataset and multimodal baseline, not a state-of-the-art classifier. Quantitative results not fully extractable from available text. GoogLeNet+LSTM outperforms CNN-alone on temporal fall sequences. Audio adds complementary signal to visual features.

**Comparability**: ❌ NOT COMPARABLE — unique audio+video multimodal setup on custom dataset.

---

### PAPER_02 — Pose Estimation + Synthetic Data (Juraev et al., 2022, IEEE Access)

| Metric | Value | Dataset | Notes |
|---|---|---|---|
| **Accuracy (AlphaPose + LSTM, real only)** | 89.22% | AI Hub CCTV (real) | Explicit, §IV.B.2c |
| **Accuracy (AlphaPose + LSTM, real+synth)** | **94.35%** (+5.16%) | AI Hub CCTV + SynADL | Explicit, §IV.B.2c |
| **Accuracy (AlphaPose + Transformer, real+synth)** | **94.35%** (comparable) | AI Hub CCTV + SynADL | Explicit |
| **F1-score (AlphaPose + LSTM, real)** | 89% | AI Hub | §IV.B.2c |
| **Precision (AlphaPose + LSTM, real)** | 89% | AI Hub | §IV.B.2c |
| **Recall (AlphaPose + LSTM, real)** | 90% | AI Hub | §IV.B.2c |
| **Sensitivity (AlphaPose, keypoint quality)** | 94.5% | AI Hub | §IV.B.2a |
| **Specificity (AlphaPose)** | 99.9% | AI Hub | §IV.B.2a |
| **AUC** | Not reported | — | — |
| **FPS (AlphaPose, GTX 1080Ti)** | ~3 FPS | GPU benchmark | §III.A, Table 3 |
| **FPS (MoveNet, GTX 1080Ti)** | ~30 FPS | GPU benchmark | Table 3 |
| **FPS (OpenPose, GTX 1080Ti)** | ~5 FPS | GPU benchmark | Table 3 |
| **Inference latency** | ~9 ms per sample (Transformer model) | — | Explicit |
| **Baseline methods** | AlphaPose, DCPose, OpenPose, OpenPifPaf, MoveNet (5 HPE methods compared) | AI Hub | §III.A, Table 3 |
| **Ablation** | Real-only vs. real+synthetic data (+5.16% accuracy); LSTM vs. Transformer | §IV.B.2c | Explicit |
| **Statistical significance** | Not reported | — | — |
| **Subject-independent eval** | Partial (67.5/32.5% split, not explicitly LOO or cross-subject) | — | §IV.A.1 |
| **Environment-independent eval** | Partially (AI Hub: real CCTV across varied locations) | — | §IV.B.1 |
| **Test set size** | 1,303 test clips (AI Hub) | AI Hub | Table 5 |

**Performance Summary**: Best result is AlphaPose+LSTM with real+synthetic data at 94.35%. Critical caveat: AlphaPose only runs at ~3 FPS on GTX 1080Ti — this is NOT real-time. MoveNet achieves 30 FPS but lower accuracy.

**Comparability**: ⚠️ PARTIALLY COMPARABLE — Uses real-world CCTV dataset (AI Hub) which is larger and more realistic than most papers. However, AI Hub is restricted and cannot be independently reproduced.

---

### PAPER_03 — AI-Based Edge Computing (Lin et al., 2022, IEEE Access)

| Metric | Value | Dataset | Notes |
|---|---|---|---|
| **System accuracy** | **91.1%** | Custom private dataset (5 indoor scenes) | Explicit, §IV.C, Table 5 |
| **YOLO-LW IoU (PC, FP32)** | 94.5% | Custom | §IV.B, Table 2 |
| **YOLO-LW IoU (K210 KPU, INT8)** | ~85-90% (degraded from quantization) | Custom | §IV.B, Table 2 |
| **SVM posture accuracy** | Not reported separately | — | — |
| **Precision** | Not reported | — | — |
| **Recall** | Not reported | — | — |
| **F1-score** | Not reported | — | — |
| **False-positive rate** | Not reported | — | — |
| **AUC** | Not reported | — | — |
| **FPS (Sipeed MAix GO / K210 KPU)** | **11.5 FPS** | Edge hardware | Explicit, §IV.B, Table 3 |
| **Power consumption** | ~0.3W (K210 KPU only) | Sipeed MAix GO | Explicit, §IV.B |
| **Total system power** | <3.5W | Sipeed MAix GO + ESP8285 | Explicit |
| **SVM inference time** | <0.001 seconds | PC | §IV.C |
| **Baseline methods** | YOLOv2-tiny vs. YOLOv3-tiny (modified) comparison (IoU) | Custom | §IV.B, Table 1-2 |
| **Ablation** | FP32 PC vs. INT8 K210; YOLO-v2-tiny vs. YOLO-LW | §IV.B | Explicit |
| **Statistical significance** | Not reported | — | — |
| **Subject-independent eval** | Not reported | — | — |
| **Environment-independent eval** | Partial (5 indoor rooms) | — | §III.C |

**Performance Summary**: The standout contribution is 11.5 FPS on a sub-1W edge device. However, system accuracy of 91.1% is on a private, non-reproducible dataset with unknown demographics. The IoU drop from 94.5% (PC FP32) to ~85-90% (K210 INT8) due to quantization is a critical finding for edge deployment trade-offs.

**Comparability**: ❌ NOT COMPARABLE — Private dataset, no cross-paper metric alignment possible.

---

### PAPER_04 — Smart Tiles / Pressure Sensors (Daher et al., 2017, IEEE Sensors J.)

| Metric | Value | Dataset | Notes |
|---|---|---|---|
| **HCM feature selection error rate** | ~1% (vs. ReliefF 30%, F-score 12%) | Custom tiles lab | §V.A, Fig.12 |
| **Posture classification accuracy (Standing)** | ~100% | Custom | §V |
| **Posture classification accuracy (Walking)** | 98.7% | Custom | §V, Table |
| **Posture classification accuracy (Sitting)** | 95.2% (92.3% one variant) | Custom | §V, Table |
| **Posture classification accuracy (Falling)** | 94.1% | Custom | §V, Table |
| **System sensitivity (all postures)** | >90% for all posture categories | Custom | §V |
| **Precision** | Not reported | — | — |
| **F1-score** | Not reported | — | — |
| **AUC** | Not reported | — | — |
| **False-positive rate** | Acknowledged (lying = fall false alarm, resolved by accelerometer) | — | §IV.C |
| **FPS** | N/A (sensor system at 50 Hz; HCM latency: 0.03s per window) | — | §IV.B.1 |
| **Inference latency** | **0.03 seconds** (HCM on i5-3317U @ 1.7GHz, 4GB RAM) | — | §IV.B.1 |
| **Baseline methods** | ReliefF vs. F-score vs. HCM feature selection | Custom | §V.A, Fig.12-13 |
| **Ablation** | HCM vs. HCM-SFS (combined) | §V.A | Explicit |
| **Statistical significance** | Not reported | — | — |
| **Subject-independent eval** | Not reported (6 subjects used collectively) | — | — |
| **Environment-independent eval** | No (single apartment lab) | — | — |

**Performance Summary**: Classification accuracy is strong in the controlled lab environment. The critical finding is the false alarm from lying → fall which requires multi-sensor fusion to resolve. 0.03s latency is excellent for real-time use, but the system requires custom floor hardware incompatible with our staircase target.

**Comparability**: ❌ NOT COMPARABLE — Non-vision modality; entirely different sensing paradigm.

---

### PAPER_05 — MUVIM Multi-Modal Dataset (Denkovski et al., 2022, IEEE Access)

| Metric | Value | Dataset | Notes |
|---|---|---|---|
| **AUC-ROC (IR camera)** | **0.94** (best) | MUVIM (controlled lab) | Explicit, Abstract |
| **AUC-ROC (Thermal camera)** | 0.87 | MUVIM | Explicit, Abstract |
| **AUC-ROC (Depth camera)** | 0.86 | MUVIM | Explicit, Abstract |
| **AUC-ROC (RGB camera)** | 0.83 | MUVIM | Explicit, Abstract |
| **Accuracy** | Not reported (AUC-only evaluation) | — | — |
| **Precision** | Not reported | — | — |
| **Recall** | Not reported | — | — |
| **F1-score** | Not reported | — | — |
| **False-positive rate** | Not reported | — | — |
| **FPS** | Not reported | — | — |
| **Inference latency** | Not reported | — | — |
| **Baseline methods** | 4 modalities compared (IR, Thermal, Depth, RGB) | MUVIM | Abstract |
| **Ablation** | Day-time vs. night-time performance per modality | §II | Explicit |
| **Statistical significance** | Not reported | — | — |
| **Subject-independent eval** | Not reported | — | — |
| **Night-time vs. day-time** | IR maintains AUC=0.94 at night; RGB degrades most | MUVIM | Abstract, §IV |

**Performance Summary**: Primary finding is that IR cameras provide superior performance in night/low-light conditions (AUC=0.94), substantially outperforming RGB (AUC=0.83). This is an important hardware selection finding for our target scenario (8:42 PM staircase monitoring).

**Comparability**: ❌ NOT COMPARABLE — AUC-only metrics on unique MUVIM dataset; no other paper evaluates MUVIM.

---

### PAPER_06 — HOG + VGG-16 Surveillance (Jain & Sitara, 2022, IEEE INCET)

| Metric | Value | Dataset | Notes |
|---|---|---|---|
| **Accuracy (HOG, UR Fall)** | **92.8%** | UR Fall Detection Dataset | Explicit, §IV |
| **Accuracy (HOG, Multiple Cameras)** | **97.4%** | Multiple Cameras Dataset | Explicit, §IV |
| **Accuracy (Optical Flow, UR Fall)** | ~92% (HOG wins) | UR Fall | §IV |
| **Accuracy (Optical Flow, Multiple Cameras)** | 96.1% | Multiple Cameras | §IV |
| **Sensitivity (referenced comparison)** | 92% | (referenced prior work) | §III |
| **Specificity (referenced comparison)** | 89% | (referenced prior work) | §III |
| **Precision** | Not reported for proposed method | — | — |
| **Recall** | Not reported | — | — |
| **F1-score** | Not reported | — | — |
| **AUC** | Not reported | — | — |
| **FPS** | Not reported | — | — |
| **Inference latency** | Not reported | — | — |
| **Baseline methods** | HOG features vs. Optical Flow features (with same VGG-16 backbone) | Both datasets | §III |
| **Ablation** | HOG vs. Optical Flow | §IV | Explicit |
| **Statistical significance** | Not reported | — | — |
| **Subject-independent eval** | Not reported | — | — |
| **Test set size** | UR Fall: subset of 70 videos; Multiple Cameras: 22 fall + 2 non-fall × 8 cameras | — | §IV.C |

**Performance Summary**: 97.4% on Multiple Cameras must be **treated as highly inflated** — this dataset contains only 1 subject with only 2 non-fall scenarios. The classifier has almost no genuine negative examples to distinguish from. 92.8% on UR Fall is more meaningful but still on a tiny 70-video controlled dataset.

> [!CAUTION]
> **MISLEADING COMPARISON FLAG**: The 97.4% accuracy on Multiple Cameras Dataset is NOT a valid benchmark. With only 2 non-fall video scenarios (16 clips), the model can achieve near-perfect scores by bias toward the fall class. This result should NOT be cited as evidence of high accuracy.

**Comparability**: ⚠️ PARTIALLY COMPARABLE on UR Fall only (shared with P10) — but different preprocessing and split make direct comparison unreliable.

---

### PAPER_07 — AI Fall Detection Survey (Nahian et al., 2026, Springer Cogn. Comp.)

*Survey paper. Reports meta-statistics about the literature's performance landscape.*

| Survey Finding | Value | Source |
|---|---|---|
| **Reported accuracy range in literature** | 85%–99.6% (across varied datasets) | §4 |
| **False-positive rate problem** | Sitting/lying/bending misclassified as falls in 95%+ of papers | §5 |
| **Real-time FPS achievement** | <10% of papers achieve validated real-time on hardware | §5 |
| **Elderly subject evaluation** | Only 5% of papers include elderly subjects | §5 |
| **Common evaluation protocol** | Accuracy + sensitivity; cross-subject rarely done | §4 |
| **Statistical significance reporting** | Rarely reported | §5 |

**Key Meta-Finding**: The wide reported accuracy range (85-99.6%) across the literature is largely **non-comparable** because papers use different datasets with wildly different difficulty levels, subject counts, and activity sets. High accuracy on small controlled datasets does not indicate real-world performance.

---

### PAPER_08 — EfficientDet Person Tracking (Sivachandiran et al., 2022, Elsevier Meas. Sens.)

| Metric | Value | Dataset | Notes |
|---|---|---|---|
| **Precision (PascalVOC)** | 92.95% | PascalVOC 2012 | Explicit, §3, Table 1 |
| **Recall (PascalVOC)** | 61.86% | PascalVOC | Explicit, §3, Table 1 |
| **Average Precision/AP (PascalVOC)** | 69.94% | PascalVOC | Explicit, §3, Table 1 |
| **FPPI (PascalVOC)** | **0.047** | PascalVOC | Explicit, §3, Table 1 |
| **Precision (PenFudan)** | 86.46% | PenFudan | Explicit, §3, Table 2 |
| **Recall (PenFudan)** | 90.54% | PenFudan | Explicit, §3, Table 2 |
| **Average Precision/AP (PenFudan)** | **88.76%** | PenFudan | Explicit, §3, Table 2 |
| **Accuracy** | Not reported | — | — |
| **F1-score** | Not reported | — | — |
| **AUC** | Not reported (Precision-Recall curve referenced) | — | — |
| **FPS** | Not reported | — | — |
| **Baseline methods** | EfficientDet vs. other DL detectors (not specified clearly in extracted text) | §3 | Partial |
| **Ablation** | RMSProp optimizer effect on FPPI | §2 | Explicit |
| **Statistical significance** | Not reported | — | — |
| **Subject-independent eval** | N/A (object detection benchmark) | — | — |
| **Fall detection metrics** | N/A — person detection only | — | — |

**Performance Summary**: The recall gap on PascalVOC (61.86%) indicates EfficientDet misses many persons in cluttered scenes. PenFudan (pedestrian-focused) shows more balanced precision/recall (86%/90%). The very low FPPI (0.047) on PascalVOC indicates minimal false person detections. Important for the front-end detection component of our pipeline.

**Comparability**: ❌ NOT COMPARABLE for fall detection — this paper only addresses person detection. Different task.

---

### PAPER_09 — DL CV Systematic Review (Gaya-Morey et al., 2024, Springer Appl. Intel.)

*Review of 87 papers. Reports meta-level performance findings.*

| Survey Finding | Value | Source |
|---|---|---|
| **Accuracy range across 87 papers** | 80%–99%+ (widely varying datasets) | §4 |
| **Most common evaluation metric** | Accuracy + sensitivity/recall | §4 |
| **Cross-subject evaluation** | Rarely implemented | §5 |
| **Cross-environment evaluation** | Rarely implemented | §5 |
| **Statistical significance** | Not commonly reported | §5 |
| **False-positive from non-fall activities** | Persistent problem in >80% of papers | §5 |
| **Real-time evaluation (hardware FPS)** | <15% of papers | §5 |
| **Skeleton tracking under occlusion** | Documented breakdown; no systematic solution found | §5 |
| **Staircase-specific evaluation** | ZERO papers across 87 reviewed | §5 |

---

### PAPER_10 — Dilated Spatio-Temporal AE (Li et al., 2023, Elsevier ICT Express)

| Metric | Value | Dataset | Notes |
|---|---|---|---|
| **Accuracy (DCLSTMAE, processed UR)** | **97.1%** | UR Fall (processed depth) | Explicit, §3, Table 3 |
| **Accuracy (DCLSTMAE, raw UR)** | 86.3% | UR Fall (raw depth) | Explicit, §3, Table 3 |
| **Sensitivity (processed UR)** | **93.9%** | UR Fall | Explicit, §3, Table 5 |
| **Precision (processed UR)** | **95.1%** | UR Fall | Explicit, Table 5 |
| **F1-score (processed UR)** | **94.7%** | UR Fall | Explicit, Table 5 |
| **Specificity (processed UR)** | **98.6%** | UR Fall | Explicit, Table 5 |
| **AUC (UR raw)** | 0.65 | UR Fall (raw) | Explicit, Table 4 |
| **AUC (processed UR)** | **0.89** | UR Fall (processed) | Explicit, Table 4 |
| **AUC (Thermal dataset)** | **0.87** | Thermal | Explicit, Table 4 |
| **AUC (CAE, UR baseline)** | 0.38 | UR Fall | Explicit, Table 4 |
| **AUC (CLSTMAE, UR baseline)** | 0.49 | UR Fall | Explicit, Table 4 |
| **Model size** | 12.3 MB | — | Explicit, Table 3 |
| **Training time per epoch** | 99–128 seconds | GTX 2080Ti | Explicit, Table 3 |
| **FPS / Inference latency** | Not reported for real-time deployment | — | — |
| **Baseline methods** | CAE, CLSTMAE (both autoencoder baselines) | UR, Thermal | Table 4 |
| **Ablation** | Dilated rate (2 vs. 3); number of DCLSTM layers (2 vs. 3 vs. 4) | §3 | Explicit |
| **Statistical significance** | Not reported | — | — |
| **Subject-independent eval** | Not reported | — | — |
| **Environment-independent eval** | Partially (UR depth + Thermal dataset = 2 modalities) | — | — |

**Performance Summary**: Strong accuracy gain from depth hole-filling preprocessing: 86.3% (raw) → 97.1% (processed). AUC improvement from 0.65 → 0.89 confirms the value of the preprocessing pipeline. Comparison baselines (CAE, CLSTMAE) are reasonable but older methods.

> [!WARNING]
> **ACCURACY INFLATION ALERT**: 97.1% on the UR Fall dataset (30 fall videos, 40 ADL videos, single room, single modality) is extremely high precision on an extremely small, controlled dataset. This CANNOT be extrapolated to real-world performance.

**State-of-Art Comparison (Table 5 — UR Dataset):**

| Method | Sensitivity | F1 | Precision | Specificity | Accuracy |
|---|:---:|:---:|:---:|:---:|:---:|
| Area-FD | 98% | 90% | 83% | 89.4% | 94% |
| CNN | 100% | — | — | 92% | 95% |
| CNN-LSTM | 91.4% | 93.1% | 94.8% | — | — |
| **DCLSTMAE (proposed)** | **93.9%** | **94.7%** | **95.1%** | **98.6%** | **97.1%** |

**Comparability**: ⚠️ PARTIALLY COMPARABLE — UR dataset is shared with P06. However, P06 uses RGB and P10 uses depth. Different modalities make direct comparison inappropriate.

---

### PAPER_11 — MobileNetV2+GRU Trustworthy (Moussa et al., 2026, Elsevier ISWA)

| Metric | Value | Dataset | Notes |
|---|---|---|---|
| **Accuracy** | **97.14%** | CAUCAFall + Le2i (combined) | Explicit, Abstract |
| **Precision** | **99.26%** | CAUCAFall + Le2i | Explicit, Abstract |
| **Recall** | **96.75%** | CAUCAFall + Le2i | Explicit, Abstract |
| **F1-score** | **97.99%** | CAUCAFall + Le2i | Explicit, Abstract |
| **Best competing method accuracy** | 99.60% (prior work, different dataset/protocol) | Not directly comparable | Abstract |
| **Federated vs. Centralized accuracy gap** | 3.73 percentage points (federated lower) | CAUCAFall + Le2i | §4 |
| **MobileNetV2 feature extraction latency** | 36.22 ms (96.8% of total inference) | — | §4, Table 1 |
| **GRU inference latency** | 0.93 ms (2.5% of total) | — | §4, Table 1 |
| **Total inference latency** | ~37.4 ms per window | — | §4, Table 1 |
| **FPS (throughput)** | **~93 FPS** | GPU platform | Explicit, Abstract |
| **AUC** | Not reported | — | — |
| **False-positive rate** | Not reported as explicit metric | — | — |
| **Fairness metrics** | Consistent F1/recall/precision across fall directions (Fairlearn) | — | §4 |
| **Baseline methods** | Centralized vs. Federated learning variants; GradCAM++ ablation | §4 | Explicit |
| **Ablation** | Centralized vs. FedAvg; with/without Grad-CAM++; with/without Fairlearn | §4 | Explicit |
| **Statistical significance** | Not reported | — | — |
| **Subject-independent eval** | Not reported explicitly | — | — |
| **Environment-independent eval** | Multi-room Le2i + CAUCAFall provides limited diversity | Partial | §4 |
| **Convergence** | Accuracy stabilizes after ~15th federated round; best at round 19 | — | §4 |

**Performance Summary**: Strong and balanced metrics (97.14% accuracy, 97.99% F1). The 93 FPS throughput is the second-highest real-time result in the 12 papers (after P03's 11.5 FPS edge — note: P11 uses a GPU and is not comparable on hardware). The decomposition of inference time (MobileNetV2: 36.22ms / GRU: 0.93ms) demonstrates that backbone feature extraction dominates, making lightweight backbone selection critical for edge deployment.

**Comparability**: ⚠️ PARTIALLY COMPARABLE — Le2i is a known public benchmark shared with other papers in the broader literature but not in our 12. CAUCAFall is publicly available. Results are among the most reproducible in the set.

---

### PAPER_12 — Real-Time Vision Review (Nabizade et al., 2026, MDPI Sensors)

*PRISMA review: 11 qualifying papers (FPS ≥ 10 on hardware) from 588 total.*

| Paper in Review | Algorithm | Dataset | Accuracy | FPS | Hardware | Year |
|---|---|---|---|---|---|---|
| [18] | Pruned CNN | Custom | 99.2% Acc, 99.1% Prec | **15 FPS** | Jetson TX2 | 2019 |
| [19] | CNN+LSTM | NTU RGB+D | Not specified | **23.16 FPS** (GPU), 10.23 (CPU) | Jetson TX2 | 2020 |
| [22] | CNN+Optical Flow | Multicam, URFD | 99.00% Acc | **48 FPS** | ARM board | 2021 |
| [24] | CNN (NanoDet-Lite) | Custom | Not specified | **22.03 FPS** | Raspberry Pi 4 | 2021 |
| [25] | CNN (YOLOv3-Tiny) | SDUFall | 98.7% Acc | **20 FPS** | Jetson Xavier | 2022 |
| [26] | CNN | Custom | 84.44% Acc | **30 FPS** | Jetson Nano | 2022 |
| [28] | CNN (ONNX-converted) | AIHub Airport | Not specified | **204 FPS** (ONNX) | RTX 3080 | 2022 |
| [30] | Rule-based CNN | UP-Fall | Not specified | **15-18 FPS** | Jetson Nano | 2022 |
| [31] | 3D-CNN (pruned) | Custom | Not specified | **30 FPS** | LattePanda | 2022 |
| [32] | SSD-MobileNetV1 | Custom | mAP50: 92.70% | **14 FPS** | Raspberry Pi 4 | 2022 |
| [33] | YOLOv5-Lite | Custom | 92.10% Acc, 85.60% Rec | **25-33 FPS** | RTX 3060 | 2023 |

**Survey meta-finding**: Range of real-time results (10–204 FPS) cannot be meaningfully cross-compared — different algorithms, datasets, resolutions, and pipeline complexities. The only common thread: all 11 qualifying papers use CNN-based architectures.

---

## B. Cross-Paper Normalized Performance Matrix

> [!WARNING]
> **READ THIS FIRST**: The following table arranges metrics side-by-side for navigability ONLY. Metrics from different papers measured on different datasets are NOT directly comparable and must NOT be treated as a performance ranking. Comparability ratings are assigned per row.

| Paper | Acc | Prec | Recall | F1 | AUC | FPS (system) | Dataset | Realism | Elderly | Comparability |
|---|:---:|:---:|:---:|:---:|:---:|:---:|---|:---:|:---:|:---:|
| P01 BiMP | NR | NR | NR | NR | NR | NR | Custom BiMP | L1 | NO | ❌ None |
| P02 AI Hub | 94.35% | 89% | 90% | 89% | NR | ~3 FPS (HPE) | AI Hub CCTV | L3 | Partial | ⚠️ Partial |
| P03 Edge | 91.1% | NR | NR | NR | NR | **11.5 FPS** | Custom private | L2 | NO | ❌ None |
| P04 Tiles | ~95%+ | NR | NR | NR | NR | 0.03s latency | Custom tiles | L2 | NO | ❌ None |
| P05 MUVIM | NR | NR | NR | NR | IR: **0.94** | NR | MUVIM lab | L2 | Partial | ❌ None |
| P06 HOG+VGG | 97.4% (⚠️) | NR | NR | NR | NR | NR | MultiCam/UR | L2 | NO | ⚠️ UR only |
| P07 Survey | — | — | — | — | — | — | Literature | — | — | N/A |
| P08 EfficientDet | NR (Prec: 92.95%) | 92.95% | 61.86% | NR | NR | NR | PascalVOC | L3 | NO | ❌ Different task |
| P09 Review | — | — | — | — | — | — | Literature | — | — | N/A |
| P10 Dilated AE | 97.1% (⚠️) | 95.1% | 93.9% | 94.7% | 0.89 | NR | UR Fall | L1 | NO | ⚠️ UR only |
| P11 MobNet+GRU | **97.14%** | **99.26%** | **96.75%** | **97.99%** | NR | **~93 FPS** | Le2i+CAUCAFall | L3 | NO | ⚠️ Partial |
| P12 Review | — | — | — | — | — | — | Literature | — | — | N/A |

*NR = Not Reported. ⚠️ = Inflation risk. Bold = highest reported value in metric category.*

---

## C. Genuinely Comparable Results

Only papers sharing the **same dataset** and evaluated with comparable protocols can be meaningfully compared:

### C1. UR Fall Dataset (Shared between P06 and P10)

| Paper | Method | Modality | Accuracy | Notes |
|---|---|---|---|---|
| PAPER_06 | HOG + VGG-16 (20-frame stack) | RGB | 92.8% | Google Colab (offline) |
| PAPER_10 | DCLSTMAE (processed depth) | Depth | 97.1% | GTX 2080Ti (offline) |

**Verdict**: ⚠️ INCOMPARABLE DESPITE SHARED DATASET — different modalities (RGB vs. depth), different preprocessing, different train/test splits. P10's depth hole-filling alone accounts for ~10% accuracy boost. These results cannot be directly attributed to architecture differences.

### C2. P12 Real-Time Review — Within-Review Comparison

The 11 qualifying papers in PAPER_12 are the **most internally consistent** comparison in the literature because they all pass the same inclusion criterion (FPS ≥ 10). However, even they use different datasets, so cross-paper accuracy comparison remains invalid.

**Within-review finding**: The highest accuracy (99.2%) comes from the most aggressive model pruning (Tsai et al., Jetson TX2, 2019). Whether pruning caused accuracy benefit or whether it was dataset size/quality cannot be determined from these results.

---

## D. Ablation Studies Summary

| Paper | Ablation Compared | Key Finding |
|---|---|---|
| P02 | Real-only vs. Real+Synthetic data | +5.16% accuracy from synthetic augmentation; supports synthetic data utility |
| P02 | LSTM vs. Transformer | Comparable accuracy; Transformer slightly faster per sample |
| P02 | 5 HPE methods (speed/accuracy) | AlphaPose best accuracy but 3 FPS; MoveNet best speed but lower accuracy |
| P03 | FP32 PC vs. INT8 K210 KPU | ~5-10% IoU degradation from quantization — important edge deployment trade-off |
| P04 | ReliefF vs. F-score vs. HCM | HCM error rate ~1% vs. 30% (ReliefF) — significant feature selection improvement |
| P06 | HOG vs. Optical Flow | HOG wins on both datasets; faster and more lighting-robust |
| P10 | Dilated rate 2 vs. 3 | Rate=2 optimal (95.1% prec, 97.1% acc); rate=3 drops to 89.7%/93.4% |
| P10 | DCLSTM layers 2 vs. 3 vs. 4 | Fewer layers better on small dataset (overfitting with deeper net) |
| P10 | Raw UR vs. Processed UR | 86.3% → 97.1% from depth hole-filling preprocessing alone |
| P11 | Centralized vs. Federated | Federated 3.73% accuracy loss — reasonable trade-off for privacy |
| P11 | MobileNetV2 extraction vs. GRU | Backbone (36.22ms) dominates over GRU (0.93ms); backbone is inference bottleneck |

---

## E. Critical Performance Flags

### E1. Misleading High-Accuracy Claims
| Paper | Claimed Accuracy | Why Misleading |
|---|---|---|
| P06 | 97.4% (Multiple Cameras) | Only 2 non-fall scenarios; trivially separable negative class |
| P10 | 97.1% (UR Fall) | 70-video dataset; single room; perfectly controlled conditions |
| P03 | 91.1% (custom) | Private non-reproducible dataset; unknown demographics |

### E2. Real-Time Performance Gap
- **Only 1 paper in our 12 (P03)** demonstrates true edge real-time inference with hardware validation
- **Only 1 paper (P11)** reports GPU-level FPS for a full fall detection system
- **P12 survey** confirms: 1.9% of 588 papers validate real-time on hardware — the gap is systemic

### E3. Missing Critical Metrics
Across 12 papers, the following are **never reported**:
- False-positive rate per non-fall activity type (sitting, kneeling, bending, stair descent)
- Miss rate for actual elderly falls
- End-to-end latency (camera → alarm trigger)
- Cross-subject validation (subject-independent evaluation)
- Statistical significance testing

---

*Phase 4 Complete — Next: Phase 5 (Failure Modes and Limitations Analysis)*  
*Cross-reference: [phase3_dataset_realism.md](file:///home/endurance/Desktop/Research%20paper/literature/analysis/phase3_dataset_realism.md) | [phase2_technical_architecture.md](file:///home/endurance/Desktop/Research%20paper/literature/analysis/phase2_technical_architecture.md)*
