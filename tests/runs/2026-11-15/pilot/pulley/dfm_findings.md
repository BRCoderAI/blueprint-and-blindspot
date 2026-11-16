# DFM findings — GT2 timing pulley, 36 tooth, aluminium

Scope: design specification `timing_pulley_spec.md` checked against
`timing_pulley.step` and the mating `nema17.step`. Every spec number
cited from the CAD files was re-measured with OCCT (`measure.py` plus a
targeted axial/flat check); all re-measured numbers agree with the
supplied facts files. Process stated in the spec: CNC machined 6061
aluminium from bar, then clear anodized — not injection moulding.

## Pinned limits — scope

- Protolabs ABS injection-moulding wall thickness range **1.14–3.56 mm**
  does **not** govern this part: the process is CNC-machined aluminium,
  and the spec (§3) correctly states there are no moulded features, so
  no wall, draft, or rib limit from moulding applies to the 5.5 mm hub
  wall or the 1.5 mm flanges. No finding arises from it.
- ISO 273 medium-series clearance **M3 Ø3.4 mm** has no target in this
  part: the pulley contains no fastener holes at all (verified — the only
  hole is the Ø5.00 mm bore), and the motor's 4× Ø3.07 mm mounting holes
  are the mating part's features, which the pulley does not use. No
  finding arises from it.

## Blockers

### B1 — Bore-to-shaft fit Ø5.00 / Ø5.00: zero interference, so no press fit exists
- Severity: blocker. Target: bore Ø5.00 mm, tolerance +0.012/−0.000 (H7), against motor shaft Ø5.00 mm nominal.
- Evidence: spec §2 ("Retention: press fit onto the motor shaft"), §4 (bore H7), §8 ("slides onto the motor shaft with a hand press fit"). Re-measured: bore is a single Ø5.00 mm cylinder (area 263.9 mm², Y 0.10..16.90); shaft is a single Ø5.00 mm cylinder (area 309.7 mm²). No shaft tolerance is stated anywhere.
- Limit failed: a press fit requires interference; nominal-equal diameters give zero interference, and the H7 bore can be up to Ø5.012 mm against a nominal Ø5.00 mm shaft, i.e. up to 0.012 mm clearance — a clearance/slip fit, not a press fit. "Slides on by hand" in §8 contradicts "press fit" in §2.
- Fix: Specify a true interference fit (bore undersize relative to a toleranced shaft) or, if the fit stays slip, add positive retention per B2.

### B2 — Shaft D-flat 0.5 mm deep × 17.75 mm long: nothing in the bore engages it
- Severity: blocker. Target: bore (plain Ø5.00 mm cylinder) vs shaft D-flat.
- Evidence: spec §2 ("engaging the shaft D-flat") and §9 ("retention is friction only, on a bore that does not engage the shaft D-flat"). Re-measured: the shaft flat is real — a 3.0 mm wide × 17.75 mm long plane at Z = 2.00, Y 20.50..38.25 — while the bore cylinder list contains no flat, keyway, or set-screw hole of any kind.
- Limit failed: the stated retention mechanism (press fit engaging the D-flat) cannot function, because a round bore cannot engage a flat; with B1 there is also no interference to supply friction, so the 40 N·cm no-slip acceptance criterion (§1) and the 50 N pull-off test (§8) have no mechanism behind them.
- Fix: Add a radial set-screw hole through the 5.5 mm hub wall landing on the shaft D-flat (or broach a matching flat into the bore).

## Majors

### M1 — Tooth profile: "per the GT2 standard" states no tolerance class or inspection method
- Severity: major. Target: 36-tooth GT2 profile (tip Ø22.40 mm, root Ø20.00 mm, R0.25 fillets).
- Evidence: spec §4 ("Tooth profile per the GT2 standard") and §9 (gap admitted: "names no tolerance class or inspection method"); §4's general ±0.05 mm does not say whether it applies to tooth form.
- Limit failed: a driving geometry with no stated profile tolerance cannot be inspected, so the §8 belt-mesh check ("teeth seat fully") has no pass/fail criterion.
- Fix: State the GT2 profile tolerance class and the inspection method (measured profile tolerance or go/no-go gauge) on the drawing.

### M2 — 40 N·cm torque capacity by friction-only press fit is assumed, not evidenced
- Severity: major. Target: acceptance criterion "no slip at 40 N·cm" (§1).
- Evidence: spec §8 open assumption (1): "a press fit on a Ø5.00 mm bore transmits 40 N·cm without slip — closing evidence: pull-off and torque test [TO BE RUN]".
- Limit failed: the headline acceptance criterion rests on closing evidence that has not been run, and B1/B2 show the fit as specified supplies no interference and no positive drive, so there is no analysis showing the torque can be transmitted at all.
- Fix: Run the torque and pull-off tests, or add positive retention (B2) and re-state the criterion against it.

### M3 — Motor front-bearing rating under the 15 N radial belt load is not on file
- Severity: major. Target: motor front bearing carrying 15 N radial load on a Ø5 mm shaft.
- Evidence: spec §9 ("No check of belt tension load against the motor shaft bearing rating: 15 N radial load on a Ø5 mm shaft is carried by the motor's front bearing, whose rating is not on file").
- Limit failed: the 10,000-hour no-service acceptance criterion (§1) depends on bearing life under this radial load, which cannot be assessed without the rating.
- Fix: Obtain the bearing rating and L10 life at 15 N radial load from the motor datasheet and record the check.

### M4 — Bore tolerance does not state whether Ø5.00 H7 is before or after anodize, or whether the bore is masked
- Severity: major. Target: bore Ø5.00 mm, +0.012/−0.000, with clear anodize (§3–§4).
- Evidence: spec §3 (material 6061, clear anodized) and §4 (bore H7); neither section states the anodize condition of the bore dimension, and no masking is specified.
- Limit failed: anodize grows material on the bore surface, consuming part or all of the 0.012 mm tolerance band on the single interface that provides retention, so the as-delivered bore size is uncontrolled.
- Fix: State the bore size after anodize, or mask the bore during anodize and dimension it accordingly.

### M5 — 15 N belt tension as worst case is assumed, not evidenced
- Severity: major. Target: belt tension 15 N (§1, §8).
- Evidence: spec §8 open assumption (2): "belt tension 15 N is the worst case — closing evidence: belt supplier tension table [TO BE OBTAINED]".
- Limit failed: belt tracking, flange loading, and the bearing check (M3) all rest on a worst-case load whose supporting evidence has not been obtained.
- Fix: Obtain the belt supplier tension table and confirm 15 N bounds the application.

## Minors

### m1 — Radial runout ≤0.05 mm at the tip diameter has no datum
- Severity: minor. Target: runout ≤0.05 mm at tip Ø22.40 mm (§1).
- Evidence: spec §1 states the runout limit and §8 describes measuring it on the motor shaft, but no datum is designated and no bore-to-tip concentricity callout exists.
- Limit failed: a geometric runout tolerance without a referenced datum has no defined measurement basis on the drawing.
- Fix: Designate the bore axis as datum A and reference the runout tolerance to it.

### m2 — No axial locating dimension: press depth / seating face is unstated
- Severity: minor. Target: pulley axial position on the 20.0 mm shaft protrusion.
- Evidence: spec §2/§8 give no seating face or press depth; re-measured, the pulley is 17.0 mm tall on a shaft protruding 20.0 mm beyond the motor front face, leaving 3.0 mm of shaft exposed with nothing stating where the pulley stops.
- Limit failed: the belt plane's position relative to the motor face is uncontrolled, so assembly cannot be repeated to a defined position.
- Fix: Dimension the seating (e.g. bottom flange against the motor front face) and the belt-centre distance from that face.

### m3 — Edge breaks are in the model but uncalled-out on the drawing
- Severity: minor. Target: bore mouths, flange outside edges, hub edges.
- Evidence: re-measured, the bore cylinder spans Y 0.10..16.90 within the 17.00 mm height, i.e. 0.10 mm entry breaks exist at both bore mouths, yet the spec contains no chamfer or edge-break callout for the bore, the Ø25.50 mm flange edges, or the hub.
- Limit failed: a machinist has no specified edge condition, so as-built breaks are uncontrolled on a part that is handled and anodized.
- Fix: Add edge-break callouts (e.g. break all sharp edges, and a bore-mouth chamfer size) to the drawing.

### m4 — Recycled-content target ≥30% has no supplier data behind it
- Severity: minor. Target: recycled 6061 content (§5).
- Evidence: spec §5 states the ≥30% recycled-content target and in the next line that the incumbent supplier has supplied no recycled-content data.
- Limit failed: a stated target with no evidence cannot be verified at acceptance.
- Fix: Obtain a recycled-content declaration or mill certificate from the supplier, or remove the target.

### m5 — "Single setup" process claim does not state how the 36 milled tooth grooves are cut with the turned features
- Severity: minor. Target: process "CNC machined from bar, single setup" (§3) vs 36 tooth grooves.
- Evidence: spec §3; the bore, hub, and flanges are turned features while the 36 grooves with R0.25 fillets are milled features, and no machine type (e.g. mill-turn) is stated.
- Limit failed: if the teeth need a second setup, the bore-to-tooth concentricity behind the ≤0.05 mm runout criterion (§1) is uncontrolled.
- Fix: State the machine type that achieves a single setup, or add a bore-to-tip concentricity tolerance.

## Controls passed

Spec claims checked against the model and found correct (all re-measured):

- Envelope Ø25.50 × 17.00 mm: bounding box 25.50 × 17.00 × 25.50 mm.
- Part count 1 solid; volume 5,106.7 mm³; 299 faces.
- Flanges 2× Ø25.50 mm × 1.5 mm thick: D25.50 faces confirmed; face planes at Y 0.00, 1.50, 8.50, 10.00 confirm 1.5 mm per flange.
- Toothed section 7.0 mm wide, 36 teeth: D20.00/D22.40 faces span Y 1.50..8.50; 36 root segments Ø20.00 mm and 36 tip segments Ø22.40 mm; 144 R0.25 fillet faces.
- Tip diameter Ø22.40 mm, root diameter Ø20.00 mm.
- Pitch diameter 22.92 mm: 36 × 2 / π = 22.92 mm.
- Bore Ø5.00 mm through, no set-screw hole, no keyway, no flat in the bore.
- Hub Ø16.00 mm × 7.0 mm tall: D16.00 face spans Y 10.00..17.00.
- Hub wall 5.5 mm: (16.0 − 5.0) / 2 = 5.5 mm.
- Overall stack arithmetic: 1.5 + 7.0 + 1.5 + 7.0 = 17.0 mm.
- Mating shaft Ø5.00 mm with 0.5 mm deep D-flat, 17.75 mm long: flat face 3.0 mm wide × 17.75 mm long at Z = 2.00, Y 20.50..38.25; shaft solid 24.00 mm long, protruding 20.0 mm beyond the motor front face.
- Motor envelope 42.30 × 55.00 × 42.30 mm; 5 solids; volume 58,681.8 mm³.
- No fastener holes in the pulley, so no clearance-hole check applies.
- Spec §3 is correct that no moulded features exist, so draft and ribs do not apply.

## UNVERIFIED — cited numbers that could not be checked from the CAD files

- Cost $3.80 per unit at 1,000 units and 4 minutes machine time per unit (§7): no rate or cycle data in the files; not asserted correct.
- 10,000-hour service life (§1): a requirement, not measurable from the model.
- Achievability of the ±0.05 mm general tolerance and the H7 bore by the stated CNC process: no machine capability data in the spec.
- Belt width 6 mm and GT2 belt properties: the belt is not a supplied CAD file.
- Motor front-bearing rating: not in any supplied file (see M3).
