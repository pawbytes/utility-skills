# Stage 3: Generate

**Goal:** Produce a complete, self-contained HTML presentation file with adaptive design.

## Output Location

Write to: `{project-root}/.pawbytes/tools-output/presentations/{sanitized-title}.html`

Sanitize title: lowercase, spaces to hyphens, remove special characters.

Create the output directory if it doesn't exist.

## Design Philosophy

**The template is a structural guide, not a rigid design.** Each presentation should have unique visual character informed by:

- **Content type** — Strategy deck, client pitch, board update, internal review — each has different tonal needs
- **Brand context** — Use brand colors, typography, and visual language if available
- **User brief** — Extract design preferences from the content itself (formal vs bold, minimalist vs data-rich)
- **Industry signals** — Tech, finance, consumer goods — adapt visual language accordingly

The HTML template provides layout patterns and structural elements. You determine the actual design — typography, color palette, spacing rhythm, visual hierarchy, and overall aesthetic.

## HTML Requirements

The generated file must be:
- **Self-contained** — all CSS inline, Chart.js from CDN, no external file dependencies except images
- **Print-ready** — `@media print` styles for clean PDF export
- **Responsive** — readable on desktop and tablet
- **Visually polished** — not generic template output

## Design Extraction from Content

Before writing HTML, analyze the input for design signals:

| Signal | Design Implication |
|--------|-------------------|
| Executive audience | Clean, minimal, high contrast, large type |
| Creative agency | Bold colors, asymmetric layouts, distinctive typography |
| Technical content | More charts, dense information, structured grids |
| Consumer brand | Vibrant, friendly, approachable typography |
| Financial/Corporate | Professional navy/gray, conservative typography, clear data |
| Startup/Pitch | Modern, confident, gradient accents, strong headlines |
| Internal review | Functional, scannable, minimal decoration |

Apply these signals to:
- **Color palette** — Primary, secondary, accent colors
- **Typography** — Font choices (via system fonts or Google Fonts CDN)
- **Spacing** — Tight/dense vs generous/airy
- **Visual weight** — Minimal vs bold graphic elements
- **Chart styling** — Subtle fills vs bold colors

## Layout Patterns

The template provides these structural patterns — adapt the visual treatment:

1. **Cover slide** — Full-viewport hero with title and subtitle
2. **Section slides** — Title + key message + supporting content
3. **Data slides** — Charts with contextual framing
4. **Closing slide** — Next steps / call to action

Use CSS custom properties for theming:
```css
:root {
  --primary: /* derived from brand or content signals */;
  --secondary: /* complementary tone */;
  --accent: /* highlight color */;
  --bg: /* background */;
  --text: /* primary text */;
}
```

## Chart Generation

For each `[Chart: type — what it shows]` flag:

1. Extract the relevant data from the input material
2. Generate Chart.js configuration inline
3. Style charts to match the overall design palette
4. Supported types: `bar`, `line`, `pie`, `doughnut`, `horizontal-bar`, `scatter`

Chart.js loads from CDN: `https://cdn.jsdelivr.net/npm/chart.js`

See `./references/chart-patterns.md` for implementation examples.

## Image Generation

Based on `{image_source}` from Stage 2:

### Gen AI (DALL-E or Gemini Imagen)

For each `[Image: cover]` or `[Image: section-header]`:

1. Write a prompt based on section context and design direction
2. Style should complement the visual language (not generic stock photo look)
3. Use configured API

### Pexels (Stock Photos)

1. Construct a search query from section context
2. Select images that match the design aesthetic
3. Call Pexels API via `pexels_api_key`

### Skip Images

Generate text-only presentation with designed section headers — no placeholders needed.

## Output Validation

Before writing, verify:
- [ ] Design reflects content type and audience
- [ ] All sections from outline are present
- [ ] Charts render with appropriate styling
- [ ] PDF export button works
- [ ] Print styles produce clean output
- [ ] No generic/template feel — design feels intentional

## Completion

Display:
> "Presentation generated: `{output-path}`"

If headless: return only the output path.

If images were skipped due to missing API keys: note this briefly.