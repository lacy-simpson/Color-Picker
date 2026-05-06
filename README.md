# Spectral

A browser-based color tool for picking, organizing, and exporting colors. Single HTML file, no build step, no dependencies.

## Features

### Picker
- **Color wheel** with HSL controls and a lightness strip for precise color crafting
- **EyeDropper** — sample any color directly from your screen (Chrome/Edge 95+)
- **Copy values** in HEX, RGB, or HSL with one click
- **Add to palette** — select a target palette from the dropdown and click + Add; the palette's current colors preview live beneath the selector so you can see what's already there as you build it
- **New Palette** and **Import** accessible directly from the picker via the ⋯ menu next to the dropdown

### History
- Last 40 picked colors displayed in a sidebar beside the picker
- Click any swatch to restore that color
- Edit mode to remove individual entries; Clear to wipe the full history
- Persisted across sessions

### Palettes
- Create named palettes and organize them into **groups**
- A palette can belong to more than one group
- **Drag to reorder** palettes within a group using the ⠿ handle
- Inline rename for both palettes and groups
- Groups are collapsible
- Each palette has a ⋯ menu with:
  - Group assignment (checkbox per group)
  - Copy HEX values to clipboard
  - Download as CSV or JSON
  - Delete

### Import
Accessible from the Palettes tab or the ⋯ menu on the Picker tab.

| Format | Description |
|--------|-------------|
| Hex codes | Paste `#RRGGBB` values, comma- or newline-separated |
| CSV | Any text file containing `#RRGGBB` values |
| JSON (single palette) | `{"name": "…", "colors": ["#…"]}` or a plain array `["#…"]` |
| JSON (group) | `{"name": "…", "palettes": [{"name": "…", "colors": ["#…"]}]}` — imports all palettes and recreates the group |

### Export
- **Per palette**: Copy HEX, Download CSV, Download JSON via the palette ⋯ menu
- **Per group**: Export all palettes in a group as a single JSON file via the group ⋯ menu

## Usage

Open `index.html` in a Chromium-based browser. The app has two tabs:

- **Picker** — color wheel, history sidebar, and the Add to Palette workflow
- **Palettes** — full palette and group management, import, and export

## Browser Support

The [EyeDropper API](https://developer.mozilla.org/en-US/docs/Web/API/EyeDropper) (screen color sampling) requires Chrome 95+ or Edge 95+. All other features work in any modern browser.

## Extracting colors from a project

A Claude Code custom command is included at `.claude/commands/extract-colors.md`. Run `/extract-colors` from any project directory to scan the codebase for hex color values and generate a `spectral-colors.json` file in Spectral's group import format.
