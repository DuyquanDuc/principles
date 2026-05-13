---
title: "Meta (Facebook) Segment Anything Model (SAM)"
subtitle: "Foundation model for promptable segmentation"
---

## 1) What is SAM?

- **Segment Anything Model (SAM)**: a promptable vision model that returns **object masks** from an image
- Prompts can be **points**, **boxes**, or **text** (via integrations / pipelines)
- Goal: make segmentation **general-purpose**, like “the segmentation equivalent of a foundation model”

**Speaker notes**
- Think “select anything in an image” with minimal task-specific training.

---

## 2) Why it mattered (2023 → now)

- Traditional segmentation: dataset + class definitions + retraining per domain
- SAM reframes segmentation as a **prompting problem**
- Enables fast annotation, interactive editing, and downstream pipelines

**Speaker notes**
- Emphasize speed: humans provide sparse cues; model does the heavy lifting.

---

## 3) The core idea: promptable masks

- Input: image + prompt(s)
- Output: one or more candidate masks + confidence/quality scores
- Works for **unknown categories** (not limited to a fixed label set)

**Speaker notes**
- Distinguish “mask generation” from “classification”; SAM is about shapes/regions.

---

## 4) High-level architecture (3 parts)

- **Image encoder**: produces an image embedding (expensive, done once per image)
- **Prompt encoder**: embeds points/boxes (cheap, per interaction)
- **Mask decoder**: predicts masks quickly from embeddings

**Speaker notes**
- Design supports interactive use: compute image embedding once, then iterate prompts.

---

## 5) Interaction loop (UX)

- User clicks a point on the object (positive) and/or background (negative)
- User can drag a box to constrain region
- Model returns mask; user refines with additional clicks

**Speaker notes**
- This is why SAM feels “magical”: tight feedback loop.

---

## 6) Data + training: SA-1B (at a glance)

- SA-1B: very large segmentation dataset used to train SAM
- Mix of **automatic + human-in-the-loop** mask generation and filtering
- Designed to cover broad visual diversity

**Speaker notes**
- Keep numbers light unless asked; focus on “scale + diversity + iterative labeling”.

---

## 7) What SAM is great at

- **Zero-shot** object mask proposals from minimal prompts
- **Annotation acceleration** (labeling tools, dataset creation)
- **Preprocessing** for downstream tasks (tracking, editing, compositing)

**Speaker notes**
- Many orgs use SAM as a “mask generator” component, not an end-to-end solution.

---

## 8) Limitations / gotchas

- May struggle with **fine structures** (hair, thin wires), heavy occlusion, tiny objects
- Prompt ambiguity → multiple plausible masks
- Not inherently “semantic”: mask ≠ class label

**Speaker notes**
- Set expectation: it’s a strong general tool, not perfect segmentation for every domain.

---

## 9) Practical patterns (how teams use it)

- **Interactive labeling**: SAM-assisted annotation UI
- **Auto-mask proposals**: generate candidate masks, humans accept/reject
- **Hybrid**: SAM masks + lightweight classifier for labels

**Speaker notes**
- Highlight the common combo: SAM for geometry; another model for semantics.

---

## 10) Evaluation (what “good” looks like)

- Mask quality (IoU / boundary metrics) vs prompt budget (clicks)
- Latency: time-to-first-mask + time-per-refinement
- Human effort saved: minutes per image → seconds

**Speaker notes**
- In business terms: “annotation throughput” and “time saved” matter most.

---

## 11) Demo story you can tell (no code)

- Show an image with 3 objects
- Click 1 point per object → show masks
- Add 1 negative point to fix spillover
- Box prompt to isolate a crowded region

**Speaker notes**
- This is a great live demo flow for stakeholders.

---

## 12) Where it’s going (SAM 2 and beyond)

- Extend from images to **video** (temporal consistency, object tracking)
- Better prompts, better small-object performance, faster runtimes
- Productization: editing, AR, robotics, labeling, search

**Speaker notes**
- Keep forward-looking: “promptable segmentation becomes a standard primitive.”

