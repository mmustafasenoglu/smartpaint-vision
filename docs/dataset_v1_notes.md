# Dataset — SmartPaint Pilot v1

## Overview

- **Name**: SmartPaint Pilot v1
- **Version**: `pilot_v1`
- **Images**: 50
- **Classes**: 5
- **Split**: train / val / test (source/session-aware)
- **Status**: Bootstrap/pilot dataset. Passed quality audit and cleanup.

## Class Distribution

| Class | Count |
|-------|-------|
| uniform_finish | 12 |
| patchy_undercoverage | 15 |
| drip_sag_overwet | 12 |
| wet_reflective_hard_negative | 5 |
| real_painting_context | 6 |
| **Total** | **50** |

## Split

| Split | Count | % |
|-------|-------|---|
| train | 34 | 68% |
| val | 8 | 16% |
| test | 8 | 16% |

Per-class split (approximate): 70/15/15.

## Split Methodology

- **Source-aware**: Multiple images from the same photographer/session are forced into the same split to prevent data leakage.
- **Session groups identified**: Dean Hochman drip pair (drip_009+drip_011), Hashtee sag pair (drip_002+drip_003), hashtee uniform frames (retired — only uniform_001 remains).
- **Leakage check**: Programmatic verification confirmed zero cross-split session groups.
- **SHA uniqueness**: All 50 images verified unique (no duplicates).

## Labels

Labels describe **visual appearance**, not physical paint properties:

| Label | Meaning |
|-------|---------|
| uniform_finish | Even, complete coverage; no visible defects |
| patchy_undercoverage | Uneven coverage, visible substrate, thin areas |
| drip_sag_overwet | Drips, runs, sags from over-application |
| wet_reflective_hard_negative | Wet/reflective surface that is NOT a painting defect |
| real_painting_context | Real painting scene (context, not defect target) |

Labels are **not** WFT ground truth. They do not encode micron measurements, wet film thickness, or physical paint properties.

## Known Limitations

- **Small dataset** — 50 images is insufficient for production training. This is a bootstrap/pilot.
- **Source bias** — images are sourced from the internet, not controlled SmartPaint-specific data collection. Some photographer/session clustering remains.
- **Wet-negative class** — only 5 images. Needs expansion at 200-scale.
- **Drip class ambiguity** — drip_002/003 have blister-vs-sag ambiguity; drip_008 has graffiti background (shortcut risk).
- **No controlled percentages** — internet images do not provide controlled coverage percentages.
- **Color-class correlation** — reduced after cleanup (red brick uniform added) but not fully eliminated.

## Future Collection

At 200-scale, collect SmartPaint-specific images with:

- Controlled lighting
- Known coverage percentages (for regression tasks)
- More wet-negative wall-scale images
- Diverse wall substrates
- Edge-case scenarios (partial coverage, mixed defects)

## Files

```
dataset/pilot_v1/
├── train/                  # 34 images
├── val/                    # 8 images
├── test/                   # 8 images
├── metadata.csv            # Per-image: license, author, source, SHA-256
├── split_manifest.csv      # 50-row split manifest
├── ATTRIBUTION.md          # License overview
├── CLEANUP_REPORT.md       # Cleanup/replacement log
└── contact_sheet_ready.jpg # Visual overview of all 50 images
```
