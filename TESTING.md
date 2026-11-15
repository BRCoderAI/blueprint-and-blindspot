# Testing

## Rename (2026-11-15)

The plugin was renamed from the `cad-review` working name to
**Blueprint & Blindspot** (plugin id `blueprint-blindspot`, repo
`BRCoderAI/blueprint-and-blindspot`, skill prefix `cr-` → `bb-`).
All live files were renamed and re-validated (6/6 manifests parse,
all agent references resolve). The run records in `tests/runs/`
pre-date the rename and keep the old `cr-` names as written — they are
historical records, not live references.

## What is tested

The product of this plugin is reviewer prompts. A prompt change is a
guess until a reviewer run proves it catches a real defect. So the
tests are **review runs against a fixture spec with planted defects**,
scored against a key the reviewers never see.

## The fixture

- **Spec:** `tests/fixtures/servo_bracket_spec.md` — a design
  specification for a micro-servo mounting bracket, written to look
  like a real spec. It cites `micro_servo.step` as its source model.
- **Model:** `~/workspace/cad-viewer/test-fixtures/micro_servo.step`
  (not copied into this repo). Measured ground truth in
  `tests/fixtures/servo_facts.md`: STEP AP214, product "1143
  MicroServo High Torque Metal Gear v1", 6 solids, bounding box
  12.00 × 31.30 × 30.68 mm, total volume 6,872.6 mm³. Measured with
  build123d / OCCT 8.0.
- **Planted defects (6)** in `tests/fixtures/defect_key.md`
  (scorer only — never give it to a reviewer):
  - DFM-1: wall 0.8 mm, injection-moulded ABS (practical minimum
    ~1.5 mm).
  - DFM-2: M3 clearance holes Ø3.0 mm (clearance is Ø3.4 mm).
  - COST-1: cost basis CNC-machined 6061 aluminium vs ABS injection
    moulding in the material section.
  - SUST-1: recycled target ≥30% vs virgin ABS with no data;
    disassembly target <2 min vs solvent-bonded bracket.
  - PLM-1: dataset MicroServo_v2 Rev B vs file product v1.
  - PLM-2: source file stated as STEP AP242; the file is AP214.
- **Controls (2)** that must NOT be flagged:
  - C-1: servo envelope 12.0 × 31.3 × 30.7 mm (correct — 30.68
    rounds to 30.7).
  - C-2: servo part count 6 (correct).

## How a run works

1. Four reviewer subagents are spawned fresh, one per lens (DFM,
   cost, sustainability, PLM). Each receives ONLY its persona file,
   the spec, and the facts file. No drafting history, no defect key.
2. Each writes findings to `tests/runs/<date>/<lens>_findings.md`.
3. The scorer checks: did each planted defect get found by its
   own-lens reviewer? Were the controls passed? Is every finding
   concrete (named feature, dimension, tolerance, material, or
   dataset)? Any generic finding fails the run.
4. A review that only produces generic findings is a failed test.

## Run 2026-11-15

### First run — CONTAMINATED, discarded

The defect key was embedded in `servo_facts.md`, which the reviewers
were told to read, so blinding was not intact. The sustainability
reviewer flagged this; the PLM and DFM reviewers noted it too. All
four first-run findings files were renamed with a `-contaminated`
suffix and discarded. Results for the record: 42 findings total
(DFM 18, PLM 12, sustainability 7, cost 5); all 6 planted defects
found; both controls passed. The findings were all derivable from the
spec text itself, but the run cannot be claimed as blind.

The fixture was fixed: the key moved to `tests/fixtures/defect_key.md`
(scorer-only) and `servo_facts.md` now carries measurements only.
Verified clean with grep (zero matches for the key or any defect ID).

### Second run — blind, counts

| Reviewer | Findings | Planted defect found | Controls passed |
| --- | --- | --- | --- |
| DFM | 13 (3 blocker, 6 major, 4 minor) | DFM-1, DFM-2 | C-1, C-2 |
| Cost | 5 (1 blocker, 4 major) | COST-1 | n/a (no model numbers in scope) |
| Sustainability | 8 (2 blocker, 5 major, 1 minor) | SUST-1 (both halves) | honest narrow checks |
| PLM | 8 (2 blocker, 6 major) | PLM-1, PLM-2 | C-1, C-2 |
| **Total** | **34** | **6 / 6** | **no false positives on controls** |

Every planted defect was found by its own-lens reviewer, and most
were cross-caught by other lenses too. Zero generic findings in the
blind run: every finding names a feature, dimension, tolerance,
material, or dataset.

### Genuine defects the reviewers found that were NOT planted

- **Envelope impossible (PLM, blocker):** bracket envelope
  16.0 × 35.0 × 14.0 mm cannot contain the servo
  12.00 × 31.30 × 30.68 mm — the 30.68 mm axis fits inside no bracket
  dimension in any orientation. Verified independently with OCCT.
- **Spline cannot reach the top face (DFM, blocker):** the bracket is
  14.0 mm tall, the servo 30.7 mm, so the spline sits ~16.7 mm above
  any bracket top face; a top face also contradicts "wraps on three
  sides".
- **M3 screws cannot engage the servo ears (DFM, blocker):** measured
  from the STEP file, the ear holes are Ø1.7 mm, vertical, through
  2.0 mm flanges on a 29.7 mm pitch — a Ø3.0 mm M3 screw cannot pass
  through them, and horizontal side-wall screws cannot engage vertical
  holes.
- **Tooling costed at none (Cost, major):** the dominant unit-cost
  component for a moulded part at 1,000 units is zeroed out.
- **2 mm hex key vs M3 screws (DFM, major):** M3 socket screws take a
  2.5 mm hex key.
- **Bracket dataset has no source file (PLM, major):** its revision is
  unverifiable.
- **Verification plan gaps (PLM, major):** §8 covers only the §1
  acceptance criteria; no verification method for any §2–§5
  requirement.

### Calibration note — RESOLVED 2026-11-15

The two DFM runs quoted different wall-thickness thresholds for ABS
(~1.5 mm vs ~1.0 mm) while agreeing on the verdict (0.8 mm fails).
Resolved by pinning thresholds to cited references in
`agents/bb-dfm-reviewer.md`: ABS injection-moulding wall per
Protolabs is 1.14–3.56 mm (typical nominal 1.5–2.5 mm) — so the
~1.0 mm figure was below the reference minimum, and ~1.5 mm was the
low end of the typical nominal, not the minimum. M3 clearance is
Ø3.4 mm per ISO 273 medium series. The pilot run below tests whether
reviewers now quote the pinned values.

### Method notes

- The DFM blind run recorded two failed exec calls during its session
  but still delivered complete findings with independently re-measured
  data; the failures did not affect the result.
- The synthesizer (`bb-synthesizer.md`) and comprehension reviewer
  were not exercised in this run — the four lens reviewers were run
  directly. A full `bb-review` end-to-end run (all five stages plus
  synthesis) is still outstanding.
- No live install test has been run on any platform yet. The Claude
  Code and Codex manifests follow the shapes EGM ships; the Gemini
  and Cursor manifests are included but untested (EGM itself ships no
  Gemini extension manifest).

## Verdict

**PASS.** 6/6 planted defects found blind, both controls passed, zero
generic findings, and 7+ genuine unplanted defects found — including
three blockers. The fresh-context mechanism works as designed on this
fixture: reviewers with no drafting history catch what the drafting
context would have excused.

## Limits

- One fixture, one spec, one model. A single fixture proves the
  mechanism, not the coverage. More fixtures (sheet metal, machined
  aluminium, a plastic housing with ribs and bosses) are needed before
  claiming breadth.
- Reviewers quote process limits from their own knowledge; thresholds
  vary between runs (see calibration note). Pinning thresholds to
  cited references is the next prompt improvement.
- The reviewers check numbers the spec cites against the model; they
  do not verify the model itself. Full model verification belongs to
  CAD/CAE tools.
- A review does not replace measurement, simulation, or human judgment.

## Pilot run 2026-11-15 — real designs, no planted defects

Full report: `tests/runs/2026-11-15/pilot/PILOT.md`. Two real specs
(NEMA-17 motor integration, GT2 36-tooth pulley) against real STEP
files, full five-stage runs plus synthesis — the first end-to-end
synthesizer runs. **91 merged findings (11 blockers, 56 majors,
24 minors) from 130 raw stage findings; both verdicts NOT READY.**
8 dropped, all generic, none wrong; 78 controls passed. Scorer
verified 91/91: all 11 blockers individually against spec text and
independent OCCT measurements, every cited model number reproduced.
Threshold pinning held: reviewers quoted Protolabs ABS 1.14–3.56 mm
and ISO 273 M3 Ø3.4 mm, correctly scoped the ABS range as
non-applicable, and the ISO 273 pin fired on the motor's Ø3.07 mm
mounting holes. Still open after the pilot: no live install test on
any platform; severity calibration (two blockers are honest open
assumptions, not hidden defects); "controls passed" needs a tighter
definition; coverage is one domain (motor + its pulley).
