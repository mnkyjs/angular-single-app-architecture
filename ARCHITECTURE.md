# Angular Single App Architecture

This document describes a strict standalone-first Angular application structure centered on `src/app`.

## Architecture Areas

- `src/app/core`
- `src/app/layout`
- `src/app/ui`
- `src/app/feature`
- `src/app/pattern`

Do not use a generic `shared/` catch-all folder.

## Folder Placement

- `core`: app-wide singleton logic and cross-cutting infrastructure needed from startup.
- `layout`: app shell structure, page chrome, navigation, and layout composition.
- `ui`: generic reusable UI building blocks, directives, pipes, and helper view types.
- `feature/<name>`: route-oriented lazy feature implementation for a specific use case.
- `pattern/<name>`: reusable drop-in business patterns or non-routed data-bound building blocks shared by features.

## Working Rules

1. Identify the artifact type and responsibility before creating or moving files.
2. Decide whether the code belongs to the eager app shell or a lazy feature.
3. Place code in the narrowest valid folder, not in a generic bucket.
4. Keep route configs inside the owning feature folder as `*.routes.ts`.
5. Keep app-wide `providedIn: 'root'` services, interceptors, guards, tokens, and startup logic in `core`.
6. Keep layout components free of direct feature imports.
7. Keep generic presentational components in `ui`, not `feature`.
8. When logic must be shared across features, extract it upward into `pattern`, `ui`, or `core`.

## Dependency Direction

- `core` may depend only on itself and external libraries.
- `ui` may depend only on itself and external libraries.
- `layout` may depend on `core`, `ui`, and `pattern`, but not on `feature`.
- `pattern` may depend on `core`, `ui`, and other `pattern` code.
- `feature` may depend on `core`, `ui`, and `pattern`.
- `feature` implementation files should not import other feature implementation files directly.

## Recommended Tree

```text
src/
  main.ts
  app/
    app.component.ts
    app.config.ts
    app.routes.ts
    core/
      <domain>/
        services/
        guards/
        interceptors/
        tokens/
        models/
        util/
    layout/
      main-layout/
      <alternate-layout>/
    ui/
      components/
      directives/
      pipes/
      models/
      util/
    pattern/
      <pattern-name>/
        components/
        directives/
        pipes/
        services/
        models/
        util/
    feature/
      <feature-name>/
        <feature-name>.routes.ts
        components/
        services/
        models/
        util/
        <sub-feature>/
```

## Validation

If the repository uses `eslint-plugin-boundaries`, configure architecture types for `main`, `app`, `core`, `layout`, `ui`, `pattern`, `feature-routes`, and `feature`, then enforce the dependency direction above.
