# Measured facts — GT2 timing pulley, 36 tooth

Source file: `~/workspace/cad-viewer/test-fixtures/timing_pulley.step`
Measured with build123d / OCCT 8.0 (simprep venv). All numbers below
are measurements from the file, not spec claims.

- STEP AP214 (`AUTOMOTIVE_DESIGN { 1 0 10303 214 3 1 1 }`).
- Product: "Aluminum Timing Pulley", "Aluminum Timing Pulley v1".
- Solids: 1. Faces: 299. Total volume: 5,106.7 mm³.
- Envelope: 25.50 × 17.00 × 25.50 mm (Y is the pulley axis).
  Layout along Y: bottom flange 0.00..1.50, toothed section
  1.50..8.50 (7.0 mm wide), top flange 8.50..10.00, hub 10.00..17.00
  (7.0 mm tall).
- Bore: Ø5.00 mm through (cylindrical length 16.80 mm). No
  set-screw hole, no keyway, no flat in the bore — the cylinder list
  of the file contains no other bore feature.
- Teeth: 36 grooves (36 root segments Ø20.00 mm, 36 tip segments
  Ø22.40 mm, 144 R0.25 fillet faces — 4 per tooth). GT2 2 mm pitch:
  pitch diameter = 36 × 2 / π = 22.92 mm [derived]; tip diameter
  22.40 mm matches the GT2 outside-diameter rule (pitch diameter
  − 0.51 mm = 22.41 mm) [derived].
- Flanges: 2× Ø25.50 mm, 1.5 mm thick each.
- Hub: Ø16.00 mm, 7.0 mm tall, on the top face.
- No other holes or features in the file.
