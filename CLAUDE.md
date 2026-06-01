# CLAUDE.md

Project conventions for the `gloomhaven-web` static site. Read this before making changes.

## What this is

Static HTML site hosting per-character, per-level reference guides for **Gloomhaven: Jaws of the Lion**. No build step, no JS framework — plain HTML/CSS files at the repo root.

## Hosting

- Served via GitHub Pages from `main` at https://fuzz-zone.github.io/gloomhaven-web/
- The path segment is **case-sensitive**. Repo is lowercase (`gloomhaven-web`); the URL must match.
- Deploy = push to `main`. Pages rebuilds automatically (~30s).

## File layout

All guides live at the repo root. Naming convention:

- `{character}_level_{N}.html` — level-N primer (playing the character at that level)
- `{character}_levelup_{N}.html` — level-up decision guide (which cards to take when reaching level N)
- `{character}_enhancements.html` — enhancement / perk guide (planned slot, not yet built)

Character slugs match the filename prefix (`demolitionist`, `redguard`, etc.). Use snake_case.

## index.html structure

The landing page is a list of collapsible character sections built with native `<details>` (no JS). When editing:

- One `<details class="character c-{slug}">` per character.
- All sections start collapsed (no `open` attribute by default).
- Within a section, guides are listed **reverse-level** (highest level first).
- For guides at the same level, **Decisions appear above Primer** (decisions are made when arriving at the level; the primer is for playing at it).
- Update the `.char-count` text ("N guides") whenever entries are added/removed.
- Each guide row has three columns: `.guide-level` (e.g. "Level 4"), `.guide-type` ("Primer" / "Decisions" / "Enhancements"), `.guide-desc` (one short sentence).

## Visual conventions

Per-character accent color is applied via a `c-{slug}` class on the `<details>` element. Existing palette:

- `c-demo` — `#C05000` (fire-orange), name color `#c97040`
- `c-redguard` — `#8B1A1A` (crimson), name color `#c04040`

When adding a new character, add a matching `.c-{slug} { border-left-color: ...; }` and `.c-{slug} .char-name { color: ...; }` block in the `<style>` section. Pick a color that reads against the dark `#1c1c1e` background.

## Git

- Branch: `main`. No PR workflow yet — commit directly.
- Line endings: repo is on Windows; Git warns about LF→CRLF conversion on commit. Ignore the warning.
- Commit author is set per-commit (`-c user.email=... -c user.name=...`) because no global git config has been established here.
