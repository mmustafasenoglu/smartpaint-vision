# Experiment — BASELINE-01

## Purpose and Scope

Determine whether meaningful visual-class signal exists before expanding the dataset.

Primary question: **Do the current five visual classes contain enough learnable signal to justify scaling the dataset?**

This is a pilot signal-detection experiment for visual classification. It is not a production model and does not measure wet-film thickness (WFT), microns, or physical paint thickness.

## Setup

| Field | Value |
|-------|-------|
| Experiment ID | BASELINE-01 |
| Date | 2026-09-19 |
| Dataset version | dataset-pilot-v1 |
| Model | PLATFORM_SELECTION_REQUIRED — small pretrained lightweight classifier |
| Task | 5-class image classification |
| Input size | 224 |
| Epochs | Maximum 60; early stopping enabled if supported |
| Batch size | Auto if supported |
| Optimizer | AdamW if supported |
| Learning rate | 0.0003 if configurable |
| Weight decay | 0.0001 if configurable |
| Train images | 34 |
| Validation images | 8 |
| Test images | 8 — final holdout only |

Actual platform settings must be confirmed from the platform UI. If an exact setting is unavailable, record the nearest available platform setting; do not claim unsupported features.

## Dataset and Split Controls

- Classes: `uniform_finish`, `patchy_undercoverage`, `drip_sag_overwet`, `wet_reflective_hard_negative`, and `real_painting_context`.
- Use only train and validation during model development.
- Do not use the test set for training, early stopping, model selection, hyperparameter adjustment, or augmentation decisions.
- Use the eight-image test set once, only after the BASELINE-01 configuration is frozen.
- Do not modify labels, images, or split assignments.

## Model Selection Rule

Select a small pretrained image classifier and use transfer learning. Prefer a Nano, Mobile, or other lightweight architecture available in the platform UI. Do not use a large foundation model, segmentation model, or object detector.

The concrete model remains `PLATFORM_SELECTION_REQUIRED` until the platform model list is inspected.

## Augmentation Plan

Use only mild, realistic augmentation on the training split:

- Small horizontal flip where semantically safe.
- Small crop or scale variation.
- Mild brightness, contrast, and saturation variation.
- Very small rotation.

Avoid extreme hue shifts, heavy blur, vertical flips, strong geometric distortion, aggressive CutMix/MixUp, and synthetic defects. Color, gloss, texture, drips, and patchiness are core signals and should not be destroyed by augmentation.

Do not augment or oversample validation or test data.

## Class Imbalance

The dataset is very small and imbalanced. In particular, `wet_reflective_hard_negative` has only five samples across all splits. Class weighting is **OPTIONAL / PLATFORM DEPENDENT** and must not be fabricated before platform support is inspected.

## Critical Evaluation Targets

1. **`uniform_finish` vs `patchy_undercoverage`:** evaluate the main coverage-quality distinction.
2. **`drip_sag_overwet` vs `wet_reflective_hard_negative`:** test whether the model learns drip/sag appearance rather than the shortcut “shiny = wet defect.”
3. **`real_painting_context`:** inspect whether painter, roller, or scene context is being used as a shortcut instead of wall-finish characteristics.

## Metrics

Leave all values blank until training and the relevant evaluation stage are complete.

| Metric | Validation | Test |
|--------|------------|------|
| Accuracy | | |
| Macro precision | | |
| Macro recall | | |
| Macro F1 | | |

Test metrics from only eight images have **high statistical uncertainty** and must not be used for production-performance claims.

## Per-Class Results

### Validation

| Class | Precision | Recall | F1 | Support |
|-------|-----------|--------|----|---------|
| uniform_finish | | | | |
| patchy_undercoverage | | | | |
| drip_sag_overwet | | | | |
| wet_reflective_hard_negative | | | | |
| real_painting_context | | | | |

### Test — Final Holdout

| Class | Precision | Recall | F1 | Support |
|-------|-----------|--------|----|---------|
| uniform_finish | | | | |
| patchy_undercoverage | | | | |
| drip_sag_overwet | | | | |
| wet_reflective_hard_negative | | | | |
| real_painting_context | | | | |

## Confusion Matrices

### Validation

```text
              pred:uni  pred:pat  pred:dri  pred:wet  pred:ctx
true:uni
true:pat
true:dri
true:wet
true:ctx
```

### Test — Final Holdout

```text
              pred:uni  pred:pat  pred:dri  pred:wet  pred:ctx
true:uni
true:pat
true:dri
true:wet
true:ctx
```

## Incorrect Classifications

Record every incorrectly classified image by filename.

### Validation

| Filename | True class | Predicted class | Confidence/score if available | Notes |
|----------|------------|-----------------|-------------------------------|-------|
| | | | | |

### Test — Final Holdout

| Filename | True class | Predicted class | Confidence/score if available | Notes |
|----------|------------|-----------------|-------------------------------|-------|
| | | | | |

## Observations



## Failure Analysis

For every incorrect prediction, assign one or more categories: ambiguous label, source/domain bias, color shortcut, texture shortcut, painting-context shortcut, reflection shortcut, insufficient class examples, or true model failure.

| Filename | Failure category or categories | Analysis |
|----------|--------------------------------|----------|
| | | |

## Decision

Do not select a decision before training. Do not introduce an arbitrary numerical accuracy threshold; judge whether meaningful class signal exists.

- [ ] KEEP — clear signal exists; proceed toward a larger dataset.
- [ ] ITERATE — some signal exists, but the dataset or class definitions require improvement.
- [ ] REJECT — the current five-class formulation does not provide useful separability.

## Next Action

Configure BASELINE-01 manually in the government training platform, confirm the actual supported settings, and record them here. Stop before launching training until the configuration has been reviewed and frozen.
