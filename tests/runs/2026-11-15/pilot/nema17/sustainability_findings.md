# Sustainability findings — NEMA-17 stepper motor integration, extruder drive

Reviewer: bb-sustainability-reviewer (stage 4, Goldfish)
Spec: `tests/fixtures/nema17_spec.md`
Mating part: GT2 timing pulley, 36 tooth (`tests/fixtures/timing_pulley_facts.md`)
Date: 2026-11-15

## Method

Every CAD-cited number in the spec was checked against the measured
facts files and re-measured from the STEP files with
`/tmp/measure.py` (OCCT 8.0). Re-measurement confirmed: motor 5 solids,
58,681.8 mm³, envelope 42.30 × 55.00 × 42.30 mm; shaft Ø5.00 mm,
24.0 mm long, 20.0 mm protrusion; D-flat 0.5 mm deep; mounting holes
4× Ø3.07 mm on 31.0 mm pitch; pilot recess Ø22.0 mm; front cap opening
Ø10.0 mm; pulley 1 solid, 5,106.7 mm³, bore Ø5.00 mm, 36 teeth
(Ø20.00 mm root / Ø22.40 mm tip). All dimensional claims in spec
§2 and §4 check out. No sustainability claim in §5 is supported by
measured model data, because the STEP files carry no material,
recycled-content, or compliance data — that absence is itself
recorded below as findings, not as a pass.

## Findings

### F1 — Blocker — Aluminium end caps: recycled-content target contradicted by stated material
- **Target/material:** end caps, recycled-content target ≥ 20% recycled aluminium (spec §5).
- **Evidence:** spec §5 states the end caps are virgin aluminium, with no recycled-content data supplied. Virgin aluminium is 0% recycled content against a ≥ 20% target — the target is not merely unevidenced, it is missed on the spec's own statement.
- **Fix:** Source end caps with ≥ 20% certified recycled aluminium and file the supplier's recycled-content declaration, or formally revise the target and record the change.

### F2 — Major — RoHS compliance claimed with no certificate on file
- **Target/material:** RoHS compliance for the whole motor assembly (spec §5).
- **Evidence:** spec §5 claims supplier RoHS compliance but states the certificate is not on file; no restricted-substance declaration, test report, or declaration of conformity is cited anywhere in the spec.
- **Fix:** Obtain and file the supplier RoHS certificate / declaration of conformity for this exact motor before acceptance.

### F3 — Major — NdFeB rotor magnets: no grade, recycled content, REACH status, or recovery route
- **Target/material:** NdFeB rotor magnets (spec §3).
- **Evidence:** spec §3 names NdFeB magnets and gives no grade, no recycled-content figure, no REACH/restricted-substance status, and §5 states material recovery requires shredding, which loses rare-earth magnets into mixed shredder output with no recovery route named.
- **Fix:** Obtain the magnet grade, recycled-content and REACH data from the supplier and name a rare-earth recovery or take-back route, or record shredding loss as an accepted impact.

### F4 — Major — Steel stator laminations and copper windings: no grade, recycled content, or material-health data
- **Target/material:** steel stator laminations, copper windings (spec §3).
- **Evidence:** spec §3 names both materials with no grade, no recycled-content percentage or source, and no REACH/RoHS status for either; §5 sets a recycled-content target only for aluminium, so steel and copper have no target and no data at all.
- **Fix:** Obtain grade, recycled-content percentage with source, and restricted-substance status for the steel and copper from the supplier and set or explicitly waive a target for each.

### F5 — Major — Insulation material unnamed, with no material-health data
- **Target/material:** winding insulation (spec §5 end-of-life list).
- **Evidence:** spec §5 lists insulation as one of the mixed materials at end of life, but no insulation material is named anywhere in §3 or §5, and no restricted-substance or material-health data is given for it.
- **Fix:** Name the insulation material and grade and file its restricted-substance / material-health data.

### F6 — Major — End of life: not designed for disassembly, shredding only, no separation plan or disassembly time
- **Target/material:** whole motor assembly — steel, copper, aluminium, magnets, insulation (spec §5).
- **Evidence:** spec §5 states the motor is a mixed-material assembly, is not designed for disassembly, and material recovery requires shredding; no disassembly time is stated, no disassembly sequence is given, no material-separation plan exists, and the §8 verification plan contains no end-of-life or disassembly test.
- **Fix:** Provide a disassembly sequence with a measured disassembly time and a separated-material recovery route, or formally record shredding-only disposal with its recovery yield as the accepted end-of-life outcome.

### F7 — Major — No carbon or energy target, number, or measurement method
- **Target/material:** carbon / energy (spec §5).
- **Evidence:** spec §5 contains one sustainability target only (recycled aluminium); there is no embodied-carbon target, no use-phase energy target, no number, and no measurement method, despite a 10,000-hour service life (§1) and a 1.5 A/phase, 12 V nominal rating (§2).
- **Fix:** Set a measurable embodied-carbon and use-phase energy target per unit, with the calculation method and the evidence required to close it.

### F8 — Minor — Process energy treated as "none" because the motor is bought in
- **Target/material:** manufacturing process energy, bought-in motor (spec §3).
- **Evidence:** spec §3 states "Process: none — bought-in motor", which accounts for no manufacturing energy at all, although steel lamination, copper winding, aluminium end-cap, and NdFeB magnet production are the energy-intensive steps of this part.
- **Fix:** Obtain per-unit manufacturing energy / embodied-carbon data from the supplier instead of recording the process as none.

### F9 — Minor — Mating pulley aluminium excluded from the sustainability scope
- **Target/material:** aluminium timing pulley, 36 tooth (spec §2; STEP product name "Aluminum Timing Pulley", 1 solid, 5,106.7 mm³).
- **Evidence:** the pulley is aluminium and part of the delivered assembly, but §5 gives no grade, no recycled-content figure, and no RoHS status for it — the recycled-content target covers the motor end caps only.
- **Fix:** Add the pulley aluminium grade and recycled-content figure to §5, or explicitly record it as out of scope with a reason.

### F10 — Minor — 10,000-hour life with no repairability or spare-part provision
- **Target/material:** whole motor, 10,000-hour service life (spec §1).
- **Evidence:** spec §1 requires 10,000 hours without service, §5 states the motor is not designed for disassembly, and no replaceable part, repair route, or spare is named anywhere in the spec, so a failed motor is whole-unit scrap.
- **Fix:** Name the replaceable parts and repair route, or record whole-unit replacement as the accepted waste stream for a failure.

## UNVERIFIED

- Supplier datasheet values (holding torque, current, insulation class) are stated in spec §9 as not on file; they were not checked and are not asserted here.
- The RoHS claim (F2) is UNVERIFIED, not disproved — no certificate was available to check.
- No recycled-content figure for any material could be verified from the model files, which carry no material data.

## Controls passed

- **End-of-life statement is consistent with the material list:** spec §5's statement that the motor is a mixed-material assembly requiring shredding is consistent with the five materials named in §3/§5 (steel, copper, aluminium, magnets, insulation) and with the 5-solid mixed assembly measured in `nema17.step` — no false disassembly or recyclability claim is made.
- **No false recycled-content claim is made for the end caps:** spec §5 discloses the end caps as virgin aluminium rather than asserting recycled content it does not have.
- **No disassembly time is claimed:** the spec makes no disassembly-time claim that the joining methods contradict, because no disassembly time is stated at all (the absence is recorded as F6, not as a contradicted claim).
- **Pulley material identity checks out:** the mating part is aluminium as implied by the spec's integration, confirmed by the STEP product name "Aluminum Timing Pulley" and the single-solid aluminium part measured at 5,106.7 mm³.
- **All CAD-cited dimensions check out:** body 42.30 × 35.00 × 42.30 mm, overall length 55.00 mm, shaft Ø5.00 mm × 24.0 mm with 20.0 mm protrusion, D-flat 0.5 mm deep × 17.75 mm long, mounting holes 4× Ø3.07 mm on 31.0 mm pitch, pilot recess Ø22.0 mm × 2.2 mm deep, front cap opening Ø10.0 mm, pulley bore Ø5.00 mm, 36 teeth — all confirmed by re-measurement of both STEP files.
