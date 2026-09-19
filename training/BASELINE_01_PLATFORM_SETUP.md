# BASELINE-01 Platform Setup

## Experiment

| Field | Value |
|-------|-------|
| Experiment | BASELINE-01 |
| Task | Classification |
| Dataset | dataset-pilot-v1 |
| Classes | 5 |
| Train / validation / test | 34 / 8 / 8 |

This is a pilot signal-detection experiment for visual classification, not a production model. It does not measure WFT, microns, or physical paint thickness.

## Upload Package

Upload the structured dataset from `training/platform_upload/baseline_01/` or use `training/platform_upload/smartpaint_baseline_01.zip`. The package contains only class-organized images in `train`, `val`, and `test`.

Preserve the supplied splits. The eight test images are the final holdout and must not be used during training or configuration selection.

## Recommended Initial Settings

| Setting | Requested value |
|---------|-----------------|
| Model | Pretrained lightweight image classifier; Nano/Mobile preferred |
| Input size | 224 |
| Maximum epochs | 60 |
| Early stopping | Enabled |
| Patience | 15 |
| Optimizer | AdamW if available |
| Learning rate | 3e-4 if configurable |
| Weight decay | 1e-4 if configurable |
| Batch size | Auto if available |
| Class weighting | Optional / platform dependent |

**ACTUAL PLATFORM SETTINGS MUST BE CONFIRMED FROM THE PLATFORM UI.** Do not assume a model or feature exists. If an exact setting is unavailable, choose the nearest suitable available setting manually and record the actual value below.

## Mild Augmentation Only

If separately configurable, allow small horizontal flips where semantically safe, small crop/scale changes, mild brightness/contrast/saturation changes, and very small rotations.

Do not use extreme hue shifts, heavy blur, vertical flips, strong geometric distortion, aggressive CutMix/MixUp, or synthetic defects. Do not augment or oversample validation or test images.

## Platform Settings Record

Complete this table from the UI before launching training.

| Setting | Actual platform value | Exact or nearest available? | Notes |
|---------|-----------------------|-----------------------------|-------|
| Model | | | |
| Pretrained/transfer learning | | | |
| Input size | | | |
| Maximum epochs | | | |
| Early stopping | | | |
| Patience | | | |
| Optimizer | | | |
| Learning rate | | | |
| Weight decay | | | |
| Batch size | | | |
| Class weighting | | | |
| Augmentation | | | |

## Pre-Launch Checklist

- [ ] Confirm a small pretrained classifier from the platform's actual model list.
- [ ] Confirm train, validation, and test counts are 34, 8, and 8.
- [ ] Confirm the five expected class names.
- [ ] Confirm test is excluded from training, early stopping, model selection, hyperparameter adjustment, and augmentation decisions.
- [ ] Record all actual platform settings above.
- [ ] Freeze the BASELINE-01 configuration before using the test set.
- [ ] Do not launch training until the configuration review is complete.

## Required Evaluation Output After Training

Capture the confusion matrix; macro precision, recall, and F1; per-class precision, recall, F1, and support; and every incorrect validation/test prediction by filename. Treat eight-image test metrics as having high statistical uncertainty and make no production-performance claims.
