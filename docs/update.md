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

---

## 2026-10-15 — Publishing Diagnosis & Recovery

### Root Causes Found

#### Problem 1 — Notes accidentally deleted from git

**What happened:**
Commit `21dae4b` ("notes") deleted all 21 markdown notes under `src/site/notes/Documents/`.
This occurred because a `git add .` or similar command was run after the notes had been
removed from the local working directory (files moved/deleted in Obsidian vault without
being re-copied back into this repo folder).

**Effect:** Notes removed from GitHub → Vercel rebuilt the site without them → pages disappeared from the live website.

**Fix:** Used `git checkout b2c741c -- src/site/notes/Documents/` to restore all 21 notes
from the original first commit in the git object store. No data was lost.

#### Problem 2 — New `303_Journal_kkantdev/` folder was empty

**What happened:**
The folder `src/site/notes/303_Journal_kkantdev/` existed on disk but contained no files.
Git does not track empty directories, so it was never committed or pushed.
New notes created in Obsidian for this folder were **never copied into this repository**
by the Digital Garden plugin — the sync step was skipped.

**Fix:** Added a `.gitkeep` placeholder so the folder is tracked in git.
Notes must be published from Obsidian using the Digital Garden plugin to populate this folder.

#### Problem 3 — Stray file at repo root

**What happened:**
A file literally named `h -u origin main --force-with-lease` was created at the repo root.
This happened when a git push command was mistyped in the shell and shell output
was accidentally redirected into a new file instead of executing the push.

**Fix:** Deleted the stray file before committing.

---

### How the Publishing Pipeline Works

```
Obsidian (your vault)
    ↓  Digital Garden plugin marks note with: dg-publish: true
    ↓  Plugin syncs the note file into this repo:
src/site/notes/<folder>/<note-name>.md
    ↓  You commit and push:
github.com/kkantdev/obsidian-journal-kkantdev  (main branch)
    ↓  Vercel detects the push automatically
    ↓  Vercel runs: npm install && npm run build
    ↓  Eleventy reads all .md files under src/site/notes/
dist/   ← generated static website
    ↓  Vercel serves the dist/ folder as your live website
```

---

### Correct Publishing Workflow

#### To publish a note (new or edited)

1. In **Obsidian**, open the note. The Digital Garden plugin adds to its frontmatter:
   ```yaml
   dg-publish: true
   ```
2. Click **"Publish"** in the Obsidian Digital Garden plugin — it copies/syncs the note
   into `src/site/notes/<path>/` in this repo folder on your computer.
3. In VS Code terminal (or any terminal in this project folder):
   ```bash
   git add src/site/notes/
   git commit -m "publish: <brief description of what changed>"
   git push origin main
   ```
4. Vercel detects the push and rebuilds in ~1–2 minutes. Done.

#### To publish a note in a new folder

1. Create the folder and notes in your Obsidian vault.
2. Add `dg-publish: true` to each note's frontmatter.
3. Use the Obsidian Digital Garden plugin to sync — it creates the subfolder inside
   `src/site/notes/` automatically.
4. Commit and push as above.

> **Note:** `src/site/notes/303_Journal_kkantdev/` currently contains only a `.gitkeep`
> placeholder. To put notes there, use the Obsidian Digital Garden plugin to sync notes
> from your vault into that folder. The plugin will create the `.md` files. Then commit
> and push.

#### To verify GitHub received your changes

```bash
git log --oneline -5     # confirm your commit is the latest
git push origin main     # push if not already done
```

Then visit: https://github.com/kkantdev/obsidian-journal-kkantdev
Check that your files appear under `src/site/notes/` in the repository.

#### To verify deployment

Open your live Vercel URL. If the site hasn't updated within 3 minutes of pushing,
go to Vercel Dashboard → your project → **Deployments** tab → check for build errors.

---

### Frontmatter Required for Publishing

Every note must have `dg-publish: true`. The Digital Garden Obsidian plugin sets this
automatically when you publish. Example of what the plugin generates:

```yaml
---
{"dg-publish":true,"permalink":"/documents/my-note/","tags":["mytag"]}
---
```

- `permalink` — sets the URL path on your website
- `tags: ["gardenEntry"]` — marks a note as the home page (`/`)

---

### Troubleshooting Future Publishing Failures

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Note not on website | `dg-publish: true` missing | Add it in Obsidian, re-sync with plugin |
| Note not on website | File not committed/pushed | Run `git add`, `git commit`, `git push` |
| Note not on website | Vercel build failed | Check Vercel Dashboard → Deployments |
| Notes disappeared | Accidental deletion before commit | Restore: `git checkout <commit> -- src/site/notes/` |
| Push rejected "stale info" | Remote has commits not local | Run `git fetch origin` then `git pull --rebase origin main` |
| Empty folder not tracked | Git ignores empty dirs | Add `.gitkeep` file inside the folder |
| Stray file at root | Mistyped shell command | Delete the file; do NOT commit it |

---

### Files Changed in This Recovery (2026-10-15)

| File | Action |
|------|--------|
| `src/site/notes/Documents/` (21 files) | ✅ Restored from git history |
| `src/site/notes/303_Journal_kkantdev/.gitkeep` | 🆕 Created to track new folder |
| `h -u origin main --force-with-lease` (root) | 🗑️ Deleted (stray file) |
| `docs/update.md` | ✏️ This entry added |

---

## 2026-10-15 — Fresh Start: Replace Old Notes with New Journal Folder

### Intent

Intentionally replaced the old `Documents/` note collection with a clean new `Journal/`
folder. The old notes were not wanted. This is not a recovery — it is a deliberate clean
slate.

### What Was Removed

| Folder | Notes Removed |
|--------|--------------|
| `src/site/notes/Documents/` | 21 notes (all subfolders) — permanently removed |
| `src/site/notes/303_Journal_kkantdev/` | Renamed to `Journal/` |

### What Was Created

```
src/site/notes/Journal/
├── Home.md               ← Digital Garden home page (gardenEntry / site root /)
├── Start Here.md         ← Orientation note explaining garden structure
├── Daily/.gitkeep        ← Subfolder for daily journal entries
├── Technical/.gitkeep    ← Subfolder for code, commands, how-tos
├── Projects/.gitkeep     ← Subfolder for project documentation
└── Ideas/.gitkeep        ← Subfolder for experiments and drafts
```

### Why the New Folder Works

The Digital Garden publishing system (Eleventy) reads **all** `.md` files under
`src/site/notes/` regardless of subfolder name. No configuration change was needed.
The folder name `Journal` works natively.

### How Publishing Works With the New Folder

#### From Obsidian (automatic sync)

When you publish a note using the **Obsidian Digital Garden plugin**, it syncs the note
into `src/site/notes/Journal/<your-note>.md` automatically, provided you:

1. Set the Digital Garden plugin's **"Note Folder"** to `src/site/notes/Journal` (or your chosen subfolder)
2. Add `dg-publish: true` to the note's frontmatter

Then commit and push:

```bash
git add src/site/notes/
git commit -m "publish: <description>"
git push origin main
```

Vercel rebuilds and the note appears on your live website within 1–2 minutes.

#### From VS Code / terminal (manual)

1. Create or edit a `.md` file inside `src/site/notes/Journal/` (or any subfolder)
2. Add frontmatter:
   ```yaml
   ---
   {"dg-publish":true,"permalink":"/journal/my-note/","tags":["journal"]}
   ---
   ```
3. Commit and push:
   ```bash
   git add src/site/notes/Journal/
   git commit -m "publish: my-note"
   git push origin main
   ```

### Obsidian Plugin Settings to Configure

Open **Obsidian → Settings → Digital Garden** and set:

| Setting | Value |
|---------|-------|
| GitHub repo name | `obsidian-journal-kkantdev` |
| GitHub username | `kkantdev` |
| GitHub token | *(your fine-grained Personal Access Token — see below)* |
| Note folder | `src/site/notes` *(plugin handles subfolder from vault structure)* |

**GitHub Token:** Create a fine-grained token at
`github.com → Settings → Developer settings → Personal access tokens → Fine-grained tokens`
with **Contents: Read and Write** permission on the `obsidian-journal-kkantdev` repository only.
Enter it in the plugin settings — never paste it into chat or commit it to the repo.

### Frontmatter Reference

| Frontmatter key | Purpose |
|----------------|---------|
| `"dg-publish":true` | **Required.** Marks the note for publishing. |
| `"permalink":"/journal/my-note/"` | Sets the URL on your website. |
| `"tags":["gardenEntry"]` | Makes this note the home page (`/`). Use on one note only. |
| `"tags":["journal","daily"]` | Regular tags for organization/filtering. |

### Files Changed

| File | Action |
|------|--------|
| `src/site/notes/Documents/` (21 notes) | 🗑️ Permanently removed |
| `src/site/notes/303_Journal_kkantdev/` | 🔄 Renamed to `Journal/` |
| `src/site/notes/Journal/Home.md` | 🆕 Created — Digital Garden home page |
| `src/site/notes/Journal/Start Here.md` | 🆕 Created — orientation note |
| `src/site/notes/Journal/Daily/.gitkeep` | 🆕 Created — subfolder placeholder |
| `src/site/notes/Journal/Technical/.gitkeep` | 🆕 Created — subfolder placeholder |
| `src/site/notes/Journal/Projects/.gitkeep` | 🆕 Created — subfolder placeholder |
| `src/site/notes/Journal/Ideas/.gitkeep` | 🆕 Created — subfolder placeholder |
| `docs/update.md` | ✏️ This entry added |
