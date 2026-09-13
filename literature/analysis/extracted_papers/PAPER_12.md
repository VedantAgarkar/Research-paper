# PAPER_12: Real-Time Vision-Based Fall Detection Systems for the Elderly: A Systematic Review

## Metadata
- **Authors**: Mahammad Nabizade, Réda Yahiaoui, Isabelle Lajoie, Nassima Nacer, Frédéric Auber, Moustafa Fayad
- **Publication Year**: 2026
- **Venue**: Sensors (MDPI, vol. 26, no. 16, 5069, pp. 1–16)
- **DOI**: [10.3390/s26165069](https://doi.org/10.3390/s26165069)
- **File Path**: [sensors-26-05069.pdf](file:///home/endurance/Desktop/Research%20paper/Springer/sensors-26-05069.pdf)
- **Keywords**: PRISMA, fall detection, computer vision, deep learning, real-time, edge devices

---

## Executive Summary & Objectives
- **Research Problem**: The vast majority of published vision-based fall detection models claim 'real-time' capability in theory but fail to benchmark on physical hardware or report inference latency; lack of standardized real-time performance thresholds.
- **Application Domain**: Real-Time Clinical & Domestic Fall Detection on Embedded Hardware
- **Main Objective**: Conduct a PRISMA-compliant systematic review filtering 588 papers down to the 11 studies that rigorously evaluate vision-based deep learning fall detection on physical hardware, establishing an empirical 10 FPS threshold based on human fall biomechanics.
- **Primary Method**: PRISMA and Kitchenham systematic review protocol; strict screening for vision models evaluated on physical edge hardware (Jetson Nano/Xavier/TX2, Raspberry Pi, Intel NUC, PC workstations); hardware latency and FPS synthesis.
- **Dataset Realism**: Level 4: Multi-Study Meta-Analysis (Systematically audits hardware benchmarks across public datasets UR Fall, Multiple FDD, Le2i, and custom sets).

---

## Claim-Evidence Audit
### Claim 1
- **Author Claim**: "Out of 588 candidate papers claiming real-time vision fall detection, only 11 (1.87%) actually implemented and evaluated their models on physical hardware with reported FPS and latency."
- **Citation**: Section 4.1 (Study Selection) & Table 1, pp. 6–8
- **Verification Status**: `SUPPORTED`
- **Evidence Level**: Level 5 (Rigorous PRISMA screening across IEEE Xplore, ACM, Web of Science, and Scopus, establishing the reality of the deployment gap).

### Claim 2
- **Author Claim**: "A minimum frame rate of 10 FPS is required for vision-based fall detection based on the 0.3s–0.8s physiological duration of the critical fall impact phase."
- **Citation**: Section 1 & Section 5.1, pp. 2, 11–12
- **Verification Status**: `SUPPORTED`
- **Evidence Level**: Level 5 (Biomechanical justification supported by geriatric motion analysis literature).

---

## Failure Scenarios & Edge Cases
- **Tested Scenarios**: Evaluates hardware bottlenecks, thermal throttling on edge devices, lightweight vs heavy model trade-offs, and alarm response mechanisms (buzzer, SMS, email). Explicitly highlights the total absence of staircase evaluations.
- **Explicit Limitations**: Systematic review; reveals that no published hardware-tested vision systems evaluate multi-person tracking or complex multi-level staircase environments; alert systems in literature are rudimentary single-shot alerts without acknowledgement or escalation (Section 5.3, pp. 12–13).

---

## Relevance to Target System
- **Target Scenario Alignment**: Foundational empirical guidance for our target system: validates our local edge PC deployment choice, establishes the 10 FPS latency requirement, documents alarm/buzzer implementations, and confirms the absence of acknowledgement/escalation in existing systems.
- **Relevance Score (0–5)**: **5 / 5**
  - *Justification*: Critically relevant systematic review proving the real-time edge deployment gap, defining the 10 FPS biomechanical threshold, and reviewing physical alarm mechanisms.
- **Methodological Usefulness Score (0–5)**: **5 / 5**
  - *Justification*: Provides indispensable hardware benchmarking standards, latency trade-off tables, and edge deployment criteria directly governing our system design.

---
*Generated via Research Roadmap Analyzer (Phase 1)*
