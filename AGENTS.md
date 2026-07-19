# AGENTS.md

Guidance for AI coding agents (Claude Code, Codex, etc.) working in this repository.

## Project

Angular boilerplate / GitHub template repository for SPAs: admin dashboards, data-heavy CRUD apps, MVPs.

Stack: Angular 21 (standalone, signals, zoneless), PrimeNG 21 + `@primeuix/themes`, Tailwind CSS v4, TypeScript 5.9 (strict), Vitest. Package manager: **pnpm**.

## Commands

- `pnpm install` — install dependencies
- `pnpm start` — dev server
- `pnpm build` — production build
- `pnpm test` — run tests (Vitest)

Always verify changes with `pnpm build` (and `pnpm test` when touching tested code) before considering work done.

## Required rules — read before making changes

- [.claude/rules/angular-standards.md](.claude/rules/angular-standards.md) — TypeScript/Angular/component/a11y standards
- [.claude/rules/architecture.md](.claude/rules/architecture.md) — feature-folder architecture, routing, naming
- [.claude/rules/theming.md](.claude/rules/theming.md) — colors, typography, PrimeNG theming

## Key conventions (summary)

- Standalone components only; do NOT set `standalone: true`
- Signals for state, `computed()` for derived state, `input()`/`output()` functions
- `ChangeDetectionStrategy.OnPush` on every component
- Native control flow (`@if`, `@for`, `@switch`) — no `*ngIf` / `*ngFor`
- `class`/`style` bindings — no `ngClass` / `ngStyle`
- Reactive Forms only; `inject()` over constructor injection
- Feature folders under `src/app/modules/<feature>/` with their own `<feature>.routes.ts`, lazy-loaded
- File naming: `<name>.ts|html|css|spec.ts` (no `.component` suffix)
- Theme tokens only (`bg-primary`, `text-heading`, `border-border`, ...) — never hardcode hex in components
- PrimeNG first, Tailwind second, custom CSS last
- WCAG AA minimum

## Environment config

`src/environments/environment.ts` (dev) / `environment.prod.ts` (prod), swapped via `fileReplacements` in `angular.json`.
