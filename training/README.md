# Training

Baseline classification experiments for SmartPaint-Edge Vision Mode.

## Goal

Check whether the five visual classes contain learnable signal for wall coating appearance analysis.

This is **not** production training. The pilot dataset is 50 images.

## Dataset

`dataset/pilot_v1/` — 50 images, 5 classes, session-aware train/val/test split.

| Split | Count |
|-------|-------|
| train | 34 |
| val | 8 |
| test | 8 |

## Planned Metrics

- Confusion matrix
- Per-class precision, recall, F1
- False negatives
- Class confusion analysis

## Critical Comparisons

| Comparison | Why |
|-----------|-----|
| uniform_finish vs patchy_undercoverage | Core use case: even vs uneven coverage |
| drip_sag_overwet vs wet_reflective_hard_negative | Hard negative disambiguation: real drip vs wet-but-not-defect |

## Current Status

- [ ] Baseline-01: Classification model (planned)
- [ ] Dataset scaling to 200 images
- [ ] SmartPaint-specific image collection

## Experiment Log

See `experiments/` for individual experiment records.
