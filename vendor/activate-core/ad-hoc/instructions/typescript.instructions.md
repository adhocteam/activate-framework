---
description: 'TypeScript conventions and project-specific patterns'
applyTo: '**/*.{ts,tsx}'
excludeAgent: []
---
# TypeScript Instructions

Project-specific TypeScript guidance. Only include what Copilot cannot infer from public documentation.

> **Note:** Do not restate TypeScript handbook basics or common patterns. Focus on your team's specific choices and constraints.

## Version and Runtime

<!-- CUSTOMIZE: Specify your TypeScript/Node versions and runtime -->

- **TypeScript version**: <!-- e.g., 5.3+ -->
- **Node version**: <!-- e.g., 20 LTS -->
- **Runtime**: <!-- e.g., Node.js, Bun, Deno -->
- **Package manager**: <!-- e.g., pnpm, npm, yarn -->

## Tooling

<!-- CUSTOMIZE: List your specific tools and how to run them -->

| Tool | Command | Purpose |
|------|---------|---------|
| Type check | <!-- e.g., `tsc --noEmit` --> | <!-- e.g., Static type analysis --> |
| Linter | <!-- e.g., `eslint .` --> | <!-- e.g., Style and error checking --> |
| Formatter | <!-- e.g., `prettier --write .` --> | <!-- e.g., Code formatting --> |
| Tests | <!-- e.g., `vitest` --> | <!-- e.g., Run test suite --> |

## Project Structure

<!-- CUSTOMIZE: Document your specific directory layout -->

```text
<!-- e.g.,
src/
├── components/    # React components
├── hooks/         # Custom React hooks
├── lib/           # Utility functions
├── services/      # API clients and business logic
└── types/         # Shared type definitions
-->
```

## Internal Libraries

<!-- CUSTOMIZE: List internal packages and their intended usage -->

<!-- e.g.,
- `@adhoc/ui`: Design system components; do not create custom buttons, inputs, etc.
- `@adhoc/api-client`: Generated API client; do not write fetch calls directly
-->

## Team Conventions

<!-- CUSTOMIZE: Document decisions where multiple valid approaches exist -->

### Preferred Patterns

<!-- e.g.,
- Use named exports over default exports
- Use `type` for type aliases, `interface` for object shapes that may be extended
- Prefer `async/await` over `.then()` chains
- Use `zod` for runtime validation, not manual type guards
-->

### Patterns to Avoid

<!-- e.g.,
- Do not use `any`; use `unknown` and narrow with type guards
- Do not use `enum`; use `as const` objects or union types
- Avoid `!` non-null assertion; prefer explicit checks or optional chaining
-->

## React Conventions

<!-- CUSTOMIZE: If using React, document your patterns (remove if not applicable) -->

<!-- e.g.,
- Use functional components only; no class components
- Prefix custom hooks with `use` (enforced by eslint-plugin-react-hooks)
- Co-locate component, styles, and tests in the same directory
- Use React Server Components for data fetching where possible
-->

## Type Definitions

<!-- CUSTOMIZE: Specify your type definition expectations -->

<!-- e.g.,
- Export types from `types/` barrel file
- Use `readonly` for immutable data structures
- Prefer strict generic constraints over loose ones
-->

## Testing Conventions

<!-- CUSTOMIZE: Document your testing patterns -->

<!-- e.g.,
- Use Vitest for unit tests; Playwright for E2E
- Name test files `*.test.ts` or `*.spec.ts`
- Use `@testing-library/react` for component tests; avoid testing implementation details
-->

## Import Organization

<!-- CUSTOMIZE: Specify import order if enforced -->

<!-- e.g.,
1. Node built-ins (`node:fs`, `node:path`)
2. External packages (`react`, `zod`)
3. Internal packages (`@adhoc/*`)
4. Relative imports (`./`, `../`)

Enforced by `eslint-plugin-import` with auto-fix.
-->
