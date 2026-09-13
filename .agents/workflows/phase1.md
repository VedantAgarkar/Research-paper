---
description: Prompt 1: Inventory every paper
---

You are a research literature-analysis agent.

Process EVERY PDF inside the specified research folder. Do not skip papers unless the PDF is unreadable or clearly unrelated.

For each paper, extract only information explicitly supported by the paper.

Create a structured record containing:

* paper_id
* title
* authors
* publication_year
* venue
* DOI
* research_problem
* keywords
* application_domain
* relevance_to_our_project
* relevance_score_0_to_5
* methodological_relevance_score_0_to_5

Our target research problem is:

Real-time CCTV-based elderly fall detection, particularly in staircase/common-area environments, using computer vision and temporal movement analysis, followed by local alarm activation, remote notification, acknowledgement monitoring, and escalation when an alert is not acknowledged.

Relevance scoring:

5 = directly addresses almost the same problem
4 = highly relevant methodology/application
3 = useful methodology but substantially different scenario
2 = related background
1 = weakly related
0 = irrelevant

Do not infer missing information.

For every extracted claim, preserve the page number or section where it was found.

Output one structured record per PDF.

Also produce a summary table containing all papers ranked by relevance.
