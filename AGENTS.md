# AGENTS.md

Vanilla HTML5 canvas game. **No dependencies, no bundler, no `package.json`** — do not add tooling or libraries; keep everything in plain scripts.

## Run / verify

- Serve locally: `npx serve .` → http://localhost:3000, or open `index.html` directly in the browser (works via `file://` since there are no modules or fetch calls).
- There are **no build, test, or lint commands**. Verification is manual: load the page and check the browser console for errors plus basic gameplay (shoot, wrap edges, respawn, game over restart).

## Structure

- All game logic lives in the single `game.js`, loaded as a plain `<script>` at the end of `<body>` — **no ES modules** (no `import`/`export`); globals are shared with `index.html`.
- Canvas size is defined in **two places**: `<canvas width="800" height="600">` in `index.html` and `W`/`H` constants in `game.js`. Change both together.
- State machine in `update()`: `playing` | `dead` (respawn countdown) | `gameover` (Space restarts via `initGame()`). Keys are read from the global `keys`/`justPressed` maps; collision helpers (`dist`) expect entities with `.x`/`.y`.

## Conventions

- Comments, HUD/overlay strings, and the README are in **Spanish** — write new user-facing strings and comments in Spanish.
- Space is toroidal: all entity positions wrap via `wrap()` (except particles, which are short-lived).
- `dt` is clamped to 0.05 s to avoid big jumps after tab-switching; don't remove the clamp.
