# Personal website — Muhammad Jibran Mughal

A single, self-contained personal site for a software engineer (full-stack & automation).
Everything is in one file: `index.html` (inline CSS + JS, no build step, no dependencies).

## Files
- `index.html` — the whole site.
- `Jibran_Mughal_Resume.pdf` — linked from the "CV (PDF)" button. Keep the filename in sync with the link in `index.html` if you rename it.

## Preview locally
```sh
open index.html
# or a screenshot:
CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
"$CHROME" --headless --disable-gpu --hide-scrollbars --window-size=1280,2400 --screenshot="preview.png" "file://$PWD/index.html"
```
The Google Fonts `<link>` needs network access; everything else works offline.

## Design system (don't drift without reason)
- **Concept:** instrument panel / "now running" — he ships software that quietly runs in production. Signature elements: the interactive hero **signal waveform** (canvas) and the **"Now Running"** live-services panel.
- **Active theme:** `indigo` (dark, moody violet with a periwinkle accent). Set via the `<html data-theme="indigo">` attribute — change that one word to switch the whole site.
- **Theming is variable-driven.** All color lives in CSS custom properties. Each scheme is a `[data-theme="…"]` block near the top of the `<style>` that sets raw values (`--void`, `--panel`, `--panel-2`, `--ink-rgb`, `--mute`, `--faint`, `--line-rgb`, `--signal-rgb`, `--signal-hover`, `--on-signal`, `--live-rgb`, `--noise-rgb`, `--bar-bg`); `:root` *derives* the rest (`--signal`, `--line*`, `--live`, etc.) so a new theme is ~12 lines.
- **Six schemes are defined** (kept for easy switching): `sand` (light warm / terracotta), `sage` (light cool / forest), `ember` (dark warm / amber — homage to the original orange), `slate` (dark neutral / azure), `tidal` (dark cool / teal), `indigo` (dark / periwinkle — current).
- **Canvas colors follow the theme:** the waveform JS reads `--signal-rgb` / `--noise-rgb` / `--line-rgb` via `getComputedStyle`, so it recolors automatically with the active theme. Don't hardcode canvas colors again.
- **Type:** display "Bricolage Grotesque", body "Inter", data/labels "IBM Plex Mono".
- **Note:** the palette evolved on request — dark orange instrument panel → light orange → minimalist grey → a 6-theme picker to compare → **indigo chosen and locked in** (picker UI removed, theme system kept). The orange/instrument-panel spirit is still available via `ember`. (An earlier Nord pass was reverted as too generic.)

## Accessibility / quality floor (keep these)
- Responsive down to mobile; keyboard focus visible; decorative canvas is `aria-hidden`.
- `@media (prefers-reduced-motion: reduce)` disables the waveform animation (static frame) and transitions.

## Hero waveform interaction
Canvas `#scope`. A primary orange signal + a muted "noise" wave. On pointer move it raises a
localized bump under the cursor with a scan line, a dot on the crest, and a live mono readout;
eased with lerp so it swells/decays. Pointer listeners are skipped entirely under reduced-motion.

## Content is honest — keep it that way
Service names in "Now Running" are git-verified as actually his (kundenbilder, reklamation,
vereinskasse, caller-lookup, callcenter, ticket-triage, supplier-search, jira-insights).
Do NOT add cloned/team-owned repos. German level is A2. Study: M.Sc. ICE, TU Darmstadt (finishing early 2027).

## Deploy to GitHub Pages (next step, free)
GitHub user: `jibran137`. For a user site at `https://jibran137.github.io`:
```sh
git init
git add .
git commit -m "feat: personal website"
gh repo create jibran137.github.io --public --source=. --push   # needs: gh auth login
# then: repo Settings → Pages → Source = deploy from branch (main / root)
```
For a project site instead (`jibran137.github.io/<repo>`), create any repo name and enable Pages the same way.
A custom domain (e.g. `jibranmughal.dev`) can be added later in Settings → Pages.
