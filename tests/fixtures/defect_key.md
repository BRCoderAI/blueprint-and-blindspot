# Defect key — SCORER ONLY

Never give this file to a reviewer. Reviewers receive only
`servo_bracket_spec.md` and `servo_facts.md`.

Planted defects in `servo_bracket_spec.md`:

- DFM-1: wall thickness 0.8 mm, injection-moulded ABS (practical
  minimum ~1.5 mm for ABS).
- DFM-2: M3 clearance holes Ø3.0 mm (M3 clearance is Ø3.4 mm).
- COST-1: cost basis is CNC-machined 6061 aluminium, but material
  section says ABS injection moulding.
- SUST-1: recycled-content target ≥30% but material is virgin ABS with
  no recycled data; disassembly target < 2 min but the bracket is
  solvent-bonded to the servo.
- PLM-1: spec cites dataset MicroServo_v2 Rev B; the file product is
  v1.
- PLM-2: spec says the source file is STEP AP242; the file is AP214.

Controls (must NOT be flagged):

- C-1: servo envelope 12.0 × 31.3 × 30.7 mm — correct (30.68 rounds
  to 30.7).
- C-2: servo part count 6 — correct.

## Methodology note, 2026-11-15

The first test run (2026-11-15) was contaminated: this key was
embedded in `servo_facts.md`, which the reviewers were told to read,
so blinding was not intact. The sustainability reviewer flagged this.
All four first-run findings were discarded and the run was repeated
blind with the key moved here. The first run's findings are kept in
`tests/runs/2026-11-15/` with a `-contaminated` suffix for the record;
only the clean re-run counts toward the test verdict.
