# Video Workspace (Hyperframes)

A workbench for building motion-graphics videos in **plain HTML + GSAP**, powered by [Hyperframes](https://hyperframes.heygen.com). Brand and content are pulled live from two sources, so videos stay on-brand and on-message without re-entering anything.

> This is **not** a Remotion / React stack. Every composition is a regular HTML file with a paused GSAP timeline attached to `window.__timelines`. The Hyperframes CLI handles lint, preview, and render.

---

## How it works (read this first)

This workspace doesn't store the brand or the content. It **references** them from two source-of-truth repos, mapped in **`DESIGN.md`**:

- **Visual brand** (colors, type, logo) → your design system repo
- **Content, voice, research** → **Daniel's Second Brain** vault

Both are made readable to the agent via a machine-local `.claude/settings.local.json` (copy `.claude/settings.local.json.example` and fill in this machine's paths). They are **read-only** — the workspace never writes to them. See `DESIGN.md` for which file to read for each decision, and `CLAUDE.md` for the full workspace guide.

`MOTION_PHILOSOPHY.md` is the motion *discipline* (pacing, transitions, structure). Your `DESIGN.md` overrides its visual layer — headlines use your headline treatment (define it in your brand tokens / design system), not the chrome/silver one described in the motion reference.

## Prerequisites

- **Node 20+** — `node --version`
- **FFmpeg** on your `PATH`
- **Chrome (latest)** — Hyperframes renders through a headless Chromium
- **~5 GB free disk**, **16 GB RAM recommended**

Run `npx hyperframes doctor` after `npm install` — it reports what's missing.

## Quickstart

```bash
npm install

# Make the brand + Brain readable (one time, per machine):
cp .claude/settings.local.json.example .claude/settings.local.json
# ...then edit it with the absolute paths to your design system and your vault

# Open Studio on a project
cd video-projects/sample-project
npx hyperframes preview    # http://localhost:3002
```

## Make a video

Use the `/make-a-video` skill. It reads `DESIGN.md`, pulls your brand + your Brain's voice/research at the start, and only asks you about what's unique to the video. Then:

```
edit → lint → preview (Studio, live) → draft render → verify frames → final render
```

| Step | Command |
|---|---|
| Lint | `npx hyperframes lint` |
| Preview | `npx hyperframes preview` |
| Draft render | `npx hyperframes render --quality draft --output renders/draft.mp4` |
| Final render | `npx hyperframes render --quality standard --output renders/final.mp4` |

Always run the CLI from inside the project folder.

## Repo layout

```
hyperframes/
├── README.md
├── CLAUDE.md                    ← full workspace guide
├── DESIGN.md                    ← brand + Brain source map (read before any video)
├── MOTION_PHILOSOPHY.md         ← motion discipline (DESIGN.md overrides visuals)
├── AGENTS.md
├── .claude/
│   ├── settings.local.json.example   ← copy to settings.local.json, add your paths
│   └── skills/                  ← /hyperframes, /gsap, /make-a-video, /short-form-video, etc.
├── assets/                      ← shared raw media (source clips, music)
├── package.json
└── video-projects/              ← one folder per video
    └── sample-project/
```

## Claude Code skills

The `.claude/skills/` folder ships slash commands that encode framework-specific patterns:

- `/make-a-video` — end-to-end video flow (reads DESIGN.md + Brain)
- `/short-form-video` — 9:16 talking-head + motion graphics
- `/hyperframes` — authoring/editing compositions, captions, TTS, transitions
- `/hyperframes-cli` — CLI reference
- `/gsap` — GSAP animation
- `/hyperframes-registry` — install catalog blocks/components
- `/website-to-hyperframes` — turn a URL into a composition

## Troubleshooting

| Symptom | First thing to try |
|---|---|
| `npx hyperframes` not found | `npm install` in the repo root |
| Render fails mid-way | `npx hyperframes doctor` |
| Agent can't find the brand or Brain | Check `.claude/settings.local.json` has the correct absolute paths |
| Studio stuck at 0s | Hard-refresh, or load a sub-composition URL: `http://localhost:3002/?comp=<id>` |

More: `npx hyperframes docs <topic>`.

## Credits and license

- **Code and compositions** — MIT, see `LICENSE`.
- **Hyperframes** — framework © HeyGen, docs at https://hyperframes.heygen.com.
