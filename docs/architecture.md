# SmartPaint-Edge — Architecture

## Overview

SmartPaint-Edge is a computer-vision-assisted painting system with three progressive phases.

---

## Phase 1 — Vision Mode

Phone camera only. No hardware required.

```
┌──────────────────────────────────────────────┐
│              Phone Camera Input              │
└──────────────────┬───────────────────────────┘
                   │
          ┌────────▼────────┐
          │  Baseline Ref   │  (reference image or default)
          │  Optimal Ref    │  (target appearance)
          └────────┬────────┘
                   │
          ┌────────▼────────┐
          │  Visual Analysis │  CNN / feature extraction
          └────────┬────────┘
                   │
          ┌────────▼────────┐
          │    Wall Grid     │  Spatial subdivision
          └────────┬────────┘
                   │
          ┌────────▼─────────────┐
          │  Visual Coverage     │
          │  Score (0–100)       │
          └────────┬─────────────┘
                   │
          ┌────────▼────────┐
          │    Heatmap       │  Per-region coverage visualization
          └────────┬────────┘
                   │
          ┌────────▼────────────┐
          │  Correction Map     │  Rework guidance
          └─────────────────────┘
```

**Key distinction**: All outputs are **visual appearance analysis**. Vision Mode does not measure actual paint thickness, WFT, or microns.

---

## Phase 2 — Edge Demo

Vision Mode + ESP32 clip-on sensor hardware.

```
┌──────────────────────────────────────────────┐
│              Vision Mode (Phase 1)           │
└──────────────────┬───────────────────────────┘
                   │
          ┌────────▼────────┐
          │  ESP32 + Sensors │
          │  ├─ ToF sensor   │  (distance to surface)
          │  ├─ IMU          │  (motion/orientation)
          │  └─ Trigger      │  (spray detection)
          └────────┬────────┘
                   │
          ┌────────▼────────┐
          │  Gun Profile     │  Spray gun characteristics
          └────────┬────────┘
                   │
          ┌────────▼────────┐
          │  Spray Kernel    │  Spray pattern model
          └────────┬────────┘
                   │
          ┌────────▼────────┐
          │  Estimated WFT   │  Wet Film Thickness (estimated)
          └─────────────────┘
```

**Key distinction**: Phase 2 produces **estimated WFT** — a model-based estimate, not a direct measurement. Estimated WFT is derived from sensor fusion (visual + distance + motion), not a calibrated instrument reading.

---

## Phase 3 — Product

Productized clip-on SmartPaint Edge.

- Integrated hardware design
- Calibration for production spray guns
- Field-validated estimated WFT
- Production-ready mobile application

---

## Future — SmartPaint Edge Control

Closed-loop spray control:

```
Sensor Input → Estimated WFT → Control Logic → Spray Gun Actuation
```

Fully autonomous paint application with real-time feedback control.

---

## Terminology

| Term | Definition |
|------|-----------|
| **Visual Coverage** | Visual appearance of paint coverage (how complete/even it looks) |
| **Visual Coverage Score** | 0–100 score based on visual analysis |
| **Estimated WFT** | Model-based wet film thickness estimate from sensor fusion (Phase 2+) |
| **Actual WFT** | Physically measured wet film thickness (requires instrument) |

Vision Mode (Phase 1) produces **Visual Coverage** only. It does not produce Estimated WFT or Actual WFT.
