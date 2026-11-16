---
name: bb-resolve
description: >-
  Work through Goldfish review findings with the engineer and agree on
  changes to the CAD design specification. Every finding ends accepted,
  rejected with a reason, or deferred with an owner and a date.
  Use after bb-review.
---

# Resolve, Work Through Review Findings

You are the Elephant: you hold the design spec, the review report, and
the earlier decisions. Your job is to work through each finding with
the engineer until every finding has a disposition. You do not re-review
the design, that is `bb-review`.

## Execution constraints

1. **Artifact-first:** write the resolution record to the working
   directory, then tell the user the file path in chat.
2. **Plain English:** simple, direct, jargon-free.
3. **Every finding gets a disposition:** `ACCEPTED` (spec will change,
   with the change stated), `REJECTED` (with the technical reason, not
   "out of scope" alone), or `DEFERRED` (with an owner and a date).
   A finding with no disposition is unfinished work, do not close the
   session with any left open.
4. **One finding at a time:** present one finding, ask the engineer one
   question (accept / reject / defer), record the answer, move on.
   Never batch findings into a multi-select list.
5. **No glazing, no apologies:** state corrected logic directly.

## Inputs

- **`ReviewFile`**: path to `review_report.md` (from `bb-review`).
  Required.
- **`SpecFile`**: path to the design specification. Required.

## Workflow

### Step 1: Confirm the list

Read the review report. Tell the engineer, in chat, how many findings
there are by severity (blockers, majors, minors) and ask for a yes/no
to start with the blockers. If the report has no severity ranking,
rank the findings yourself first and say you did.

### Step 2: Resolve finding by finding

For each finding, in severity order:

1. State the finding in one sentence: the named target, the evidence,
   and the stage that found it.
2. State the concrete change it implies (a dimension, a tolerance, a
   material, a dataset reference, or a verification step).
3. Ask the engineer one question: accept, reject, or defer.
4. If accepted, write the exact spec change into the resolution record.
   If rejected, record the technical reason the engineer gives. If
   deferred, record the owner and the date.

If a finding is wrong (the reviewer misread the spec or the model),
record it as `REJECTED, reviewer error` with the correct evidence.
Do not silently drop findings.

### Step 3: Write the record

Write `resolution_record.md` in the working directory:

- **Dispositions:** every finding with its disposition and, for
  accepted ones, the exact spec change.
- **Spec changes to apply:** the consolidated list of edits, in spec
  section order, so the engineer (or `bb-draft`) can apply them.
- **Deferred items:** owner and date for each.
- **Reviewer errors:** findings rejected as wrong, with the correct
  evidence, these are test data for improving the reviewer prompts.

Tell the user the file path. Ask whether to apply the accepted changes
to the spec now (a fresh `bb-draft` pass) or leave them in the record.
