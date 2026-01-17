# Copilot Instructions for AgentCore Landing (concise)

## Quick summary
- This is a **small static marketing site**: primary files are `index.html` and `styles/` (no JS, no build system, no package.json). Open `index.html` in a browser or serve the folder with a static server to preview.

## Big picture & structure
- `index.html` — single-page landing content, accessible markup (roles/aria) and meta tags. Language is set (`lang="en"`).
- `styles/` — modular CSS:
  - `variables.css` (design tokens; must be loaded first)
  - `reset.css` (browser reset)
  - `layout.css` (page grids and structural rules)
  - `components.css` (buttons, cards, small UI pieces)
- `img.png` at repo root is the primary image used by the hero/how-it-works visual.

Why this matters to an agent:
- CSS order matters: `styles/main.css` imports `variables.css` first — changing the import order will break tokens and theming.
- There is no build/test infra; minimal changes should be self-contained and validated in-browser.

## Conventions and patterns (actionable)
- Keep design tokens centralized in `styles/variables.css`. To rebrand colors or spacing, update tokens here rather than editing many CSS rules.
- Add new component styles to `styles/components.css`, global layout changes go to `styles/layout.css`.
- Class names are simple hyphenated nouns (e.g., `site-header`, `feature-card`) — follow the existing naming style.
- Preserve accessibility attributes (role, aria-label) when editing markup. Many components already include roles and aria labels.

## Notable issue (must-fix example)
- In `index.html` the visual placeholder incorrectly used a file path in a `role` attribute; this has been fixed by replacing the placeholder with a proper `<img>` element:

  <img src="img.png" alt="Workflow visualization showing agent processing steps" class="how-visual-img">

  Rationale: `role` should not contain file paths; images need `alt` for accessibility and the proper element. When opening a PR for visual changes, include a screenshot and an accessibility check (axe or Lighthouse).

## How to run & test locally (simple)
- Open `index.html` in the browser directly, or run a lightweight static server (examples):
  - `python -m http.server 8000` (Python 3)
  - `npx serve .` (if `serve` is installed)
- Check responsiveness at CSS breakpoints defined in `styles/variables.css` (e.g. `--breakpoint-md: 768px`).
- Run HTML validation and an accessibility check (axe, Lighthouse) before merging visual or markup changes.

## When adding JS or tests (project currently has none)
- If adding JS, place files under a new `scripts/` folder and include via `<script src="scripts/main.js" defer></script>` at the end of `body`.
- If you introduce a build/test toolchain (e.g., Node, bundler, test framework), add a `README` section describing install/run commands and update this file with the new workflows.

## PR checklist for contributors (for Copilot or humans to follow)
- [ ] Keep `styles/main.css` import order intact (`variables`, `reset`, `layout`, `components`).
- [ ] Preserve or improve ARIA attributes and semantics (no path strings in `role`).
- [ ] Validate in at least Chrome and Firefox (mobile viewport too).
- [ ] Include screenshots for visual changes and a short description of what was changed and why.
- [ ] If adding infra (build/tests), update this file and add a short `README` with commands.

---

If anything here is unclear or you'd like additional checks (linters, CI steps, or a tests scaffold), tell me what to add and I will iterate on this file. Thank you!