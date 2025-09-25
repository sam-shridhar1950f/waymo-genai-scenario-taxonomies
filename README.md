# Inspiration & Description
This notebook demonstrates a tiny end-to-end pipeline that automates scenario taxonomy using GenAI from sample testing data in the [Waymo Motion Dataset](https://waymo.com/open/).

The goal is to replace the manual, time-consuming process of curating corner cases with an automated pipeline that parses multi-agent motion data, extracts interpretable features, and generates structured, human-readable scenario summaries. For systems and test engineering at Waymo, this matters because the space of possible driving situations is enormous (and growing!). Humans cannot hand-label or exhaustively enumerate them.  

By introducing GenAI at the summarization step, we scalably turn raw kinematics into labeled scenarios that are easy to cluster and incorporate into test design. 

Inspiration: I started this project after reading more about Waymo's [safety framework](https://waymo.com/blog/2020/10/sharing-our-safety-framework) and thinking about how scenario taxonomy might use GenAI as Waymo rapidly scales its worldwide footprint (and thus testing).

Open up ```scenarios.ipynb``` to read through the project.
