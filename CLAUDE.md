# CLAUDE.md — Instructions for Claude Code

## Project Overview

This is a **2×1 thermal label printer web app** for printing numbered labels for online auctions. It generates sequential numbered labels that can be downloaded as a PDF or printed directly to a thermal printer.

## Key Facts

- **Single-file app**: Everything is in `index.html`. No build system, no framework.
- **Only external dep**: jsPDF loaded from CDN (`https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js`)
- **Label size**: 2 inches wide × 1 inch tall
- **Output**: PDF (one 2×1 page per label) or direct browser print with CSS paged media
- **Deploy**: Static site on Vercel. Just push and it deploys.

## When making changes

- Keep it as a single `index.html` unless there's a strong reason to split
- The dark theme uses CSS variables defined in `:root` — change colors there
- jsPDF uses built-in Helvetica — no custom font files
- If adding features, keep the UI pattern consistent: cards with `.card` class, `.card-title` for headers, `.form-group` for inputs
- The `getConfig()` function is the single source of truth for all settings
- Both `downloadPDF()` and `printDirect()` read from `getConfig()` — keep them in sync
- For large label runs (1000+), use the async pattern with `setTimeout(0)` to avoid freezing

## Testing

- Test PDF output by downloading and opening in a PDF viewer — each page should be exactly 2" × 1"
- Test print by clicking Print Direct — the popup should show one label per page
- Test with: 1-10 (small), 1-300 (medium), 1-1000 (large run)
- Test with all options: prefix, suffix, business name, border, different font sizes, different padding

## Business Context

This is for printing numbered labels for online auctions (lot numbers / item tags). The owner uses thermal label printers. Keep it simple and reliable — this is a production tool, not a demo.
