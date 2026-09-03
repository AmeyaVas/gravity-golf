# Gravity Golf

A tiny physics mini-golf game. One file, no build, no dependencies —
double-click `index.html` to play in any browser.

## How to play

- **Drag back from the ball and release** to putt (slingshot style).
  The dotted line previews your path; the ring around the ball shows power.
- Planets **pull** the ball with real gravity — bank shots off their wells,
  slingshot around them, or hit one dead-on and bounce straight back.
- **Suns** (orange) burn the ball up — you respawn at your last resting spot,
  losing the stroke.
- **Repulsors** (purple) push the ball away instead of pulling.
- Get the ball into the cup moving slowly enough and it drops. Fewest strokes wins.
- 9 hand-made holes, par tracked against the field.

## Getting around

- **Hole selector** — the numbered row under the scoreboard. A hole unlocks once
  you reach it, so you can jump back to any hole you have played, but not skip
  ahead. Green means holed, highlighted is where you are, dimmed is still locked.
- **Replay hole** — restart the current hole
- **New game** — back to hole 1 with a clean scorecard. Holes you have already
  reached stay unlocked.

Your unlocked holes and scorecard are saved in the browser, so closing the tab
and coming back keeps your progress. Replaying a hole overwrites that hole's
score rather than adding to your total.

**Saving may not work when you open `index.html` directly.** Browsers restrict
storage on `file://` pages — Safari blocks it outright, and others vary — so
progress can silently reset between sessions. Nothing breaks either way: the
game runs the same, it just starts over. If you want progress to stick, serve
the folder over HTTP instead:

```sh
npx serve .        # or: python -m http.server
```

Then open the address it prints. Verified working over `http://localhost`.

## Tinkering

Open `index.html#debug` to expose `window.gg` in the console:

```js
gg.state           // current hole / strokes / score / scores[] / furthest unlocked
gg.ball            // live ball: {x, y, vx, vy, alive, captured}
gg.load(4)         // jump to hole 5 (0-indexed)
gg.putt(300, -200) // fire the ball with a velocity vector
gg.sim(2.5)        // fast-forward the physics 2.5s, return where the ball ended up
```

`gg.sim()` steps the physics directly instead of waiting on animation frames,
so it is the quick way to test a shot from the console. It stops early if the
ball sinks, and reports where things ended up:

```js
gg.sim(6) // -> {x, y, v, sunk, strokes, captured, atRest}
```

Course layout and physics constants are all near the top of the `<script>`
block in `index.html` (`HOLES`, `G`, `FRICTION`, `CUP_MOUTH`, …).
