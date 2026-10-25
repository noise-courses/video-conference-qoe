# Assignment 2 (take-home midterm): Video Conferencing QoE Inference

Infer per-participant video frame rate from a packet trace of a three-person
Microsoft Teams call. The notebook `video-conference-qoe-clean.ipynb` walks
through it: identify the call architecture (peer-to-peer vs. SFU), separate
the participants' video streams by SSRC, build per-second network-layer
features, align them with the ground-truth frame rates, and train a model with
a temporal train/test split, reporting mean absolute error per participant.
The trace is in `data/teams.csv`.

**This is individual work.** No collaboration with other students. Any tools
are fine, including AI tools (acknowledge them in the notebook); the TAs will
discuss concepts but not give answers.

**Submission.** Copy the notebook into your private course repository (the one
`feamster` and the TAs are collaborators on), complete it, run it end to end so
the outputs are saved, and push. Grading is from that repository against
[`RUBRIC.md`](RUBRIC.md). Due date and time are on the course dates sheet.
