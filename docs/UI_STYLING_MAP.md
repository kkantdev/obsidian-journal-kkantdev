# UI & Styling Map

## 1. Styling Architecture

**How Styling Works:**
- **Global CSS**: `src/site/styles/digital-garden-base.scss` (core layout and components)
- **Component CSS**: Styles embedded within component templates where needed
- **Theme CSS**: External Obsidian themes fetched via `THEME` environment variable
- **Variables**: Extensive CSS custom properties system for customization
- **CSS Custom Properties**: 100+ variables for colors, layout, typography
- **SCSS**: Source files compiled to CSS during build
- **Inline Styles**: Minimal, used for dynamic behavior
- **Utility Classes**: Component-specific classes (not a full utility system)
- **Component-level Styling**: Styles scoped to component classes

**Primary Styling Files:**
- `src/site/styles/digital-garden-base.scss` → Core layout and component styles (1000+ lines)
- `src/site/styles/style.scss` → Base theme variables and callout styles
- `src/site/styles/custom-style.scss` → **User customization file** (empty by default)
- `src/site/styles/obsidian-bases.scss` → Dataview table and card styles
- `src/site/styles/obsidian-base.scss` → Additional base styles

## 2. Color System

**Color Variables (defined in `style.scss` and `digital-garden-base.scss`):**

| Purpose | Variable/File | Current Value | Used By |
|---------|---------------|---------------|---------|
| Background Primary | `--background-primary` | `rgb(32, 31, 31)` | Page background |
| Background Secondary | `--background-secondary` | `rgb(57, 56, 56)` | Sidebars, navbar |
| Text Normal | `--text-normal` | `#dcddde` | Body text |
| Text Accent | `--text-accent` | `rgb(97, 186, 245)` | Links, accents |
| Text Muted | `--text-muted` | Inherited from theme | Secondary text |
| Text Faint | `--text-faint` | Inherited from theme | Tertiary text |
| Link Color | `--link-color` | Inherited from theme | Standard links |
| Link Color Hover | `--link-color-hover` | Inherited from theme | Link hover |
| Interactive Normal | `--interactive-normal` | Inherited from theme | Interactive elements |
| Interactive Hover | `--interactive-hover` | Inherited from theme | Interactive hover |
| Graph Node Color | `--dg-graph-node-color` | `var(--text-accent)` | Active graph nodes |
| Graph Node Color Muted | `--dg-graph-node-color-muted` | `var(--text-faint)` | Neighbor graph nodes |
| Overlay Background | `--dg-overlay-bg` | `rgba(0, 0, 0, 0.5)` | Modal backdrops |

**Heading Colors (defined in `style.scss`):**
- h1: `#ffef60` (yellow)
- h2: `#f06449` (orange-red)
- h3: `#d4fcc3` (light green)
- h4: `#72dcff` (light blue)

**Callout Colors (RGB values in `style.scss`):**
- Default/Note: `68, 138, 255` (blue)
- Abstract/Summary/TLDR: `0, 176, 255` (cyan)
- Info/Todo: `0, 184, 212` (info blue)
- Tip/Hint/Important: `0, 191, 165` (teal)
- Success/Check/Done: `0, 200, 83` (green)
- Question/Help/FAQ: `100, 221, 23` (lime green)
- Warning/Caution/Attention: `255, 145, 0` (orange)
- Failure/Fail/Missing: `255, 82, 82` (red)
- Danger/Error: `255, 23, 68` (dark red)
- Bug: `245, 0, 87` (pink)
- Example: `124, 77, 255` (purple)
- Quote/Cite: `158, 158, 158` (gray)

## 3. Typography

**Font System:**
- Font Family: Inherited from Obsidian theme (`var(--font-default)`)
- Font Files: Not specified in template - uses system/browser defaults
- Font Variables: `--font-default` from theme

**Text Sizes (CSS Variables):**
- Content Font Size: `--dg-content-font-size` (default: `18px`)
- Content Line Height: `--dg-content-line-height` (default: `1.5`)
- Note Link Size: `--dg-notelink-size` (default: `0.85rem`)
- TOC Font Size: `--dg-toc-font-size` (default: `1rem`)
- Backlinks Title Size: `--dg-backlinks-title-size` (default: `0.9rem`)
- Search Input Size: `--dg-search-input-size` (default: `0.9rem`)

**Heading Styles:** Custom colors defined in `style.scss` (see Color System)

**Links:**
- External: `.external-link` class with outgoing arrow icon
- Internal: `.internal-link` class
- Unresolved: `.is-unresolved` class for broken links

**Code Text:**
- Inline: `p > code` styled in `style.scss` (`#c7254e` text, `#1a1a1a` background)
- Blocks: Default markdown-it styling

**Metadata:** Smaller font sizes for timestamps, backlinks, etc.

**Responsive Typography:** Media queries adjust sizes for mobile

## 4. Buttons

**Search Button:**
- Location: `src/plugins/dg-search/templates/searchButton.njk`
- Styling: `src/site/styles/digital-garden-base.scss` (.search-button)
- Variables: `--dg-search-btn-*` series (radius, height, padding, etc.)
- Hover State: Theme variable `--interactive-hover`
- Active State: Not specifically defined
- Disabled State: Not specifically defined
- Mobile: Adapts to smaller screens in navbar

**Page Panel Toggle (Mobile Sidebar):**
- Location: `src/site/_includes/components/pagePanelButton.njk`
- Styling: `src/site/styles/digital-garden-base.scss` (.page-panel-toggle)
- Mobile Behavior: Shows/hides sidebar sheet on mobile

**Graph Controls:**
- Location: Graph components
- Styling: `src/site/styles/digital-garden-base.scss` (.graph-controls)
- Variables: `--dg-graph-ctrl-*` series

## 5. Navigation

**Header/Navbar:**
- File: `src/site/_includes/components/navbar.njk`
- Styling: `src/site/styles/digital-garden-base.scss` (.navbar)
- Variables: `--dg-navbar-*` series (height, title sizes, etc.)
- Logo: `.site-logo` with size variables

**Desktop Navigation:**
- File Tree: `src/plugins/dg-filetree/` plugin
- Styling: `src/site/styles/digital-garden-base.scss` (.filetree-*)
- Variables: `--dg-filetree-*` series (width, padding, gap, etc.)

**Mobile Navigation:**
- Implementation: Same sidebar with mobile media queries
- Breakpoint: `< 1400px` transforms to bottom sheet
- Styling: `src/site/styles/digital-garden-base.scss` (media queries)

**Sidebar (Right):**
- File: `src/site/_includes/components/sidebar.njk`
- Styling: `src/site/styles/digital-garden-base.scss` (.sidebar)
- Variables: `--dg-sidebar-*` series (top, gap, widths, etc.)

**Navigation Links:**
- File Tree Links: `.notelink` class styling
- Active Note: `.active-note` class with accent border

## 6. Cards and Containers

**Cards:**
- Dataview Cards: `src/site/styles/obsidian-bases.scss` (.obsidian-base-card)
- Backlink Cards: `src/site/styles/digital-garden-base.scss` (.backlink-card)
- Search Result Cards: Search plugin styling

**Note Containers:**
- Main Content: `.content` class with max-width and margins
- Canvas Pages: `.content.canvas-page` special full-width layout

**Content Containers:**
- Sidebars: `.sidebar-container`, `.filetree-sidebar`
- Graph Container: `#link-graph` with border and background

**Search Containers:**
- Search Modal: `.search-container` and `.search-box`
- Results Panel: `.search-results-panel`

**Modals:**
- Search: `.search-container.active` overlay
- Fullscreen Graph: Graph plugin implementation

## 7. Spacing and Layout

**Key Layout Variables:**
- Max Width: `--dg-content-max-width` (default: `700px`)
- Padding Top: `--dg-content-padding-top` (default: `90px`)
- Mobile Padding Top: `--dg-content-padding-top-mobile` (default: `75px`)
- Filetree Width: `--dg-filetree-width` (default: `250px`)
- Sidebar Max Width: `--dg-sidebar-max-width` (default: `350px`)
- Sidebar Gap: `--dg-sidebar-gap` (default: `80px`)
- Filetree Gap: `--dg-filetree-gap` (default: `80px`)

**Grid/Flex Usage:**
- Flexbox: Used throughout for component layouts
- Grid: Limited use (dataview cards, search layout)

**Breakpoints:**
- Mobile: `< 800px` (content adjustments)
- Tablet: `< 1000px` (filetree hiding)
- Desktop Medium: `< 1400px` (sidebar mobile transformation)
- Large Desktop: `>= 1400px` (full layout)

**Responsive Layout Rules:**
- Content centering with filetree/sidebar space calculation
- Dynamic margins based on viewport and component widths
- Mobile sidebar becomes bottom sheet

## 8. Responsive Design

**Mobile Breakpoint:** `800px`
- Navbar title shrinks
- Logo size reduces
- Content padding adjusts
- Search button simplifies

**Tablet Breakpoint:** `1000px`
- Filetree sidebar hides
- Content becomes centered
- Canvas pages adjust margins

**Sidebar Mobile Transformation:** `1400px`
- Right sidebar becomes bottom sheet
- Page panel toggle appears
- Overlay backdrop shown

**Desktop Behavior:**
- Fixed sidebars (left filetree, right sidebar)
- Centered content with dynamic margins
- Full feature set visible

**Mobile-specific Components:**
- Page Panel (mobile sidebar sheet)
- Mobile navbar with compact logo
- Bottom sheet controls

**Responsive CSS Files:** All responsiveness in `digital-garden-base.scss` via media queries

## 9. Icons

**Icon Library:** Lucide Icons
**Implementation:** `src/site/_includes/components/lucideIcons.njk`
**SVGs:** Inline SVG sprites in template
**Icon Components:** `<i data-lucide="icon-name">` elements
**Icon Styling:** `.svg-icon` class in CSS
**Icon Usage:** Throughout UI (folders, links, buttons, etc.)
**Icon Size Variables:** Multiple `--*-icon-size` variables for different contexts

## 10. Theme System

**Light/Dark Themes:** Controlled by `meta.baseTheme` in templates
**Theme Variables:** Obsidian theme CSS variables imported via `THEME` env var
**Theme Switching:** Not implemented - set by `baseTheme` at build time
**Default Theme:** Dark theme (based on CSS variable defaults)
**Theme-specific CSS:** External Obsidian theme CSS fetched and cached

**Theme Integration:**
1. `THEME` environment variable points to Obsidian theme CSS
2. `get-theme.js` fetches and caches theme
3. Theme CSS loaded alongside template styles
4. CSS variables from theme override defaults

## 11. UI Change Guide

| If you want to change... | Go here |
|---------------------------|---------|
| Website background | `custom-style.scss`: Override `--background-primary` |
| Text color | `custom-style.scss`: Override `--text-normal` |
| Accent color | `custom-style.scss`: Override `--text-accent` |
| Button appearance | `custom-style.scss`: Override `--dg-search-btn-*` variables |
| Header | `src/site/_includes/components/navbar.njk` (structure) + `custom-style.scss` (styling) |
| Sidebar | `src/site/_includes/components/sidebar.njk` (structure) + `custom-style.scss` (override `--dg-sidebar-*`) |
| Note layout | `src/site/_includes/layouts/note.njk` (structure) + `custom-style.scss` (override `--dg-content-*`) |
| Typography | `custom-style.scss`: Override `--dg-content-font-size`, `--dg-content-line-height`, etc. |
| Mobile layout | `custom-style.scss`: Add media queries or override responsive variables |
| Search UI | `src/plugins/dg-search/templates/` (templates) + `custom-style.scss` (override `--dg-search-*`) |
| Graph UI | Graph plugin templates + `custom-style.scss` (override `--dg-graph-*`) |
| Links | `custom-style.scss`: Override `--link-color`, `--link-color-hover`, `.external-link`, `.internal-link` |
| Cards | `custom-style.scss`: Override `.obsidian-base-card` or component-specific card classes |
| File tree | `src/plugins/dg-filetree/templates/` + `custom-style.scss` (override `--dg-filetree-*`, `--dg-notelink-*`) |
| Callouts | `custom-style.scss`: Override `.callout` styles and `--callout-*` variables |
| Code blocks | Theme controls most styling, override in `custom-style.scss` |
| Images | `custom-style.scss`: Override `img` styles or picture element |

## 12. Recommended Editing Strategy

**Color-only Changes:**
1. Edit `src/site/styles/custom-style.scss`
2. Override CSS variables starting with `--`
3. Test with `npm run dev`

**Typography Changes:**
1. Edit `src/site/styles/custom-style.scss`
2. Override `--dg-content-font-size`, `--dg-content-line-height`, etc.
3. Adjust heading colors if needed

**Spacing Changes:**
1. Edit `src/site/styles/custom-style.scss`
2. Override layout variables (`--dg-content-max-width`, `--dg-sidebar-gap`, etc.)
3. Consider responsive implications

**Button Changes:**
1. Edit `src/site/styles/custom-style.scss`
2. Override `--dg-search-btn-*` variables for search buttons
3. Override `.page-panel-toggle` for mobile sidebar button

**Header Changes:**
1. Edit `src/site/_includes/components/navbar.njk` for structure
2. Edit `src/site/styles/custom-style.scss` for styling
3. Override `--dg-navbar-*` variables

**Sidebar Changes:**
1. Edit `src/site/_includes/components/sidebar.njk` for structure
2. Edit `src/site/styles/custom-style.scss` for styling
3. Override `--dg-sidebar-*` variables

**Responsive Changes:**
1. Edit `src/site/styles/custom-style.scss`
2. Add media queries targeting existing breakpoints
3. Override variables within media queries

**Component Redesign:**
1. Copy component from `src/site/_includes/components/` or plugin templates
2. Modify as needed
3. Ensure CSS overrides in `custom-style.scss`
4. Test across breakpoints

**Goal:** Make the smallest possible change in the most maintainable location. Always prefer CSS variable overrides in `custom-style.scss` over template modifications when possible.
