# Project Structure

## Directory Layout

```
spark/
├── public/                  # Static assets served as-is (favicon)
├── src/
│   ├── assets/
│   │   └── images/
│   │       ├── hero/        # Slideshow background images (webp/jpg)
│   │       └── logo/        # Spark logo variants
│   ├── components/          # All UI components (Astro only, no framework)
│   ├── data/
│   │   └── translations.ts  # Bilingual copy (FR + AR) — single source of truth
│   ├── layouts/
│   │   └── Layout.astro     # Root HTML shell (fonts, meta, theme/lang init)
│   ├── pages/
│   │   └── index.astro      # Single-page app — imports and sequences all sections
│   └── styles/
│       └── global.css       # CSS custom properties, Tailwind import, global resets
├── astro.config.mjs
├── package.json
└── tsconfig.json
```

## Component Inventory

Each component maps to one landing page section:

| File | Section |
|------|---------|
| `Navbar.astro` | Sticky header, language switcher, theme toggle, mobile menu |
| `Hero.astro` | Full-screen hero with rotating background slideshow |
| `ProblemSection.astro` | Pain points + solution pivot |
| `SparkSystem.astro` | 4-step process explanation |
| `OfferSection.astro` | Pricing card + feature list |
| `Testimonials.astro` | Social proof / metrics |
| `WhySpark.astro` | Differentiators section |
| `FinalCTA.astro` | Bottom call-to-action |
| `Footer.astro` | Site footer |

## Architecture Patterns

- **Single page**: `pages/index.astro` is the only route; all sections are imported components laid out sequentially.
- **Scoped styles**: Each `.astro` component carries its own `<style>` block. Global tokens (colors, shadows, radii, container width) live in `global.css` as CSS custom properties on `:root` and `[data-theme="dark"]`.
- **i18n via `data-i18n` attributes**: Text nodes carry a `data-i18n="keyName"` attribute. `Navbar.astro` contains the language-switching script that walks the DOM and swaps text from `translations.ts`. Default render language is French.
- **RTL support**: Switching to Arabic sets `dir="rtl"` on `<html>`. Components use `[dir="rtl"]` CSS selectors for directional overrides.
- **Dark / light theme**: Toggled by setting `data-theme="dark"` on `<html>`. Persisted in `localStorage` under key `spark-theme`. An inline script in `Layout.astro` applies the saved preference before first paint to prevent flash.
- **Environment config**: The WhatsApp URL is read from `import.meta.env.PUBLIC_WHATSAPP_URL` with a fallback default.

## Styling Conventions

- CSS custom properties (not Tailwind utilities) are preferred for layout, spacing, and theming.
- Tailwind utility classes may be used for rapid one-off styles but are secondary to the component `<style>` blocks.
- Responsive breakpoints follow a mobile-first approach with explicit `@media (max-width: ...)` overrides for tablet (1024px), mobile (768px), small phone (480px), and very small phone (360px).
