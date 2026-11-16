# DFM review — micro servo mounting bracket

Reviewer: cr-dfm-reviewer (Goldfish — no prior project knowledge)
Spec: `tests/fixtures/servo_bracket_spec.md`
Model checked: `micro_servo.step` (measured facts in `tests/fixtures/servo_facts.md`,
independently re-measured with build123d / OCCT 8.0: 6 solids,
12.00 × 31.30 × 30.68 mm — matches the facts file)
Date: 2026-11-15

No bracket CAD file was supplied, so every bracket dimension below is
checked against the spec's own numbers and the stated process, not
against a bracket model. Bracket dimensions that could not be checked
against any model are listed as UNVERIFIED at the end, not passed.

---

## Findings

### F-01 — blocker — Side-wall thickness 0.8 mm, injection-moulded ABS
- **Target:** side walls, 0.8 mm thick (§3, §4).
- **Evidence:** spec §3 states minimum wall thickness 0.8 mm
  throughout; §4 gives side walls 0.8 mm thick, 12.0 mm high.
  Process is injection-moulded ABS.
- **Limit failed:** practical minimum wall for injection-moulded ABS
  is about 1.5 mm (about 1.0 mm only with thin-wall tooling and
  high-flow grades). At 0.8 mm the walls risk short shots, poor fill
  and sink, and are too weak to hold a servo against a 1.5 kg·cm
  stall torque with no visible deflection.
- **Fix:** thicken the side walls to at least 1.5 mm and re-check the
  16.0 mm bracket width against the 12.0 mm servo width for fit.

### F-02 — blocker — Bracket solvent-bonded to the servo, but servo must come off in under 2 minutes
- **Target:** joining, full side-wall contact area (§5) vs.
  serviceability (§1, §8).
- **Evidence:** §5 says the bracket is solvent-bonded to the servo
  case along the full side-wall contact area for stiffness. §1
  acceptance criteria require the servo to be removable in under
  2 minutes with a 2 mm hex key, and §5 targets disassembly under
  2 minutes for recycling.
- **Limit failed:** a solvent bond cannot be undone in 2 minutes
  with a hex key, and it makes the §5 end-of-life separation of
  bracket from servo impossible without destroying one of them.
- **Fix:** delete the solvent bond and hold the servo with the two
  M3 screws alone; prove stiffness another way (wall thickness,
  ribs) and re-run the deflection test.

### F-03 — major — M3 clearance holes are Ø3.0 mm
- **Target:** servo-ear holes and base mounting holes, Ø3.0 mm (§4).
- **Evidence:** §4 calls out two M3 clearance holes through the
  0.8 mm side walls and two M3 clearance holes through the 2.0 mm
  base plate, both Ø3.0 mm.
- **Limit failed:** M3 clearance per ISO 273 is Ø3.4 mm (medium).
  Ø3.0 mm equals the screw's nominal diameter, so an M3 screw
  cannot pass through the hole at all.
- **Fix:** enlarge all four M3 clearance holes to Ø3.4 mm.

### F-04 — major — Spline cannot reach the hole in the bracket top face
- **Target:** spline clearance hole, Ø6.0 mm, in the bracket top
  face (§2) vs. servo height 30.68 mm (measured).
- **Evidence:** the servo's output spline is the 5.00 × 4.95 × 3.50 mm
  solid at the top end of the servo's 30.68 mm axis (measured
  Z 8.38–11.88 mm, the extreme end of the part). The bracket is
  14.0 mm tall with 12.0 mm side walls (§2, §4). Under the only
  orientation in which a top-face hole makes sense (servo standing
  on the base, 30.68 mm vertical), the bracket top face sits about
  16.7 mm below the spline.
- **Limit failed:** the spline never reaches the bracket top face,
  so it cannot exit through a Ø6.0 mm hole in that face as specified.
- **Fix:** define the servo orientation in the spec, set the bracket
  height so its top face actually meets the spline, or delete the
  top-face hole and leave the spline exposed above the bracket.

### F-05 — major — Retention screws cannot be shown to reach the servo ears
- **Target:** servo retention, two M3 screws through the side walls
  into the servo mounting ears (§2).
- **Evidence:** the screws pass through 12.0 mm-high side walls,
  but the spec gives no dimension for the height of the servo
  mounting ears above the base, and the servo is 30.68 mm tall
  (measured). The ears sit near the spline end of the servo, well
  above a 12.0 mm wall if the servo stands on the base.
- **Limit failed:** with no ear-height dimension, the screws through
  12.0 mm walls cannot be shown to meet the ears at all; the
  assembly as specified may have nothing for the screws to bite into.
- **Fix:** dimension the ear-hole height from the base, and raise
  the side walls or relocate the screws so they meet the ears.

### F-06 — major — Cost basis is a different material and a different process
- **Target:** cost target $4.20/unit at 1,000 units (§7).
- **Evidence:** §7 bases the cost on CNC-machined 6061 aluminium,
  12 minutes machine time per unit, no tooling. §3 states the part
  is ABS, injection moulded, single cavity, family tool.
- **Limit failed:** the $4.20 figure is costed for a machined
  aluminium part, not a moulded ABS part; it includes no tooling
  cost for the mould the process section requires.
- **Fix:** re-cost the part as injection-moulded ABS, including
  tooling amortisation over 1,000 units.

### F-07 — major — Recycled-content target is unmet by the specified material
- **Target:** recycled content, ≥ 30% recycled ABS (§5).
- **Evidence:** §5 sets a ≥ 30% recycled-content target, then
  specifies virgin ABS, supplier grade GP-22, with no
  recycled-content data supplied.
- **Limit failed:** virgin ABS contains 0% recycled content, so the
  specified material fails the spec's own ≥ 30% target.
- **Fix:** specify a recycled-content ABS grade with supplier data
  showing ≥ 30%, or drop the target.

### F-08 — major — No boss, position, or edge distance for the M3 holes in 0.8 mm walls
- **Target:** M3 holes through the 0.8 mm side walls (§4).
- **Evidence:** §4 gives the hole diameter only. No boss diameter,
  no hole position, and no edge distance are stated for the
  retention screws.
- **Limit failed:** a 0.8 mm wall gives essentially no bearing area
  for an M3 screw, and with no boss the screw load goes straight
  into a thin moulded wall that is already below the ABS minimum
  thickness (see F-01).
- **Fix:** add bosses around the retention holes (minimum about
  Ø6 mm boss, 1.5 mm wall) with stated positions and edge distance,
  or move retention to the base plate.

### F-09 — major — Base mounting holes are too close to the ends of the base
- **Target:** base mounting holes, 28.0 mm pitch on a 35.0 mm base (§4).
- **Evidence:** (35.0 − 28.0) / 2 = 3.5 mm from hole centre to each
  end of the base. With the required Ø3.4 mm clearance holes
  (see F-03), only 1.8 mm of material remains between the hole edge
  and the end of the base.
- **Limit failed:** minimum edge distance for a loaded hole in ABS
  is about one hole diameter of material past the hole edge
  (3.4 mm), or 1.5× diameter centre-to-edge. 1.8 mm fails both and
  risks breakout and cracking at the base ends.
- **Fix:** shorten the pitch or lengthen the base to leave at least
  3.4 mm of material past each hole edge.

### F-10 — major — Spec cites the wrong STEP format for the servo file
- **Target:** servo source file `micro_servo.step` (§6).
- **Evidence:** §6 says the file is STEP AP242. The measured file
  is STEP AP214; the AP242 twin is the separate file
  `micro_servo_ap242.step`.
- **Limit failed:** the dataset as cited does not match the file
  that was actually measured and reviewed.
- **Fix:** correct §6 to AP214, or cite the AP242 twin file and
  review that file instead.

### F-11 — major — Spec cites a v2 servo dataset; the file is v1
- **Target:** servo dataset `MicroServo_v2` Rev B (§6).
- **Evidence:** §6 cites dataset `MicroServo_v2` Rev B. The product
  name stored in the file is "1143 MicroServo High Torque Metal Gear
  v1".
- **Limit failed:** the reviewed file is the v1 product, not the v2
  dataset the spec claims. The design may have been checked against
  the wrong servo revision.
- **Fix:** reconcile the dataset — cite the v1 dataset, or obtain
  the v2 file and re-check the envelope and interfaces against it.

### F-12 — minor — Driving tolerances have no datums and no stack-up
- **Target:** "all driving dimensions toleranced ±0.1 mm" (§4).
- **Evidence:** §4 assigns ±0.1 mm to driving dimensions with no
  datum reference frame, and §9 admits no tolerance stack-up has
  been run on the 28.0 mm mounting pitch.
- **Limit failed:** a tolerance without a datum cannot be inspected
  or held, and the 28.0 mm pitch that locates the part on the base
  plate is unverified against the mating holes.
- **Fix:** assign datums to the driving dimensions and run the
  stack-up on the 28.0 mm pitch before release.

### F-13 — minor — ±0.1 mm flatness on a 35 mm ABS base is unevidenced
- **Target:** base plate flatness 0.1 mm over 16.0 × 35.0 mm (§4).
- **Evidence:** §4 specifies flatness 0.1 mm on the 2.0 mm ABS base
  plate. No process-capability evidence is given.
- **Limit failed:** 0.1 mm flatness over 35 mm is at the tight end
  for a thin injection-moulded ABS plate, which is prone to warpage;
  the spec gives no basis for holding it.
- **Fix:** get process-capability data for flatness from the moulder
  or relax the flatness callout.

### F-14 — minor — Acceptance criteria rest on two unconfirmed assumptions
- **Target:** stall torque 1.5 kg·cm and ABS grade GP-22 availability (§8).
- **Evidence:** §8 lists both as open assumptions with closing
  evidence marked TO BE OBTAINED: the servo datasheet torque curve
  and supplier confirmation for GP-22.
- **Limit failed:** the deflection limit (≤ 0.5 mm at stall torque)
  and the 10,000-cycle life requirement are set against a load case
  and a material that are both still unconfirmed.
- **Fix:** obtain the datasheet torque curve and the supplier
  confirmation before freezing the acceptance criteria.

### F-15 — minor — Servo ear-hole diameter is not stated, so M3 fit cannot be checked
- **Target:** servo mounting ears (§2, §4).
- **Evidence:** the spec never gives the diameter of the holes in
  the servo's own mounting ears, and the facts file gives part sizes
  only, no hole diameters.
- **Limit failed:** the M3 retention screws cannot be shown to fit
  the ears they screw into.
- **Fix:** state the ear-hole diameter from the servo datasheet and
  confirm M3 screws fit, or change the fastener size.

### F-16 — minor — 2 mm hex key specified but no screw head type is given
- **Target:** disassembly with a 2 mm hex key (§1, §8).
- **Evidence:** §1 and §8 require servo removal with a 2 mm hex key.
  No screw head type is specified anywhere in the spec. An M3
  socket-head cap screw takes a 2.5 mm key; a 2 mm key fits an M3
  button head.
- **Limit failed:** the specified tool cannot be verified against
  the specified fastener.
- **Fix:** state the screw head type, or correct the key size to
  match the head.

### F-17 — minor — Family tool references a mating clip that is never specified
- **Target:** process, "family tool with the mating clip" (§3).
- **Evidence:** §3 says the tool is a family tool with the mating
  clip, but the mating clip has no dimensions, material, dataset,
  or specification anywhere in the document.
- **Limit failed:** the tooling plan depends on a second part that
  is not defined, so the family-tool claim cannot be costed or built.
- **Fix:** specify the mating clip (or delete the family-tool reference).

### F-18 — minor — No thermal analysis for a warm servo in an ABS bracket
- **Target:** thermal behaviour of the ABS bracket (§9).
- **Evidence:** §9 states no thermal analysis has been done: the
  servo runs warm and the bracket is ABS.
- **Limit failed:** ABS softens well below its heat-deflection
  temperature under sustained load, so the no-deflection claim (§1)
  is unevidenced at operating temperature.
- **Fix:** measure the servo case temperature under stall and run a
  thermal check on the bracket before relying on the deflection test.

---

## Controls passed

Spec claims checked against the measured model and found correct:

- **C-1 — Servo envelope 12.0 × 31.3 × 30.7 mm (§2).** Measured
  12.00 × 31.30 × 30.68 mm; 30.68 rounds to 30.7. Correct.
- **C-2 — Servo part count 6 (§6).** Measured 6 solids.
  Correct.
- **C-3 — Servo product name (§1, §6).** File product name is
  "1143 MicroServo High Torque Metal Gear v1", matching the spec.
  Correct.
- **C-4 — Draft 1° on vertical walls (§3).** 1° is an adequate
  minimum draft for injection-moulded ABS. Pass.
- **C-5 — Corner radii 0.5 mm minimum (§3).** 0.5 mm is an adequate
  minimum inside radius for ABS. Pass.
- **C-6 — Base plate 2.0 mm thick (§4).** 2.0 mm meets the ABS
  injection-moulding minimum wall thickness. Pass.
- **C-7 — Spline hole Ø6.0 mm vs. spline size (measured).** The
  spline solid is 5.00 × 4.95 mm, so a Ø6.0 mm hole gives about
  0.5 mm radial clearance — adequate as a diameter. (Its position
  fails; see F-04.)

## UNVERIFIED — could not be checked (no bracket CAD file supplied)

- Bracket envelope 16.0 × 35.0 × 14.0 mm (§2).
- Base plate 16.0 × 35.0 × 2.0 mm and its flatness (§4).
- Side-wall height 12.0 mm (§4).
- 28.0 mm mounting pitch (§2, §4).
- Spline hole, ear holes, and base holes as built — positions and
  diameters exist only as spec text, no bracket model.
- Bracket dataset `BRACKET_SERVO_MOUNT` Rev A, change request
  CR-114 (§6) — no PLM record supplied.
- Servo mass — not stored in the STEP file; no mass claim in the
  spec was checkable against the model.
