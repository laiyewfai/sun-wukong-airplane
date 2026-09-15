# 🐒 Sun Wukong Flying a Plane

孙悟空开飞机 — the Monkey King, red scarf streaming, pilots a small tan
propeller plane over layered green hills. A single self-contained HTML file
(inline SVG, CSS + SMIL animations, **no JavaScript, no dependencies**).

## Features

- **The world slides, the plane holds station.** Every scrolling band — three
  hill layers plus the clouds — is drawn as an exactly periodic module and
  shifted by precisely its own period, so each loop is seamless (verified: the
  module-to-module height difference is 0.0 across all three ridgelines).
- **Parallax ordered by distance**: far hills 75 s per cycle, mid 42.2 s, near
  24.6 s, clouds 11.5 s — near moves fastest, so the depth reads correctly.
- **Spinning propeller**: two blades plus a translucent blur disc rotating about
  the spinner (0.1 s per revolution, explicit SMIL centre), with a faint arc so
  the disc reads as a propeller rather than a smudge.
- **Rippling scarf**: SMIL path morphing on a 1.5 s loop, with the plane's
  gentle bob (translateY) and pitch (rotate about its centre) out of phase.
- Flat vector scene: pale sun with a soft halo, puffy white clouds with grey
  undersides, layered blue-grey/green hills, and 齐天 lettered on the rear
  fuselage.
- The caption is real HTML text, so a full-bleed crop can never eat it.
- `prefers-reduced-motion` stops the CSS-driven motion (cloud and hill scroll,
  plane bob). The propeller, head, and scarf are SMIL and continue — SMIL cannot
  be switched off from CSS without scripting.

## Run it

Just open `index.html` in any modern browser — no build step, no server needed.

Or view the live page: **https://laiyewfai.github.io/sun-wukong-airplane/**

## License

MIT
