# The reviewers

Five Goldfish reviewers, each in a fresh context, each checking one
lens. Every reviewer receives only the specification and the CAD files
it cites — no drafting conversation. Every finding must name a feature,
dimension, tolerance, material, or dataset. Generic advice is not a
finding.

## Comprehension — `agents/bb-comprehension-reviewer.md`

Can a competent engineer who never saw the project build the part from
this document alone? Reads only the spec.

Checks: undefined terms, missing dimensions, tolerances without datums,
requirements without acceptance criteria, contradictions between
sections, assumed knowledge not written in the spec.

## DFM / manufacturing — `agents/bb-dfm-reviewer.md`

Every feature against the stated process and its limits; every cited
model number against the CAD file.

Checks: minimum wall, draft, radii, hole sizes and clearances,
fastener callouts, tolerances the process can hold, mating faces and
assembly access, and agreement between spec numbers and the measured
model (envelope, part count, feature sizes).

Example finding: "Bracket wall 0.8 mm, injection-moulded ABS — below
the 1.5 mm practical minimum for ABS. Blocker."

## Cost — `agents/bb-cost-reviewer.md`

The cost story must be internally consistent.

Checks: process and material in the cost section match the material and
process section; named cost drivers are the ones that actually move
cost at the stated quantity; tolerance cost; missing breakdowns.

Example finding: "Cost section prices CNC-machined 6061 aluminium at
$4.20/unit, but the material section specifies ABS injection moulding.
Blocker — the cost figure belongs to a different process and material."

## Sustainability — `agents/bb-sustainability-reviewer.md`

GreenBOM-style: material, energy, and end-of-life from the bill of
materials, not from claims.

Checks: recycled-content data present or missing against the stated
target; material-health data; disassembly possible or blocked by
bonding, overmoulding, or mixed materials; whether sustainability
targets are measurable. Missing data is a finding, not a pass.

Example finding: "Sustainability target is ≥30% recycled content, but
the material section names virgin ABS with no recycled-content data.
Major."

## PLM / Teamcenter — `agents/bb-plm-reviewer.md`

Every dataset, revision, and source-file reference against the cited
files and the stated PLM state.

Checks: dataset name and revision match the file; stated STEP format
version matches the file; stated part count and envelope match the
measured file; change-control status stated for every dependency;
every requirement has a verification method; every open assumption
names its closing evidence.

Example finding: "Spec cites dataset MicroServo_v2 Rev B, but the
source STEP file is product '1143 MicroServo High Torque Metal Gear
v1'. Major — revision mismatch."

## Synthesizer — `agents/bb-synthesizer.md`

Merges the five stage reports into one ranked report: duplicates
merged, generic or wrong findings dropped with reasons, controls
passed counted, verdict `NOT READY`, `READY WITH CHANGES`, or `READY`.
