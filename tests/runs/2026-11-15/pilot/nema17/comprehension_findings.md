# Comprehension findings — NEMA-17 stepper motor integration, extruder drive

Reviewer role: competent engineer who has never seen this project. Source read only:
`tests/fixtures/nema17_spec.md`. No CAD file, no conversation, no facts file.
Question answered: could a stranger build / procure / assemble this from the document alone?

## Dropped generic findings

The following generic findings were considered and dropped because they name no
feature, dimension, tolerance, material, or dataset: "the spec is unclear in
places", "more detail is needed on the motor", "undefined terms in general",
"the verification plan could be stronger", "sustainability needs more work".
Only concrete, named findings below are retained.

## Blockers

### B1 — Pilot recess and locating boss have the same nominal diameter: Ø22.0 mm = Ø22.0 mm, zero clearance
- **Target:** Ø22.0 mm pilot recess (§2) / Ø22.0 mm locating boss on the mounting plate (§2).
- **Evidence (§2):** "Centering: Ø22.0 mm pilot recess on the front face, 2.2 mm deep, receives the Ø22.0 mm locating boss on the mounting plate."
- **Problem:** identical nominal diameters with no tolerance or fit class on either part give zero clearance. The boss cannot enter the recess as dimensioned.
- **Fix:** state the recess tolerance, the boss tolerance, and the fit (e.g. clearance range), and state the boss height against the 2.2 mm recess depth.

### B2 — Pulley bore and shaft have the same nominal diameter: Ø5.00 mm = Ø5.00 mm, zero interference for a claimed press fit
- **Target:** shaft Ø5.00 mm (§2, §4) / GT2 pulley bore Ø5.00 mm (§2).
- **Evidence (§2):** "Shaft: Ø5.00 mm" and "Mating part: GT2 timing pulley, 36 tooth, bore Ø5.00 mm"; (§9) "Pulley retention relies on a press fit onto the D-flat shaft."
- **Problem:** identical nominal diameters give no interference, so the stated press fit does not exist as dimensioned. No interference range, fit class, or bore/shaft tolerance is given anywhere.
- **Fix:** state shaft tolerance, bore tolerance, and the intended interference range; state the D-flat's effect on that interference.

### B3 — Recycled-content requirement contradicts the stated material: ≥20% recycled vs virgin aluminium
- **Target:** end-cap aluminium, recycled content (§5).
- **Evidence (§5):** "Recycled-content target: ≥ 20% recycled aluminium in the end caps" and, in the same section, "Material: end caps are virgin aluminium, no recycled-content data supplied."
- **Problem:** the two lines in one section cannot both be satisfied. A stranger cannot tell whether to procure ≥20% recycled end caps or accept virgin end caps.
- **Fix:** state which line governs, and state the required recycled-content value and its verification method.

### B4 — Holding-torque requirement is unverified: supplier datasheet is not on file
- **Target:** holding torque ≥ 40 N·cm (§1, §8).
- **Evidence (§8):** "Open assumptions: (1) holding torque ≥ 40 N·cm is the worst case — closing evidence: supplier datasheet torque curve [TO BE OBTAINED]"; (§9) "No supplier datasheet on file: torque, current, and insulation class are requirements, not verified values."
- **Problem:** the §1 acceptance criterion (holding torque ≥ 40 N·cm at rated current) has no source data. The motor cannot be accepted against this spec as written.
- **Fix:** obtain the datasheet torque curve and record the verified torque at 1.5 A/phase, or replace the requirement with a measured value.

### B5 — Locating-boss interface is unverified: mounting-plate drawing is not on file
- **Target:** Ø22.0 mm locating boss on the mounting plate (§2, §8).
- **Evidence (§8):** "Open assumptions: (2) the Ø22.0 mm locating boss on the mounting plate exists at the stated diameter — closing evidence: mounting plate drawing [TO BE OBTAINED]."
- **Problem:** the centring interface the whole mounting scheme depends on is an assumption, not a dimensioned mating part. Boss diameter, boss height, and boss tolerance are all missing from this spec.
- **Fix:** obtain the mounting-plate drawing and copy the boss diameter, height, and tolerance into this spec.

### B6 — Tolerance rule is unusable: no dimension is classified driving vs free, and no datum is stated
- **Target:** all §4 dimensions; tolerance rule "All driving dimensions toleranced ±0.1 mm; free dimensions ±0.25 mm" (§4).
- **Evidence (§4):** "All driving dimensions toleranced ±0.1 mm; free dimensions ±0.25 mm [engineer]."
- **Problem:** the spec never says which dimensions are driving and which are free, and no datum system (no datum faces, axes, or reference features) is stated for any tolerance. A stranger cannot tell whether shaft Ø5.00 mm is ±0.1 mm or ±0.25 mm, and cannot tell what any tolerance is measured from.
- **Fix:** list each dimension as driving or free, give its tolerance explicitly, and state the datum for each toleranced dimension.

## Majors

### M1 — Shaft has two different lengths with no explanation: 24.0 mm long (§4) vs 20.0 mm protrusion (§2, §4)
- **Target:** shaft length (§2, §4).
- **Evidence (§2):** "Shaft: Ø5.00 mm, protrudes 20.0 mm beyond the front face"; (§4) "Shaft: Ø5.00 mm × 24.0 mm long, 20.0 mm protrusion."
- **Problem:** the 4.0 mm difference is never explained (embedded length inside the body is assumed, not stated). A stranger cannot tell where the 24.0 mm is measured from.
- **Fix:** state the shaft total length, the protrusion, and the datum each is measured from (front face vs shaft end vs internal shoulder).

### M2 — Mounting holes have no tolerance and no position datum: 4× Ø3.07 mm on 31.0 mm pitch
- **Target:** mounting holes 4× Ø3.07 mm, 31.0 mm square pitch (§2, §4).
- **Evidence (§2):** "Mounting: four M3 screws through the Ø3.07 mm mounting holes on a 31.0 mm square pitch"; (§4) "Mounting holes: 4× Ø3.07 mm on 31.0 mm pitch."
- **Problem:** no hole-diameter tolerance, no pitch tolerance, no position tolerance, and no stated centre (pilot-recess centre is assumed, not stated). M3 through a Ø3.07 mm hole leaves 0.07 mm diametral clearance, so pitch error alone can prevent assembly.
- **Fix:** give hole tolerance, pitch tolerance, position tolerance, and the datum the pitch is measured from.

### M3 — D-flat orientation and flat width are missing
- **Target:** D-flat, 0.5 mm deep × 17.75 mm long (§2, §4).
- **Evidence (§4):** "D-flat: 0.5 mm deep, 17.75 mm long, starting 2.0 mm from the front face."
- **Problem:** no angular orientation of the flat relative to any datum (body face, mounting holes, or shaft axis reference) and no flat width (chord width) are given. A stranger cannot reproduce the flat's position.
- **Fix:** state the flat width and its angular orientation with a datum.

### M4 — Body dimensions do not label which axis is axial: 42.30 × 35.00 × 42.30 mm
- **Target:** motor body 42.30 × 35.00 × 42.30 mm (§2, §4).
- **Evidence (§2):** "Motor body: 42.30 × 35.00 × 42.30 mm."
- **Problem:** the spec never labels which of the three numbers is the axial length. The reader must infer that 35.00 mm is axial because 35.00 + 20.0 = 55.00 mm overall length. The two 42.30 mm faces are also not distinguished (front vs side).
- **Fix:** label each dimension (axial length × width × height) and state which face is the front face.

### M5 — GT2 pulley is undefined and its hub is undimensioned
- **Target:** GT2 timing pulley, 36 tooth (§1, §2).
- **Evidence (§1):** "through a 36-tooth GT2 timing pulley on its shaft"; (§2) "Mating part: GT2 timing pulley, 36 tooth, bore Ø5.00 mm."
- **Problem:** "GT2" is never defined (tooth pitch, tooth profile, and belt width are not stated), and no pulley dimension beyond bore is given — no hub diameter, hub length, overall pulley width, or pulley material.
- **Fix:** define the GT2 tooth pitch/profile and belt width, and dimension the pulley hub (diameter, length) and material.

### M6 — M3 mounting screws are undimensioned: no length, grade, head, or tightening torque
- **Target:** four M3 screws (§2).
- **Evidence (§2):** "Mounting: four M3 screws through the Ø3.07 mm mounting holes on a 31.0 mm square pitch, into the extruder mounting plate."
- **Problem:** screw length, thread engagement, strength grade, head type, and tightening torque are all missing. Mounting-plate thickness is also missing, so screw length cannot be derived.
- **Fix:** state screw length, grade, head type, minimum thread engagement, and tightening torque, plus mounting-plate thickness.

### M7 — Electrical interface is incomplete: 4-wire, 1.5 A/phase, 12 V, with no leads or connector
- **Target:** electrical interface, 4-wire (§2).
- **Evidence (§2):** "Electrical: 4-wire, 1.5 A/phase rated, 12 V nominal."
- **Problem:** lead length, wire gauge, connector type, and pinout/phase order are not stated. A stranger cannot wire the motor from this spec.
- **Fix:** state lead length, wire gauge, connector part/type, and the pinout for the four wires.

### M8 — Materials have no grades: steel, aluminium, copper, NdFeB are named without specification
- **Target:** steel stator laminations, aluminium end caps, copper windings, NdFeB rotor magnets (§3).
- **Evidence (§3):** "Purchased assembly, not manufactured in-house: steel stator laminations, aluminium end caps, copper windings, NdFeB rotor magnets."
- **Problem:** no alloy, grade, temper, or magnet grade/coating is given for any of the four materials, so no equivalent motor can be procured or verified against the spec.
- **Fix:** state the grade/specification for each material (aluminium alloy and temper, steel lamination grade, magnet grade and coating).

### M9 — Step-accuracy test does not measure the stated acceptance: per-step ±5% (§1) vs 200-step cumulative test (§8)
- **Target:** step angle 1.8° ± 5% per step (§1); step-accuracy verification (§8).
- **Evidence (§1):** "step angle 1.8° ± 5% per step"; (§8) "Step accuracy: index 200 steps, measure shaft angle with an encoder."
- **Problem:** indexing 200 steps and measuring total angle measures cumulative angle (360° nominal), not per-step error. A motor can pass the 200-step total while failing the per-step ±5% criterion, or vice versa. Encoder resolution/accuracy is also not stated.
- **Fix:** state a per-step measurement method and the encoder resolution/accuracy required.

### M10 — Thermal acceptance and installed condition conflict, and the measurement point is missing
- **Target:** case temperature ≤ 80 °C (§1); thermal verification (§8); mounting against the extruder heat sink (§9).
- **Evidence (§1):** "motor case temperature ≤ 80 °C after 1 hour at rated current in 25 °C still air"; (§8) "Thermal: run 1 hour at rated current, measure case temperature with a thermocouple"; (§9) "the motor runs warm and sits against an aluminium mounting plate that is also the extruder heat sink."
- **Problem:** the §1 acceptance is in still air, but the installed motor sits against a heat sink, which changes the temperature — the spec never says which condition governs. The thermocouple location on the case is also not stated.
- **Fix:** state whether the ≤80 °C limit applies unmounted in still air or mounted to the plate, and state the thermocouple location on the case.

### M11 — Service life has no verification: 10,000 hours without service, no life test in §8
- **Target:** 10,000-hour service life (§1).
- **Evidence (§1):** "run for 10,000 hours without service"; (§8) lists holding-torque, step-accuracy, fit-check, and thermal tests only — no life, endurance, or bearing-wear test.
- **Problem:** "without service" is also undefined (what counts as service, what failure ends the life). The requirement has no acceptance test.
- **Fix:** define service/failure for the life requirement and state the life verification method (test duration, sample size, or accepted accelerated/analysis basis).

### M12 — Shaft runout tolerance has no datum: ≤ 0.05 mm at the pulley hub
- **Target:** shaft runout ≤ 0.05 mm (§1).
- **Evidence (§1):** "shaft runout ≤ 0.05 mm measured at the pulley hub."
- **Problem:** the datum axis the runout is measured about (shaft axis, pilot-recess axis, or mounting-face datum) is not stated, and the axial position along the hub is not stated.
- **Fix:** state the runout datum axis and the measurement position along the pulley hub.

### M13 — Pilot-recess depth vs boss height: boss height is missing, bottoming risk is unstated
- **Target:** pilot recess 2.2 mm deep (§2); locating boss height (missing).
- **Evidence (§2):** "Ø22.0 mm pilot recess on the front face, 2.2 mm deep, receives the Ø22.0 mm locating boss on the mounting plate."
- **Problem:** the boss height is never given. If the boss is taller than 2.2 mm, the motor will not seat against the plate; if shorter, centring engagement is unknown.
- **Fix:** state the boss height and its tolerance against the 2.2 mm recess depth.

### M14 — Dataset authority is ambiguous: NEMA17_EXTRUDER Rev C vs NEMA17_MOTOR Rev B, and 5 solids are unnamed
- **Target:** datasets NEMA17_EXTRUDER Rev C and NEMA17_MOTOR Rev B (§6); motor part count 5 solids (§6).
- **Evidence (§6):** "CAD system: Siemens NX, dataset `NEMA17_EXTRUDER` Rev C"; "Motor source file: `nema17.step` (STEP AP214), dataset `NEMA17_MOTOR` Rev B"; "Motor part count: 5 solids."
- **Problem:** two datasets at two revisions are named for the same motor with no statement of which is authoritative or how they relate, and the 5 solids are not named, so a stranger cannot verify the STEP file is complete.
- **Fix:** state which dataset/revision governs, the relationship between the two, and name the 5 solids.

## Minors

### m1 — Abbreviations undefined: NdFeB, AP214, NEMA-17
- **Target:** "NdFeB rotor magnets" (§3), "STEP AP214" (§6), "NEMA-17" (title, §6).
- **Evidence (§3):** "NdFeB rotor magnets"; (§6) "`nema17.step` (STEP AP214)".
- **Problem:** none of the three terms is defined in the spec. Dimensions are given for the body, so the NEMA-17 frame size is partly mitigated, but NdFeB and AP214 are not expanded anywhere.
- **Fix:** expand and define each abbreviation on first use.

### m2 — Insulation class: no required value is stated anywhere
- **Target:** insulation class (§9).
- **Evidence (§9):** "No supplier datasheet on file: torque, current, and insulation class are requirements, not verified values."
- **Problem:** insulation class is called a requirement, but no required class (e.g. Class B/F/H) appears in §1–§8. A stranger cannot procure or accept against a value that is never stated.
- **Fix:** state the required insulation class in §1 or §2.

### m3 — RoHS compliance is claimed with no certificate on file
- **Target:** RoHS compliance (§5).
- **Evidence (§5):** "RoHS compliance claimed by the supplier; certificate not on file."
- **Problem:** the claim has no evidence and no acceptance criterion for closing it.
- **Fix:** obtain the certificate and file its reference, or state the alternative acceptance evidence.

### m4 — Front-cap shaft opening Ø10.0 mm has no tolerance, depth, or concentricity
- **Target:** front-cap shaft opening Ø10.0 mm (§2).
- **Evidence (§2):** "Front cap shaft opening: Ø10.0 mm."
- **Problem:** no tolerance, no depth, and no concentricity to the shaft axis are given, so the opening cannot be reproduced or checked.
- **Fix:** give the opening tolerance, depth, and concentricity to the shaft axis.

### m5 — Cost target has no acceptance rule and the hardware cost is unitemised
- **Target:** cost target $14.50 per unit at 1,000 units (§7); mounting hardware $1.70 (§7).
- **Evidence (§7):** "Cost target: $14.50 per unit at 1,000 units"; "Basis: purchased motor $12.80 + mounting hardware $1.70."
- **Problem:** the spec never says whether $14.50 is a maximum, a target with a tolerance, or an estimate, and the $1.70 hardware is not itemised (screw count, type, and length are missing — see M6), so the basis cannot be checked.
- **Fix:** state whether $14.50 is a not-to-exceed limit, and itemise the $1.70 hardware.

### m6 — Change-request status is unstated: CR-207
- **Target:** change request CR-207 (§6).
- **Evidence (§6):** "Change control: motor dataset under change request CR-207; mounting plate dataset released."
- **Problem:** the status and effect of CR-207 are not stated (open, approved, what it changes), so a stranger cannot tell whether the motor dataset as specified is released for build.
- **Fix:** state the CR-207 status and whether the motor dataset is released, frozen, or under change.

## Controls passed

- §1 acceptance values are stated as measurable numbers: holding torque ≥ 40 N·cm, step angle 1.8° ± 5%, shaft runout ≤ 0.05 mm, case temperature ≤ 80 °C after 1 hour at rated current in 25 °C still air.
- §2 overall length is arithmetically consistent with body plus protrusion: 35.00 mm + 20.0 mm = 55.00 mm.
- §4 D-flat start is dimensioned from a stated reference: 2.0 mm from the front face.
- §7 cost arithmetic checks: $12.80 + $1.70 = $14.50.
- §8 verification methods are named per requirement (bench-rig torque meter, encoder, dial indicator, thermocouple), even where the methods are incomplete per the findings above.
