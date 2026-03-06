# corti-ds Docs Design

**Date:** 2026-03-06
**Registry:** https://github.com/maxxdwh/corti-ds
**Docs platform:** Mintlify (`docs.json`)

## What We're Building

Lightweight documentation for the corti-ds ShadCN UI Registry — a registry that provides the full shadcn component catalog under the `@corti/*` namespace, plus three Corti theme suites (Console, Assistant, Showcase).

Scope: `@corti/*` component catalog + themes. Custom Corti components (button, stat-card, etc.) have been removed from the registry and are out of scope.

## Site Structure

One docs tab with three sidebar groups:

```
Getting Started
  ├── Introduction         (index.mdx)
  └── Installation         (getting-started/installation.mdx)

Themes
  ├── Overview             (themes/overview.mdx)
  ├── Console              (themes/console.mdx)
  ├── Assistant            (themes/assistant.mdx)
  ├── Showcase             (themes/showcase.mdx)
  └── Theme Switcher       (themes/theme-switcher.mdx)

Components
  └── Reference            (components/reference.mdx)
```

## Page Content

### Introduction (`index.mdx`)
- What corti-ds is: a shadcn registry for Corti projects
- What it provides: full `@corti/*` component catalog + Corti themes
- Brief how-it-works (shadcn registry, install via CLI)
- CTA to Installation

### Installation (`getting-started/installation.mdx`)
- Prerequisite: shadcn already initialized in the project (`components.json` exists)
- Step 1: Add the registry URL to `registries` in `components.json`
  ```json
  {
    "registries": [
      { "name": "corti", "url": "https://corti-ds.vercel.app/r" }
    ]
  }
  ```
- Step 2: Install any component
  ```bash
  npx shadcn@latest add @corti/button
  ```
- Note: installing themes is the same pattern (`@corti/theme-console` etc.)

### Themes Overview (`themes/overview.mdx`)
- Explain the data-attribute system: themes apply by setting `document.documentElement.dataset.theme`
- All 7 available theme values:
  - `corti-console-light` / `corti-console-dark`
  - `corti-assistant-light` / `corti-assistant-dark`
  - `corti-showcase-light` / `corti-showcase-dark`
  - `shadcn-default` (removes theme, restores shadcn base)
- theme-core: provides semantic CSS variables (success, warning, error, info). Install separately: `@corti/theme-core`
- Dark mode: themes set `class="dark"` and `style.colorScheme` automatically

### Console (`themes/console.mdx`)
- Description: monochrome, terminal-inspired
- Install: `npx shadcn@latest add @corti/theme-console`
- Variants: `corti-console-light`, `corti-console-dark`
- Manual activation snippet:
  ```js
  document.documentElement.dataset.theme = "corti-console-light"
  ```

### Assistant (`themes/assistant.mdx`)
- Description: blue-dominant, suited for AI/assistant UIs
- Install: `npx shadcn@latest add @corti/theme-assistant`
- Variants: `corti-assistant-light`, `corti-assistant-dark`

### Showcase (`themes/showcase.mdx`)
- Description: playful 90s/8-bit aesthetic, IBM Plex Mono typography, square edges
- Install: `npx shadcn@latest add @corti/theme-showcase`
- Variants: `corti-showcase-light`, `corti-showcase-dark`

### Theme Switcher (`themes/theme-switcher.mdx`)
- Install: `npx shadcn@latest add @corti/theme-switcher`
- What it does: dropdown UI component, persists selection to localStorage, applies `data-theme` + dark class
- Includes "Shadcn Default" option to clear theme overrides
- Usage: drop `<CortiThemeSwitcher />` anywhere in the app

### Components Reference (`components/reference.mdx`)
- Intro: corti-ds mirrors the full shadcn catalog under `@corti/*` — install any component via CLI
- Table with two columns: Component, Install command
- All ~60 components listed (accordion, alert, avatar, badge, button, calendar, card, carousel, checkbox, collapsible, command, context-menu, dialog, drawer, dropdown-menu, form, hover-card, input, input-otp, kbd, label, menubar, navigation-menu, pagination, popover, progress, radio-group, resizable, scroll-area, select, separator, sheet, sidebar, skeleton, slider, sonner, switch, table, tabs, textarea, toast, toggle, toggle-group, tooltip, etc.)

## docs.json Changes

- Update `name`, `colors`, `logo`, `favicon`, `navbar`, `footer`
- Replace current navigation groups with the three new groups
- Remove API Reference tab (not needed)
- Remove "Mint Starter Kit" example pages

## Files to Create/Modify

| Action   | File |
|----------|------|
| Modify   | `docs.json` |
| Rewrite  | `index.mdx` |
| Create   | `getting-started/installation.mdx` |
| Create   | `themes/overview.mdx` |
| Create   | `themes/console.mdx` |
| Create   | `themes/assistant.mdx` |
| Create   | `themes/showcase.mdx` |
| Create   | `themes/theme-switcher.mdx` |
| Create   | `components/reference.mdx` |
| Delete   | `quickstart.mdx`, `development.mdx`, `essentials/`, `api-reference/`, `ai-tools/` |

## Registry URL

The hosted registry URL is `https://corti-ds.vercel.app/r` — verify this against the live deployment before publishing docs.
