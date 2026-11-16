# Cost review findings — NEMA-17 stepper motor integration, extruder drive

Reviewer: cost (Goldfish, stage 3). Scope: §7 Cost against §3 Material and
process, §5 Sustainability, §1/§4 tolerances, §8 Verification plan, and the
measured model files (`nema17.step`, `timing_pulley.step`, re-measured for
this review). All CAD-cited dimensions in the spec were checked against the
models and agree (see Controls passed); the cost figures themselves cannot
be verified from CAD and no supplier quote or datasheet is on file.

## Findings

### Blocker

**B1 — §7 prices a motor that fails §5's own material requirement.**
§7 bases the $14.50 target on a $12.80 purchased motor, but §5 states the
end caps are virgin aluminium with no recycled-content data supplied,
while §5 also sets a ≥20% recycled-aluminium target for those same end
caps — the costed part is the non-compliant configuration, so $12.80 is
the price of a motor that does not meet the spec.
Fix: re-price the motor against a recycled-content-compliant supply and
re-baseline the $14.50 target on that price.

### Major

**M1 — $12.80 (88% of the $14.50 target) is an unsourced engineer estimate.**
§7 gives no supplier, no quote, and no validity date for the $12.80 motor
price, and §9 admits no supplier datasheet is on file, so torque, current
and insulation class — the ratings the price must cover — are unverified
requirements, not confirmed values.
Fix: obtain a written supplier quote tied to a datasheet that confirms the
§1 ratings, and cite it in §7.

**M2 — The required GT2 pulley is missing from the cost basis entirely.**
§1 defines the drive as motor plus 36-tooth GT2 timing pulley on the
shaft, and the pulley model confirms an aluminium part (bore Ø5.00 mm,
36 teeth, 25.50 mm envelope), yet §7's basis is motor $12.80 + mounting
hardware $1.70 only — the pulley's purchase cost is $0 in a target that
claims to cover the extruder drive unit.
Fix: add the pulley as a priced line item in §7 or state explicitly that
the $14.50 target excludes it and where its cost sits.

**M3 — Neither line price is stated at the 1,000-unit quantity.**
§7 states the $14.50 target "at 1,000 units", but neither the $12.80
motor price nor the $1.70 hardware price is stated as a 1,000-unit price,
and there is no volume break, minimum order quantity, or quote validity
period — if $12.80 is a list or single-unit price, the 1,000-unit target
is ungrounded.
Fix: state both line prices explicitly as 1,000-unit prices with the
quote's validity dates.

**M4 — No cost driver is named for a target that is 88% one bought-in part.**
§7 names no cost driver and carries no contingency, while §3 identifies
the motor's cost-relevant contents as NdFeB rotor magnets and copper
windings — the two volatile inputs — so the dominant line item has no
sensitivity analysis and no allowance for magnet or copper price movement.
Fix: add a driver breakdown for the $12.80 (magnets, copper, steel,
aluminium) with a stated contingency or price-validity window.

**M5 — The ±0.1 mm tolerances and ≤0.05 mm runout carry no cost.**
§4 imposes ±0.1 mm on all driving dimensions and §1 requires shaft
runout ≤0.05 mm at the pulley hub, but the $12.80 prices a bought-in
motor with no datasheet on file (§9) proving a standard motor meets
those limits — a screened, selected, or premium-grade motor, and the
incoming inspection to enforce the limits, are costed at $0.
Fix: confirm the quoted motor meets the §4 tolerances and §1 runout or
add the screening/premium cost to §7.

### Minor

**m1 — $1.70 mounting hardware is un-itemized and unverifiable.**
§7 charges $1.70 for mounting hardware, but the spec never states the
screw length, grade, or finish for the four M3 screws (§2) and lists no
washers or other items, so the figure cannot be checked against any
parts list.
Fix: itemize the hardware (screw specification × 4, plus any washers)
and price each line.

**m2 — §8 acceptance testing has no cost in the $14.50.**
§8 requires a torque-rig stall test, a 200-step encoder check, a dial-
indicator runout check, and a 1-hour thermal run, but §7 contains no
inspection, acceptance, or qualification cost — it is unstated whether
acceptance is per-unit or sampled and who pays for it.
Fix: state the acceptance sampling basis and add its per-unit cost (or
amortised qualification cost) to §7.

**m3 — The mounting plate's cost scope is unstated.**
§2 mounts the motor to the extruder mounting plate with four M3 screws
and §3 notes the plate is a separate part, but §7 never states whether
the $14.50 target excludes the plate — a reader cannot tell if the
target covers the installed motor or only motor plus screws.
Fix: state explicitly in §7 that the mounting plate is excluded and
where its cost is carried.

## Controls passed

- **Arithmetic (§7):** $12.80 + $1.70 = $14.50 exactly.
- **Tooling (§3 vs §7):** "tooling: none" is consistent with §3
  ("bought-in motor", process none) — no tooling amortisation risk at
  1,000 units, and no moulding/CNC process mismatch at that quantity.
- **Quantity/process fit (§7 vs §3):** a bought-in part needs no tooling,
  so the 1,000-unit quantity carries no amortisation problem.
- **Costed geometry matches the model (re-measured):** body
  42.30 × 35.00 × 42.30 mm, overall length 55.00 mm, shaft Ø5.00 mm ×
  24.0 mm with 20.0 mm protrusion, D-flat 0.5 mm deep × 17.75 mm long
  starting 2.0 mm from the front face, 4× Ø3.07 mm holes on 31.0 mm
  pitch, pilot recess Ø22.0 mm × 2.2 mm deep, front cap opening Ø10.0 mm,
  5 solids, volume 58,681.8 mm³ — all as specified; mating pulley bore
  Ø5.00 mm, 36 teeth, tip Ø22.40 mm, 1 solid, volume 5,106.7 mm³ — all
  as specified. No cost figure depends on a dimension the model
  contradicts.

## UNVERIFIED

- The $12.80 motor price, the $1.70 hardware price, and the $14.50
  target cannot be verified from the CAD files; no supplier quote,
  price list, or datasheet was supplied with the spec, so none of these
  figures is asserted correct — see M1 and M3.
