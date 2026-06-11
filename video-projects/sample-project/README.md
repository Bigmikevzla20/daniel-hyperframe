# sample-project

A minimal, brand-neutral starter so the tool has a working example to model and
copy from. It's a 5-second title card using the placeholder tokens in
`../../assets/brand-tokens.css`.

## Use it

```bash
cd video-projects/sample-project
npx hyperframes lint
npx hyperframes preview          # opens Studio on http://localhost:3002
npx hyperframes render --quality draft --output renders/draft.mp4
```

## Make your own

- `cp -r ../sample-project/{hyperframes.json,meta.json} ../my-new-video/` and edit `meta.json`.
- Replace the placeholder colors/font/headline in `index.html` with your brand once you've
  defined it (see `DESIGN.md` at the repo root, and `assets/brand-tokens.css`).
- Or just run `/make-a-video` and let the skill walk you through it end to end.
