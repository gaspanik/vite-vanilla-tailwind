# Vite + Vanilla JS + Tailwind CSS v4 Project Context

## Project Overview

This is a **Vite-based Vanilla JavaScript project** styled with **Tailwind CSS v4** and using **Lucide Icons**. It features a multi-page build setup where HTML files at the project root are automatically detected and built. Code quality is maintained using **Biome** for both linting and formatting.

## Tech Stack

*   **Build Tool**: Vite 7.x
*   **CSS Framework**: Tailwind CSS 4.x (via `@tailwindcss/vite`)
*   **Icons**: Lucide Icons
*   **Linter/Formatter**: Biome
*   **Package Manager**: pnpm (v10.x)
*   **Environment Manager**: mise

## Key Files & Directories

*   `vite.config.js`: Configures Vite, including the **multi-page build strategy** using `glob` to find `*.html` files.
*   `src/main.js`: The main JavaScript entry point shared across pages. Handles Lucide icon initialization.
*   `src/style.css`: Imports Tailwind CSS (`@import "tailwindcss";`).
*   `biome.json`: Configuration for Biome (indentation, quoting, etc.).
*   `*.html`: HTML pages located at the project root.
*   `dist/`: Output directory for production builds.

## Development Workflow

### Commands

Use `pnpm` for all script execution.

| Command | Description |
| :--- | :--- |
| `pnpm dev` | Start the development server at `http://localhost:5173`. |
| `pnpm build` | Build the project for production (output to `dist/`). |
| `pnpm preview` | Preview the production build locally. |
| `pnpm check` | Run Biome to **lint and format** code (recommended before commit). |
| `pnpm format` | Auto-format code using Biome. |
| `pnpm lint` | Lint code using Biome. |

*Note: `mise` tasks are also available (e.g., `mise run vite:dev`).*

### Adding New Pages

1.  Create a new `*.html` file in the **project root** (e.g., `contact.html`).
2.  Include the main script: `<script type="module" src="/src/main.js"></script>`.
3.  Vite will automatically detect it during build thanks to the `glob` pattern in `vite.config.js`.

### Using Icons (Lucide)

1.  **Import**: In `src/main.js`, import the icon component from `lucide`.
2.  **Register**: Add it to the `createIcons` function.
3.  **Use**: In HTML, use the `<i>` tag with the `data-lucide` attribute (kebab-case).

**Example:**
*   `src/main.js`: `import { IceCreamCone } from 'lucide'; createIcons({ icons: { IceCreamCone } });`
*   `index.html`: `<i data-lucide="ice-cream-cone" class="text-blue-500"></i>`

## Coding Standards (Biome)

*   **Indentation**: 2 spaces.
*   **Line Width**: 80 characters.
*   **Quotes**: Single quotes for JavaScript, double quotes for HTML/CSS.
*   **Semicolons**: As needed (ASI).
*   **Trailing Commas**: Always.
*   **HTML**: Void elements are self-closed.

## Architecture Notes

*   **Tailwind v4**: Uses the `@tailwindcss/vite` plugin. No `tailwind.config.js` or `postcss.config.js` is required. Configuration is handled within Vite or CSS variables if needed.
*   **Multi-Page**: The `vite.config.js` uses `glob.sync('*.html')` to dynamically generate the `rollupOptions.input` object, ensuring all root HTML files are entry points.
