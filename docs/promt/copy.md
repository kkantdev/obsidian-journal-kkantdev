# ADD COPY BUTTON TO CODE BLOCKS

Add a Copy function to every code block rendered by the Digital Garden website.

IMPORTANT:
- First read `docs/PROJECT_MAP.md`.
- First read `docs/UI_STYLING_MAP.md`.
- Read the repository README's CSS Customization section.
- Use `src/site/styles/user/` for the Copy button styling whenever possible.
- Do not change unrelated functionality.
- Do not change Obsidian publishing behavior.
- Do not change Markdown/code syntax highlighting.
- Do not add unnecessary dependencies.
- Do not run `npm run build`.
- Do not commit or push changes.

==================================================
FUNCTIONALITY
==================================================

Every rendered code block should have a small `Copy` button.

Example:

┌──────────────────────────────────────────────┐
│                                  [ Copy ]    │
│ #include <stdio.h>                           │
│                                              │
│ int main() {                                 │
│     printf("Hello");                         │
│ }                                            │
└──────────────────────────────────────────────┘

When the user clicks `Copy`:

1. Read only the code inside that code block.
2. Copy the exact code text to the user's clipboard.
3. Do NOT copy the `Copy` button text.
4. Preserve whitespace, indentation, and line breaks.
5. Change the button text temporarily to:
   `Copied ✓`
6. After a short delay, change it back to:
   `Copy`

Use the browser Clipboard API where appropriate:

`navigator.clipboard.writeText(...)`

Handle clipboard failure gracefully.

==================================================
CODE BLOCK REQUIREMENTS
==================================================

- Every code block should receive the Copy button automatically.
- Do not manually add buttons to individual Markdown notes.
- Do not hardcode code content.
- Do not duplicate the code block.
- Do not modify the actual code displayed.
- Do not interfere with syntax highlighting.
- Do not interfere with scrolling inside large code blocks.
- Do not interfere with text selection.
- Do not interfere with existing code-block functionality.

If the project already has a reusable code-block component or renderer, use it instead of creating a parallel implementation.

==================================================
BUTTON DESIGN
==================================================

Use the existing Digital Garden styling system.

Prefer:

`src/site/styles/user/`

for the visual styling.

The button should:

- be small and compact
- appear at the top-right of the code block
- have clear contrast against the code block
- match the existing redesigned Digital Garden UI
- have a subtle border/background
- have a hover state
- have a visible focus state
- work on desktop and mobile

Do not introduce a completely separate button design system.

==================================================
POSITIONING
==================================================

The Copy button should remain associated with its code block.

For long code blocks:

- it should not cover important code unnecessarily
- it should not break horizontal scrolling
- it should remain usable on mobile

Use the existing code-block structure where possible.

==================================================
ACCESSIBILITY
==================================================

The button must be keyboard accessible.

Use:

- a real `<button>` element where possible
- an appropriate accessible label
- visible focus styling

Do not rely only on an icon without an accessible label.

==================================================
IMPLEMENTATION RULES
==================================================

Before editing, identify:

1. Where Markdown/code blocks are rendered.
2. Whether an existing code-block component exists.
3. Whether syntax highlighting is handled by a library or existing component.
4. Where custom CSS should be placed.

Make the smallest possible implementation.

Prefer modifying the existing code-block rendering mechanism rather than creating a separate global script that unnecessarily scans the entire DOM.

==================================================
FINAL REPORT
==================================================

After making the changes, provide:

# Copy Button Implementation Report

## Files Changed

| File | Change |
|------|--------|

## Code Block Implementation

Explain where the existing code-block renderer/component was located.

## Copy Function

Explain how the code is extracted and copied.

## Button State

Explain:

`Copy` → `Copied ✓` → `Copy`

## Styling

Explain which CSS file was used and what was changed.

## Functionality Preserved

Confirm that:

- Markdown rendering was preserved
- syntax highlighting was preserved
- code content was not modified
- Obsidian publishing was not modified
- unrelated functionality was not modified

## Git Status

Run:

`git status --short`

and show the result.

Do not commit or push anything.