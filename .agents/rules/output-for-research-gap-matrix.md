---
trigger: always_on
---

RESEARCH GAP HEATMAP

Create a Research Gap Heatmap after completing the individual-paper extraction and cross-paper comparison.

The heatmap must be evidence-driven and must NOT be based on subjective intuition alone.

PURPOSE

The heatmap is a visual research landscape showing:

- How extensively each research dimension has been studied.
- How relevant each dimension is to our target system.
- How adequately existing research addresses it.
- Where the strongest potential research gaps are.

The heatmap is NOT itself proof of a research gap.

It is a screening and prioritization tool. Every high-gap area must be traceable back to the underlying papers.

TARGET SYSTEM

Our target system is:

A real-time CCTV-based elderly fall-detection system operating in staircase/common-area environments.

The system should:

- Continuously monitor CCTV video.
- Detect people.
- Track people over time.
- Analyze posture and temporal movement.
- Distinguish falls from normal activities.
- Handle realistic environmental conditions.
- Operate in real time.
- Trigger a local alarm.
- Send remote alerts.
- Optionally provide visual evidence.
- Wait for human acknowledgement.
- Escalate an unanswered alert.

HEATMAP DIMENSIONS

Create rows for the following research dimensions.

A. CORE COMPUTER VISION

1. Person detection
2. Person tracking
3. Pose estimation
4. Skeleton/body representation
5. Feature extraction
6. Motion analysis
7. Temporal modelling
8. Fall classification
9. Fall verification

B. ROBUSTNESS

10. False-positive reduction
11. Non-fall activity discrimination
12. Multiple-person detection
13. Multiple-person tracking
14. Occlusion handling
15. Lighting variation
16. Night/low-light conditions
17. Camera-angle variation
18. Distance from camera
19. Partial visibility
20. Person entering/leaving frame

C. REAL-WORLD FALL DETECTION

21. Staircase environments
22. Elderly-specific evaluation
23. Real-world CCTV
24. Real rather than simulated falls
25. Uncontrolled environments
26. Cross-environment generalization
27. Cross-camera generalization
28. Realistic negative activities

D. COMPUTATION AND DEPLOYMENT

29. Real-time inference
30. Low-latency processing
31. Local/edge processing
32. Resource efficiency
33. Privacy-preserving processing

E. EMERGENCY RESPONSE

34. Local alarm
35. Remote notification
36. Security notification
37. Image/clip evidence
38. Human acknowledgement
39. Alert timeout
40. Alert escalation
41. End-to-end emergency response

You may add additional dimensions if the literature reveals an important recurring research issue.

Do not remove dimensions simply because few papers discuss them.

LITERATURE COVERAGE SCORE

For every dimension calculate how extensively the literature addresses it.

Use the number of papers that genuinely evaluate the dimension, not merely mention it.

Calculate:

Coverage Percentage =
(Number of papers with meaningful evaluation / Total relevant papers) × 100

Then convert to:

5 = 81–100%
4 = 61–80%
3 = 41–60%
2 = 21–40%
1 = 1–20%
0 = 0%

Meaning:

5 = heavily studied
4 = well studied
3 = moderately studied
2 = limited coverage
1 = highly underexplored
0 = essentially absent

IMPORTANT:

A paper that merely mentions a capability without experimentally evaluating it should NOT count as meaningful coverage.

A paper marked "NOT REPORTED" should NOT count as coverage.

A paper with PARTIAL evaluation should receive 0.5 contribution when calculating coverage.

OUR RELEVANCE SCORE

Score how important the dimension is specifically to our target scenario.

5 = critical to our system
4 = highly important
3 = important
2 = useful but not essential
1 = peripheral
0 = irrelevant

Examples:

Staircase environments = 5

False-positive reduction = 5

Temporal fall verification = 5

Alert escalation = 4 or 5

Person detection = 4

A minor architectural optimization unrelated to deployment = 1 or 2

Do not automatically assign high relevance. Justify each score.

EXISTING SOLUTION MATURITY

Add a separate score representing how well existing literature appears to solve the problem.

5 = mature and extensively validated
4 = strong existing solutions
3 = reasonably developed but limitations remain
2 = weak/limited solutions
1 = very limited solutions
0 = essentially unresolved

This score must consider:

- Number of papers
- Experimental quality
- Dataset realism
- Generalization
- Robustness
- Reproducibility
- Reported failures
- Real-world validation

Do NOT equate "many papers" with "solved".

A topic can have many papers but still have poor real-world validation.

POTENTIAL GAP SCORE

Calculate a potential gap score using:

Gap Potential =
Literature Undercoverage
×
Our Relevance
×
Unresolvedness

Normalize the result to a 0–5 scale.

Use the following conceptual interpretation:

5 = very strong potential gap
4 = strong potential gap
3 = moderate potential gap
2 = weak potential gap
1 = minimal gap
0 = essentially no gap

The gap score must never be based purely on low paper count.

For example:

If only one paper studies staircases but that paper completely solves the problem with strong real-world validation, the gap should NOT automatically be high.

Likewise:

If 15 papers study fall detection but all use controlled simulated datasets, real-world robustness may still have high gap potential.

EVIDENCE STRENGTH

For every heatmap row also calculate evidence strength.

5 = multiple papers directly support the conclusion
4 = several papers support it
3 = moderate evidence
2 = limited evidence
1 = weak evidence
0 = insufficient evidence

This prevents a dimension from appearing as a major research gap simply because only one paper happened to mention it.

HEATMAP TABLE

Create a master table with these columns:

Dimension
Category
Papers Evaluating
Coverage %
Coverage Score
Our Relevance
Existing Solution Maturity
Unresolvedness
Gap Potential
Evidence Strength
Key Evidence
Important Papers
Main Limitation
Research Gap Candidate

Example structure:

| Dimension | Coverage | Relevance | Maturity | Gap Potential |
| Person detection | High | High | High | Low |
| Temporal reasoning | High | Very High | Medium | Medium |
| False-positive reduction | Medium | Very High | Medium | High |
| Staircase environments | Low | Very High | Low | Very High |
| Occlusion | Low | Very High | Low | High |
| Night CCTV | Low | High | Low | High |
| Multiple people | Low | High | Low | High |
| Real elderly subjects | Low | Very High | Low | Very High |
| Alert acknowledgement | Very Low | High | Very Low | Very High |
| Alert escalation | Very Low | High | Very Low | Very High |

These example classifications are ONLY examples.

Calculate the actual values from the analyzed papers.

HEATMAP VISUALIZATION

Create a visual heatmap where:

ROWS = research dimensions

COLUMNS = analytical factors

Columns should be:

1. Literature Coverage
2. Our Relevance
3. Existing Solution Maturity
4. Unresolvedness
5. Gap Potential
6. Evidence Strength

Use a 0–5 numerical scale.

Use a consistent visual scale:

0 = absent
1 = very low
2 = low
3 = medium
4 = high
5 = very high

Do not use arbitrary colors for individual rows.

Use one consistent gradient where darker/intense cells represent higher numerical values and lighter cells represent lower values.

Do not make "high gap" visually equivalent to "high coverage".

They represent different things.

GAP INTERPRETATION

After creating the heatmap, create four zones:

ZONE 1 — HIGH COVERAGE / LOW GAP

These are mature areas.

Examples may include:

- Person detection
- Basic fall classification
- Standard CNN architectures

Do not prioritize these as primary research gaps unless a specific unresolved issue exists.

ZONE 2 — HIGH COVERAGE / HIGH GAP

These are heavily studied but still poorly solved.

These are extremely important.

They may indicate:

- persistent technical difficulty
- disagreement between methods
- poor real-world generalization
- high false-positive rates
- unrealistic evaluation datasets

These can produce stronger research questions than simply finding an unexplored topic.

ZONE 3 — LOW COVERAGE / HIGH RELEVANCE

These are potential research-gap hotspots.

Examples might include:

- staircase environments
- elderly-specific evaluation
- realistic CCTV deployment
- occlusion
- night conditions
- real-world negative activities
- alert acknowledgement
- escalation

However, do not automatically call these research gaps.

Investigate whether the lack of literature reflects:

- genuinely neglected research
- lack of suitable datasets
- ethical constraints
- engineering rather than scientific novelty
- papers simply not reporting the feature

ZONE 4 — LOW COVERAGE / LOW RELEVANCE

These are low priority.

Do not waste research effort here unless another reason makes them important.

RESEARCH GAP PRIORITY MAP

After the heatmap, create a second table ranking the top potential research areas.

Columns:

Rank
Research Dimension
Coverage
Relevance
Maturity
Gap Potential
Evidence Strength
Technical Difficulty
Experimental Testability
Novelty Potential
Practical Importance
Overall Priority
Reason

Overall Priority should consider:

Gap Potential
×
Evidence Strength
×
Experimental Testability
×
Practical Importance

Do not prioritize a theoretically novel gap that cannot realistically be tested.

INTERSECTION HEATMAP

After the single-dimension heatmap, create an INTERSECTION ANALYSIS.

Look for combinations of dimensions that are poorly studied together.

Examples:

- Staircase + elderly + CCTV
- Staircase + occlusion
- Staircase + multiple people
- Night CCTV + fall detection
- Temporal verification + non-fall discrimination
- Multiple people + temporal tracking
- Real-world CCTV + elderly subjects
- Realistic falls + false-positive evaluation
- Local AI + privacy
- Fall detection + human acknowledgement
- Fall detection + escalation

For each combination calculate:

- Number of papers studying the combination
- Coverage
- Relevance
- Evidence strength
- Potential gap

This intersection analysis is extremely important.

A research gap may exist not because individual components are new, but because an important combination remains poorly investigated.

FINAL HEATMAP INTERPRETATION

After generating the heatmaps, write a concise research interpretation answering:

1. Which areas are already mature?
2. Which areas remain technically difficult despite substantial research?
3. Which areas are underexplored?
4. Which areas are highly relevant to our system?
5. Which areas have the strongest evidence of unresolved problems?
6. Which apparent gaps are probably false gaps?
7. Which combinations of dimensions appear most promising?
8. Which 3–5 research directions deserve deeper investigation?

Then perform the skeptical gap validation process.

Do not say:

"Staircase fall detection is a research gap because only one paper studied it."

Instead say something like:

"Only X of Y analyzed papers experimentally evaluate staircase environments. Among those that do, the evaluated scenarios are limited by A, B, and C. Therefore, staircase-specific fall detection under conditions X and Y may represent a potential gap. This requires further verification."

Every conclusion must remain proportional to the evidence.

TRACEABILITY

Every high-gap heatmap cell must be traceable to:

Paper ID
Page
Section/table/figure
Evidence type

Maintain an evidence table:

| Gap | Paper | Page | Evidence | Supports/Contradicts |
| ... | ... | ... | ... | ... |

The heatmap must therefore function as a visual summary of the literature database rather than a subjective diagram.

FINAL RULE

The heatmap is an analytical instrument, not the conclusion.

The final research gap must be established only after:

Paper extraction
→ Cross-paper comparison
→ Coverage analysis
→ Heatmap
→ Intersection analysis
→ Gap candidates
→ Skeptical stress test
→ Final gap selection