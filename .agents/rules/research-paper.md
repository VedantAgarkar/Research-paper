---
trigger: always_on
---

Create a reusable research literature-analysis skill for my project on real-time CCTV-based elderly fall detection.

The skill will be used to analyze a folder containing multiple research-paper PDFs, potentially 25–30+ papers. I will upload/add the papers after this skill is created.

PROJECT CONTEXT

Target scenario:

An elderly person falls on a staircase at approximately 8:42 PM.

A CCTV camera continuously provides video to a local computer. The computer detects and tracks the person, analyzes their posture and temporal movement, and determines whether the sequence represents an actual fall rather than normal activities such as sitting, lying down, kneeling, bending, stumbling, or walking down stairs.

When a fall is sufficiently verified:

1. Activate a local alarm/buzzer.
2. Send an alert to nearby flats/building security.
3. Include the location, for example:
   "Possible Fall Detected — Staircase, Floor 2"
4. Optionally send a CCTV frame or short video clip as evidence.
5. Wait for acknowledgement.
6. If nobody acknowledges within X seconds, escalate the alert to another contact/security desk.

The laptop/computer is expected to perform the computationally intensive AI processing. External hardware may be used for local alarms and communication.

RESEARCH OBJECTIVE

The purpose of the literature analysis is NOT simply to summarize papers.

The ultimate goal is to systematically analyze the existing research, identify what has already been solved, identify recurring limitations and underexplored areas, and discover a defensible research gap that can become the basis of our research contribution.

The skill must therefore behave like a rigorous research assistant and comparative literature-analysis system.

IMPORTANT RESEARCH RULES

1. Analyze EVERY paper provided in the folder.
2. Never silently skip a paper.
3. Never invent information that is not present in a paper.
4. Distinguish clearly between:
   - Explicitly reported
   - Not reported
   - Inferred from methodology
5. "Not reported" must NOT automatically be interpreted as "not supported".
6. Preserve the exact paper title and identify each paper with a unique Paper ID.
7. Record page number and/or section for important extracted claims.
8. Do not treat high accuracy on one dataset as proof that a method is superior to another method evaluated on a different dataset.
9. Do not declare something a research gap merely because one paper did not discuss it.
10. A research gap must be supported by evidence across multiple papers whenever possible.
11. Actively search for evidence that could DISPROVE a proposed research gap.
12. Separate genuine research contributions from simple engineering/integration work.

PHASE 1 — PAPER INVENTORY

For every PDF create a structured record containing:

- Paper ID
- Title
- Authors
- Publication year
- Journal/conference
- DOI
- Keywords
- Research problem
- Application domain
- Main objective
- Relevance to our project
- Relevance score from 0–5
- Methodological usefulness score from 0–5

Relevance scoring:

5 = directly addresses almost the same problem
4 = highly relevant
3 = relevant methodology but different scenario
2 = related/background
1 = weakly related
0 = irrelevant

Rank all papers by relevance.

PHASE 2 — TECHNICAL METHODOLOGY EXTRACTION

For every paper extract:

- Input modality
- RGB/depth/thermal/etc.
- Camera type
- Camera placement
- Camera viewpoint
- Person detection method
- Person tracking method
- Pose estimation
- Skeleton/body representation
- Feature extraction
- Spatial features
- Motion features
- Temporal features
- Classification algorithm
- Deep learning architecture
- CNN/RNN/LSTM/GRU/Transformer/etc.
- Fall-decision mechanism
- Confidence thresholds
- Temporal window
- False-positive reduction
- Multiple-person handling
- Occlusion handling
- Lighting handling
- Camera-angle variation
- Staircase handling
- Real-time capability
- FPS
- Latency
- Hardware
- Software/frameworks
- Computational requirements

Create a cross-paper comparison matrix.

PHASE 3 — DATASET AND EXPERIMENTAL REALISM

For every paper extract:

- Dataset name
- Dataset source
- Public/private
- Number of videos
- Number of subjects
- Age information
- Fall samples
- Non-fall samples
- Fall types
- Normal activities
- Real vs simulated falls
- Controlled vs uncontrolled environment
- Indoor/outdoor
- CCTV usage
- Staircase scenarios
- Multiple people
- Occlusion
- Lighting conditions
- Camera viewpoints
- Training/test methodology
- Cross-subject testing
- Cross-environment testing
- Evaluation protocol

Classify experimental realism as:

1. Highly controlled
2. Moderately controlled
3. Semi-realistic
4. Real-world

Explain the classification using evidence from the paper.

PHASE 4 — PERFORMANCE ANALYSIS

Extract wherever available:

- Accuracy
- Precision
- Recall
- Sensitivity
- Specificity
- F1-score
- AUC
- False-positive rate
- False-negative rate
- Detection rate
- Miss rate
- FPS
- Inference latency
- Processing time

Also record:

- Dataset used
- Number of test samples
- Baseline methods
- Ablation studies
- Evaluation protocol
- Whether results are directly comparable

Flag misleading or non-comparable performance comparisons.

PHASE 5 — FAILURE MODES AND LIMITATIONS

Identify:

- Explicit limitations
- Future work
- False positives
- False negatives
- Occlusion failures
- Lighting failures
- Camera-angle failures
- Multiple-person failures
- Staircase failures
- Sitting confusion
- Lying-down confusion
- Kneeling confusion
- Bending confusion
- Stumbling confusion
- Walking confusion
- Slow falls
- Fast falls
- Partial falls
- Person leaving frame
- Tracking failures
- Detection failures
- Dataset limitations
- Generalization limitations
- Computational limitations
- Real-time limitations
- Privacy concerns
- Deployment limitations
- Alert/communication limitations

For every limitation classify it as:

A. Demonstrated failure
B. Explicitly acknowledged limitation
C. Limitation implied by experimental design

Always provide supporting evidence.

PHASE 6 — SYSTEM-LEVEL ANALYSIS

Analyze whether each paper addresses:

- Continuous CCTV monitoring
- Person detection
- Person tracking
- Fall verification
- Temporal reasoning
- Local alarm
- Remote alert
- Mobile notification
- Security-desk notification
- Image/clip evidence
- Human acknowledgement
- Alert timeout
- Escalation
- Multi-level emergency response
- Privacy/local processing

Create a YES / NO / PARTIAL / NOT REPORTED matrix.

Do NOT interpret NOT REPORTED as NO.

PHASE 7 — MASTER COMPARISON MATRIX

Create a master table where:

ROWS = research papers

COLUMNS = important research/system features

Include at least:

Paper
Year
Dataset
Environment
Detection
Tracking
Pose
Features
Temporal Model
Classifier
Real/Simulated Falls
Multiple People
Occlusion
Lighting
Camera Variation
Staircase
Non-Fall Activities
False-Positive Handling
Real-Time
FPS
Accuracy
Precision
Recall
F1
Hardware
Local Alarm
Remote Alert
Evidence
Acknowledgement
Escalation
Privacy
Main Limitation
Relevance Score

Keep the table structured and sortable.

PHASE 8 — RESEARCH COVERAGE ANALYSIS

For every research dimension calculate:

- Number of papers addressing it
- Percentage of papers addressing it
- Number partially addressing it
- Number not reporting it

Classify each dimension as:

- Saturated
- Well explored
- Moderately explored
- Underexplored
- Highly underexplored

Pay special attention to:

- Staircase environments
- Elderly subjects
- Real-world CCTV
- Multiple people
- Occlusion
- Night/low-light conditions
- Non-fall activity discrimination
- False-positive reduction
- Temporal verification
- Real-time deployment
- Privacy/local processing
- Alert systems
- Acknowledgement
- Escalation

PHASE 9 — RESEARCH GAP DISCOVERY

Generate candidate research gaps based on the evidence.

For each candidate gap provide:

- Gap statement
- Supporting papers
- Number of papers addressing the issue
- Number not addressing it
- Evidence
- Why it matters
- Technical difficulty
- Novelty potential
- Practical importance
- Student-project feasibility
- Potential experimental design
- Risks
- Existing work that might invalidate the gap

Score each candidate:

Novelty: 1–5
Importance: 1–5
Feasibility: 1–5
Evidence strength: 1–5

Do NOT generate generic gaps such as:

"Improve accuracy"
"Use deep learning"
"Use a larger dataset"

unless the literature provides a specific unresolved reason.

PHASE 10 — GAP STRESS TEST

Act as a hostile peer reviewer.

For every proposed research gap, actively attempt to disprove it.

Search the analyzed papers for evidence that:

- The problem has already been solved.
- Another paper already implements the proposed approach.
- The problem is actually well studied.
- The apparent gap exists only because papers failed to report something.
- The proposed contribution is merely engineering integration.
- The proposed novelty is too incremental.
- The gap cannot be experimentally evaluated.
- The proposed research would not produce meaningful scientific knowledge.

Classify each proposed gap as:

VALID
WEAK
UNSUPPORTED
ALREADY ADDRESSED

Only retain gaps that survive the stress test.

PHASE 11 — RESEARCH DIRECTION

For the strongest surviving gaps, produce:

- Research problem
- Research gap
- Research question
- Hypothesis
- Objectives
- Proposed technical approach
- Novel components
- Experimental variables
- Baselines
- Dataset strategy
- Testing strategy
- Negative/non-fall scenarios
- Evaluation metrics
- Ablation studies
- Real-time evaluation
- False-positive evaluation
- Staircase-specific evaluation
- Hardware architecture
- Alert architecture
- Acknowledgement mechanism
- Escalation mechanism
- Privacy considerations
- Expected contribution
- Risks
- Alternative/fallback research direction

Clearly distinguish:

RESEARCH CONTRIBUTION
from
ENGINEERING IMPLEMENTATION
from
EXPERIMENTAL CONTRIBUTION

PHASE 12 — FINAL OUTPUTS

Maintain the following outputs inside the research workspace:

1. Paper Inventory
2. Individual Paper Analyses
3. Master Literature Matrix
4. Dataset Comparison
5. Methodology Comparison
6. Performance Comparison
7. Limitations Matrix
8. System-Level Comparison
9. Research Coverage Matrix
10. Research Gap Candidates
11. Gap Stress Test
12. Final Research Gaps
13. Proposed Research Questions
14. Research Roadmap

Use consistent terminology across all papers.

When new papers are added, analyze only the new papers first and then update all aggregate matrices and gap analyses without destroying previous work.

The final purpose of this skill is to transform a folder of research PDFs into an evidence-backed understanding of:

WHAT HAS BEEN DONE
WHAT HAS NOT BEEN DONE
WHAT IS ACTUALLY DIFFICULT
WHAT THE LITERATURE DISAGREES ABOUT
WHERE THE REAL RESEARCH GAP EXISTS
AND WHAT WE CAN SCIENTIFICALLY INVESTIGATE.