# Cost review findings — micro servo mounting bracket

Reviewer: cr-cost-reviewer (Goldfish). Scope: cost section (§7) checked
against the material and process section (§3) and the rest of the spec.
No data beyond the spec was used.

## Findings

### 1. Blocker — Cost basis is a different material and process from the spec

- **Figure:** $4.20 per unit at 1,000 units (§7, "Cost target").
- **Contradiction:** §7 states the basis as "CNC-machined 6061 aluminium,
  12 minutes machine time per unit". §3 states the material as "ABS,
  natural colour, injection moulded" and the process as "injection
  moulding, single cavity, family tool". The cost target is therefore
  priced for a machined aluminium part while the design specifies a
  moulded ABS part — different material, different process, different
  cost structure.
- **Fix:** Re-price the $4.20 target on the specified basis (ABS,
  injection moulding) and state the new basis in §7.

### 2. Major — Tooling costed at zero despite a specified injection mould

- **Figure:** "Tooling: none (machined from plate)" (§7) against a
  target of $4.20 per unit at 1,000 units.
- **Contradiction:** §3 specifies "injection moulding, single cavity,
  family tool with the mating clip". An injection moulding tool is the
  dominant cost driver at 1,000 units, yet §7 costs tooling at zero.
  At this quantity the per-unit tooling share is exactly the figure
  that decides whether $4.20 is achievable, and it is absent.
- **Fix:** State the tool cost (including the family-tool share) and
  the amortised per-unit tooling figure at 1,000 units in §7.

### 3. Major — No cost breakdown behind the $4.20 target

- **Figure:** $4.20 per unit at 1,000 units (§7).
- **Contradiction:** §7 gives no breakdown — no material cost, no
  process cost, no tooling amortisation, and no machine rate to go
  with the "12 minutes machine time per unit" basis. With no rate,
  the 12-minute figure cannot be converted into dollars, so the
  $4.20 cannot be checked against its own stated basis, let alone
  against the specified ABS moulding process.
- **Fix:** Add a line-item breakdown (material, process, tooling per
  unit) that sums to the target, with the rate behind the machine
  time.

### 4. Minor — Tight tolerances are not costed

- **Figure:** $4.20 per unit (§7) against "All driving dimensions
  toleranced ±0.1 mm" and "Base plate ... flatness 0.1 mm" (§4).
- **Contradiction:** The cost basis is CNC machining, a process that
  meets ±0.1 mm and 0.1 mm flatness routinely, while the specified
  process is injection moulding, where those tolerances sit at the
  tight end and would need tighter tooling or secondary operations.
  §7 carries no allowance for either, so the target assumes the
  tolerance capability of the wrong process.
- **Fix:** State the tolerance cost allowance (tooling precision or
  secondary operation) for the moulded ABS part, or relax the
  tolerances and re-price.

### 5. Minor — Quantity sensitivity is untested at 1,000 units

- **Figure:** $4.20 per unit at 1,000 units (§7).
- **Contradiction:** 1,000 units is low volume for injection moulding,
  where unit cost is dominated by tooling amortisation, yet §7 shows
  no per-unit cost at any other quantity and no tooling figure to
  scale. The reader cannot tell whether $4.20 holds at 1,000 units
  or only at a much larger run, and the CNC basis (12 minutes machine
  time per unit) scales linearly with quantity while moulding does
  not — so the stated basis cannot even answer the quantity question
  for the specified process.
- **Fix:** Show the unit cost at 1,000 units with the tooling share
  broken out, and note how it moves at a lower and a higher quantity.

## Controls passed

- The cost target is tied to a stated quantity: $4.20 per unit **at
  1,000 units** (§7) — the quantity is explicit, not implied.
- Within §7 itself, "Tooling: none" is consistent with "machined from
  plate" — the cost section is internally self-consistent; the
  contradiction is with §3, not inside §7.
- The machine-time basis is stated per unit ("12 minutes machine time
  per unit"), so the basis is unit-scoped and comparable to the
  per-unit target.
