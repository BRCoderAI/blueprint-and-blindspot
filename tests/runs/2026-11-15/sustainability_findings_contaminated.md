# Sustainability review — micro servo mounting bracket

Reviewer: cr-sustainability-reviewer (Goldfish). Scope: sustainability only
(material, recycled content, material health, carbon/energy, end-of-life and
disassembly). Sources: `servo_bracket_spec.md` (§5 and supporting sections)
and `servo_facts.md` (measured STEP data). No data invented; figures not in
the spec are called missing.

## Findings

### SUST-F1 — Recycled-content target contradicted by the specified material
- **Severity:** blocker
- **Material / target:** ABS, supplier grade GP-22; recycled-content target
  ≥ 30% recycled ABS (§5).
- **Evidence:** §5 states the material is "virgin ABS, supplier grade GP-22,
  no recycled-content data supplied", against the target of ≥ 30% recycled
  ABS in the same section. Virgin material is 0% recycled content, so the
  specified material cannot meet the stated target.
- **Fix:** Source a recycled-content ABS grade meeting ≥ 30% with supplier
  certification, or revise the target to match what the specified material
  actually delivers.

### SUST-F2 — Disassembly target contradicted by the joining method
- **Severity:** blocker
- **Material / target:** ABS bracket bonded to the servo case; end-of-life
  disassembly target under 2 minutes (§5, §1).
- **Evidence:** §5 states the bracket "is solvent-bonded to the servo case
  along the full side-wall contact area for stiffness", while §5 and §1
  require the servo to be separated from the bracket (for recycling, and
  for servicing) in under 2 minutes with a 2 mm hex key. Solvent bonding is
  a permanent joint: it cannot be undone with a hex key, and the full
  side-wall contact area gives no separation path. The joining method makes
  the stated disassembly time unachievable.
- **Fix:** Remove the solvent bond and retain the servo by mechanical means
  only (the two M3 side-wall screws already specified in §2), then re-time
  the disassembly test in the verification plan.

### SUST-F3 — No material-health data for the specified ABS grade
- **Severity:** major
- **Material / target:** ABS, grade GP-22 (§3, §5); no material-health target
  or declaration in the spec.
- **Evidence:** The spec names the grade (GP-22) but supplies no restricted-
  substances data and no REACH or RoHS status for it. The measured STEP
  facts confirm the file contains no material data at all, so there is no
  independent source for this either.
- **Fix:** Obtain a supplier material-health declaration (REACH/RoHS status,
  restricted-substances statement) for grade GP-22 and record it in §5.

### SUST-F4 — No carbon or process-energy data or measurement method
- **Severity:** major
- **Material / target:** ABS injection moulding (§3); no carbon or energy
  target, figure, or method anywhere in the spec.
- **Evidence:** §3 specifies injection moulding (single cavity, family tool
  with the mating clip) and §5 sets sustainability targets, but no embodied-
  carbon figure, no moulding energy per unit, and no measurement method for
  either is given. A process change or tooling choice with an energy
  implication is therefore unassessed.
- **Fix:** Add an embodied-carbon figure for the bracket and a moulding-
  energy figure per unit, each with its method (supplier EPD, metered
  machine energy, or a named calculation basis).

### SUST-F5 — Recycled-content target has no verification method
- **Severity:** major
- **Material / target:** ABS; recycled-content target ≥ 30% (§5).
- **Evidence:** §5 states the ≥ 30% target but names no method for measuring
  or verifying it — no supplier certificate, mass-balance basis, or incoming
  inspection check — and §8's verification plan contains no recycled-content
  test. The target is not measurable as written.
- **Fix:** Name the verification method in §5 and add it to the §8
  verification plan (e.g. supplier recycled-content certificate per batch).

### SUST-F6 — No resin identification or recycling route for the bracket
- **Severity:** minor
- **Material / target:** ABS bracket; end-of-life "separated from the servo
  for recycling" (§5).
- **Evidence:** §5 states the bracket is to be recycled after separation,
  but the spec names no recycling route, no recycler, and no moulded resin
  identification marking on the part that would let a sorter recognise the
  ABS grade. The end-of-life claim has no route attached to it.
- **Fix:** Specify a moulded resin ID marking on the bracket and name the
  intended recycling route.

### SUST-F7 — No material breakdown for the servo assembly
- **Severity:** minor
- **Material / target:** Servo assembly, 6 parts (§6); end-of-life separation
  of the whole assembly (§5).
- **Evidence:** §5's end-of-life claim covers separating bracket from servo,
  but the spec gives no material breakdown for the servo's 6 parts (the
  measured facts confirm the STEP file stores no material data, and the
  product name "High Torque Metal Gear" implies metal content that is
  nowhere itemised). Without it, the recyclability of the assembly as a
  whole cannot be assessed.
- **Fix:** Obtain the servo bill of materials with materials per part and
  record the separation route for each.

## Controls passed

- **No false recycled-content claim is asserted.** §5 honestly states the
  material is virgin ABS with no recycled-content data supplied; the spec
  does not claim recycled content it does not have.
- **Single-material bracket.** Only ABS is named for the bracket — no
  overmoulding, insert, or second material in the bracket itself — which
  supports material separation in principle.
- **Natural (unpigmented) colour.** §3 specifies natural-colour ABS, which
  is favourable for the ABS recycling stream (no pigment contamination).
- **Disassembly target is measurable as specified.** §8 gives a concrete
  measurement method (time a technician removing the servo with a 2 mm hex
  key), so the < 2 minute target itself is testable — it is the solvent
  bond (SUST-F2), not the target's measurability, that fails.
