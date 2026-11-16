# Comprehension findings — GT2 timing pulley, 36 tooth, aluminium

Reviewer: goldfish (stage 1, comprehension). Read ONLY
`tests/fixtures/timing_pulley_spec.md`. No CAD file, no conversation, no
facts file. Question: could a competent engineer who never saw this
project build the part from this document alone? Answer: no — the
retention mechanism contradicts itself, the tooth geometry is
unbuildable, and the bore fit is specified as clearance while being
called a press fit.

## Blockers

### B1 — Retention contradicts itself: bore has no flat, yet retention "engages the shaft D-flat"
- **Severity:** blocker
- **Target:** bore / shaft D-flat engagement (§2, §9)
- **Evidence:** §2 states "No set-screw hole, no keyway, no flat in the
  bore" and, in the same section, "Retention: press fit onto the motor
  shaft, engaging the shaft D-flat". §9 repeats the contradiction:
  "retention is friction only, on a bore that does not engage the shaft
  D-flat." A round Ø5.00 mm bore cannot engage a D-flat. The torque
  path is undefined.
- **Fix:** Pick one retention mechanism — D-flat in the bore (with flat
  depth, width, and angular orientation), a set screw (size, position,
  torque), or a defined interference fit — and delete the contradicting
  sentence.

### B2 — Bore specified as clearance, called a press fit
- **Severity:** blocker
- **Target:** bore Ø5.00 mm tolerance +0.012/−0.000 (H7) vs shaft
  Ø5.00 mm (§2, §4, §8)
- **Evidence:** §4 gives the bore as "Ø5.00 mm, tolerance +0.012/−0.000
  (H7)"; §2 gives the mating NEMA-17 shaft as "Ø5.00 mm". A bore that
  is never smaller than the shaft is a clearance/slip fit, never a
  press fit. §8 then instructs to "check the pulley slides onto the
  motor shaft with a hand press fit" — a part that slides on by hand
  cannot transmit 40 N·cm by friction. No interference value, fit
  class (e.g. H7/p6), or minimum interference is stated anywhere.
- **Fix:** State the required interference (minimum and maximum, in mm)
  and the fit class, with the shaft tolerance band, so the bore
  tolerance is smaller than the shaft in every case.

### B3 — Tooth profile is unbuildable: "per the GT2 standard" names no geometry
- **Severity:** blocker
- **Target:** 36-tooth GT2 tooth profile (§4, §9)
- **Evidence:** §4 states only "Tooth profile per the GT2 standard".
  No standard body, edition, or document number is cited, and no tooth
  dimension is given: no groove width, groove depth, flank radius,
  tip radius, or pitch tolerance. The only derivable number is groove
  depth 1.20 mm ((22.40 − 20.0)/2 from the tip and root diameters in
  §2), which is never stated. §9 admits "Tooth profile tolerance is
  not stated: 'per the GT2 standard' names no tolerance class or
  inspection method."
- **Fix:** Cite the exact GT2 standard document and edition, tabulate
  the groove geometry (width, depth, radii) with tolerances, and state
  the pitch tolerance and inspection method.

## Majors

### M1 — Radial runout tolerance has no datum
- **Severity:** major
- **Target:** radial runout ≤ 0.05 mm at the tip diameter (§1, §8)
- **Evidence:** §1 requires "radial runout ≤ 0.05 mm measured at the tip
  diameter" and §8 measures it "with a dial indicator" on the pulley
  "mount[ed] on the motor shaft". Neither section states the datum axis
  (bore axis, shaft axis, or hub axis), and the motor shaft's own
  runout is uncontrolled, so the measurement cannot be reproduced.
- **Fix:** Name the datum (e.g. bore axis A) and the measurement setup,
  including the shaft runout limit.

### M2 — "Driving" vs "free" dimensions are never identified
- **Severity:** major
- **Target:** general tolerance ±0.05 mm driving / ±0.1 mm free (§4)
- **Evidence:** §4 states "All driving dimensions toleranced ±0.05 mm;
  free dimensions ±0.1 mm" but never lists which dimensions are
  driving. Tip diameter Ø22.40 mm, root diameter Ø20.0 mm, pitch
  diameter 22.92 mm, flange Ø25.50 mm, hub Ø16.00 mm, and the 7.0 mm
  tooth width carry no individual tolerances, so a builder cannot tell
  whether Ø22.40 mm is ±0.05 or ±0.1.
- **Fix:** Attach a tolerance to every dimension in §2 and §4, or list
  the driving dimensions explicitly.

### M3 — Bore tolerance vs anodize sequence is undefined
- **Severity:** major
- **Target:** Ø5.00 mm bore H7 vs clear anodize (§3, §4)
- **Evidence:** §3 specifies "6061 aluminium, clear anodized" after
  "CNC machined from bar", and §4 gives the bore as Ø5.00
  +0.012/−0.000. No anodize type or layer thickness is stated, and the
  spec never says whether the bore tolerance applies before or after
  anodizing. An anodize layer grows into the bore and changes its
  diameter by twice the layer thickness — enough to consume the whole
  0.012 mm tolerance band.
- **Fix:** State anodize type and thickness (µm) and state that the bore
  tolerance applies after anodizing (or that the bore is masked/machined
  after anodizing).

### M4 — Material temper is missing
- **Severity:** major
- **Target:** 6061 aluminium (§3)
- **Evidence:** §3 states only "Material: 6061 aluminium, clear
  anodized". No temper is given (e.g. T6, T651). Temper determines
  strength, machinability, and whether the hub wall and press fit
  behave as assumed; 6061-O and 6061-T6 are different materials for
  engineering purposes.
- **Fix:** State the temper (e.g. 6061-T6) and the governing material
  standard.

### M5 — No surface finish anywhere, including the press-fit bore
- **Severity:** major
- **Target:** bore Ø5.00 mm and tooth flanks (§2, §4)
- **Evidence:** The spec gives no surface-finish (Ra) requirement for
  any feature. The bore is the friction torque path (§2 retention) and
  the tooth flanks are the belt-mesh surfaces, yet neither has a finish
  value, so neither the friction nor the mesh can be controlled or
  inspected.
- **Fix:** State Ra for the bore, tooth flanks, flange faces, and hub
  outside diameter.

### M6 — Axial stack-up is ambiguous: hub position and bore length undefined
- **Severity:** major
- **Target:** hub Ø16.00 mm × 7.0 mm tall, overall height 17.0 mm (§2,
  §4)
- **Evidence:** §2 gives "Hub: Ø16.00 mm × 7.0 mm tall, on the top
  face" and overall height 17.0 mm. The numbers only add up
  (1.5 + 7.0 + 1.5 + 7.0 = 17.0) if the hub sits entirely above the top
  flange, but the spec never states that stacking order, never states
  which face is "top", and never states the bore length (through the
  full 17.0 mm, or only part of it). The axial position of the toothed
  section between the flanges is likewise not dimensioned.
- **Fix:** Provide a section view or an axial dimension chain from one
  datum face: flange positions, tooth-section position, hub start and
  end, and bore depth.

### M7 — Belt centring has no dimension or measurable test
- **Severity:** major
- **Target:** 6 mm GT2 belt in 7.0 mm tooth width between flanges (§1,
  §2, §8)
- **Evidence:** §2 gives a 6 mm belt in a 7.0 mm wide toothed section
  (1.0 mm total clearance, never stated), but no axial position of the
  belt relative to the flanges and no allowable off-centre value. §1
  requires the belt to track "centred with no flange contact", and §8
  tests it by "check the teeth seat fully and the belt tracks centred"
  — with no measurement, no duration, and no load stated in the test.
- **Fix:** State the belt's nominal axial position and allowable
  off-centre (±mm), and state the test duration, tension, and how
  centring is measured.

### M8 — 10,000-hour life requirement has no test
- **Severity:** major
- **Target:** 10,000 hours without service (§1)
- **Evidence:** §1 requires the pulley to "run for 10,000 hours without
  service", but no section gives a life test, an accelerated-test
  method, or any acceptance criterion for wear, anodize loss, or bore
  loosening over that life. The §8 verification plan covers fit, mesh,
  runout, and a 50 N pull-off only.
- **Fix:** State how 10,000-hour life is verified (test duration,
  conditions, and pass criteria for wear and retention), or downgrade
  the requirement to a design goal.

### M9 — Recycled-content target is unverifiable and contradicted
- **Severity:** major
- **Target:** ≥ 30% recycled 6061 aluminium (§5)
- **Evidence:** §5 sets a "Recycled-content target: ≥ 30% recycled 6061
  aluminium" and in the next line states "Material: 6061 aluminium
  from the incumbent supplier, no recycled-content data supplied".
  No verification method, certificate, or supplier declaration is
  specified, so the target cannot be checked at receipt.
- **Fix:** State the evidence required (e.g. supplier recycled-content
  declaration per batch) and what happens if the supplier cannot
  provide it.

### M10 — 15 N belt tension is an unclosed assumption, and the shaft bearing rating is unknown
- **Severity:** major
- **Target:** 15 N belt tension; motor front-bearing rating (§1, §8,
  §9)
- **Evidence:** §1 and §8 use "15 N belt tension" as the worst case, but
  §8 lists it as open assumption (2): "belt tension 15 N is the worst
  case — closing evidence: belt supplier tension table [TO BE
  OBTAINED]". §9 adds that the 15 N radial load is carried by the
  motor's front bearing, "whose rating is not on file". The belt-load
  case and the bearing that carries it are both unverified.
- **Fix:** Obtain the belt supplier tension table and the NEMA-17 motor
  front-bearing radial-load rating, and record both numbers in the spec.

## Minors

### m1 — D-flat dimensions incomplete
- **Severity:** minor
- **Target:** shaft D-flat, 0.5 mm deep, 17.75 mm long (§2)
- **Evidence:** §2 gives the shaft D-flat as "0.5 mm deep, 17.75 mm
  long" but not its width (chord) or its axial position along the
  shaft, so a mating flat (if one were added per B1) could not be
  dimensioned from this spec.
- **Fix:** State the flat width and its axial start position from the
  shaft end.

### m2 — Flange-to-tooth clearance and edge treatment missing
- **Severity:** minor
- **Target:** flanges Ø25.50 mm × 1.5 mm thick (§2, §4)
- **Evidence:** The flange outside diameter overhangs the tooth tip
  diameter by 1.55 mm radially ((25.50 − 22.40)/2, never stated), and
  no chamfer, edge break, or burr requirement is given for the flange
  rims, hub edge, or bore mouths anywhere in the spec.
- **Fix:** State the flange overhang and a maximum edge break (e.g.
  0.2 mm × 45° or "break sharp edges").

### m3 — "Hand press fit" and 50 N pull-off are undefined
- **Severity:** minor
- **Target:** pull-off test 50 N; hand press fit (§8)
- **Evidence:** §8 requires an "axial pull test to 50 N; the pulley
  must not move", but the spec never derives 50 N from any service
  axial load, and "hand press fit" states no assembly force or method.
  A 50 N pass limit with no service-load basis is an arbitrary number.
- **Fix:** State the service axial load the 50 N derives from, and the
  assembly force/method for the press fit.

### m4 — "Single setup" and stock size undefined
- **Severity:** minor
- **Target:** CNC machined from bar, single setup (§3)
- **Evidence:** §3 states "CNC machined from bar, single setup, then
  anodized" but gives no bar stock diameter or length, no setup datum,
  and no definition of what "single setup" constrains (e.g. whether
  the bore and tooth profile are cut without re-chucking).
- **Fix:** State the bar stock size and the setup datum, or delete
  "single setup" as a process instruction.

### m5 — Cost target has no verifiable basis
- **Severity:** minor
- **Target:** $3.80 per unit at 1,000 units, 4 minutes machine time
  (§7)
- **Evidence:** §7 gives "$3.80 per unit at 1,000 units" with "4 minutes
  machine time per unit" as the only basis — no labour rate, material
  cost, anodize cost, or scrap allowance — so the target cannot be
  checked or challenged.
- **Fix:** Break the $3.80 into material, machine, anodize, and overhead
  lines.

### m6 — Undefined terms: GT2, NEMA-17, H7, anodize type
- **Severity:** minor
- **Target:** terminology (§2, §3, §4)
- **Evidence:** The spec uses "GT2", "NEMA-17", "H7", and "clear
  anodized" without citing the governing standard for any of them
  (GT2 tooth standard, NEMA ICS 16 / motor standard, ISO 286 for H7,
  anodize specification such as MIL-A-8625 Type II). A stranger must
  guess which edition applies.
- **Fix:** Cite the standard and edition for each term at first use.

## Dropped generic findings

The following candidate findings were considered and dropped because
they name no feature, dimension, tolerance, material, or dataset:

- "The spec is hard to follow" — no target named.
- "More detail is needed overall" — no target named.
- "The verification plan could be stronger" — no target named.

## Controls passed

Sections read and found complete (arithmetic or identification only —
none of these cures the findings above):

- §6 PLM identification: CAD system (Siemens NX), dataset
  `PULLEY_GT2_36T` Rev B, source file `timing_pulley.step` (STEP
  AP214), and part count (1 solid) are all stated.
- §3 hub-wall arithmetic: (16.0 − 5.0)/2 = 5.5 mm is correct as stated.
- §2 pitch-diameter arithmetic: 36 teeth × 2 mm pitch gives 22.92 mm
  pitch diameter (36 × 2 / π = 22.918), correct as stated.
- §2 overall-height arithmetic: 1.5 + 7.0 + 1.5 + 7.0 = 17.0 mm is
  consistent with the stated overall height, assuming the hub sits
  above the top flange (see M6 — the assumption itself is unstated).
- §9 known gaps: the spec itself correctly flags the missing
  bearing-rating check, the missing set-screw provision, and the
  unstated tooth-profile tolerance.
