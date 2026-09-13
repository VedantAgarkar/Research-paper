---
name: research-roadmap-analyzer
description: >-
  Executes evidence-driven literature analysis, claim-evidence audits, comparability analysis,
  failure scenario mining, gap-type classification, and experiment generation based on the research roadmap.
  Use when analyzing academic papers, assessing fall detection methodologies, validating research gaps,
  or designing empirical ablation studies.
---

# Research Roadmap Analyzer Skill

This skill provides an evidence-based operational toolkit for conducting literature research on real-time CCTV-based elderly fall detection in staircase/common-area environments.

## Core Directives & References
- **Roadmap Blueprint**: [roadmap.md](file:///home/endurance/Desktop/Research%20paper/.agents/roadmap.md)
- **Detailed Gemini Skill Manual**: [gemini.md](file:///home/endurance/Desktop/Research%20paper/.agents/skills/gemini.md)
- **Research Rules**: [research-paper.md](file:///home/endurance/Desktop/Research%20paper/.agents/rules/research-paper.md)
- **Heatmap Guidelines**: [output-for-research-gap-matrix.md](file:///home/endurance/Desktop/Research%20paper/.agents/rules/output-for-research-gap-matrix.md)

## Operational Procedures

1. **Paper Claim-Evidence Audit**:
   - Verify all author claims against concrete tables, figures, and ablation data.
   - Tag claims as `SUPPORTED`, `PARTIALLY SUPPORTED`, `WEAKLY SUPPORTED`, `NOT DEMONSTRATED`, or `CONTRADICTED`.
   - Strictly apply the Evidence Hierarchy (Level 0: Speculation to Level 5: Multi-Study Realistic Proof). Disallow Level 0–1 evidence from forming a gap.

2. **Comparability Normalization**:
   - Normalize cross-paper comparisons across the 8 dimensions: dataset type, fall definition, class distribution, train/test split, subject demographics, environment/angle, sensor setup, and metrics.

3. **Failure Scenario Mining**:
   - Explicitly evaluate systems against critical staircase edge cases: sitting on stairs, stair descent, banister/railing occlusion, night/IR noise, and multi-person tracking crossings.

4. **Gap-Type Classification**:
   - Categorize all candidate gaps into the 8 taxonomy types (Scientific, Methodological, Dataset, Evaluation, Generalization, Deployment, System, Integration).
   - Enforce the Neutral System Test and Minimum Novelty Test to ensure genuine scientific merit rather than off-the-shelf integration.

5. **Experiment Generation & Ablation Mapping**:
   - Map surviving gaps to concrete multi-condition test matrices ($E_1$ to $E_4$) and 5-stage incremental ablation suites (Baseline 1: Detection only to Baseline 5: Full verification system).
