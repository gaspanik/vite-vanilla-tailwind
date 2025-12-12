# Copilot Instructions

## Project Overview

This is a Vite-based vanilla JavaScript project using Tailwind CSS v4 with multi-page build support. HTML files live at the project root (not in `pages/`), and Vite automatically builds all `*.html` files found there.

## Architecture

- **Multi-page setup**: All `*.html` files at root are auto-detected via `glob.sync('*.html')` in `vite.config.js` and built as separate entry points
- **Tailwind CSS v4**: Uses `@tailwindcss/vite` plugin (no `tailwind.config.js` or `postcss.config.js` needed)
- **Lucide icons**: Import only the specific icons needed in `src/main.js`, then use `data-lucide="icon-name"` in HTML (e.g., `IceCreamCone` → `ice-cream-cone`)

## Key Files

- `vite.config.js`: Defines multi-page input using glob pattern `*.html` at root
- `src/main.js`: Shared JavaScript entry point for all pages, imports Lucide icons
- `src/style.css`: Single line: `@import "tailwindcss";`
- `biome.json`: Code formatting/linting configuration (Biome replaces ESLint/Prettier)

## Developer Workflows

### Commands (use pnpm)
```bash
pnpm dev       # Start dev server on http://localhost:5173
pnpm build     # Production build to dist/
pnpm preview   # Preview production build
pnpm format    # Format code with Biome
pnpm lint      # Lint code with Biome
pnpm check     # Format + lint in one command
```

### mise Tasks (alternative)
```bash
mise run vite:dev       # Same as pnpm dev
mise run vite:build     # Same as pnpm build (with confirmation)
mise run biome:format   # Format with confirmation
mise run biome:lint     # Lint with confirmation
```

## Code Conventions

### Biome Settings
- **Indentation**: 2 spaces
- **Line width**: 80 characters
- **Quote style**: Single quotes for JS, double for HTML/CSS
- **Semicolons**: As needed (ASI-aware)
- **Trailing commas**: Always

### HTML Structure
- Each HTML file must include `<script type="module" src="/src/main.js"></script>`
- Use `lang="ja"` for Japanese language
- Always use `<i data-lucide="icon-name"></i>` for icons (icon must be imported in `src/main.js`)

### Adding New Pages
1. Create new `*.html` file at project root (e.g., `contact.html`)
2. Add the standard `<script type="module" src="/src/main.js"></script>` tag
3. No configuration changes needed—Vite auto-detects it

### Adding New Icons
1. Import in `src/main.js`: `import { createIcons, NewIcon } from 'lucide'`
2. Add to `createIcons({ icons: { NewIcon } })`
3. Use in HTML with kebab-case: `<i data-lucide="new-icon"></i>`

**Example:**
```javascript
// src/main.js
import { createIcons, IceCreamCone, Heart, Star } from 'lucide'

createIcons({ 
  icons: { 
    IceCreamCone,
    Heart,
    Star
  } 
})
```

```html
<!-- Basic icon -->
<i data-lucide="ice-cream-cone"></i>

<!-- With Tailwind styling -->
<i class="text-amber-400" data-lucide="ice-cream-cone"></i>

<!-- With size and color -->
<i class="w-6 h-6 text-red-500" data-lucide="heart"></i>
```

## Package Management

- **Package manager**: pnpm (enforced via `packageManager` field)
- **Version manager**: mise (see `mise.toml` for Node.js version)
- Always use `pnpm install` (not npm/yarn)
