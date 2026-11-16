# Design specification — GT2 timing pulley, 36 tooth, aluminium

## 1. Function and requirements

The pulley drives a 6 mm GT2 timing belt on a desktop 3D printer
extruder drive. It mounts on the Ø5.00 mm shaft of a NEMA-17 stepper
motor and must transmit the motor torque to the belt without slip,
hold the belt centred between its flanges, and run for 10,000 hours
without service.

Acceptance criteria: no slip at 40 N·cm transmitted torque; belt
tracks centred with no flange contact under 15 N belt tension;
radial runout ≤ 0.05 mm measured at the tip diameter.

## 2. Envelope and interfaces

- Overall: Ø25.50 mm flanges, 17.0 mm tall [measured:
  timing_pulley.step].
- Toothed section: 7.0 mm wide, between the flanges [measured:
  timing_pulley.step]. Belt: GT2, 6 mm wide [engineer].
- Teeth: 36 grooves, tip diameter Ø22.40 mm, root diameter Ø20.0 mm
  [measured: timing_pulley.step]. Pitch diameter 22.92 mm
  (36 × 2 mm pitch) [derived].
- Bore: Ø5.00 mm through [measured: timing_pulley.step]. No set-screw
  hole, no keyway, no flat in the bore [measured: timing_pulley.step].
- Hub: Ø16.00 mm × 7.0 mm tall, on the top face [measured:
  timing_pulley.step].
- Mating part: NEMA-17 motor shaft Ø5.00 mm with a 0.5 mm deep
  D-flat, 17.75 mm long [measured: nema17.step].
- Retention: press fit onto the motor shaft, engaging the shaft
  D-flat [engineer].

## 3. Material and process

- Material: 6061 aluminium, clear anodized [engineer].
- Process: CNC machined from bar, single setup, then anodized
  [engineer].
- Minimum wall: hub wall around the bore is 5.5 mm
  ((16.0 − 5.0) / 2) [derived].
- No moulded features; draft and ribs do not apply [engineer].

## 4. Features and dimensions

- Flanges: 2× Ø25.50 mm × 1.5 mm thick [measured:
  timing_pulley.step].
- Toothed section: 7.0 mm wide, 36 teeth [measured:
  timing_pulley.step].
- Bore: Ø5.00 mm, tolerance +0.012/−0.000 (H7) [engineer].
- Hub: Ø16.00 mm × 7.0 mm [measured: timing_pulley.step].
- All driving dimensions toleranced ±0.05 mm; free dimensions ±0.1 mm
  [engineer].
- Tooth profile per the GT2 standard [engineer].

## 5. Sustainability

- Recycled-content target: ≥ 30% recycled 6061 aluminium [engineer].
- Material: 6061 aluminium from the incumbent supplier, no
  recycled-content data supplied [engineer].
- End-of-life: single-material part, fully recyclable as aluminium
  once the anodize layer is stripped; no disassembly needed
  [engineer].

## 6. PLM and change control

- CAD system: Siemens NX, dataset `PULLEY_GT2_36T` Rev B [engineer].
- Pulley source file: `timing_pulley.step` (STEP AP214), dataset
  `PULLEY_GT2_36T` Rev B [engineer].
- Pulley part count: 1 solid [measured: timing_pulley.step].
- Change control: pulley dataset released [engineer].

## 7. Cost

- Cost target: $3.80 per unit at 1,000 units [engineer].
- Basis: CNC-machined 6061 aluminium, 4 minutes machine time per unit
  [engineer].
- Tooling: none (machined from bar) [engineer].

## 8. Verification plan

- Bore fit: gauge the Ø5.00 mm bore; check the pulley slides onto
  the motor shaft with a hand press fit and does not rotate by hand
  [engineer].
- Belt mesh: run the belt over the pulley, check the teeth seat fully
  and the belt tracks centred [engineer].
- Runout: mount the pulley on the motor shaft, measure radial runout
  at the tip diameter with a dial indicator [engineer].
- Pull-off: axial pull test to 50 N; the pulley must not move
  [engineer].
- Open assumptions: (1) a press fit on a Ø5.00 mm bore transmits
  40 N·cm without slip — closing evidence: pull-off and torque test
  [TO BE RUN]; (2) belt tension 15 N is the worst case — closing
  evidence: belt supplier tension table [TO BE OBTAINED].

## 9. Known gaps

- No check of belt tension load against the motor shaft bearing
  rating: 15 N radial load on a Ø5 mm shaft is carried by the motor's
  front bearing, whose rating is not on file.
- No set-screw provision: retention is friction only, on a bore that
  does not engage the shaft D-flat.
- Tooth profile tolerance is not stated: "per the GT2 standard" names
  no tolerance class or inspection method.
