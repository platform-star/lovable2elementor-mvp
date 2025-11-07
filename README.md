
# Lovable → Elementor Converter (MVP)

This is a self-hosted MVP that takes a Lovable site URL **or** a static site ZIP and outputs:
- `export/elementor-kit.json` (Elementor Site Kit)
- `export/media.zip` (all images)
- `export/report.json` (what was mapped)

> Intended runtime: Node 18+; headless render via Playwright.

## Quick Start

```bash
# 1) Install dependencies
npm install

# 2) Install Playwright browsers (one-time)
npx playwright install

# 3) Run
npm start
```

Open http://localhost:3000 and use the upload form.

## How it works
1. Crawls the provided URL (or unpacks the ZIP) to get HTML, CSS, images.
2. Uses Playwright to render and compute DOM; falls back to axios if needed.
3. Heuristically detects sections (hero, features, CTA, about, services, faq, contact).
4. Maps DOM nodes to Elementor widgets (Heading, Text Editor, Image, Button, Spacer).
5. Builds a minimal Site Kit JSON (pages + global colors/typography) and zips media.

## Notes / Limitations
- This MVP focuses on common static sections. Advanced JS widgets may be flattened.
- Pixel-perfect typography/spacing may need small tweaks post-import.
- Forms are mapped to Elementor Forms when a typical `<form>` is detected; custom APIs require manual wiring.
- You can extend the mappers in `server/mapping/` to support more widgets.

## Output
- `export/elementor-kit.json` → Import in WordPress → Elementor → *Tools → Import/Export Kit*.
- `export/media.zip` → Not always required; the importer plugin can auto-upload media URLs.

