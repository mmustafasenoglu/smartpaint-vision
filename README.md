# SmartPaint Vision

Computer-vision-assisted painting system for visual wall coating analysis.

## Repository

SmartPaint Vision is the official development repository for SmartPaint-Edge's Vision Mode — a phone-only camera-based wall finish analysis system.

This repository contains:

- **Versioned dataset** — curated training/validation/test images with verified licenses
- **Training** — baseline classification experiments and configs
- **Application** — Flutter-based Vision Mode (Phase 1)
- **Documentation** — architecture, dataset notes, attribution

## Vision Mode (Phase 1)

Vision Mode works without any ESP32 hardware. It uses the phone camera to analyze visual wall coating appearance and produces:

- **Visual Coverage Score** (0–100)
- **Heatmap** of coverage distribution
- **Correction map** for rework guidance

Vision Mode does **not** measure actual paint thickness or WFT. All outputs are visual appearance analysis.

## Roadmap

| Phase | Name | Description |
|-------|------|-------------|
| 1 | **Vision Mode** | Phone camera only. Visual Coverage Score, heatmap, correction map. |
| 2 | **Edge Demo** | Vision Mode + ESP32 clip-on (ToF + IMU + trigger sensor). Estimated WFT. |
| 3 | **Product** | Productized clip-on SmartPaint Edge hardware. |
| Future | **Edge Control** | Closed-loop spray control system. |

## Dataset

Current dataset: `dataset/pilot_v1/` — 50 images, 5 classes, session-aware split.

See [docs/dataset_v1_notes.md](docs/dataset_v1_notes.md) for details.

### Dataset Licensing

Dataset images retain their original licenses and attribution requirements. A software license (if any) for this repository does **not** apply to the dataset images themselves.

All licensing and attribution records are maintained in:

- `dataset/pilot_v1/metadata.csv` — per-image license, author, source URL, SHA-256
- `dataset/pilot_v1/ATTRIBUTION.md` — overview of licensing approach

## Project Structure

```
smartpaint-vision/
├── dataset/pilot_v1/     # Versioned dataset (train/val/test + metadata)
├── training/             # Baseline experiments and configs
├── app/                  # Flutter Vision Mode application
└── docs/                 # Dataset notes, architecture
```

## Status

Current phase: **Vision Mode / Phase 1 — Dataset Collection & Baseline Training**

First baseline classification model is planned but not yet trained.
