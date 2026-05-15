# Agent Knowledge Base: Gotchas & Lessons Learned

This document serves as a repository of knowledge, errors, and gotchas specific to this Hugo codebase. Other AI agents should reference this document to avoid repeating past mistakes.

## 1. Hugo Asset Mounting Priority & Silent Failures
**Issue:** Changes made to the theme's SCSS file (`themes/wallet-hugo/assets/scss/custom.scss`) were being completely ignored. The website looked like an unstyled wireframe.
**Root Cause:** There was an empty `custom.scss` file located in the root directory (`assets/scss/custom.scss`). Hugo's asset mounting system prioritizes files in the root project over the theme directory. Because the root file was empty, Hugo loaded it instead of the theme's populated SCSS file, effectively removing all custom styling.
**Lesson Learned:** Before debugging why a theme asset isn't loading, check if there is an overriding file in the root `assets/` directory. Delete or merge the root file if the theme file is intended to be used.

## 2. SCSS Compilation: `rgba()` and `currentColor`
**Issue:** `hugo server` failed to build or silently dropped SCSS compilation, throwing the error: `argument $color of rgba($color, $alpha) must be a color`.
**Root Cause:** The `currentColor` CSS keyword was passed into the SASS `rgba()` function (e.g., `rgba(currentColor, .12)`). LibSass/DartSass does not understand `currentColor` as an evaluatable color and will throw a compilation error.
**Lesson Learned:** Never use `currentColor` or other CSS-native variables inside SASS manipulation functions like `rgba()`, `lighten()`, or `darken()`. Use explicit SASS variables (e.g., `$coral`) or fallback to pure CSS implementations (e.g., `background: rgba(0, 0, 0, 0.05)`).

## 3. Bootstrap Utility Class Interference
**Issue:** The footer text was "white on white" despite custom SCSS rules being written to give the footer a dark background.
**Root Cause:** The `footer.html` partial had a hardcoded Bootstrap utility class (`bg-light`). This utility class uses `!important`, which completely overrode the custom `background: #0A0A0A;` defined in `custom.scss` for the `footer` element. Because the typography was styled for a dark background (almost white text), it became invisible against the forced white background.
**Lesson Learned:** When writing custom element-level SCSS, always audit the HTML templates for conflicting Bootstrap utility classes (like `bg-light`, `text-dark`, `border`, etc.). These utility classes often use `!important` and will silently sabotage custom CSS logic.

## 4. General Repository Context for LLMs
**Tech Stack & Tooling:**
- **Hugo Version:** Requires Hugo Extended (currently v0.123.7+) because the theme heavily relies on Hugo Pipes for SCSS compilation (`toCSS`).
- **Frameworks:** Uses Bootstrap for layouts/utilities and AOS for scroll animations. Note that some utility classes might be from an older Bootstrap version, so always check `bootstrap/_variables.scss` before assuming modern utilities like `.rounded-4` are available.

**Configuration & Content Structure:**
- **Config Directory:** Configuration is split across multiple files in `config/_default/` (e.g., `menus.de.toml`, `params.toml`) rather than a single root `config.toml`.
- **Content:** The primary site content is stored in the `content/german/` directory.

**SCSS Architecture & Pipeline:**
- **Dynamic Variables:** The SCSS pipeline is initiated in `themes/wallet-hugo/layouts/partials/style.html`. The main entry point is `style.scss`, which uses Go templating to inject Hugo config parameters directly into SASS variables (e.g., `$primary-color: {{.primary_color}}`).
- **Overriding Themes:** If you need to make changes to layouts, partials, or assets, prioritize creating the mirrored file path in the project root (e.g., `layouts/partials/...` or `assets/scss/...`) rather than modifying the `themes/wallet-hugo/` folder directly. However, be extremely careful not to create empty root files (like an empty `custom.scss`), as they will blindly override the theme files and break the site.
