# corti-ds Docs Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build lightweight Mintlify documentation for the corti-ds ShadCN registry, covering installation, the three theme suites, and a full `@corti/*` component reference.

**Architecture:** Replace the Mintlify starter kit content with corti-ds docs. Three sidebar groups: Getting Started, Themes, Components. One components reference page listing all `@corti/*` components — no individual component pages since they're standard shadcn components.

**Tech Stack:** Mintlify (MDX), docs.json for navigation config.

**Registry URL:** The hosted registry URL is a placeholder (`<REGISTRY_URL>`) — fill in before publishing. Likely the Vercel deployment URL + `/r`.

---

### Task 1: Update docs.json

**Files:**
- Modify: `docs.json`

**Step 1: Replace docs.json with corti-ds config**

Replace the entire file contents with:

```json
{
  "$schema": "https://mintlify.com/docs.json",
  "theme": "willow",
  "name": "corti-ds",
  "colors": {
    "primary": "#0F172A",
    "light": "#64748B",
    "dark": "#0F172A"
  },
  "favicon": "/favicon.svg",
  "navigation": {
    "tabs": [
      {
        "tab": "Docs",
        "groups": [
          {
            "group": "Getting Started",
            "pages": [
              "index",
              "getting-started/installation"
            ]
          },
          {
            "group": "Themes",
            "pages": [
              "themes/overview",
              "themes/console",
              "themes/assistant",
              "themes/showcase",
              "themes/theme-switcher"
            ]
          },
          {
            "group": "Components",
            "pages": [
              "components/reference"
            ]
          }
        ]
      }
    ],
    "global": {
      "anchors": [
        {
          "anchor": "GitHub",
          "href": "https://github.com/maxxdwh/corti-ds",
          "icon": "github"
        }
      ]
    }
  },
  "logo": {
    "light": "/logo/light.svg",
    "dark": "/logo/dark.svg"
  },
  "navbar": {
    "links": [
      {
        "label": "GitHub",
        "href": "https://github.com/maxxdwh/corti-ds"
      }
    ]
  },
  "footer": {
    "socials": {
      "github": "https://github.com/maxxdwh/corti-ds"
    }
  }
}
```

**Step 2: Commit**

```bash
git add docs.json
git commit -m "chore: configure docs.json for corti-ds"
```

---

### Task 2: Rewrite Introduction (index.mdx)

**Files:**
- Modify: `index.mdx`

**Step 1: Replace index.mdx with corti-ds introduction**

```mdx
---
title: Introduction
description: A ShadCN registry for Corti applications.
---

corti-ds is a [shadcn registry](https://ui.shadcn.com/docs/registry) that provides the full shadcn component catalog under the `@corti/*` namespace, together with a set of Corti themes.

Rather than copying component source files directly into your project from shadcn, you install them through this registry. Components land in your codebase the same way, but they come pre-wired to Corti's design tokens and theme system.

## What's included

**`@corti/*` components** — every component from the standard shadcn catalog, installable via the CLI.

**Themes** — three Corti theme suites (Console, Assistant, Showcase) plus shared semantic color tokens. Themes work by setting a `data-theme` attribute on `<html>` and are fully compatible with shadcn's dark mode approach.

## Next steps

<CardGroup cols={2}>
  <Card title="Installation" icon="download" href="/getting-started/installation">
    Add the registry to your project and install your first component.
  </Card>
  <Card title="Themes" icon="palette" href="/themes/overview">
    Learn how Corti themes work and how to apply them.
  </Card>
</CardGroup>
```

**Step 2: Commit**

```bash
git add index.mdx
git commit -m "docs: write introduction page"
```

---

### Task 3: Create Installation page

**Files:**
- Create: `getting-started/installation.mdx`

**Step 1: Create the getting-started directory and file**

```mdx
---
title: Installation
description: Add corti-ds to an existing shadcn project.
---

## Prerequisites

Your project must already have shadcn initialized — meaning a `components.json` file exists at the root. If you haven't done that yet, follow the [shadcn installation guide](https://ui.shadcn.com/docs/installation) first.

## Add the registry

Open `components.json` and add corti-ds to the `registries` array:

```json
{
  "registries": [
    {
      "name": "corti",
      "url": "<REGISTRY_URL>"
    }
  ]
}
```

Replace `<REGISTRY_URL>` with the hosted registry URL (e.g. `https://your-deployment.vercel.app/r`).

## Install a component

Use the shadcn CLI with the `@corti/` prefix:

```bash
npx shadcn@latest add @corti/button
```

The component source is copied into your project at `components/ui/button.tsx`, exactly as it would be with a direct shadcn install.

## Install a theme

Themes are registry items too:

```bash
npx shadcn@latest add @corti/theme-console
```

See the [Themes](/themes/overview) section for what each theme provides.
```

**Step 2: Commit**

```bash
git add getting-started/installation.mdx
git commit -m "docs: write installation page"
```

---

### Task 4: Create Themes Overview page

**Files:**
- Create: `themes/overview.mdx`

**Step 1: Create the themes directory and overview file**

```mdx
---
title: Overview
description: How Corti themes work.
---

corti-ds ships three theme suites — Console, Assistant, and Showcase — plus a shared set of semantic color tokens via `theme-core`.

## How themes work

Themes are applied by setting a `data-theme` attribute on `<html>`. The CSS variables for colors, radius, and typography are scoped to that attribute, so switching themes is a single DOM change.

```js
document.documentElement.dataset.theme = "corti-console-light"
```

Each theme comes in light and dark variants. Setting a dark variant also adds the `dark` class and sets `color-scheme` automatically — no separate dark mode handling needed.

To return to the shadcn default (no Corti theme), remove the attribute:

```js
delete document.documentElement.dataset.theme
```

## Available themes

| Theme value | Suite |
|---|---|
| `corti-console-light` | Console |
| `corti-console-dark` | Console |
| `corti-assistant-light` | Assistant |
| `corti-assistant-dark` | Assistant |
| `corti-showcase-light` | Showcase |
| `corti-showcase-dark` | Showcase |

## theme-core

`theme-core` provides semantic CSS variables shared across all Corti themes — success, warning, error, and info color tokens. Install it alongside any theme:

```bash
npx shadcn@latest add @corti/theme-core
```

## Theme Switcher

The [`theme-switcher`](/themes/theme-switcher) component is a ready-made dropdown that handles theme selection and persistence for you.
```

**Step 2: Commit**

```bash
git add themes/overview.mdx
git commit -m "docs: write themes overview page"
```

---

### Task 5: Create Console theme page

**Files:**
- Create: `themes/console.mdx`

**Step 1: Create the file**

```mdx
---
title: Console
description: Monochrome, terminal-inspired theme.
---

The Console theme is a high-contrast monochrome design suited to data-dense, developer-facing interfaces. It strips color in favour of sharp typographic hierarchy.

## Install

```bash
npx shadcn@latest add @corti/theme-console
```

## Variants

| Variant | `data-theme` value |
|---|---|
| Light | `corti-console-light` |
| Dark | `corti-console-dark` |

## Apply

```js
// Light
document.documentElement.dataset.theme = "corti-console-light"

// Dark
document.documentElement.dataset.theme = "corti-console-dark"
```

Dark variants also apply the `dark` class and `color-scheme: dark` automatically.
```

**Step 2: Commit**

```bash
git add themes/console.mdx
git commit -m "docs: write console theme page"
```

---

### Task 6: Create Assistant theme page

**Files:**
- Create: `themes/assistant.mdx`

**Step 1: Create the file**

```mdx
---
title: Assistant
description: Blue-dominant theme for AI and assistant UIs.
---

The Assistant theme uses a blue-dominant palette suited to chat interfaces, AI-powered tools, and any product where a calm, focused feel is appropriate.

## Install

```bash
npx shadcn@latest add @corti/theme-assistant
```

## Variants

| Variant | `data-theme` value |
|---|---|
| Light | `corti-assistant-light` |
| Dark | `corti-assistant-dark` |

## Apply

```js
// Light
document.documentElement.dataset.theme = "corti-assistant-light"

// Dark
document.documentElement.dataset.theme = "corti-assistant-dark"
```
```

**Step 2: Commit**

```bash
git add themes/assistant.mdx
git commit -m "docs: write assistant theme page"
```

---

### Task 7: Create Showcase theme page

**Files:**
- Create: `themes/showcase.mdx`

**Step 1: Create the file**

```mdx
---
title: Showcase
description: Playful 90s-inspired theme with IBM Plex Mono and square edges.
---

The Showcase theme is deliberately distinctive — a 90s/8-bit aesthetic using IBM Plex Mono for typography and hard square corners throughout. Use it for demos, internal tools, or anywhere personality matters.

## Install

```bash
npx shadcn@latest add @corti/theme-showcase
```

## Variants

| Variant | `data-theme` value |
|---|---|
| Light | `corti-showcase-light` |
| Dark | `corti-showcase-dark` |

## Apply

```js
// Light
document.documentElement.dataset.theme = "corti-showcase-light"

// Dark
document.documentElement.dataset.theme = "corti-showcase-dark"
```
```

**Step 2: Commit**

```bash
git add themes/showcase.mdx
git commit -m "docs: write showcase theme page"
```

---

### Task 8: Create Theme Switcher page

**Files:**
- Create: `themes/theme-switcher.mdx`

**Step 1: Create the file**

```mdx
---
title: Theme Switcher
description: A dropdown component for switching Corti themes at runtime.
---

`CortiThemeSwitcher` is a ready-made dropdown that handles theme selection, application, and persistence. Drop it anywhere in your app.

## Install

```bash
npx shadcn@latest add @corti/theme-switcher
```

## Usage

```tsx
import { CortiThemeSwitcher } from "@/components/ui/corti-theme-switcher"

export function App() {
  return (
    <div>
      <CortiThemeSwitcher />
    </div>
  )
}
```

## How it works

- Renders a `<Select>` with all seven theme options plus **Shadcn Default**
- On mount, reads the current `data-theme` attribute or falls back to `localStorage`
- On change, sets `data-theme` on `<html>`, toggles the `dark` class, sets `color-scheme`, and persists to `localStorage` under the key `corti-theme`
- Selecting **Shadcn Default** removes the `data-theme` attribute entirely and resets dark mode

## Manual theme switching

If you want to apply themes without the component:

```js
// Apply a theme
document.documentElement.dataset.theme = "corti-console-dark"
document.documentElement.classList.add("dark")
document.documentElement.style.colorScheme = "dark"

// Reset to shadcn default
delete document.documentElement.dataset.theme
document.documentElement.classList.remove("dark")
document.documentElement.style.colorScheme = "light"
```
```

**Step 2: Commit**

```bash
git add themes/theme-switcher.mdx
git commit -m "docs: write theme-switcher page"
```

---

### Task 9: Create Components Reference page

**Files:**
- Create: `components/reference.mdx`

**Step 1: Create the components directory and file**

```mdx
---
title: Reference
description: All components available under the @corti/* namespace.
---

corti-ds mirrors the full shadcn component catalog under the `@corti/*` namespace. Install any component the same way:

```bash
npx shadcn@latest add @corti/<component>
```

Components are copied into your project at `components/ui/` just as they would be with a direct shadcn install.

## Available components

| Component | Install |
|---|---|
| Accordion | `npx shadcn@latest add @corti/accordion` |
| Alert | `npx shadcn@latest add @corti/alert` |
| Alert Dialog | `npx shadcn@latest add @corti/alert-dialog` |
| Aspect Ratio | `npx shadcn@latest add @corti/aspect-ratio` |
| Avatar | `npx shadcn@latest add @corti/avatar` |
| Badge | `npx shadcn@latest add @corti/badge` |
| Breadcrumb | `npx shadcn@latest add @corti/breadcrumb` |
| Button | `npx shadcn@latest add @corti/button` |
| Calendar | `npx shadcn@latest add @corti/calendar` |
| Card | `npx shadcn@latest add @corti/card` |
| Carousel | `npx shadcn@latest add @corti/carousel` |
| Checkbox | `npx shadcn@latest add @corti/checkbox` |
| Collapsible | `npx shadcn@latest add @corti/collapsible` |
| Command | `npx shadcn@latest add @corti/command` |
| Context Menu | `npx shadcn@latest add @corti/context-menu` |
| Dialog | `npx shadcn@latest add @corti/dialog` |
| Drawer | `npx shadcn@latest add @corti/drawer` |
| Dropdown Menu | `npx shadcn@latest add @corti/dropdown-menu` |
| Form | `npx shadcn@latest add @corti/form` |
| Hover Card | `npx shadcn@latest add @corti/hover-card` |
| Input | `npx shadcn@latest add @corti/input` |
| Input OTP | `npx shadcn@latest add @corti/input-otp` |
| Kbd | `npx shadcn@latest add @corti/kbd` |
| Label | `npx shadcn@latest add @corti/label` |
| Menubar | `npx shadcn@latest add @corti/menubar` |
| Navigation Menu | `npx shadcn@latest add @corti/navigation-menu` |
| Pagination | `npx shadcn@latest add @corti/pagination` |
| Popover | `npx shadcn@latest add @corti/popover` |
| Progress | `npx shadcn@latest add @corti/progress` |
| Radio Group | `npx shadcn@latest add @corti/radio-group` |
| Resizable | `npx shadcn@latest add @corti/resizable` |
| Scroll Area | `npx shadcn@latest add @corti/scroll-area` |
| Select | `npx shadcn@latest add @corti/select` |
| Separator | `npx shadcn@latest add @corti/separator` |
| Sheet | `npx shadcn@latest add @corti/sheet` |
| Sidebar | `npx shadcn@latest add @corti/sidebar` |
| Skeleton | `npx shadcn@latest add @corti/skeleton` |
| Slider | `npx shadcn@latest add @corti/slider` |
| Sonner | `npx shadcn@latest add @corti/sonner` |
| Switch | `npx shadcn@latest add @corti/switch` |
| Table | `npx shadcn@latest add @corti/table` |
| Tabs | `npx shadcn@latest add @corti/tabs` |
| Textarea | `npx shadcn@latest add @corti/textarea` |
| Toast | `npx shadcn@latest add @corti/toast` |
| Toggle | `npx shadcn@latest add @corti/toggle` |
| Toggle Group | `npx shadcn@latest add @corti/toggle-group` |
| Tooltip | `npx shadcn@latest add @corti/tooltip` |
```

**Step 2: Commit**

```bash
git add components/reference.mdx
git commit -m "docs: write components reference page"
```

---

### Task 10: Clean up starter kit files

**Files:**
- Delete: `quickstart.mdx`
- Delete: `development.mdx`
- Delete: `essentials/` (whole directory)
- Delete: `api-reference/` (whole directory)
- Delete: `ai-tools/` (whole directory)
- Delete: `snippets/` (whole directory)

**Step 1: Remove starter kit content**

```bash
rm quickstart.mdx development.mdx
rm -rf essentials/ api-reference/ ai-tools/ snippets/
```

**Step 2: Commit**

```bash
git add -A
git commit -m "chore: remove mintlify starter kit content"
```

---

## Notes

- **Registry URL:** Replace `<REGISTRY_URL>` in `getting-started/installation.mdx` with the actual hosted URL before publishing. Check the corti-ds Vercel deployment or README for the correct value.
- **Logo/favicon:** The existing `/logo/light.svg`, `/logo/dark.svg`, and `/favicon.svg` are Mintlify defaults — replace with Corti branding if available.
- **Component list:** The reference table is based on the `public/r` directory at time of writing. If new components are added to the registry, add them to the table.
- **Mintlify preview:** Run `mintlify dev` locally to preview before deploying.
