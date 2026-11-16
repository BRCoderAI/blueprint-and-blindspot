# Sustainability review — micro servo mounting bracket

Reviewer: cr-sustainability-reviewer (Goldfish, fresh context)
Date: 2026-11-15
Sources reviewed: `tests/fixtures/servo_bracket_spec.md` (design specification) and
`tests/fixtures/servo_facts.md` (measured CAD facts for `micro_servo.step`).

Scope note: the measured facts file contains no material, process, cost, or
PLM data, and no mass is stored in the STEP file. Every sustainability
claim in the spec is therefore engineer-sourced, not file-verified, and
nothing in the facts file closes a sustainability gap. Where a figure is
not in the spec, it is recorded below as missing — no typical value has
been substituted.

## Findings

### F1 — Blocker: virgin ABS specified against a ≥ 30% recycled-content target

- **Material / target:** ABS, supplier grade GP-22; recycled-content target
  ≥ 30% recycled ABS (spec §5).
- **Evidence:** §5 states the material is "virgin ABS, supplier grade
  GP-22, no recycled-content data supplied", in the same section as the
  ≥ 30% target. Virgin material is 0% recycled content by definition, so
  the specified material directly contradicts the stated target.
- **What would fix it:** specify a grade with a stated recycled-content
  percentage (≥ 30%) backed by a supplier certificate or declaration,
  or revise the target to match the material actually specified.

### F2 — Blocker: solvent bonding blocks the claimed separation for recycling and the < 2 minute disassembly target

- **Material / target:** ABS bracket bonded to the servo case; end-of-life
  target is separation of the bracket from the servo for recycling, with
  disassembly in under 2 minutes (spec §5; repeated in §1).
- **Evidence:** §5 states the "bracket is solvent-bonded to the servo case
  along the full side-wall contact area for stiffness". A full-area
  solvent bond is a permanent joint: it cannot be separated by hand tools
  in under 2 minutes, and it leaves adhesive residue on both parts, so
  the bracket cannot be cleanly separated for recycling as claimed.
- **What would fix it:** replace solvent bonding with a reversible
  mechanical retention method (the M3 side-wall screws already specified
  in §2), and re-time disassembly on the revised joint; or drop the
  separation-for-recycling and < 2 minute claims.

### F3 — Major: no measurement method or evidence for the recycled-content target

- **Material / target:** ABS; recycled-content target ≥ 30% (spec §5).
- **Evidence:** §5 gives a number (≥ 30%) but no method — no test
  standard, mass-balance or chain-of-custody scheme, supplier
  declaration, or verification step in §8. The verification plan (§8)
  contains no recycled-content check at all.
- **What would fix it:** name the measurement/verification method and
  the evidence that closes it (e.g. supplier recycled-content
  declaration with scheme and percentage), and add it to the
  verification plan.

### F4 — Major: no material-health data for the ABS or for the solvent adhesive

- **Material / target:** ABS grade GP-22, and the unnamed solvent adhesive
  used for the side-wall bond (spec §3, §5).
- **Evidence:** the spec gives the grade (GP-22) but no restricted-
  substance, REACH, or RoHS status for the ABS, and it does not name
  the solvent/adhesive at all, so there is no safety data sheet,
  composition, or restricted-substance status for the bonding agent
  either.
- **What would fix it:** supply REACH/RoHS and restricted-substance
  status for grade GP-22, and name the adhesive with its safety data
  sheet and restricted-substance status.

### F5 — Major: no carbon target, no process-energy data, and no method for either

- **Material / target:** ABS bracket, injection moulded (spec §3); no
  carbon or energy target is stated anywhere in the spec.
- **Evidence:** there is no embodied-carbon figure, no moulding energy
  per unit, and no measurement method for either. The process-energy
  implication is ignored entirely: injection moulding energy is
  unquantified, and the solvent-bonding step (§5) adds a further
  process (adhesive application and curing) whose energy and chemical
  use are also unquantified. §7's cost basis (CNC-machined 6061
  aluminium, 12 minutes machine time) is a different material and
  process from the specified injection-moulded ABS, so it supplies no
  usable energy or carbon basis either.
- **What would fix it:** state a carbon target and an energy-per-unit
  figure for injection moulding plus the bonding step, with the
  calculation method and source, or explicitly record that no carbon /
  energy target is set.

### F6 — Major: the materials on the other side of the bond, and the mating clip, are unnamed

- **Material / target:** servo case material and mating-clip material;
  end-of-life target is separation of the bracket for recycling
  (spec §5).
- **Evidence:** §3 states the bracket is injection moulded in a "family
  tool with the mating clip", but the clip's material is not named, and
  the servo case material — the other side of the full-area solvent
  bond — is not named anywhere in the spec. The measured facts file
  confirms the STEP file contains no material data, so the case
  material cannot be recovered from the CAD file. Without knowing
  whether the bonded pair and the clip are the same polymer or mixed
  materials, separability and recycling-stream contamination cannot be
  assessed.
- **What would fix it:** name the servo case material and the mating-clip
  material, state whether each is ABS or a different polymer, and
  assess the bonded pair for recycling-stream compatibility.

### F7 — Major: the disassembly verification plan cannot test the joint actually specified

- **Material / target:** ABS bracket / servo assembly; disassembly target
  under 2 minutes with a 2 mm hex key (spec §1, §5, §8).
- **Evidence:** §8 verifies disassembly by timing "a technician removing
  the servo with a 2 mm hex key". A hex key removes the M3 screws (§2);
  it cannot break a full-area solvent bond (§5). The plan contains no
  bond-breaking method, no tool for it, and no time allowance for it,
  so the stated verification would pass or fail a different joint from
  the one specified.
- **What would fix it:** rewrite the §8 disassembly verification to
  match the actual joining method — either the reversible mechanical
  joint (F2 fix) timed with a hex key, or a specified bond-breaking
  procedure with its own timed method.

### F8 — Minor: no end-of-life route is named for the separated ABS

- **Material / target:** ABS bracket; end-of-life claim "bracket to be
  separated from the servo for recycling" (spec §5).
- **Evidence:** the spec names no recycling stream, regrind route,
  recycler, or take-back arrangement for the ABS, and no regrind
  content or reuse route for production scrap from the single-cavity
  family tool (§3). "For recycling" is stated as a destination with no
  route attached.
- **What would fix it:** name the recycling route (stream, recycler or
  take-back scheme) and state what happens to moulding scrap and to
  end-of-life brackets.

## Controls passed

Narrow checks only — none of these passes the contradicted targets above.

- **Material grade identified:** ABS, supplier grade GP-22, is named in
  §3 and §5, so the material-identification check passes (recycled
  content and material health for that grade do not — see F1, F3, F4).
- **Recycled-content target is quantified:** the ≥ 30% figure in §5 is a
  specific number, not a vague aspiration; what is missing is the
  material, method, and evidence to meet it (F1, F3).
- **Disassembly target is quantified and consistent:** the under-2-minute
  target is stated the same way in §1 and §5; what fails is its
  achievability against the solvent bond (F2, F7).
- **Bracket is a single polymer as specified:** no second polymer is
  named for the bracket itself — it is ABS throughout (§3) — which is
  the mono-material starting point for recyclability, before the bond
  to the servo case defeats separation (F2, F6).
- **Natural colour specified:** ABS is specified "natural colour" (§3),
  with no pigment named, so no colourant contamination is introduced
  by the specification as written.

## Summary

- Findings: 8 (2 blocker, 5 major, 1 minor).
- Blockers: F1 (virgin ABS vs ≥ 30% recycled target), F2 (solvent bond vs
  separation for recycling and < 2 minute disassembly).
- No sustainability target in the spec is supported by evidence as
  written.
