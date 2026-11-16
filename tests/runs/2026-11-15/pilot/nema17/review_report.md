# Merged design review report — NEMA-17 stepper motor integration, extruder drive

Sources merged: comprehension, DFM, cost, sustainability, and PLM stage
reports (pilot run, 2026-11-15). Only the stage reports were used; no
drafting conversation, spec, or CAD file was consulted directly. Where
two stages disagreed, the disagreement is stated in the finding — no
side was silently picked.

## Verdict: NOT READY

8 blockers. The design cannot be built, procured, or accepted as
specified: three mating fits have zero clearance/interference, the
recycled-content requirement contradicts the stated material, the
holding-torque requirement and the locating-boss interface are
unverified, the tolerance scheme is unusable, the mounting holes are
undersize for M3 screws, and the cited motor dataset revision does not
match the measured file.

## Findings

69 raw findings across the five stages merged into 53 findings below
(16 duplicate instances absorbed; DFM Minor 3 was split across two
merged findings because it covers both recycled content and RoHS).

### Blockers (8)

**B1 — Pilot recess and locating boss have the same nominal diameter:
Ø22.0 mm = Ø22.0 mm, zero clearance**
- Stages: comprehension (B1), DFM (Blocker 2).
- Target: Ø22.0 mm pilot recess, 2.2 mm deep (§2) / Ø22.0 mm locating
  boss on the mounting plate (§2).
- Evidence: "Centering: Ø22.0 mm pilot recess on the front face,
  2.2 mm deep, receives the Ø22.0 mm locating boss on the mounting
  plate." Recess re-measured Ø22.0 mm; boss not in either model file
  (open assumption §8(2)). The §4 ±0.1 mm tolerance on each side
  allows up to 0.20 mm interference.
- Fix: state the recess tolerance, the boss tolerance, and the fit
  (clearance range), and state the boss height against the 2.2 mm
  recess depth; obtain the mounting-plate drawing.

**B2 — Pulley bore and shaft have the same nominal diameter:
Ø5.00 mm = Ø5.00 mm, zero interference for a claimed press fit**
- Stages: comprehension (B2), DFM (Blocker 3).
- Target: shaft Ø5.00 mm (§2, §4) / GT2 pulley bore Ø5.00 mm (§2).
- Evidence: bore re-measured Ø5.00 mm (single cylindrical face);
  shaft re-measured Ø5.00 mm. §9: "Pulley retention relies on a press
  fit onto the D-flat shaft." No interference range, fit class, or
  bore/shaft tolerance is given; the §4 ±0.1 mm tolerance allows
  anything from 0.20 mm clearance to 0.20 mm interference.
- Fix: state shaft tolerance, bore tolerance, and the intended
  interference range; state the D-flat's effect on that interference.

**B3 — Recycled-content requirement contradicts the stated material:
≥20% recycled vs virgin aluminium**
- Stages: comprehension (B3, blocker), DFM (Minor 3, in part),
  cost (B1, blocker), sustainability (F1, blocker), PLM (major).
- Target: end-cap aluminium, recycled content (§5).
- Evidence: "Recycled-content target: ≥ 20% recycled aluminium in
  the end caps" and, in the same section, "Material: end caps are
  virgin aluminium, no recycled-content data supplied." Virgin
  aluminium is 0% recycled content against a ≥20% target. Cost
  adds: the $12.80 priced motor is therefore the non-compliant
  configuration, so the $14.50 target is priced on a motor that does
  not meet the spec.
- Disagreement: PLM graded this major and DFM graded its part of it
  minor; comprehension, cost, and sustainability graded it blocker.
  Ranked blocker: the two lines in one section cannot both be
  satisfied, and the cost basis depends on which governs.
- Fix: state which line governs, state the required recycled-content
  value and its verification method, and re-price the motor against a
  compliant supply, re-baselining the $14.50 target.

**B4 — Holding-torque requirement is unverified: supplier datasheet
is not on file**
- Stages: comprehension (B4).
- Target: holding torque ≥ 40 N·cm (§1, §8).
- Evidence: §8 open assumption (1): "holding torque ≥ 40 N·cm is
  the worst case — closing evidence: supplier datasheet torque curve
  [TO BE OBTAINED]"; §9: "No supplier datasheet on file: torque,
  current, and insulation class are requirements, not verified values."
- Fix: obtain the datasheet torque curve and record the verified
  torque at 1.5 A/phase, or replace the requirement with a measured
  value.

**B5 — Locating-boss interface is unverified: mounting-plate drawing
is not on file**
- Stages: comprehension (B5).
- Target: Ø22.0 mm locating boss on the mounting plate (§2, §8).
- Evidence: §8 open assumption (2): "the Ø22.0 mm locating boss on
  the mounting plate exists at the stated diameter — closing
  evidence: mounting plate drawing [TO BE OBTAINED]." Boss diameter,
  boss height, and boss tolerance are all missing from this spec.
  Related: M17 (plate undefined as a manufactured part) and M18
  (plate dataset status contradiction).
- Fix: obtain the mounting-plate drawing and copy the boss diameter,
  height, and tolerance into this spec.

**B6 — Tolerance rule is unusable: no dimension is classified driving
vs free, and no datum is stated**
- Stages: comprehension (B6, blocker), DFM (Major 3).
- Target: all §4 dimensions; "All driving dimensions toleranced
  ±0.1 mm; free dimensions ±0.25 mm" (§4).
- Evidence: the spec never says which dimensions are driving and
  which are free, and no datum system is stated for any tolerance.
  The blanket tolerance is what turns the three zero-clearance fits
  (B1, B2, B7) into possible interference, and the §1 shaft runout
  limit of ≤ 0.05 mm is tighter than the general ±0.1 mm with no
  datum stated for the runout.
- Disagreement: comprehension graded this blocker, DFM graded it
  major. Ranked blocker: without a driving/free classification and
  datums, no toleranced dimension in the spec can be applied.
- Fix: list each dimension as driving or free, give its tolerance
  explicitly, and state the datum for each toleranced dimension,
  including a stated runout datum.

**B7 — Mounting holes 4× Ø3.07 mm for M3 screws are undersize**
- Stages: DFM (Blocker 1).
- Target: mounting holes, 4× Ø3.07 mm on 31.0 mm square pitch
  (spec §2, §4).
- Evidence: holes measured Ø3.07 mm at centres (±15.50, ±15.50);
  spec calls for M3 screws through them. ISO 273 medium series M3
  clearance is Ø3.4 mm; Ø3.07 mm is 0.33 mm undersize, leaving
  0.07 mm diametral clearance over a Ø3.0 mm screw, and the §4
  ±0.1 mm tolerance allows a Ø2.97 mm hole — smaller than the screw.
  Related: M2 (holes have no tolerance or position datum).
- Fix: enlarge the clearance holes to Ø3.4 mm, or state that the
  motor holes are threaded M3 and put the Ø3.4 mm clearance in the
  mounting plate instead, correcting the screw path in §2.

**B8 — Cited motor dataset revision does not match the measured file:
`NEMA17_MOTOR` Rev B vs "NEMA-17 Stepper Motor v11"**
- Stages: PLM (blocker).
- Target: dataset `NEMA17_MOTOR` Rev B (§6).
- Evidence: the spec cites the motor source file as dataset
  `NEMA17_MOTOR` Rev B, but the file's product version is
  "NEMA-17 Stepper Motor v11" — the cited revision does not match
  the file, so the spec cannot be traced to the measured model.
  Related: M14 (which dataset/revision governs).
- Fix: correct the cited revision to the file's version (v11), or
  cite the dataset revision that actually matches the measured file.

### Majors (33)

**M1 — Shaft has two different lengths with no explanation:
24.0 mm long (§4) vs 20.0 mm protrusion (§2, §4)**
- Stages: comprehension (M1).
- Target: shaft length (§2, §4).
- Evidence: "Shaft: Ø5.00 mm, protrudes 20.0 mm beyond the front
  face"; "Shaft: Ø5.00 mm × 24.0 mm long, 20.0 mm protrusion." The
  4.0 mm difference is never explained (embedded length inside the
  body is assumed, not stated).
- Fix: state the shaft total length, the protrusion, and the datum
  each is measured from (front face vs shaft end vs internal
  shoulder).

**M2 — Mounting holes have no tolerance and no position datum:
4× Ø3.07 mm on 31.0 mm pitch**
- Stages: comprehension (M2).
- Target: mounting holes 4× Ø3.07 mm, 31.0 mm square pitch (§2, §4).
- Evidence: no hole-diameter tolerance, no pitch tolerance, no
  position tolerance, and no stated centre (pilot-recess centre is
  assumed, not stated). M3 through a Ø3.07 mm hole leaves 0.07 mm
  diametral clearance, so pitch error alone can prevent assembly.
  Related: B7 (holes undersize for M3).
- Fix: give hole tolerance, pitch tolerance, position tolerance, and
  the datum the pitch is measured from.

**M3 — D-flat orientation and flat width are missing**
- Stages: comprehension (M3).
- Target: D-flat, 0.5 mm deep × 17.75 mm long (§2, §4).
- Evidence: "D-flat: 0.5 mm deep, 17.75 mm long, starting 2.0 mm
  from the front face." No angular orientation of the flat relative
  to any datum and no flat width (chord width) are given.
- Fix: state the flat width and its angular orientation with a datum.

**M4 — Body dimensions do not label which axis is axial:
42.30 × 35.00 × 42.30 mm**
- Stages: comprehension (M4).
- Target: motor body 42.30 × 35.00 × 42.30 mm (§2, §4).
- Evidence: "Motor body: 42.30 × 35.00 × 42.30 mm." The spec never
  labels which number is the axial length; the reader must infer
  that 35.00 mm is axial because 35.00 + 20.0 = 55.00 mm overall
  length. The two 42.30 mm faces are also not distinguished (front
  vs side).
- Fix: label each dimension (axial length × width × height) and state
  which face is the front face.

**M5 — GT2 pulley is undefined and its hub is undimensioned**
- Stages: comprehension (M5).
- Target: GT2 timing pulley, 36 tooth (§1, §2).
- Evidence: "GT2" is never defined (tooth pitch, tooth profile, and
  belt width are not stated), and no pulley dimension beyond bore is
  given — no hub diameter, hub length, overall pulley width, or
  pulley material. (DFM measured hub Ø16.00 × 7.0 mm, tip Ø22.40 mm,
  root Ø20.00 mm, flanges 2× Ø25.50 mm × 1.5 mm — none of which the
  spec states.)
- Fix: define the GT2 tooth pitch/profile and belt width, and
  dimension the pulley hub (diameter, length) and material.

**M6 — M3 mounting screws are undimensioned: no length, grade, head,
or tightening torque**
- Stages: comprehension (M6).
- Target: four M3 screws (§2).
- Evidence: "Mounting: four M3 screws through the Ø3.07 mm mounting
  holes on a 31.0 mm square pitch, into the extruder mounting plate."
  Screw length, thread engagement, strength grade, head type, and
  tightening torque are all missing; mounting-plate thickness is also
  missing, so screw length cannot be derived.
- Fix: state screw length, grade, head type, minimum thread
  engagement, and tightening torque, plus mounting-plate thickness.

**M7 — Electrical interface is incomplete: 4-wire, 1.5 A/phase, 12 V,
with no leads or connector**
- Stages: comprehension (M7).
- Target: electrical interface, 4-wire (§2).
- Evidence: "Electrical: 4-wire, 1.5 A/phase rated, 12 V nominal."
  Lead length, wire gauge, connector type, and pinout/phase order are
  not stated. Related: M22 (the 1.5 A/phase and 12 V ratings
  themselves are unverified).
- Fix: state lead length, wire gauge, connector part/type, and the
  pinout for the four wires.

**M8 — Materials have no grades and no source: steel, aluminium,
copper, NdFeB named without specification**
- Stages: comprehension (M8), PLM (minor, material composition).
- Target: steel stator laminations, aluminium end caps, copper
  windings, NdFeB rotor magnets (§3).
- Evidence: "Purchased assembly, not manufactured in-house: steel
  stator laminations, aluminium end caps, copper windings, NdFeB
  rotor magnets." No alloy, grade, temper, or magnet grade/coating is
  given for any of the four materials; the composition is not
  verifiable from the STEP file and no supplier datasheet is on file
  (§9). Related: M29–M31 (sustainability data gaps for the same
  materials).
- Fix: state the grade/specification for each material (aluminium
  alloy and temper, steel lamination grade, magnet grade and coating)
  and cite the supplier datasheet or material declaration.

**M9 — Step-accuracy test does not measure the stated acceptance:
per-step ±5% (§1) vs 200-step cumulative test (§8)**
- Stages: comprehension (M9).
- Target: step angle 1.8° ± 5% per step (§1); step-accuracy
  verification (§8).
- Evidence: "step angle 1.8° ± 5% per step"; "Step accuracy: index
  200 steps, measure shaft angle with an encoder." Indexing 200 steps
  and measuring total angle measures cumulative angle (360°
  nominal), not per-step error. Encoder resolution/accuracy is also
  not stated.
- Fix: state a per-step measurement method and the encoder
  resolution/accuracy required.

**M10 — Thermal acceptance and installed condition conflict, and the
measurement point is missing**
- Stages: comprehension (M10).
- Target: case temperature ≤ 80 °C (§1); thermal verification (§8);
  mounting against the extruder heat sink (§9).
- Evidence: "motor case temperature ≤ 80 °C after 1 hour at rated
  current in 25 °C still air"; "Thermal: run 1 hour at rated current,
  measure case temperature with a thermocouple"; "the motor runs warm
  and sits against an aluminium mounting plate that is also the
  extruder heat sink." The §1 acceptance is in still air, but the
  installed motor sits against a heat sink, which changes the
  temperature — the spec never says which condition governs. The
  thermocouple location on the case is also not stated.
- Fix: state whether the ≤80 °C limit applies unmounted in still air
  or mounted to the plate, and state the thermocouple location on the
  case.

**M11 — Service life has no verification: 10,000 hours without
service, no life test in §8**
- Stages: comprehension (M11), PLM (major).
- Target: 10,000-hour service life (§1).
- Evidence: "run for 10,000 hours without service"; §8 lists
  holding-torque, step-accuracy, fit-check, and thermal tests only —
  no life, endurance, or bearing-wear test, and no life test,
  accelerated test, or supplier data is named. "Without service" is
  also undefined (what counts as service, what failure ends the
  life). Related: m11 (no repairability or spare-part provision).
- Fix: define service/failure for the life requirement and state the
  life verification method (test duration, sample size, or accepted
  accelerated/analysis basis).

**M12 — Shaft runout tolerance has no datum: ≤ 0.05 mm at the pulley
hub**
- Stages: comprehension (M12).
- Target: shaft runout ≤ 0.05 mm (§1).
- Evidence: "shaft runout ≤ 0.05 mm measured at the pulley hub." The
  datum axis the runout is measured about (shaft axis, pilot-recess
  axis, or mounting-face datum) is not stated, and the axial position
  along the hub is not stated.
- Fix: state the runout datum axis and the measurement position along
  the pulley hub.

**M13 — Pilot-recess depth vs boss height: boss height is missing,
bottoming risk is unstated**
- Stages: comprehension (M13).
- Target: pilot recess 2.2 mm deep (§2); locating boss height
  (missing).
- Evidence: "Ø22.0 mm pilot recess on the front face, 2.2 mm deep,
  receives the Ø22.0 mm locating boss on the mounting plate." The
  boss height is never given. If the boss is taller than 2.2 mm, the
  motor will not seat against the plate; if shorter, centring
  engagement is unknown.
- Fix: state the boss height and its tolerance against the 2.2 mm
  recess depth.

**M14 — Dataset authority is ambiguous: NEMA17_EXTRUDER Rev C vs
NEMA17_MOTOR Rev B, and 5 solids are unnamed**
- Stages: comprehension (M14, major), PLM (major, NEMA17_EXTRUDER
  Rev C).
- Target: datasets NEMA17_EXTRUDER Rev C and NEMA17_MOTOR Rev B
  (§6); motor part count 5 solids (§6).
- Evidence: "CAD system: Siemens NX, dataset `NEMA17_EXTRUDER`
  Rev C"; "Motor source file: `nema17.step` (STEP AP214), dataset
  `NEMA17_MOTOR` Rev B"; "Motor part count: 5 solids." Two datasets
  at two revisions are named for the same motor with no statement of
  which is authoritative or how they relate, and the 5 solids are not
  named. PLM adds: the top-level assembly dataset Rev C is cited with
  no source file, no product name, no part count and no envelope, so
  Rev C cannot be verified against any file. Related: B8 (Rev B does
  not match the file's v11) and M19 (NX provenance claim).
- Fix: state which dataset/revision governs, the relationship between
  the two, cite the assembly file with its measured contents (or
  remove the revision claim), and name the 5 solids.

**M15 — D-flat has no mating feature in the pulley: retention is
press-fit-only against a ≥ 40 N·cm requirement**
- Stages: DFM (Major 1), PLM (major, pulley retention interface).
- Target: shaft D-flat, 0.5 mm deep × 17.75 mm long (spec §2, §4) /
  pulley bore.
- Evidence: flat verified in the motor (plane at Z = 2.00,
  Y 20.50..38.25); the pulley bore is a plain Ø5.00 mm cylinder with
  no flat, no keyway and no set-screw hole (single Ø5.00 mm cylinder,
  no other bore feature), and spec §9 admits the hub carries no set
  screw. A round bore cannot engage a flat, so the flat transmits no
  torque and retention is press-fit-only against the §1 holding-torque
  requirement of ≥ 40 N·cm, with no torque capacity stated or tested;
  shaft and bore are both stated Ø5.00 with no interference value.
  Related: B2 (the press fit itself has no interference).
- Fix: add a matching flat in the pulley bore, or a set screw in the
  Ø16.00 × 7.0 mm hub, specify the bore/shaft interference, and prove
  the retention torque by test.

**M16 — Pulley axial position and retention undefined**
- Stages: DFM (Major 2).
- Target: pulley axial location on the shaft (spec §2, §8 fit check).
- Evidence: shaft protrudes 20.0 mm beyond the front face while the
  pulley is 17.0 mm tall overall, so 3.0 mm of shaft stands proud if
  the pulley seats on the front face, and the spec states no seating
  face, shoulder, stop or axial retention feature.
- Fix: define the seating face and axial position of the pulley on the
  shaft and add an axial retention feature.

**M17 — Mounting plate, the only part to be manufactured, is
undefined**
- Stages: DFM (Major 4).
- Target: extruder mounting plate (spec §2, §3).
- Evidence: the plate carries the Ø22.0 mm locating boss, the mating
  M3 holes and the extruder heat-sink interface, but the spec gives it
  no material, no process, no dimensions and no drawing (boss
  existence is open assumption §8(2)); §3 states no moulded or
  machined features are defined by this spec. With no process or
  material stated, no process limit can be checked — including the
  Protolabs ABS wall range of 1.14–3.56 mm, the 1° draft rule and the
  40–60% rib/boss rule, none of which has a target in this document.
  Related: B5 (boss unverified) and M18 (plate dataset status).
- Fix: issue the mounting plate drawing with material, process and
  toleranced dimensions so its features can be checked against that
  process's limits.

**M18 — Mounting plate dataset is stated "released" but its drawing
is not on file: status contradiction**
- Stages: PLM (major).
- Target: mounting plate dataset (§6 vs §8).
- Evidence: the mounting plate dataset is stated "released" but is
  never named, has no revision and no cited file, and §8 assumption
  (2) says its drawing is still TO BE OBTAINED — a released dataset
  whose drawing is not on file is a contradiction. Related: B5 and
  M17.
- Fix: name the dataset and revision and put its drawing on file, or
  change its status to unreleased.

**M19 — CAD-system / dataset provenance: spec claims Siemens NX, file
is an Adafruit vendor import**
- Stages: PLM (major).
- Target: CAD system / dataset provenance (§6).
- Evidence: the spec claims the motor is a Siemens NX dataset, but
  `nema17.step` is authored by Adafruit (FILE_NAME path is an
  Adafruit Dropbox folder, generated by STEP Tools ST-Developer,
  2018-07-07) and contains zero references to NX or Siemens.
  Related: M14 (dataset authority).
- Fix: record the motor as a vendor-supplied Adafruit STEP import,
  not an NX-authored dataset, and name the import record.

**M20 — Timing pulley has no dataset: cited only by filename**
- Stages: PLM (major).
- Target: timing pulley dataset (§2, §6).
- Evidence: the mating part is cited only by filename
  (`timing_pulley.step`); it has no dataset name, no revision and no
  change-control status, although the file's product is "Aluminum
  Timing Pulley v1".
- Fix: assign the pulley a dataset name and revision and state its
  change-control status.

**M21 — Change-request status unstated: CR-207**
- Stages: comprehension (m6, minor), PLM (major).
- Target: change request CR-207 (§6).
- Evidence: "Change control: motor dataset under change request
  CR-207; mounting plate dataset released." The status and effect of
  CR-207 are not stated (open, approved, what it changes), and no
  statement is made of which revision CR-207 applies to, while the
  spec depends on the cited revision for acceptance — so a stranger
  cannot tell whether the motor dataset as specified is released for
  build.
- Disagreement: comprehension graded this minor, PLM graded it
  major. Ranked major: the build/release status of the motor dataset
  is a driving fact, not a clarity issue.
- Fix: state the CR-207 status and whether the motor dataset is
  released, frozen, or under change, and whether the cited revision
  is pre- or post-change.

**M22 — Electrical ratings unverified: 1.5 A/phase and 12 V have no
verification method and no datasheet on file**
- Stages: PLM (major).
- Target: electrical ratings (§2 vs §8, §9).
- Evidence: 1.5 A/phase and 12 V nominal are stated with no
  verification method in §8, and §9 admits current is a requirement,
  not a verified value, with no supplier datasheet on file. Related:
  B4 (holding torque unverified on the same missing datasheet) and
  M7 (electrical interface incomplete).
- Fix: add a verification method (supplier datasheet on file) or mark
  the ratings as assumptions with named closing evidence.

**M23 — $12.80 motor price (88% of the $14.50 target) is an unsourced
engineer estimate**
- Stages: cost (M1, major), PLM (minor, cost basis).
- Target: $12.80 purchased motor price (§7).
- Evidence: §7 gives no supplier, no quote, and no validity date for
  the $12.80 motor price, and §9 admits no supplier datasheet is on
  file, so torque, current and insulation class — the ratings the
  price must cover — are unverified requirements, not confirmed
  values.
- Disagreement: cost graded this major, PLM graded it minor. Ranked
  major: the dominant line item of the target has no source.
- Fix: obtain a written supplier quote tied to a datasheet that
  confirms the §1 ratings, and cite it in §7.

**M24 — The required GT2 pulley is missing from the cost basis
entirely**
- Stages: cost (M2).
- Target: GT2 pulley cost (§7 vs §1, §2).
- Evidence: §1 defines the drive as motor plus 36-tooth GT2 timing
  pulley on the shaft, and the pulley model confirms an aluminium
  part (bore Ø5.00 mm, 36 teeth, 25.50 mm envelope), yet §7's basis
  is motor $12.80 + mounting hardware $1.70 only — the pulley's
  purchase cost is $0 in a target that claims to cover the extruder
  drive unit.
- Fix: add the pulley as a priced line item in §7 or state explicitly
  that the $14.50 target excludes it and where its cost sits.

**M25 — Neither line price is stated at the 1,000-unit quantity**
- Stages: cost (M3).
- Target: $12.80 motor price and $1.70 hardware price (§7).
- Evidence: §7 states the $14.50 target "at 1,000 units", but neither
  the $12.80 motor price nor the $1.70 hardware price is stated as a
  1,000-unit price, and there is no volume break, minimum order
  quantity, or quote validity period — if $12.80 is a list or
  single-unit price, the 1,000-unit target is ungrounded.
- Fix: state both line prices explicitly as 1,000-unit prices with the
  quote's validity dates.

**M26 — No cost driver is named for a target that is 88% one
bought-in part**
- Stages: cost (M4).
- Target: $12.80 motor price, cost drivers (§7 vs §3).
- Evidence: §7 names no cost driver and carries no contingency, while
  §3 identifies the motor's cost-relevant contents as NdFeB rotor
  magnets and copper windings — the two volatile inputs — so the
  dominant line item has no sensitivity analysis and no allowance for
  magnet or copper price movement.
- Fix: add a driver breakdown for the $12.80 (magnets, copper, steel,
  aluminium) with a stated contingency or price-validity window.

**M27 — The ±0.1 mm tolerances and ≤0.05 mm runout carry no cost**
- Stages: cost (M5).
- Target: §4 tolerances and §1 runout vs §7 cost basis.
- Evidence: §4 imposes ±0.1 mm on all driving dimensions and §1
  requires shaft runout ≤0.05 mm at the pulley hub, but the $12.80
  prices a bought-in motor with no datasheet on file (§9) proving a
  standard motor meets those limits — a screened, selected, or
  premium-grade motor, and the incoming inspection to enforce the
  limits, are costed at $0.
- Fix: confirm the quoted motor meets the §4 tolerances and §1 runout
  or add the screening/premium cost to §7.

**M28 — RoHS compliance claimed with no certificate on file**
- Stages: sustainability (F2, major), comprehension (m3, minor), DFM
  (Minor 3, in part), PLM (minor).
- Target: RoHS compliance for the whole motor assembly (§5).
- Evidence: §5 claims supplier RoHS compliance but states the
  certificate is not on file; no restricted-substance declaration,
  test report, or declaration of conformity is cited anywhere in the
  spec, and §8 contains no verification step for it.
- Disagreement: sustainability graded this major; comprehension, DFM,
  and PLM graded it minor. Ranked major: a compliance claim with no
  evidence and no acceptance criterion cannot be accepted against
  the spec.
- Fix: obtain and file the supplier RoHS certificate / declaration of
  conformity for this exact motor before acceptance, or add a
  verification step to §8.

**M29 — NdFeB rotor magnets: no grade, recycled content, REACH
status, or recovery route**
- Stages: sustainability (F3).
- Target: NdFeB rotor magnets (§3, §5).
- Evidence: §3 names NdFeB magnets and gives no grade, no
  recycled-content figure, no REACH/restricted-substance status, and
  §5 states material recovery requires shredding, which loses
  rare-earth magnets into mixed shredder output with no recovery
  route named. Related: M8 (no magnet grade).
- Fix: obtain the magnet grade, recycled-content and REACH data from
  the supplier and name a rare-earth recovery or take-back route, or
  record shredding loss as an accepted impact.

**M30 — Steel stator laminations and copper windings: no grade,
recycled content, or material-health data**
- Stages: sustainability (F4).
- Target: steel stator laminations, copper windings (§3, §5).
- Evidence: §3 names both materials with no grade, no
  recycled-content percentage or source, and no REACH/RoHS status
  for either; §5 sets a recycled-content target only for aluminium,
  so steel and copper have no target and no data at all. Related:
  M8 (no steel/copper grade).
- Fix: obtain grade, recycled-content percentage with source, and
  restricted-substance status for the steel and copper from the
  supplier and set or explicitly waive a target for each.

**M31 — Insulation material unnamed, with no material-health data**
- Stages: sustainability (F5).
- Target: winding insulation (§5 end-of-life list).
- Evidence: §5 lists insulation as one of the mixed materials at end
  of life, but no insulation material is named anywhere in §3 or §5,
  and no restricted-substance or material-health data is given for
  it. Related: m2 (no required insulation class value).
- Fix: name the insulation material and grade and file its
  restricted-substance / material-health data.

**M32 — End of life: not designed for disassembly, shredding only,
no separation plan or disassembly time**
- Stages: sustainability (F6).
- Target: whole motor assembly — steel, copper, aluminium, magnets,
  insulation (§5).
- Evidence: §5 states the motor is a mixed-material assembly, is not
  designed for disassembly, and material recovery requires shredding;
  no disassembly time is stated, no disassembly sequence is given, no
  material-separation plan exists, and the §8 verification plan
  contains no end-of-life or disassembly test.
- Fix: provide a disassembly sequence with a measured disassembly
  time and a separated-material recovery route, or formally record
  shredding-only disposal with its recovery yield as the accepted
  end-of-life outcome.

**M33 — No carbon or energy target, number, or measurement method**
- Stages: sustainability (F7).
- Target: carbon / energy (§5).
- Evidence: §5 contains one sustainability target only (recycled
  aluminium); there is no embodied-carbon target, no use-phase energy
  target, no number, and no measurement method, despite a 10,000-hour
  service life (§1) and a 1.5 A/phase, 12 V nominal rating (§2).
- Fix: set a measurable embodied-carbon and use-phase energy target
  per unit, with the calculation method and the evidence required to
  close it.

### Minors (12)

**m1 — Abbreviations undefined: NdFeB, AP214, NEMA-17**
- Stages: comprehension (m1).
- Target: "NdFeB rotor magnets" (§3), "STEP AP214" (§6), "NEMA-17"
  (title, §6).
- Evidence: none of the three terms is defined in the spec.
  Dimensions are given for the body, so the NEMA-17 frame size is
  partly mitigated, but NdFeB and AP214 are not expanded anywhere.
- Fix: expand and define each abbreviation on first use.

**m2 — Insulation class: no required value is stated anywhere**
- Stages: comprehension (m2).
- Target: insulation class (§9).
- Evidence: "No supplier datasheet on file: torque, current, and
  insulation class are requirements, not verified values." Insulation
  class is called a requirement, but no required class (e.g. Class
  B/F/H) appears in §1–§8. Related: M31 (insulation material unnamed).
- Fix: state the required insulation class in §1 or §2.

**m3 — Front-cap shaft opening Ø10.0 mm has no tolerance, depth, or
concentricity**
- Stages: comprehension (m4).
- Target: front-cap shaft opening Ø10.0 mm (§2).
- Evidence: "Front cap shaft opening: Ø10.0 mm." No tolerance, no
  depth, and no concentricity to the shaft axis are given. (DFM
  measured 2.5 mm radial clearance around the Ø5.00 mm shaft.)
- Fix: give the opening tolerance, depth, and concentricity to the
  shaft axis.

**m4 — Cost target has no acceptance rule and the hardware cost is
unitemised**
- Stages: comprehension (m5, minor), cost (m1, minor).
- Target: cost target $14.50 per unit at 1,000 units (§7); mounting
  hardware $1.70 (§7).
- Evidence: the spec never says whether $14.50 is a maximum, a target
  with a tolerance, or an estimate, and the $1.70 hardware is not
  itemised (screw count, type, and length are missing — see M6), so
  the basis cannot be checked.
- Fix: state whether $14.50 is a not-to-exceed limit, and itemise the
  $1.70 hardware (screw specification × 4, plus any washers) with a
  price per line.

**m5 — Pilot recess depth datum ambiguous by 0.15 mm**
- Stages: DFM (Minor 1).
- Target: pilot recess depth, 2.2 mm (spec §2, §4).
- Evidence: recess cylinder spans Y 16.15..18.35 (2.20 mm,
  re-measured) but the front face plane is at Y 18.50, so depth
  measured from the face is 2.35 mm. Note: this is a datum ambiguity,
  not a disagreement with the 2.2 mm cylinder length — the cylinder
  itself measures 2.20 mm.
- Fix: dimension the recess depth from the front face plane.

**m6 — Small internal features in the model are undimensioned**
- Stages: DFM (Minor 2).
- Target: undimensioned cylindrical features in `nema17.step`
  (spec §4 silent).
- Evidence: measured Ø1.00 mm (40 faces), Ø2.00 mm (9 faces) and
  Ø2.67 mm (56 faces) cylindrical faces, re-measured; none is
  dimensioned or described in the spec.
- Fix: dimension the functional ones or state in the spec that they
  are non-functional detail carried from the supplier model.

**m7 — §8 acceptance testing has no cost in the $14.50**
- Stages: cost (m2).
- Target: acceptance testing cost (§8 vs §7).
- Evidence: §8 requires a torque-rig stall test, a 200-step encoder
  check, a dial-indicator runout check, and a 1-hour thermal run, but
  §7 contains no inspection, acceptance, or qualification cost — it
  is unstated whether acceptance is per-unit or sampled and who pays
  for it.
- Fix: state the acceptance sampling basis and add its per-unit cost
  (or amortised qualification cost) to §7.

**m8 — The mounting plate's cost scope is unstated**
- Stages: cost (m3).
- Target: mounting plate cost scope (§7 vs §2, §3).
- Evidence: §2 mounts the motor to the extruder mounting plate with
  four M3 screws and §3 notes the plate is a separate part, but §7
  never states whether the $14.50 target excludes the plate — a reader
  cannot tell if the target covers the installed motor or only motor
  plus screws.
- Fix: state explicitly in §7 that the mounting plate is excluded and
  where its cost is carried.

**m9 — Process energy treated as "none" because the motor is bought
in**
- Stages: sustainability (F8).
- Target: manufacturing process energy, bought-in motor (§3).
- Evidence: §3 states "Process: none — bought-in motor", which
  accounts for no manufacturing energy at all, although steel
  lamination, copper winding, aluminium end-cap, and NdFeB magnet
  production are the energy-intensive steps of this part.
- Fix: obtain per-unit manufacturing energy / embodied-carbon data
  from the supplier instead of recording the process as none.

**m10 — Mating pulley aluminium excluded from the sustainability
scope**
- Stages: sustainability (F9).
- Target: aluminium timing pulley, 36 tooth (§2; STEP product name
  "Aluminum Timing Pulley", 1 solid, 5,106.7 mm³).
- Evidence: the pulley is aluminium and part of the delivered
  assembly, but §5 gives no grade, no recycled-content figure, and no
  RoHS status for it — the recycled-content target covers the motor
  end caps only.
- Fix: add the pulley aluminium grade and recycled-content figure to
  §5, or explicitly record it as out of scope with a reason.

**m11 — 10,000-hour life with no repairability or spare-part
provision**
- Stages: sustainability (F10).
- Target: whole motor, 10,000-hour service life (§1).
- Evidence: §1 requires 10,000 hours without service, §5 states the
  motor is not designed for disassembly, and no replaceable part,
  repair route, or spare is named anywhere in the spec, so a failed
  motor is whole-unit scrap. Related: M11 (life has no verification).
- Fix: name the replaceable parts and repair route, or record
  whole-unit replacement as the accepted waste stream for a failure.

**m12 — "Motor part count: 5 solids" misstates the assembly**
- Stages: PLM (minor).
- Target: "Motor part count: 5 solids" (§6).
- Evidence: the file's 5 solids are 4 overlapping body construction
  sections plus the shaft, not 5 separable parts, so calling them the
  part count misstates the assembly. Note: the count of 5 solids is
  itself verified by every stage (see Controls passed); only the
  label "part count" is wrong. Related: M14 (solids unnamed).
- Fix: describe the count as 5 solids in the imported model, not a
  part count.

## Dropped findings (5)

All five were generic findings considered and dropped by the
comprehension stage; no finding was dropped as wrong — no stage's
finding was contradicted by evidence quoted in another stage's report.

- "The spec is unclear in places" — names no feature, dimension,
  tolerance, material, or dataset.
- "More detail is needed on the motor" — names no feature, dimension,
  tolerance, material, or dataset.
- "Undefined terms in general" — names no feature, dimension,
  tolerance, material, or dataset.
- "The verification plan could be stronger" — names no feature,
  dimension, tolerance, material, or dataset.
- "Sustainability needs more work" — names no feature, dimension,
  tolerance, material, or dataset.

## Stage disagreements (not silently resolved)

- **Recycled content (B3):** blocker (comprehension, cost,
  sustainability) vs major (PLM) vs minor (DFM, in part). Ranked
  blocker.
- **Tolerance scheme (B6):** blocker (comprehension) vs major (DFM).
  Ranked blocker.
- **RoHS certificate (M28):** major (sustainability) vs minor
  (comprehension, DFM, PLM). Ranked major.
- **CR-207 status (M21):** minor (comprehension) vs major (PLM).
  Ranked major.
- **$12.80 unsourced price (M23):** major (cost) vs minor (PLM).
  Ranked major.
- **"5 solids" as a part count:** every stage's Controls passed lists
  the 5-solid count as verified, while PLM's minor m12 says calling
  it a "part count" misstates the assembly. Both stand: the count is
  correct, the label is wrong.

## Controls passed: 36 total

Checked-and-correct claims collected from all five stages (5
comprehension + 9 DFM + 4 cost + 5 sustainability + 13 PLM). Many
repeat the same dimension checks across stages; the count below is
the total of the per-stage lists, not a de-duplicated count.

### Comprehension (5)

1. §1 acceptance values are stated as measurable numbers: holding
   torque ≥ 40 N·cm, step angle 1.8° ± 5%, shaft runout ≤ 0.05 mm,
   case temperature ≤ 80 °C after 1 hour at rated current in 25 °C
   still air.
2. §2 overall length is arithmetically consistent with body plus
   protrusion: 35.00 mm + 20.0 mm = 55.00 mm.
3. §4 D-flat start is dimensioned from a stated reference: 2.0 mm
   from the front face.
4. §7 cost arithmetic checks: $12.80 + $1.70 = $14.50.
5. §8 verification methods are named per requirement (bench-rig torque
   meter, encoder, dial indicator, thermocouple), even where the
   methods are incomplete per the findings above.

### DFM (9)

1. Motor body 42.30 × 35.00 × 42.30 mm; overall length with shaft
   55.00 mm; envelope 42.30 × 55.00 × 42.30 mm.
2. Shaft Ø5.00 mm × 24.0 mm long, protruding 20.0 mm beyond the front
   face (front face Y 18.50, shaft tip Y 38.50).
3. D-flat 0.5 mm deep (plane Z = 2.00 against shaft surface Z = 2.50),
   17.75 mm long (Y 20.50..38.25), starting 2.0 mm from the front
   face.
4. Mounting holes 4× Ø3.07 mm on 31.0 mm square pitch (centres
   (±15.50, ±15.50), verified by face positions).
5. Pilot recess Ø22.0 mm; front cap shaft opening Ø10.0 mm.
6. Motor part count 5 solids; total volume 58,681.8 mm³.
7. Pulley: 36 teeth, bore Ø5.00 mm, tip diameter Ø22.40 mm, root
   Ø20.00 mm, flanges 2× Ø25.50 mm × 1.5 mm thick, hub Ø16.00 mm ×
   7.0 mm tall, envelope 25.50 × 17.00 × 25.50 mm, 1 solid,
   volume 5,106.7 mm³.
8. Front cap shaft opening Ø10.0 mm gives 2.5 mm radial clearance
   around the Ø5.00 mm shaft.
9. No number cited from either model was found to disagree with the
   model; nothing required an UNVERIFIED mark — every cited model
   number was re-measured or verified by face position, except the
   mounting plate boss Ø22.0 mm, which is not in either model file
   (open assumption §8(2), not a model claim).

### Cost (4)

1. Arithmetic (§7): $12.80 + $1.70 = $14.50 exactly.
2. Tooling (§3 vs §7): "tooling: none" is consistent with §3
   ("bought-in motor", process none) — no tooling amortisation risk
   at 1,000 units, and no moulding/CNC process mismatch at that
   quantity.
3. Quantity/process fit (§7 vs §3): a bought-in part needs no
   tooling, so the 1,000-unit quantity carries no amortisation
   problem.
4. Costed geometry matches the model (re-measured): body
   42.30 × 35.00 × 42.30 mm, overall length 55.00 mm, shaft Ø5.00 mm
   × 24.0 mm with 20.0 mm protrusion, D-flat 0.5 mm deep × 17.75 mm
   long starting 2.0 mm from the front face, 4× Ø3.07 mm holes on
   31.0 mm pitch, pilot recess Ø22.0 mm × 2.2 mm deep, front cap
   opening Ø10.0 mm, 5 solids, volume 58,681.8 mm³; mating pulley
   bore Ø5.00 mm, 36 teeth, tip Ø22.40 mm, 1 solid, volume
   5,106.7 mm³. No cost figure depends on a dimension the model
   contradicts.

### Sustainability (5)

1. End-of-life statement is consistent with the material list: §5's
   statement that the motor is a mixed-material assembly requiring
   shredding is consistent with the five materials named in §3/§5
   (steel, copper, aluminium, magnets, insulation) and with the
   5-solid mixed assembly measured in `nema17.step` — no false
   disassembly or recyclability claim is made.
2. No false recycled-content claim is made for the end caps: §5
   discloses the end caps as virgin aluminium rather than asserting
   recycled content it does not have.
3. No disassembly time is claimed: the spec makes no disassembly-time
   claim that the joining methods contradict, because no disassembly
   time is stated at all (the absence is recorded as M32, not as a
   contradicted claim).
4. Pulley material identity checks out: the mating part is aluminium
   as implied by the spec's integration, confirmed by the STEP
   product name "Aluminum Timing Pulley" and the single-solid
   aluminium part measured at 5,106.7 mm³.
5. All CAD-cited dimensions check out: body 42.30 × 35.00 ×
   42.30 mm, overall length 55.00 mm, shaft Ø5.00 mm × 24.0 mm with
   20.0 mm protrusion, D-flat 0.5 mm deep × 17.75 mm long, mounting
   holes 4× Ø3.07 mm on 31.0 mm pitch, pilot recess Ø22.0 mm ×
   2.2 mm deep, front cap opening Ø10.0 mm, pulley bore Ø5.00 mm,
   36 teeth — all confirmed by re-measurement of both STEP files.

### PLM (13)

1. Motor body 42.30 × 35.00 × 42.30 mm (§2, §4) — measured body
   Y −16.50..18.50, envelope 42.30 × 55.00 × 42.30 mm.
2. Overall length with shaft 55.00 mm (§2) — measured
   Y −16.50..38.50.
3. Shaft Ø5.00 mm × 24.0 mm long, 20.0 mm protrusion (§2, §4) —
   measured Y 14.50..38.50, front face at Y 18.50.
4. D-flat 0.5 mm deep × 17.75 mm long, starting 2.0 mm from the front
   face (§2, §4) — measured plane Z = 2.00 vs shaft surface
   Z = 2.50, Y 20.50..38.25.
5. Mounting holes 4× Ø3.07 mm on 31.0 mm pitch (§2, §4) — measured
   centres (±15.50, ±15.50).
6. Pilot recess Ø22.0 mm × 2.2 mm deep (§2, §4) — measured.
7. Front cap shaft opening Ø10.0 mm (§2) — measured D10.00.
8. Motor source file format STEP AP214 (§6) — measured header
   `AUTOMOTIVE_DESIGN { 1 0 10303 214 3 1 1 }`.
9. Motor solid count 5 (§6) — measured 5 solids (see minor finding
   m12 on calling this a part count).
10. Pulley 36 tooth, bore Ø5.00 mm (§2) — measured 36 root segments
    Ø20.00 mm and 36 tip segments Ø22.40 mm, bore Ø5.00 mm.
11. Cost arithmetic $12.80 + $1.70 = $14.50 (§7) — agrees.
12. Verification methods named for holding torque, step accuracy,
    runout and thermal (§8) — present.
13. Both open assumptions name their closing evidence (§8) — supplier
    datasheet torque curve, mounting plate drawing, both TO BE
    OBTAINED.

## Counts

- Blockers: 8
- Majors: 33
- Minors: 12
- Total merged findings: 53 (from 69 raw findings; 16 duplicate
  instances absorbed)
- Dropped findings: 5 (all generic; none dropped as wrong)
- Controls passed: 36 (5 comprehension + 9 DFM + 4 cost +
  5 sustainability + 13 PLM)
