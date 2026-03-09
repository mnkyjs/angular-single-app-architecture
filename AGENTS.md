# Agent Instructions

Use [`ARCHITECTURE.md`](ARCHITECTURE.md) as the source of truth when modifying Angular applications that follow this structure.

## Scope

Apply these rules whenever creating, moving, or refactoring Angular files under `src/app`.

## Rules

1. Classify new or moved code into `core`, `layout`, `ui`, `feature`, or `pattern` before writing files.
2. Use a standalone-first structure and lazy route-based features.
3. Do not create a generic `shared/` folder.
4. Keep layout code independent from feature implementation.
5. Keep generic presentational code in `ui`.
6. Keep reusable business-aware drop-in functionality in `pattern`.
7. Keep app-wide startup and singleton logic in `core`.
8. Keep feature routes in the owning feature folder as `*.routes.ts`.
9. Avoid direct imports between feature implementation folders.

When in doubt, choose the narrowest valid folder and preserve one-way dependency flow.
