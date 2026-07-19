# Frontend Boilerplate

Internal Angular frontend template. Clone at the start of every new frontend project.

## Use cases

Built for:

- internal admin dashboards
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

## Quick start

```bash
git clone https://github.com/Geoplan-Philippines/frontend-boilerplate <new-project-name>
cd <new-project-name>
rm -rf .git && git init
npm install
npm start
```

Post-clone checklist:

- rename `name` in [package.json](package.json)
- update `apiBaseUrl` in [src/environments/environment.ts](src/environments/environment.ts) (dev) and [src/environments/environment.prod.ts](src/environments/environment.prod.ts) (prod)
- update this README title + description
- update brand colors in [src/app/app.preset.ts](src/app/app.preset.ts) and [src/styles.css](src/styles.css)
- replace the sample image at [src/assets/images/](src/assets/images/) and the `<img>` in [src/app/app.html](src/app/app.html)

## Scripts

- `npm start` — dev server
- `npm run build` — prod build
- `npm run watch` — dev build, watch mode
- `npm test` — Vitest

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
  assets/images/        # static images, served at /assets/**
  styles.css            # Tailwind, fonts, CSS tokens
.claude/
  rules/                # required reading for contributors + Claude Code
  skills/               # project-specific Claude Code skills
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

## Environments

`apiBaseUrl` and flags live in [src/environments/environment.ts](src/environments/environment.ts) (dev, imported by default) and [src/environments/environment.prod.ts](src/environments/environment.prod.ts). Angular swaps them via `fileReplacements` in `angular.json`'s `production` build configuration.

## License

Internal — Geoplan. Not for distribution.
