# README Showcase Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Redesign all four user READMEs around shared English application visuals and a clearer first-time-user reading path.

**Architecture:** Build a disposable RPG Maker fixture and run the compiled Electron application offscreen with an isolated `userData` directory, following the established pattern in `tests/electron-smoke.cjs`. Compose two shared PNGs from those real English UI captures, then rewrite the English README as the canonical structure and mirror its meaning in Traditional Chinese, Simplified Chinese, and Japanese.

**Tech Stack:** Markdown, PNG, Electron offscreen capture, Sharp

**Spec:** `docs/superpowers/specs/2026-11-05-readme-showcase-design.md`

## Global Constraints

- Do not change application behavior, dependencies, historical handoff files, or `INTEGRATION_MANIFEST.json`.
- Shared images contain English UI only and must be referenced by every language.
- Application UI inside screenshots must remain factual and legible.
- Never load the user's normal R-aW catalog; set an isolated Electron `userData` path before importing the compiled main process.
- Keep every disposable fixture, raw capture, script, and profile beneath `.superpowers/sdd/2026-11-05-readme-showcase/`.
- Bump the completed batch from 0.5.12 to 0.5.13, commit, and push `main` to `origin`; do not tag or publish a Release.

## Review Focus

- Screenshot content must not expose absolute paths, private game assets, personal information, or test-only claims presented as user content.
- The capture bootstrap must set the isolated `userData` path before loading `out/main/index.js`; otherwise it could expose the normal project catalog.
- Cleanup must resolve and boundary-check its targets before removing only the disposable workspace.
- Image links must resolve correctly from both the root README and `docs/user/` READMEs.
- Safe workflow wording must keep selection separate from deployment.
- Project deletion wording must say that game files remain in their current state.
- Release wording must not imply that 1.0 or a downloadable package has been published.

---

### Task 1: Capture and produce the shared visuals

**Files:**
- Temporary: `.superpowers/sdd/2026-11-05-readme-showcase/demo-game/`
- Temporary: `.superpowers/sdd/2026-11-05-readme-showcase/demo-user-data/`
- Temporary: `.superpowers/sdd/2026-11-05-readme-showcase/raw-captures/`
- Temporary: `.superpowers/sdd/2026-11-05-readme-showcase/capture-readme.cjs`
- Create: `docs/user/images/readme-overview.png`
- Create: `docs/user/images/readme-safe-workflow.png`

**Interfaces:**
- Consumes: `out/main/index.js`, `tests/electron-capture.cjs`, the isolation pattern in `tests/electron-smoke.cjs`, `resources/icon.png`, product rules in the spec
- Produces: two repository-local PNG assets referenced by Task 2

- [ ] **Step 1: Build the current application and prepare the isolated workspace**

Run `npm run native:electron` and `npm run build`. Resolve the disposable workspace as `<repo>/.superpowers/sdd/2026-11-05-readme-showcase/`; abort if any temporary target resolves outside it.

- [ ] **Step 2: Create the Moonlit Archive fixture**

Create the minimum RPG Maker MZ structure under `demo-game/` (`js/rmmz_core.js`, `data/System.json`, and `img/pictures/`). Populate it only with newly generated neutral fantasy-environment PNGs: no people, logos, text, or third-party game material. Use the project name `Moonlit Archive` and generic filenames such as `moonlit-library.png`, `crystal-garden.png`, and `sky-ruins.png`.

- [ ] **Step 3: Write and inspect the disposable offscreen capture runner**

In `capture-readme.cjs`, import Electron, replace `BrowserWindow` with an offscreen hidden window, call `app.setPath('userData', <demo-user-data>)` before requiring `out/main/index.js`, force locale `en`, create and scan only the Moonlit Archive fixture, and exercise import, version selection, apply confirmation, and restore states. Write raw captures only to `raw-captures/` and log all resolved fixture/profile/output paths.

- [ ] **Step 4: Prove isolation before accepting any capture**

Verify the runner log shows every disposable path beneath the plan workspace, the catalog contains exactly one project named `Moonlit Archive`, and no normal user-data path or pre-existing project name appears in the captured DOM text.

- [ ] **Step 5: Compose the two final PNGs deterministically with Sharp**

Create `readme-overview.png` from the English workbench and asset-detail captures. Create `readme-safe-workflow.png` as a four-stage sequence: fixed original → import replacement → select version → confirm apply/restore. Keep captured UI pixels unaltered; limit additions to English labels, arrows, crop, background, and the existing icon.

- [ ] **Step 6: Inspect both final PNGs**

Decode both files with Sharp and verify dimensions, readable text, no clipped controls, no fabricated UI, no absolute paths, and practical GitHub README dimensions. Visually inspect both images before Task 2.

### Task 2: Rewrite the four user READMEs

**Files:**
- Modify: `README.md`
- Modify: `docs/user/README.zh-TW.md`
- Modify: `docs/user/README.zh-CN.md`
- Modify: `docs/user/README.ja.md`

**Interfaces:**
- Consumes: `docs/user/images/readme-overview.png`, `docs/user/images/readme-safe-workflow.png`
- Produces: four equivalent user-facing entry points

- [ ] **Step 1: Rewrite the English canonical README**

Use this section order: value proposition, overview visual, key capabilities, download/run, safe workflow visual and steps, safety rules, compatibility/limits, project status, reporting, license.

- [ ] **Step 2: Mirror the structure and meaning in all three translations**

Reference the same English PNGs. Preserve technical values, safety semantics, and legal wording; translate prose, headings, and alt text.

- [ ] **Step 3: Check document structure and links**

Run a local Markdown link/image target check and compare headings and numeric constraints across all four files.

### Task 3: Version, release notes, and final verification

**Files:**
- Modify: `package.json`
- Modify: `package-lock.json`
- Modify: `docs/development/INDEX.md`
- Modify: `docs/CHANGELOG.md`
- Create: `docs/UPDATE_0.5.13.md`

**Interfaces:**
- Consumes: completed visuals and README rewrite
- Produces: a consistent 0.5.13 documentation batch and local commit

- [ ] **Step 1: Set all current-version references to 0.5.13**

Update both root package-lock version fields, all four READMEs, and the development index.

- [ ] **Step 2: Record the batch**

Add `docs/UPDATE_0.5.13.md` and a top changelog row dated 2026-11-05 describing the shared English showcase images and four-language README restructuring.

- [ ] **Step 3: Run documentation-focused verification**

Check image dimensions and PNG decoding, Markdown targets, four-language version references, `git diff --check`, and the exact changed-file list. Confirm that no file beneath `.superpowers/` is staged. Run broader build/tests only if application code or build-affecting configuration changed; the capture build from Task 1 may be reused if sources remain unchanged.

- [ ] **Step 4: Clean the disposable capture workspace safely**

Resolve `demo-game/`, `demo-user-data/`, `raw-captures/`, and `capture-readme.cjs`; remove them only after confirming that each target is beneath `.superpowers/sdd/2026-11-05-readme-showcase/`. Keep the ignored progress ledger until final review is complete.

- [ ] **Step 5: Commit the verified batch**

Commit only the files in this plan with a message that describes the README showcase refresh and includes version 0.5.13.

- [ ] **Step 6: Push the committed batch**

Confirm `git status --short` is clean and `HEAD` is the new 0.5.13 commit, then push the current `main` branch to `origin`. Verify that `origin/main` resolves to the same commit. Do not tag or publish a Release.
