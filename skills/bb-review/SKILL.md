---
name: bb-review
description: >-
  Run the Goldfish review protocol on a CAD design specification.
  Fresh reviewers with no memory of the drafting conversation check the
  draft against the live CAD model and the stated requirements, in five
  stages: comprehension, DFM/manufacturing, cost, sustainability, and
  PLM consistency plus implementation readiness. Every finding must name
  a feature, dimension, tolerance, material, or dataset — never generic
  advice. Use to review a design draft before building it.
---

# Review — CAD Goldfish Review Protocol

Reviews a CAD design specification through specialised reviewer personas.
Each reviewer runs in a fresh context with no conversation history. That
context isolation is the mechanism: a reviewer who never saw the drafting
conversation cannot fill gaps from memory, so unstated assumptions and
blind spots surface.

## Delegation

A Goldfish runs in a fresh context with no conversation history. Spawn
each subagent with your harness's subagent tool. Each subagent is defined
in `agents/<file>.md`, and its frontmatter `name` is the subagent type
to request where your harness registers named subagents. Otherwise spawn
a general-purpose subagent and tell it to read that persona file first.
Pass the prompt verbatim and wait for the report.

If your harness cannot spawn fresh subagents, stop and tell the user: a
review in the same context is not a Goldfish review. Do not review in
the drafting context and call it a review.

## Execution constraints (CRITICAL)

1. **Artifact-first delivery (MANDATORY):** write every report to the
   working directory with your file-writing tool, then tell the user the
   file path in chat. Never present long reports in the chat pane.
2. **Plain English:** simple, direct, jargon-free. Explain mechanisms
   directly. No ungrounded promotional adjectives (`seamless`, `robust`,
   `blazingly fast`) and no decorative adverbs.
3. **Default to stress-testing:** never agree by default. Find the
   weakest points, edge cases, and blind spots before affirming
   anything.
4. **No glazing:** do not call the design "great", "brilliant", or
   "smart". Compliments without substance are noise.
5. **Critique first:** lead with what is wrong, missing, or risky before
   any merits.
6. **Concrete findings only (MANDATORY):** every finding MUST name a
   feature, dimension, tolerance, material, process parameter, cost
   figure, or dataset/revision. A finding without a named target is not
   a finding — drop it and say it was dropped. "Consider
   manufacturability", "review tolerances", and "check sustainability"
   are not findings.
7. **Verify against the model:** where the draft cites a CAD file, the
   reviewer MUST check the cited numbers against the file (bounding box,
   part count, volume, feature sizes where measurable). A cited number
   that does not match the file is a finding. A cited number the
   reviewer did not check is marked `UNVERIFIED`.
8. **One question at a time:** any interactive gate asks exactly one
   question and is the sole tool call in that turn.

## Inputs

- **`TargetFile`**: path to the design specification document. Required.
- **`ModelFiles`** (optional): CAD files the spec cites (STEP, IGES,
  BREP, STL). If the spec names a file, resolve it relative to the spec
  folder and give its path to every reviewer. If a cited file is missing,
  that is a finding (PLM stage), not a reason to stop.
- **`Step`** (optional): `interactive` (pause after each stage),
  `consolidated` (run all stages, one report), or a single stage
  (`comprehension`, `dfm`, `cost`, `sustainability`, `plm`). Default:
  ask the user once, then run.

## Workflow

### Step 1: Intake

Verify `TargetFile` is provided. If missing, ask for the path in chat
and end the turn. Read the spec. Resolve `ModelFiles` from the spec's
references. If a cited file resolves outside the working directory or
is a URL, list it in chat, ask which to include, and end the turn; if
no one can answer, leave it out and keep going.

### Step 2: Run the five stages

Run stages in order. In `interactive` mode, pause after each stage and
ask the engineer one question: continue, stop, or change scope. In
`consolidated` mode, run all five and write one report.

**Stage 1 — Comprehension.** Persona: `agents/bb-comprehension-reviewer.md`.
Can a competent engineer who never saw this project build the part from
this document alone? Findings: undefined terms, missing dimensions,
tolerances without datums, requirements without acceptance criteria,
sections that contradict each other. The reviewer reads ONLY the spec —
no CAD file, no conversation.

**Stage 2 — DFM / manufacturing.** Persona: `agents/bb-dfm-reviewer.md`.
Check every feature against the stated process and its limits: minimum
wall, draft, radii, hole sizes and clearances, tolerances the process
can hold, fastener and insert sizes. Check every cited model number
against the CAD file. Findings name the feature and the number that
fails, and the process limit it fails against.

**Stage 3 — Cost.** Persona: `agents/bb-cost-reviewer.md`. Check that
the cost story is internally consistent: process and material in the
cost section must match the material and process section. Check that
the named cost drivers are the ones that actually move cost for this
part at this quantity. Findings name the figure and the contradiction.

**Stage 4 — Sustainability.** Persona:
`agents/bb-sustainability-reviewer.md`. Check the material and
end-of-life claims: recycled-content data present or missing, material
health data, disassembly possible or blocked (bonding, overmoulding,
mixed materials), and whether the stated sustainability targets are
measurable. Missing data is a finding, not a pass. Findings name the
material, the target, and the missing evidence.

**Stage 5 — PLM consistency and implementation readiness.** Persona:
`agents/bb-plm-reviewer.md`. Check every dataset name, revision, and
source-file reference: does the dataset exist, is the revision current,
does the cited STEP format version match the file, does the part count
and envelope in the spec match the file? Check the verification plan:
is every requirement checkable, and does every open assumption have
closing evidence named? Findings name the dataset, revision, or file.

### Step 3: Synthesise

Persona: `agents/bb-synthesizer.md`. The synthesizer receives the five
stage reports (and nothing else — no drafting conversation) and merges
them into `review_report.md`:

- **Findings, ranked:** each finding has a severity (blocker / major /
  minor), a named target, the evidence (spec line or measured model
  number), and the stage that found it. Duplicates across stages are
  merged, with both stages noted.
- **Dropped findings:** findings any reviewer produced that were generic
  or wrong, listed with one line each saying why they were dropped.
- **Controls passed:** spec claims the reviewers checked against the
  model and found correct (bounding box, part count, format version).
  A review with no passed controls did not check the model — say so.
- **Verdict:** `NOT READY` (has blockers), `READY WITH CHANGES`
  (majors only), or `READY` (minors only).

Tell the user the file path. Suggest `bb-resolve` next. Do not fix the
spec yourself — the engineer decides which findings to address.
