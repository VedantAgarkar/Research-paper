# PAPER_08: Deep Learning driven automated person detection and tracking model on surveillance videos

## Metadata
- **Authors**: S. Sivachandiran, K. Jagan Mohan, G. Mohammed Nazer
- **Publication Year**: 2022
- **Venue**: Measurement: Sensors (Elsevier, vol. 24, 100422, pp. 1–7)
- **DOI**: [10.1016/j.measen.2022.100422](https://doi.org/10.1016/j.measen.2022.100422)
- **File Path**: [Deep Learning driven automated person detection and tracking model on
surveillance videos .pdf](file:///home/endurance/Desktop/Research%20paper/Springer/Deep Learning driven automated person detection and tracking model on
surveillance videos .pdf)
- **Keywords**: Object detection, Object tracking, Surveillance videos, Deep learning, Hyperparameter optimizer

---

## Executive Summary & Objectives
- **Research Problem**: Sub-optimal bounding box accuracy, identity loss, and high tracking failure rates in multi-person surveillance footage due to background clutter, lighting variations, and improper hyperparameter configuration.
- **Application Domain**: Automated Video Surveillance, Crowd Monitoring, and Security Analytics
- **Main Objective**: Propose the DLD-APDT model combining an EfficientDet deep architecture for person detection, RMSProp-based hyperparameter optimization, and continuous multi-frame object tracking in surveillance video streams.
- **Primary Method**: Surveillance video frames -> Pre-processing / frame conversion -> EfficientDet feature pyramid network -> RMSProp hyperparameter tuning -> Bounding box tracking across consecutive frames.
- **Dataset Realism**: Level 3: Semi-Realistic (Trained and validated on standard surveillance benchmark datasets MOT16 and MOT17 featuring real-world CCTV cameras, varied outdoor/indoor environments, and multiple moving pedestrians).

---

## Claim-Evidence Audit
### Claim 1
- **Author Claim**: "The DLD-APDT model achieves 98.2% person detection accuracy and outperforms Faster R-CNN and standard YOLO on MOT surveillance benchmarks."
- **Citation**: Section 3 (Results and Discussion), pp. 4–6, Table 1 & Figure 4
- **Verification Status**: `SUPPORTED`
- **Evidence Level**: Level 4 (Standardized benchmark evaluation on MOT dataset with quantitative precision, recall, and tracking accuracy comparisons).

### Claim 2
- **Author Claim**: "EfficientDet with RMSProp optimization maintains robust person tracking under partial occlusions."
- **Citation**: Section 3, pp. 5–6, Figure 5
- **Verification Status**: `PARTIALLY SUPPORTED`
- **Evidence Level**: Level 3 (Demonstrated on pedestrian crossing sequences, but tracking drift occurs during severe prolonged occlusions).

---

## Failure Scenarios & Edge Cases
- **Tested Scenarios**: Evaluates multi-person tracking and camera perspective variations in pedestrian surveillance. Does not evaluate falls, posture classification, staircase geometry, night IR CCTV, or emergency alerts.
- **Explicit Limitations**: Focuses solely on person detection and tracking; does NOT perform fall detection, posture analysis, or abnormal behavior classification; inference latency on embedded edge hardware is not evaluated (Section 4, p. 7).

---

## Relevance to Target System
- **Target Scenario Alignment**: Directly implements the essential front-end stage of our target CCTV system (person detection and continuous tracking over time in surveillance video). However, does not include fall classification or emergency response.
- **Relevance Score (0–5)**: **3 / 5**
  - *Justification*: Solves the vital front-end prerequisite (detecting and tracking persons in CCTV video), but does not perform fall detection, posture verification, or emergency response orchestration.
- **Methodological Usefulness Score (0–5)**: **3 / 5**
  - *Justification*: Strong automated tracking and EfficientDet optimization, but lacks fall-specific temporal logic or edge deployment benchmarking.

---
*Generated via Research Roadmap Analyzer (Phase 1)*
