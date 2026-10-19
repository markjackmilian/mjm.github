# Project Showcase Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a concise English project showcase and prepare its publication on GitHub Pages.

**Architecture:** Two static HTML pages share one CSS file. GitHub Pages serves the repository root from `main`; a README documents adding projects and publishing with GitHub CLI. No build or runtime JavaScript is needed.

**Tech Stack:** HTML5, CSS, Python 3 standard library for content and link checks, GitHub CLI.

**Spec:** `docs/superpowers/specs/2026-10-19-project-showcase-design.md`

## Global Constraints

- Visible content is in English; no invented claims about Toolotoolo.
- External destinations are `https://toolotoolo.com/`, `https://project-orb.it/`, `https://github.com/markjackmilian/mjm.cleaner`, and `https://buymeacoffee.com/bugbrew`.
- Show three real project cards and two non-interactive “Coming soon” cards.
- Pages work without JavaScript, use relative internal paths, and remain responsive and keyboard accessible.
- Publish from `main` and `/(root)` on GitHub Pages; do not add a build system.

## Review Focus

1. A project link from the nested cleaner page must resolve to the homepage: tested in Task 2.
2. A “Coming soon” card must not masquerade as an active link: tested in Task 1.
3. Every external link must have an `https://` destination: tested in Tasks 1 and 2.
4. Keyboard focus must be visible and reduced-motion preferences respected: checked in Task 1 CSS and browser review.
5. The site must work under a GitHub Pages repository prefix: relative URLs tested in Task 2 and checked in local preview.

---

### Task 1: Homepage and shared visual system

**Files:**
- Create: `index.html` — introduction, project grid, support section, footer.
- Create: `assets/site.css` — layout, responsive states, focus and reduced motion.
- Create: `tests/test_site.py` — standard-library HTML/link checks.
- Create: `.nojekyll` — allow GitHub Pages to serve files directly.

**Interfaces:**
- Produces `#projects` as the homepage section target, and CSS classes `.site-header`, `.project-grid`, `.project-card`, `.support`, `.site-footer` for Task 2 to reuse.

- [ ] **Step 1: Write failing homepage tests in `tests/test_site.py`.** Check that `index.html` has one `h1`, five `.project-card` articles, two “Coming soon” articles without `a` elements, links to Toolotoolo, Orbit, `projects/mjm-cleaner.html`, and Buy Me a Coffee; every external `href` begins `https://`; local links and stylesheet paths resolve to existing files. Check `.nojekyll` exists.
- [ ] **Step 2: Run `python3 -m unittest discover -s tests -v`.** Expect failures because homepage files are absent.
- [ ] **Step 3: Implement `index.html`, `assets/site.css`, and `.nojekyll`.** Use a calm light palette, a system font stack, CSS grid with desktop/tablet/mobile layouts, `:focus-visible`, and `@media (prefers-reduced-motion: reduce)`. Give placeholders a distinct passive appearance.
- [ ] **Step 4: Run `python3 -m unittest discover -s tests -v`.** Expect all Task 1 tests to pass.
- [ ] **Step 5: Commit:** `git add index.html assets/site.css .nojekyll tests/test_site.py && git commit -m "feat: add project showcase homepage"`.

### Task 2: Cleaner detail page and cross-page navigation

**Files:**
- Create: `projects/mjm-cleaner.html` — concise product detail, repository and support links.
- Modify: `tests/test_site.py` — detail-page and relative-link tests.

**Interfaces:**
- Consumes `../assets/site.css` and `../index.html#projects`; no JavaScript or shared data format.

- [ ] **Step 1: Add failing tests.** Assert the detail page has a single `h1`, mentions macOS, analysis, preview and explicit confirmation, and links to `../index.html#projects`, `../assets/site.css`, the specified GitHub repository and Buy Me a Coffee URL. Resolve each local path against the page directory and assert the target exists.
- [ ] **Step 2: Run `python3 -m unittest discover -s tests -v`.** Expect the new detail-page tests to fail.
- [ ] **Step 3: Implement `projects/mjm-cleaner.html`.** Reuse the visual system; include an accurate summary based on the local cleaner README and a clear route back to the project grid.
- [ ] **Step 4: Run `python3 -m unittest discover -s tests -v`.** Expect all tests to pass.
- [ ] **Step 5: Commit:** `git add projects/mjm-cleaner.html tests/test_site.py && git commit -m "feat: add cleaner project detail"`.

### Task 3: Publishing preparation and end-to-end verification

**Files:**
- Create: `README.md` — project editing guide and GitHub Pages publication runbook.

**Interfaces:**
- Consumes the static pages and the GitHub CLI; publishes `main` from `/(root)` when authenticated access is available.

- [ ] **Step 1: Run `gh auth status` and `git remote -v`.** Record whether the CLI can access the intended GitHub account and whether a repository already exists.
- [ ] **Step 2: Write `README.md`.** Document where to edit cards, the two placeholders, local preview, and these release steps: verify `gh auth status`; create or select a public `markjackmilian/mjm.github` repository; push `main`; enable Pages using `gh api -X POST repos/markjackmilian/mjm.github/pages -f 'source[branch]=main' -f 'source[path]=/'` if Pages is not enabled; read the actual URL using `gh api repos/markjackmilian/mjm.github/pages --jq .html_url`; confirm the live homepage and cleaner page load. If a remote with another owner/name is selected, substitute its exact identity throughout.
- [ ] **Step 3: Run tests and inspect in a browser at desktop and phone widths.** Check navigation, legibility, focus, reduced motion, and lack of horizontal overflow. Check `git diff --check` and verify the README commands against `gh` help.
- [ ] **Step 4: Commit:** `git add README.md && git commit -m "docs: prepare GitHub Pages publication"`.
- [ ] **Step 5: Publish if credentials and remote access are valid.** Use the README runbook and confirm the actual `html_url` and live pages. If `gh auth status` still reports an invalid token, report the exact authentication step needed and retain the finished local site and runbook.
