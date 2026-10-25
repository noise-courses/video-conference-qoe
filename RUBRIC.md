# Grading rubric — Assignment 2 (take-home midterm): Video Conferencing QoE Inference

**10 points, graded for completion.** This is the take-home midterm. The same
rule as Assignment 1 applies: if the notebook runs end to end and each step
does what it asks, you get full credit. The MAE you achieve is *not* graded; a
working pipeline with a poor frame-rate predictor is 10/10.

**Collaboration: none.** Unlike Assignment 1, this is individual work. Do not
discuss the problems or your code with other students. You may use any tools,
including AI tools (acknowledge them in the notebook, as on Assignment 1), and
you may talk to the TAs, who will discuss concepts but not give answers.

| # | Item | Pts |
|---|---|---|
| **Step 1 — Inspecting the trace** | | **5** |
| 1.1 | Load `teams.csv` into a DataFrame | 1 |
| 1.2 | Answer whether the call was peer-to-peer or SFU, **with a brief justification** from the trace | 1 |
| 1.3 | Filter to SRTP video packets only (payload types 102 and 107) | 1 |
| 1.4 | Compute the total call duration in minutes from the filtered trace, and identify participant A's IP address (the capturing host, which sends less video than it receives) | 1 |
| 1.5 | Extract the SSRC from the `Info` column, keep only SSRCs present for at least 5 seconds, and add a `Participant` column labelled A/B/C with A as the captured participant | 1 |
| **Step 2 — Ground-truth frame rate** | | **1** |
| 2.1 | **Plot** the three ground-truth frame-rate series against call time (seconds from the first packet in the trace) in a single figure | 1 |
| **Step 3 — QoE prediction** | | **4** |
| 3.1 | Add a `window_id` column following the stated rounding rule, with times relative to the first packet in the trace | 1 |
| 3.2 | Compute per-`window_id`, per-`Participant` features from the transport and network layers only (packet size and inter-arrival statistics, etc.); no application-layer features | 1 |
| 3.3 | Split the feature matrix per participant and join a `Ground Truth` column from `FPS_A`, `FPS_B`, `FPS_C`, accounting for the 2-second offset of B and C | 1 |
| 3.4 | Temporal 80/20 split per participant (first 80% of windows train, last 20% test), at least one model, and the mean absolute error printed separately for each participant | 1 |

## Bonus (not part of the 10 points)

| # | Item | Pts |
|---|---|---|
| B1 | Plot feature-importance scores for each participant's model, with a sentence on whether they agree across participants | bonus |
| B2 | Train a single model for all three participants and compare its MAE with the average MAE of the three per-participant models | bonus |

A good-faith attempt at either bonus item is noted in feedback; it does not
change the 10-point score and skipping it costs nothing.

## Requirements that gate the score

- **The notebook must run.** Submit it *executed* (outputs saved). A notebook
  with error tracebacks in the cells that implement graded items, or with no
  outputs at all, is treated as not running: those items earn 0 until fixed
  and resubmitted.
- **Sub-items are all-or-nothing.** Each row is 1 point if done in good faith,
  0 if absent. There are no half points; "did the thing" is the bar.
- **Written answers count.** Item 1.2 requires a sentence or two of
  justification, not just a one-word answer.
- **Random splits do not count for 3.4.** The notebook asks for a temporal
  split; a shuffled `train_test_split` earns 0 for that row until fixed.
- **Data.** `teams.csv` is in
  [noise-courses/data](https://github.com/noise-courses/data) under
  `video-conference-qoe/`; the notebook expects that repository cloned at
  `data/`. A copy also ships in this repo's `data/` folder. Paths are not
  graded.
- **AI use.** Encouraged, but acknowledge it in the notebook and be ready to
  explain your code. Not acknowledging AI use does not cost points on this
  assignment, but see the syllabus on assessment of understanding.

## Late policy

Due 11:59 p.m. Chicago time on the due date; 96-hour grace balance for the term,
then half credit within one week, then zero. See the syllabus.
