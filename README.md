# Blueprint & Blindspot

**Design with context. Review with fresh eyes.**

An open-source plugin for AI coding assistants that brings the
design-review discipline to CAD and PLM work. One agent holds your
design intent, requirements, and Teamcenter context and drafts the
specification. Independent reviewers examine the draft and the live CAD
model **without the earlier conversation**, exposing unstated
assumptions and blind spots. **You** make the engineering trade-offs
and approve the specification before anything is built.

No training, no model weights, no server, no API keys, no file uploads.
The plugin is prompts and manifests only — skills your coding agent
runs, in the tools you already use.

> Repo: `BRCoderAI/blueprint-and-blindspot`. License is Apache 2.0.

## The problem it solves

A CAD design decision made in conversation with an AI assistant is
never challenged by that same assistant: it remembers everything you
said, agrees with the direction, and fills gaps from memory. The
result is a specification that looks complete and is not — a wall
thickness below the process minimum, a clearance hole that does not
clear, a cost figure computed for a different process, a dataset
revision that does not exist.

This plugin fixes that with context isolation: the reviewers start
fresh. They read only the specification and the CAD files it cites. If
the spec does not justify a decision on its own, that is a finding.

## How it works

| Role | Context | Responsibility |
| --- | --- | --- |
| **Elephant** | Your design intent, requirements, and earlier decisions | Explore the problem and draft the specification. |
| **Goldfish** | The specification and the cited CAD files, without the earlier conversation | Find missing assumptions, unclear requirements, DFM failures, cost contradictions, sustainability gaps, and PLM mismatches. |
| **You** | The goals and constraints that matter | Resolve trade-offs, approve the design, and decide what to build. |

Goldfish reviews require fresh subagent contexts. If your agent cannot
create them, the plugin stops the review — a review in the drafting
context is not a Goldfish review. A review does not replace
measurement, simulation, or human judgment.

## Install

Choose your coding agent. Install the complete plugin so its skills can
read the reviewer prompts.

### Claude Code

```
claude plugin marketplace add BRCoderAI/blueprint-and-blindspot
claude plugin install blueprint-blindspot@blueprint-blindspot
```

### Codex CLI

```
codex plugin marketplace add BRCoderAI/blueprint-and-blindspot
codex plugin add blueprint-blindspot@blueprint-blindspot
```

### Gemini CLI

Install the extension from the repo (see `docs/install.md`). The
Gemini extension manifest is included; a live install test on Gemini
is still outstanding — see TESTING.md.

### Cursor

See `docs/install.md`. The Cursor manifest is included; a live install
test on Cursor is still outstanding — see TESTING.md.

## Try a 60-second review on an existing spec

Review an existing design specification against the live CAD model. You
do not need to write a new specification first.

```
/bb-review docs/designs/servo-bracket.md
```

Fresh reviewers check the spec, its clarity, its fit with the CAD
model, and its implementation plan. The DFM reviewer checks every
feature against the stated process; the cost reviewer checks the cost
story for contradictions; the sustainability reviewer checks material
and end-of-life claims; the PLM reviewer checks every dataset,
revision, and source-file reference.

## Try your first design

Open your project in your coding agent and pick a part that needs
design decisions — a bracket, a housing, an enclosure.

```
/bb-brainstorm Add a mounting bracket for this servo.
/bb-draft
/bb-review design_draft.md
```

Discuss requirements and trade-offs with the agent. Fresh reviewers
challenge the proposal, and the agent saves the agreed direction.
When you approve the design, ask your coding agent to implement it.

See `docs/how-it-works.md` for the full process.

## Choose a skill

You can use each skill when you need it. You do not have to follow the
full sequence.

| Skill | Use it to… |
| --- | --- |
| `bb-brainstorm` | Test a CAD idea and write a concept brief. |
| `bb-draft` | Turn a brief into a design specification, one section at a time. |
| `bb-review` | Review a spec with fresh reviewers across five stages. |
| `bb-resolve` | Work through review findings and agree on changes. |
| `bb-drift-report` | Compare checked-in design docs against the current CAD/PLM state. |

## The reviewers

| Reviewer | Checks |
| --- | --- |
| Comprehension | Can a stranger build the part from this document alone? |
| DFM / manufacturing | Every feature against the stated process limits; every cited model number against the CAD file. |
| Cost | Cost story consistency; process and material in the cost section must match the rest of the spec. |
| Sustainability | Material data, recycled content, end-of-life and disassembly. Missing data is a finding, not a pass. |
| PLM / Teamcenter | Every dataset, revision, and source-file reference against the cited files. |

See `docs/reviewers.md` for what each reviewer checks and what a
finding looks like.

## Learn more

- `docs/how-it-works.md`: the workflow and the Elephant/Goldfish roles.
- `docs/install.md`: installation per platform and known limits.
- `docs/reviewers.md`: the five reviewers and their checklists.
- `TESTING.md`: checks, execution records, and verification limits.

## Contribute

See `CONTRIBUTING.md` for PRs and issues. Reviewer prompts are the
product: a contribution that makes a reviewer catch a real defect, with
a test fixture that proves it, is the most valuable kind.

## License

[Apache 2.0](LICENSE). This is not an officially supported product of
any CAD or PLM vendor.
