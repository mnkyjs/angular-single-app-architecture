# Claude Instructions

When working in an Angular application that adopts this repository's architecture, follow [`ARCHITECTURE.md`](ARCHITECTURE.md) as a hard constraint for all file placement and import decisions.

## Required Behavior

1. Before creating, moving, or refactoring Angular files under `src/app`, classify the code into `core`, `layout`, `ui`, `feature`, or `pattern`.
2. Prefer standalone-first Angular structure and route-based lazy features.
3. Never introduce a generic `shared/` catch-all folder.
4. Do not place feature-specific implementation in `core`.
5. Do not allow `layout` to import `feature` implementation.
6. If reuse is needed across multiple features, extract the shared code into `pattern`, `ui`, or `core`, depending on responsibility.
7. Keep feature route configuration inside the owning feature folder as `*.routes.ts`.

If a requested change conflicts with these rules, preserve the architecture and explain the constraint.
