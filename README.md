# PPE Compliance Detector

**Project Name:** PPE Compliance Detector
**Team Members:** Huy Nguyen & Raymond Newton
**Course:** ITAI 1378 — Final Project Submission

---

## Status: Complete ✅

Model trained, evaluated, and demoed. Final mAP@0.5: **90.0%** (target was ≥75–80%).

---

## Tier Selection

**Tier 1** — a pretrained model (YOLOv8n) fine-tuned on an existing public labeled dataset, no custom data collection or novel architecture required.

**Justification:** The project fine-tunes an off-the-shelf object detection model on a public Roboflow dataset already annotated in YOLO format. This kept scope realistic for the timeline while still requiring real training, evaluation, and a working demo — appropriate for a Tier 1 submission.

---

## Problem Statement

Home health and personal care agencies are expected to verify that caregivers wear required PPE (masks, gloves) during certain visits, but compliance is currently tracked through self-reporting or occasional manual supervisor spot-checks. This does not scale across a large caregiver workforce and creates documentation gaps during infection-control audits. Automating PPE verification from a photo gives agencies a fast, consistent way to confirm compliance without adding to supervisors' workload.

## Solution Overview

An object detection system that takes a photo of a caregiver and automatically identifies whether they are wearing a mask, flagging the result as compliant or non-compliant. A YOLOv8-based detector scans an image and outputs bounding boxes plus a compliance flag.

---

## Technical Approach

- **Technique:** Object detection (not classification) — bounding boxes localize *where* PPE is present or missing, rather than a single whole-image label.
- **Model:** YOLOv8n (nano), via the Ultralytics library.
- **Framework:** Ultralytics YOLOv8 (built on PyTorch).
- **Justification:** YOLOv8n is fast to fine-tune on free GPU compute, has strong community tooling for PPE-style datasets, and runs fast enough to demo in real time.

---

## Dataset Plan

- **Source:** Public dataset from Roboflow Universe — "Mask-Detection-YOLOv8" by AGH.
  Link: https://universe.roboflow.com/agh-ett2f/mask-detection-yolov8
- **Size:** 4,547 labeled images (train/valid/test split).
- **Labels:** 3 classes — `with_mask`, `without_mask`, `incorrectly_worn_mask`. Core deliverable used `with_mask` / `without_mask`.
- **Preparation:** No manual labeling needed — dataset shipped pre-annotated in YOLOv8 format, exported directly via the Roboflow Python package. Standard Ultralytics augmentation (flip, mosaic, brightness) applied at train time.

---

## Final Results

Trained for 75 epochs on a Colab T4 GPU (~76.4 minutes total).

| Metric | Best Epoch (64) | Final Epoch (75) | Target |
|---|---|---|---|
| mAP@0.5 | **90.5%** | 90.0% | ≥ 75–80% ✅ |
| mAP@0.5:0.95 | 61.2% | 60.8% | — |
| Precision | 92.1% | 93.4% | — |
| Recall | 84.4% | 82.5% | — |

Full per-epoch log, training curve chart, and demo screenshots are in [`results/`](./results).

Reference point: a comparable model trained on this same dataset publicly reports ~91% mAP@50, ~93% precision, ~85% recall — our result lines up closely with that benchmark.

---

## Live Demo

Built with [Gradio](https://gradio.app) — upload a caregiver photo, get back an annotated detection image and a compliant/non-compliant flag. See `notebooks/PPE_Compliance_Detector_Colab.ipynb`, Section 10, for the interface code (`demo.launch(share=True)`).

Sample outputs:
- `results/demo_non_compliant_1.png` — mask missing, flagged correctly (0.87 confidence)
- `results/demo_non_compliant_2.png` — mask missing, flagged correctly (0.90 confidence)
- `results/demo_compliant.png` — two people, both masked, flagged correctly (0.84 / 0.83 confidence)

**Demo Video:** *[add YouTube (Unlisted) or Google Drive link here before submitting]*

---

## Week-by-Week Plan (Completed)

| Week | Task | Outcome |
|---|---|---|
| 1 | Dataset + environment setup | ✅ Complete |
| 2 | Sanity-check training run | ✅ Complete |
| 3 | Full training run (75 epochs), evaluate mAP | ✅ 90.0% mAP@0.5 |
| 4 | Build demo | ✅ Gradio interface live |
| 5 | Final testing, documentation, slides | ✅ Complete |
| 6 | Present project | 🎉 Presentation day |

---

## Resources Used

| Resource | Notes |
|---|---|
| Compute | Google Colab (free T4 GPU) — 76.4 min total training time |
| Frameworks | Ultralytics YOLOv8, PyTorch, Roboflow (dataset export), Gradio (demo UI) |
| Total Cost | $0 — free tiers covered the entire project |

---

## Challenges & How We Handled Them

| Challenge | Resolution |
|---|---|
| Full 75-epoch run took ~76 minutes | Used checkpointing (`save_period=10`) so progress was never lost to a Colab disconnect |
| Domain mismatch (dataset ≠ real home-visit conditions) | Accepted as a known limitation — can't use real patient photos for privacy reasons |
| Confirming model quality wasn't a fluke | Cross-checked our 90% mAP against a published benchmark on the same dataset (~91%) |
| Turning raw detections into a usable signal | Built a compliance-flag function on top of raw YOLO output, wrapped in a Gradio UI for a real interactive demo |

---

## AI Usage Log

See [`docs/AI_usage_log.md`](./docs/AI_usage_log.md) for the full log of AI tool usage throughout this project.

---

## Repo Structure

```
ITAI1378_Midterm_PPEComplianceDetector/
├── README.md                       ← you are here
├── requirements.txt                ← Python packages
├── notebooks/
│   └── PPE_Compliance_Detector_Colab.ipynb   ← full pipeline: data, training, eval, Gradio demo
├── data/
│   └── README.md                   ← dataset info and download instructions
├── results/
│   ├── README.md                   ← results summary
│   ├── results.csv                 ← full per-epoch training log
│   ├── training_curve.png          ← mAP/precision/recall chart
│   ├── demo_non_compliant_1.png    ← Gradio demo screenshot
│   ├── demo_non_compliant_2.png    ← Gradio demo screenshot
│   └── demo_compliant.png          ← Gradio demo screenshot
└── docs/
    ├── presentation.pdf            ← final presentation slides
    ├── presentation.pptx           ← editable version
    ├── proposal.pdf                ← original proposal slides
    └── AI_usage_log.md             ← AI tool usage log
```
