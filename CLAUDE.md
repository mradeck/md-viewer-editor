# CLAUDE.md
## Project
Single-file Markdown viewer/editor. Output is `md-viewer.html` — no build step.
Live: https://mradeck.github.io/md-viewer-editor/
## Versioning: Year.Push.Iteration
- Year = two-digit year (e.g. 26 for 2026)
- Push = running count of GitHub pushes in that year
- Push counter increments only at git push time; iteration resets to 1.
- Iteration counts local steps between pushes.
## On user trigger "git push" (or equivalent)
Before pushing, in this order:
1. Bump APP_VERSION in md-viewer.html (push +1, iteration = 1).
2. Add new section to CHANGELOG.md (Keep-a-Changelog format).
3. Update version header and feature list in README.md.
4. Reconcile in-code info texts (i18n.de.demoMD, i18n.en.demoMD).
5. Then git add -A && git commit && git push origin main.
6. Verify with git status afterwards.
## House style
- German for user-facing prose, third person, no direct address.
- Source comments in German, four-space indent.
- UI strings bilingual (DE/EN) via the i18n object.
- Surgical edits only — touch what was asked, leave the rest alone.
- Prefer minimal interventions (sed via osascript, str_replace) over full rewrites.
