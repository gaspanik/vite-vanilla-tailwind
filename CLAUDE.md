# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

Use `pnpm` for all scripts:

```bash
pnpm dev       # Dev server at http://localhost:5173
pnpm build     # Production build to dist/
pnpm preview   # Preview production build
pnpm check     # Lint + format with Biome (run before committing)
pnpm format    # Format only
pnpm lint      # Lint only
```

## Architecture

This is a Vite + Vanilla JS + Tailwind CSS v4 multi-page app. No framework—plain HTML, CSS, and JS.

**Multi-page build**: `vite.config.js` uses `glob.sync('*.html')` to auto-detect all HTML files at the project root as Rollup entry points. Adding a new page requires only creating a new `.html` file at the root—no config changes needed.

**Tailwind CSS v4**: Uses `@tailwindcss/vite` plugin. No `tailwind.config.js` or `postcss.config.js` needed. CSS entry is a single `@import "tailwindcss";` in `src/style.css`.

**Lucide Icons**: Icons are tree-shaken at build time. Each icon used in HTML must be explicitly imported and registered in `src/main.js`:
```javascript
import { createIcons, IconName } from 'lucide'
createIcons({ icons: { IconName } })
```
Then used in HTML with kebab-case: `<i data-lucide="icon-name"></i>`

**Path alias**: `@` resolves to `./src`.

## Code Conventions (Biome)

- 2-space indentation, 80-char line width, LF line endings
- Single quotes in JS, double quotes in HTML/CSS
- Semicolons as needed (ASI), trailing commas always
- Void elements self-closed in HTML
- `dist/` is excluded from linting

## HTML Page Requirements

Every HTML file must include:
```html
<script type="module" src="/src/main.js"></script>
```
Use `lang="ja"` for Japanese-language pages.
