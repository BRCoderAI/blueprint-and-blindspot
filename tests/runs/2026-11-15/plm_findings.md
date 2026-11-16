# PLM review findings — micro servo mounting bracket

Reviewer: cr-plm-reviewer (Goldfish — no prior project knowledge)
Date: 2026-11-15
Spec reviewed: `~/workspace/cad-review-plugin/tests/fixtures/servo_bracket_spec.md`
Facts checked against: `~/workspace/cad-review-plugin/tests/fixtures/servo_facts.md`
(measured 2026-11-15 with build123d / OCCT 8.0 from `~/workspace/cad-viewer/test-fixtures/micro_servo.step`)

## Findings

### F1 — blocker — §5 joining vs §1 / §8 removability requirement

- **Named item:** §5 joining method (solvent bonding) vs §1 acceptance criterion "servo removable in under 2 minutes with a 2 mm hex key" and §5 end-of-life separation target.
- **Evidence:** §5 states the bracket "is solvent-bonded to the servo case along the full side-wall contact area for stiffness", while §1 requires the servo to be removable with hand tools in under 2 minutes and §5 separately targets disassembly under 2 minutes for recycling. A full-area solvent bond cannot be undone by hand with a 2 mm hex key in under 2 minutes, and §8's disassembly verification ("time a technician removing the servo with a 2 mm hex key") presumes a removability the joining method rules out.
- **Fix:** Replace solvent bonding with a mechanical retention method consistent with the 2-minute hand-tool removal requirement, or change the removability requirement and its verification method to match a bonded joint.

### F2 — blocker — §2 bracket envelope cannot contain the servo envelope

- **Named item:** §2 bracket envelope 16.0 × 35.0 × 14.0 mm vs §2 servo envelope 12.0 × 31.3 × 30.7 mm [measured: micro_servo.step].
- **Evidence:** Measured servo bounding box is 12.00 × 31.30 × 30.68 mm. Sorted, the servo is 12.0 / 30.7 / 31.3 mm and the bracket is 14.0 / 16.0 / 35.0 mm; the 30.7 mm servo dimension has no bracket dimension it fits inside (the next-largest bracket dimension after 35.0 is 16.0). No orientation of the servo fits inside the stated bracket envelope, so the bracket as dimensioned cannot wrap the servo on three sides, and the Ø6.0 mm spline clearance hole in the "bracket top face" cannot be where the spline is.
- **Fix:** Correct the bracket envelope (or the stated servo orientation) so that every servo dimension fits inside the corresponding bracket dimension with wall thickness allowed for, and re-state the spline-hole location against the corrected geometry.

### F3 — major — §7 cost basis contradicts §3 material and process

- **Named item:** §7 cost basis vs §3 material/process for the bracket.
- **Evidence:** §3 specifies ABS, natural colour, injection moulded, single cavity, family tool with the mating clip. §7 prices the $4.20/unit target on "CNC-machined 6061 aluminium, 12 minutes machine time per unit" with "Tooling: none (machined from plate)". The cost basis describes a different material, a different process, and a no-tooling route that contradicts the family tool in §3, so the $4.20 figure has no valid basis for the part as specified.
- **Fix:** Re-price the unit cost on the specified route (injection-moulded ABS, including the family tool amortisation) and correct the tooling line.

### F4 — major — §5 recycled-content target vs §5 specified material

- **Named item:** §5 recycled-content target (≥ 30% recycled ABS) vs §5 material (virgin ABS, supplier grade GP-22).
- **Evidence:** §5 sets a recycled-content target of ≥ 30% recycled ABS, then specifies virgin ABS grade GP-22 with "no recycled-content data supplied". Virgin ABS contains 0% recycled content, so the specified material cannot meet the stated target.
- **Fix:** Either specify a recycled-content ABS grade that meets the ≥ 30% target (with supplier data), or drop/revise the target to match virgin GP-22.

### F5 — major — §6 servo dataset `MicroServo_v2` Rev B vs file product name v1

- **Named item:** Dataset `MicroServo_v2` Rev B (§6).
- **Evidence:** §6 cites the servo source file as dataset `MicroServo_v2` Rev B, but the product name stored in `micro_servo.step` is "1143 MicroServo High Torque Metal Gear v1". The dataset name and revision in the spec do not match the version recorded in the file (v1, not v2 / Rev B), so it is unclear whether the spec depends on the file at hand or on a different, uncited revision — and the §6 "servo dataset released" status cannot be tied to the measured file.
- **Fix:** Reconcile the dataset name and revision with the file (correct the spec to the v1 dataset, or cite and supply the v2 / Rev B file the spec intends).

### F6 — major — §6 servo source file stated as STEP AP242; measured file is AP214

- **Named item:** Source file `micro_servo.step` (§6).
- **Evidence:** §6 states `micro_servo.step` is "(STEP AP242)". The measured file is STEP AP214; the AP242 twin is a different file, `micro_servo_ap242.step`. The stated format version does not match the cited file.
- **Fix:** Correct §6 to AP214, or cite `micro_servo_ap242.step` as the source file if the AP242 edition is the intended one.

### F7 — major — §6 bracket dataset `BRACKET_SERVO_MOUNT` Rev A cites no source file

- **Named item:** Dataset `BRACKET_SERVO_MOUNT` Rev A (§6).
- **Evidence:** §6 names the bracket dataset and revision but cites no CAD source file for the bracket anywhere in the spec — no file path, no format, no measured envelope. The dataset name and Rev A cannot be checked against any file, and none of the §2–§4 bracket dimensions can be verified against a model.
- **Fix:** Cite the bracket CAD file (path and format) in §6 and confirm Rev A matches the file's version.

### F8 — major — §8 verification plan covers only the §1 acceptance criteria, not §§2–5

- **Named item:** Requirements in §2 (envelope, mounting pitch, spline hole), §3 (wall thickness 0.8 mm, draft 1°, corner radii 0.5 mm), §4 (dimensions and ±0.1 / ±0.25 mm tolerances), §5 (recycled-content target).
- **Evidence:** §8 names verification methods only for the three §1 acceptance criteria (static deflection, cycle life, disassembly). No verification method is named for any dimensional, tolerance, material, or sustainability requirement in §§2–5 — e.g. nothing verifies the 28.0 mm mounting pitch, the 0.8 mm wall thickness, or the ≥ 30% recycled-content target. (§9 discloses that no tolerance stack-up has been run on the 28.0 mm pitch; that gap is disclosed, not hidden.)
- **Fix:** Add a verification method to §8 for each requirement in §§2–5 (dimensional inspection, wall/draft/radii check, material certificate for recycled content), or state explicitly which requirements are not verified.

## UNVERIFIED (could not be checked against the facts file)

These are engineer-sourced claims with no cited file to check them against; they are not findings of mismatch, but they are unverified:

- Bracket envelope and all §2–§4 bracket dimensions, wall thickness, draft, radii, tolerances — no bracket CAD file is cited (§6, see F7).
- Servo mass / "9 g class" (§1) — mass is not stored in the STEP file, so no mass claim can be verified from it.
- CAD system (Siemens NX), dataset revisions, and release/change status (§6) — the STEP file contains no material, process, cost, or PLM data.
- Ø6.0 mm spline clearance vs the actual spline size, and the M3 ear-hole positions (§§2, 4) — the facts file lists solid sizes but does not identify which solid is the spline or the mounting ears.
- All §3 material/process claims, §5 sustainability claims, and §7 cost figures — engineer-sourced; the STEP file contains no such data.

## Controls passed

- Servo product name "1143 MicroServo High Torque Metal Gear v1" (§1) matches the product name stored in `micro_servo.step` exactly.
- Servo envelope 12.0 × 31.3 × 30.7 mm (§2) matches the measured bounding box 12.00 × 31.30 × 30.68 mm (30.68 rounds to 30.7 at the spec's one-decimal precision).
- Servo part count 6 (§6) matches the 6 solids measured in `micro_servo.step`.
- Servo source file `micro_servo.step` exists at the fixture path and was measured 2026-11-15.
- Change-control status is stated for both datasets (§6): bracket dataset under change request CR-114; servo dataset released.
- All three §1 acceptance criteria (deflection ≤ 0.5 mm, no cracking after 10,000 cycles, removal in under 2 minutes with a 2 mm hex key) have a named verification method in §8.
- Both open assumptions name their closing evidence (§8): (1) servo datasheet torque curve for the 1.5 kg·cm worst-case assumption; (2) supplier confirmation for ABS grade GP-22 availability. Both items of evidence are still outstanding ([TO BE OBTAINED]).
- Internal consistency: base plate 2.0 mm + side walls 12.0 mm = bracket height 14.0 mm (§§2, 4); base footprint 16.0 × 35.0 mm matches the bracket envelope footprint (§§2, 4).
- No internal section cross-references exist in the spec to check (§§1–9 contain no "see §" references).
- §9 gaps (no tolerance stack-up on the 28.0 mm pitch; no thermal analysis for a warm servo in an ABS bracket) are disclosed in the spec rather than hidden.
