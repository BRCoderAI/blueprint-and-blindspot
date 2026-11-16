# DFM findings — NEMA-17 stepper motor integration, extruder drive

Reviewer: DFM (manufacturing) review, stage 2. Spec: `nema17_spec.md`.
Models re-measured with OCCT: `nema17.step` (5 solids, 278 faces,
42.30 × 55.00 × 42.30 mm, 58,681.8 mm³) and `timing_pulley.step`
(1 solid, 299 faces, 25.50 × 17.00 × 25.50 mm, 5,106.7 mm³) — all
re-measured values agree with the supplied facts files.

Pinned limits used (quoted, not recalled): Protolabs ABS injection
moulding wall thickness **1.14–3.56 mm**; ISO 273 medium (normal)
series **M3 clearance Ø3.4 mm**. No ABS or injection-moulded feature
is defined anywhere in this spec (the motor is a bought-in assembly,
spec §3), so the 1.14–3.56 mm wall range has no feature to check
against — see Finding 7 for the part that would carry that check.

## Findings

### Blocker 1 — Mounting holes 4× Ø3.07 mm for M3 screws
- **Target:** mounting holes, 4× Ø3.07 mm on 31.0 mm square pitch (spec §2, §4).
- **Evidence:** measured Ø3.07 mm (64 cylindrical faces) at centres
  (±15.50, ±15.50), re-measured; spec calls for M3 screws through them.
- **Limit failed:** ISO 273 medium series M3 clearance is **Ø3.4 mm**;
  Ø3.07 mm is 0.33 mm undersize, leaving 0.07 mm diametral clearance
  over a Ø3.0 mm screw, and the §4 ±0.1 mm tolerance allows a Ø2.97 mm
  hole — smaller than the screw.
- **Fix:** Enlarge the clearance holes to Ø3.4 mm, or state that the
  motor holes are threaded M3 and put the Ø3.4 mm clearance in the
  mounting plate instead, correcting the screw path in §2.

### Blocker 2 — Pilot recess Ø22.0 mm receives locating boss Ø22.0 mm
- **Target:** pilot recess, Ø22.0 mm × 2.2 mm deep (spec §2, §4).
- **Evidence:** recess measured Ø22.0 mm (Y 16.15..18.35),
  re-measured; mating boss stated as Ø22.0 mm in §2, with no plate
  drawing on file (open assumption §8(2)).
- **Limit failed:** zero nominal clearance — a line-to-line fit — and
  the §4 ±0.1 mm tolerance on each side allows up to 0.20 mm
  interference, so the motor cannot reliably seat on the plate.
- **Fix:** Specify a clearance fit with stated tolerances on both
  parts (e.g. recess Ø22.0 mm with a defined tolerance class and boss
  0.1–0.2 mm smaller) and obtain the mounting plate drawing.

### Blocker 3 — Pulley bore Ø5.00 mm on shaft Ø5.00 mm
- **Target:** timing pulley bore Ø5.00 mm mating with motor shaft
  Ø5.00 mm (spec §2, §4).
- **Evidence:** bore measured Ø5.00 mm (single cylindrical face,
  re-measured); shaft measured Ø5.00 mm (Y 14.50..37.75 cylindrical
  portion, re-measured).
- **Limit failed:** zero nominal clearance with no fit class stated,
  and the §4 ±0.1 mm tolerance allows anything from 0.20 mm clearance
  (loose slip fit) to 0.20 mm interference (seized press), so the fit
  is uncontrolled.
- **Fix:** Specify the fit explicitly (fit class and tolerances on
  both diameters, or a defined interference value for a press fit).

### Major 1 — D-flat has no mating feature in the pulley
- **Target:** shaft D-flat, 0.5 mm deep × 17.75 mm long (spec §2, §4).
- **Evidence:** flat verified in the motor (plane at Z = 2.00,
  Y 20.50..38.25, re-measured); the pulley bore is a plain Ø5.00 mm
  cylinder with no flat, no keyway and no set-screw hole (pulley
  cylinder list contains no other bore feature, re-measured), and
  spec §9 admits the hub carries no set screw.
- **Limit failed:** a round bore cannot engage a flat, so the flat
  transmits no torque and retention is press-fit-only against the
  §1 holding-torque requirement of ≥ 40 N·cm, with no torque
  capacity stated or tested.
- **Fix:** Add a matching flat in the pulley bore, or a set screw in
  the Ø16.00 × 7.0 mm hub, and prove the retention torque by test.

### Major 2 — Pulley axial position and retention undefined
- **Target:** pulley axial location on the shaft (spec §2, §8 fit check).
- **Evidence:** shaft protrudes 20.0 mm beyond the front face while
  the pulley is 17.0 mm tall overall, so 3.0 mm of shaft stands proud
  if the pulley seats on the front face, and the spec states no
  seating face, shoulder, stop or axial retention feature.
- **Limit failed:** no defined assembly position — the pulley can
  slide axially along the shaft with nothing fixing it, so belt
  alignment with the extruder drive is uncontrolled.
- **Fix:** Define the seating face and axial position of the pulley on
  the shaft and add an axial retention feature.

### Major 3 — Blanket tolerance scheme with no datums
- **Target:** §4 "all driving dimensions ±0.1 mm; free dimensions
  ±0.25 mm".
- **Evidence:** the blanket tolerance is what turns the three
  zero-clearance fits (Blockers 1–3) into possible interference, and
  the §1 shaft runout limit of ≤ 0.05 mm at the pulley hub is tighter
  than the general ±0.1 mm with no datum stated for the runout
  (shaft axis or front face).
- **Limit failed:** driving fits require fit-specific tolerances with
  datums; a blanket ±0.1 mm is not a tolerance scheme for mating
  features.
- **Fix:** Replace the blanket tolerance with per-feature fit
  tolerances and datums, including a stated runout datum.

### Major 4 — Mounting plate, the only part to be manufactured, is undefined
- **Target:** extruder mounting plate (spec §2, §3).
- **Evidence:** the plate carries the Ø22.0 mm locating boss, the
  mating M3 holes and the extruder heat-sink interface, but the spec
  gives it no material, no process, no dimensions and no drawing
  (boss existence is open assumption §8(2)); §3 states no moulded or
  machined features are defined by this spec.
- **Limit failed:** with no process or material stated, no process
  limit can be checked — including the Protolabs ABS wall range of
  **1.14–3.56 mm**, the 1° draft rule and the 40–60% rib/boss rule,
  none of which has a target in this document.
- **Fix:** Issue the mounting plate drawing with material, process
  and toleranced dimensions so its features can be checked against
  that process's limits.

### Minor 1 — Pilot recess depth datum ambiguous by 0.15 mm
- **Target:** pilot recess depth, 2.2 mm (spec §2, §4).
- **Evidence:** recess cylinder spans Y 16.15..18.35 (2.20 mm,
  re-measured) but the front face plane is at Y 18.50, so depth
  measured from the face is 2.35 mm.
- **Limit failed:** a depth dimension without a stated datum face is
  ambiguous by 0.15 mm.
- **Fix:** Dimension the recess depth from the front face plane.

### Minor 2 — Small internal features in the model are undimensioned
- **Target:** undimensioned cylindrical features in `nema17.step`
  (spec §4 silent).
- **Evidence:** measured Ø1.00 mm (40 faces), Ø2.00 mm (9 faces) and
  Ø2.67 mm (56 faces) cylindrical faces, re-measured; none is
  dimensioned or described in the spec.
- **Limit failed:** features present in the model but absent from the
  spec are uncontrolled — if functional they need dimensions and
  tolerances, if not they should be explicitly excluded.
- **Fix:** Dimension the functional ones or state in the spec that
  they are non-functional detail carried from the supplier model.

### Minor 3 — Recycled-content and RoHS claims unverified
- **Target:** §5 recycled-content target ≥ 20% and RoHS compliance.
- **Evidence:** spec §5 states the end caps are virgin aluminium
  with no recycled-content data supplied, and RoHS is claimed with
  the certificate not on file.
- **Limit failed:** a stated material target and a compliance claim
  with no supporting evidence cannot be accepted against the spec.
- **Fix:** Obtain the recycled-content data and RoHS certificate, or
  remove the target and the claim from the spec.

## Controls passed

Spec claims checked against the re-measured models and found correct:

- Motor body 42.30 × 35.00 × 42.30 mm; overall length with shaft
  55.00 mm; envelope 42.30 × 55.00 × 42.30 mm.
- Shaft Ø5.00 mm × 24.0 mm long, protruding 20.0 mm beyond the front
  face (front face Y 18.50, shaft tip Y 38.50).
- D-flat 0.5 mm deep (plane Z = 2.00 against shaft surface Z = 2.50),
  17.75 mm long (Y 20.50..38.25), starting 2.0 mm from the front face.
- Mounting holes 4× Ø3.07 mm on 31.0 mm square pitch (centres
  (±15.50, ±15.50), verified by face positions).
- Pilot recess Ø22.0 mm; front cap shaft opening Ø10.0 mm.
- Motor part count 5 solids; total volume 58,681.8 mm³.
- Pulley: 36 teeth, bore Ø5.00 mm, tip diameter Ø22.40 mm, root
  Ø20.00 mm, flanges 2× Ø25.50 mm × 1.5 mm thick, hub Ø16.00 mm ×
  7.0 mm tall, envelope 25.50 × 17.00 × 25.50 mm, 1 solid,
  volume 5,106.7 mm³.
- Front cap shaft opening Ø10.0 mm gives 2.5 mm radial clearance
  around the Ø5.00 mm shaft.
- No number cited from either model was found to disagree with the
  model; nothing required an UNVERIFIED mark — every cited model
  number was re-measured or verified by face position, except the
  mounting plate boss Ø22.0 mm, which is not in either model file
  (open assumption §8(2), not a model claim).
