# Label Printer — 2×1 Thermal Label Generator

A lightweight web app for generating sequential numbered labels (2" × 1") for thermal printers. Built for printing numbered labels for online auctions.

## Live Stack

- **Single-file app**: Everything lives in `index.html` (HTML + CSS + JS)
- **No build step**: Static site, no framework, no bundler
- **External dependency**: [jsPDF](https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js) loaded via CDN for PDF generation
- **Fonts**: DM Sans (UI) + JetBrains Mono (numbers) via Google Fonts
- **Deploy target**: Vercel (static)

## Features

### Label Content
- **Prefix text** — line above the number (e.g. "Bag #", "Order")
- **Sequential numbers** — configurable start, end, and step increment
- **Suffix text** — line below the number (e.g. "of 300", "— Wash & Fold")
- **Business name** — small text at bottom of label

### Formatting Options
- Number padding: none, 2-digit, 3-digit, 4-digit
- Font size: Small / Medium / Large
- Bold toggle
- Optional border around each label
- Step/increment for non-sequential numbering

### Output Methods
1. **Download PDF** — Generates a PDF where each page is exactly 2" × 1". One label per page. Ready for thermal printer or standard printer.
2. **Print Direct** — Opens browser print dialog with CSS `@page { size: 2in 1in; }` and page breaks between labels. Ideal for direct thermal printer connection (Dymo, Brother, Zebra).

### Preview
- Live preview showing first 50 labels
- Label count and page count stats
- Real-time updates as you change settings

## Architecture

```
index.html          ← entire app (single file)
├── <style>         ← dark theme UI, responsive, grain texture overlay
├── <body>          ← form inputs, preview area, action buttons
└── <script>        ← all logic:
    ├── getConfig()        → reads all form inputs into a config object
    ├── generatePreview()  → renders label cards in the preview area
    ├── downloadPDF()      → uses jsPDF to create 2x1 per-page PDF
    ├── printDirect()      → opens popup with CSS paged media for thermal printing
    ├── setFontSize()      → toggles S/M/L font size
    ├── clearAll()         → resets form to defaults
    └── formatNum()        → handles zero-padding
```

## PDF Generation Details

- Page size: 2" wide × 1" tall (landscape orientation in jsPDF)
- Font: Helvetica (built into jsPDF, no font embedding needed)
- Number font sizes: Small=18pt, Medium=24pt, Large=32pt
- Progress updates every 200 labels to keep UI responsive
- Uses async/await with setTimeout(0) to prevent browser freezing on large runs

## Direct Print Details

- Opens a new window with clean HTML
- CSS `@page { size: 2in 1in; margin: 0; }` sets the page to label size
- Each label div has `page-break-after: always`
- Font: Arial + Courier New (system fonts for reliability)
- Auto-triggers `window.print()` on load

## Design

- Dark theme with amber (#f59e0b) accent
- Grain texture overlay via inline SVG filter
- Cards with subtle borders
- Toggle switches for boolean options
- Responsive — works on mobile

## Deployment

```bash
# Already deployable as-is on Vercel
# No vercel.json needed — auto-detected as static site
vercel
```

## Future Ideas / TODOs

- [ ] Barcode/QR code on labels
- [ ] Custom label sizes (not just 2×1)
- [ ] Logo/image upload for labels
- [ ] Save/load label templates
- [ ] Batch print with different text per label (CSV import)
- [ ] Dymo SDK direct integration
- [ ] Convert to React/Next.js if complexity grows
