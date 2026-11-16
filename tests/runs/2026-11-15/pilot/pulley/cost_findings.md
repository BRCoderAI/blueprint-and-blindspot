# Cost findings — GT2 timing pulley, 36 tooth, aluminium

Reviewer: cost (Goldfish, stage 3). Spec: `timing_pulley_spec.md`.
Measured model re-checked this review with
`~/workspace/simprep-cad/.venv/bin/python /tmp/measure.py`:
`timing_pulley.step` — 1 solid, 299 faces, envelope 25.50 × 17.00 × 25.50 mm,
volume 5,106.7 mm³, bore Ø5.00, hub Ø16.00, tip Ø22.40, root Ø20.00,
flanges 2× Ø25.50 — all match the spec's cited numbers and the facts file.
`nema17.step` — 5 solids, volume 58,681.8 mm³, shaft Ø5.00 × 24.0 mm —
matches the facts file. Finished pulley mass from measured volume at
6061 density 2.70 g/cm³: 13.8 g; bar-stock slice Ø25.50 × 17.0 mm:
≈ 8,683 mm³ ≈ 23.4 g, so ≈ 41% of the bar becomes chips.

## Findings

### 1. Blocker — $3.80/unit target has no cost breakdown and cannot be reproduced
- **Target:** §7 cost target, $3.80 per unit at 1,000 units, basis "4 minutes
  machine time per unit".
- **Evidence:** §7 gives no machine rate, no material cost, no setup cost,
  no anodize cost, and no inspection cost — 4 min × an unstated rate cannot
  be checked against $3.80, and no line item sums to $3.80.
- **Fix:** Publish a per-unit breakdown (material, machine time × stated
  shop rate, setup amortised over 1,000 units, anodize, inspection) that
  sums to the target.

### 2. Major — Cost basis omits anodizing, which §3 requires
- **Target:** §7 basis "CNC-machined 6061 aluminium" vs §3 "CNC machined
  from bar, single setup, then anodized" (clear anodized, §3).
- **Evidence:** The cost basis prices machining only; the clear-anodize
  step specified in §3 has no cost line anywhere in §7, so the $3.80
  figure is computed for a different (un-anodized) part than the one
  specified.
- **Fix:** Add a per-unit anodize line (batch rate at 1,000 units) to the
  §7 breakdown or restate the target as machined-only.

### 3. Major — H7 bore and ±0.05 / 0.05 mm runout tolerances are uncosted
- **Target:** §4 bore Ø5.00 mm tolerance +0.012/−0.000 (H7); §1 radial
  runout ≤ 0.05 mm; §4 driving dimensions ±0.05 mm.
- **Evidence:** An H7 bore on Ø5.00 mm needs a reaming or precision-boring
  operation plus gauging, and the 0.05 mm runout check needs a dial-indicator
  inspection step (§8) — neither appears in the 4-minute machine-time basis
  or anywhere in §7, so the tightest tolerance on the part carries no cost.
- **Fix:** Cost the H7 bore as a separate operation (extra time or a
  reaming pass) and add per-unit inspection time for bore gauge and runout.

### 4. Major — Dominant cost driver is unpriced; material is trivial and unnamed
- **Target:** §7 names only "4 minutes machine time" as its basis, with no
  rate and no driver ranking.
- **Evidence:** Measured volume 5,106.7 mm³ gives 13.8 g finished mass
  (≈ 23.4 g of bar stock), so 6061 material is on the order of $0.10 per
  unit and cannot move the $3.80 target — machine time, anodize, and setup
  dominate, yet the section prices none of them (no shop rate, no anodize
  line, no setup line).
- **Fix:** State the shop rate and rank the drivers (machine time first,
  then anodize, then setup) with a priced line for each.

### 5. Minor — Setup / first-article cost at 1,000 units is never amortised
- **Target:** §7 "Tooling: none (machined from bar)" and §3 "single setup",
  against the $3.80 target at 1,000 units.
- **Evidence:** A single-setup CNC job still carries programming, fixturing,
  and first-article time, none of which is stated or amortised per unit in
  §7 — the quantity is stated but no setup figure is tied to it.
- **Fix:** State setup hours once and show the per-unit share at 1,000 units.

### 6. Minor — GT2 tooth cutting needs tooling the cost section claims is "none"
- **Target:** §7 "Tooling: none (machined from bar)" vs §4 "36 teeth" and
  §2 "36 grooves" (measured: 36 root segments Ø20.00 mm, 36 tip segments
  Ø22.40 mm, 144 R0.25 fillet faces).
- **Evidence:** Cutting 36 GT2 tooth profiles needs a dedicated form cutter
  or hob — a consumable/tooling expense with a finite life — which the
  "none" line and the 4-minute basis both ignore.
- **Fix:** Add a per-unit tooling/consumable allowance for the GT2 cutter,
  amortised over its expected life at 1,000 units.

### 7. Minor — ≥ 30% recycled-content target carries no costed premium or source
- **Target:** §5 recycled-content target ≥ 30% recycled 6061 vs §7 $3.80
  target; §5 notes the incumbent supplier supplied no recycled-content data.
- **Evidence:** No supplier can currently certify the 30% content, and any
  certified recycled-6061 bar premium is absent from the §7 figure, so the
  sustainability target and the cost target are not reconciled.
- **Fix:** Price the target from a supplier that can certify ≥ 30% recycled
  content, or drop the target from the costed baseline.

## UNVERIFIED (not asserted as correct)
- The 4-minute machine-time figure itself: no operation breakdown
  (turning, tooth cutting, boring, finishing) is given, so it cannot be
  checked against the measured geometry (36 teeth, Ø5.00 H7 bore, Ø16.00
  hub, 2 flanges). It is used as a basis above only as the spec's own claim.
- The $3.80 target: unverifiable for the reason in Finding 1, not
  confirmed wrong — no rate or breakdown exists to test it against.

## Controls passed
- Material/process match: §3 (CNC machined 6061 aluminium from bar, then
  anodized) matches the §7 basis material and process (CNC-machined 6061,
  machined from bar) — no process/material mismatch between the two sections.
- Quantity is stated: the $3.80 figure is tied to 1,000 units (§7), so the
  target is quantity-anchored rather than a quantity-free number.
- No mould-tooling contradiction: the part has no moulded features (§3) and
  the model confirms a single solid with no moulded geometry, so claiming
  no injection-mould tooling amortised over 1,000 units is consistent.
- Geometry does not contradict the machining basis: re-measured model is
  1 solid, 5,106.7 mm³, Ø25.50 × 17.00 mm envelope — a small single-piece
  part consistent with "machined from bar" and with material being a minor
  cost driver.
- All spec numbers cited from the CAD files check out against re-measurement:
  envelope Ø25.50 × 17.00 mm, tip Ø22.40 mm, root Ø20.00 mm, bore Ø5.00 mm,
  hub Ø16.00 × 7.0 mm, flanges 2× Ø25.50 × 1.5 mm, 36 teeth, 1 solid;
  mating shaft Ø5.00 mm confirmed in `nema17.step`.
