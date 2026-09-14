# Phase 2: Technical Architecture Extraction & Cross-Paper Analysis

> **Project**: Real-Time CCTV-Based Elderly Fall Detection in Staircase / Common-Area Environments  
> **Phase**: Phase 2 — Technical Methodology Extraction  
> **Status**: Completed  
> **Papers Analyzed**: 12 (PAPER_01 – PAPER_12)

---

## Extraction Schema

For every field:
- **Explicit** = directly stated in the paper text/table/figure with page/section reference
- **Inferred** = deduced from methodology description
- **Not reported** = no evidence in paper (NOT assumed to mean unsupported)

All 24 extraction fields from the Phase 2 workflow are populated for each paper.

---

## A. Individual Paper Records


### PAPER_01 — BiMP Dataset (Dibble & Bazzocchi, 2025, IEEE Access)

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | RGB (4 camera video) + 4-channel spatial percussive audio | Explicit | Abstract; §III.E |
| 2 | **Camera type** | Reolink RLK8-800B4 — 4x 3840x2160p IP cameras at 20 FPS | Explicit | §III.E, p.7-8 |
| 3 | **Camera placement/viewpoint** | Four cameras evenly around room; height 90-180 cm; aimed at central incident point | Explicit | §III.E, p.7-8 |
| 4 | **Person detection method** | Not reported (dataset paper; no real-time detection pipeline) | Not reported | — |
| 5 | **Person tracking method** | Not reported | Not reported | — |
| 6 | **Pose estimation method** | Not reported (keypoint-free; image-level CNN features used) | Not reported | — |
| 7 | **Feature extraction** | GoogLeNet (144-layer) spatial features; STFT and CWT spectrograms for audio | Explicit | §V.A, p.9-10 |
| 8 | **Motion features** | Frame-level visual patterns via GoogLeNet inception modules; temporal ordering of frames | Inferred | §V.A-B |
| 9 | **Spatial features** | GoogLeNet multi-scale inception features; audio wavelet and spectrogram maps | Explicit | §V.A, p.9-10 |
| 10 | **Temporal features** | GoogLeNet+LSTM: sequential frame feature arrays fed to bi-directional LSTM | Explicit | §V.B, p.10-11 |
| 11 | **Classification model** | GoogLeNet (standalone CNN) and GoogLeNet+LSTM | Explicit | §V.A-B, p.9-11 |
| 12 | **Temporal model** | Bi-directional LSTM appended after GoogLeNet global pooling layer | Explicit | §V.B, p.10-11 |
| 13 | **Fall-decision logic** | Binary classification: fall vs. non-fall; per-sequence softmax output | Explicit | §V.A, p.9 |
| 14 | **Confidence/threshold mechanism** | Not reported (class probability from softmax used directly) | Not reported | — |
| 15 | **False-positive reduction mechanism** | Not reported | Not reported | — |
| 16 | **Multiple-person handling** | Not reported; single-person-per-room experimental design | Not reported | §III.C |
| 17 | **Occlusion handling** | Not reported; acknowledged as limitation | Not reported | §VII, p.15 |
| 18 | **Lighting variation handling** | Not reported; controlled laboratory rooms only | Not reported | §III.C |
| 19 | **Camera-angle variation** | Tested across 4 fixed viewpoints (evenly spaced around room, 90-180 cm height) | Explicit | §III.E, p.7-8 |
| 20 | **Staircase handling** | Not reported; exclusively flat indoor rooms | Not reported | §III.C |
| 21 | **Real-time implementation** | Not reported; offline evaluation only | Not reported | — |
| 22 | **Hardware** | Reolink RLK8-800B4 NVR; training hardware unspecified | Partial | §III.E |
| 23 | **Software/frameworks** | MATLAB (data processing); MATLAB Deep Learning Toolbox (GoogLeNet) | Inferred | §V.A |
| 24 | **Computational requirements** | Not reported (no FPS or inference time benchmarks) | Not reported | — |

---

### PAPER_02 — Pose Estimation + Synthetic Data (Juraev et al., 2022, IEEE Access)

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | RGB video (CCTV, real-world surveillance) | Explicit | Abstract; §I |
| 2 | **Camera type** | AI Hub CCTV cameras at 3840x2160; KIST SynADL (synthetic Unity 3D) | Explicit | §IV.A.1 |
| 3 | **Camera placement/viewpoint** | AI Hub: varied real-world locations, multiple distances, steep angles, day/night | Explicit | §II.A.6 |
| 4 | **Person detection method** | YOLOv3 used as detector in top-down HPE (AlphaPose, DCPose) | Inferred | §III.A |
| 5 | **Person tracking method** | Not reported; no multi-frame identity tracking described | Not reported | — |
| 6 | **Pose estimation method** | 5 HPE benchmarked: AlphaPose (top-down), DCPose, OpenPose (bottom-up), OpenPifPaf, MoveNet. Best: AlphaPose | Explicit | §III.A, Table 3 |
| 7 | **Feature extraction** | 2D keypoints (X, Y, confidence C) per frame; 17 COCO or 18 OpenPose keypoints; normalized [0,1] | Explicit | §III.A, p.5 |
| 8 | **Motion features** | Temporal keypoint trajectories across frames; inter-frame displacement | Inferred | §III.A |
| 9 | **Spatial features** | Normalized 2D skeleton keypoints (X,Y,C) for joint positions | Explicit | §III.A, p.5 |
| 10 | **Temporal features** | TxK keypoint sequence to LSTM (3 layers: 32-64-32 units) or Transformer (4 encoder layers) | Explicit | §IV.A.2, Table 4 |
| 11 | **Classification model** | LSTM and Transformer; 4-class output (fall, stand-up, lying, walking) | Explicit | §IV.A.2 |
| 12 | **Temporal model** | LSTM (3 layers, hidden: 32,64,32) and Transformer (4 encoder layers, multi-head attention) | Explicit | §IV.A.2, Table 4 |
| 13 | **Fall-decision logic** | 4-class softmax; highest probability class wins | Inferred | §III.B |
| 14 | **Confidence/threshold mechanism** | Keypoint confidence score per HPE method; ACV and AMV metrics | Explicit | §III.C.1 |
| 15 | **False-positive reduction mechanism** | Not reported | Not reported | — |
| 16 | **Multiple-person handling** | Not reported; single-subject inference assumed | Not reported | — |
| 17 | **Occlusion handling** | Qualitatively tested (AI Hub); AlphaPose failed in indoor dim-light occlusion | Explicit | §IV.B.1 |
| 18 | **Lighting variation handling** | Qualitatively evaluated; most models fail under dim light | Explicit | §IV.B.1 |
| 19 | **Camera-angle variation** | Tested across multiple angles, heights, indoor/outdoor. AlphaPose most robust | Explicit | §IV.B.1 |
| 20 | **Staircase handling** | Not reported; stair-like locations in AI Hub not specifically evaluated | Not reported | §II.A.6 |
| 21 | **Real-time implementation** | FPS benchmarked: AlphaPose ~3 FPS, MoveNet ~30 FPS, OpenPose ~5 FPS (GTX 1080Ti) | Explicit | §III.A, Table 3 |
| 22 | **Hardware** | Intel i9-11900K + NVIDIA GTX 1080Ti, 16 GB RAM | Explicit | §IV.A.2 |
| 23 | **Software/frameworks** | Python, TensorFlow/Keras (implied), Optuna, Hyperband | Explicit | §IV.A.2 |
| 24 | **Computational requirements** | AlphaPose+Transformer: 89.22->94.35% accuracy; ~9ms inference per sample | Explicit | §IV.B.2c, Table 6 |

---

### PAPER_03 — AI-Based Edge Computing (Lin et al., 2022, IEEE Access)

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | RGB video (monocular camera) | Explicit | §III.A |
| 2 | **Camera type** | OmniVision OV2640 CMOS sensor | Explicit | §III.A |
| 3 | **Camera placement/viewpoint** | 5 different indoor scenes (living room, bedroom, etc.); various angles | Explicit | §III.C |
| 4 | **Person detection method** | Custom YOLO-LW (modified YOLOv3-tiny, deep separable convolutions, INT8 quantization) | Explicit | §III.B |
| 5 | **Person tracking method** | Not reported (ROI-based sequential analysis only) | Not reported | — |
| 6 | **Pose estimation method** | None; bounding box-based approach only | Explicit | §III.A-B |
| 7 | **Feature extraction** | YOLO-LW bounding box ROI; aspect ratio and position as posture features for SVM | Explicit | §III.B-C |
| 8 | **Motion features** | Bounding box position/shape change across frames; sliding window of posture states | Explicit | §IV.C |
| 9 | **Spatial features** | Human bounding box aspect ratio (height/width ratio: standing vs. fallen) | Inferred | §III.A-B |
| 10 | **Temporal features** | Sliding window: fall confirmed if "falling" state appears >3x in window | Explicit | §IV.C, p.8 |
| 11 | **Classification model** | SVM trained on posture features from bounding box | Explicit | §III.A-B |
| 12 | **Temporal model** | Sliding window majority-voting over SVM posture outputs | Explicit | §IV.C, Figure 11 |
| 13 | **Fall-decision logic** | SVM classifies posture per frame; sliding window vote triggers alarm when threshold exceeded | Explicit | §IV.C |
| 14 | **Confidence/threshold mechanism** | YOLO IoU threshold; SVM confidence; >3 fall states per sliding window | Explicit | §IV.C |
| 15 | **False-positive reduction mechanism** | Sliding window temporal filtering (>3 consecutive "fall" states required) | Explicit | §IV.C |
| 16 | **Multiple-person handling** | Not reported; single-person scenario assumed | Not reported | — |
| 17 | **Occlusion handling** | Acknowledged limitation; IoU decreases for self-occluded body / back-to-camera | Explicit | §V |
| 18 | **Lighting variation handling** | Acknowledged limitation; "variety of light may affect performance" | Explicit | §V |
| 19 | **Camera-angle variation** | Tested in 5 different indoor scenes with varied placement | Explicit | §III.C |
| 20 | **Staircase handling** | Not reported | Not reported | — |
| 21 | **Real-time implementation** | YES — 11.5 FPS on Sipeed MAix GO (Kendryte K210 RISC-V + KPU); <3.5W | Explicit | §IV.B Table 3 |
| 22 | **Hardware** | Sipeed MAix GO (K210 + KPU + ESP8285 Wi-Fi); Training: i7-10700F + RTX 3080 10G, 64GB | Explicit | §III.A |
| 23 | **Software/frameworks** | Darknet (training); TensorFlow (deploy); Kendryte KPU; Wi-Fi alert via ESP8285 | Explicit | §III.A-B |
| 24 | **Computational requirements** | 11.5 FPS (INT8 KPU); 94.5% IoU; SVM <0.001s; system accuracy 91.1%; power ~0.3W | Explicit | §IV.B-C, Tables 3-5 |

---

### PAPER_04 — Smart Tiles / Pressure Sensors (Daher et al., 2017, IEEE Sensors J.)

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | Underfloor pressure sensors + 3-axis accelerometers in tiles; RGB-D only for annotation | Explicit | Abstract; §III |
| 2 | **Camera type** | RGB-D camera (wall-mounted) for data annotation only — NOT in detection pipeline | Explicit | §IV.A |
| 3 | **Camera placement/viewpoint** | Wall-mounted camera for annotation only; tile sensors embedded in floor | Explicit | §IV.A |
| 4 | **Person detection method** | Pressure sensor threshold-based localization (high load = person on tile) | Explicit | §III.B |
| 5 | **Person tracking method** | Mass-center tracking via pressure sensor tile occupancy map (footstep trajectory) | Explicit | §VI (Fig.17) |
| 6 | **Pose estimation method** | None (non-vision-based system) | Not reported | — |
| 7 | **Feature extraction** | Accelerometer signal features: DWT variance, TR, Lyapunov Exponent, Sample Entropy, DFA, MPF, Deciles | Explicit | §IV.A.3 |
| 8 | **Motion features** | Accelerometer force signal changes; signal change detection for fall onset | Explicit | §IV.A.5 |
| 9 | **Spatial features** | Pressure tile occupancy map (which tiles loaded) and count of simultaneously loaded tiles | Explicit | §III.B |
| 10 | **Temporal features** | 1-second sliding windows (50 samples), 0.5-second overlap; signal change detection | Explicit | §IV.A.2 |
| 11 | **Classification model** | Rule-based threshold (pressure) + HCM-SFS feature selection + signal change detection (accel) | Explicit | §III-IV |
| 12 | **Temporal model** | Signal change detection on accelerometer windowed segments | Explicit | §IV.A.5 |
| 13 | **Fall-decision logic** | Stage 1: Force threshold (>3 linear tiles rapidly). Stage 2: Accelerometer confirms fall vs. lying | Explicit | §III.A-B |
| 14 | **Confidence/threshold mechanism** | threshold1=75% of max load; threshold2=25% (seated/fallen) | Explicit | §III.A |
| 15 | **False-positive reduction mechanism** | Sensor fusion: pressure false alarms (lying=fall) resolved by accelerometer | Explicit | §IV.C |
| 16 | **Multiple-person handling** | Not reported; single-person apartment scenario | Not reported | — |
| 17 | **Occlusion handling** | N/A — non-vision-based | Not reported | — |
| 18 | **Lighting variation handling** | Inherently unaffected (non-vision-based) | Not reported | — |
| 19 | **Camera-angle variation** | N/A — non-vision-based | Not reported | — |
| 20 | **Staircase handling** | Not reported; floor-tile system incompatible with stairs | Not reported | — |
| 21 | **Real-time implementation** | Tiles at ~50 Hz; 0.03s HCM latency | Explicit | §III.A; §IV.B.1 |
| 22 | **Hardware** | Smart tiles (embedded MCU + pressure + accelerometer + Wi-Fi/wired) | Explicit | §III.A |
| 23 | **Software/frameworks** | MATLAB (signal processing) | Explicit | §V.A |
| 24 | **Computational requirements** | HCM latency: 0.03s (i5-3317U @ 1.7GHz, 4GB RAM) | Explicit | §IV.B.1 |

---

### PAPER_05 — MUVIM Multi-Modal Dataset (Denkovski et al., 2022, IEEE Access)

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | IR, Depth, Thermal, RGB (4 types, 6 cameras); wearables collected but excluded from ML | Explicit | Abstract; §II.D |
| 2 | **Camera type** | Hikvision IP dome (IR, 20 FPS, 704x408); StereoLabs ZED (depth+RGB); FLIR Lepton (thermal); Kinect XBOX 360 | Explicit | §II.A, Table 3 |
| 3 | **Camera placement/viewpoint** | All cameras ceiling-mounted; overhead top-down view | Explicit | §II.A |
| 4 | **Person detection method** | Not reported; pre-cropped video used | Not reported | — |
| 5 | **Person tracking method** | Not reported | Not reported | — |
| 6 | **Pose estimation method** | None; anomaly detection on raw pixel-level video | Explicit | §I.B |
| 7 | **Feature extraction** | 3D convolutional autoencoder learns spatio-temporal features from raw video frames | Explicit | §III |
| 8 | **Motion features** | Spatio-temporal reconstruction error encodes motion anomalies | Inferred | §III |
| 9 | **Spatial features** | 3D CNN spatial feature maps from video frames | Inferred | §III |
| 10 | **Temporal features** | 3D convolution captures temporal dimension across consecutive frames | Inferred | §III |
| 11 | **Classification model** | 3D spatio-temporal convolutional autoencoder (trained on ADLs only); threshold on reconstruction error | Explicit | Abstract |
| 12 | **Temporal model** | 3D convolutional layers span temporal dimension; no explicit LSTM/RNN | Inferred | §III |
| 13 | **Fall-decision logic** | Falls produce high reconstruction error (model trained on non-fall only) | Explicit | Abstract |
| 14 | **Confidence/threshold mechanism** | AUC-ROC threshold on reconstruction error | Explicit | Abstract |
| 15 | **False-positive reduction mechanism** | Not reported explicitly; tunable via threshold | Not reported | — |
| 16 | **Multiple-person handling** | Not reported | Not reported | — |
| 17 | **Occlusion handling** | IR and depth cameras partially mitigate occlusion | Inferred | §I.B |
| 18 | **Lighting variation handling** | Explicitly tested: 5 day-time + 5 night-time trials; IR best in low-light (AUC=0.94) | Explicit | §II.A, Abstract |
| 19 | **Camera-angle variation** | Fixed ceiling-mounted top-down only; no angle variation tested | Explicit | §II.A |
| 20 | **Staircase handling** | Not reported | Not reported | — |
| 21 | **Real-time implementation** | Not reported | Not reported | — |
| 22 | **Hardware** | Hikvision IP, StereoLabs ZED, FLIR Lepton, Kinect; compute hardware not specified | Explicit | §II.A |
| 23 | **Software/frameworks** | Not reported (GitHub: https://github.com/MUVIM/FallDetection) | Not reported | — |
| 24 | **Computational requirements** | Not reported | Not reported | — |

---

### PAPER_06 — HOG + VGG-16 Surveillance (Jain & Sitara, 2022, IEEE INCET)

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | RGB video (surveillance cameras) | Explicit | Abstract |
| 2 | **Camera type** | IP cameras (8x, 480x480) — Multiple Cameras Dataset; single cam (URFD) | Explicit | §IV.C |
| 3 | **Camera placement/viewpoint** | Multiple angles in same room (front, back, sideways fall directions) | Explicit | §IV.C |
| 4 | **Person detection method** | Not reported; pre-segmented video clips from datasets | Not reported | — |
| 5 | **Person tracking method** | Not reported | Not reported | — |
| 6 | **Pose estimation method** | None; appearance-based HOG features | Explicit | §III |
| 7 | **Feature extraction** | HOG (Histogram of Oriented Gradients) from grayscale frames; VGG-16 deep features | Explicit | §III.b-c |
| 8 | **Motion features** | HOG gradient orientation change across consecutive frames (motion direction shifts) | Explicit | §III.a |
| 9 | **Spatial features** | HOG per frame (edge/gradient direction histograms); VGG-16 multi-scale features | Explicit | §III.b-c |
| 10 | **Temporal features** | Sliding window of 20 frames (stack size=20, step=1) | Explicit | §III.a |
| 11 | **Classification model** | VGG-16 CNN feature extractor + dense layers; binary fall/non-fall | Explicit | §III.c |
| 12 | **Temporal model** | Stacking 20 consecutive frames; no explicit LSTM/RNN | Explicit | §III.a |
| 13 | **Fall-decision logic** | CNN classifier output on 20-frame stack | Inferred | §III |
| 14 | **Confidence/threshold mechanism** | Not reported | Not reported | — |
| 15 | **False-positive reduction mechanism** | Not reported | Not reported | — |
| 16 | **Multiple-person handling** | Not reported | Not reported | — |
| 17 | **Occlusion handling** | Not reported | Not reported | — |
| 18 | **Lighting variation handling** | HOG normalization provides robustness to brightness variation (stated advantage) | Explicit | §V |
| 19 | **Camera-angle variation** | Multiple camera angles tested (fall direction: front, back, sideways) | Explicit | §IV.C |
| 20 | **Staircase handling** | Not reported | Not reported | — |
| 21 | **Real-time implementation** | Not reported; Google Colab GPU only (not real-time deployment) | Not reported | §IV.C |
| 22 | **Hardware** | Google Colab: Intel Xeon 2.3GHz, 13GB RAM, Nvidia K80 12GB | Explicit | §IV.C, Table II |
| 23 | **Software/frameworks** | Python 3.7, OpenCV, Google Colab | Explicit | §IV.C |
| 24 | **Computational requirements** | Not reported (no FPS or latency benchmarks) | Not reported | — |

---

### PAPER_07 — AI Fall Detection Survey (Nahian et al., 2026, Springer Cogn. Comp.)

*Systematic review paper. Extraction covers survey's analytical findings about the literature.*

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | Survey covers: RGB, depth, thermal, IR, wearable IMU, pressure, radar | Explicit | §2-5 |
| 2 | **Camera type** | RGB CCTV, depth cameras (Kinect), thermal, IR surveyed | Explicit | §3 |
| 3 | **Camera placement/viewpoint** | Ceiling-mount, wall-mount, eye-level all found in literature | Inferred | §3 |
| 4 | **Person detection method** | Survey: YOLO variants, Faster R-CNN, SSD are common | Explicit | §3 |
| 5 | **Person tracking method** | Survey: SORT, DeepSORT, Kalman filter, re-ID methods mentioned | Explicit | §3 |
| 6 | **Pose estimation method** | Survey: OpenPose, AlphaPose, MediaPipe, HRNet, PoseNet mentioned | Explicit | §3 |
| 7 | **Feature extraction** | Survey: CNN (ResNet, VGG, MobileNet), skeleton keypoints, HOG, optical flow | Explicit | §3-4 |
| 8 | **Motion features** | Survey: optical flow, inter-frame differences, velocity vectors, joint angle change | Explicit | §3 |
| 9 | **Spatial features** | Survey: bounding box aspect ratio, body keypoints, silhouette | Explicit | §3 |
| 10 | **Temporal features** | Survey: LSTM, GRU, BiLSTM, Transformer, sliding window, 3D CNN | Explicit | §4 |
| 11 | **Classification model** | Survey: CNN, LSTM, GRU, Transformer, SVM, Random Forest, Hybrid | Explicit | §4 |
| 12 | **Temporal model** | Survey: LSTM and GRU dominate fall classification | Explicit | §4 |
| 13 | **Fall-decision logic** | Survey: binary (fall/non-fall) or multi-class (fall + ADL types) | Explicit | §4 |
| 14 | **Confidence/threshold mechanism** | Survey: threshold-based and DL probability-based; wide variation | Explicit | §4 |
| 15 | **False-positive reduction mechanism** | Survey: MAJOR GAP — false alarms from sitting/lying/bending are common; 95% papers inadequate | Explicit | §5 |
| 16 | **Multiple-person handling** | Survey: rarely addressed; <5% of papers evaluate multi-person | Explicit | §5 |
| 17 | **Occlusion handling** | Survey: major open challenge; partial occlusion inadequately handled | Explicit | §5 |
| 18 | **Lighting variation handling** | Survey: night/low-light rarely addressed; thermal/IR proposed but not validated at scale | Explicit | §5 |
| 19 | **Camera-angle variation** | Survey: rarely systematically evaluated | Explicit | §5 |
| 20 | **Staircase handling** | Survey: not mentioned as researched topic — absence noted | Inferred | §5 |
| 21 | **Real-time implementation** | Survey: critical gap — real-time edge deployment rarely validated | Explicit | §5 |
| 22 | **Hardware** | Survey: GPU servers used almost universally; very few edge deployments | Explicit | §5 |
| 23 | **Software/frameworks** | Survey: TensorFlow, PyTorch, Keras dominant | Explicit | §3 |
| 24 | **Computational requirements** | Survey: 95% of papers lack elderly subjects; real-world generalization unproven | Explicit | §5 |

---

### PAPER_08 — EfficientDet Person Tracking (Sivachandiran et al., 2022, Elsevier Meas. Sens.)

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | RGB video (surveillance cameras) | Explicit | Abstract |
| 2 | **Camera type** | Not specified (PascalVOC and PenFudan datasets) | Not reported | — |
| 3 | **Camera placement/viewpoint** | Not reported; varied in benchmark datasets | Not reported | — |
| 4 | **Person detection method** | EfficientDet (EfficientNet backbone + BiFPN + compound scaling); PascalVOC/PenFudan trained | Explicit | §2.1 |
| 5 | **Person tracking method** | EfficientDet frame-by-frame detection with bounding box continuity | Inferred | §2.1 |
| 6 | **Pose estimation method** | Not reported (detection-only; no skeleton) | Not reported | — |
| 7 | **Feature extraction** | BiFPN bi-directional feature pyramid (multi-scale); EfficientNet backbone features | Explicit | §2.1 |
| 8 | **Motion features** | Not reported (detection system only) | Not reported | — |
| 9 | **Spatial features** | Multi-scale BiFPN feature maps; bounding box coordinates | Explicit | §2.1 |
| 10 | **Temporal features** | Not reported (single-frame detection; no temporal modeling) | Not reported | — |
| 11 | **Classification model** | EfficientDet object detector (person class) | Explicit | §2.1 |
| 12 | **Temporal model** | None (frame-by-frame detection) | Not reported | — |
| 13 | **Fall-decision logic** | Not applicable (person detection/tracking only; no fall classification) | Not reported | — |
| 14 | **Confidence/threshold mechanism** | RMSProp hyperparameter optimizer | Explicit | §2.2 |
| 15 | **False-positive reduction mechanism** | RMSProp reduces FP; FPPI=0.047 (PascalVOC) | Explicit | §3, Table 1 |
| 16 | **Multiple-person handling** | YES — EfficientDet detects and tracks multiple persons per frame | Explicit | Abstract |
| 17 | **Occlusion handling** | Not reported | Not reported | — |
| 18 | **Lighting variation handling** | Not reported | Not reported | — |
| 19 | **Camera-angle variation** | Not reported | Not reported | — |
| 20 | **Staircase handling** | Not reported | Not reported | — |
| 21 | **Real-time implementation** | Not reported (no FPS metric for system) | Not reported | — |
| 22 | **Hardware** | Not reported | Not reported | — |
| 23 | **Software/frameworks** | Not reported | Not reported | — |
| 24 | **Computational requirements** | PascalVOC: Prec 92.95%, Rec 61.86%, AP 69.94%; PenFudan: Prec 86.46%, Rec 90.54%, AP 88.76% | Explicit | §3, Tables 1-2 |

---

### PAPER_09 — DL CV Systematic Review (Gaya-Morey et al., 2024, Springer Appl. Intel.)

*Review of 87 DL-based computer-vision fall detection papers.*

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | Survey: RGB (dominant), depth, skeleton, optical flow | Explicit | §2-4 |
| 2 | **Camera type** | Survey: RGB CCTV, Kinect (depth+RGB), thermal | Explicit | §3 |
| 3 | **Camera placement/viewpoint** | Survey: wall-mount and ceiling-mount common; angle variation underexplored | Explicit | §5 |
| 4 | **Person detection method** | Survey: YOLO (most common), Faster R-CNN, SSD | Explicit | §3 |
| 5 | **Person tracking method** | Survey: Skeleton tracking breakdown under occlusion documented; IoU tracking, SORT | Explicit | §5 |
| 6 | **Pose estimation method** | Survey: OpenPose, AlphaPose, MediaPipe dominant; degrades under occlusion and steep angles | Explicit | §3, §5 |
| 7 | **Feature extraction** | Survey: CNN spatial, skeleton keypoints, optical flow, silhouette | Explicit | §3 |
| 8 | **Motion features** | Survey: optical flow, bounding box velocity, keypoint velocity | Explicit | §3 |
| 9 | **Spatial features** | Survey: keypoint coordinates, body aspect ratio, silhouette orientation | Explicit | §3 |
| 10 | **Temporal features** | Survey: LSTM (most common), GRU, Transformer, 3D CNN | Explicit | §3-4 |
| 11 | **Classification model** | Survey: CNN-LSTM hybrid most common in 87 papers | Explicit | §4 |
| 12 | **Temporal model** | Survey: LSTM/BiLSTM dominant temporal model | Explicit | §4 |
| 13 | **Fall-decision logic** | Survey: binary classification; some multi-class | Explicit | §3 |
| 14 | **Confidence/threshold mechanism** | Survey: threshold on probability or anomaly score | Explicit | §3 |
| 15 | **False-positive reduction mechanism** | Survey: persistent problem; sitting/lying/bending confusable with falls | Explicit | §5 |
| 16 | **Multiple-person handling** | Survey: <5% of papers; confirmed underexplored gap | Explicit | §5 |
| 17 | **Occlusion handling** | Survey: skeleton tracking breaks down under partial occlusion — confirmed gap | Explicit | §5 |
| 18 | **Lighting variation handling** | Survey: night/low-light rarely tested; depth cameras partially address | Explicit | §5 |
| 19 | **Camera-angle variation** | Survey: steep angles rarely validated; staircase perspectives absent | Explicit | §5 |
| 20 | **Staircase handling** | Survey: STAIRCASE ENVIRONMENTS ABSENT from all 87 analyzed papers — explicit gap | Explicit | §5 |
| 21 | **Real-time implementation** | Survey: <15% deploy/evaluate real-time on hardware | Explicit | §5 |
| 22 | **Hardware** | Survey: GPU server prevalent; edge deployment uncommon | Explicit | §5 |
| 23 | **Software/frameworks** | Survey: TensorFlow, PyTorch | Explicit | §3 |
| 24 | **Computational requirements** | Survey: real-time performance rarely reported | Explicit | §5 |

---

### PAPER_10 — Dilated Spatio-Temporal AE (Li et al., 2023, Elsevier ICT Express)

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | Depth video (UR dataset primary); Thermal video (Thermal dataset) | Explicit | §3.1 |
| 2 | **Camera type** | Microsoft Kinect (depth, 640x480, 30 FPS); Android phone thermal (640x480, 15-25 FPS) | Explicit | §3.1 |
| 3 | **Camera placement/viewpoint** | Kinect: lab placement; thermal: not specified | Explicit | §3.1 |
| 4 | **Person detection method** | Not reported; pre-processed video from datasets | Not reported | — |
| 5 | **Person tracking method** | Not reported | Not reported | — |
| 6 | **Pose estimation method** | None; appearance-based autoencoder on depth/thermal frames | Explicit | §2 |
| 7 | **Feature extraction** | Dilated convolutional encoder (DCLSTMAE): dilated convolution + pooling; depth hole-filling preprocessing | Explicit | §2 |
| 8 | **Motion features** | DCLSTM: temporal motion via 3-gate LSTM over dilated features | Explicit | §2 |
| 9 | **Spatial features** | Dilated features (rate=2 optimal); expanded receptive field with fewer parameters | Explicit | §2, §3.2, Table 1 |
| 10 | **Temporal features** | DCLSTM input/forget/output gates over T consecutive depth frames | Explicit | §2 |
| 11 | **Classification model** | Unsupervised DCLSTMAE: trained on ADLs; fall = high reconstruction error | Explicit | §1-2 |
| 12 | **Temporal model** | DCLSTM — dilated convolutional LSTM integrating spatial and temporal features | Explicit | §2 |
| 13 | **Fall-decision logic** | Fall score = normalized reconstruction error; lower score = fall; threshold on score | Explicit | §2 (eq.10) |
| 14 | **Confidence/threshold mechanism** | Normalized reconstruction error [0,1]; tunable threshold on ROC | Explicit | §2, §3.3 |
| 15 | **False-positive reduction mechanism** | Training on ADLs only; novel fall score formulation | Explicit | §2 |
| 16 | **Multiple-person handling** | Not reported; single-person UR/Thermal datasets | Not reported | — |
| 17 | **Occlusion handling** | Depth hole-filling addresses missing pixels; not full occlusion handling | Partial | §2 |
| 18 | **Lighting variation handling** | Thermal modality inherently lighting-independent; validated on Thermal dataset | Explicit | §3.1 |
| 19 | **Camera-angle variation** | Not reported | Not reported | — |
| 20 | **Staircase handling** | Not reported | Not reported | — |
| 21 | **Real-time implementation** | Not reported; training: 128s/epoch on GTX 2080Ti | Explicit | §3, Table 3 |
| 22 | **Hardware** | NVIDIA GTX 2080Ti, 11 GB RAM | Explicit | §3 |
| 23 | **Software/frameworks** | Python, Keras (TensorFlow backend) | Explicit | §3 |
| 24 | **Computational requirements** | Model size: 12.3 MB; 97.1% accuracy, 93.9% sensitivity, 95.1% precision (processed UR depth) | Explicit | §3, Tables 3-5 |

---

### PAPER_11 — MobileNetV2+GRU Trustworthy (Moussa et al., 2026, Elsevier ISWA)

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | RGB video (CCTV stream) | Explicit | Abstract, §1 |
| 2 | **Camera type** | Existing CCTV infrastructure (Le2i and CAUCAFall datasets); specific camera model not reported | Explicit | §4 |
| 3 | **Camera placement/viewpoint** | Le2i: multiple indoor rooms (office, home, coffee room), multi-camera views; CAUCAFall: unconstrained indoor | Explicit | §4 |
| 4 | **Person detection method** | Not explicitly reported; frames fed directly to MobileNetV2 from video | Not reported | — |
| 5 | **Person tracking method** | Not reported | Not reported | — |
| 6 | **Pose estimation method** | None; RGB frame-level appearance features via MobileNetV2 | Explicit | Abstract, §3.1 |
| 7 | **Feature extraction** | MobileNetV2 (depthwise separable convolutions, inverted residuals): spatial features from 224x224 RGB frames | Explicit | §3.1 |
| 8 | **Motion features** | GRU processes MobileNetV2 feature sequence; abrupt changes (rapid descent/collapse) produce large gate updates | Explicit | §3.2 |
| 9 | **Spatial features** | MobileNetV2 convolutional feature maps (body appearance) | Explicit | §3.1 |
| 10 | **Temporal features** | GRU sliding window (20-frame window, 5 uniformly sampled frames); update gate + reset gate + hidden state | Explicit | §3.2 |
| 11 | **Classification model** | MobileNetV2 + GRU; binary fall/non-fall; two-consecutive-window confirmation | Explicit | §3.2 |
| 12 | **Temporal model** | GRU with BPTT; sliding non-overlapping windows | Explicit | §3.2 |
| 13 | **Fall-decision logic** | Fall confirmed only if two consecutive windows both predict fall | Explicit | §3.2 (formula) |
| 14 | **Confidence/threshold mechanism** | Two-consecutive-window confirmation rule; binary sigmoid output | Explicit | §3.2 |
| 15 | **False-positive reduction mechanism** | Two-consecutive-window confirmation; federated fairness via Fairlearn | Explicit | §3.2, §3.5 |
| 16 | **Multiple-person handling** | Not reported | Not reported | — |
| 17 | **Occlusion handling** | Not reported | Not reported | — |
| 18 | **Lighting variation handling** | Tested on Le2i multi-room (natural lighting variation); low-light not explicitly tested | Partial | §4 |
| 19 | **Camera-angle variation** | Multi-camera, multi-room Le2i provides varied viewpoints | Partial | §4 |
| 20 | **Staircase handling** | Not reported | Not reported | — |
| 21 | **Real-time implementation** | ~93 FPS on experimental GPU platform | Explicit | Abstract |
| 22 | **Hardware** | GPU platform (specific model not detailed) | Partial | Abstract |
| 23 | **Software/frameworks** | TensorFlow/Keras (implied); Fairlearn; Grad-CAM++ | Inferred | §3.4-3.5 |
| 24 | **Computational requirements** | 97.14% accuracy, 99.26% precision, 96.75% recall, 97.99% F1 (CAUCAFall+Le2i); 93 FPS | Explicit | Abstract, §4 |

---

### PAPER_12 — Real-Time Vision Review (Nabizade et al., 2026, MDPI Sensors)

*PRISMA review: only 11 of 588 papers met all inclusion criteria (hardware FPS >= 10).*

| # | Field | Value | Status | Reference |
|---|---|---|---|---|
| 1 | **Input modality** | Survey: RGB dominant; 11 qualifying papers all RGB or depth | Explicit | §Results |
| 2 | **Camera type** | Survey: RGB and depth cameras; edge devices dominate deployment | Explicit | §Results |
| 3 | **Camera placement/viewpoint** | Survey: placement variation underexplored in qualifying papers | Explicit | §Discussion |
| 4 | **Person detection method** | Survey: CNN-based detection dominant | Explicit | §Results |
| 5 | **Person tracking method** | Survey: not systematically reported | Not reported | — |
| 6 | **Pose estimation method** | Survey: skeleton-based in minority among qualifying papers | Explicit | §Results |
| 7 | **Feature extraction** | Survey: CNN features dominate; bounding box and skeleton also used | Explicit | §Results |
| 8 | **Motion features** | Survey: temporal CNN models dominant in qualifying papers | Explicit | §Results |
| 9 | **Spatial features** | Survey: CNN spatial; bounding box ratios | Explicit | §Results |
| 10 | **Temporal features** | Survey: 3D CNN and LSTM most common | Explicit | §Results |
| 11 | **Classification model** | Survey: CNN architectures dominate; 11/11 qualifying papers use CNN | Explicit | §Results |
| 12 | **Temporal model** | Survey: LSTM and 3D CNN; real-time favors lightweight | Explicit | §Results |
| 13 | **Fall-decision logic** | Survey: binary fall/non-fall | Explicit | §Results |
| 14 | **Confidence/threshold mechanism** | Survey: varies; not standardized | Not reported | — |
| 15 | **False-positive reduction mechanism** | Survey: not systematically reported in qualifying papers | Not reported | — |
| 16 | **Multiple-person handling** | Survey: not addressed in ANY qualifying paper | Explicit | §Discussion |
| 17 | **Occlusion handling** | Survey: not addressed in qualifying papers | Explicit | §Discussion |
| 18 | **Lighting variation handling** | Survey: not systematically tested | Explicit | §Discussion |
| 19 | **Camera-angle variation** | Survey: not systematically evaluated | Explicit | §Discussion |
| 20 | **Staircase handling** | Survey: NOT PRESENT in any qualifying paper | Explicit | §Discussion |
| 21 | **Real-time implementation** | KEY FINDING: Only 11/588 papers (1.9%) report hardware FPS >= 10 | Explicit | Abstract, §Results |
| 22 | **Hardware** | Survey: edge devices (Jetson, Raspberry Pi, custom NPU) dominate qualifying papers | Explicit | §Results |
| 23 | **Software/frameworks** | Survey: TensorFlow Lite and PyTorch for edge deployment | Explicit | §Results |
| 24 | **Computational requirements** | Quantization/pruning critical for real-time; persistent limitations: no elderly subjects, small controlled datasets | Explicit | Abstract, §Discussion |



---

## B. Cross-Paper Comparison Matrix

**Legend**: YES = Explicitly present | PARTIAL = Partial/Inferred | NO = Not reported/Not applicable | SURVEY = Survey finding

| Feature | P01 BiMP | P02 Pose+Synth | P03 Edge YOLO | P04 Tiles | P05 MUVIM | P06 HOG+VGG | P07 Survey | P08 EfficientDet | P09 DL Review | P10 Dilated AE | P11 MobNet+GRU | P12 RT Review |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Modality** | RGB+Audio | RGB CCTV | RGB Edge | Pressure+Accel | IR/Depth/Thermal/RGB | RGB | Multi | RGB Surv. | RGB | Depth+Thermal | RGB CCTV | RGB/Depth |
| **Person Detection** | NO | PARTIAL | YES YOLO-LW | PARTIAL | NO | NO | SURVEY | YES EfficientDet | SURVEY | NO | NO | SURVEY |
| **Person Tracking** | NO | NO | NO | YES Pressure-map | NO | NO | SURVEY | YES | SURVEY | NO | NO | NO |
| **Pose Estimation** | NO | YES AlphaPose | NO | NO | NO | NO | SURVEY | NO | SURVEY | NO | NO | NO |
| **CNN Feature Extractor** | YES GoogLeNet | NO | YES YOLO-LW | NO | YES 3D-Conv AE | YES VGG-16 | SURVEY | YES EfficientNet | SURVEY | YES Dilated CNN | YES MobileNetV2 | SURVEY |
| **Temporal Model** | YES LSTM | YES LSTM/Transformer | YES Sliding Win. | YES Win+SCD | PARTIAL 3D-Conv | YES Frame Stack | SURVEY | NO | SURVEY | YES DCLSTM | YES GRU | SURVEY |
| **Anomaly Detection** | NO | NO | NO | NO | YES | NO | NO | NO | NO | YES | NO | NO |
| **Sliding Window FP Filter** | NO | NO | YES | YES | NO | YES | NO | NO | NO | NO | YES | NO |
| **False-Positive Reduction** | NO | NO | YES | YES | NO | NO | SURVEY (gap) | PARTIAL | SURVEY (gap) | PARTIAL | YES | NO |
| **Multi-Person** | NO | NO | NO | NO | NO | NO | SURVEY <5% | YES | SURVEY <5% | NO | NO | SURVEY absent |
| **Occlusion Handling** | NO | PARTIAL qual. | PARTIAL ack. | N/A | PARTIAL IR/Depth | NO | SURVEY gap | NO | SURVEY gap | PARTIAL hole-fill | NO | SURVEY absent |
| **Low-Light/Night** | NO | PARTIAL dim-light | PARTIAL ack. | YES unaffected | YES IR/Thermal | PARTIAL HOG | SURVEY gap | NO | SURVEY gap | YES Thermal | NO | SURVEY absent |
| **Camera-Angle Variation** | YES 4 views | YES multi-angle | YES 5 scenes | N/A | PARTIAL ceiling | YES multi-angle | SURVEY rare | NO | SURVEY rare | NO | PARTIAL multi-room | NO |
| **STAIRCASE** | NO | NO | NO | NO | NO | NO | NO | NO | NO (explicit gap) | NO | NO | NO |
| **Real-Time FPS** | NO | PARTIAL HPE-only | YES 11.5 FPS | YES 50Hz | NO | NO | SURVEY gap | NO | SURVEY <15% | NO | YES ~93 FPS | SURVEY 1.9% |
| **Edge Hardware** | NO | NO | YES Sipeed K210 | YES MCU tiles | NO | NO | SURVEY rare | NO | SURVEY rare | NO | NO | SURVEY dominant |
| **Privacy Preservation** | PARTIAL Audio | PARTIAL Skeleton | YES Local | YES Floor | YES IR/Depth | NO | SURVEY | NO | SURVEY | YES Depth/Thermal | YES Federated | NO |
| **Remote Alert** | NO | NO | YES Wi-Fi | NO | NO | NO | NO | NO | NO | NO | NO | NO |
| **XAI/Explainability** | NO | NO | NO | NO | NO | NO | NO | NO | NO | NO | YES Grad-CAM++ | NO |
| **Federated Learning** | NO | NO | NO | NO | NO | NO | NO | NO | NO | NO | YES FedAvg | NO |
| **Alert Acknowledgement** | NO | NO | NO | NO | NO | NO | NO | NO | NO | NO | NO | NO |
| **Alert Escalation** | NO | NO | NO | NO | NO | NO | NO | NO | NO | NO | NO | NO |
| **Elderly Subjects** | NO | PARTIAL 60+ | NO | PARTIAL 6 subj. | PARTIAL 10 older | NO | SURVEY 95% absent | NO | SURVEY absent | NO | NO | SURVEY absent |
| **Simulated Falls** | YES | YES | YES | YES | YES | YES | SURVEY | SURVEY | SURVEY | YES | YES | SURVEY |
| **Real/Actual Falls** | NO | NO | NO | NO | NO | NO | NO | NO | NO | NO | NO | NO |

---

## C. Frequency Counts — Technical Approach Prevalence

### C1. Person Detection Methods

| Method | N Papers | Paper IDs |
|---|:---:|---|
| YOLO family (YOLOv3-tiny / YOLO-LW) | 2 | P03 (explicit), P02 (via top-down HPE) |
| EfficientDet (BiFPN backbone) | 1 | P08 |
| Pressure sensor threshold | 1 | P04 |
| Not reported / Not applicable | 8 | P01, P05, P06, P07(S), P09(S), P10, P11, P12(S) |

### C2. Pose Estimation Methods

| Method | N Papers | Paper IDs |
|---|:---:|---|
| AlphaPose (top-down, YOLO detector) | 1 | P02 (benchmark + selected) |
| OpenPose (bottom-up) | 1 | P02 (benchmark only) |
| DCPose | 1 | P02 (benchmark only) |
| OpenPifPaf | 1 | P02 (benchmark only) |
| MoveNet | 1 | P02 (benchmark only) |
| None (bounding box or pixel-level) | 8 | P01, P03, P04, P05, P06, P08, P10, P11 |
| Survey mentions various | 3 | P07, P09, P12 |

### C3. Temporal Models

| Model | N Papers | Paper IDs |
|---|:---:|---|
| LSTM (standalone or combined) | 3 | P01 (BiLSTM), P02, P10 (DCLSTM) |
| GRU | 1 | P11 |
| Transformer (multi-head attention) | 1 | P02 |
| Sliding window majority vote | 2 | P03 (>3 fall states), P11 (2 consecutive windows) |
| 3D Convolutional AE (temporal) | 1 | P05 |
| Frame stacking (20 frames) | 1 | P06 |
| Signal change detection | 1 | P04 |
| None (detection-only, no temporal) | 1 | P08 |

### C4. Classification Models

| Model | N Papers | Paper IDs |
|---|:---:|---|
| CNN (GoogLeNet / VGG-16 / MobileNetV2 / EfficientNet) | 5 | P01 (GoogLeNet), P06 (VGG-16), P08 (EfficientDet), P11 (MobileNetV2), P03 (YOLO-LW+SVM) |
| Autoencoder anomaly detection | 2 | P05 (3D-Conv AE), P10 (DCLSTMAE) |
| SVM | 1 | P03 |
| Rule-based threshold | 1 | P04 |
| LSTM/GRU classifier | 3 | P02 (LSTM), P01 (+LSTM), P11 (GRU) |
| Transformer | 1 | P02 |

### C5. Input Modalities

| Modality | N Papers | Paper IDs |
|---|:---:|---|
| RGB only | 4 | P02, P03, P06, P11 |
| RGB + Audio | 1 | P01 |
| Depth | 2 | P10 (primary), P05 (one of four) |
| Thermal | 2 | P10 (secondary), P05 (one of four) |
| IR (infrared) | 1 | P05 (one of four) |
| Multi-modal (thermal+IR+depth+RGB) | 1 | P05 |
| Pressure + Accelerometer (floor) | 1 | P04 |
| RGB (survey meta-finding) | 3 | P07, P09, P12 |

### C6. False-Positive Reduction Mechanisms

| Mechanism | N Papers | Paper IDs |
|---|:---:|---|
| Sliding window / consecutive confirmation | 3 | P03 (>3 of window), P11 (2 consec windows), P06 (partial) |
| Sensor fusion (multimodal) | 1 | P04 (pressure + accelerometer) |
| Anomaly score threshold tuning | 2 | P05, P10 |
| None reported / gap identified | 8 | P01, P02, P06, P07(S), P08, P09(S), P12(S) |

### C7. Real-Time / Hardware Deployment

| Implementation | N Papers | Paper IDs |
|---|:---:|---|
| Edge hardware + FPS reported | 1 | P03 (11.5 FPS on Sipeed MAix GO K210) |
| GPU + FPS reported | 1 | P11 (~93 FPS) |
| Real-time sensor (non-vision) | 1 | P04 (50 Hz pressure tiles) |
| HPE FPS only (not system-level) | 1 | P02 (3-30 FPS depending on model) |
| No real-time benchmark reported | 8 | P01, P05, P06, P08, P09, P10 |
| Survey: 1.9% of 588 papers report hardware FPS | — | P12 |

### C8. Staircase Handling (CRITICAL FINDING)

| Status | N Papers | Paper IDs |
|---|:---:|---|
| Explicitly evaluated in experiments | 0 | NONE |
| Explicitly identified as research gap | 2 | P09, P12 |
| Not reported (environment absent) | 10 | P01, P02, P03, P04, P05, P06, P07, P08, P10, P11 |

### C9. Multiple-Person Handling

| Status | N Papers | Paper IDs |
|---|:---:|---|
| Explicitly implemented (detection level) | 1 | P08 (EfficientDet) |
| Not reported / not addressed | 11 | P01-P07, P09-P12 |
| Survey gap confirmed (<5% of papers) | 2 | P07, P09 |
| Survey: absent from all qualifying papers | 1 | P12 |

### C10. Emergency Response Features

| Feature | N Papers | Paper IDs |
|---|:---:|---|
| Local alarm / buzzer | 0 | NONE |
| Remote alert (any) | 1 | P03 (Wi-Fi alert to server) |
| Alert with location metadata | 0 | NONE |
| Visual evidence (clip/frame) transmission | 0 | NONE |
| Grad-CAM++ heatmap (explainability, not alert) | 1 | P11 |
| Human acknowledgement | 0 | NONE |
| Alert timeout | 0 | NONE |
| Alert escalation | 0 | NONE |
| End-to-end emergency response pipeline | 0 | NONE |

---

## D. Key Analytical Findings

### D1. Dominant Architecture Pattern
The most common fall-detection pipeline across the 12 papers:
**RGB Input -> CNN Feature Extractor -> LSTM/GRU Temporal Model -> Binary Classifier**
Present in approximately 5/9 empirical papers (P01, P02, P10, P11, P06 variants). Confirmed by survey papers P07, P09, P12 as the dominant literature approach.

### D2. Detection vs. Tracking Gap
Only **P08** implements dedicated multi-person detection and tracking. All other vision-based papers assume single-person scenes or do not address identity tracking. This is a critical gap for real-world CCTV scenarios where multiple people co-exist in shared spaces.

### D3. Pose Estimation Concentration
Skeleton-based pose estimation is **evaluated in only 1 paper (P02)**. PAPER_02 shows AlphaPose is most robust but achieves only ~3 FPS on high-end GPU hardware. The majority of papers bypass pose estimation in favor of appearance-based CNN features or bounding box ratios. This suggests that pose-based approaches are computationally expensive for real-time use.

### D4. Sliding Window Confirmation Pattern
Three papers independently converge on sliding-window temporal confirmation as an effective FP-reduction strategy:
- P03: majority vote (>3 of window)
- P11: two-consecutive-window rule
- P06: frame stack of 20 (partial temporal fusion)
This practical mechanism is **underutilized** across the broader literature and warrants adoption in our target system.

### D5. Edge vs. Server Deployment Gap
Only PAPER_03 demonstrates true edge deployment (K210 @ 11.5 FPS, 0.3W). PAPER_11 reports 93 FPS but on unspecified GPU hardware. PAPER_12 confirms this: only 1.9% of 588 papers validate real-time on physical hardware. This is a significant literature gap for practical deployment.

### D6. Complete Absence: Staircase Environments
**0/12 papers** experimentally evaluate any component of the fall detection pipeline in a staircase or multi-level environment. Both survey papers (P09: 87 papers reviewed, P12: 588 papers reviewed) explicitly identify this as an unaddressed gap. This is the most consistently confirmed void in the literature.

### D7. Emergency Response Pipeline Gap
End-to-end emergency response is almost entirely absent:
- Only P03 sends a real remote alert (Wi-Fi)
- Only P11 generates visual evidence (Grad-CAM++ heatmap -- not for alert)
- **0 papers** implement: local alarm + remote alert + location metadata + acknowledgement + escalation
This complete multi-tier emergency response pipeline required by our target system represents a major unaddressed engineering-research gap.

### D8. Elderly Subject Evaluation
- P05 includes 10 older adults aged 70+ for ADL data (no falls simulated for them)
- P02 includes some subjects aged 60+ in AI Hub (minor coverage)
- All other empirical papers (P01, P03, P04, P06, P10, P11): young subjects only
- Survey P07 confirms: 95% of literature lacks elderly subjects
This means performance metrics across literature are NOT validated on the target demographic (elderly).

---

*Phase 2 Complete — Next: Phase 3 (Dataset and Experimental Realism Analysis)*  
*Cross-reference: [paper_inventory.md](file:///home/endurance/Desktop/Research paper/literature/analysis/paper_inventory.md) | [phase2_technical_architecture.md](file:///home/endurance/Desktop/Research paper/literature/analysis/phase2_technical_architecture.md)*
