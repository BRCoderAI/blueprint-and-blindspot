# Install

Choose your coding agent. Install the complete plugin so its skills can
read the reviewer prompts and document standards. Start a new session
after installation.

## Claude Code

```
claude plugin marketplace add BRCoderAI/blueprint-and-blindspot
claude plugin install blueprint-blindspot@blueprint-blindspot
```

Manifests: `.claude-plugin/plugin.json` and
`.claude-plugin/marketplace.json`. The reviewer personas are registered
in `.claude-plugin/agents/`.

## Codex CLI

```
codex plugin marketplace add BRCoderAI/blueprint-and-blindspot
codex plugin add blueprint-blindspot@blueprint-blindspot
```

Manifest: `.codex-plugin/plugin.json`. Reviews require a local executor
and isolated subagents; cloud support remains partial.

## Gemini CLI

The Gemini extension manifest is `.gemini/gemini-extension.json`.
Install the extension from the repo following the Gemini CLI extension
instructions. **A live install test on Gemini is still outstanding**
(see TESTING.md) — the manifest is included in the EGM shape, but no
review has been run through a Gemini install yet.

## Cursor

Manifest: `.cursor-plugin/plugin.json`. Install following the Cursor
plugin instructions. **A live install test on Cursor is still
outstanding** (see TESTING.md).

## Known limits

- Goldfish reviews require fresh subagent contexts. If your agent
  cannot create them, `bb-review` stops the review and says so.
- The plugin reads CAD files only through the agent's own tools. It
  does not parse STEP/IGES itself; the DFM and PLM reviewers check the
  numbers the spec cites against measurements the agent makes with
  whatever CAD tooling is available in the session (for example, an
  OCCT-based reader).
- The public repo is `BRCoderAI/blueprint-and-blindspot` (renamed from
  the `cad-review` working name on 2026-11-15); the manifests and
  install commands already point at it.
