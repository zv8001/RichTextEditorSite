# Editor bug fixes

Updated the standalone index.html after repeated source and browser checks.

## Fixed
- Formatting is applied only to the selected characters. Partial small-caps removal and repeated color/font changes preserve surrounding text.
- Styles can be chosen at a caret for subsequent typing, including composed text input.
- Font dropdowns preserve selection and keyboard focus.
- Undo/redo covers typing, deletion, formatting, imports, and Clear (Ctrl/Cmd+Z; Ctrl+Y or Ctrl/Cmd+Shift+Z for redo). History holds 200 edit states.
- Real trailing and consecutive newlines are retained; the visual caret sentinel is excluded from export.
- XML import uses a parser, decodes entities once, accepts single-quoted attributes, and retains whitespace.
- Malformed or unsupported imports show an error and preserve the existing document.
- Font weight, stroke thickness/transparency/joins/sizing, and nested transparency survive export/import.
- Preview elements are constructed safely, with attribute values escaped in XML export.
- Plain-text paste avoids importing arbitrary HTML. HTML drag/drop is disabled.
- Alpha zero, 8-digit hex colors, opaque replacements, and numeric color bounds work.
- Character count uses decoded Unicode code points rather than XML entity length.
- Clipboard rejection has a fallback and a visible error message.
- Color popup positioning, touch dragging, modal Escape, focus trapping, and small-screen layout are handled.

## Verification
36 regression checks passed in both installed Chrome and Edge. The suite includes a deterministic 180-step randomized editing/DOM/XML round-trip check and composed input through the browser's input protocol. Browser runtime-error checks passed.

Run locally with Node.js:
    node bug-checks.cjs

The test script uses Playwright from this machine's bundled Codex runtime and launches installed Chrome. Set EDITOR_TEST_BROWSER to an Edge executable path to test Edge.

## Scope
The browser preview is approximate: Roblox fonts and stroke joins can differ from the browser. Actual rendering in Roblox Studio was not tested. This remains a single HTML application with no build or runtime dependency beyond a browser; fonts load from Google Fonts with local fallbacks.
