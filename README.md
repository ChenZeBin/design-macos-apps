# Design Native macOS Apps

An evidence-backed Codex skill for designing, reviewing, translating, and implementing the user-facing UI and interaction layer of native macOS apps.

It focuses on Mac window and scene structure, commands and menus, keyboard and pointer behavior, SwiftUI/AppKit UI mapping, accessibility, Figma-to-Mac translation, and honest runtime verification of Apple-native fit.

## Install

Codex loads personal skills from `~/.agents/skills`. Clone this repository into that directory:

```bash
mkdir -p "$HOME/.agents/skills"
git clone git@github.com:ChenZeBin/design-macos-apps.git "$HOME/.agents/skills/design-macos-apps"
```

Codex detects skill changes automatically. Restart Codex if the skill does not appear. See the official [Build skills documentation](https://learn.chatgpt.com/docs/build-skills) for skill structure, discovery locations, and invocation behavior.

Invoke it explicitly with `$design-macos-apps`, or let Codex select it when a request matches the scope in `SKILL.md`.

## Repository layout

- `SKILL.md` — routing, evidence boundaries, completion gates, and mode-specific workflow.
- `references/` — focused macOS design, implementation, accessibility, motion, and audit guidance.
- `assets/` — reusable macOS design specification template.
- `scripts/` — deterministic specification validation.
- `evals/` — reproducible deterministic and semantic evaluation cases plus regression tests.
- `agents/openai.yaml` — Codex display metadata and default prompt.

## Validate

```bash
python3 scripts/validate_spec.py --template assets/macos-design-spec-template.md
python3 -m unittest discover -s evals/regressions -p 'test_*.py' -v
skill-up validate evals/eval.yaml
skill-up validate evals/eval-semantic.yaml
```

`skill-up` is only required for the evaluation suites. See `evals/README.md` for the isolated evaluation-home requirement.

## Provenance and distribution

This repository contains an independently written synthesis. It does not bundle Apple HIG prose, third-party skills, research snapshots, login credentials, or historical local evaluation workspaces. Source decisions and pinned upstream revisions are recorded in `references/source-provenance.md`.

No license has been granted in this repository. Obtain permission from the copyright owner before redistribution or modification beyond rights provided by GitHub access.
