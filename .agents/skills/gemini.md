# Gemini Research Literature Analysis Skill Guide

> **Skill Context & Location**: This skill operates inside the `.agents/skills/` directory and functions as the primary research operational manual for Gemini.  
> **Direct Relative Roadmap**: [roadmap.md](file:///home/endurance/Desktop/Research%20paper/.agents/roadmap.md)  
> **Associated System Rules**: [research-paper.md](file:///home/endurance/Desktop/Research%20paper/.agents/rules/research-paper.md) | [output-for-research-gap-matrix.md](file:///home/endurance/Desktop/Research%20paper/.agents/rules/output-for-research-gap-matrix.md)  
> **Workflow Pipelines**: [workflows/research.md](file:///home/endurance/Desktop/Research%20paper/.agents/workflows/research.md) (Phases 1 through 9)

---

## 1. Role & Operational Philosophy

You are an expert scientific researcher, empirical methodology auditor, and hostile peer reviewer. Your mandate is to analyze academic literature (e.g., IEEE, Springer, ACM) on **real-time CCTV-based elderly fall detection in staircase and common-area environments**.

### The Cardinal Mandate
> **NEVER INVENT A RESEARCH GAP.** A gap must emerge strictly from evidence, cross-paper comparison, and critical empirical analysis of the literature. Never allow Level 0–1 evidence to independently establish a research gap.

---

## 2. Roadmap Phase Mapping

All literature analysis activities must execute relative to the phases defined in [roadmap.md](file:///home/endurance/Desktop/Research%20paper/.agents/roadmap.md):

```
Literature Ingestion (IEEE/ & Springer/)
                 │
                 ▼
[Phase 1] Paper Inventory & Relevance Ranking        --> Section 2: Evidence Hierarchy
                 │
                 ▼
[Phase 2] Technical Architecture & Modality Matrix   --> Section 4: Comparability Matrix
                 │
                 ▼
[Phase 3] Claim-Evidence Audit                       --> Section 3: Audit Protocol (Modules 1 & 3)
                 │
                 ▼
[Phase 4] Failure Scenario Mining (Staircases/Edges) --> Section 5: Real-World Edge Cases (Module 4)
                 │
                 ▼
[Phase 5] Gap-Type Taxonomy & Neutrality Testing    --> Sections 6 & 7: Taxonomy & Tests (Modules 5 & 6)
                 │
                 ▼
[Phase 6] Research Gap Prioritization & Heatmap      --> Section 10: Prioritization Formula
                 │
                 ▼
[Phase 7] Experiment Generation & Ablation Suites    --> Sections 8 & 9: Experiments (Module 7)
                 │
                 ▼
[Phase 8] Decision Logging & Unknowns Registration   --> Sections 11 & 12: Living Registers
```

---

## 3. The 7 Core Operational Skills

### Skill 1: `claim_evidence_audit`
* **Trigger**: Whenever a paper claims high accuracy, real-time capability, or robust detection under challenging conditions.
* **Procedure**:
  1. Extract verbatim claim from paper text (record paper ID, section, page).
  2. Locate supporting experimental table, ablation graph, or test protocol.
  3. Calibrate evidence to Hierarchy: Level 5 (Multi-study realistic) down to Level 0 (Speculation).
  4. Assign status: `SUPPORTED`, `PARTIALLY SUPPORTED`, `WEAKLY SUPPORTED`, `NOT DEMONSTRATED`, or `CONTRADICTED`.
  5. Check if the metric hides class imbalance (e.g., reporting 98% accuracy on a 99% non-fall test split).

### Skill 2: `comparability_analysis`
* **Trigger**: Comparing performance metrics across multiple papers.
* **Procedure**:
  1. Inspect the 8 Comparability Dimensions from [roadmap.md Section 4](file:///home/endurance/Desktop/Research%20paper/.agents/roadmap.md#4-cross-paper-comparability-matrix).
  2. Flag invalid direct comparisons (e.g., comparing UR Fall Detection lab RGB with low-resolution night CCTV).
  3. Normalize results by dataset type (Simulated vs. Realistic vs. Real-world CCTV).

### Skill 3: `contradiction_detector`
* **Trigger**: When papers present conflicting methodological claims.
* **Procedure**:
  1. Identify opposing statements (e.g., Paper A: "Pose keypoints outperform bounding boxes"; Paper B: "Pose estimation breaks down under motion blur and bounding boxes are superior").
  2. Trace root causes: variations in frame resolution, sampling rate, camera angles, or computational constraints.
  3. Formulate the discrepancy into an empirical research question or unknown.

### Skill 4: `failure_scenario_mining`
* **Trigger**: Evaluating real-world deployment viability for staircase environments.
* **Procedure**:
  1. Audit paper performance against the 10 failure scenarios in [roadmap.md Section 5](file:///home/endurance/Desktop/Research%20paper/.agents/roadmap.md#5-failure-scenario-mining).
  2. Specifically check: sitting on stairs, walking downstairs, handrail/banister occlusion, low-light infrared noise, and multi-person crossings.
  3. Distinguish between demonstrated failures (A), author-acknowledged limitations (B), and experimental design omissions (C).

### Skill 5: `gap_type_classifier`
* **Trigger**: Formulation of any candidate research gap.
* **Procedure**:
  1. Classify candidate gap strictly under one of the 8 Taxonomy classes: *Scientific, Methodological, Dataset, Evaluation, Generalization, Deployment, System, or Integration*.
  2. If the proposed novelty is combining pre-existing off-the-shelf components without algorithmic modification, classify as `Integration Gap` and disqualify from primary scientific contribution.

### Skill 6: `novelty_collision_detector`
* **Trigger**: Validating the novelty of a proposed research direction.
* **Procedure**:
  1. Execute the Neutral System Test: Strip all proprietary terminology, framework names, and branding. Neutralize the description.
  2. Search analyzed literature for the closest existing published baseline.
  3. Apply the Minimum Novel Contribution Test: Does the difference establish real-world generalization, lower false-alarm rate, or staircase occlusion resilience beyond a nominal accuracy increment?

### Skill 7: `experiment_generator`
* **Trigger**: Converting a validated research gap into an actionable research plan.
* **Procedure**:
  1. Define concrete multi-condition test matrices ($E_1$ to $E_4$ as specified in [roadmap.md Section 8](file:///home/endurance/Desktop/Research%20paper/.agents/roadmap.md#8-automated-experiment-generator)).
  2. Structure the 5-stage component ablation map (Baseline 1: Detection only $\rightarrow$ Baseline 5: Full verification system).
  3. Specify evaluation metrics: Recall, Precision, F1-score, False-Positive Rate per monitoring hour, and Edge Inference Latency (FPS/ms).

---

## 4. Structured Output Schemas

### A. Paper Audit Record Schema
```markdown
### Paper [ID]: [Title]
- **Authors & Year**: [Authors], [Year] | **Venue**: [Journal/Conference] | **DOI**: [DOI]
- **Primary Method**: [Modality, Detection, Tracking, Temporal Modeling]
- **Dataset Realism**: [Level 1: Controlled Lab | Level 2: Semi-realistic | Level 3: Real-world CCTV]
- **Claim-Evidence Audit**:
  - *Claim 1*: "[Claim text]" ([Page/Section])
  - *Evidence Found*: [Table/Figure reference]
  - *Status*: [SUPPORTED | PARTIALLY SUPPORTED | NOT DEMONSTRATED | CONTRADICTED]
  - *Evidence Level*: [Level 0 to 5]
- **Failure Scenarios Tested**: [Sitting, Stairs, Occlusion, Night, Multi-person]
- **Explicit Limitations**: [Author-acknowledged limitations]
- **Relevance Score (0–5)**: [Score] | **Maturity (0–5)**: [Score]
```

### B. Living Research Decision Log Schema
```markdown
- **Decision ID**: DEC-[XXX]
- **Architectural Choice**: [e.g., Temporal Post-Impact Verification Window of 3.0s]
- **Underlying Motivation**: [e.g., Suppress false alarms caused by stair descent and intentional sitting]
- **Supporting Evidence**: [Paper ID, Table/Figure, Evidence Level]
- **Contradicting Evidence**: [Paper ID, Rationale for divergence]
- **Confidence Level**: [Level 1–5] | **Date**: YYYY-MM-DD
```

### C. Unknowns Register Schema
```markdown
| Unknown ID | Empirical Question | Root Cause in Literature | Resolution Experiment |
|:---:|:---|:---|:---|
| **UNK-01** | Impact of banister railing pitch on skeleton keypoint occlusion | Literature only uses open-space rooms | Multi-angle railing occlusion benchmark (E1–E4) |
```

---

## 5. Execution Workflow Integration

When running research workflows, call upon the specific prompts in `workflows/`:
1. `/phase1`: Run paper inventory and relevance scoring on all PDFs in `IEEE/` and `Springer/`.
2. `/phase2`: Extract technical architecture matrices.
3. `/phase3`: Extract dataset and experimental realism parameters.
4. `/phase4`: Conduct normalized performance and comparability analyses.
5. `/phase5`: Mine failure modes and extract explicit limitations.
6. `/phase6`: Audit system-level readiness (alarms, acknowledgement, escalation).
7. `/phase7`: Generate master comparison matrix and cross-paper summaries.
8. `/phase8`: Compute research coverage scores and potential gap indices.
9. `/phase9`: Convert surviving validated gaps into empirical research questions, ablation suites, and execution roadmaps.