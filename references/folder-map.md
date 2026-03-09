# Folder Map

Use this map as the source of truth for folder placement in a single Angular app that follows this strict standalone-first architecture.

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

## Quick Placement Decisions

- Needed from application startup across multiple areas? -> `core`
- Defines shell, navigation, or page chrome? -> `layout`
- Generic reusable UI with no feature-specific orchestration? -> `ui`
- Route-oriented use case owned by one lazy feature? -> `feature/<feature-name>`
- Reusable business-aware drop-in functionality shared by features? -> `pattern/<pattern-name>`

## Notes

- Do not create a generic `shared/` catch-all folder.
- Do not place reusable business-aware components in `ui`; they belong in `pattern`.
- Do not place feature-specific implementation in `core`.
- Prefer further grouping inside `core` by domain instead of large flat folders.
- Keep feature routes near their feature code.
