# 大春之道线下实训营市场服务手册 Brand Refresh Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Apply the approved four-item brand refresh to the existing static GitHub Pages manual and publish it as an independent GitHub repository without changing existing functionality.

**Architecture:** Keep the existing buildless single-page `index.html` and inline data/interaction logic. Make only targeted text, CSS theme, and asset changes; validate with the repository's existing interaction checks plus a browser smoke check.

**Tech Stack:** Static HTML, inline CSS/JavaScript, PNG asset, GitHub Pages, Node.js validation scripts.

**Spec:** `docs/superpowers/specs/2026-11-12-dachun-brand-refresh-design.md`

## Global Constraints

- Keep all existing content, navigation, search, copy, tabs, and interaction behavior unchanged.
- Change the page title to `大春之道线下实训营市场服务手册`.
- Replace `assets/logo.png` with the user-provided logo image.
- Change the primary visual theme to lake blue while preserving readable contrast.
- Replace `总监思维` with `领导人思维`.
- Add `百战归来再相见！` directly below the main title.
- Publish to a new GitHub repository; do not overwrite the original repository.

## Review Focus

- Exact Chinese copy and punctuation: text assertions must pin the four requested strings and ensure the old `总监思维` label is absent from visible page markup.
- Asset replacement: the page must reference `assets/logo.png`, and the committed PNG must be the supplied logo rather than the previous multicolor mark.
- Theme consistency: primary controls, active states, accents, and focus styles should use the lake-blue palette without leaving the old blue as the primary action color.
- Interaction regression: existing structural checks must pass after the inline CSS/HTML edit.
- Independent publication: the new remote must receive the commit while the original remote remains untouched.

### Task 1: Apply the approved brand refresh

**Files:**
- Modify: `index.html:6, root CSS variables, primary color references, hero markup, thinking section labels`
- Replace: `assets/logo.png`

**Interfaces:**
- Consumes: existing single-page markup, styles, and `assets/logo.png` path.
- Produces: a static page with the requested title, subtitle, logo, lake-blue palette, and `领导人思维` copy while preserving all existing IDs and handlers.

- [ ] **Step 1: Write the failing content assertions**

  Check the current file for the exact expected strings and old label using a small PowerShell assertion command; expected failure is the old title/label being found and the new subtitle missing.

- [ ] **Step 2: Run the assertions to verify they fail**

  Run from the repository root:

  ```powershell
  $html = Get-Content -Raw index.html
  if ($html -notmatch '大春之道线下实训营市场服务手册') { throw 'new title missing' }
  if ($html -notmatch '百战归来再相见！') { throw 'subtitle missing' }
  if ($html -match '总监思维') { throw 'old label remains' }
  ```

- [ ] **Step 3: Implement the minimal refresh**

  Update only the title/hero/label text, add the subtitle immediately beneath `h1`, replace the page's primary blue palette with a lake-blue palette derived from the supplied logo, and copy the supplied PNG over `assets/logo.png`.

- [ ] **Step 4: Run content and structural checks**

  Run the content assertions above and the existing checks:

  ```powershell
  node scripts/check-interaction-structure.mjs
  python scripts/check-export-md.py
  python scripts/check-export-docx.py
  ```

  Expected: all commands exit successfully; no old visible label remains; required strings and logo path are present.

- [ ] **Step 5: Commit the implementation**

  ```powershell
  git add index.html assets/logo.png
  git commit -m "feat: refresh manual branding for dachun training camp"
  ```

### Task 2: Verify the page visually and publish independently

**Files:**
- Modify: none unless a verification-only repair is required
- Test: the committed page in a local static preview and the published GitHub Pages URL

**Interfaces:**
- Consumes: Task 1 commit and existing static GitHub Pages layout.
- Produces: an independent GitHub repository containing the verified commit and its published URL.

- [ ] **Step 1: Start a local static preview**

  Serve the repository root with a local HTTP server and inspect the hero, logo, subtitle, primary controls, navigation, and the renamed section in a browser.

- [ ] **Step 2: Run a browser smoke check**

  Confirm the page loads without console-blocking errors, the search and tab interactions still respond, and the requested visual changes are visible at desktop and narrow viewport sizes.

- [ ] **Step 3: Create and configure the independent GitHub repository**

  Use the authenticated GitHub account to create a new repository named `dachun-market-service-manual`, set it as the push target for the new publication copy, and leave the original repository untouched.

- [ ] **Step 4: Push and enable GitHub Pages**

  Push the committed `main` branch and enable Pages from the repository root on `main`; record the resulting URL.

- [ ] **Step 5: Verify the published URL**

  Open the GitHub Pages URL and confirm the same hero, logo, subtitle, lake-blue theme, and `领导人思维` label are present.
