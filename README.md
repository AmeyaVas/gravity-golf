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

## Buttons

- **Replay hole** — restart the current hole
- **New game** — back to hole 1, score reset

## Tinkering

Open `index.html#debug` to expose `window.gg` in the console:

```js
gg.state           // current hole / strokes / score
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
