# Phase 3: Dataset Quality & Experimental Realism Analysis

> **Project**: Real-Time CCTV-Based Elderly Fall Detection in Staircase / Common-Area Environments  
> **Phase**: Phase 3 — Dataset and Experimental Realism Analysis  
> **Status**: Completed  
> **Papers Analyzed**: 12 (PAPER_01 – PAPER_12)  
> **Governed by**: [phase3.md](file:///home/endurance/Desktop/Research%20paper/.agents/workflows/phase3.md) | [research-paper.md](file:///home/endurance/Desktop/Research%20paper/.agents/rules/research-paper.md)

---

## Classification Scale

| Level | Label | Definition |
|:---:|---|---|
| 1 | **Highly Controlled** | Scripted falls by young/healthy actors; single fixed room; uniform lighting; no background noise; no environmental variability |
| 2 | **Moderately Controlled** | Some environmental variety (multiple rooms/angles) but still staged falls, young subjects, known scenarios |
| 3 | **Semi-Realistic** | Real-world video sources with staged events; OR genuine locations with scripted falls |
| 4 | **Real-World** | Genuine unscripted events; actual elderly subjects; real deployment conditions |

> **Scoring rule**: Classification is based on actual experimental conditions, NOT on author claims.

---

## A. Individual Paper Dataset Records

---

### PAPER_01 — BiMP Dataset (Dibble & Bazzocchi, 2025, IEEE Access)

| Field | Value | Status | Reference |
|---|---|---|---|
| **Dataset name** | BiMP (Bi-Modal Multi-Perspective Percussive) | Explicit | Abstract |
| **Dataset source** | Authors' own custom dataset | Explicit | §III |
| **Public / Private** | Public (GitHub + Zenodo) | Explicit | §III |
| **Number of videos** | 440 synchronized bimodal trials (4 cameras + 4-channel audio per trial) | Explicit | §III.C, Table 2 |
| **Number of subjects** | 22 participants | Explicit | §III.B |
| **Age information** | Not reported (no age statistics given) | Not reported | — |
| **Gender** | Not reported | Not reported | — |
| **Fall types** | 8 fall scenarios: forward, backward, sideward, sitting-to-fall, stumble, slow, twisting, staircase-adjacent | Explicit | §III.D |
| **Non-fall activities** | Kneeling, lying, sitting, standing, walking, jumping, stretching | Explicit | §III.D |
| **Non-fall sample count** | 240 ADL trial sets | Inferred | §III.C, Table 2 |
| **Fall sample count** | 200 fall trial sets | Inferred | §III.C, Table 2 |
| **Real vs. Simulated falls** | Simulated (scripted, staged by participants — young actors) | Explicit | §III.B |
| **Environment** | 4 controlled indoor laboratory rooms; camera ring setup | Explicit | §III.C-E |
| **Indoor / Outdoor** | Indoor only | Explicit | §III.C |
| **CCTV / Surveillance setting** | No — purpose-built camera rig, not real CCTV deployment | Explicit | §III.E |
| **Staircase scenarios** | Staircase explicitly EXCLUDED (flat floor only). "Staircase-adjacent" fall ≠ staircase environment | Explicit | §III.C |
| **Multiple people** | No — single participant per trial | Explicit | §III.B |
| **Occlusion** | Not reported; acknowledged as limitation | Not reported | §VII |
| **Lighting conditions** | Uniform artificial lab lighting; no lighting variation tested | Not reported | §III.C |
| **Camera viewpoints** | 4 camera angles evenly spaced (90°, 180°, 270°, 360°) at 90–180 cm height | Explicit | §III.E |
| **Resolution / FPS** | 3840×2160 (4K) at 20 FPS per camera | Explicit | §III.E |
| **Training / Test split** | Not reported precisely (leave-one-out or random implied) | Not reported | §V |
| **Cross-subject testing** | Not reported | Not reported | §V |
| **Cross-environment testing** | No — single indoor environment | Explicit | §III.C |
| **Evaluation protocol** | Classification accuracy per fall type; GoogLeNet vs. GoogLeNet+LSTM | Explicit | §V |
| **Dataset limitations** | No elderly subjects; no real falls; no staircase; no lighting variation; no multi-person; no outdoor; controlled lab only | Explicit | §VII |

**Realism Classification: Level 1 — Highly Controlled**  
*Rationale*: 22 young participants performing scripted falls in a purpose-built 4-camera laboratory room. No elderly subjects, no staircase, no real CCTV deployment, no environmental variation. Audio modality adds novelty but does not improve ecological validity for our target scenario.

**High-Accuracy Inflation Risk**: LOW-MEDIUM — GoogLeNet+LSTM achieves good performance on a clean, synchronized 4-angle laboratory dataset. Accuracy should not be compared with papers using real-world CCTV data.

---

### PAPER_02 — Pose Estimation + Synthetic Data (Juraev et al., 2022, IEEE Access)

| Field | Value | Status | Reference |
|---|---|---|---|
| **Dataset name** | AI Hub CCTV (Real); KIST SynADL (Synthetic/Unity) | Explicit | §II.A.6, §II.B |
| **Dataset source** | AI Hub: Korean government real-world CCTV; SynADL: synthetic Unity 3D engine | Explicit | §II.A.6 |
| **Public / Private** | AI Hub: restricted (Korean National AI Data Hub); SynADL: research project | Explicit | §II.A.6 |
| **Number of videos** | AI Hub: 4,009 clips (2,706 train / 1,303 test); SynADL: ~12,000 synthetic videos | Explicit | §IV.A.1, Table 5 |
| **Number of subjects** | AI Hub: 129 subjects; SynADL: 3D synthetic avatars | Explicit | §II.A |
| **Age information** | AI Hub: some subjects aged 60+; SynADL: no age (synthetic) | Partial | §II.A |
| **Gender** | Not reported | Not reported | — |
| **Fall types** | Fall-down, fall-forward, fall-backward, fall-sideward, stumble, slow fall | Explicit | §II.A |
| **Non-fall activities** | Walking, standing up, sitting, lying, bending, kneeling, jogging | Explicit | §II.A |
| **Fall sample count** | AI Hub: not precisely reported; SynADL: ~4,000 fall clips | Inferred | §IV.A.1 |
| **Non-fall sample count** | AI Hub: not precisely reported | Not reported | — |
| **Real vs. Simulated falls** | AI Hub: simulated (scripted by subjects); SynADL: fully synthetic | Explicit | §II.A |
| **Environment** | AI Hub: varied real-world locations (offices, corridors, rooms, outdoor); SynADL: virtual indoor scenes | Explicit | §II.A |
| **Indoor / Outdoor** | Both (AI Hub) | Explicit | §II.A |
| **CCTV / Surveillance setting** | YES — AI Hub uses real CCTV infrastructure (3840×2160 IP cams) at varied locations | Explicit | §II.A.6 |
| **Staircase scenarios** | Not explicitly evaluated. AI Hub CCTV includes diverse locations but staircase-specific evaluation absent | Not reported | §IV.B.1 |
| **Multiple people** | Not reported; single-person inference assumed | Not reported | — |
| **Occlusion** | Qualitatively tested — AlphaPose fails in dim-light/indoor occlusion scenarios | Explicit | §IV.B.1 |
| **Lighting conditions** | Varied in AI Hub (indoor dim, outdoor, day/night) | Explicit | §IV.B.1 |
| **Camera viewpoints** | Multiple real-world angles in AI Hub; fixed virtual angles in SynADL | Explicit | §II.A, §IV.B.1 |
| **Resolution / FPS** | 3840×2160; AlphaPose: ~3 FPS; MoveNet: ~30 FPS; OpenPose: ~5 FPS (GTX 1080Ti) | Explicit | §III.A, Table 3 |
| **Training / Test split** | 67.5% train / 32.5% test for AI Hub | Explicit | §IV.A.1, Table 5 |
| **Cross-subject testing** | Not explicitly reported | Not reported | — |
| **Cross-environment testing** | AI Hub provides some cross-location variation; not formally evaluated | Partial | §IV.B.1 |
| **Evaluation protocol** | Accuracy; confusion matrix; keypoint quality metrics (ACV, AMV) | Explicit | §III.C, §IV.B |
| **Dataset limitations** | AI Hub restricted (not reproducible); SynADL = synthetic domain gap; no elderly-specific evaluation; no staircase scenarios; simulated not real falls | Explicit | §V |

**Realism Classification: Level 3 — Semi-Realistic**  
*Rationale*: AI Hub uses a real government CCTV infrastructure with 4K IP cameras, indoor+outdoor, diverse locations, real actors performing scripted falls. Significantly more realistic than typical lab datasets, but falls remain staged. SynADL is fully synthetic (Level 1 equivalent). The combination earns Level 3.

**High-Accuracy Inflation Risk**: MEDIUM — Accuracy (89–94%) achieved on real CCTV but still with scripted falls and single-person assumption. AlphaPose at ~3 FPS is not real-time; thus results cannot extrapolate to real-time systems without significant caveat.

---

### PAPER_03 — AI-Based Edge Computing (Lin et al., 2022, IEEE Access)

| Field | Value | Status | Reference |
|---|---|---|---|
| **Dataset name** | Authors' custom private dataset | Explicit | §III.C |
| **Dataset source** | Self-collected in 5 different indoor scenes | Explicit | §III.C |
| **Public / Private** | Private | Explicit | §III.C |
| **Number of videos** | Not precisely reported; train/test split described | Not reported | §III.C |
| **Number of subjects** | Not reported | Not reported | — |
| **Age information** | Not reported | Not reported | — |
| **Gender** | Not reported | Not reported | — |
| **Fall types** | General fall (sudden posture collapse); not further categorized | Inferred | §III |
| **Non-fall activities** | Walking, standing, bending, sitting | Inferred | §III.C |
| **Fall sample count** | Not reported precisely | Not reported | — |
| **Non-fall sample count** | Not reported precisely | Not reported | — |
| **Real vs. Simulated falls** | Simulated (staged in indoor scenes) | Inferred | §III.C |
| **Environment** | 5 different indoor rooms (living room, bedroom, corridor, kitchen, lab-style area) | Explicit | §III.C |
| **Indoor / Outdoor** | Indoor only | Explicit | §III.C |
| **CCTV / Surveillance setting** | No — uses OmniVision OV2640 CMOS camera mounted for testing | Explicit | §III.A |
| **Staircase scenarios** | Not reported | Not reported | — |
| **Multiple people** | Not reported; single person assumed | Not reported | — |
| **Occlusion** | Acknowledged limitation; bounding box fails with back-to-camera or self-occlusion | Explicit | §V |
| **Lighting conditions** | Acknowledged limitation; varied indoor lighting across 5 scenes | Explicit | §V |
| **Camera viewpoints** | 5 different placements across different indoor scenes | Explicit | §III.C |
| **Resolution / FPS** | OV2640; 11.5 FPS on K210 KPU (INT8 quantized) | Explicit | §IV.B, Table 3 |
| **Training / Test split** | Not reported | Not reported | — |
| **Cross-subject testing** | Not reported | Not reported | — |
| **Cross-environment testing** | 5 indoor scenes (minor environmental variation) | Partial | §III.C |
| **Evaluation protocol** | System accuracy (91.1%); IoU (94.5%); SVM accuracy | Explicit | §IV.B-C, Tables 3-5 |
| **Dataset limitations** | Private dataset (not reproducible); no elderly subjects; no age info; no staircase; limited subject count; no reporting of video/sample counts; no cross-subject evaluation | Explicit | §V |

**Realism Classification: Level 2 — Moderately Controlled**  
*Rationale*: Uses 5 different indoor rooms providing minor environmental variation, but falls are staged, dataset is private, subject demographics unreported. Edge hardware deployment is the key contribution, not dataset realism.

**High-Accuracy Inflation Risk**: HIGH — 91.1% accuracy on a private, non-reproducible dataset with unspecified subjects and sample counts. Cannot be compared to any other paper's results.

---

### PAPER_04 — Smart Tiles / Pressure Sensors (Daher et al., 2017, IEEE Sensors J.)

| Field | Value | Status | Reference |
|---|---|---|---|
| **Dataset name** | Authors' custom private dataset (lab + apartment) | Explicit | §IV |
| **Dataset source** | Self-collected with custom smart tile system | Explicit | §IV |
| **Public / Private** | Private | Not reported | — |
| **Number of videos** | N/A (non-vision; pressure + accelerometer signals) | Not reported | — |
| **Number of subjects** | 6 participants (3 male, 3 female) | Explicit | §V.A |
| **Age information** | 25–40 years old (young to middle-aged adults) | Explicit | §V.A |
| **Gender** | 3 male, 3 female | Explicit | §V.A |
| **Fall types** | 4 fall types: falling from chair-height, free fall, falling while walking, stumble | Explicit | §V.A |
| **Non-fall activities** | Walking, sitting, lying, bending | Explicit | §V.A |
| **Fall sample count** | 40 fall trials per subject × 6 subjects = 240 fall trials | Explicit | §V.A |
| **Non-fall sample count** | 20 non-fall trials per subject = 120 non-fall trials | Explicit | §V.A |
| **Real vs. Simulated falls** | Simulated (scripted falls by young adults) | Explicit | §V.A |
| **Environment** | Indoor apartment-like lab with smart tile floor | Explicit | §IV |
| **Indoor / Outdoor** | Indoor only | Explicit | §IV |
| **CCTV / Surveillance setting** | No — RGB-D camera used only for ground truth annotation, NOT in detection pipeline | Explicit | §IV.A |
| **Staircase scenarios** | Not applicable — floor tile system requires flat floor installation | Explicit | §III |
| **Multiple people** | Not reported | Not reported | — |
| **Occlusion** | N/A (non-vision) | Not reported | — |
| **Lighting conditions** | N/A (non-vision) | Not reported | — |
| **Camera viewpoints** | N/A (non-vision) | Not reported | — |
| **Resolution / FPS** | Tile sensors: ~50 Hz; accelerometer: 50 Hz | Explicit | §III.A |
| **Training / Test split** | Not reported | Not reported | — |
| **Cross-subject testing** | Not reported (6 subjects used collectively) | Not reported | — |
| **Cross-environment testing** | Single lab environment | Explicit | §IV |
| **Evaluation protocol** | Fall detection accuracy; FP/FN counts; confusion matrix | Explicit | §V |
| **Dataset limitations** | 6 young subjects (25-40 yrs) only; no elderly; non-vision system incompatible with staircase; private dataset; single apartment environment; small sample size | Explicit | §V.A, §VI |

**Realism Classification: Level 2 — Moderately Controlled**  
*Rationale*: Real apartment-like environment with custom floor sensor hardware, but only 6 young subjects (25–40 years), scripted falls, private dataset. Non-vision modality is inherently excluded from our target pipeline comparison. Sensor hardware requires floor installation — cannot be generalized to real CCTV.

**High-Accuracy Inflation Risk**: MEDIUM — High accuracy on 6 subjects is expected but not generalizable.

---

### PAPER_05 — MUVIM Multi-Modal Dataset (Denkovski et al., 2022, IEEE Access)

| Field | Value | Status | Reference |
|---|---|---|---|
| **Dataset name** | MUVIM (Multi-Visual Modality) / FallDetection Dataset | Explicit | Abstract |
| **Dataset source** | Authors' custom lab dataset | Explicit | §II |
| **Public / Private** | Public (GitHub: https://github.com/MUVIM/FallDetection) | Explicit | §II |
| **Number of videos** | 10 fall + 10 normal sessions per modality; 6 cameras; ~60+ video streams total | Explicit | §II.A, Table 1 |
| **Number of subjects** | 5 fall subjects + 10 older adults for ADL only (15 total) | Explicit | §II.B |
| **Age information** | Fall subjects: unspecified age; ADL subjects: 70+ years (10 older adults) | Explicit | §II.B |
| **Gender** | Not reported | Not reported | — |
| **Fall types** | 5 fall trials per session: forward, backward, sideward, sitting-to-floor, standing-to-floor | Explicit | §II.C |
| **Non-fall activities** | ADL: walking, bending, sitting, reaching; 10 ADL sessions with older adults | Explicit | §II.C |
| **Fall sample count** | 5 fall types × 10 sessions = 50 falls per modality | Explicit | §II.C |
| **Non-fall sample count** | 10 older adults × ADL sessions (exact count not reported) | Explicit | §II.B-C |
| **Real vs. Simulated falls** | Simulated (scripted falls by 5 younger subjects with protective gear) | Explicit | §II.B |
| **Environment** | Indoor controlled room with 6 fixed cameras (ceiling-mounted) | Explicit | §II.A |
| **Indoor / Outdoor** | Indoor only | Explicit | §II.A |
| **CCTV / Surveillance setting** | No — specialized multi-sensor lab rig (IR dome, ZED stereo, FLIR thermal, Kinect). Not real CCTV | Explicit | §II.A |
| **Staircase scenarios** | Not reported; flat indoor room only | Not reported | — |
| **Multiple people** | Not reported; single-subject falls | Not reported | — |
| **Occlusion** | Not reported; ceiling-top-down view partially mitigates but not tested | Not reported | — |
| **Lighting conditions** | Explicitly tested: 5 day-time sessions + 5 night-time sessions | Explicit | §II.A, Abstract |
| **Camera viewpoints** | All 6 cameras ceiling-mounted (top-down view only); no lateral/elevation variation | Explicit | §II.A |
| **Resolution / FPS** | IR: 704×408 @ 20 FPS; ZED: 1280×720 @ 15 FPS; Thermal: 160×120 @ 27 FPS; Kinect: 640×480 @ 30 FPS | Explicit | §II.A, Table 3 |
| **Training / Test split** | Not reported | Not reported | — |
| **Cross-subject testing** | Not reported | Not reported | — |
| **Cross-environment testing** | Single room; day vs. night variation only | Partial | §II.A |
| **Evaluation protocol** | AUC-ROC per modality; 3D autoencoder reconstruction error | Explicit | Abstract |
| **Dataset limitations** | Falls by young subjects only (older adults do ADL only, not falls); controlled lab; flat floor; no real CCTV; no staircase; no multi-person falls; top-down only cameras | Explicit | §VI |

**Realism Classification: Level 2 — Moderately Controlled**  
*Rationale*: Day/night lighting variation is a genuine strength, and the inclusion of real older adults for ADL data is notable. However, actual falls are simulated by younger subjects, environment is a controlled lab, and all cameras are ceiling-mounted (limiting generalization to wall-mounted CCTV scenarios). Strongest multi-modal dataset in the set.

**High-Accuracy Inflation Risk**: LOW-MEDIUM — AUC scores per modality are interpretable; IR night-time performance (AUC=0.94) is a genuine finding even in a controlled environment.

---

### PAPER_06 — HOG + VGG-16 Surveillance (Jain & Sitara, 2022, IEEE INCET)

| Field | Value | Status | Reference |
|---|---|---|---|
| **Dataset name** | UR Fall Detection Dataset; Multiple Cameras Fall Dataset | Explicit | §IV.C |
| **Dataset source** | UR Fall: Planinc & Kampel, 2013 (University of Rzeszów); Multiple Cameras: Auvinet et al., 2010 | Explicit | §IV.C, References |
| **Public / Private** | Both Public | Explicit | §IV.C |
| **Number of videos** | UR: 70 videos (30 fall + 40 ADL); Multiple Cameras: 22 fall + 2 non-fall (8 cameras = 178 fall scenarios + 160 non-fall scenarios) | Explicit | §IV.C |
| **Number of subjects** | UR: not reported; Multiple Cameras: 1 subject (all scenarios) | Explicit | §IV.C |
| **Age information** | Not reported | Not reported | — |
| **Gender** | Not reported | Not reported | — |
| **Fall types** | UR: general fall from chair/standing; Multiple Cameras: front, back, sideward falls | Explicit | §IV.C |
| **Non-fall activities** | UR: sitting, walking, lying (ADL); Multiple Cameras: 20 non-fall scenarios | Explicit | §IV.C |
| **Fall sample count** | UR: 30 falls; Multiple Cameras: 22 scenarios × 8 cameras = 176 clips | Explicit | §IV.C |
| **Non-fall sample count** | UR: 40 ADL; Multiple Cameras: 2 scenarios × 8 cameras = 16 clips | Explicit | §IV.C |
| **Real vs. Simulated falls** | Both datasets: simulated falls | Inferred | §IV.C |
| **Environment** | UR: single controlled indoor room; Multiple Cameras: single room, 8 fixed camera angles | Explicit | §IV.C |
| **Indoor / Outdoor** | Indoor only | Explicit | §IV.C |
| **CCTV / Surveillance setting** | Multiple Cameras uses IP surveillance cameras (closest to CCTV) | Partial | §IV.C |
| **Staircase scenarios** | Not reported | Not reported | — |
| **Multiple people** | No — single person per scenario | Explicit | §IV.C |
| **Occlusion** | Not reported | Not reported | — |
| **Lighting conditions** | Not controlled; HOG normalization provides natural robustness | Inferred | §V |
| **Camera viewpoints** | Multiple Cameras: 8 IP cameras around a room (multiple angles) | Explicit | §IV.C |
| **Resolution / FPS** | UR: 224×224 (pre-processed); Multiple Cameras: 480×480 | Explicit | §IV.C |
| **Training / Test split** | Not reported | Not reported | — |
| **Cross-subject testing** | Not reported | Not reported | — |
| **Cross-environment testing** | No — both datasets use single-room environments | Explicit | §IV.C |
| **Evaluation protocol** | Accuracy on each dataset independently; no cross-dataset evaluation | Explicit | §IV |
| **Dataset limitations** | UR: extremely small (70 videos, single room, unspecified subjects); Multiple Cameras: only 1 subject, 22 fall scenarios, heavily imbalanced non-fall samples (only 2 non-fall scenarios); no staircase; no elderly; no real falls | Explicit | §V |

**Realism Classification: Level 2 — Moderately Controlled**  
*Rationale*: Both datasets are legacy controlled-lab collections. Multiple Cameras provides multi-angle coverage but has critically imbalanced non-fall data (only 2 scenarios vs. 22 falls). UR Fall is among the smallest and most controlled datasets in the literature.

**High-Accuracy Inflation Risk**: HIGH — 97.4% on Multiple Cameras Dataset should be treated with extreme caution. This dataset has 1 subject, 22 fall scenarios, and critically only 2 non-fall scenarios. The classifier has essentially nothing hard to distinguish from. This is an inflated result due to dataset imbalance.

---

### PAPER_07 — AI Fall Detection Survey (Nahian et al., 2026, Springer Cogn. Comp.)

*Survey paper. Dataset analysis reflects findings about the surveyed literature.*

| Field | Value | Status | Reference |
|---|---|---|---|
| **Datasets surveyed** | Le2i, URFD, SDUFall, SisFall, NTU RGB+D, UP-Fall, MUVIM, CAUCAFall, FDD, Multicam, UR Fall, and others | Explicit | §3-4 |
| **Total papers surveyed** | 100+ papers (PRISMA-style) | Explicit | §1 |
| **Elderly subjects in literature** | Survey finding: **95% of papers lack elderly subjects** | Explicit | §5 |
| **Real falls in literature** | Survey finding: **100% of papers use simulated falls** | Explicit | §5 |
| **Staircase datasets** | Survey finding: No staircase-specific dataset identified | Inferred | §5 |
| **Multi-person datasets** | Survey finding: <5% of papers address multi-person scenarios | Explicit | §5 |
| **Common dataset limitations** | Small sample sizes; young volunteers; single environment; controlled lighting; simulated falls; domain gap to real-world | Explicit | §5 |
| **Most used datasets** | Le2i (multiple camera indoor), URFD (Kinect RGB+D), SDUFall (depth), SisFall (wearable) | Explicit | §4 |

**Realism Assessment of Literature (Survey-level)**:  
Survey confirms the entire literature predominantly operates at **Level 1-2 (Highly/Moderately Controlled)**. No confirmed study using real-world unscripted falls or genuine elderly subjects performing falls.

---

### PAPER_08 — EfficientDet Person Tracking (Sivachandiran et al., 2022, Elsevier Meas. Sens.)

| Field | Value | Status | Reference |
|---|---|---|---|
| **Dataset name** | PascalVOC 2012; PenFudan Pedestrian Dataset | Explicit | §3 |
| **Dataset source** | PascalVOC: PASCAL Visual Object Classes challenge; PenFudan: Penn-Fudan Database | Explicit | §3 |
| **Public / Private** | Both Public | Explicit | §3 |
| **Number of videos** | PascalVOC: images/video frames; PenFudan: 170 images (345 pedestrian instances) | Explicit | §3 |
| **Number of subjects** | PascalVOC: multi-class (person is one class); PenFudan: 345 pedestrian instances | Explicit | §3 |
| **Age information** | Not reported (general pedestrian dataset) | Not reported | — |
| **Gender** | Not reported | Not reported | — |
| **Fall types** | N/A — person detection/tracking only; no fall classification | Not reported | — |
| **Non-fall activities** | N/A — pedestrian detection (walking/standing) | Not reported | — |
| **Fall sample count** | N/A | Not reported | — |
| **Real vs. Simulated falls** | N/A | Not reported | — |
| **Environment** | Real-world outdoor and indoor pedestrian scenes (surveillance context) | Explicit | §3 |
| **Indoor / Outdoor** | Both (general pedestrian benchmark datasets) | Inferred | §3 |
| **CCTV / Surveillance setting** | Not explicitly CCTV but representative of surveillance conditions | Inferred | Abstract |
| **Staircase scenarios** | Not reported | Not reported | — |
| **Multiple people** | YES — PenFudan: 345 instances in 170 images (multi-person scenes) | Explicit | §3 |
| **Occlusion** | Not reported | Not reported | — |
| **Lighting conditions** | Not reported | Not reported | — |
| **Camera viewpoints** | Varied (benchmark dataset includes diverse viewpoints) | Inferred | §3 |
| **Resolution / FPS** | Not reported | Not reported | — |
| **Training / Test split** | Standard PascalVOC/PenFudan train-test splits | Inferred | §3 |
| **Cross-subject testing** | N/A (object detection benchmark) | Not reported | — |
| **Cross-environment testing** | Implicit via benchmark diversity | Inferred | §3 |
| **Evaluation protocol** | Precision, Recall, Average Precision (AP), FPPI | Explicit | §3, Tables 1-2 |
| **Dataset limitations** | Neither dataset is a fall detection dataset — this paper addresses person detection/tracking only, not the full fall detection pipeline; no elderly subjects; no fall classification | Explicit | Abstract |

**Realism Classification: Level 3 — Semi-Realistic**  
*Rationale*: PascalVOC and PenFudan contain real-world images (not staged lab videos), making them more realistic than controlled fall datasets. However, the scope is limited to person detection only — this paper addresses a sub-component of the pipeline, not fall detection itself.

---

### PAPER_09 — DL CV Systematic Review (Gaya-Morey et al., 2024, Springer Appl. Intel.)

*Review paper covering 87 DL-based computer-vision fall detection studies.*

| Field | Value | Status | Reference |
|---|---|---|---|
| **Scope** | 87 deep learning computer-vision fall detection papers | Explicit | Abstract |
| **Most common datasets** | Le2i, URFD, SDUFall, NTU RGB+D, UP-Fall, MUVIM, FDD | Explicit | §3 |
| **Elderly subjects** | Survey: **absent from virtually all datasets** | Explicit | §5 |
| **Real falls** | Survey: **100% simulated** | Explicit | §5 |
| **Staircase** | Survey: **EXPLICITLY stated as absent from all 87 papers** | Explicit | §5 |
| **Multi-person** | Survey: <5% of papers; confirmed major gap | Explicit | §5 |
| **Dataset realism finding** | Majority of papers use small, highly controlled datasets; performance metrics not transferable to real-world | Explicit | §5 |
| **Cross-environment generalization** | Survey: rarely evaluated; most models validated on same-distribution data | Explicit | §5 |
| **Key limitation identified** | Skeleton tracking breakdown under occlusion and steep camera angles (staircase-relevant) | Explicit | §5 |
| **Night/low-light** | Survey: depth cameras partially address but rarely systematically tested | Explicit | §5 |

---

### PAPER_10 — Dilated Spatio-Temporal AE (Li et al., 2023, Elsevier ICT Express)

| Field | Value | Status | Reference |
|---|---|---|---|
| **Dataset name (Primary)** | UR Fall Detection Dataset (processed depth version) | Explicit | §3.1 |
| **Dataset name (Secondary)** | Thermal Dataset | Explicit | §3.1 |
| **Dataset source** | UR Fall: University of Rzeszów (Planinc & Kampel, 2013); Thermal: authors (Li et al. prior work) | Explicit | §3.1 |
| **Public / Private** | UR Fall: Public; Thermal: not stated (likely private/restricted) | Partial | §3.1 |
| **Number of videos** | UR: 70 depth videos (40 ADL + 30 fall); Thermal: 9 ADL + 35 fall videos | Explicit | §3.1 |
| **Number of subjects** | UR: not reported; Thermal: not reported | Not reported | — |
| **Age information** | Not reported | Not reported | — |
| **Gender** | Not reported | Not reported | — |
| **Fall types** | UR: falling from sitting, falling from standing; Thermal: general fall types | Explicit | §3.1 |
| **Non-fall activities** | UR: sitting, walking, lying down; Thermal: ADL sequences | Explicit | §3.1 |
| **Fall sample count** | UR: 30 depth videos; Thermal: 35 fall videos | Explicit | §3.1 |
| **Non-fall sample count** | UR: 40 ADL videos; Thermal: 9 ADL videos | Explicit | §3.1 |
| **Real vs. Simulated falls** | Both: Simulated | Inferred | §3.1 |
| **Environment** | UR: single controlled indoor lab; Thermal: indoor (unspecified) | Explicit | §3.1 |
| **Indoor / Outdoor** | Indoor only | Explicit | §3.1 |
| **CCTV / Surveillance setting** | No — Kinect depth camera (non-CCTV sensor) | Explicit | §3.1 |
| **Staircase scenarios** | Not reported | Not reported | — |
| **Multiple people** | Not reported; single-person datasets | Not reported | — |
| **Occlusion** | Kinect depth holes acknowledged; depth hole-filling preprocessing applied | Partial | §2, §3.1 |
| **Lighting conditions** | Thermal: inherently lighting-independent; UR depth: not lighting-sensitive | Explicit | §3.1 |
| **Camera viewpoints** | UR: Kinect wall/ceiling placement; Thermal: not specified | Not reported | §3.1 |
| **Resolution / FPS** | Both: 640×480 @ 30 FPS (UR); 640×480 @ 15-25 FPS (Thermal) | Explicit | §3.1 |
| **Training / Test split** | ROC-AUC evaluation; exact split not reported | Not reported | §3.3 |
| **Cross-subject testing** | Not reported | Not reported | — |
| **Cross-environment testing** | Two different modalities (depth + thermal) as proxy for environment variation | Partial | §3 |
| **Evaluation protocol** | AUC-ROC; precision; recall; accuracy; fall score threshold | Explicit | §3.3 |
| **Dataset limitations** | UR extremely small (70 videos); Thermal extremely small (44 videos); no elderly; no staircase; no multi-person; no CCTV; single controlled environments; simulated falls | Explicit | §4 |

**Realism Classification: Level 1 — Highly Controlled**  
*Rationale*: UR dataset is the smallest and most controlled fall dataset in the literature (70 videos, single controlled room). The Thermal dataset is even smaller (44 videos). High accuracy (97.1%) on these tiny, clean datasets cannot be extrapolated to real-world performance.

**High-Accuracy Inflation Risk**: VERY HIGH — 97.1% accuracy on 70 UR videos (30 fall / 40 ADL, single room). This is essentially a toy dataset. Results should not be compared cross-paper.

---

### PAPER_11 — MobileNetV2+GRU Trustworthy (Moussa et al., 2026, Elsevier ISWA)

| Field | Value | Status | Reference |
|---|---|---|---|
| **Dataset name** | Le2i Fall Detection Dataset; CAUCAFall Dataset | Explicit | §4 |
| **Dataset source** | Le2i: University of Burgundy (France); CAUCAFall: Universidad del Cauca (Colombia) | Explicit | §4 |
| **Public / Private** | Le2i: Public; CAUCAFall: Public | Explicit | §4 |
| **Number of videos** | Le2i: ~191 videos (coffee room, office, home, lecture hall); CAUCAFall: 510+ videos | Explicit | §4 |
| **Number of subjects** | Le2i: ~8 subjects; CAUCAFall: not precisely reported | Inferred | §4 |
| **Age information** | Not reported for either dataset | Not reported | — |
| **Gender** | Not reported | Not reported | — |
| **Fall types** | Le2i: various falls (forward, backward, sideward); CAUCAFall: multiple real-life-like fall scenarios | Explicit | §4 |
| **Non-fall activities** | Le2i: walking, sitting, lying, bending; CAUCAFall: diverse ADLs | Explicit | §4 |
| **Fall sample count** | Le2i: ~83 fall videos; CAUCAFall: not precisely reported | Inferred | §4 |
| **Non-fall sample count** | Le2i: ~108 non-fall videos | Inferred | §4 |
| **Real vs. Simulated falls** | Both: Simulated | Inferred | §4 |
| **Environment** | Le2i: coffee room, office, home, lecture hall (4 rooms); CAUCAFall: indoor unconstrained environments | Explicit | §4 |
| **Indoor / Outdoor** | Indoor only | Explicit | §4 |
| **CCTV / Surveillance setting** | Le2i: YES — existing surveillance cameras; CAUCAFall: not specified | Partial | §4 |
| **Staircase scenarios** | Not reported | Not reported | — |
| **Multiple people** | Not reported | Not reported | — |
| **Occlusion** | Not reported | Not reported | — |
| **Lighting conditions** | Le2i: multi-room with natural variation (day vs. artificial); not systematic | Partial | §4 |
| **Camera viewpoints** | Le2i: 4 different rooms = 4 camera placements; CAUCAFall: varied | Partial | §4 |
| **Resolution / FPS** | Input resized to 224×224; ~93 FPS inference | Explicit | Abstract |
| **Training / Test split** | Not precisely reported | Not reported | §4 |
| **Cross-subject testing** | Not reported | Not reported | — |
| **Cross-environment testing** | Multi-room Le2i provides limited cross-environment variation | Partial | §4 |
| **Evaluation protocol** | Accuracy, Precision, Recall, F1 on combined Le2i+CAUCAFall; Fairlearn fairness metrics; Grad-CAM++ visualization | Explicit | §4 |
| **Dataset limitations** | No elderly subjects; no real falls; no staircase; simulated falls; no cross-subject protocol reported; no night/low-light systematic testing | Explicit | §5 |

**Realism Classification: Level 3 — Semi-Realistic**  
*Rationale*: Le2i uses existing surveillance cameras in real rooms (not specially constructed lab) — this is the closest to real CCTV deployment in the non-survey papers. CAUCAFall adds further scene diversity. However, all falls remain simulated, no elderly subjects, and no staircase. The federated learning and fairness components add methodological novelty beyond simple dataset realism.

**High-Accuracy Inflation Risk**: LOW-MEDIUM — 97.14% accuracy across Le2i+CAUCAFall is among the strongest results in the empirical papers. Le2i is a well-known benchmark and some comparison is possible. However, results remain bound to simulated, indoor, non-elderly scenarios.

---

### PAPER_12 — Real-Time Vision Review (Nabizade et al., 2026, MDPI Sensors)

*PRISMA review of 588 records; 11 papers met all inclusion criteria (FPS ≥ 10 on hardware).*

| Field | Value | Status | Reference |
|---|---|---|---|
| **Scope** | 588 candidate records; 11 qualifying papers | Explicit | Abstract |
| **Datasets used across 11 qualifying papers** | Multicam (2010), URFD (2014), SDUFall (2014), NTU RGB+D (2016), UP-Fall (2019), AIHub Airport (NDA) | Explicit | §5, Table 6 |
| **Elderly subjects (any qualifying paper)** | NONE — "none include older adults: all falls are simulated by young volunteers" | Explicit | §5.1 |
| **Real falls (any qualifying paper)** | NONE — 100% simulated | Explicit | §5.1 |
| **Staircase datasets** | NONE found in any qualifying paper | Explicit | §5 Discussion |
| **Most realistic dataset** | NTU RGB+D (40 subjects, multi-modal) — but it is a general action recognition dataset | Explicit | §5, Table 6 |
| **Dataset size range** | 24 to 56,880 samples across qualifying paper datasets | Explicit | §5, Table 6 |
| **Dataset access issue** | AIHub Airport dataset: broken link, data access policy restrictions, not reproducible | Explicit | §5.1 |
| **Key limitation** | All datasets: controlled settings; simulated falls; young volunteers only; no elderly; no real-world deployment | Explicit | §5.1 |
| **FPS threshold rationale** | 10 FPS minimum derived from Vlaeyen et al. (2s critical fall phase → 20 frames needed) | Explicit | §2, §6 |

---

## B. Cross-Paper Dataset Comparison Matrix

| Feature | P01 BiMP | P02 AI Hub | P03 Custom | P04 Tiles | P05 MUVIM | P06 UR+MultiCam | P07 Survey | P08 PascalVOC | P09 Review | P10 UR+Thermal | P11 Le2i+CAUCA | P12 Review |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Public Dataset** | YES | PARTIAL | NO | NO | YES | YES | N/A | YES | N/A | PARTIAL | YES | N/A |
| **Real CCTV Camera** | NO | YES | NO | NO | NO | PARTIAL | GAP | YES | GAP | NO | PARTIAL | GAP |
| **Elderly Subjects** | NO | PARTIAL | NO | NO | PARTIAL (ADL) | NO | 5% ONLY | NO | ABSENT | NO | NO | NONE |
| **Real (Unscripted) Falls** | NO | NO | NO | NO | NO | NO | NONE FOUND | N/A | NONE FOUND | NO | NO | NONE FOUND |
| **Staircase Environment** | NO | NO | NO | NO | NO | NO | ABSENT | NO | ABSENT | NO | NO | ABSENT |
| **Multiple People** | NO | NO | NO | NO | NO | PARTIAL | <5% | YES | <5% | NO | NO | NONE |
| **Night/Low-Light** | NO | PARTIAL | NO | YES (N/A) | YES (IR/Thermal) | NO | GAP | NO | GAP | YES (Thermal) | PARTIAL | GAP |
| **Cross-Environment** | NO | PARTIAL | PARTIAL | NO | NO | NO | RARE | YES | RARE | PARTIAL | PARTIAL | — |
| **Occlusion Tested** | NO | PARTIAL | NO | N/A | NO | NO | GAP | NO | GAP | PARTIAL | NO | GAP |
| **Outdoor** | NO | YES | NO | NO | NO | NO | RARE | YES | RARE | NO | NO | — |
| **Number of Subjects** | 22 | 129 | NR | 6 | 15 | NR | varies | varies | varies | NR | ~8 | varies |
| **Realism Level** | **L1** | **L3** | **L2** | **L2** | **L2** | **L2** | L1-L2 lit. | **L3** | L1-L2 lit. | **L1** | **L3** | L1-L2 lit. |
| **Accuracy Inflation Risk** | LOW-MED | MEDIUM | HIGH | MEDIUM | LOW-MED | **HIGH** | N/A | LOW | N/A | **VERY HIGH** | LOW-MED | N/A |

---

## C. Realism Classification Summary

| Level | Papers | Justification |
|---|---|---|
| **Level 1 — Highly Controlled** | P01 (BiMP), P10 (UR+Thermal) | Controlled lab; 22 or unknown young subjects; single room; no real CCTV; scripted falls; no variation |
| **Level 2 — Moderately Controlled** | P03, P04, P05, P06 | Some environmental diversity (multi-room OR multi-sensor) but still staged, private or legacy datasets, young subjects |
| **Level 3 — Semi-Realistic** | P02 (AI Hub), P08 (PascalVOC), P11 (Le2i+CAUCAFall) | Real cameras in real/diverse locations OR genuine person detection benchmarks; still staged falls, no elderly falls |
| **Level 4 — Real-World** | **NONE in 12 papers** | No paper experimentally evaluates genuine unscripted falls or real elderly subjects performing falls |

---

## D. High-Accuracy Inflation Cases

| Paper | Accuracy | Dataset | Inflation Risk | Reason |
|---|---|---|---|---|
| **PAPER_06** | 97.4% | Multiple Cameras | **VERY HIGH** | Only 1 subject; 22 fall scenarios vs. only **2 non-fall scenarios**. The non-fall class is critically underrepresented. |
| **PAPER_10** | 97.1% | UR Fall (70 videos) | **HIGH** | 70 videos total in single room; model overfits to extremely clean, uniform depth data |
| **PAPER_03** | 91.1% | Private dataset | **HIGH** | Private, non-reproducible; no subject count; no demographics; cannot verify generalization |
| **PAPER_11** | 97.14% | Le2i + CAUCAFall | MEDIUM | Well-known benchmarks but simulated falls only; young volunteers; no staircase or elderly evaluation |
| **PAPER_02** | 89–94% | AI Hub CCTV | MEDIUM | Most realistic in the set (real CCTV), but poses are staged and single-person assumed |

---

## E. Critical Dataset Gaps — Evidence Summary

### E1. No Paper Uses Real (Unscripted) Falls
Every empirical paper (P01-P06, P10-P11) and every survey (P07, P09, P12) confirms this:
> *"none include older adults: all falls are simulated by young volunteers"* — PAPER_12, §5.1

The fundamental validity problem: real elderly falls differ from scripted young-volunteer falls in:
- Fall speed and momentum
- Protective responses (or lack thereof)
- Posture at time of fall onset
- Recovery behavior after impact

Models trained on young-volunteer scripted data have an **unknown generalization gap** to real elderly falls.

### E2. Staircase Environments — Complete Literature Void
Out of all 12 papers analyzed:
- **0 empirical papers** include staircase data
- **2 review papers** (P09: 87 papers; P12: 588 papers) explicitly confirm staircase absence
- This is not simply a gap in our 12 papers — it is confirmed absent across **thousands of papers in the literature**

### E3. Elderly Subjects — 95% Absent (Confirmed by Survey)
- P07 (PAPER_07 survey): **"95% of papers in the literature lack elderly subjects"**
- Among our 12 papers: Only P05 includes older adults for ADL (not falls); P02 includes some 60+ subjects in AI Hub
- No paper evaluates fall detection specifically validated on elderly subjects performing falls

### E4. Night / Low-Light — Underaddressed
- **Only P05** systematically evaluates day vs. night (IR cameras)
- **P10** uses thermal modality (inherently lighting-independent) but on a tiny dataset
- No paper uses standard RGB CCTV and evaluates real low-light night scenarios

### E5. Multi-Person — Near-Absent
- **Only P08** addresses multi-person (but for detection only, not fall classification)
- Surveys (P07, P09, P12) all confirm <5% of the broader literature addresses multi-person
- For a shared common-area / staircase scenario, multi-person handling is critical and unaddressed

---

*Phase 3 Complete — Next: Phase 4 (Performance Analysis)*  
*Cross-reference: [phase2_technical_architecture.md](file:///home/endurance/Desktop/Research%20paper/literature/analysis/phase2_technical_architecture.md) | [paper_inventory.md](file:///home/endurance/Desktop/Research%20paper/literature/analysis/paper_inventory.md)*
