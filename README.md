# Angular Boilerplate

A GitHub template repository for Angular SPAs. Use it to bootstrap every new frontend project.

## Use cases

Built for:

- admin dashboards
- data-heavy CRUD apps
- MVPs / prototypes
- any SPA needing PrimeNG + Tailwind

Not for: marketing sites, SSR-heavy sites, mobile-first PWAs.

## Stack

- Angular 21 (standalone, signals)
- PrimeNG 21 (Nora-based custom preset) + PrimeIcons
- `@primeuix/themes` (theme engine — see [Design system](#design-system))
- Tailwind CSS v4 (+ `tailwindcss-primeui`)
- TypeScript 5.9
- Vitest
- pnpm

## Quick start

This is a **template repository** — don't clone it directly. Create a new repo from it:

- GitHub UI: click **Use this template** → **Create a new repository**, or
- GitHub CLI:

```bash
gh repo create <new-project-name> --template <owner>/angular-boilerplate --private --clone
cd <new-project-name>
pnpm install
pnpm start
```

Post-clone checklist:

- rename `name` in [package.json](package.json)
- rename the `angular-boilerplate` project key (and its two `buildTarget` refs) in [angular.json](angular.json)
- update `<title>` in [src/index.html](src/index.html)
- update `apiBaseUrl` in [src/environments/environment.ts](src/environments/environment.ts) (dev) and [src/environments/environment.prod.ts](src/environments/environment.prod.ts) (prod)
- update this README title + description
- update brand colors in [src/app/app.preset.ts](src/app/app.preset.ts) and [src/styles.css](src/styles.css)
- replace the sample image at [src/assets/images/](src/assets/images/) and the `<img>` in [src/app/app.html](src/app/app.html)
- update the copyright holder in [LICENSE](LICENSE) if needed

## Scripts

- `pnpm start` — dev server
- `pnpm build` — prod build
- `pnpm watch` — dev build, watch mode
- `pnpm test` — Vitest

## Structure

```
src/
  app/
    core/             # cross-cutting singletons (auth, interceptors, guards, types)
    layout/           # app chrome: main-layout, header, sidebar
    modules/          # feature folders, each with its own <feature>.routes.ts
    shared/ui/        # reusable, feature-agnostic UI components
    app.config.ts     # providers, router, PrimeNG theme
    app.routes.ts     # top-level lazy routes
    app.preset.ts     # PrimeNG theme preset (brand colors)
  environments/        # environment.ts (dev, default) / environment.prod.ts, swapped via angular.json fileReplacements
  assets/images/       # static images, served at /assets/**
  styles.css           # Tailwind, fonts, CSS tokens
.claude/
  rules/               # required reading for contributors + AI agents
  skills/              # project-specific Claude Code skills
AGENTS.md              # source of truth for AI coding agents (Codex, Claude Code, etc.)
CLAUDE.md              # Claude Code entry point — imports AGENTS.md
```

See [.claude/rules/architecture.md](.claude/rules/architecture.md) for the full feature-folder convention.

## Design system

**Tokens** — defined as CSS vars in [src/styles.css](src/styles.css), exposed to Tailwind via `@theme`. Examples: `bg-primary`, `text-heading`, `border-border`.

**Fonts** — Poppins (headings, auto-applied to `h1`–`h6`), Work Sans (body, auto-applied to `body`, `button`, `input`, `textarea`, `select`).

**PrimeNG theme** — custom preset extending Nora, defined in [src/app/app.preset.ts](src/app/app.preset.ts) via `@primeuix/themes` (the current PrimeNG v21 theming package — `@primeng/themes` is the older/deprecated import path, do not use it). Brand colors live here. Keep hex values in sync with [src/styles.css](src/styles.css).

**Layout** — `.main-container` utility in [src/styles.css](src/styles.css) for page-level max-width wrapper.

## Conventions

Required reading before contributing:

- [.claude/rules/angular-standards.md](.claude/rules/angular-standards.md)
- [.claude/rules/architecture.md](.claude/rules/architecture.md)
- [.claude/rules/theming.md](.claude/rules/theming.md)

Highlights:

- standalone components only, no NgModules (standalone is the default in v20+, don't set it explicitly)
- signals for state, `computed()` for derived state
- `ChangeDetectionStrategy.OnPush` on every component
- native control flow (`@if`, `@for`, `@switch`) — no `*ngIf` / `*ngFor`
- `class`/`style` bindings — no `ngClass` / `ngStyle`
- Reactive Forms only
- PrimeNG first, Tailwind second, custom CSS last
- WCAG AA minimum, must pass AXE

## AI-assisted development

This repo is optimized for agentic development (Claude Code, Codex, etc.):

- [AGENTS.md](AGENTS.md) is the single source of truth for AI agents — stack, commands, conventions, and pointers to the rules.
- [CLAUDE.md](CLAUDE.md) imports `AGENTS.md` and adds Claude-specific config (skills).
- `.claude/rules/` contains the enforceable coding standards both humans and agents follow.
- `.claude/settings.json` ships with `bypassPermissions` enabled for autonomous agent runs — review it if you prefer approval prompts.

## Environments

`apiBaseUrl` and flags live in [src/environments/environment.ts](src/environments/environment.ts) (dev, imported by default) and [src/environments/environment.prod.ts](src/environments/environment.prod.ts). Angular swaps them via `fileReplacements` in `angular.json`'s `production` build configuration.

## License

[MIT](LICENSE)
