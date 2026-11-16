# Sustainability findings — GT2 timing pulley, 36 tooth, aluminium

Reviewer: sustainability (GreenBOM-style), stage 4. Sources: spec
`tests/fixtures/timing_pulley_spec.md`, measured facts
`tests/fixtures/timing_pulley_facts.md` and
`tests/fixtures/nema17_facts.md`, and re-measurement of
`timing_pulley.step` (1 solid, 25.50 × 17.00 × 25.50 mm,
volume 5,106.7 mm³, bore Ø5.00 mm, hub Ø16.00 mm, flanges
Ø25.50 mm — all confirmed against the facts file).

## Findings

### 1. Blocker — Recycled content, 6061 aluminium: ≥ 30% target with no data

- **Severity:** blocker
- **Target/material:** 6061 aluminium; recycled-content target ≥ 30% (spec §5).
- **Evidence:** Spec §5 states the target and in the next line states
  "6061 aluminium from the incumbent supplier, no recycled-content
  data supplied" — no percentage, no supplier certificate, no chain
  of custody, and no named supplier.
- **Fix:** Obtain a supplier declaration stating the actual recycled
  content percentage for the supplied 6061 and its evidence basis,
  and record it against the ≥ 30% target.

### 2. Blocker — End-of-life claim "fully recyclable once the anodize layer is stripped" is conditional with no stripping evidence

- **Severity:** blocker
- **Target/material:** 6061 aluminium, clear anodized (spec §3, §5).
- **Evidence:** Spec §5 claims the part is "fully recyclable as
  aluminium once the anodize layer is stripped" but names no
  stripping method, facility, or evidence that stripping happens,
  and gives no anodize thickness or composition; the recyclability
  claim therefore rests on an unstated, unevidenced step.
- **Fix:** Name the stripping process and the recycler/route that
  performs it, or downgrade the claim to recyclable subject to a
  stated stripping route.

### 3. Major — "Single-material part" contradicted by the anodized coating the spec itself names

- **Severity:** major
- **Target/material:** 6061 aluminium plus clear anodize coating
  (spec §3, §5).
- **Evidence:** Spec §5 calls the part "single-material" while §3
  specifies a clear anodized coating, a second material layer on
  every surface; the re-measured model is a single solid
  (1 solid, 5,106.7 mm³) but a STEP solid carries no coating data,
  so the model cannot support the single-material claim for the
  finished, coated part.
- **Fix:** State the anodize layer as a separate material/coating
  stream in §5 with its thickness and composition, and revise the
  single-material claim accordingly.

### 4. Major — "No disassembly needed" contradicted by the press-fit joint to the motor

- **Severity:** major
- **Target/material:** Pulley-to-NEMA-17 press-fit joint; end-of-life
  separation (spec §2, §5).
- **Evidence:** Spec §5 says "no disassembly needed", but §2 retains
  the pulley by press fit on the Ø5.00 mm motor shaft (measured
  shaft Ø5.00 mm, 0.5 mm D-flat, in `nema17_facts.md`), so at
  end-of-life the pulley must be pulled off the motor before the
  aluminium can be recycled as a separate stream, and no removal
  method, tool, or disassembly time is given.
- **Fix:** Add an end-of-life separation step for the press-fit joint
  with a stated method and disassembly time.

### 5. Major — No carbon or energy target, method, or evidence anywhere in the spec

- **Severity:** major
- **Target/material:** Whole-part carbon footprint and process energy
  (spec §5, §7).
- **Evidence:** Spec §5 contains only the recycled-content target and
  the end-of-life claim — no carbon target, no energy target, no
  measurement method, and no figure — while §7 states 4 minutes of
  CNC machine time per unit with no kWh per unit or machine power.
- **Fix:** Add a carbon target and an energy-per-unit figure with
  their measurement methods, or record explicitly that neither is
  assessed.

### 6. Major — Machining waste of at least 41% of the bar is unaddressed

- **Severity:** major
- **Target/material:** 6061 aluminium bar stock; CNC machining
  (spec §3, §7).
- **Evidence:** Spec §3/§7 state "CNC machined from bar" with no
  bar size, yield, or swarf-recycling statement, while the measured
  envelope (Ø25.50 × 17.00 mm) gives a minimum enclosing bar volume
  of 8,682.0 mm³ against a finished volume of 5,106.7 mm³, so at
  least 3,575.3 mm³ — 41.2% of the minimum bar — is removed as chips,
  and any bar larger than the envelope wastes more.
- **Fix:** State the actual bar size, the material yield, and whether
  the swarf is collected and recycled, with the recycled-content
  accounting for it.

### 7. Major — No material-health data for the 6061 or the anodize layer

- **Severity:** major
- **Target/material:** 6061 aluminium and clear anodize coating
  (spec §3).
- **Evidence:** Spec §3 names only "6061 aluminium, clear anodized"
  — no temper, no REACH/RoHS status, no restricted-substance
  statement, and no anodize seal chemistry — so material health
  cannot be assessed from the spec.
- **Fix:** Add the temper, the REACH/RoHS compliance status, and the
  anodize process/seal chemistry from the supplier.

### 8. Minor — No part mass, so no recycled mass or carbon figure can be derived

- **Severity:** minor
- **Target/material:** 6061 aluminium part mass (spec §5).
- **Evidence:** The spec gives no part mass and no 6061 density;
  the measured volume is 5,106.7 mm³ (re-measured, confirmed), but
  without a stated density or mass the recycled-content mass and
  any carbon figure cannot be computed from the spec.
- **Fix:** Record the part mass (and the density used) in §5.

### 9. Minor — No disassembly time target or measurement method

- **Severity:** minor
- **Target/material:** End-of-life disassembly time (spec §5).
- **Evidence:** Spec §5 gives no disassembly-time target and no
  measurement method, and the only joining method in the spec is
  the §2 press fit, for which no removal time is stated.
- **Fix:** State a disassembly-time target with its measurement
  method, or record that none is set.

### 10. Minor — Anodizing process energy and chemistry ignored

- **Severity:** minor
- **Target/material:** Clear anodizing process (spec §3).
- **Evidence:** Spec §3 lists anodizing as a process step with no
  energy, chemical, or waste-water data, so a process step with
  known energy and chemical implications is carried in §5's
  end-of-life claim with no assessment.
- **Fix:** Add the anodizing energy per unit and the process
  chemistry/waste route from the supplier.

## Controls passed

- **One solid, no mixed-material features in the model:** re-measured
  `timing_pulley.step` as 1 solid, 299 faces, volume 5,106.7 mm³,
  with no second solid, inserted fastener, overmould, or
  solvent-bonded joint in the file — consistent with spec §6
  ("1 solid") and with no moulded features (§3).
- **Spec dimensional claims checked against the model and correct:**
  envelope Ø25.50 × 17.00 mm, bore Ø5.00 mm, hub Ø16.00 mm,
  flanges Ø25.50 mm, tip diameter Ø22.40 mm, root diameter
  Ø20.00 mm, 36 teeth — all confirmed by re-measurement, so the
  geometry the sustainability assessment rests on is as specified.
- **No disassembly-blocking joining method inside the part itself:**
  the model contains no bonded, overmoulded, or permanently
  fastened sub-part, so separation of the pulley body itself
  requires no internal disassembly step.

## Notes on verification

- Numbers cited from the CAD files were checked against
  `timing_pulley_facts.md` / `nema17_facts.md` and by
  re-measurement with `/tmp/measure.py` on `timing_pulley.step`
  (solids 1, bbox 25.50 × 17.00 × 25.50 mm, volume 5,106.7 mm³).
- The 41.2% machining-waste figure is derived from the measured
  envelope and finished volume (minimum enclosing bar
  8,682.0 mm³); the actual bar size is not in the spec, so the
  true waste is at least this figure.
- No sustainability figure was filled in from a typical value:
  where the spec gives no number, the finding records it as missing.
