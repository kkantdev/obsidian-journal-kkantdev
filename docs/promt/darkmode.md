# ADD LIGHT / DARK MODE TOGGLE

Add a global theme toggle to the Digital Garden website.

IMPORTANT:
- First read `docs/PROJECT_MAP.md`.
- First read `docs/UI_STYLING_MAP.md`.
- Inspect the existing theme/color system before making changes.
- Use the existing Digital Garden theme functionality if available.
- Do not create a separate theme system if one already exists.
- Do not change unrelated functionality.
- Do not modify Obsidian publishing logic.
- Do not modify GitHub integration.
- Do not modify backend/data logic.
- Do not modify package.json or dependencies.
- Do not run `npm run build`.
- Do not commit or push changes.

==================================================
TOGGLE LOCATION
==================================================

Place the theme toggle on the LEFT SIDEBAR.

Place it near the bottom of the sidebar, below the folder/file tree.

It should be a compact button that fits naturally with the existing sidebar design.

Example:

    Documents
    ├── Folder
    ├── Folder
    └── Folder


                    [ ☀ / 🌙 ]

The toggle should NOT take significant space away from the file tree.

==================================================
BUTTON
==================================================

The button should have the accessible label:

"Switch theme"

Use an appropriate sun/moon icon or the project's existing icon system.

Do not use a large toggle switch.

Prefer a small, clean icon/button that matches the existing Digital Garden UI.

The button should have:

- normal state
- hover state
- active state
- keyboard focus state
- tooltip/accessibility label: "Switch theme"

==================================================
FUNCTIONALITY
==================================================

When clicked:

Dark mode → Light mode

and:

Light mode → Dark mode

The change should happen immediately without a page reload if the existing theme architecture supports it.

Use the existing Digital Garden theme system whenever possible.

Do not duplicate theme logic.

==================================================
THEME STYLING
==================================================

Make sure the toggle works correctly with the existing:

- background colors
- text colors
- sidebar colors
- borders
- links
- buttons
- code blocks
- file tree
- content area

Use the existing CSS variables/theme system.

For custom visual overrides, prefer:

`src/site/styles/user/`

Do not unnecessarily modify the core Digital Garden CSS.

==================================================
PERSISTENCE
==================================================

If the existing theme system already persists the user's selected theme, preserve that behavior.

If it does not, implement persistence only if it can be done with a minimal change that fits the existing architecture.

The selected theme should ideally remain after refreshing the website.

Do not introduce a new dependency for this.

==================================================
RESPONSIVE DESIGN
==================================================

The toggle must remain accessible on:

- desktop
- tablet
- mobile

Do not let it interfere with the existing mobile sidebar/navigation behavior.

==================================================
FINAL REPORT
==================================================

After editing, provide:

# Theme Toggle Report

## Files Changed

| File | What Changed | Why |
|------|--------------|-----|

## Toggle Location

Explain where the button was added.

## Theme System

Explain which existing theme system was used.

## Behavior

Explain:

- Dark → Light
- Light → Dark
- persistence, if supported

## Styling

Explain where the toggle styling was added.

## Accessibility

Confirm the button has the accessible label:

"Switch theme"

and is keyboard accessible.

## Functionality Preserved

Confirm that unrelated Digital Garden functionality was not changed.

## Git Status

Run:

`git status --short`

and show the result.

Do not commit or push anything.