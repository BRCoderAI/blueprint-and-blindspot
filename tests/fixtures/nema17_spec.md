# Design specification — NEMA-17 stepper motor integration, extruder drive

## 1. Function and requirements

The motor drives the filament feed on a desktop 3D printer extruder
through a 36-tooth GT2 timing pulley on its shaft. It must hold
position against the extruder back-pressure torque, index 1.8° per
full step, and run for 10,000 hours without service.

Acceptance criteria: holding torque ≥ 40 N·cm at rated current;
step angle 1.8° ± 5% per step; shaft runout ≤ 0.05 mm measured at the
pulley hub; motor case temperature ≤ 80 °C after 1 hour at rated
current in 25 °C still air.

## 2. Envelope and interfaces

- Motor body: 42.30 × 35.00 × 42.30 mm [measured: nema17.step].
- Overall length with shaft: 55.00 mm [measured: nema17.step].
- Shaft: Ø5.00 mm, protrudes 20.0 mm beyond the front face
  [measured: nema17.step]. D-flat 0.5 mm deep × 17.75 mm long on the
  shaft [measured: nema17.step].
- Mating part: GT2 timing pulley, 36 tooth, bore Ø5.00 mm
  [measured: timing_pulley.step].
- Mounting: four M3 screws through the Ø3.07 mm mounting holes on a
  31.0 mm square pitch, into the extruder mounting plate [engineer;
  holes measured: nema17.step].
- Centering: Ø22.0 mm pilot recess on the front face, 2.2 mm deep,
  receives the Ø22.0 mm locating boss on the mounting plate
  [engineer; recess measured: nema17.step].
- Front cap shaft opening: Ø10.0 mm [measured: nema17.step].
- Electrical: 4-wire, 1.5 A/phase rated, 12 V nominal [engineer].

## 3. Material and process

- Purchased assembly, not manufactured in-house: steel stator
  laminations, aluminium end caps, copper windings, NdFeB rotor
  magnets [engineer].
- Process: none — bought-in motor, accepted against this spec
  [engineer].
- No moulded or machined features are defined by this spec; the
  mounting plate is a separate part [engineer].

## 4. Features and dimensions

- Body: 42.30 × 35.00 × 42.30 mm [measured: nema17.step].
- Shaft: Ø5.00 mm × 24.0 mm long, 20.0 mm protrusion [measured:
  nema17.step].
- D-flat: 0.5 mm deep, 17.75 mm long, starting 2.0 mm from the front
  face [measured: nema17.step].
- Mounting holes: 4× Ø3.07 mm on 31.0 mm pitch [measured:
  nema17.step].
- Pilot recess: Ø22.0 mm × 2.2 mm deep [measured: nema17.step].
- All driving dimensions toleranced ±0.1 mm; free dimensions ±0.25 mm
  [engineer].

## 5. Sustainability

- Recycled-content target: ≥ 20% recycled aluminium in the end caps
  [engineer].
- Material: end caps are virgin aluminium, no recycled-content data
  supplied [engineer].
- End-of-life: the motor is a mixed-material assembly (steel, copper,
  aluminium, magnets, insulation); it is not designed for
  disassembly, and material recovery requires shredding [engineer].
- RoHS compliance claimed by the supplier; certificate not on file
  [engineer].

## 6. PLM and change control

- CAD system: Siemens NX, dataset `NEMA17_EXTRUDER` Rev C [engineer].
- Motor source file: `nema17.step` (STEP AP214), dataset
  `NEMA17_MOTOR` Rev B [engineer].
- Motor part count: 5 solids [measured: nema17.step].
- Change control: motor dataset under change request CR-207; mounting
  plate dataset released [engineer].

## 7. Cost

- Cost target: $14.50 per unit at 1,000 units [engineer].
- Basis: purchased motor $12.80 + mounting hardware $1.70 [engineer].
- Tooling: none (bought-in part) [engineer].

## 8. Verification plan

- Holding torque: stall the shaft on a bench rig at rated current,
  measure torque with a torque meter [engineer].
- Step accuracy: index 200 steps, measure shaft angle with an encoder
  [engineer].
- Fit check: assemble the motor to the mounting plate with M3 screws
  and the pulley on the shaft; check runout at the pulley hub with a
  dial indicator [engineer].
- Thermal: run 1 hour at rated current, measure case temperature with
  a thermocouple [engineer].
- Open assumptions: (1) holding torque ≥ 40 N·cm is the worst case —
  closing evidence: supplier datasheet torque curve [TO BE OBTAINED];
  (2) the Ø22.0 mm locating boss on the mounting plate exists at the
  stated diameter — closing evidence: mounting plate drawing
  [TO BE OBTAINED].

## 9. Known gaps

- No supplier datasheet on file: torque, current, and insulation
  class are requirements, not verified values.
- No thermal analysis: the motor runs warm and sits against an
  aluminium mounting plate that is also the extruder heat sink.
- Pulley retention relies on a press fit onto the D-flat shaft; the
  pulley hub carries no set screw.
