# DESIGN.md — Brand & Knowledge Sources

> **This file is the source map for every video in this workspace.** It tells the
> agent where your brand (colors, type, logo) and your content/voice come from.
>
> Brand and content are **not copied** into this repo. They are **referenced** from
> their source-of-truth locations so updates flow through automatically. Read from
> these sources at the start of every video — see `make-a-video` Gate 2 (script/voice)
> and Gate 3 (style).

> **PLACEHOLDER STATE:** This copy ships with no brand wired up. Until you point the
> two sources below at real locations, the tool falls back to the neutral
> `assets/brand-tokens.css` placeholder + the `MOTION_PHILOSOPHY.md` defaults. Fill
> these in when you're ready — nothing here assumes a specific brand.

## Access (per machine, set once)

Both sources are made readable to the agent via **`.claude/settings.local.json`**
(gitignored, machine-local). It lists the real local paths to the two folders under
`permissions.additionalDirectories`. Copy `.claude/settings.local.json.example`, fill in
this machine's paths, and the agent can read both. Because paths live in that local file,
nothing here hardcodes a location — always find a source by its signature file (below).

## Two sources of truth (both READ-ONLY)

### 1. Visual brand → your design system *(optional — placeholder until set)*

- **Repo / folder:** your own design-system or brand-kit folder, if you have one. Add it
  as a Claude Code working directory (see `.claude/settings.local.json`) and locate it by
  a signature file at its root (e.g. a `colors_and_type.css` or `tokens.css`). Do not
  assume a fixed path.

Read these for any visual decision — colors, type, logo:

| Read this | For |
|---|---|
| your color/type token file | Canonical color tokens + type scale. **Never hardcode brand colors — read them here.** |
| your brand/usage doc | Full visual guidance and usage rules |
| your fonts folder | The actual typeface files the renderer needs |
| your logo assets | Logomarks (light + dark backgrounds) |

**No design system yet?** Use the neutral placeholders in `assets/brand-tokens.css` and
let the user supply per-video colors/fonts/logo, or fall back to `MOTION_PHILOSOPHY.md`
defaults. Define your own headline treatment (e.g. a text gradient) in your brand tokens —
there is intentionally no brand gradient baked in here.

### 2. Content, voice & research → Daniel's Second Brain

- **Repo:** Daniel's live Obsidian vault — the single source of truth for content/voice (never copied)
- **Where it is:** the real vault on this machine, added as a **read-only** Claude Code working directory (see `.claude/settings.local.json`). Locate it among your working directories by its signature file **`knowledge/_index.md`**. Do not assume a fixed path, and never write to it.

Read these for content and voice decisions:

| Read this | For |
|---|---|
| `knowledge/concepts/brand-voice.md` | Voice + tone (how Daniel sounds) |
| `knowledge/concepts/script-structure.md` | How scripts are shaped |
| `knowledge/concepts/video-type-playbook.md` | Per-video-type conventions |
| `projects/video-production/` | Existing scripts (`scripts/`), state, and plan |
| `knowledge/_index.md` | Catalog → follow to relevant research pages (`companies/`, `people/`, `tools/`) |

## Rules

1. **Read-only.** Never write to either source from this workspace.
2. **Reference, don't copy.** Read the live files each build. The *only* things copied
   in are the binary font + logo files the renderer physically needs — copied from your
   design-system source (or supplied per-video) into a project's `assets/` at build time.
3. **Updates propagate.** When the brand or the brain changes, `git pull` that source
   and the specs flow through automatically. Re-copy font/logo files only if those
   binaries themselves changed.
4. **Fallback.** Use the `MOTION_PHILOSOPHY.md` / `house-style.md` / `brand-tokens.css`
   defaults only for things neither source specifies. Your `DESIGN.md` sources override
   the visual layer; keep MOTION_PHILOSOPHY's motion *discipline* (pacing, transitions,
   structure).
