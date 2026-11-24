# Public repository work plan

Reviewed: 24 November 2026. This is a working plan; task completion is recorded in the relevant pull request.

## Goal

Make the public projects easy to understand, try, verify and reuse. Each repository keeps its own purpose: a desktop product, a reusable design skill, a small research tool, a profile and a research website.

## Working together

| Role | Responsibility | Handoff |
| --- | --- | --- |
| Ray | Product and research direction; priorities and editorial decisions | Decisions attached to the relevant task or pull request |
| ChatGPT | Cross-repository review, documentation, task definition and review of evidence | A scoped change or task with file paths and acceptance criteria |
| Codex | Implementation, local reproduction, runtime checks and repair | A diff or pull request, commands actually run, results and remaining blockers |

Use the repository as the shared record. Before starting a task, read its current instructions, fetch the current branch and check open pull requests for overlapping work. Each change should solve one concrete problem. Record the commit tested and distinguish local checks, existing CI records and checks that have not run.

A task in this document is a handoff specification, not a claim that a separate Codex session has started it.

## Repository map

| Repository | Public purpose | Current evidence | Next focus |
| --- | --- | --- | --- |
| [raylee-ai](https://github.com/raylee-ai/raylee-ai) | Profile and navigation | Introduces the three projects and links to the research site | Accurate project names and useful entry points |
| [lancer](https://github.com/raylee-ai/lancer) | Desktop AI workspace built on pi-gui and pi | Public source Alpha, existing CI, extension examples and Light UI | Review existing PRs; align installation and release documentation |
| [ai-native-ui-skill](https://github.com/raylee-ai/ai-native-ui-skill) | ANUI, one Codex-first UI design skill | Bilingual references, interactive demo and automated checks | Make the isolated Skill installation and its validation instructions agree |
| [bibliographic-metadata-audit](https://github.com/raylee-ai/bibliographic-metadata-audit) | Offline comparison of citation pairs before and after conversion | Standard-library Python CLI, four-pair fixtures and existing unit tests | Reproducible continuous checks and example provenance |
| [raylee-ai.github.io](https://github.com/raylee-ai/raylee-ai.github.io) | Research notes and methods | English homepage and methods note; Chinese reading note and about page | Keep the repository guide aligned with published pages |

## First tasks

### BMA-01 — Run the existing citation audit checks in CI

Owner: ChatGPT initial implementation; Codex review. Status: [draft PR #1](https://github.com/raylee-ai/bibliographic-metadata-audit/pull/1) prepared.

Scope: a small workflow in `bibliographic-metadata-audit/.github/workflows/`. Keep the existing algorithm and input formats.

Acceptance:

- Run on pull requests and pushes to the default branch with read-only repository permissions.
- A clean checkout needs no third-party Python packages.
- Run `python -m unittest -v`.
- Verify the README examples: preserved has 4 before / 4 after / 0 lost / 0 added and exit code 0; filtered has 4 before / 2 after / 2 lost / 0 added and exit code 1.
- Treat the filtered example's expected exit code 1 as a successful demonstration, not a broken build.
- Record the Python versions and exact commit checked.

### BMA-02 — Explain the four-pair example

Owner: ChatGPT draft; Codex reproduction. Status: a reproduction guide is included in [draft PR #1](https://github.com/raylee-ai/bibliographic-metadata-audit/pull/1); review the fixture explanation with the implementation.

Scope: `docs/REPRODUCING.md` and a short link from the root README.

Explain which fields come from the linked OpenAlex records, which references were selected for the fixture, how the filtered and preserved CSV files were constructed, and how to reproduce their reports.

Acceptance: a reader can reconstruct the four-pair example from the public materials. Describe larger historical audit numbers as historical findings unless their complete reproduction materials are published. Use only documented collection dates. Keep bibliographic identity decisions separate from citation-pair comparison.

### ANUI-01 — Complete the isolated Skill installation path

Owner: Codex implementation; ChatGPT documentation review. Status: queued.

Scope: the root README, `skills/anui/README.md` and corresponding Chinese instructions.

Acceptance:

- Installing only `skills/anui` into a clean temporary location provides the Skill entry, references and applicable notices.
- Links inside the installed directory resolve without depending on absent parent files.
- Distinguish using the installed Skill from developing and testing the demo in a full repository checkout.
- State the dependencies needed for demo checks and use commands that work from the documented location.
- Keep English and Chinese instructions consistent.

### ANUI-02 — Make incomplete checks fail clearly

Owner: Codex implementation; ChatGPT review. Status: queued.

Scope: `skills/anui/scripts/check.mjs` and narrowly targeted regression checks.

Acceptance:

- A required contrast check cannot be skipped because Python is missing while the run still reports all checks passed.
- Missing required run/toast controls produce a visible failure instead of a swallowed click error.
- The existing theme, language, rendering and external-request checks continue to pass.
- Report the browser/runtime versions used.

Follow-up: add pull-request checking to `.github/workflows/pages.yml`, keep Pages deployment on the default branch, and make lockfile failures explicit.

### LANCER-01 — Review existing pull requests before expanding the queue

Owner: ChatGPT review; Codex reproduction. Status: queued.

Start with [#24](https://github.com/raylee-ai/lancer/pull/24) and [#25](https://github.com/raylee-ai/lancer/pull/25), which address related tool-confirmation layout work. Then review [#3](https://github.com/raylee-ai/lancer/pull/3), [#4](https://github.com/raylee-ai/lancer/pull/4), [#6](https://github.com/raylee-ai/lancer/pull/6), [#14](https://github.com/raylee-ai/lancer/pull/14), [#16](https://github.com/raylee-ai/lancer/pull/16) and [#17](https://github.com/raylee-ai/lancer/pull/17).

Acceptance: for each current PR head, record the change, overlap with main or another PR, checks available, runtime evidence still needed and a concrete next action. An existing green run only supports its tested commit. Preserve the repository's own branch and Electron-verification instructions.

### LANCER-02 — Align contributor and release documentation

Owner: Codex implementation; ChatGPT editorial review. Status: queued.

Scope: `CONTRIBUTING.md`, `CHANGELOG.md`, `SECURITY.md`, `docs/release-readiness.md` and the extension example guide.

Acceptance:

- Installation commands agree with the root README and `packageManager`.
- Distinguish the published source Alpha, later development-branch features and any future application installers.
- Replace stale repository placeholders with verified links.
- Check extension tarball names against actual pack output.
- Preserve upstream attribution.
- Verify a security-reporting route before documenting it as available.

### PROFILE-01 — Keep navigation accurate

Owner: ChatGPT. Status: prepared in this pull request.

Changes: identify ANUI as the single current Skill; link its interactive demo; describe citation loss and additions accurately; label the research site as English / Chinese; link this work plan.

Acceptance: existing project links and visual assets remain valid, each description agrees with public project evidence, and no capability is described as tested without evidence.

### SITE-01 — Update the repository's page inventory

Owner: Codex or ChatGPT. Status: queued.

Scope: `raylee-ai.github.io/README.md`.

Acceptance: list the current homepage, about page, Ghazali note, citation-audit methods note, stylesheet and favicon; accurately describe the mixed-language content and the repository's existing publication workflow.

## Evidence for the first review

The snapshots below are review references, not versions that future work must stay on. Refresh main and open PR state before implementation.

| Repository | Reviewed commit | Useful evidence |
| --- | --- | --- |
| raylee-ai | `83d4d252c4eaee6c6a2724d9cec6532cdf2f1e9f` | [README](https://github.com/raylee-ai/raylee-ai/blob/83d4d252c4eaee6c6a2724d9cec6532cdf2f1e9f/README.md) |
| lancer | `0ccc4584fc0753fa128e71464814d1ed09dd1dbc` | [README](https://github.com/raylee-ai/lancer/blob/0ccc4584fc0753fa128e71464814d1ed09dd1dbc/README.md), [existing successful CI](https://github.com/raylee-ai/lancer/actions/runs/44035877210), [source Alpha](https://github.com/raylee-ai/lancer/releases/tag/v1.0.1) |
| ai-native-ui-skill | `ae53614421814655a9ef2cfdb5372354badfb9d8` | [README](https://github.com/raylee-ai/ai-native-ui-skill/blob/ae53614421814655a9ef2cfdb5372354badfb9d8/README.md), [existing successful CI](https://github.com/raylee-ai/ai-native-ui-skill/actions/runs/45140852309) |
| bibliographic-metadata-audit | `3d01455322887880e1469f8a0419542396925906` | [README](https://github.com/raylee-ai/bibliographic-metadata-audit/blob/3d01455322887880e1469f8a0419542396925906/README.md), [existing tests](https://github.com/raylee-ai/bibliographic-metadata-audit/blob/3d01455322887880e1469f8a0419542396925906/test_reference_audit.py) |
| raylee-ai.github.io | `487334ef36f8c7f1043ccd8e81284cca4605365a` | [homepage](https://github.com/raylee-ai/raylee-ai.github.io/blob/487334ef36f8c7f1043ccd8e81284cca4605365a/index.html), [methods note](https://github.com/raylee-ai/raylee-ai.github.io/blob/487334ef36f8c7f1043ccd8e81284cca4605365a/citation-audit.html) |

## Later decisions

After the first tasks, consider a versioned ANUI release, clearer Lancer Light UI entry points, and licensing/citation metadata for the bibliographic tool. Check the intended license scope and actual authorship before adding a license or citation record. Further projects should follow a demonstrated need rather than a target repository count.
