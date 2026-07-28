# Results

Outputs from the final YOLOv8n training run (75 epochs, Colab T4 GPU, ~76.4 min total).

| File | Description |
|---|---|
| `results.csv` | Full per-epoch training log exported by Ultralytics (loss, precision, recall, mAP@0.5, mAP@0.5:0.95, learning rate) |
| `training_curve.png` | mAP@0.5 / precision / recall plotted across all 75 epochs |
| `demo_non_compliant_1.png` | Gradio demo screenshot \u2014 caregiver without mask detected, flagged NON-COMPLIANT (confidence 0.87) |
| `demo_non_compliant_2.png` | Gradio demo screenshot \u2014 caregiver without mask detected, flagged NON-COMPLIANT (confidence 0.90) |
| `demo_compliant.png` | Gradio demo screenshot \u2014 two people both wearing masks, flagged COMPLIANT (confidence 0.84, 0.83) |

## Final Metrics (epoch 75 / best epoch 64)

| Metric | Best Epoch (64) | Final Epoch (75) | Target |
|---|---|---|---|
| mAP@0.5 | 90.5% | 90.0% | \u2265 75\u201380% \u2705 |
| mAP@0.5:0.95 | 61.2% | 60.8% | \u2014 |
| Precision | 92.1% | 93.4% | \u2014 |
| Recall | 84.4% | 82.5% | \u2014 |

Trained weights (`best.pt`) are saved to Google Drive per the notebook's save step, not committed to this repo (binary model file, kept out of version control).
