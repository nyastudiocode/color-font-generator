# Æsthetic — Random Color & Font Generator

A static, single-file web tool for generating cohesive color palettes and font pairings. Built for designers and developers who want beautiful, export-ready combinations fast.

![Æsthetic Generator](favicon.png)

---

## Features

### 🎨 Color Palettes
- Generates 4–6 color palettes using 5 harmony strategies: **monochromatic**, **analogous**, **split-complementary**, **triadic**, and **tetradic**
- **Base Hue picker** — lock the palette to any hue using a native color picker
- **Saturation slider** — slide from muted to vivid; remaps the existing palette's saturation without regenerating new hues
- **Lock to first swatch** — checkbox that anchors the base hue to the current first swatch, carrying it forward on every shuffle
- WCAG AA contrast badges on every swatch (vs. white and black)
- Click any swatch to copy its HEX value to clipboard

### ✍️ Typography
- 100 curated Google Font pairings across 10 categories: Editorial, Elegant, Modern Sans, Tech, Humanist, Display, Slab Serif, Geometric, Refined, and Transitional
- Live preview with heading, subheading, body text, and button sample
- Fonts are loaded dynamically — only the selected pair is fetched

### 👁 Palette in Context
- A live mini-UI mockup (nav bar, hero, feature cards, footer) rendered with the current palette
- Text colors auto-computed per region using WCAG contrast ratios

### 💾 Favorites
- Save any palette + font combination to `localStorage`
- Re-apply or delete saved favorites at any time
- Favorites persist across page reloads

### 📤 Export
- **CSS variables** — copy a `:root {}` block with `--color-1` through `--color-n` plus font family vars
- **JSON** — copy or download a structured object: `{ palette, fonts, name }`

### ⌨️ Keyboard Shortcuts
| Key | Action |
|-----|--------|
| `Space` | Shuffle palette and fonts |
| `S` | Save current combination |
| `C` | Copy CSS variables |
| `↑` / `↓` | Adjust saturation by 5% |

---

## Presets

Three curated starting points are built in:

| Preset | Description |
|--------|-------------|
| **Minimal** | Warm neutrals with a gold accent — Playfair Display + Source Sans 3 |
| **Playful** | Pinks, reds, and sky blue — Josefin Sans + Nunito |
| **Bold** | Deep navy and electric red on near-black — Unbounded + Plus Jakarta Sans |

---

## Getting Started

This is a fully static project — no build steps, no dependencies, no server required.

### Run locally

```bash
# Clone the repo
git clone https://github.com/your-username/aesthetic-generator.git
cd aesthetic-generator

# Open directly in your browser
open index.html
```

Or serve it with any static file server:

```bash
npx serve .
# or
python3 -m http.server 8080
```

### Deploy to GitHub Pages

1. Push the repo to GitHub
2. Go to **Settings → Pages**
3. Set source to `main` branch, `/ (root)`
4. Your site will be live at `https://your-username.github.io/aesthetic-generator`

> The favicon is linked as `favicon.png` (relative path, no leading slash) so it resolves correctly on both root and subdirectory GitHub Pages deployments.

---

## Project Structure

```
aesthetic-generator/
├── index.html      # Entire app — markup, styles, and scripts in one file
├── favicon.png     # Site favicon
└── README.md       # This file
```

Everything lives in `index.html`:

- **`<style>`** — CSS custom properties, two-column responsive layout, component styles, dark mode, animations
- **`<script>`** — All JS: palette generation, font loading, contrast checking, clipboard, localStorage, keyboard shortcuts

---

## Technical Notes

### Palette Generation
Palettes are generated in HSL color space using a randomly selected harmony strategy. When a base hue is set (via picker or lock-to-swatch), the hue is fixed while strategy and lightness values are randomized. Saturation remapping scales each swatch's original saturation proportionally without touching hues or lightness.

### Contrast Checking
Uses the WCAG 2.1 relative luminance formula with full sRGB linearization. AA pass threshold is 4.5:1 for normal text.

### Font Loading
Google Fonts are injected as `<link>` tags on demand — only the active pair is loaded. Previously loaded pairs are cached to avoid duplicate requests.

### Storage Keys
| Key | Contents |
|-----|----------|
| `aesthetic.favorites` | JSON array of saved palette + font combinations |
| `aesthetic.settings` | `{ theme: "light" \| "dark" }` |

---

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge). Uses:
- CSS Grid and Custom Properties
- `navigator.clipboard` with `execCommand` fallback
- `localStorage`
- Native `<input type="color">` and `<input type="range">`

---

## License

MIT — free to use, modify, and distribute.