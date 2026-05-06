# Spectral

A browser-based color tool for picking, editing, and organizing colors.

## Features

- **Color wheel editor** with HSL controls and a lightness strip
- **EyeDropper** — pick any color directly from your screen (Chrome/Edge 95+)
- **Copy values** in HEX, RGB, or HSL format with one click
- **History** — last 40 picked colors, editable and persistent
- **Palettes** — create named collections, rename, and delete colors
- **Import/Export** palettes as CSV or JSON

## Usage

Open `index.html` in a Chromium-based browser. No build step or dependencies required.

To pick a color from the screen, click **Pick from Screen** (requires Chrome 95+ or Edge 95+). The color wheel and lightness strip let you manually craft any color without leaving the app.

## Palette Import Format

**Hex codes** (paste directly): one or more `#RRGGBB` values, comma- or newline-separated.

**CSV**: any text file containing `#RRGGBB` values.

**JSON**: either `["#FF0000", ...]` or `{"name": "My Palette", "colors": ["#FF0000", ...]}`.

## Browser Support

Full functionality requires the [EyeDropper API](https://developer.mozilla.org/en-US/docs/Web/API/EyeDropper). The editor and palette features work in any modern browser.
