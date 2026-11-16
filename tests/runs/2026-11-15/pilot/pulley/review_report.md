# Review report — GT2 timing pulley, 36 tooth, aluminium

**Verdict: NOT READY**

The design cannot be built as specified: the retention mechanism contradicts itself and the bore cannot transmit the required torque, and the tooth profile names no geometry. 61 stage findings merged into **38 findings: 3 blockers, 23 majors, 12 minors**. 23 stage findings were duplicates folded into merged findings; 3 generic findings were dropped. Controls passed: **42 entries collected across the five stages** (about 24 distinct checks — the dimensional checks were repeated by several stages).

## Stage disagreements

Where stages graded the same defect differently, the merged severity follows the severity definitions in the synthesizer brief (blocker = cannot be built, or spec contradicts the model on a driving fact; major = can be built but a requirement, process limit, or cost/sustainability claim fails; minor = clarity or missing non-driving data), and the disagreement is noted on the finding.

- **Tooth profile:** comprehension graded blocker; DFM and PLM graded major. Merged as blocker — no groove geometry is given at all, so the part is unbuildable, not merely uninspectable.
- **Recycled content ≥ 30%:** sustainability graded blocker; comprehension graded major; DFM, cost, and PLM graded minor. Merged as major — the target is unverifiable and contradicted by the spec's own "no data supplied", but it does not prevent building the part.
- **Cost target $3.80:** cost graded blocker; comprehension and PLM graded minor. Merged as major — the target has no verifiable basis, so the cost requirement fails, but it does not prevent building the part.
- **End-of-life "fully recyclable once stripped":** sustainability graded blocker. Merged as major — the claim rests on an unstated, unevidenced stripping step; it is a failed sustainability claim, not a build blocker.
- **Radial runout datum:** comprehension graded major; DFM graded minor. Merged as major — without a datum the acceptance criterion cannot be reproduced.
- **Belt centring:** comprehension graded major; PLM graded minor (PLM's point is narrower — the §8 check omits the 15 N tension). Merged as major.
- **Bore-to-shaft fit:** comprehension and DFM graded blocker; PLM graded major. Merged as blocker — zero interference means no press fit exists.
- **Comprehension's Controls passed vs PLM findings 2, 3, 11:** comprehension counted §6 identification (CAD system Siemens NX, dataset `PULLEY_GT2_36T` Rev B, source file `timing_pulley.step`) as "stated" in the spec. PLM found the stated dataset name and revision do not appear in the measured file (product "Aluminum Timing Pulley v1", no "Rev B") and the file contains no reference to Siemens NX. The identification is stated in the spec but does not match the file — the control records what the spec says, not what the file verifies.
- **PLM's runout control vs the runout finding:** PLM counts as passed that the runout criterion has a named verification method (§8 dial indicator). That does not cure the finding: the method names no datum, so the measurement cannot be reproduced.

## Blockers

### F1 — Retention contradicts itself: bore has no flat, yet retention "engages the shaft D-flat"
- **Severity:** blocker
- **Target:** bore / shaft D-flat engagement (§2, §9)
- **Stages:** comprehension (B1), DFM (B2), PLM (1)
- **Evidence:** §2 states "No set-screw hole, no keyway, no flat in the bore" and, in the same section, "Retention: press fit onto the motor shaft, engaging the shaft D-flat". §9 repeats the contradiction: "retention is friction only, on a bore that does not engage the shaft D-flat." Re-measured: the shaft flat is real (3.0 mm wide × 17.75 mm long plane at Z = 2.00), while the bore is a single plain Ø5.00 mm cylinder (area 263.9 mm²) with no flat, keyway, or set-screw hole. A round bore cannot engage a D-flat; the torque path is undefined.
- **Fix:** Pick one retention mechanism — D-flat in the bore (with flat depth, width, and angular orientation), a set screw (size, position, torque), or a defined interference fit — model it, and delete the contradicting sentence.

### F2 — Bore specified as clearance, called a press fit: zero interference
- **Severity:** blocker (PLM graded this major — see disagreements)
- **Target:** bore Ø5.00 mm tolerance +0.012/−0.000 (H7) vs shaft Ø5.00 mm (§2, §4, §8)
- **Stages:** comprehension (B2), DFM (B1), PLM (5)
- **Evidence:** §4 gives the bore as "Ø5.00 mm, tolerance +0.012/−0.000 (H7)"; §2 gives the mating NEMA-17 shaft as "Ø5.00 mm" with no shaft tolerance stated anywhere. Nominal-equal diameters give zero interference, and the H7 bore can be up to Ø5.012 mm against a nominal Ø5.00 mm shaft — up to 0.012 mm clearance, a clearance/slip fit, never a press fit. §8 then instructs to "check the pulley slides onto the motor shaft with a hand press fit" — a part that slides on by hand cannot transmit 40 N·cm by friction. No interference value, fit class (e.g. H7/p6), or minimum interference is stated anywhere.
- **Fix:** State the required interference (minimum and maximum, in mm) and the fit class, with the shaft tolerance band, so the bore tolerance is smaller than the shaft in every case.

### F3 — Tooth profile is unbuildable: "per the GT2 standard" names no geometry, tolerance, or inspection method
- **Severity:** blocker (DFM and PLM graded major — see disagreements)
- **Target:** 36-tooth GT2 tooth profile (§4, §9)
- **Stages:** comprehension (B3), DFM (M1), PLM (8)
- **Evidence:** §4 states only "Tooth profile per the GT2 standard". No standard body, edition, or document number is cited, and no tooth dimension is given: no groove width, groove depth, flank radius, tip radius, or pitch tolerance. The only derivable number is groove depth 1.20 mm ((22.40 − 20.0)/2 from the tip and root diameters in §2), which is never stated. §9 admits "Tooth profile tolerance is not stated: 'per the GT2 standard' names no tolerance class or inspection method." §4's general ±0.05 mm does not say whether it applies to tooth form, so the §8 belt-mesh check ("teeth seat fully") has no pass/fail criterion.
- **Fix:** Cite the exact GT2 standard document and edition, tabulate the groove geometry (width, depth, radii) with tolerances, and state the pitch tolerance and inspection method.

## Majors

### F4 — Radial runout tolerance has no datum
- **Severity:** major (DFM graded minor — see disagreements)
- **Target:** radial runout ≤ 0.05 mm at the tip diameter (§1, §8)
- **Stages:** comprehension (M1), DFM (m1)
- **Evidence:** §1 requires "radial runout ≤ 0.05 mm measured at the tip diameter" and §8 measures it "with a dial indicator" on the pulley "mount[ed] on the motor shaft". Neither section states the datum axis (bore axis, shaft axis, or hub axis), and the motor shaft's own runout is uncontrolled, so the measurement cannot be reproduced. No bore-to-tip concentricity callout exists.
- **Fix:** Name the datum (e.g. bore axis A) and the measurement setup, including the shaft runout limit.

### F5 — "Driving" vs "free" dimensions are never identified
- **Severity:** major
- **Target:** general tolerance ±0.05 mm driving / ±0.1 mm free (§4)
- **Stages:** comprehension (M2)
- **Evidence:** §4 states "All driving dimensions toleranced ±0.05 mm; free dimensions ±0.1 mm" but never lists which dimensions are driving. Tip diameter Ø22.40 mm, root diameter Ø20.0 mm, pitch diameter 22.92 mm, flange Ø25.50 mm, hub Ø16.00 mm, and the 7.0 mm tooth width carry no individual tolerances, so a builder cannot tell whether Ø22.40 mm is ±0.05 or ±0.1.
- **Fix:** Attach a tolerance to every dimension in §2 and §4, or list the driving dimensions explicitly.

### F6 — Bore tolerance vs anodize sequence is undefined
- **Severity:** major
- **Target:** Ø5.00 mm bore H7 vs clear anodize (§3, §4)
- **Stages:** comprehension (M3), DFM (M4)
- **Evidence:** §3 specifies "6061 aluminium, clear anodized" after "CNC machined from bar", and §4 gives the bore as Ø5.00 +0.012/−0.000. No anodize type or layer thickness is stated, and the spec never says whether the bore tolerance applies before or after anodizing, or whether the bore is masked. An anodize layer grows into the bore and changes its diameter by twice the layer thickness — enough to consume the whole 0.012 mm tolerance band on the single interface that provides retention.
- **Fix:** State anodize type and thickness (µm) and state that the bore tolerance applies after anodizing (or that the bore is masked/machined after anodizing).

### F7 — Material data missing: no temper, no REACH/RoHS status, no anodize seal chemistry
- **Severity:** major
- **Target:** 6061 aluminium, clear anodized (§3)
- **Stages:** comprehension (M4), sustainability (7)
- **Evidence:** §3 states only "Material: 6061 aluminium, clear anodized". No temper is given (e.g. T6, T651); temper determines strength, machinability, and whether the hub wall and press fit behave as assumed — 6061-O and 6061-T6 are different materials for engineering purposes. No REACH/RoHS status, restricted-substance statement, or anodize seal chemistry is given either, so material health cannot be assessed.
- **Fix:** State the temper (e.g. 6061-T6) and the governing material standard, plus the REACH/RoHS compliance status and the anodize process/seal chemistry from the supplier.

### F8 — No surface finish anywhere, including the press-fit bore
- **Severity:** major
- **Target:** bore Ø5.00 mm and tooth flanks (§2, §4)
- **Stages:** comprehension (M5)
- **Evidence:** The spec gives no surface-finish (Ra) requirement for any feature. The bore is the friction torque path (§2 retention) and the tooth flanks are the belt-mesh surfaces, yet neither has a finish value, so neither the friction nor the mesh can be controlled or inspected.
- **Fix:** State Ra for the bore, tooth flanks, flange faces, and hub outside diameter.

### F9 — Axial stack-up is ambiguous: hub position and bore length undefined
- **Severity:** major
- **Target:** hub Ø16.00 mm × 7.0 mm tall, overall height 17.0 mm (§2, §4)
- **Stages:** comprehension (M6)
- **Evidence:** §2 gives "Hub: Ø16.00 mm × 7.0 mm tall, on the top face" and overall height 17.0 mm. The numbers only add up (1.5 + 7.0 + 1.5 + 7.0 = 17.0) if the hub sits entirely above the top flange, but the spec never states that stacking order, never states which face is "top", and never states the bore length (through the full 17.0 mm, or only part of it). The axial position of the toothed section between the flanges is likewise not dimensioned.
- **Fix:** Provide a section view or an axial dimension chain from one datum face: flange positions, tooth-section position, hub start and end, and bore depth.

### F10 — Belt centring has no dimension or measurable test
- **Severity:** major (PLM graded its narrower point minor — see disagreements)
- **Target:** 6 mm GT2 belt in 7.0 mm tooth width between flanges (§1, §2, §8)
- **Stages:** comprehension (M7), PLM (9)
- **Evidence:** §2 gives a 6 mm belt in a 7.0 mm wide toothed section (1.0 mm total clearance, never stated), but no axial position of the belt relative to the flanges and no allowable off-centre value. §1 requires the belt to track "centred with no flange contact" under 15 N belt tension, and §8 tests it by "check the teeth seat fully and the belt tracks centred" — with no measurement, no duration, no load, and no tension value stated in the check, so the check as written does not test the stated condition.
- **Fix:** State the belt's nominal axial position and allowable off-centre (±mm), and state the test duration, tension (15 N), and how centring is measured.

### F11 — 10,000-hour life requirement has no test
- **Severity:** major
- **Target:** 10,000 hours without service (§1)
- **Stages:** comprehension (M8), PLM (7)
- **Evidence:** §1 requires the pulley to "run for 10,000 hours without service", but no section gives a life test, an accelerated-test method, or any acceptance criterion for wear, anodize loss, or bore loosening over that life. The §8 verification plan covers fit, mesh, runout, and a 50 N pull-off only — no life, wear, fatigue, or accelerated-ageing test of any kind.
- **Fix:** State how 10,000-hour life is verified (test duration, conditions, and pass criteria for wear and retention), or downgrade the requirement to a design goal.

### F12 — Recycled-content target ≥ 30% is unverifiable and contradicted
- **Severity:** major (sustainability graded blocker; DFM, cost, and PLM graded minor — see disagreements)
- **Target:** ≥ 30% recycled 6061 aluminium (§5)
- **Stages:** comprehension (M9), DFM (m4), cost (7), sustainability (1), PLM (13)
- **Evidence:** §5 sets a "Recycled-content target: ≥ 30% recycled 6061 aluminium" and in the next line states "Material: 6061 aluminium from the incumbent supplier, no recycled-content data supplied". No percentage, no supplier certificate, no chain of custody, and no named supplier — so the target cannot be checked at receipt and the material dataset is incomplete for the requirement it carries. No supplier can currently certify the 30% content, and any certified recycled-6061 bar premium is absent from the §7 cost figure, so the sustainability target and the cost target are not reconciled.
- **Fix:** Obtain a supplier declaration stating the actual recycled-content percentage and its evidence basis, price the target from a supplier that can certify ≥ 30%, and record what happens if the supplier cannot provide it.

### F13 — 15 N belt tension is an unclosed assumption, and the shaft bearing rating is unknown
- **Severity:** major
- **Target:** 15 N belt tension; motor front-bearing rating (§1, §8, §9)
- **Stages:** comprehension (M10), DFM (M3, M5)
- **Evidence:** §1 and §8 use "15 N belt tension" as the worst case, but §8 lists it as open assumption (2): "belt tension 15 N is the worst case — closing evidence: belt supplier tension table [TO BE OBTAINED]". Belt tracking, flange loading, and the bearing check all rest on a worst-case load whose supporting evidence has not been obtained. §9 adds that the 15 N radial load is carried by the motor's front bearing, "whose rating is not on file". The 10,000-hour no-service acceptance criterion (§1) depends on bearing life under this radial load, which cannot be assessed without the rating.
- **Fix:** Obtain the belt supplier tension table and the NEMA-17 motor front-bearing radial-load rating (and L10 life at 15 N), and record both numbers in the spec.

### F14 — 40 N·cm torque capacity has no evidence and no verification method
- **Severity:** major
- **Target:** acceptance criterion "no slip at 40 N·cm" (§1, §8)
- **Stages:** DFM (M2), PLM (6)
- **Evidence:** Spec §8 open assumption (1): "a press fit on a Ø5.00 mm bore transmits 40 N·cm without slip — closing evidence: pull-off and torque test [TO BE RUN]". The headline acceptance criterion rests on closing evidence that has not been run, and F1/F2 show the fit as specified supplies no interference and no positive drive, so there is no analysis showing the torque can be transmitted at all. §8 offers only a hand "does not rotate by hand" check and an axial pull-off test to 50 N — neither measures transmitted torque.
- **Fix:** Run the torque and pull-off tests, or add positive retention (F1) and re-state the criterion against it; add a torque test to §8 that applies 40 N·cm and measures slip.

### F15 — $3.80/unit cost target has no verifiable basis
- **Severity:** major (cost graded blocker; comprehension and PLM graded minor — see disagreements)
- **Target:** $3.80 per unit at 1,000 units, 4 minutes machine time (§7)
- **Stages:** comprehension (m5), cost (1), PLM (12)
- **Evidence:** §7 gives "$3.80 per unit at 1,000 units" with "4 minutes machine time per unit" as the only basis — no machine rate, no material cost, no setup cost, no anodize cost, no inspection cost, no labour rate, no scrap allowance, and no quote — so 4 min × an unstated rate cannot be checked against $3.80 and no line item sums to $3.80. The 4-minute figure itself has no operation breakdown (turning, tooth cutting, boring, finishing), so it cannot be checked against the measured geometry either.
- **Fix:** Publish a per-unit breakdown (material, machine time × stated shop rate, setup amortised over 1,000 units, anodize, inspection) that sums to the target, or cite the quote it comes from.

### F16 — Cost basis omits anodizing, which §3 requires
- **Severity:** major
- **Target:** §7 basis "CNC-machined 6061 aluminium" vs §3 "CNC machined from bar, single setup, then anodized"
- **Stages:** cost (2)
- **Evidence:** The cost basis prices machining only; the clear-anodize step specified in §3 has no cost line anywhere in §7, so the $3.80 figure is computed for a different (un-anodized) part than the one specified.
- **Fix:** Add a per-unit anodize line (batch rate at 1,000 units) to the §7 breakdown or restate the target as machined-only.

### F17 — H7 bore and ±0.05 / 0.05 mm runout tolerances are uncosted
- **Severity:** major
- **Target:** §4 bore Ø5.00 mm tolerance +0.012/−0.000 (H7); §1 radial runout ≤ 0.05 mm; §4 driving dimensions ±0.05 mm
- **Stages:** cost (3)
- **Evidence:** An H7 bore on Ø5.00 mm needs a reaming or precision-boring operation plus gauging, and the 0.05 mm runout check needs a dial-indicator inspection step (§8) — neither appears in the 4-minute machine-time basis or anywhere in §7, so the tightest tolerance on the part carries no cost.
- **Fix:** Cost the H7 bore as a separate operation (extra time or a reaming pass) and add per-unit inspection time for bore gauge and runout.

### F18 — Dominant cost driver is unpriced; material is trivial and unnamed
- **Severity:** major
- **Target:** §7 names only "4 minutes machine time" as its basis, with no rate and no driver ranking
- **Stages:** cost (4)
- **Evidence:** Measured volume 5,106.7 mm³ gives 13.8 g finished mass (≈ 23.4 g of bar stock), so 6061 material is on the order of $0.10 per unit and cannot move the $3.80 target — machine time, anodize, and setup dominate, yet the section prices none of them (no shop rate, no anodize line, no setup line).
- **Fix:** State the shop rate and rank the drivers (machine time first, then anodize, then setup) with a priced line for each.

### F19 — "Single-material part" contradicted by the anodized coating the spec itself names
- **Severity:** major
- **Target:** 6061 aluminium plus clear anodize coating (§3, §5)
- **Stages:** sustainability (3)
- **Evidence:** §5 calls the part "single-material" while §3 specifies a clear anodized coating, a second material layer on every surface; the re-measured model is a single solid (1 solid, 5,106.7 mm³) but a STEP solid carries no coating data, so the model cannot support the single-material claim for the finished, coated part.
- **Fix:** State the anodize layer as a separate material/coating stream in §5 with its thickness and composition, and revise the single-material claim accordingly.

### F20 — "No disassembly needed" contradicted by the press-fit joint, with no separation method or time
- **Severity:** major
- **Target:** pulley-to-NEMA-17 press-fit joint; end-of-life separation (§2, §5)
- **Stages:** sustainability (4, 9)
- **Evidence:** §5 says "no disassembly needed", but §2 retains the pulley by press fit on the Ø5.00 mm motor shaft, so at end-of-life the pulley must be pulled off the motor before the aluminium can be recycled as a separate stream, and no removal method, tool, or disassembly time is given. §5 gives no disassembly-time target and no measurement method. Note: the press-fit joint this finding assumes is itself unbuildable as specified (F1, F2) — the joint must be defined before its separation step can be.
- **Fix:** Add an end-of-life separation step for the joint with a stated method and disassembly time, plus a disassembly-time target with its measurement method, or record that none is set.

### F21 — No carbon or energy target, method, or evidence anywhere in the spec
- **Severity:** major
- **Target:** whole-part carbon footprint and process energy (§5, §7)
- **Stages:** sustainability (5)
- **Evidence:** §5 contains only the recycled-content target and the end-of-life claim — no carbon target, no energy target, no measurement method, and no figure — while §7 states 4 minutes of CNC machine time per unit with no kWh per unit or machine power.
- **Fix:** Add a carbon target and an energy-per-unit figure with their measurement methods, or record explicitly that neither is assessed.

### F22 — Machining waste of at least 41% of the bar is unaddressed
- **Severity:** major
- **Target:** 6061 aluminium bar stock; CNC machining (§3, §7)
- **Stages:** sustainability (6)
- **Evidence:** §3/§7 state "CNC machined from bar" with no bar size, yield, or swarf-recycling statement, while the measured envelope (Ø25.50 × 17.00 mm) gives a minimum enclosing bar volume of 8,682.0 mm³ against a finished volume of 5,106.7 mm³, so at least 3,575.3 mm³ — 41.2% of the minimum bar — is removed as chips, and any bar larger than the envelope wastes more.
- **Fix:** State the actual bar size, the material yield, and whether the swarf is collected and recycled, with the recycled-content accounting for it.

### F23 — End-of-life claim "fully recyclable once the anodize layer is stripped" is conditional with no stripping evidence
- **Severity:** major (sustainability graded blocker — see disagreements)
- **Target:** 6061 aluminium, clear anodized (§3, §5)
- **Stages:** sustainability (2)
- **Evidence:** §5 claims the part is "fully recyclable as aluminium once the anodize layer is stripped" but names no stripping method, facility, or evidence that stripping happens, and gives no anodize thickness or composition; the recyclability claim therefore rests on an unstated, unevidenced step.
- **Fix:** Name the stripping process and the recycler/route that performs it, or downgrade the claim to recyclable subject to a stated stripping route.

### F24 — Dataset name and revision do not match the cited file
- **Severity:** major
- **Target:** dataset `PULLEY_GT2_36T` Rev B (§6)
- **Stages:** PLM (2)
- **Evidence:** The STEP file's product is "Aluminum Timing Pulley", "Aluminum Timing Pulley v1" — the string `PULLEY_GT2_36T` and any "Rev B" appear nowhere in the file, and the file version is v1, not Rev B.
- **Fix:** Correct §6 to the dataset name and revision that actually identify this file, or re-export and check in the file under `PULLEY_GT2_36T` Rev B.

### F25 — "Released" change-control status cannot be tied to the measured file
- **Severity:** major
- **Target:** dataset `PULLEY_GT2_36T` Rev B, §6 "Change control: pulley dataset released"
- **Stages:** PLM (3)
- **Evidence:** The release claim attaches to Rev B, but the cited file is v1 (see F24), so there is no evidence the released revision is the revision measured here — the released file and the reviewed file may not be the same revision.
- **Fix:** State the release status against the revision that matches the file on record (v1, or Rev B once F24 is resolved) and cite the release record.

### F26 — Mating part has no dataset, revision, or change-control status
- **Severity:** major
- **Target:** NEMA-17 stepper motor (§2, mating part)
- **Stages:** PLM (4)
- **Evidence:** §2 depends on nema17.step (product "NEMA-17 Stepper Motor v11", 5 solids), but §6 names no dataset, revision, or change-control status for it, so a superseded motor revision could change the shaft interface without this spec noticing.
- **Fix:** Add the motor dataset name, revision, and release status to §6.

## Minors

### F27 — D-flat dimensions incomplete
- **Severity:** minor
- **Target:** shaft D-flat, 0.5 mm deep, 17.75 mm long (§2)
- **Stages:** comprehension (m1)
- **Evidence:** §2 gives the shaft D-flat as "0.5 mm deep, 17.75 mm long" but not its width (chord) or its axial position along the shaft, so a mating flat (if one were added per F1) could not be dimensioned from this spec. (The model does carry the flat — 3.0 mm wide, Y 20.50..38.25 — but the spec does not state it.)
- **Fix:** State the flat width and its axial start position from the shaft end.

### F28 — Flange-to-tooth clearance and edge treatment missing
- **Severity:** minor
- **Target:** flanges Ø25.50 mm × 1.5 mm thick (§2, §4); bore mouths, flange outside edges, hub edges
- **Stages:** comprehension (m2), DFM (m3)
- **Evidence:** The flange outside diameter overhangs the tooth tip diameter by 1.55 mm radially ((25.50 − 22.40)/2, never stated), and no chamfer, edge break, or burr requirement is given for the flange rims, hub edge, or bore mouths anywhere in the spec. Re-measured, the bore cylinder spans Y 0.10..16.90 within the 17.00 mm height, i.e. 0.10 mm entry breaks exist at both bore mouths, yet the spec contains no chamfer or edge-break callout — so as-built breaks are uncontrolled on a part that is handled and anodized.
- **Fix:** State the flange overhang and a maximum edge break (e.g. 0.2 mm × 45° or "break sharp edges"), and add bore-mouth chamfer callouts to the drawing.

### F29 — "Hand press fit" and 50 N pull-off are undefined
- **Severity:** minor
- **Target:** pull-off test 50 N; hand press fit (§8)
- **Stages:** comprehension (m3)
- **Evidence:** §8 requires an "axial pull test to 50 N; the pulley must not move", but the spec never derives 50 N from any service axial load, and "hand press fit" states no assembly force or method. A 50 N pass limit with no service-load basis is an arbitrary number.
- **Fix:** State the service axial load the 50 N derives from, and the assembly force/method for the press fit.

### F30 — "Single setup" and stock size undefined
- **Severity:** minor
- **Target:** CNC machined from bar, single setup (§3)
- **Stages:** comprehension (m4), DFM (m5)
- **Evidence:** §3 states "CNC machined from bar, single setup, then anodized" but gives no bar stock diameter or length, no setup datum, and no definition of what "single setup" constrains (e.g. whether the bore and tooth profile are cut without re-chucking). The bore, hub, and flanges are turned features while the 36 grooves with R0.25 fillets are milled features, and no machine type (e.g. mill-turn) is stated — so if the teeth need a second setup, the bore-to-tooth concentricity behind the ≤0.05 mm runout criterion (§1) is uncontrolled.
- **Fix:** State the bar stock size and the setup datum and machine type that achieves a single setup, or add a bore-to-tip concentricity tolerance, or delete "single setup" as a process instruction.

### F31 — Undefined terms: GT2, NEMA-17, H7, anodize type
- **Severity:** minor
- **Target:** terminology (§2, §3, §4)
- **Stages:** comprehension (m6)
- **Evidence:** The spec uses "GT2", "NEMA-17", "H7", and "clear anodized" without citing the governing standard for any of them (GT2 tooth standard, NEMA ICS 16 / motor standard, ISO 286 for H7, anodize specification such as MIL-A-8625 Type II). A stranger must guess which edition applies.
- **Fix:** Cite the standard and edition for each term at first use.

### F32 — No axial locating dimension: press depth / seating face is unstated
- **Severity:** minor
- **Target:** pulley axial position on the 20.0 mm shaft protrusion
- **Stages:** DFM (m2)
- **Evidence:** Spec §2/§8 give no seating face or press depth; re-measured, the pulley is 17.0 mm tall on a shaft protruding 20.0 mm beyond the motor front face, leaving 3.0 mm of shaft exposed with nothing stating where the pulley stops. The belt plane's position relative to the motor face is uncontrolled, so assembly cannot be repeated to a defined position.
- **Fix:** Dimension the seating (e.g. bottom flange against the motor front face) and the belt-centre distance from that face.

### F33 — Setup / first-article cost at 1,000 units is never amortised
- **Severity:** minor
- **Target:** §7 "Tooling: none (machined from bar)" and §3 "single setup", against the $3.80 target at 1,000 units
- **Stages:** cost (5)
- **Evidence:** A single-setup CNC job still carries programming, fixturing, and first-article time, none of which is stated or amortised per unit in §7 — the quantity is stated but no setup figure is tied to it.
- **Fix:** State setup hours once and show the per-unit share at 1,000 units.

### F34 — GT2 tooth cutting needs tooling the cost section claims is "none"
- **Severity:** minor
- **Target:** §7 "Tooling: none (machined from bar)" vs §4 "36 teeth" and §2 "36 grooves"
- **Stages:** cost (6)
- **Evidence:** Cutting 36 GT2 tooth profiles needs a dedicated form cutter or hob — a consumable/tooling expense with a finite life — which the "none" line and the 4-minute basis both ignore. (Measured: 36 root segments Ø20.00 mm, 36 tip segments Ø22.40 mm, 144 R0.25 fillet faces.)
- **Fix:** Add a per-unit tooling/consumable allowance for the GT2 cutter, amortised over its expected life at 1,000 units.

### F35 — No part mass, so no recycled mass or carbon figure can be derived
- **Severity:** minor
- **Target:** 6061 aluminium part mass (§5)
- **Stages:** sustainability (8)
- **Evidence:** The spec gives no part mass and no 6061 density; the measured volume is 5,106.7 mm³ (re-measured, confirmed), but without a stated density or mass the recycled-content mass and any carbon figure cannot be computed from the spec.
- **Fix:** Record the part mass (and the density used) in §5.

### F36 — Anodizing process energy and chemistry ignored
- **Severity:** minor
- **Target:** clear anodizing process (§3)
- **Stages:** sustainability (10)
- **Evidence:** §3 lists anodizing as a process step with no energy, chemical, or waste-water data, so a process step with known energy and chemical implications is carried in §5's end-of-life claim with no assessment.
- **Fix:** Add the anodizing energy per unit and the process chemistry/waste route from the supplier.

### F37 — Bearing-rating gap names no closing evidence
- **Severity:** minor
- **Target:** §9 "No check of belt tension load against the motor shaft bearing rating"
- **Stages:** PLM (10)
- **Evidence:** The gap is recorded, but unlike the §8 open assumptions it names no evidence that would close it (no bearing datasheet, rating, or owner), so it can sit open indefinitely. (The missing rating itself is F13; this finding is the record-keeping defect in the §9 entry.)
- **Fix:** Add the closing evidence (motor bearing rating from the motor datasheet) and an owner to the §9 entry.

### F38 — "Siemens NX" CAD-system claim has no evidence in the cited file
- **Severity:** minor
- **Target:** §6 "CAD system: Siemens NX"
- **Stages:** PLM (11)
- **Evidence:** The cited STEP AP214 file contains no reference to Siemens NX, so the claim rests on the engineer's word alone.
- **Fix:** Cite the NX dataset or part-file reference that shows the model origin, or mark the claim as engineer-stated rather than file-verified.

## Dropped findings

- "The spec is hard to follow" (comprehension) — names no feature, dimension, tolerance, material, or dataset.
- "More detail is needed overall" (comprehension) — names no feature, dimension, tolerance, material, or dataset.
- "The verification plan could be stronger" (comprehension) — names no feature, dimension, tolerance, material, or dataset.

No stage finding was dropped as wrong: no finding was contradicted by evidence quoted in another stage's report. (The DFM pinned limits — Protolabs moulding wall range and ISO 273 M3 clearance — produced no findings and are not counted as dropped.)

## Controls passed — 42 entries collected

Counts by stage: comprehension 5, DFM 14, cost 5, sustainability 3, PLM 15. The same dimensional checks were repeated by several stages, so the 42 entries cover about 24 distinct checks.

**Comprehension (5):** §6 PLM identification stated (Siemens NX, dataset `PULLEY_GT2_36T` Rev B, source file `timing_pulley.step` STEP AP214, part count 1 solid); hub-wall arithmetic (16.0 − 5.0)/2 = 5.5 mm correct; pitch-diameter arithmetic 36 × 2 / π = 22.92 mm correct; overall-height arithmetic 1.5 + 7.0 + 1.5 + 7.0 = 17.0 mm consistent (assuming the hub sits above the top flange — see F9); §9 correctly flags the missing bearing-rating check, the missing set-screw provision, and the unstated tooth-profile tolerance.

**DFM (14):** envelope Ø25.50 × 17.00 mm (bounding box 25.50 × 17.00 × 25.50 mm); part count 1 solid, volume 5,106.7 mm³, 299 faces; flanges 2× Ø25.50 mm × 1.5 mm thick (face planes at Y 0.00, 1.50, 8.50, 10.00); toothed section 7.0 mm wide, 36 teeth (36 root segments Ø20.00 mm, 36 tip segments Ø22.40 mm, 144 R0.25 fillet faces); tip diameter Ø22.40 mm, root diameter Ø20.00 mm; pitch diameter 22.92 mm; bore Ø5.00 mm through, no set-screw hole, no keyway, no flat in the bore; hub Ø16.00 mm × 7.0 mm tall (D16.00 face spans Y 10.00..17.00); hub wall 5.5 mm; overall stack arithmetic 1.5 + 7.0 + 1.5 + 7.0 = 17.0 mm; mating shaft Ø5.00 mm with 0.5 mm deep D-flat, 17.75 mm long (flat face 3.0 mm wide × 17.75 mm long at Z = 2.00, Y 20.50..38.25; shaft solid 24.00 mm long, protruding 20.0 mm beyond the motor front face); motor envelope 42.30 × 55.00 × 42.30 mm, 5 solids, volume 58,681.8 mm³; no fastener holes in the pulley, so no clearance-hole check applies; spec §3 correct that no moulded features exist, so draft and ribs do not apply.

**Cost (5):** material/process match — §3 (CNC machined 6061 aluminium from bar, then anodized) matches the §7 basis material and process; quantity stated — the $3.80 figure is tied to 1,000 units; no mould-tooling contradiction — the part has no moulded features and the model confirms a single solid with no moulded geometry; geometry does not contradict the machining basis — re-measured model is 1 solid, 5,106.7 mm³, Ø25.50 × 17.00 mm envelope, consistent with "machined from bar" and with material being a minor cost driver; all spec numbers cited from the CAD files check out against re-measurement (envelope Ø25.50 × 17.00 mm, tip Ø22.40 mm, root Ø20.00 mm, bore Ø5.00 mm, hub Ø16.00 × 7.0 mm, flanges 2× Ø25.50 × 1.5 mm, 36 teeth, 1 solid; mating shaft Ø5.00 mm confirmed).

**Sustainability (3):** one solid, no mixed-material features in the model (1 solid, 299 faces, volume 5,106.7 mm³, no second solid, inserted fastener, overmould, or solvent-bonded joint) — consistent with §6 ("1 solid") and with no moulded features (§3); spec dimensional claims checked against the model and correct (envelope Ø25.50 × 17.00 mm, bore Ø5.00 mm, hub Ø16.00 mm, flanges Ø25.50 mm, tip Ø22.40 mm, root Ø20.00 mm, 36 teeth); no disassembly-blocking joining method inside the part itself (no bonded, overmoulded, or permanently fastened sub-part).

**PLM (15):** source file exists at the stated path and format matches — `timing_pulley.step` is STEP AP214, as §6 states; part count 1 solid, 299 faces, volume 5,106.7 mm³ — matches §6; envelope 25.50 × 17.00 × 25.50 mm — matches §2; toothed section 7.0 mm wide (Y 1.50..8.50), 36 grooves — matches §2/§4; tip diameter Ø22.40 mm, root diameter Ø20.00 mm — matches §2/§4; pitch diameter 22.92 mm (36 × 2 / π = 22.92) — derived figure in §2 correct; bore Ø5.00 mm through, no set-screw hole, no keyway, no flat — matches §2; flanges 2× Ø25.50 mm × 1.5 mm thick — matches §4; hub Ø16.00 mm × 7.0 mm tall on the top face (Y 10.00..17.00) — matches §2/§4; hub wall (16.0 − 5.0)/2 = 5.5 mm — derived figure in §3 correct; mating shaft Ø5.00 mm, D-flat 0.5 mm deep (plane at Z = 2.00 against a Ø5.00 shaft surface at Z = 2.50), 17.75 mm long (Y 20.50..38.25) — matches §2; belt vs toothed section — 6 mm belt in a 7.0 mm wide toothed section, figures in §2 agree; runout acceptance criterion (§1, ≤ 0.05 mm) has a named verification method (§8, dial indicator at the tip diameter) — this does not cure F4, which is the missing datum; open assumptions (1) and (2) in §8 each name the evidence that would close them (torque/pull-off test; belt supplier tension table); no broken internal section references — the spec contains no numbered cross-references pointing at non-existent sections.
