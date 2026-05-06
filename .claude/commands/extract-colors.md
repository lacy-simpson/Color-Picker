# extract-colors

Scan the current project for hex color values and export them as a Spectral-compatible JSON file ready for import.

## What to scan

Search these file types for hex color values:
- **CSS / SCSS / LESS / SASS**: custom properties (`--color: #…`), variables (`$var: #…`), property values (`color: #…`, `background: #…`, `fill: #…`, `stroke: #…`, `border-color: #…`, `box-shadow: … #…`)
- **JS / TS / JSX / TSX**: string literals that are hex colors (e.g. `'#F94616'`, `"#182126"`) — common in theme files, design tokens, styled-components, CSS-in-JS
- **HTML**: inline `style="color:#…"` attribute values
- **JSON**: string values that are hex colors (e.g. theme config files, token files)

Use `grep` or `find` to locate candidate files efficiently. Search recursively from the project root, skipping `node_modules`, `.git`, `dist`, `build`, `.next`, `.nuxt`, and `coverage` directories.

## Hex color regex

Extract values matching `#[0-9A-Fa-f]{6}\b` or `#[0-9A-Fa-f]{3}\b`.

Ignore hex values that appear in:
- URL fragments / hrefs (`href="#…"`)
- HTML `id` and `class` attributes (`id="…"`)
- CSS selector context (i.e. the `#` is a selector, not a color — a color hex always follows `:`, `(`, `,`, a space after a property, or `=`)
- Code comments and strings that are clearly not colors (e.g. git SHAs — 40-char hex strings, short 1–2 char hex)

## Normalisation

- Expand 3-character shorthand to 6: `#RGB` → `#RRGGBB` (each digit doubled, e.g. `#F94` → `#FF9944`)
- Uppercase all letters
- Deduplicate globally across all files

## Output structure

Organise colors into palettes — one palette per file that contributes **2 or more** unique colors. Name each palette after the file's path relative to the project root. Skip files that contribute fewer than 2 unique colors — add those to a catch-all "Misc" palette instead (only if at least 2 misc colors exist).

Wrap all palettes in a group named after the current working directory's basename (the project name).

The output JSON must match the Spectral group import format exactly:

```json
{
  "name": "<project-name>",
  "palettes": [
    {
      "name": "<relative/file/path>",
      "colors": ["#RRGGBB", "#RRGGBB"]
    }
  ]
}
```

Sort palettes by descending color count (most colors first). Sort colors within each palette by their hue (convert to HSL, sort by H then S then L).

## Output file

Write the result to `spectral-colors.json` in the current working directory. If the file already exists, confirm with the user before overwriting.

## Summary report

After writing the file, report:
- How many files were scanned
- How many unique colors were found in total
- How many palettes were created
- The output file path
- A one-line note reminding the user how to import: open Spectral → Palettes tab → ↑ Import → JSON File → select `spectral-colors.json`
