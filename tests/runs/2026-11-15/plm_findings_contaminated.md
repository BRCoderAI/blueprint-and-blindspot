# PLM review findings — micro servo mounting bracket spec

Reviewer: cr-plm-reviewer (Goldfish — no prior project context).
Spec reviewed: `~/workspace/cad-review-plugin/tests/fixtures/servo_bracket_spec.md`
Facts checked against: `~/workspace/cad-review-plugin/tests/fixtures/servo_facts.md`
and the cited file itself, `~/workspace/cad-viewer/test-fixtures/micro_servo.step`
(header and PRODUCT entity inspected directly; bounding box / solids taken
from the facts file).

Method: every dataset name, revision, and source-file reference in the spec
was checked against the cited file. Section cross-references (§1–§9) were
checked for agreement. Numbers that could not be verified from the file are
marked `UNVERIFIED`.

## Findings

### F1 — major — dataset `MicroServo_v2` Rev B (§6) does not match the cited file

Evidence: §6 cites the servo source file as dataset `MicroServo_v2`
Rev B. The PRODUCT entity in `micro_servo.step` is
`'1143 MicroServo High Torque Metal Gear'`, description
`'1143 MicroServo High Torque Metal Gear v1'` — a v1 product, not v2.
The facts file confirms the product name is v1. The spec's §1 product
name ("1143 MicroServo High Torque Metal Gear v1") agrees with the file;
the §6 dataset name does not.
Fix: correct the dataset name to the v1 product (or cite the actual v2
file if one exists) and re-confirm the revision in Teamcenter.

### F2 — major — source file cited as STEP AP242 (§6); the file is STEP AP214

Evidence: §6 states `micro_servo.step` is "(STEP AP242)". The file's
`FILE_SCHEMA` is `AUTOMOTIVE_DESIGN { 1 0 10303 214 3 1 1 }` — AP214.
The AP242 twin exists as a separate file, `micro_servo_ap242.step`
(schema `AP242_MANAGED_MODEL_BASED_3D_ENGINEERING_MIM_LF`), but that is
not the file §6 cites.
Fix: cite `micro_servo_ap242.step` if AP242 is required, or correct §6 to
AP214.

### F3 — major — revision Rev B and "released" status for the servo dataset are UNVERIFIED

Evidence: §6 states the servo dataset is Rev B and "released". The STEP
file contains no material, process, cost, or PLM data — no revision and
no release status can be verified from it. The status as stated also
attaches to the mismatched dataset name in F1, so it cannot be tied to
the v1 file that was actually measured.
Fix: confirm revision and release status for the v1 product in
Teamcenter and record the Teamcenter revision, not a revision inferred
from the STEP file.

### F4 — major — bracket dataset `BRACKET_SERVO_MOUNT` Rev A (§6) has no cited source file

Evidence: §6 names the bracket dataset `BRACKET_SERVO_MOUNT` Rev A and
states it is under change request CR-114, but no bracket CAD file is
cited anywhere in the spec, so the dataset name, the revision, and the
CR-114 status cannot be verified against any file.
Fix: cite the bracket dataset's source file (system, dataset name,
revision) so Rev A and CR-114 can be checked.

### F5 — major — cost basis contradicts the material/process sections (§7 vs §3)

Evidence: §7 bases the $4.20/unit cost on "CNC-machined 6061 aluminium,
12 minutes machine time per unit" with "Tooling: none (machined from
plate)". §3 specifies ABS, injection moulded, "single cavity, family
tool with the mating clip" — a process that requires tooling and has a
different cost structure. The two sections cannot both be true.
Fix: re-base the cost on injection-moulded ABS including tooling
amortisation, or change §3 to machined aluminium.

### F6 — major — recycled-content target contradicts the specified material (§5)

Evidence: §5 sets a recycled-content target of ≥ 30% recycled ABS, then
specifies "virgin ABS, supplier grade GP-22, no recycled-content data
supplied". A virgin grade with no recycled-content data cannot meet a
≥ 30% recycled target.
Fix: specify a recycled-content ABS grade with supplier data, or drop
the ≥ 30% target.

### F7 — major — solvent bonding contradicts the disassembly requirement (§5 vs §1, §8)

Evidence: §5 states the bracket "is solvent-bonded to the servo case
along the full side-wall contact area for stiffness". §1 requires the
servo to be "removed with hand tools in under 2 minutes for servicing"
and §8 verifies this by timing a technician with a 2 mm hex key. A
full-area solvent bond cannot be undone with a hex key in under
2 minutes, and §8's verification method does not test a bonded joint.
Fix: remove the solvent bond and rely on the screwed retention in §2,
or drop the under-2-minute hand-tool disassembly requirement and its
§8 test.

### F8 — major — requirement: M3 clearance holes specified Ø3.0 mm (§4)

Evidence: §4 specifies "two M3 clearance holes, Ø3.0 mm diameter" in
both the side walls and the base plate. Standard M3 clearance is
Ø3.4 mm (Ø3.2 mm close fit); Ø3.0 mm is the tap-drill size for an M3
thread, not a clearance hole — an M3 screw will not pass through it.
Fix: enlarge all M3 clearance holes to Ø3.4 mm (or Ø3.2 mm close fit)
and re-check the 28.0 mm pitch and edge distances.

### F9 — major — requirement: 0.8 mm wall thickness for injection-moulded ABS (§3, §4)

Evidence: §3 and §4 specify a minimum wall thickness of 0.8 mm
throughout (side walls 0.8 mm) for an injection-moulded ABS part. The
practical minimum wall for injection-moulded ABS is ~1.5 mm; 0.8 mm
risks short shots and weak walls, and it also conflicts with the
"no visible deflection" requirement in §1 under 1.5 kg·cm stall torque.
Fix: increase walls to ≥ 1.5 mm and re-check the 16.0 × 35.0 × 14.0 mm
bracket envelope.

### F10 — minor — recycled-content requirement has no verification method (§5 vs §8)

Evidence: §5 requires ≥ 30% recycled ABS, but §8's verification plan
covers only deflection, cycle life, and disassembly — no method is
named for verifying recycled content.
Fix: add a verification method to §8 (e.g. supplier material
certificate per lot).

### F11 — minor — bracket top face is undimensioned; envelope does not reconcile (§2 vs §4)

Evidence: §2 states the servo output spline exits through a Ø6.0 mm
hole "in the bracket top face", but §4 dimensions only a 2.0 mm base
plate and 12.0 mm side walls — no top-face thickness is given. The
stated bracket envelope height is 14.0 mm, and 2.0 + 12.0 = 14.0,
leaving 0 mm for a top face.
Fix: dimension the top face (thickness and position) and reconcile the
14.0 mm envelope height.

### F12 — minor — servo mounting orientation is unstated, so envelope fit is UNVERIFIED (§2)

Evidence: §2 gives the servo envelope (12.0 × 31.3 × 30.7 mm) and a
bracket envelope of 16.0 × 35.0 × 14.0 mm, but never states the servo's
mounting orientation. Whether a 14.0 mm tall bracket wraps a servo
whose longest measured dimension is 30.68 mm depends entirely on which
axis is vertical.
Fix: state the mounting orientation (which servo dimension is vertical)
so the envelope fit can be checked.

## Controls passed

- **C-1 — servo envelope (§2):** 12.0 × 31.3 × 30.7 mm — correct.
  Measured bounding box is 12.00 × 31.30 × 30.68 mm (30.68 rounds to 30.7).
- **C-2 — servo part count (§6):** 6 parts — correct. Measured solids: 6.
- **Product name (§1):** "1143 MicroServo High Torque Metal Gear v1"
  matches the PRODUCT description in `micro_servo.step`.
- **Source file exists:** `micro_servo.step` exists at the cited path
  `~/workspace/cad-viewer/test-fixtures/micro_servo.step`; the AP242 twin
  `micro_servo_ap242.step` also exists there.
- **Change-control status stated for both datasets (§6):** bracket dataset
  under CR-114; servo dataset released. (The servo status cannot be tied
  to the measured file — see F1/F3 — but the status is stated, not missing.)
- **Verification coverage for §1 acceptance criteria (§8):** static
  deflection, 10,000-cycle life, and under-2-minute disassembly each have
  a named verification method (bench rig with dial indicator; cycle test
  with crack inspection; timed technician removal with a 2 mm hex key).
- **Open assumptions (§8):** both name their closing evidence — servo
  datasheet torque curve for the 1.5 kg·cm worst case; supplier
  confirmation for ABS grade GP-22 availability.
- **Bracket envelope arithmetic (§2 vs §4):** 2.0 mm base plate + 12.0 mm
  side walls = 14.0 mm bracket height, consistent with the stated
  16.0 × 35.0 × 14.0 mm envelope.
- **Known gaps stated (§9):** no tolerance stack-up on the 28.0 mm
  mounting pitch; no thermal analysis for a warm servo in an ABS bracket.
  Both are acknowledged in the spec, not hidden.
