# DFM review — micro servo mounting bracket

Reviewer: cr-dfm-reviewer (Goldfish — no prior project context).
Spec: `tests/fixtures/servo_bracket_spec.md`.
Model checked: `micro_servo.step`, measured facts in `tests/fixtures/servo_facts.md`,
plus independent re-measurement with build123d / OCCT 8.0 (simprep venv).
Process under review: injection-moulded ABS (§3).

## Findings

### Blocker 1 — Solvent bond makes the servo unremovable
- **Target:** side-wall joint, full side-wall contact area (§5) vs servo removal (§1, §8).
- **Severity:** blocker.
- **Evidence:** §5 says the bracket "is solvent-bonded to the servo case along the
  full side-wall contact area for stiffness", while §1 requires the servo to be
  "removed with hand tools in under 2 minutes for servicing" and §8 times a
  technician removing it with a 2 mm hex key.
- **Limit failed:** a solvent bond is permanent; it cannot be undone in 2 minutes
  with hand tools, and breaking it destroys the bracket and risks the servo case.
- **Fix:** delete the solvent bond and retain the servo with screws or clips only,
  or change the §1 requirement to permanent assembly.

### Blocker 2 — Spline hole in the bracket top face cannot line up with the spline
- **Target:** Ø6.0 mm spline clearance hole in the bracket top face (§2).
- **Severity:** blocker.
- **Evidence:** bracket envelope is 16.0 × 35.0 × 14.0 mm (§2), so the top face
  sits at 14 mm, but the servo is 30.7 mm tall (§2; measured 30.68 mm) with the
  output spline at its top — the spline is ~16.7 mm above any top face the
  bracket has, and the servo body (12.0 × 31.3 mm) would have to pass through
  that top face; a top face is also a fourth side, contradicting "wraps the
  servo on three sides" (§2).
- **Limit failed:** the stated geometry cannot be assembled as drawn.
- **Fix:** restate the servo orientation and bracket height so the spline exit
  and the hole are at the same height, or leave the top open and put the
  spline exit through a side wall.

### Blocker 3 — M3 retention screws do not fit the servo mounting ears
- **Target:** two M3 screws through the bracket side walls into the servo
  mounting ears (§2, §4).
- **Severity:** blocker.
- **Evidence:** measured from `micro_servo.step`, the servo mounting-ear holes
  are Ø1.7 mm (radius 0.85 mm cylinders), vertical (axis Z), through 2.0 mm
  flanges, on a 29.7 mm pitch (axes at y = −9.70 and y = 20.00 mm); an M3 screw
  is Ø3.0 mm, and screws through the vertical side walls would run horizontal,
  at right angles to the vertical ear holes.
- **Limit failed:** a Ø3.0 mm screw cannot pass through or thread into a Ø1.7 mm
  hole, and a horizontal screw cannot engage a vertical hole.
- **Fix:** redesign retention to the servo's real interface — for example M1.6
  screws (Ø1.8 mm clearance) through the Ø1.7 mm ear holes vertically, or a
  clamping strap — and record the ear hole size and 29.7 mm pitch in the spec.

### Major 1 — M3 clearance holes drawn at Ø3.0 mm
- **Target:** two M3 clearance holes in the side walls and two M3 clearance holes
  in the base plate, all Ø3.0 mm (§4).
- **Severity:** major.
- **Evidence:** §4 calls out Ø3.0 mm for every M3 clearance hole.
- **Limit failed:** M3 clearance is Ø3.4 mm (medium fit); Ø3.0 mm is the M3 tap
  drill size, so an M3 screw will not pass through the hole.
- **Fix:** enlarge all four M3 clearance holes to Ø3.4 mm.

### Major 2 — Side walls 0.8 mm thick, and wall thickness is not uniform
- **Target:** side walls 0.8 mm thick, 12.0 mm high (§4); minimum wall 0.8 mm
  "throughout" (§3) vs base plate 2.0 mm thick (§4).
- **Severity:** major.
- **Evidence:** §3 states 0.8 mm throughout, §4 states a 2.0 mm base — the two
  contradict each other, and the 0.8 mm walls meet the 2.0 mm base in an abrupt
  2.5× thickness step.
- **Limit failed:** injection-moulded ABS practice is ~1.0 mm minimum wall, and
  0.8 mm walls 12 mm tall risk short shots and warpage; an abrupt thick-to-thin
  step causes sink marks and warpage at the wall-to-base junction.
- **Fix:** thicken the side walls to at least 1.2 mm and taper the transition
  into the 2.0 mm base instead of a step.

### Major 3 — Cost basis uses the wrong process and material
- **Target:** cost target $4.20 per unit at 1,000 units (§7).
- **Severity:** major.
- **Evidence:** §7 bases the cost on "CNC-machined 6061 aluminium, 12 minutes
  machine time per unit" with "Tooling: none (machined from plate)", while §3
  specifies injection-moulded ABS in a "single cavity, family tool".
- **Limit failed:** the cost basis contradicts the stated process and material,
  and injection moulding needs tooling cost amortised over the run, which the
  basis omits entirely.
- **Fix:** re-cost on injection-moulded ABS including tool amortisation, or
  change the process in §3 to machining.

### Major 4 — Recycled-content target is not met by the specified material
- **Target:** recycled content ≥ 30% (§5).
- **Severity:** major.
- **Evidence:** §5 sets the target at ≥ 30% recycled ABS, then specifies
  "virgin ABS, supplier grade GP-22, no recycled-content data supplied".
- **Limit failed:** virgin material with no recycled-content data cannot meet a
  ≥ 30% recycled-content target as specified.
- **Fix:** specify a recycled-content ABS grade that meets ≥ 30%, or drop the
  target.

### Major 5 — Tolerances have no datums and the mounting pitch has no stack-up
- **Target:** all driving dimensions ±0.1 mm; base flatness 0.1 mm; mounting
  pitch 28.0 mm (§4).
- **Severity:** major.
- **Evidence:** §4 gives ±0.1 mm and a 0.1 mm flatness with no datum reference
  frame anywhere in the spec, and §9 admits "No tolerance stack-up has been run
  on the 28.0 mm mounting pitch".
- **Limit failed:** tolerances without datums cannot be inspected or verified,
  and ±0.1 mm on the 28.0 mm pitch is at the limit of what moulded ABS holds,
  so the pitch fit to the base plate is unproven.
- **Fix:** add a datum scheme (A/B/C), reference the flatness to a datum, and
  run the tolerance stack-up on the 28.0 mm pitch.

### Major 6 — Disassembly tool does not match the fastener
- **Target:** servo removal with a 2 mm hex key (§1, §8) vs M3 screws (§2, §4).
- **Severity:** major.
- **Evidence:** §1 and §8 require removal with a 2 mm hex key, but the retention
  and mounting screws are M3.
- **Limit failed:** an M3 socket-head screw takes a 2.5 mm hex key, not 2 mm, so
  the stated tool cannot drive the stated screws.
- **Fix:** call out a 2.5 mm hex key, or change the screws to M2.5 (which uses a
  2 mm hex key) with Ø2.9 mm clearance holes.

### Minor 1 — Edge distance on the base mounting holes is too small
- **Target:** two base mounting holes on a 28.0 mm pitch in a 35.0 mm base (§4).
- **Severity:** minor.
- **Evidence:** 28.0 mm pitch in a 35.0 mm base leaves 3.5 mm from hole centre to
  each end; with the correct Ø3.4 mm clearance hole (see Major 1) the edge
  distance is 1.8 mm.
- **Limit failed:** 1.8 mm edge distance is about 0.5× the hole diameter in
  moulded ABS, below the usual 1–2× diameter, risking breakout and cracking.
- **Fix:** lengthen the base or shorten the pitch to give at least 3 mm edge
  distance.

### Minor 2 — Draft of 1° is the bare minimum on tall thin walls
- **Target:** draft 1° on all vertical walls (§3), side walls 0.8 mm thick and
  12.0 mm high (§4).
- **Severity:** minor.
- **Evidence:** §3 specifies 1° on all vertical walls including the 12 mm tall
  side walls.
- **Limit failed:** 1° is the minimum recommended draft for ABS, and on tall
  thin walls it risks ejection drag and scuffing, while also thinning the
  0.8 mm wall further toward the top.
- **Fix:** increase draft to 1.5–2° on the tall side walls, or confirm 1° with
  the moulder on first articles.

### Minor 3 — No thermal check for a warm servo in an ABS bracket
- **Target:** ABS bracket around a servo that "runs warm" (§9).
- **Severity:** minor.
- **Evidence:** §9 lists as a known gap: "No thermal analysis: the servo runs
  warm and the bracket is ABS", with no maximum servo case temperature stated.
- **Limit failed:** ABS softens at its heat-deflection temperature (~85–100 °C),
  so an unchecked warm servo next to a 0.8 mm ABS wall risks softening and
  loss of the §1 no-deflection requirement.
- **Fix:** get the servo's maximum case temperature and check it against the
  GP-22 grade's heat-deflection temperature with margin.

### Minor 4 — STEP format in the PLM record is wrong
- **Target:** servo source file `micro_servo.step`, "STEP AP242" (§6).
- **Severity:** minor.
- **Evidence:** §6 records the file as STEP AP242, but the file is STEP AP214;
  the AP242 twin is the separate file `micro_servo_ap242.step` (facts file).
- **Limit failed:** the PLM record names the wrong file format, so a downstream
  AP242-only import would fail against the cited file.
- **Fix:** correct the record to AP214, or cite `micro_servo_ap242.step`.

## UNVERIFIED — spec claims that cannot be checked from the model
- "9 g class" servo (§1): mass is not stored in the STEP file, so no mass
  claim can be verified from `micro_servo.step`.
- Stall torque 1.5 kg·cm as worst case (§8): closing evidence is the servo
  datasheet, marked [TO BE OBTAINED].
- ABS grade GP-22 available from the incumbent supplier (§8): closing evidence
  is supplier confirmation, marked [TO BE OBTAINED].
- Cost target $4.20, 12 minutes machine time (§7): the STEP file contains no
  material, process, or cost data; these are engineer claims.
- Servo ear thread or insert: the ears have plain Ø1.7 mm holes; no thread
  callout exists in the file or the spec.

## Controls passed
- Servo envelope 12.0 × 31.3 × 30.7 mm (§2) matches the measured bounding box
  12.00 × 31.30 × 30.68 mm (30.7 mm is the one-decimal rounding of 30.68 mm).
- Servo part count 6 (§6) matches the 6 solids in the file.
- Product name "1143 MicroServo High Torque Metal Gear v1" (§1) matches the
  product name stored in the file.
- Spline clearance hole Ø6.0 mm (§2, §4): the output spline (topmost solid)
  measures 5.00 × 4.95 mm, so a Ø6.0 mm hole gives ~0.5 mm radial clearance.
- Corner radii 0.5 mm minimum (§3): acceptable minimum inside radius for
  injection-moulded ABS.
- Bracket footprint 16.0 × 35.0 mm (§2) fits the servo 12.0 × 31.3 mm envelope:
  12.0 + 2 × 0.8 mm walls = 13.6 mm ≤ 16.0 mm.
- Bracket height is internally consistent: 2.0 mm base + 12.0 mm side walls =
  14.0 mm envelope height (§2, §4).
