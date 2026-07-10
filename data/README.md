# Dataset Info

**Source:** Roboflow Universe — "Mask-Detection-YOLOv8" by AGH
**Link:** https://universe.roboflow.com/agh-ett2f/mask-detection-yolov8

## Overview
- **Size:** 4,547 images total (train/valid/test split provided by Roboflow export)
- **Format:** YOLOv8 (images + `.txt` label files + `data.yaml`)
- **Classes (3):**
  - `with_mask`
  - `without_mask`
  - `incorrectly_worn_mask`

Core deliverable focuses on `with_mask` / `without_mask`. `incorrectly_worn_mask` is a stretch goal if time and accuracy allow.

## How to Download

Data is not committed to this repo (too large / licensing). Download it directly from Roboflow:

```python
import roboflow

roboflow.login()

rf = roboflow.Roboflow()
project = rf.workspace("agh-ett2f").project("mask-detection-yolov8")
dataset = project.version(16).download("yolov8")  # check current version number on Roboflow page
```

This will create a local folder (e.g. `mask-detection-yolov8-16/`) containing `train/`, `valid/`, `test/` subfolders and a `data.yaml` file ready to point Ultralytics at directly.

## License
CC BY 4.0 — see the Roboflow project page for full citation details.

## Notes
- No manual labeling required; annotations are provided.
- Standard Ultralytics augmentation (flip, mosaic, brightness/contrast) will be used during training rather than a separate preprocessing step.
- If this dataset becomes unavailable, backup public alternatives include other Roboflow "face mask detection" datasets (see project proposal, Risks section).
