# Cost review — micro servo mounting bracket

Reviewer: cr-cost-reviewer (Goldfish). Sources: `servo_bracket_spec.md` (§3, §4, §7)
and `servo_facts.md`. No data beyond the spec was used.

## Findings

### F1 — Blocker: cost basis is for a different material and process than the design specifies

- **Figure:** $4.20 per unit at 1,000 units (§7).
- **Contradiction:** §7 costs the part as "CNC-machined 6061 aluminium, 12 minutes
  machine time per unit" with "Tooling: none (machined from plate)". §3 specifies
  the part as "ABS, natural colour, injection moulded" with a "single cavity,
  family tool with the mating clip". The $4.20 figure is priced for a machined
  aluminium part; the design is a moulded ABS part. Material, process, and
  tooling all disagree between the two sections.
- **Fix:** Re-cost the part for injection-moulded ABS, including the family-tool
  cost, or change §3 to machined 6061 aluminium — the two sections must describe
  the same part.

### F2 — Major: tooling cost stated as "none" while §3 specifies a family tool

- **Figure:** "Tooling: none" (§7) at 1,000 units.
- **Contradiction:** §3 specifies a "single cavity, family tool with the mating
  clip". A mould tool exists and has a cost, yet §7 books zero tooling against
  1,000 units. At this quantity, tooling amortised over 1,000 units is the
  dominant unit-cost component for a moulded part, and it is absent from the
  $4.20 figure entirely.
- **Fix:** State the family-tool cost, the share allocated to this bracket versus
  the mating clip, and the amortised per-unit amount at 1,000 units.

### F3 — Major: $4.20 target has no cost breakdown

- **Figure:** $4.20 per unit (§7).
- **Contradiction:** §7 gives no breakdown — no material (resin) cost, no machine
  or cycle-time rate, no tooling amortisation, no inspection or scrap allowance.
  The only supporting number is "12 minutes machine time per unit", which belongs
  to the CNC basis in F1 and cannot produce $4.20 without a machine rate that is
  never stated. The target cannot be verified, challenged, or re-derived.
- **Fix:** Provide a line-item breakdown (material, process, tooling amortised at
  1,000 units, inspection/scrap) that sums to the target.

### F4 — Major: the named cost driver does not drive cost for the specified process

- **Figure:** "12 minutes machine time per unit" (§7) as the cost basis.
- **Contradiction:** Machine time is the driver for CNC machining, not for
  injection moulding. For the moulded ABS part §3 specifies, the drivers that
  actually move cost at 1,000 units are tooling amortisation and resin, neither
  of which §7 names or prices. The spec names a driver for a process the part
  does not use and ignores the drivers for the process it does use.
- **Fix:** Name and price the moulding drivers (tool amortisation, resin per
  part, cycle time) and drop the CNC machine-time basis.

### F5 — Major: ±0.1 mm driving tolerance is not costed

- **Figure:** "All driving dimensions toleranced ±0.1 mm" (§4).
- **Contradiction:** §7 contains no cost line for holding ±0.1 mm — no tooling
  precision, process-control, inspection, or scrap/rework allowance. A tight
  tolerance on a moulded part is a cost item, and the $4.20 figure prices the
  part as if the tolerance were free.
- **Fix:** Add a tolerance cost line (or the scrap/inspection allowance it
  implies) to the §7 breakdown, or relax the driving tolerance to one the
  moulding process holds at the stated cost.

## Controls passed

- **Cost target is tied to a stated quantity.** §7 states "$4.20 per unit at
  1,000 units" — the figure and the quantity appear together, so the
  quantity-tie check passes as stated.
- **No second, conflicting cost figure exists in the spec.** $4.20 is the only
  unit-cost figure anywhere in the document; there is no internal contradiction
  between two cost numbers.
- **No cost claim is contradicted by the measured STEP facts.** `servo_facts.md`
  contains no material, process, or cost data, so nothing in the measured facts
  conflicts with the cost section; the cost story stands or falls on its own
  internal consistency (see F1–F5).
