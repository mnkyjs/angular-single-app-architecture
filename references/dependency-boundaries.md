# Dependency Boundaries

These rules summarize the intended dependency direction and a matching `eslint-plugin-boundaries` setup for enforcing it.

## Architecture Types

- `main`: `src/main.ts`
- `app`: app bootstrap and root composition files such as `app.component.ts`, `app.config.ts`, `app.routes.ts`
- `core`: `src/app/core/**`
- `layout`: `src/app/layout/**`
- `ui`: `src/app/ui/**`
- `pattern`: `src/app/pattern/**`
- `feature-routes`: `src/app/feature/*/*.routes.ts`
- `feature`: `src/app/feature/**`

## Allowed Imports

- `main` -> `app`
- `app` -> `app`, `core`, `layout`, `feature-routes`
- `core` -> `core`
- `ui` -> `ui`
- `layout` -> `core`, `ui`, `pattern`
- `pattern` -> `core`, `ui`, `pattern`
- `feature` -> `core`, `ui`, `pattern`
- `feature-routes` -> `core`, `pattern`, same-feature `feature`, other-feature `feature-routes`

## Enforcement Notes

- Every validated TypeScript file should belong to a known architecture type when using `plugin:boundaries/strict`.
- Additional file groups such as testing config or generated environments need either a dedicated type or a narrow `boundaries/ignore` entry.
- `layout` importing `feature` is a violation and should be treated as an architecture break.
- Cross-feature implementation imports are a smell. Prefer extracting shared logic upward into `pattern`, `ui`, or `core`, or share a feature through routing.

## Minimal Boundaries Elements Sketch

```json
[
  { "type": "main", "mode": "file", "pattern": "main.ts", "basePattern": "projects/**/src" },
  { "type": "app", "mode": "file", "pattern": "app(.*)*.ts", "basePattern": "projects/**/src/app" },
  { "type": "core", "pattern": "core", "basePattern": "projects/**/src/app" },
  { "type": "ui", "pattern": "ui", "basePattern": "projects/**/src/app" },
  { "type": "layout", "pattern": "layout", "basePattern": "projects/**/src/app" },
  { "type": "pattern", "pattern": "pattern", "basePattern": "projects/**/src/app" },
  { "type": "feature-routes", "mode": "file", "pattern": "feature/*/*.routes.ts", "basePattern": "projects/**/src/app" },
  { "type": "feature", "pattern": "feature/**", "basePattern": "projects/**/src/app" }
]
```

Adapt the exact glob patterns to the workspace layout, but preserve the dependency direction.
