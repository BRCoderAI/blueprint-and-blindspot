# Launch pilot — Blueprint & Blindspot

Date: 2026-11-15. Two real designs, no planted defects, no defect key.
Full end-to-end `bb-review` runs (all five stages plus synthesis) on
specs written for real STEP files.

## Headline number

**91 findings, 11 blockers, across two real designs — both verdicts
NOT READY.** 130 raw stage findings merged into 91 (11 blockers,
56 majors, 24 minors). 8 findings dropped, all generic, none dropped
as wrong. 78 controls-passed entries. Scorer verification: 91/91
findings checked — all 11 blockers individually against the spec text
and independent OCCT measurements, every cited model number
reproduced by independent measurement, zero findings wrong.

## The designs

A matched pair: a NEMA-17 stepper motor and the 36-tooth GT2 timing
pulley that mounts on its shaft. Specs written as production design
specs, citing measured numbers from the STEP files. No defects were
planted; every finding below is something the reviewers found in a
real spec against a real model.

- **NEMA-17 stepper motor integration, extruder drive**
  (`nema17_spec.md` / `nema17.step`, AP214, 5 solids, 278 faces,
  58,681.8 mm³, envelope 42.30 × 55.00 × 42.30 mm).
- **GT2 timing pulley, 36 tooth, aluminium**
  (`timing_pulley_spec.md` / `timing_pulley.step`, AP214, 1 solid,
  299 faces, 5,106.7 mm³, envelope Ø25.50 × 17.00 mm).

Ground truth for both parts is in `tests/fixtures/nema17_facts.md`
and `tests/fixtures/timing_pulley_facts.md`, measured with build123d /
OCCT 8.0.

## Per-design breakdown

### NEMA-17 — NOT READY

| Stage | Findings | Blockers | Majors | Minors |
| --- | --- | --- | --- | --- |
| Comprehension | 26 | 6 | 14 | 6 |
| DFM | 10 | 3 | 4 | 3 |
| Cost | 9 | 1 | 5 | 3 |
| Sustainability | 10 | 1 | 6 | 3 |
| PLM | 14 | 1 | 9 | 4 |
| **Stage total** | **69** | **12** | **38** | **19** |
| **Merged** | **53** | **8** | **33** | **12** |

16 duplicate instances absorbed; 5 dropped, all generic; 36 controls
passed. Top blockers: Ø22.0 mm pilot recess vs Ø22.0 mm locating
boss (zero clearance); pulley bore Ø5.00 mm on shaft Ø5.00 mm (zero
interference for a claimed press fit); ≥20% recycled target vs virgin
aluminium end caps; mounting holes Ø3.07 mm for M3 screws (ISO 273
medium is Ø3.4 mm); dataset `NEMA17_MOTOR` Rev B vs file product
"NEMA-17 Stepper Motor v11" — and the file is an Adafruit vendor
import, not a Siemens NX dataset.

### GT2 pulley — NOT READY

| Stage | Findings | Blockers | Majors | Minors |
| --- | --- | --- | --- | --- |
| Comprehension | 19 | 3 | 10 | 6 |
| DFM | 12 | 2 | 5 | 5 |
| Cost | 7 | 1 | 3 | 3 |
| Sustainability | 10 | 2 | 5 | 3 |
| PLM | 13 | 1 | 7 | 5 |
| **Stage total** | **61** | **9** | **30** | **22** |
| **Merged** | **38** | **3** | **23** | **12** |

23 duplicate instances folded; 3 dropped, all generic; 42 controls
passed. Top blockers: retention contradicts itself (bore has "no flat
in the bore" yet retention "engages the shaft D-flat"); bore Ø5.00 mm
H7 (+0.012/−0.000) on a nominal Ø5.00 mm shaft is a clearance fit
called a press fit; tooth profile "per the GT2 standard" names no
geometry, tolerance, or inspection method.

## What the reviewers proved

- **The mechanism works on real designs, not just the fixture.**
  The blind fixture run caught 6/6 planted defects; the pilot caught
  91 findings in specs with nothing planted — including three
  zero-clearance/zero-interference fits and a retention mechanism that
  contradicts itself in the same section.
- **Reviewers check the model, not just the text.** Every cited model
  number was re-measured from the STEP files by the reviewers with
  OCCT and matched the facts files; zero model-agreement failures on
  cited numbers, and zero UNVERIFIED marks needed on the NEMA-17 run.
  The failures found are in the spec's reasoning about the model, not
  in the numbers themselves.
- **The synthesizer works end-to-end (first time).** Both runs merged
  five stages into one ranked report with verdicts, dropped generic
  findings (8 total), and stated cross-stage severity disagreements
  instead of silently resolving them (5 per design).
- **Threshold pinning worked.** DFM reviewers quoted the pinned
  values: Protolabs ABS wall 1.14–3.56 mm and ISO 273 M3 clearance
  Ø3.4 mm. The ABS range was correctly scoped as non-applicable to
  both pilot parts (bought-in motor, machined aluminium pulley);
  the ISO 273 pin fired on the motor's Ø3.07 mm mounting holes
  (blocker B7). No reviewer quoted a competing threshold this run.

## Threshold reference used

- ABS, injection moulding, wall thickness: Protolabs recommended
  range **1.14–3.56 mm** (0.045–0.140 in), typical nominal 1.5–2.5 mm.
  Source: Protolabs, "Injection Molding Wall Thickness Guidelines"
  and "Designing for Mouldability Vol. 1".
- Metric clearance holes: ISO 273 medium (normal) series — **M3
  Ø3.4 mm** (fine 3.2, coarse 3.6), M4 Ø4.5 mm, M5 Ø5.5 mm, M6 Ø6.6 mm.
  Source: ISO 273:1979 (reviewed and confirmed 2024).
- Draft, injection moulding: 1° per 1 in. of cavity depth; 0.5°
  minimum on polished faces. Ribs/bosses: 40–60% of adjacent nominal
  wall. Source: Protolabs design guidelines.
- Pinned in `agents/bb-dfm-reviewer.md` (synced to
  `.claude-plugin/agents/`).

## Rename record (same run)

The plugin was renamed from the `cad-review` working name to
**Blueprint & Blindspot** before the pilot, so the pilot ran under the
new identity: plugin id `blueprint-blindspot`, repo
`BRCoderAI/blueprint-and-blindspot`, skill prefix `cr-` → `bb-`
(5 skills, 6 reviewer personas, all cross-references), README title
and install commands, all six manifests, docs. Verified after the
rename: 6/6 manifests parse with the new name, all 11 frontmatter
names match, every agent reference resolves, zero `cad-review` or
`cr-` survivors in live files (the only `CR-` left is change-request
`CR-114` in the fixture spec). Run records in `tests/runs/` pre-dating
the rename keep the old names as historical records. License stays
Apache 2.0, Copyright 2026 Balaji Rajendran.

## What the pilot exposed as still unready for launch

1. **No live install test on any platform.** Carried from v1: the
   Claude Code and Codex manifests follow EGM's shipped shapes; the
   Gemini and Cursor manifests are included but untested. A launch
   that points at a one-command install must have run that command.
2. **Severity is the least stable output.** Two of the eleven blockers
   (NEMA-17 B4 holding torque, B5 locating boss) are honest open
   assumptions marked TO BE OBTAINED in the spec, not hidden defects —
   the protocol ranks unverified acceptance criteria as blockers,
   which is consistent but aggressive. Five severity disagreements per
   design were stated, not resolved. The launch story should say
   "11 blockers" with that qualification, not as eleven surprises.
3. **"Controls passed" needs a tighter definition.** On the pulley run,
   comprehension counted the §6 dataset identification as passed
   ("stated in the spec") while PLM showed it does not match the
   measured file. The synthesizer flagged the tension; the plugin
   should decide that a control counts only when checked against the
   model and found correct — "stated" is not "passed".
4. **Stage self-reported counts need scorer recounts.** The NEMA-17
   PLM reviewer reported 13 findings; the file holds 14 (one major
   undercounted). All counts in this report are recounts from the
   files, not the reviewers' summaries.
5. **Coverage is still narrow.** Two real designs, but a matched pair
   from one domain (a motor and its pulley). No sheet-metal part, no
   moulded plastic part — so the pinned ABS wall range was never
   exercised by a finding. A third pilot fixture in one of those
   shapes would close that before launch claims breadth.
