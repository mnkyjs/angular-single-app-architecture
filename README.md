# Angular Single App Architecture

Cross-agent Angular architecture guidance for a strict standalone-first `src/app` folder structure.

This repository packages the same architecture rules in formats that can be consumed by different coding agents. The goal is to keep Angular applications organized around clear application areas and one-way dependency boundaries instead of drifting into a generic `shared/` structure.

## Architecture Model

The application is organized around these top-level areas under `src/app`:

- `core`
- `layout`
- `ui`
- `feature`
- `pattern`

At a high level:

- `core` contains app-wide singleton and startup logic.
- `layout` contains shell and page composition.
- `ui` contains generic reusable presentation building blocks.
- `feature` contains route-oriented lazy feature code.
- `pattern` contains reusable business-aware drop-in functionality shared across features.

## Repository Structure

```text
.
├── SKILL.md
├── agents/openai.yaml
├── references/
├── ARCHITECTURE.md
├── AGENTS.md
└── CLAUDE.md
```

## Agent Compatibility

- `SKILL.md`, `agents/openai.yaml`, `references/`
  Root-level packaged skill for Codex and `skills.sh`-style installers.
- `ARCHITECTURE.md`
  Neutral source of truth for the architecture rules.
- `AGENTS.md`
  Generic agent instructions for tools that support repo-level agent guidance.
- `CLAUDE.md`
  Claude-oriented instruction wrapper around the same rules.

## How To Use

### Codex

Install this GitHub repository as a skill:

```bash
npx skills add https://github.com/mnkyjs/angular-single-app-architecture
```

The repository root is the skill root and contains:

- `SKILL.md`
- `agents/openai.yaml`
- `references/`

Codex uses these files to apply the architecture rules when creating, moving, or refactoring Angular files.

### Claude and Other Agents

Use the repository root files:

- `ARCHITECTURE.md` as the neutral architecture reference
- `CLAUDE.md` for Claude-style repo instructions
- `AGENTS.md` for generic repo-level agent instructions

## What The Rules Enforce

- No generic `shared/` catch-all folder
- Standalone-first Angular structure
- Route-based lazy feature organization
- Layout code must not depend on feature implementation
- Feature reuse should be extracted into `pattern`, `ui`, or `core`
- One-way dependency boundaries between architecture areas

## Example Uses

- "Create a new document-upload feature and place all files in the correct architecture folders."
- "Refactor this Angular app to move misplaced components and services into core, ui, feature, and pattern."
- "Review my src/app structure and point out architecture and import-boundary violations."

## Repository Purpose

This repository is intended to make the same Angular architecture guidance reusable across multiple agent environments instead of rewriting the rules for each tool.
