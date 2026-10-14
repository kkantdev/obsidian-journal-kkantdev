# Update Log — obsidian-journal-kkantdev

> This file records every meaningful update made to the Digital Garden website template.
> For each update it answers: **What changed? Which files? Where do you go? What do you change there?**

---

## 2026-10-14 — Copy Button + Light/Dark Mode Toggle

### Summary

Two new features were added as self-contained Garden plugins:

| # | Feature | Type | Status |
|---|---------|------|--------|
| 1 | **Copy button on every code block** | New plugin (`copy-code`) | ✅ Done |
| 2 | **Light / Dark mode toggle in sidebar** | New plugin (`theme-switcher`) | ✅ Done |
| 3 | **Plugin registry** (`plugins.json`) | New file | ✅ Done |
| 4 | **CSS additions** in `custom-style.scss` | Modified file | ✅ Done |
| 5 | **docs/** updated to reflect changes | Modified files | ✅ Done |

---

## Feature 1 — Copy Button on Code Blocks

### What was added?

Every rendered `<pre><code>` block now gets a small **"Copy"** button in its top-right corner.

- Click → copies code text to clipboard using the browser Clipboard API
- Button text changes: `Copy` → `Copied ✓` → `Copy` (resets after 2 seconds)
- Fallback textarea copy for browsers without Clipboard API support
- Fully keyboard accessible (`<button>` element, `aria-label`, `:focus-visible` ring)

### Which files were created?

```
src/plugins/copy-code/
├── garden-plugin.json          ← plugin manifest
└── templates/
    └── copyScript.njk          ← the JavaScript that adds Copy buttons
```

### Where do you go? What do you change there?

| Goal | Folder / File | What to change |
|------|--------------|----------------|
| Change button text ("Copy") | `src/plugins/copy-code/templates/copyScript.njk` | Edit `btn.textContent = "Copy"` and `btn.textContent = "Copied ✓"` |
| Change reset delay (2 s) | `src/plugins/copy-code/templates/copyScript.njk` | Edit the `2000` value in `setTimeout` |
| Restyle button (colors, size, position) | `src/site/styles/custom-style.scss` → section **COPY CODE BUTTON** | Override `.copy-code-btn` CSS rules |
| Change "Copied ✓" color (green) | `src/site/styles/custom-style.scss` → `.copy-code-btn--copied` | Change `color: #3fb950` |
| Change button position | `src/site/styles/custom-style.scss` → `.copy-code-btn` | Change `top` / `right` values |
| Disable the plugin | `src/plugins/plugins.json` | Set `"copy-code": { "enabled": false }` |

### CSS classes introduced

| Class | Location | Purpose |
|-------|----------|---------|
| `.copy-code-btn` | `custom-style.scss` | Main button style |
| `.copy-code-btn--copied` | `custom-style.scss` | Green color when "Copied ✓" is shown |

---

## Feature 2 — Light / Dark Mode Toggle

### What was added?

A **☀️ / 🌙 Switch theme** button that appears at the bottom of the left file-tree sidebar.

- Clicking it toggles between **Dark mode** (default) and **Light mode**
- The selected theme is saved in `localStorage` under the key `dg-theme`
- Theme is restored on every page load (no flash of wrong theme)
- Light mode activates by adding `data-theme="light"` to `<html>` and `<body>`
- All colors are driven by CSS custom properties — no color is hardcoded in JS

### Which files were created?

```
src/plugins/theme-switcher/
├── garden-plugin.json              ← plugin manifest
└── templates/
    ├── toggleButton.njk            ← the button HTML (sun/moon icons + label)
    └── themeScript.njk             ← the JavaScript (toggle logic + localStorage)
```

### Where does the button appear?

The button is injected into the `filetree.actions` slot — this is the area **below the site title** and **above the folder/file list** in the left sidebar. On mobile it appears inside the slide-in drawer.

### Where do you go? What do you change there?

| Goal | Folder / File | What to change |
|------|--------------|----------------|
| Change button icons (☀️ 🌙) | `src/plugins/theme-switcher/templates/toggleButton.njk` | Replace the emoji or swap in SVG/Lucide icons |
| Change button label text | `src/plugins/theme-switcher/templates/toggleButton.njk` | Edit the `<span class="theme-toggle-label">` text |
| Change aria-label / tooltip | `src/plugins/theme-switcher/templates/toggleButton.njk` | Edit `aria-label` and `title` attributes on `<button>` |
| Restyle toggle button | `src/site/styles/custom-style.scss` → section **THEME TOGGLE BUTTON** | Override `.theme-toggle-btn` rules |
| Change light mode background | `src/site/styles/custom-style.scss` → `[data-theme="light"]` block | Edit `--background-primary` |
| Change light mode sidebar color | `src/site/styles/custom-style.scss` → `[data-theme="light"]` block | Edit `--background-secondary` |
| Change light mode accent / link color | `src/site/styles/custom-style.scss` → `[data-theme="light"]` block | Edit `--text-accent` |
| Change light mode text color | `src/site/styles/custom-style.scss` → `[data-theme="light"]` block | Edit `--text-normal` |
| Change light mode heading colors | `src/site/styles/custom-style.scss` → `[data-theme="light"] h1/h2/h3/h4` | Edit each `color` value |
| Change localStorage key name | `src/plugins/theme-switcher/templates/themeScript.njk` | Edit `var STORAGE_KEY = "dg-theme"` |
| Move button location | Plugin `garden-plugin.json` → change `"filetree.actions"` to another slot | See `skills/garden-plugin-author/SKILL.md` for slot list |
| Disable the plugin | `src/plugins/plugins.json` | Set `"theme-switcher": { "enabled": false }` |

### CSS classes introduced

| Class | Location | Purpose |
|-------|----------|---------|
| `.theme-toggle-btn` | `custom-style.scss` | Toggle button container |
| `.theme-toggle-label` | `custom-style.scss` | "Switch theme" label inside button |
| `.theme-toggle-icon--dark` | `toggleButton.njk` (inline) | 🌙 icon, visible in dark mode |
| `.theme-toggle-icon--light` | `toggleButton.njk` (inline) | ☀️ icon, visible in light mode |

### Light mode variables (full list)

All of these live inside the `[data-theme="light"]` block in `src/site/styles/custom-style.scss`:

| Variable | Light Value | What it controls |
|----------|-------------|-----------------|
| `--background-primary` | `#ffffff` | Page / content background |
| `--background-secondary` | `#f5f6f8` | Sidebar and navbar background |
| `--background-primary-alt` | `#f0f2f5` | Alternate background |
| `--background-secondary-alt` | `#eaecef` | Alternate sidebar |
| `--text-normal` | `#1c2128` | Body text |
| `--text-muted` | `#57606a` | Secondary text |
| `--text-faint` | `#8c959f` | Tertiary text |
| `--text-accent` | `#0969da` | Links, active states, accents |
| `--link-color-hover` | `#1a7fd4` | Hovered link color |
| `--interactive-normal` | `#eaeef2` | Button / interactive background |
| `--interactive-hover` | `#d8dee4` | Button / interactive hover |
| `--background-modifier-border` | `#d0d7de` | Borders |
| `--background-modifier-border-hover` | `#b0bac5` | Hovered borders |
| `--dg-overlay-bg` | `rgba(240,242,245,0.88)` | Modal backdrops |

---

## Feature 3 — Plugin Registry (`plugins.json`)

### What was added?

`src/plugins/plugins.json` is the **user-owned registry** that tells the plugin loader which plugins are enabled and in what order they render.

```json
{
  "plugins": {
    "copy-code":      { "enabled": true },
    "theme-switcher": { "enabled": true }
  }
}
```

### Where do you go? What do you change there?

| Goal | File | What to change |
|------|------|----------------|
| Disable copy button | `src/plugins/plugins.json` | `"copy-code": { "enabled": false }` |
| Disable theme toggle | `src/plugins/plugins.json` | `"theme-switcher": { "enabled": false }` |
| Change render order of plugins in a slot | `src/plugins/plugins.json` | Add `"order": <number>` — lower numbers render first |

---

## CSS Additions Summary (`custom-style.scss`)

The following sections were **appended** to `src/site/styles/custom-style.scss`.
The file previously only had the dark-mode color system and layout tweaks.

| Section added | What it does |
|--------------|--------------|
| `/* COPY CODE BUTTON */` | Styles `.copy-code-btn` and `.copy-code-btn--copied` |
| `/* THEME TOGGLE BUTTON */` | Styles `.theme-toggle-btn` and `.theme-toggle-label` |
| `/* LIGHT MODE */` | `[data-theme="light"]` CSS variable overrides + heading colors + surface colors |

> **Safe to edit**: All additions are in `custom-style.scss` only.
> `style.scss` and `digital-garden-base.scss` were **not touched** (they are overwritten on template updates).

---

## Files Changed — Complete List

| File | Status | What changed |
|------|--------|-------------|
| `src/plugins/copy-code/garden-plugin.json` | 🆕 Created | Plugin manifest |
| `src/plugins/copy-code/templates/copyScript.njk` | 🆕 Created | JS copy button script |
| `src/plugins/theme-switcher/garden-plugin.json` | 🆕 Created | Plugin manifest |
| `src/plugins/theme-switcher/templates/toggleButton.njk` | 🆕 Created | Toggle button HTML |
| `src/plugins/theme-switcher/templates/themeScript.njk` | 🆕 Created | Toggle JS + localStorage |
| `src/plugins/plugins.json` | 🆕 Created | Plugin registry |
| `src/site/styles/custom-style.scss` | ✏️ Modified | Appended copy button CSS, toggle CSS, light mode CSS |
| `docs/PROJECT_MAP.md` | ✏️ Modified | Added new plugins to structure, tables, and Section 10 |
| `docs/UI_STYLING_MAP.md` | ✏️ Modified | Updated color table (dark+light), UI change guide, Section 12 |
| `docs/update.md` | 🆕 Created | This file |

---

## What Was NOT Changed

- `src/site/styles/style.scss` — untouched ✅
- `src/site/styles/digital-garden-base.scss` — untouched ✅
- `.eleventy.js` — untouched ✅
- `package.json` — untouched ✅
- All existing plugin code (`dg-filetree`, `dg-search`, etc.) — untouched ✅
- Markdown rendering / syntax highlighting — untouched ✅
- Obsidian publishing workflow — untouched ✅
- GitHub integration — untouched ✅
