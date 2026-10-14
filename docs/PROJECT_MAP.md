# Project Map

## 1. Project Overview

This is an Obsidian Digital Garden website template that works with the Digital Garden Obsidian Plugin. It's an Eleventy (11ty) static site generator project that transforms Obsidian markdown notes into a publicly accessible website.

**Main Parts:**
- **Website Generation**: Eleventy-based static site generation from Obsidian notes
- **Plugin System**: Extensible architecture for adding features via plugins
- **Theme System**: Supports Obsidian theme CSS for consistent styling
- **Build Tooling**: Node.js build process with SCSS compilation

**Difference between Obsidian plugin code and public website code:**
- **Obsidian Plugin**: Not present in this repository - this is the website template only
- **Digital Garden Website**: All code in this repository generates the public website

**Build/Development Tooling:**
- Eleventy configuration (`.eleventy.js`)
- SCSS compilation (`src/site/styles/`)
- Node.js build scripts (`package.json`)

**Deployed Website Components:**
- Generated static files in `dist/` directory
- CSS compiled from SCSS sources
- Plugin JavaScript and templates

## 2. Repository Structure

```
obsidian-digital-garden/
├── .eleventy.js                    # Eleventy configuration
├── .env.example                    # Environment variables template
├── netlify.toml                    # Netlify deployment config
├── vercel.json                     # Vercel deployment config
├── package.json                    # Node.js dependencies and scripts
├── plugin-info.json               # Plugin metadata
├── README.md                      # Project documentation
├── src/
│   ├── helpers/                   # Utility functions
│   │   ├── basesPlugin.js         # Bases (dataview) plugin
│   │   ├── constants.js          # Constants and defaults
│   │   ├── filetreeUtils.js      # File tree utilities
│   │   ├── linkUtils.js          # Link resolution utilities
│   │   ├── pluginLoader.js       # Plugin loading system
│   │   └── utils.js              # General utilities
│   ├── plugins/                   # Built-in + custom plugins
│   │   ├── dg-filetree/          # File tree sidebar
│   │   ├── dg-link-preview/      # Link preview functionality
│   │   ├── dg-math/              # Math equation support
│   │   ├── dg-search/            # Full-text search
│   │   ├── dg-timestamps/        # Note timestamps
│   │   ├── copy-code/            # ✨ NEW: Copy button for code blocks
│   │   │   ├── garden-plugin.json
│   │   │   └── templates/copyScript.njk
│   │   ├── theme-switcher/       # ✨ NEW: Light/Dark mode toggle
│   │   │   ├── garden-plugin.json
│   │   │   └── templates/ (toggleButton.njk, themeScript.njk)
│   │   └── plugins.json          # ✨ NEW: Plugin registry (enables plugins)
│   └── site/                     # Website source
│       ├── _data/                # Eleventy data files
│       ├── _includes/            # Templates and components
│       │   ├── components/       # UI components
│       │   └── layouts/          # Page layouts
│       ├── notes/                # Obsidian notes (content)
│       ├── styles/               # CSS/SCSS styling
│       ├── get-theme.js          # Theme fetching script
│       ├── index.njk             # Home page template
│       ├── note.njk              # Note page template
│       └── graph.njk             # Graph visualization page
├── docs/                          # Documentation (created)
├── img/                          # Images and assets
├── skills/                       # AI agent skills
└── .kilo/                        # Kiro workspace configuration
```

## 3. Important Files

| File | Purpose | Affects Public Website? | Safe Area for UI Changes? |
|------|---------|-------------------------|----------------------------|
| `src/site/styles/custom-style.scss` | Custom CSS overrides | Yes | **YES** - Primary location for UI changes |
| `src/site/styles/style.scss` | Base styling with CSS variables | Yes | NO - Will be overwritten on updates |
| `src/site/styles/digital-garden-base.scss` | Core layout and component styles | Yes | NO - Will be overwritten on updates |
| `src/site/_includes/components/navbar.njk` | Navigation bar component | Yes | Yes - For navbar structure changes |
| `src/site/_includes/components/sidebar.njk` | Right sidebar component | Yes | Yes - For sidebar layout changes |
| `src/site/_includes/layouts/note.njk` | Note page layout | Yes | Yes - For page structure changes |
| `src/site/_includes/layouts/index.njk` | Home page layout | Yes | Yes - For homepage changes |
| `src/plugins/dg-search/templates/` | Search UI templates | Yes | Yes - For search UI modifications |
| `src/plugins/dg-filetree/` | File tree plugin | Yes | Yes - For file tree UI changes |
| `src/plugins/copy-code/` | ✨ NEW Copy button plugin | Yes | Yes - Edit `templates/copyScript.njk` for JS behavior |
| `src/plugins/theme-switcher/` | ✨ NEW Light/Dark mode toggle plugin | Yes | Yes - Edit templates or CSS variables |
| `src/plugins/plugins.json` | ✨ NEW Plugin registry | Yes | Yes - Enable/disable/order plugins here |
| `.eleventy.js` | Eleventy configuration | Yes | NO - Build configuration, not UI |
| `package.json` | Dependencies and scripts | Indirectly | NO - Build tooling only |

## 4. Website Architecture

**Flow:**
1. **Obsidian** → User writes notes in Obsidian with Digital Garden plugin
2. **Digital Garden Plugin** → Publishes notes to Git repository
3. **GitHub** → Repository contains notes and this template
4. **Build Process** → Eleventy generates static website from notes
5. **Website** → Static files served via Vercel/Netlify
6. **Vercel/Netlify** → Hosting platform for deployment

**Website Generation Files:**
- `src/site/notes/` → Source markdown files
- `src/site/_includes/` → Templates and layouts
- `src/site/styles/` → Styling
- `src/plugins/` → Feature extensions
- `dist/` → Generated output (not in repository)

## 5. UI Component Map

| UI Element | File/Folder | Main Purpose |
|------------|-------------|--------------|
| Header/Navbar | `src/site/_includes/components/navbar.njk` | Main website header with logo and actions |
| Navigation (Filetree) | `src/plugins/dg-filetree/` | Left sidebar file tree navigation |
| Sidebar (Right) | `src/site/_includes/components/sidebar.njk` | Right sidebar with TOC, backlinks, graph |
| Mobile Navigation | `src/site/_includes/components/sidebar.njk` (media queries) | Mobile sidebar sheet |
| Search Interface | `src/plugins/dg-search/templates/` | Search modal and results |
| Search Button | `src/plugins/dg-search/templates/searchButton.njk` | Search trigger buttons |
| Note/Page Layout | `src/site/_includes/layouts/note.njk` | Individual note page structure |
| Note Title | `src/site/_includes/layouts/note.njk` | Note title display in header |
| Note Content | `src/site/_includes/layouts/note.njk` (content section) | Main note content area |
| Tags | `src/site/_includes/layouts/note.njk` (header-meta section) | Note tags display |
| Backlinks | `src/site/_includes/components/sidebar.njk` | Backlinks section in sidebar |
| Local Graph | `src/site/_includes/components/graphScript.njk` | Local graph visualization |
| Global Graph | `src/site/graph.njk` | Full graph visualization page |
| File Tree | `src/plugins/dg-filetree/` | Left sidebar file navigation |
| Table of Contents | `src/site/_includes/components/sidebar.njk` (toc section) | Auto-generated TOC |
| Footer | `src/site/_includes/components/references.njk` | Page references and citations |
| Buttons | `src/site/styles/digital-garden-base.scss` (search-btn, etc.) | Button styling throughout |
| Links | `src/site/styles/digital-garden-base.scss` (external-link, internal-link) | Link styling |
| Cards | `src/site/styles/obsidian-bases.scss` (obsidian-base-card) | Card components for dataview |
| Callouts | `src/site/styles/style.scss` (.callout) | Callout/alert styling |
| Code Blocks | Default Eleventy/markdown-it | Code syntax highlighting |
| **Copy Button** ✨ | `src/plugins/copy-code/templates/copyScript.njk` | Copy-to-clipboard button on every code block |
| Images | `src/site/styles/digital-garden-base.scss` (img rules) | Image styling and optimization |
| Modal/Dialog | `src/site/styles/digital-garden-base.scss` (search-container) | Search modal overlay |
| Menus/Dropdowns | Not identified during repository analysis | |
| Icons | `src/site/_includes/components/lucideIcons.njk` | Lucide icon system |
| **Theme Toggle** ✨ | `src/plugins/theme-switcher/templates/toggleButton.njk` | Light/Dark mode button in left sidebar |
| Responsive Behavior | Media queries throughout `digital-garden-base.scss` | Mobile/tablet adaptations |

## 6. Feature → File Map

**Feature Locations:**
- **Search** → `src/plugins/dg-search/` (templates and JavaScript)
- **Graph** → `src/site/_includes/components/graphScript.njk` (local) + `src/site/graph.njk` (global)
- **Backlinks** → `src/site/_includes/components/sidebar.njk` (backlinks section)
- **File Tree** → `src/plugins/dg-filetree/` (plugin with templates)
- **Theme** → `src/site/styles/` (CSS variables in `digital-garden-base.scss`)
- **Navigation** → `src/site/_includes/components/navbar.njk` + `src/plugins/dg-filetree/`
- **Math Support** → `src/plugins/dg-math/` (MathJax integration)
- **Timestamps** → `src/plugins/dg-timestamps/` (note date display)
- **Link Previews** → `src/plugins/dg-link-preview/` (hover previews)
- **Copy Button** ✨ → `src/plugins/copy-code/` (JS injected via `common.footer` slot)
- **Light/Dark Toggle** ✨ → `src/plugins/theme-switcher/` (toggle in `filetree.actions` slot, CSS in `custom-style.scss`)

## 7. Safe Editing Areas

**Intended for UI Changes:**
- `src/site/styles/custom-style.scss` → **PRIMARY** location for CSS customizations
- `src/site/_includes/components/` → Component template modifications
- `src/site/_includes/layouts/` → Page layout changes
- `src/plugins/[plugin-name]/templates/` → Plugin UI templates

**Intended for CSS Changes:**
- `src/site/styles/custom-style.scss` → Override CSS variables and add custom styles

**Intended for Theme Changes:**
- Environment variable `THEME` → External Obsidian theme URL
- `src/site/styles/custom-style.scss` → CSS variable overrides

**Intended for Component Changes:**
- `src/site/_includes/components/` → Nunjucks template components
- `src/plugins/[plugin-name]/templates/` → Plugin-specific components

**Intended for Website Layout Changes:**
- `src/site/_includes/layouts/` → Page layout templates
- `src/site/_includes/components/` → Layout components

**Intended for Typography:**
- `src/site/styles/custom-style.scss` → Override `--dg-content-font-size` and related variables

**Areas to Generally Avoid for Simple Visual Changes:**
- `src/site/styles/style.scss` → Will be overwritten on template updates
- `src/site/styles/digital-garden-base.scss` → Will be overwritten on template updates
- `.eleventy.js` → Build configuration, not UI
- `src/helpers/` → Utility functions, not UI
- `src/plugins/[plugin-name]/index.js` → Plugin logic, not templates

## 8. Build and Deployment

**Package Manager:** npm (Node.js)
**Install Command:** `npm install`
**Development Command:** `npm run dev` (starts Eleventy dev server with SCSS watch)
**Production Build Command:** `npm run build` (builds Eleventy site and compiles SCSS)

**Build Scripts (package.json):**
- `dev` → Development server with watch modes
- `build` → Production build
- `build:sass` → SCSS compilation
- `get-theme` → Fetches external Obsidian theme
- `test` → Runs Vitest tests

**Vercel Configuration:** `vercel.json`
**Netlify Configuration:** `netlify.toml`

**Generated Files:**
- `dist/` → Built website (not tracked in git)
- `dist/styles/` → Compiled CSS
- `dist/img/optimized/` → Optimized images

**Important Environment Variables:**
- `THEME` → URL to Obsidian theme CSS (optional)
- `ELEVENTY_ENV` → `dev` or `prod` environment
- `NOTE_ICON_DEFAULT` → Default note icon

## 9. Important Warnings

1. **Generated Files**: `dist/` directory is build output - do not edit directly
2. **Build Output**: Files in `dist/` are regenerated on each build
3. **Plugin Code vs Website Code**: All code in this repository is for website generation only
4. **Files That Should Not Be Edited Directly:**
   - `src/site/styles/style.scss` → Marked as overwritten on updates
   - `src/site/styles/digital-garden-base.scss` → Marked as overwritten on updates
5. **Dependencies**: Plugin system allows third-party plugins - only install from trusted sources
6. **Configuration Files**: `.eleventy.js` contains build logic - changes may break generation
7. **Paths Overwritten During Builds:**
   - `dist/` directory completely regenerated
   - `src/site/styles/_theme.*.css` → Generated theme cache files
8. **CSS Variables**: Extensive CSS variable system in `digital-garden-base.scss` - override in `custom-style.scss`

## 10. Recent Additions (2026-10-14)

### Copy Button Plugin (`src/plugins/copy-code/`)
- Adds a **Copy** button to every `<pre><code>` code block automatically
- Button appears top-right, styled with existing CSS variables
- Uses `navigator.clipboard.writeText()` with textarea fallback
- State: `Copy` → `Copied ✓` → `Copy` (2 s delay)
- Injected via `common.footer` slot (no template edits needed)
- Enabled in `src/plugins/plugins.json`

### Light / Dark Mode Toggle Plugin (`src/plugins/theme-switcher/`)
- Adds a **☀️ / 🌙 Switch theme** button at the bottom of the left file-tree sidebar
- Toggles `data-theme="light"` attribute on `<html>` / `<body>`
- Full light-mode CSS variable overrides in `custom-style.scss` under `[data-theme="light"]`
- Persists user preference in `localStorage` key `dg-theme`
- Theme applied before DOMContentLoaded to prevent flash of wrong theme
- Button injected via `filetree.actions` slot; script via `common.footer` slot
- Enabled in `src/plugins/plugins.json`

### Plugin Registry (`src/plugins/plugins.json`)
- Created for the first time; controls which plugins are enabled and their render order
- To disable a plugin: set `"enabled": false` for its entry