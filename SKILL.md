---
name: angular-single-app-architecture
description: Enforce a strict Angular application folder structure built around src/app core, layout, ui, feature, and pattern areas. Use when creating, moving, or refactoring Angular files under src/app, deciding where components, services, routes, guards, interceptors, pipes, or models belong, or checking that imports follow the intended boundaries.
---

# Angular Single App Architecture

Use this skill to keep an Angular application aligned with a strict standalone-first project structure focused on `src/app`.

## Goal

Keep application code organized around these architecture areas:

- `src/app/core`
- `src/app/layout`
- `src/app/ui`
- `src/app/feature`
- `src/app/pattern`

Treat the architecture as standalone-first. Do not fall back to `SharedModule`-style placement rules.

## Required Workflow

Before generating or editing files:

1. Identify the artifact type and responsibility.
2. Classify it using [references/folder-map.md](references/folder-map.md).
3. Verify whether it belongs to the eager app shell or a lazy feature.
4. Place the file in the narrowest valid folder, not in a catch-all bucket.
5. Check intended imports against [references/dependency-boundaries.md](references/dependency-boundaries.md).
6. Only then scaffold, move, or refactor files.

After changes:

1. Confirm the file still lives in the correct architecture area.
2. Confirm no `shared` catch-all structure or ad hoc top-level folder was introduced.
3. Confirm imports still respect the allowed dependency direction.

## Placement Rules

- `core`: app-wide singleton logic and cross-cutting infrastructure needed from startup.
- `layout`: app shell structure, page chrome, navigation, and layout composition.
- `ui`: generic reusable UI building blocks, directives, pipes, and helper view types.
- `feature/<name>`: route-oriented lazy feature implementation for a specific use case.
- `pattern/<name>`: reusable drop-in business patterns or non-routed data-bound building blocks shared by features.

Use `ui` instead of a generic `shared` folder for reusable presentation pieces.
Use `pattern` instead of `shared feature` for reusable, business-aware drop-in functionality.

## Practical Rules

- Put app-wide `providedIn: 'root'` services, interceptors, guards, tokens, and startup logic in `core`.
- Keep layout components free of direct feature imports.
- Keep generic presentational components in `ui`, not `feature`.
- Keep route configs inside the owning feature folder as `*.routes.ts`.
- Treat lazy features as isolated black boxes. Share logic by extracting it one level up into `pattern`, `ui`, or `core`, depending on responsibility.
- If a feature becomes reusable via sub-routing from multiple features, keep it as a feature and integrate it through routing instead of collapsing it into a generic shared folder.

## Routing Guidance

- Root app routing belongs in app-level files such as `app.routes.ts`.
- Feature routes live in `src/app/feature/<feature-name>/<feature-name>.routes.ts` or equivalent `*.routes.ts` files in that feature folder.
- Prefer lazy feature entrypoints loaded with `loadChildren`.
- Keep feature-local components and services inside the owning feature folder.

## Dependency Discipline

- `core` may depend on itself and external libraries, but not on `layout`, `ui`, `pattern`, or `feature`.
- `ui` may depend on itself and external libraries, but not on `feature`, `pattern`, or `layout`.
- `layout` may depend on `core`, `ui`, and `pattern`, but not on `feature`.
- `pattern` may depend on `core`, `ui`, and other `pattern` code.
- `feature` may depend on `core`, `ui`, and `pattern`.
- `feature` code should not import other feature implementation files directly. Cross-feature reuse should happen through routing, `pattern`, `ui`, or `core`.

## Validation Guidance

- If the repo uses `eslint-plugin-boundaries`, map folders to architecture types using the reference rules in [references/dependency-boundaries.md](references/dependency-boundaries.md).
- If a new folder category is introduced, extend the boundaries configuration instead of bypassing it.
- If testing or tooling files fall outside the architecture types, either define a dedicated type or add a narrow ignore rule.
