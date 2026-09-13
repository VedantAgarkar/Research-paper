# Phase 1 Deliverable: Comprehensive Literature Inventory & Relevance Ranking

> **Project**: Real-Time CCTV-Based Elderly Fall Detection in Staircase / Common-Area Environments  
> **Framework**: Research Roadmap Analyzer Skill (`.agents/skills/research-roadmap/SKILL.md`)  
> **Directives**: [research-paper.md](file:///home/endurance/Desktop/Research%20paper/.agents/rules/research-paper.md) & [output-for-research-gap-matrix.md](file:///home/endurance/Desktop/Research%20paper/.agents/rules/output-for-research-gap-matrix.md)  
> **Status**: Completed Phase 1 (Paper Inventory & Relevance Ranking)  
> **Deliverable Path**: `literature/analysis/paper_inventory.md` | `literature/analysis/paper_inventory.csv`

---

## 1. Executive Summary & Inventory Overview

A total of **12 peer-reviewed academic papers** (6 IEEE papers and 6 Springer/Elsevier/MDPI papers) have been comprehensively ingested, verified, and audited from the local repository folders `IEEE/` and `Springer/`.

Each paper has been evaluated against our **Target System Scenario**:
* **Scenario**: An elderly resident falls on a staircase at 8:42 PM in a common-area residential facility.
* **Computer Vision Pipeline**: Continuous CCTV video capture, human person detection, persistent multi-person tracking, 2D/3D pose estimation, and spatio-temporal posture analysis.
* **Temporal Verification**: Distinguishing true falls from normal staircase activities (stair descent, intentional sitting on steps, bending down, kneeling, stumble-recovery).
* **Edge Deployment**: Real-time execution ($\ge 10 FPS$, latency $<100 ms$) on local PC/edge computing hardware without cloud video streaming.
* **Emergency Orchestration**: Multi-tier response triggering a local hardware buzzer/alarm, remote emergency notification with location metadata ("Possible Fall Detected — Staircase, Floor 2"), visual verification frame/clip transmission, two-stage human acknowledgement countdown, and automatic escalation to secondary security if unacknowledged.

---

## 2. Master Paper Inventory & Relevance Ranking

Papers are ranked by **Relevance Score (0–5)** followed by **Methodological Usefulness Score (0–5)** according to Phase 1 standards:
- **Score 5**: Directly addresses almost the same problem / foundational guidance.
- **Score 4**: Highly relevant methodology or application domain.
- **Score 3**: Useful methodology but substantially different scenario.
- **Score 2**: Related background or divergent sensing modality.
- **Score 1**: Weakly related.
- **Score 0**: Irrelevant.

| Rank | Paper ID | Title | Authors | Year | Venue | Modality | Relevance (0–5) | Methodology (0–5) | Realism Level | Key Contribution / Focus |
|:---:|:---:|:---|:---|:---:|:---|:---:|:---:|:---:|:---:|:---|
| **1** | [**PAPER_12**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_12.md) | Real-Time Vision-Based Fall Detection Systems for the Elderly: A Systematic Review | M. Nabizade et al. | 2026 | MDPI Sensors | RGB / Depth / Edge | **5** | **5** | Level 4 (Meta-Analysis) | Proves edge hardware gap (only 11 of 588 papers report hardware FPS); sets 10 FPS threshold. |
| **2** | [**PAPER_11**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_11.md) | Trustworthy fall detection: A responsible AI approach for real-time video monitoring of the elderly | M. M. Moussa et al. | 2026 | Elsevier ISWA | RGB CCTV | **5** | **5** | Level 3 (Semi-Realistic) | MobileNetV2 + GRU sliding window (32 FPS), Grad-CAM++ visual evidence, federated learning. |
| **3** | [**PAPER_09**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_09.md) | Deep learning for computer vision based activity recognition and fall detection of the elderly: a systematic review | F. X. Gaya-Morey et al. | 2024 | Springer Appl. Intel. | CV / Skeleton / RGB | **5** | **5** | Level 4 (Meta-Analysis) | In-depth DL CV review; audits 87 papers; confirms skeleton tracking breakdown and lack of stair testing. |
| **4** | [**PAPER_02**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_02.md) | Exploring Human Pose Estimation and the Usage of Synthetic Data for Elderly Fall Detection in Real-World Surveillance | S. Juraev et al. | 2022 | IEEE Access | RGB CCTV / Pose | **4** | **4** | Level 2 (Moderately Cont.) | Benchmarks 5 pose estimators (AlphaPose, OpenPose) + Transformer/LSTM; Unity synthetic data. |
| **5** | [**PAPER_03**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_03.md) | Fall Detection System With Artificial Intelligence-Based Edge Computing | B.-S. Lin et al. | 2022 | IEEE Access | RGB Edge / BBox | **4** | **4** | Level 2 (Moderately Cont.) | Ported YOLOv3-tiny to edge accelerator (22 FPS, <3.5W); SVM posture classifier; Wi-Fi alert. |
| **6** | [**PAPER_07**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_07.md) | Artificial Intelligence for Elderly Fall Detection: State-of-the-Art Methods, Applications, and Challenges | M. J. Al Nahian et al. | 2026 | Springer Cogn. Comp. | Multi-sensor / Vision | **4** | **4** | Level 4 (Meta-Analysis) | PRISMA survey of 100+ papers; proves 95% lack elderly subjects; false alarms in sitting/lying. |
| **7** | [**PAPER_05**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_05.md) | Multi Visual Modality Fall Detection Dataset | S. Denkovski et al. | 2022 | IEEE Access | Thermal / IR / Depth | **3** | **4** | Level 2 (Moderately Cont.) | Multi-modal MMFD dataset (6 visual streams); night IR & thermal anomaly autoencoders. |
| **8** | [**PAPER_10**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_10.md) | Dilated spatial–temporal convolutional auto-encoders for human fall detection in surveillance videos | S. Li et al. | 2023 | Elsevier ICT Express | Depth / Thermal | **3** | **4** | Level 2 (Moderately Cont.) | Dilated Conv + ConvLSTM Autoencoder; expands receptive field for temporal motion anomaly scoring. |
| **9** | [**PAPER_01**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_01.md) | Bi-Modal Multiperspective Percussive (BiMP) Dataset for Visual and Audio Human Fall Detection | J. Dibble & M. Bazzocchi | 2025 | IEEE Access | RGB + Audio | **3** | **3** | Level 1 (Controlled Lab) | Synchronized 4-angle CCTV video + percussive spatial impact sound; GoogLeNet+LSTM baseline. |
| **10** | [**PAPER_08**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_08.md) | Deep Learning driven automated person detection and tracking model on surveillance videos | S. Sivachandiran et al. | 2022 | Elsevier Meas. Sens. | RGB Surveillance | **3** | **3** | Level 3 (Semi-Realistic) | EfficientDet + RMSProp optimization for multi-person CCTV tracking; solves front-end tracking. |
| **11** | [**PAPER_04**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_04.md) | Elder Tracking and Fall Detection System using Smart Tiles | M. Daher et al. | 2017 | IEEE Sensors J. | Pressure / Floor Tiles | **2** | **2** | Level 2 (Moderately Cont.) | Underfloor pressure sensors + accelerometers; non-vision floor tracking and posture analysis. |
| **12** | [**PAPER_06**](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_06.md) | Human Fall Detection in Surveillance Videos | S. Jain & K. Sitara | 2022 | IEEE INCET | RGB Surveillance | **2** | **2** | Level 2 (Moderately Cont.) | Handcrafted HOG features + shallow ANN; evaluated on small Le2i subset; no latency benchmarks. |

---

## 3. High-Level Empirical Findings & Cross-Cutting Audits

Auditing all 12 papers against the [Roadmap Evidence Hierarchy](file:///home/endurance/Desktop/Research%20paper/.agents/roadmap.md#2-research-evidence-hierarchy) yields critical empirical baseline insights:

### A. The Staircase Environment Deficit (100% Literature Void)
* **Finding**: Exactly **0 out of 12 papers** experimentally evaluate or benchmark fall detection in **staircase environments**.
* **Evidence**: Benchmark datasets utilized (UR Fall, Le2i, CAUCA Fall, Multiple FDD, MOT16/17, MMFD, BiMP) are exclusively recorded on flat floors in bedrooms, living rooms, offices, and lab stages.
* **Significance**: Staircase dynamics (steep descent velocity, banister/railing keypoint occlusions, perspective foreshortening, and confusing negative activities like walking down stairs or sitting on steps) represent an unaddressed research void.

### B. The Edge Deployment & Real-Time Gap
* **Finding**: Only **2 empirical papers** ([PAPER_03](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_03.md) and [PAPER_11](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_11.md)) report physical inference frame rates (22 FPS and 32 FPS, respectively) on edge/local hardware.
* **Evidence**: As systematically proven by [PAPER_12](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_12.md) across 588 literature records, over 98% of published papers evaluate strictly on high-powered server GPUs without testing physical hardware constraints, latency, or thermal stability.

### C. The Real-Elderly Demographic Disconnect
* **Finding**: Across all empirical papers evaluating falls ([PAPER_01](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_01.md), [PAPER_02](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_02.md), [PAPER_03](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_03.md), [PAPER_05](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_05.md), [PAPER_06](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_06.md), [PAPER_10](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_10.md), [PAPER_11](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_11.md)), **100% of fall events are simulated by young, healthy volunteers** landing on cushioned mats.
* **Evidence**: Both systematic reviews ([PAPER_07](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_07.md), [PAPER_09](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_09.md)) explicitly confirm that geriatric falls differ biomechanically (slower onset, involuntary muscle guarding, staggered collapse, secondary impacts), yet ethical constraints prevent unscripted elderly fall recording.

### D. Emergency Response & Escalation Void
* **Finding**: While [PAPER_03](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_03.md) implements a basic single-shot Wi-Fi alert and [PAPER_11](file:///home/endurance/Desktop/Research%20paper/literature/analysis/extracted_papers/PAPER_11.md) generates Grad-CAM++ visual evidence maps, **0 out of 12 papers** implement or evaluate a **multi-stage emergency response pipeline** incorporating local audio-visual alarms, human acknowledgement monitoring, and automatic timeout escalation.

---

## 4. Deliverable File Directory

The structured deliverables produced during Phase 1 have been organized within the workspace:

```
literature/
├── analysis/
│   ├── paper_inventory.csv                  # Complete CSV inventory (12 papers, all metadata)
│   ├── paper_inventory.md                   # This master synthesis deliverable
│   └── extracted_papers/                    # Individual audited records
│       ├── PAPER_01.md                      # Dibble & Bazzocchi (2025) - BiMP Dataset
│       ├── PAPER_02.md                      # Juraev et al. (2022) - Pose & Synthetic Data
│       ├── PAPER_03.md                      # Lin et al. (2022) - Edge Neuromorphic AI
│       ├── PAPER_04.md                      # Daher et al. (2017) - Smart Floor Tiles
│       ├── PAPER_05.md                      # Denkovski et al. (2022) - MMFD Dataset
│       ├── PAPER_06.md                      # Jain & Sitara (2022) - Surveillance HOG
│       ├── PAPER_07.md                      # Nahian et al. (2026) - AI Review (Cognitive Comp.)
│       ├── PAPER_08.md                      # Sivachandiran et al. (2022) - Person Tracking
│       ├── PAPER_09.md                      # Gaya-Morey et al. (2024) - DL CV Review
│       ├── PAPER_10.md                      # Li et al. (2023) - Dilated Spatio-Temporal AE
│       ├── PAPER_11.md                      # Moussa et al. (2026) - Trustworthy MobileNetV2
│       └── PAPER_12.md                      # Nabizade et al. (2026) - Real-Time Hardware Review
└── synthesis/                               # Reserved for Phases 6–9
```

---
*Executed strictly under the guidelines of `research-roadmap-analyzer` and Phase 1 Workflow.*
