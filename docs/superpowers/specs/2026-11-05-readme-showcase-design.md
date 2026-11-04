# README Showcase Redesign

## Intent

Make the repository landing page easier for a first-time RPG Maker MV/MZ user to understand and trust. English is the canonical README; Traditional Chinese, Simplified Chinese, and Japanese keep equivalent copy while reusing the English screenshots.

## Goals

- Lead with the product's purpose and the safe replacement workflow.
- Show the real application instead of asking readers to infer it from prose.
- Separate getting started, safety rules, compatibility limits, and project/legal information.
- Keep all four README languages aligned without producing four image sets.

## Non-goals

- No application UI or behavior changes.
- No invented screens, features, release availability, or validation claims.
- No localization of text inside screenshots.
- No change to historical handoff documents or `INTEGRATION_MANIFEST.json`.

## Approach

Use real English application screens as the factual center of the visuals. The capture session must run against a generated RPG Maker fixture and a separate Electron `userData` directory, using the same `app.setPath('userData', ...)` isolation pattern already established by `tests/electron-smoke.cjs`. It must never load the user's normal project catalog.

The generated fixture is named **Moonlit Archive** and contains only neutral, newly generated fantasy-environment PNGs with no people, logos, copyrighted game material, personal paths, or text baked into the art. Fixture files, isolated application data, raw captures, and capture automation live only under `.superpowers/sdd/2026-11-05-readme-showcase/` and are removed after the final PNGs pass inspection.

Create one wide overview image for the README opening and one compact workflow image that explains fixed original, import, version selection, confirmation, and apply/restore. Compose the images deterministically from unmodified offscreen Electron captures; decorative framing is limited to background, crop, labels, arrows, and the existing R-aW icon. Final application controls and UI text must remain legible and materially unaltered.

Rewrite each README around the same reader path: product value, visual overview, key capabilities, download/run, safe workflow, three safety rules, compatibility/limits, project status, problem reporting, and license. Keep detailed warnings, but move them behind clear headings and concise summaries instead of presenting every topic at equal weight.

## Constraints

- English image assets are shared by all four languages.
- Static PNG assets only; use repository-relative links that work on GitHub.
- Do not open, read, rename, delete, or display any project from the user's normal R-aW catalog.
- The capture runner must call `app.setPath('userData', <isolated path>)` before loading `out/main/index.js`.
- All disposable paths must resolve beneath `.superpowers/sdd/2026-11-05-readme-showcase/`; cleanup must validate that boundary before removal.
- Final images must not contain an absolute filesystem path, personal name, private game title, third-party game asset, or test-only claim presented as user data.
- Preserve the fixed-original, staged-versus-deployed, external-change blocking, and deletion semantics exactly.
- Keep the unreleased/validation status explicit and do not imply a downloadable release exists when none is present.
- Complete the batch as version 0.5.13, commit it, and push the current `main` branch to `origin`; do not tag or publish a Release.

## Success criteria

- A reader can identify what the tool does, its core safety model, and how to start from the first screenful.
- Both showcase images display correctly from all four README locations.
- The capture log proves that `userData`, fixture, and raw capture paths were inside the isolated workspace and that normal application data was not opened.
- The committed images contain only the English UI and generated Moonlit Archive content, with no absolute paths or private material.
- The four documents have matching section intent and no contradictory product claims.
- Version references and release notes consistently identify 0.5.13.
