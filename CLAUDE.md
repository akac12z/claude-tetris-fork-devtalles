# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the game

No build step. Open directly or serve statically:

```bash
open index.html
# or
python3 -m http.server 8000
```

## Architecture

Three files, no dependencies, no bundler:

- **`index.html`** — DOM structure: `<canvas id="board">` (300×600px), sidebar panel (score/lines/level/next-piece preview), and a shared overlay div for PAUSE and GAME OVER states.
- **`style.css`** — Dark/retro arcade theme. Overlay uses `backdrop-filter: blur`.
- **`game.js`** — All game logic (~305 lines, `'use strict'`, no modules).

### Key data model (`game.js`)

- `board`: `ROWS×COLS` matrix; `0` = empty, `1–7` = piece color index.
- `current` / `next`: `{ type, shape, x, y }` — `shape` is a 2D array of color indices.
- Rotation: `rotateCW` (transpose + row-reverse); `tryRotate` applies 5 wall-kick offsets `[0, -1, 1, -2, 2]`.
- Game loop: `requestAnimationFrame`-based; `dropAccum` accumulates `dt` and triggers gravity when it exceeds `dropInterval`.
- `dropInterval` formula: `max(100, 1000 − (level − 1) × 90)` ms.

### Tunable constants

| Constant | Default | Note |
|---|---|---|
| `COLS` / `ROWS` / `BLOCK` | 10 / 20 / 30 | If changed, update canvas `width`/`height` in `index.html` accordingly |
| `COLORS` | 7 hues | Index 0 = null (empty) |
| `LINE_SCORES` | `[0,100,300,500,800]` | Multiplied by current level |
