# Measured facts — NEMA-17 stepper motor

Source file: `~/workspace/cad-viewer/test-fixtures/nema17.step`
Measured with build123d / OCCT 8.0 (simprep venv). All numbers below
are measurements from the file, not spec claims.

- STEP AP214 (`AUTOMOTIVE_DESIGN { 1 0 10303 214 3 1 1 }`).
- Product: "NEMA-17 Stepper Motor", "NEMA-17 Stepper Motor v11".
- Solids: 5. Faces: 278. Total volume: 58,681.8 mm³.
- Envelope: 42.30 × 55.00 × 42.30 mm (Y is the motor axis).
  Body: 42.30 × 35.00 × 42.30 mm, Y −16.50..18.50.
  Shaft extends to Y 38.50; overall length 55.00 mm.
- Body stack (Y extents): rear section −16.50..−4.00 (12.5 mm),
  middle section −6.00..6.00 (12.0 mm), front stator 4.00..14.50
  (10.5 mm), front end cap 14.50..18.50 (4.0 mm). Sections overlap;
  union body length is 35.0 mm.
- Shaft: Ø5.00 mm, 24.0 mm long (Y 14.50..38.50). Protrudes 20.0 mm
  beyond the front face (Y 18.50..38.50). Cylindrical portion ends at
  Y 37.75.
- Shaft D-flat: one flat milled on the shaft, 0.5 mm deep (plane at
  Z = 2.00, shaft surface at Z = 2.50), 17.75 mm long (Y 20.50..38.25).
- Mounting holes: 4× Ø3.07 mm, centres (±15.50, ±15.50) — 31.0 mm
  square pitch — in the front end cap. In the file they appear as 64
  small Ø3.07 cylindrical faces (segmented in the source model);
  treat the diameter as Ø3.07 and the pitch as 31.0 mm.
- Front face: Ø22.0 mm circular pilot recess, 2.2 mm deep
  (Y 16.15..18.35); front face plane at Y 18.50.
- Front cap shaft opening: Ø10.0 mm (shaft Ø5.0 passes through it).
- Other cylindrical features: Ø1.0 (40 faces) and Ø2.0 (9 faces)
  small internal detail — not dimensioned in the spec.
