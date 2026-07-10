# PPE Compliance Detector

**Project Name:** PPE Compliance Detector

**Team Members:** Huy Nguyen & Raymond Newton

**Course:** ITAI 1378 — Midterm Project

---

## Tier Selection

**Tier 1** — using a pretrained model (YOLOv8n) fine-tuned on an existing public labeled dataset, no custom data collection or novel architecture required.

**Justification:** The project fine-tunes an off-the-shelf object detection model on a public Roboflow dataset that is already annotated in YOLO format. This keeps scope realistic for the timeline (no manual labeling, no model architecture design) while still requiring real training, evaluation, and a working demo — appropriate for a Tier 1 midterm submission.

---

## Problem Statement

Home health and personal care agencies are expected to verify that caregivers wear required PPE (masks, gloves) during certain visits, but compliance is currently tracked through self-reporting or occasional manual supervisor spot-checks. This does not scale across a large caregiver workforce and creates documentation gaps during infection-control audits. Automating PPE verification from a photo would give agencies a fast, consistent way to confirm compliance without adding to supervisors' workload.

## Solution Overview

This project builds an object detection system that takes a photo of a caregiver and automatically identifies whether they are wearing a mask (and optionally gloves), flagging the result as compliant or non-compliant. In one sentence: a YOLOv8-based detector that scans an image and outputs bounding boxes plus a compliance flag for required PPE.

---

## Technical Approach

- **Technique:** Object detection (not classification) — bounding boxes are needed to localize *where* PPE is present or missing, rather than a single whole-image label.
- **Model:** YOLOv8n (nano) as the baseline, via the Ultralytics library. YOLOv8s (small) will be tested as a stretch comparison if training time allows, to evaluate the accuracy/speed tradeoff.
- **Framework:** Ultralytics YOLOv8 (built on PyTorch).
- **Justification:** YOLOv8n is fast to fine-tune on free GPU compute, has strong community tooling for PPE-style datasets, and its speed makes it realistic to demo in near real-time — appropriate for the project's timeline and resources.

---

## Dataset Plan

- **Source:** Public dataset from Roboflow Universe — "Mask-Detection-YOLOv8" by AGH.
  Link: https://universe.roboflow.com/agh-ett2f/mask-detection-yolov8
- **Size:** 4,547 images (pre-split train/valid/test; exact split sizes to be confirmed on export).
- **Labels:** 3 classes — `with_mask`, `without_mask`, `incorrectly_worn_mask`. Project will focus primarily on `with_mask` / `without_mask` as the core two-class deliverable, with the third class as a stretch goal.
- **Preparation:** No manual labeling needed — dataset is already annotated and exportable directly in YOLOv8 format via the Roboflow Python package. Standard train-time augmentation (flip, brightness, mosaic) will be applied through Ultralytics defaults.

---

## Metrics

| Metric Type | Metric | Target |
|---|---|---|
| Primary | mAP@0.5 | ≥ 0.75–0.80 |
| Secondary | Inference speed | < 0.5s per image (Colab T4 GPU) |

Reference point: a similar model trained on this same dataset publicly reports ~91% mAP@50, ~93% precision, ~85% recall, which supports the feasibility of the target above.

---

## Week-by-Week Plan

| Week | Task | Milestone |
|---|---|---|
| 1 | Fork/export Roboflow dataset, set up Colab + Ultralytics environment | Dataset ready in YOLO format, environment runs |
| 2 | Quick sanity-check training run (10–15 epochs) to confirm pipeline works | Baseline model trains without errors |
| 3 | Full training run (50–100 epochs), evaluate mAP, tune augmentation/thresholds | Model meets target mAP |
| 4 | Build demo script/notebook for inference on new images (optionally webcam) | Working demo |
| 5 | Final testing, documentation, slides, rehearse presentation | Submission-ready |
| 6 | Present project | 🎉 Presentation day |

---

## Resources Needed

| Resource | Options / Notes |
|---|---|
| Compute | Google Colab (free T4 GPU), Kaggle Notebooks as backup (longer session limits) |
| Frameworks | Ultralytics YOLOv8, PyTorch (underlying), Roboflow (dataset export) |
| Estimated Cost | $0 — Colab free tier + Roboflow free tier fully cover this project |

---

## Risks & Mitigation

| Risk | Probability | Mitigation |
|---|---|---|
| Class imbalance (uneven mask/no-mask counts) | Medium | Apply data augmentation; consider class-weighted loss if needed |
| Domain mismatch (dataset photos ≠ real home-visit conditions) | Medium | Acknowledge as a known limitation in final report; cannot use real patient photos due to privacy |
| Low mAP on full training run | Medium | Increase epochs, try YOLOv8s instead of YOLOv8n, add augmentation |
| Colab GPU unavailable / session timeout | Medium | Save checkpoints (`save_period`) regularly; fall back to Kaggle Notebooks (30 hrs/week free GPU) |
| Missing/incomplete dataset annotations | Low | Dataset is pre-labeled and validated on Roboflow; fallback is switching to an alternate public mask dataset (several available) |
| Running out of time before demo is ready | Medium | Build demo incrementally starting Week 3, not left until Week 4 only |

---

## AI Usage Log

| Date | Tool | How it was used |
|---|---|---|
| *(update as you go)* | Claude | Helped scope project idea, select model/dataset, draft README structure, and outline presentation content |

*(Keep updating this table throughout the project with any AI tool used and how.)*

---

## Repo Structure

```
ITAI1378_Midterm_PPEComplianceDetector/
├── README.md              ← you are here
├── requirements.txt       ← Python packages
├── notebooks/
│   └── 01_exploration.ipynb   ← initial experiments / dataset exploration
├── data/
│   └── README.md          ← dataset info and download instructions
└── docs/
    └── proposal.pdf        ← presentation slides
```
