# Contributing

## What this project is

A plugin of prompt-skills and manifests for AI coding assistants. There
is no application code: the product is the reviewer prompts, the
workflow, and the tests that prove the reviewers catch real defects.

## The most valuable contributions

1. **A reviewer prompt improvement with a test fixture.** Show a real
   design defect the current reviewers miss, add a fixture spec that
   contains it, and show the improved reviewer catching it concretely
   (named feature, dimension, or dataset).
2. **A new reviewer.** Same bar: persona file, checklist, and a fixture
   that proves it catches something the existing five do not.
3. **A platform manifest.** A verified install on a new agent platform,
   with the install steps documented in `docs/install.md`.

## Rules

- **Concrete findings only.** A reviewer finding must name a feature,
  dimension, tolerance, material, or dataset. Generic advice is not a
  finding and will not be merged.
- **Every reviewer change needs a test.** See `TESTING.md`. A prompt
  change with no fixture run is a guess.
- **Plain English.** Simple, direct, jargon-free. No promotional
  adjectives.
- **No model training, no servers, no API keys.** Prompts and manifests
  only. A contribution that needs a backend does not fit this project.
- **No AI credit.** Do not credit any AI assistant in code, docs, or
  commit messages.

## How to contribute

1. Open an issue describing the defect, reviewer gap, or platform.
2. Fork the repo, make the change, run the tests in `TESTING.md`.
3. Open a pull request with the fixture and the before/after review
   output.

## License

Contributions are under the Apache License 2.0, the same as the project.
