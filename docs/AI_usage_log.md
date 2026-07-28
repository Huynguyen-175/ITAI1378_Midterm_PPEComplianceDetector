# AI Usage Log

Record of AI tool usage throughout this project, per course requirements. Tool used: **Claude** (Anthropic).

| # | Date | Tool | How It Was Used |
|---|---|---|---|
| 1 | Project scoping | Claude | Brainstormed project topic options (including face recognition vs. PPE detection), compared feasibility/privacy tradeoffs, and helped scope the project down to a Tier 1, timeline-realistic idea. |
| 2 | Project scoping | Claude | Selected model (YOLOv8n via Ultralytics) and dataset (Roboflow "Mask-Detection-YOLOv8," 4,547 images) with justification for both choices. |
| 3 | Presentation prep | Claude | Drafted an in-class spoken script for the proposal presentation, then trimmed it down to a shorter version for time constraints. |
| 4 | Repo setup | Claude | Generated initial GitHub repository structure (README.md, requirements.txt, notebooks/, data/README.md, docs/) matching the course's required layout. |
| 5 | Notebook development | Claude | Built the full Colab training notebook (`PPE_Compliance_Detector_Colab.ipynb`) covering dataset download, training, evaluation, and inference demo steps. |
| 6 | Notebook development | Claude | Explained the role of the `patience` (early stopping) parameter vs. epoch count in controlling actual training time. |
| 7 | Demo development | Claude | Added a Gradio web-interface cell to the notebook, wrapping the trained model and compliance-flag logic into an interactive upload-and-detect UI for demoing. |
| 8 | Results analysis | Claude | Parsed the real `results.csv` training log to identify best-epoch vs. final-epoch metrics (90.5% / 90.0% mAP@0.5) and generated a training-curve chart from the actual data. |
| 9 | Slide design | Claude | Built the proposal slide deck (10 slides) and later the final presentation deck (12 slides), incorporating real training metrics and demo screenshots once available. |
| 10 | Documentation | Claude | Assisted with final README updates, results/ folder documentation, and this AI usage log. |

*All technical decisions, dataset selection, model training execution, and final results are the students' own work; Claude was used as a planning, coding-assistance, and documentation tool throughout.*
