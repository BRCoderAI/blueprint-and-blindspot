# PLM findings — GT2 timing pulley, 36 tooth, aluminium (stage 5)

Reviewer: PLM consistency and implementation readiness (goldfish review — spec and cited files only).
Spec: `~/workspace/cad-review-plugin/tests/fixtures/timing_pulley_spec.md`.
Files checked: `~/workspace/cad-viewer/test-fixtures/timing_pulley.step`,
`~/workspace/cad-viewer/test-fixtures/nema17.step`.
Measured values below were re-verified with OCCT 8.0 (`/tmp/measure.py`):
pulley 1 solid, 299 faces, 5,106.7 mm³, envelope 25.50 × 17.00 × 25.50 mm;
motor 5 solids, 278 faces, 58,681.8 mm³, envelope 42.30 × 55.00 × 42.30 mm.
Both files are STEP AP214.

## Findings

### Blocker

1. **Retention method claimed in §2 does not exist in the model.**
   Severity: blocker. Target: spec §2 "Retention" and §1 acceptance criterion
   "no slip at 40 N·cm".
   Evidence: §2 states retention is a "press fit onto the motor shaft,
   engaging the shaft D-flat", but the measured bore is a plain Ø5.00 mm
   cylinder (1 face, Ø5.00, area 263.9 mm²) with no flat, no set-screw hole
   and no keyway, and §9 admits retention is "friction only, on a bore that
   does not engage the shaft D-flat" — §2 and §9 directly contradict each
   other, and the shaft D-flat (0.5 mm deep, 17.75 mm long, verified in
   nema17.step) has nothing to engage with.
   Fix: decide one retention method (D-flat in the bore, set screw, or a
   dimensioned interference fit with a torque calculation), model it, and
   rewrite §2 and §9 to agree.

### Major

2. **Dataset name and revision do not match the cited file.**
   Severity: major. Target: dataset `PULLEY_GT2_36T` Rev B (§6).
   Evidence: the STEP file's product is "Aluminum Timing Pulley",
   "Aluminum Timing Pulley v1" — the string `PULLEY_GT2_36T` and any
   "Rev B" appear nowhere in the file, and the file version is v1, not
   Rev B.
   Fix: correct §6 to the dataset name and revision that actually identify
   this file, or re-export and check in the file under `PULLEY_GT2_36T`
   Rev B.

3. **"Released" change-control status cannot be tied to the measured file.**
   Severity: major. Target: dataset `PULLEY_GT2_36T` Rev B, §6 "Change
   control: pulley dataset released".
   Evidence: the release claim attaches to Rev B, but the cited file is
   v1 (see finding 2), so there is no evidence the released revision is
   the revision measured here — the released file and the reviewed file
   may not be the same revision.
   Fix: state the release status against the revision that matches the
   file on record (v1, or Rev B once finding 2 is resolved) and cite the
   release record.

4. **Mating part has no dataset, revision, or change-control status.**
   Severity: major. Target: NEMA-17 stepper motor (§2, mating part).
   Evidence: §2 depends on nema17.step (product "NEMA-17 Stepper Motor
   v11", 5 solids), but §6 names no dataset, revision, or change-control
   status for it, so a superseded motor revision could change the shaft
   interface without this spec noticing.
   Fix: add the motor dataset name, revision, and release status to §6.

5. **Press fit is assumed, not dimensioned — interference is not guaranteed.**
   Severity: major. Target: §2 bore/shaft interface and §4 bore tolerance.
   Evidence: bore is Ø5.00 mm H7 (+0.012/−0.000), so the bore can be
   5.000–5.012 mm, while the shaft is stated as Ø5.00 mm with no tolerance
   at all; at nominal sizes there is zero clearance and no guaranteed
   interference, so "press fit" is a hope, not a dimensioned joint.
   Fix: state the shaft tolerance (or a minimum interference) and show the
   resulting fit range in §2/§4.

6. **40 N·cm no-slip acceptance criterion has no verification method.**
   Severity: major. Target: §1 acceptance criterion "no slip at 40 N·cm"
   and §8 verification plan.
   Evidence: §8 offers only a hand "does not rotate by hand" check and an
   axial pull-off test to 50 N — neither measures transmitted torque — and
   the only torque evidence is open assumption (1), marked [TO BE RUN].
   Fix: add a torque test to §8 that applies 40 N·cm and measures slip, and
   close assumption (1) with its result before release.

7. **10,000-hour service life has no verification method.**
   Severity: major. Target: §1 "run for 10,000 hours without service".
   Evidence: §8 contains no life, wear, fatigue, or accelerated-ageing
   test of any kind, so the headline life requirement is unverified.
   Fix: name a verification method for the life requirement (accelerated
   wear test, analysis, or supplier life data) or downgrade it to a design
   goal.

8. **Tooth profile requirement has no tolerance class or inspection method.**
   Severity: major. Target: §4 "Tooth profile per the GT2 standard".
   Evidence: §9 itself records that "per the GT2 standard" names no
   tolerance class or inspection method; §8 has a belt-mesh check but no
   tooth-measurement method, so the 36-tooth profile (verified: 36 grooves,
   tip Ø22.40 mm, root Ø20.00 mm) cannot be accepted or rejected against
   the spec.
   Fix: state the GT2 tolerance class and the tooth inspection method in
   §4 and §8.

### Minor

9. **Belt-centring check does not state the 15 N tension it must verify under.**
   Severity: minor. Target: §8 "Belt mesh" check vs §1 acceptance criterion.
   Evidence: §1 requires centred tracking "under 15 N belt tension", but
   the §8 belt-mesh check says only "run the belt over the pulley" with no
   tension value, so the check as written does not test the stated
   condition.
   Fix: add "at 15 N belt tension" to the §8 belt-mesh check.

10. **Bearing-rating gap names no closing evidence.**
    Severity: minor. Target: §9 "No check of belt tension load against the
    motor shaft bearing rating".
    Evidence: the gap is recorded, but unlike the §8 open assumptions it
    names no evidence that would close it (no bearing datasheet, rating, or
    owner), so it can sit open indefinitely.
    Fix: add the closing evidence (motor bearing rating from the motor
    datasheet) and an owner to the §9 entry.

11. **"Siemens NX" CAD-system claim has no evidence in the cited file.**
    Severity: minor. Target: §6 "CAD system: Siemens NX".
    Evidence: the cited STEP AP214 file contains no reference to Siemens NX
    (UNVERIFIED — no originating-system string in the file), so the claim
    rests on the engineer's word alone.
    Fix: cite the NX dataset or part-file reference that shows the model
    origin, or mark the claim as engineer-stated rather than file-verified.

12. **Cost target has no verifiable basis on file.**
    Severity: minor. Target: §7 cost target $3.80 per unit at 1,000 units.
    Evidence: the only basis given is "4 minutes machine time per unit"
    with no machine rate, material cost, or quote (UNVERIFIED — no cost
    source is cited), so the $3.80 figure cannot be checked against
    anything in the spec.
    Fix: add the machine rate and material cost behind the $3.80, or cite
    the quote it comes from.

13. **Recycled-content target cannot be verified against the material dataset.**
    Severity: minor. Target: §5 recycled-content target ≥ 30%.
    Evidence: §5 itself states the incumbent supplier has supplied "no
    recycled-content data", so the target has no data behind it and the
    material dataset is incomplete for the requirement it carries.
    Fix: obtain the recycled-content data from the supplier or record the
    target as unmet/unverified in §5.

## Controls passed

- Source file exists at the stated path and format matches: `timing_pulley.step`
  is STEP AP214 (`AUTOMOTIVE_DESIGN { 1 0 10303 214 3 1 1 }`), as §6 states.
- Part count: 1 solid, 299 faces, volume 5,106.7 mm³ — matches §6.
- Envelope: 25.50 × 17.00 × 25.50 mm — matches §2.
- Toothed section: 7.0 mm wide (Y 1.50..8.50), 36 grooves — matches §2/§4.
- Tip diameter Ø22.40 mm, root diameter Ø20.00 mm — matches §2/§4.
- Pitch diameter 22.92 mm (36 × 2 / π = 22.92) — derived figure in §2 is correct.
- Bore: Ø5.00 mm through, no set-screw hole, no keyway, no flat — matches §2.
- Flanges: 2× Ø25.50 mm × 1.5 mm thick — matches §4.
- Hub: Ø16.00 mm × 7.0 mm tall on the top face (Y 10.00..17.00) — matches §2/§4.
- Hub wall: (16.0 − 5.0) / 2 = 5.5 mm — derived figure in §3 is correct.
- Mating shaft: Ø5.00 mm, D-flat 0.5 mm deep (plane at Z = 2.00 against a
  Ø5.00 shaft surface at Z = 2.50), 17.75 mm long (Y 20.50..38.25) — matches §2.
- Belt vs toothed section: 6 mm belt in a 7.0 mm wide toothed section — figures
  in §2 agree with each other.
- Runout acceptance criterion (§1, ≤ 0.05 mm) has a named verification method
  (§8, dial indicator at the tip diameter).
- Open assumptions (1) and (2) in §8 each name the evidence that would close
  them (torque/pull-off test; belt supplier tension table).
- No broken internal section references: the spec contains no numbered
  cross-references pointing at non-existent sections.
