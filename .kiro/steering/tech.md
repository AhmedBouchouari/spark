# Tech Stack

## Framework & Build

| Layer | Technology |
|-------|-----------|
| Framework | [Astro](https://astro.build) v7 |
| CSS | Tailwind CSS v4 (via `@tailwindcss/vite` plugin) |
| Bundler | Vite (built into Astro) |
| Language | TypeScript (strict tsconfig) |
| Node | ≥ 22.12.0 |

## Integrations

- **`@tailwindcss/vite`** — Tailwind v4 is loaded as a Vite plugin, not a PostCSS plugin. There is no `tailwind.config.js`; configuration lives in `src/styles/global.css` using `@import "tailwindcss"` and `@variant`/`@custom-variant` directives.
- **Astro `Image` component** (`astro:assets`) — used for all image rendering with `width`/`height` props for CLS prevention.
- **Google Fonts** — loaded via `<link>` in the layout: *Plus Jakarta Sans* (body) and *Outfit* (headings).
- No UI framework (React, Vue, etc.) — all components are `.astro` files with vanilla JS `<script>` blocks.

## Environment Variables

| Variable | Purpose |
|----------|---------|
| `PUBLIC_WHATSAPP_URL` | WhatsApp contact link (default: `https://wa.me/212600000000`) |

## Common Commands

```bash
# Start dev server (use background mode per project rules)
astro dev --background

# Stop background dev server
astro dev stop

# Check dev server status / logs
astro dev status
astro dev logs

# Production build
astro build

# Preview production build
astro preview
```

> The `dev` script in `package.json` uses `--host` to expose the server on the local network.
