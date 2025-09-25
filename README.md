[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1ptYkebA35ejXSE1y4IZibZv2nYMmdnmY?usp=sharing)
# Inspiration & Description
This notebook demonstrates a tiny end-to-end pipeline that automates scenario taxonomy using GenAI from sample testing data in the [Waymo Motion Dataset](https://waymo.com/open/).

The goal is to replace the manual, time-consuming process of curating corner cases with an automated pipeline that parses multi-agent motion data, extracts interpretable features, and generates structured, human-readable scenario summaries. For systems and test engineering at Waymo, this matters because the space of possible driving situations is enormous (and growing!). Humans cannot hand-label or exhaustively enumerate them.  

By introducing GenAI at the summarization step, we scalably turn raw kinematics into labeled scenarios that are easy to cluster and incorporate into test design. 

Inspiration: I started this project after reading more about Waymo's [safety framework](https://waymo.com/blog/2020/10/sharing-our-safety-framework) and thinking about how scenario taxonomy might use GenAI as Waymo rapidly scales its worldwide footprint (and thus testing).

Open up ```scenarios.ipynb``` to read through the project. 

## Quick Highlighs

This prototype shows how structured GenAI outputs can not only label and summarize events at scale, but also surface edge cases and interesting scenarios.

- **Potentially dangerous tail-lapse caught**  
  Recognized a `following_too_close` event with **0.22 s headway** while the ego vehicle was moving ~13.4 m/s. Exactly the sort of split-second risk worth surfacing:  
  > *“The self vehicle, traveling at 13.43 m/s, followed another vehicle, traveling at 2.66 m/s, with a dangerously low headway of 0.22 seconds, indicating a following too close event.”*  
  **Min dist:** 9.43 m · **Headway:** 0.22 s · **Ahead frac:** 1.00  

- **Pedestrian close-call scenario surfaced**  
  A `crossing_paths` event where the ego vehicle came within ~3 m of a pedestrian, with TTC ≈ 1.8 s. A clear-cut VRU edge case that would need review:  
  > *“A stationary vehicle had a close interaction with a pedestrian who was moving and potentially crossing its path, with a minimum distance of 3.05 meters and a time-to-collision of 1.79 seconds.”*  
  **Min dist:** 3.05 m · **TTC:** 1.79 s · **Oncoming frac:** 0.55  

- **Oncoming vehicles**  
  Interactions with TTC ~3–5 s and large min distances (15–50 m). Useful for tuning alert thresholds vs. nuisance alerts.  
  Example:  
  > *“The self vehicle had an oncoming interaction with another vehicle, maintaining a minimum distance of 54.23 meters and a time to collision of 3.33 seconds.”*

- **Cyclist proximity alert**  
  `ped_or_cyclist_nearby` surfaced with ~9 m gap and headway ~0.09 s. Helps ensure cyclists aren’t missed in crowded scenes.


