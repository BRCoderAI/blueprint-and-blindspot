# Design specification — micro servo mounting bracket

## 1. Function and requirements

The bracket mounts a 9 g class micro servo (product "1143 MicroServo
High Torque Metal Gear v1") to a 3 mm aluminium base plate in a desktop
robotic arm. It must hold the servo against a 1.5 kg·cm stall torque
with no visible deflection, survive 10,000 load cycles, and allow the
servo to be removed with hand tools in under 2 minutes for servicing.

Acceptance criteria: static deflection under stall torque ≤ 0.5 mm
measured at the servo output spline; no cracking after 10,000 cycles;
servo removable in under 2 minutes with a 2 mm hex key.

## 2. Envelope and interfaces

- Servo envelope: 12.0 × 31.3 × 30.7 mm [measured: micro_servo.step].
- Bracket envelope: 16.0 × 35.0 × 14.0 mm [engineer].
- The bracket wraps the servo on three sides; the servo output spline
  exits through a Ø6.0 mm clearance hole in the bracket top face
  [engineer].
- Mounting: two M3 clearance holes through the bracket base, on a
  28.0 mm pitch, for M3 screws into the base plate [engineer].
- Servo retention: two M3 screws through the bracket side walls into
  the servo mounting ears [engineer].

## 3. Material and process

- Material: ABS, natural colour, injection moulded [engineer].
- Process: injection moulding, single cavity, family tool with the
  mating clip [engineer].
- Minimum wall thickness: 0.8 mm throughout [engineer].
- Draft: 1° on all vertical walls [engineer].
- Corner radii: 0.5 mm minimum [engineer].

## 4. Features and dimensions

- Base plate: 16.0 × 35.0 × 2.0 mm, flatness 0.1 mm [engineer].
- Side walls: 0.8 mm thick, 12.0 mm high [engineer].
- Servo mounting ears: two M3 clearance holes, Ø3.0 mm diameter,
  through the 0.8 mm side walls [engineer].
- Base mounting holes: two M3 clearance holes, Ø3.0 mm diameter,
  through the 2.0 mm base plate, on a 28.0 mm pitch [engineer].
- Spline clearance hole: Ø6.0 mm through the bracket top face
  [engineer].
- All driving dimensions toleranced ±0.1 mm; free dimensions ±0.25 mm
  [engineer].

## 5. Sustainability

- Recycled-content target: ≥ 30% recycled ABS [engineer].
- Material: virgin ABS, supplier grade GP-22, no recycled-content data
  supplied [engineer].
- End-of-life: bracket to be separated from the servo for recycling;
  target disassembly time under 2 minutes [engineer].
- Joining: bracket is solvent-bonded to the servo case along the full
  side-wall contact area for stiffness [engineer].

## 6. PLM and change control

- CAD system: Siemens NX, dataset `BRACKET_SERVO_MOUNT` Rev A
  [engineer].
- Servo source file: `micro_servo.step` (STEP AP242), dataset
  `MicroServo_v2` Rev B [engineer].
- Servo part count: 6 parts [measured: micro_servo.step].
- Change control: bracket dataset under change request CR-114; servo
  dataset released [engineer].

## 7. Cost

- Cost target: $4.20 per unit at 1,000 units [engineer].
- Basis: CNC-machined 6061 aluminium, 12 minutes machine time per unit
  [engineer].
- Tooling: none (machined from plate) [engineer].

## 8. Verification plan

- Static deflection: load the spline to stall torque on a bench rig,
  measure deflection with a dial indicator [engineer].
- Cycle life: 10,000 cycles on the robotic arm, inspect for cracking
  [engineer].
- Disassembly: time a technician removing the servo with a 2 mm hex
  key [engineer].
- Open assumptions: (1) stall torque 1.5 kg·cm is the worst case —
  closing evidence: servo datasheet torque curve [TO BE OBTAINED];
  (2) ABS grade GP-22 is available from the incumbent supplier —
  closing evidence: supplier confirmation [TO BE OBTAINED].

## 9. Known gaps

- No tolerance stack-up has been run on the 28.0 mm mounting pitch.
- No thermal analysis: the servo runs warm and the bracket is ABS.
