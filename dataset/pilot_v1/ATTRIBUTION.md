# Attribution — SmartPaint-Edge 50-Image Pilot

All images are used under their stated open licenses. Roboflow Universe
images: CC BY 4.0 (credit the dataset author + link the source).
Wikimedia Commons images: per-file license in `metadata.csv` (CC BY 2.0 /
3.0 / 4.0, CC BY-SA 2.0 / 3.0 / 4.0, CC0, or Public domain); authors credited
per file. CC0 / Public-domain files require no attribution but are listed
for traceability.

## 1. Roboflow Universe — Internal Wall Finishing Defects

- Source: https://universe.roboflow.com/chew-poh-yee/internal-wall-finishing-defects
- Author: Chew Poh Yee
- License: CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/)
- Attribution: credit "Chew Poh Yee / Roboflow Universe" + link above.
- Full-resolution files fetched as the project's publicly served
  `original.jpg` images (bulk ZIP requires login and was not used).
- Selected IDs: patchy_xx (pin-hole / rough-patchy / trowel classes),
  drip_xx (paint-drips class). Exact mapping in `metadata.csv`.

## 2. Roboflow Universe — paint_defect (Hashtee)

- Source: https://universe.roboflow.com/hashtee/paint_defect
- Author: Hashtee
- License: CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/)
- Attribution: credit "Hashtee / Roboflow Universe" + link above.
- Full-resolution files fetched as the project's publicly served
  `original.jpg` images.
- Selected IDs: uniform_xx, patchy_xx (Patchiness), drip_xx (Sagging).
  Exact mapping in `metadata.csv`.

## 3. Wikimedia Commons — individually verified files

- Source: https://commons.wikimedia.org (per-file pages in `metadata.csv`
  `source_page_url`)
- License/author: per file, see `metadata.csv` (`license`, `author`).
- Files kept only when the exact file license was visible, the subject is a
  genuinely painted wall / paint finish / wet non-paint surface, and the
  class is visually defensible.
- Categories sampled (all individually verified, heavy rejection):
  `House painting`, `Paint rollers`, `Peeling paint`, `White walls`,
  `Painted walls`, `Wet surfaces`, `Empty rooms` (rejected as source).
- Selected IDs: uniform_xx, patchy_xx, drip_xx (roller close-ups showing
  heavy wet coating), wetneg_xx, context_xx. Exact mapping in
  `metadata.csv`.

## 4. Openverse-indexed Flickr files (drip class only)

- Source: https://api.openverse.org (records link the Flickr landing page
  and theCreator; licenses CC BY 2.0 / CC BY-SA 2.0, verified per record).
- Used only for 4 drip-class images (`drip_009`–`drip_012`), one of which
  (`drip_010`) is a Wikimedia Commons file found via Openverse, because
  wall-drip images with verifiable licenses could not be sourced in
  sufficient numbers from the priority sources. Documented deviation,
  not a silent substitution.
- Files, authors, landing pages: see `metadata.csv`
  (`drip_009` Dean Hochman, `drip_010` Charles & Hudson,
  `drip_011` Dean Hochman, `drip_012` stockerre).
- Attribution: credit the named creator + link the landing page
  (`source_page_url`).

## Sources inspected but NOT used in the pilot

- `baopersonal/paint-defect-detection-lx0xk` and
  `baopersonal/paint-defect-combine-zkijl` (CC BY 4.0): 24 full-res previews
  inspected, ~20/24 automotive car panels + many sub-640px crops. Rejected.
- `aprovell/paint-defects-u2wuj-cbs2i` (CC BY 4.0): preview filenames include
  AI-generated images (`pixlr-image-generator-…`). Rejected.
