# How it works

## The two roles

**Elephant**, one agent holds the whole context: the design intent,
the requirements, the earlier decisions, the Teamcenter state. It
explores the idea with the engineer (`bb-brainstorm`) and drafts the
specification (`bb-draft`), one section at a time, pausing for feedback.

**Goldfish**, independent reviewers examine the draft and the cited
CAD files **without the earlier conversation**. Each reviewer runs in a
fresh subagent context. A reviewer who never saw the drafting
conversation cannot fill gaps from memory, so unstated assumptions,
contradictions, and blind spots surface. That context isolation is the
whole mechanism.

**You**, the engineer resolves trade-offs, approves the design, and
decides what to build. The plugin never approves anything on your
behalf.

## The workflow

```
bb-brainstorm  →  concepts_brief.md
bb-draft       →  design_draft.md        (one section at a time)
bb-review      →  review_report.md       (five fresh reviewers)
bb-resolve     →  resolution_record.md   (every finding dispositioned)
```

You can also enter at any step: review an existing spec with
`bb-review` alone, or check whether checked-in docs still match the
current model with `bb-drift-report`.

## The five review stages

Run in order, in `bb-review`:

1. **Comprehension**, can a competent engineer who never saw the
   project build the part from this document alone? Reads only the
   spec: no CAD file, no conversation.
2. **DFM / manufacturing**, every feature against the stated process
   limits; every cited model number against the CAD file.
3. **Cost**, the cost story must be internally consistent: the process
   and material in the cost section must match the rest of the spec.
4. **Sustainability**, material data, recycled content, end-of-life
   and disassembly. Missing data is a finding, not a pass.
5. **PLM consistency and implementation readiness**, every dataset,
   revision, and source-file reference checked; every requirement
   checkable; every open assumption with closing evidence named.

A synthesizer merges the five stage reports into one ranked report
with a verdict: `NOT READY`, `READY WITH CHANGES`, or `READY`.

## Why fresh contexts matter

An agent that drafted the spec knows what the engineer *meant*. A
reviewer in the same context inherits that knowledge and will read the
spec charitably, the exact failure mode this plugin exists to prevent.
Each Goldfish reviewer is spawned fresh, given only the spec and the
cited CAD files, and told nothing about the drafting conversation. If
your agent platform cannot spawn fresh subagents, `bb-review` stops
and tells you: a review in the same context is not a Goldfish review.

## What a review does not do

- It does not replace measurement, simulation, prototyping, or human
  judgment.
- It does not verify the CAD model itself beyond the numbers the spec
  cites (envelope, part count, feature sizes where measurable). Full
  model verification belongs to CAD/CAE tools.
- It does not approve a design. Only the engineer does.
