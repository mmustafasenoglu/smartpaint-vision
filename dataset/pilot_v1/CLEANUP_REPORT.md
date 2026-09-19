# Cleanup Report — SmartPaint Pilot 50 → Ready

Minor cleanup for first baseline training. Originals preserved in
`smartpaint_pilot_50/replaced_originals/`; audit CSVs frozen as record.

## 1. Images replaced (5/50, within 7 budget; optional drip cleanup skipped)

| slot | old → new | reason |
|---|---|---|
| drip_006 | primed plywood → pink paint drips w/ droplets on wall (Roboflow chew-poh-yee, CC BY 4.0, Chew Poh Yee) | old was not a wall (audit CRITICAL) |
| uniform_002 | hashtee video frame → White Stucco Wall (Flickr shaire productions, CC BY 2.0) | session-leakage cleanup; white/light pick |
| uniform_003 | hashtee video frame → Red Painted Brick Wall (Flickr shaire productions, CC BY 2.0) | session-leakage cleanup; colored pick |
| wetneg_002 | droplet macro → dual-head shower, glossy tiles (Flickr andrechinn, CC BY 2.0) | domain-matched hard negative |
| wetneg_005 | rain-water surface → blue mosaic tile wall (Flickr Mr Thinktank, CC BY 2.0) | domain-matched hard negative |

uniform_001 kept as the best of the beige session (cleanest framing).
drip_002/003/008 kept (audit: useful signals, no unnecessary churn).

Known caveat: new drip_006 is 612px on the short side (below preferred
640). Accepted because it passes every strict replacement requirement
(wall primary, real drips, CC BY 4.0 priority source, no graffiti) — the
alternative candidates all failed a hard requirement.

## 2. Replacement sources

- Roboflow Universe chew-poh-yee/internal-wall-finishing-defects (CC BY 4.0):
  https://universe.roboflow.com/chew-poh-yee/internal-wall-finishing-defects
- Openverse-indexed Flickr, each CC BY 2.0 with landing page in metadata:
  White Stucco Wall / Red Painted Brick Wall (shaire productions),
  dual-head shower (andrechinn), tiled wall (Mr Thinktank).

## 3. Final class counts (unchanged)

uniform_finish 12 / patchy_undercoverage 15 / drip_sag_overwet 12 /
wet_reflective_hard_negative 5 / real_painting_context 6 = 50.

## 4–6. Split counts (session-aware, class-balanced)

- train: 34 (68%)
- val: 8 (16%)
- test: 8 (16%)

Per-class: uniform 8/2/2, patchy 11/2/2, drip 8/2/2, wetneg 3/1/1,
context 4/1/1.

## 7. Source/session leakage checks

- Multi-image session groups forced into one split: hashtee sag wall
  (drip_002+drip_003 → val), Dean Hochman drips (drip_009+drip_011 → train).
- Beige video session retired (only uniform_001 remains).
- Verified programmatically: no session group spans splits (NONE).
- No exact duplicates: 50 unique SHA-256 (re-verified after swap).

## 8. Remaining known weaknesses

- drip_002/003 blister-vs-sag ambiguity (kept, useful).
- drip_008 graffiti background (shortcut watch).
- uniform_005 railing shadow; uniform_007 text sign (minor).
- patchy_004 weak positive; patchy_015 cluttered room (real-room context).
- Color-class correlation reduced (red brick uniform added) but not gone.
- Wetneg now 2 domain walls + 3 macros — good spread, add more wall-scale
  wet negatives at 200-scale.

## 9. License verification

All 50 finals: known license + named author in metadata.csv (CC BY 4.0 ×16,
CC BY 2.0 ×12, CC BY-SA 4.0 ×12, CC BY-SA 2.0 ×4, CC BY-SA 3.0 ×2,
CC BY-SA 3.0 de ×1, Public domain ×3). Zero missing fields.

## 10. Verdict

**READY FOR BASELINE TRAINING**
