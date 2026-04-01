# HTML Layout Patterns

**This is a structural reference, not a strict design template.** Use these patterns for layout structure, but generate the visual design dynamically based on content signals.

## Design is Adaptive

Each presentation should have unique visual character. Extract design direction from:

- Content type (pitch vs report vs strategy)
- Audience (executive vs creative vs technical)
- Brand context (if available)
- Industry signals
- Tone of the brief

Do NOT output generic template styling. Design with intention.

## Structural Patterns

### Pattern 1: Cover Slide

Full-viewport hero establishing visual identity.

```html
<div class="cover">
  <!-- Optional hero image -->
  <h1>{title}</h1>
  <p class="subtitle">{key-message}</p>
  <p class="meta">{date} | {context}</p>
</div>
```

**Design variations:**
- Gradient background (corporate/tech)
- Hero image overlay (consumer/creative)
- Bold typography focus (minimalist)
- Asymmetric layout (modern/bold)

### Pattern 2: Section Slide

Content sections with clear visual hierarchy.

```html
<section>
  <h2>{section-title}</h2>
  <p class="key-message">{governing-claim}</p>
  {content}
</section>
```

**Design variations:**
- Left-aligned, generous whitespace (executive)
- Centered, large type (impact-focused)
- Two-column grid (data-rich)
- Card-based layout (scannable)

### Pattern 3: Data Slide

Charts with contextual framing.

```html
<section>
  <h2>{title}</h2>
  <p class="insight">{what-this-data-means}</p>
  <div class="chart-container">
    <canvas id="chart-{id}"></canvas>
  </div>
</section>
```

**Design variations:**
- Large single chart (focal point)
- Multi-chart grid (comparison)
- Chart + callout sidebar (narrative)

### Pattern 4: Closing Slide

Next steps and call to action.

```html
<section class="closing">
  <h2>Next Steps</h2>
  {actions}
</section>
```

## CSS Architecture

Use CSS custom properties for theming:

```css
:root {
  /* Derive these from content/brand signals */
  --primary: {adaptive};
  --secondary: {adaptive};
  --accent: {adaptive};
  --bg: {adaptive};
  --text: {adaptive};
  
  /* Spacing rhythm */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 32px;
  --space-xl: 64px;
}
```

## Required Technical Elements

These are non-negotiable for functionality:

```html
<!-- Chart.js CDN -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<!-- PDF Export Button -->
<button class="pdf-btn" onclick="window.print()">Export PDF</button>

<!-- Print Styles -->
<style>
@media print {
  .pdf-btn { display: none; }
  .cover { page-break-after: always; }
  section { page-break-inside: avoid; }
}
</style>
```

## Typography Approaches

Choose based on content signals:

| Style | When | Implementation |
|-------|------|----------------|
| **System** | Corporate, safe | `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto` |
| **Modern** | Tech, startup | Add `'Inter', 'DM Sans'` via Google Fonts |
| **Editorial** | Consumer, lifestyle | Add `'Playfair Display', 'Merriweather'` for headlines |
| **Technical** | Data-heavy | `'JetBrains Mono', 'IBM Plex Sans'` for charts |

## Color Palette Strategies

| Palette | Signals | Colors |
|---------|---------|--------|
| **Executive** | Corporate, finance | Navy primary, gold accent, white/light gray |
| **Tech** | SaaS, startup | Deep blue or purple, cyan accent, dark mode capable |
| **Creative** | Agency, consumer | Bold primary, contrasting accent, vibrant |
| **Minimal** | Luxury, editorial | Black/white/gray, single accent |
| **Friendly** | Consumer brand | Warm colors, approachable, soft shadows |

## Responsive Base

```css
@media (max-width: 768px) {
  .container { padding: 40px 20px; }
  .cover h1 { font-size: 2rem; }
  h2 { font-size: 1.5rem; }
}
```

## The Test

Before finalizing, ask:

- Does this look like a unique presentation or a generic template?
- Does the design match the content's tone and audience?
- Would a human designer make similar choices?

If the answer is "generic template," regenerate with stronger design intent.