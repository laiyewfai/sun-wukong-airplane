# 孙悟空开飞机 · Sun Wukong Flying a Plane

An animated vector scene (card 2 of the "三个有趣的绘图测试" set) — a monkey in an
aviator cap flies a small tan propeller plane over layered hills, red scarf streaming.

Single self-contained `index.html`: inline SVG, CSS animations and SMIL only.
No JavaScript, no build step, no external requests, no dependencies.

Live: https://laiyewfai.github.io/sun-wukong-airplane/

## Composition

| Layer | Motion | Period | Speed |
|---|---|---|---|
| Cloud band | drifts left | 300 u | 26.0 u/s |
| Far hills | parallax left | 900 u | 6.0 u/s |
| Mid hills | parallax left | 760 u | 9.0 u/s |
| Near hills | parallax left | 640 u | 13.0 u/s |
| Plane | bob (±6 u) + pitch (±1.3°) | 3.1 s | — |
| Pilot | counter-sway (±1.6°) | 2.3 s | — |
| Propeller | rotation about its hub | 0.1 s/rev | — |
| Scarf | two SMIL path morphs | 1.5 s / 1.1 s | — |

## Verified invariants

Measured by parsing the generated DOM and sampling the rendered page — not asserted:

- **Every scrolling band loops seamlessly.** A band only loops if the drawn content
  repeats exactly every period, so one module is authored and tiled unchanged.
  Verified at 0.0000 height difference between a module and the next for the far, mid
  and near ridges — for both the fill *and* the lit crest — and by confirming the cloud
  band's 55 groups reduce to 5 offsets repeated 11 times.
- **No scroll band is randomised per period.** An earlier revision re-randomised the
  cloud offsets each period, which left a visible jump every 11.5 s.
- **All modelling is clipped to a silhouette** (9 `clipPath` definitions), so no shade
  band, highlight or panel line can spill outside the form it belongs to.
- **Subject/background separation** ≥ 8 L\* between every adjacent pair (flank/sky
  −136, fin lit/shade +65, far/mid hill +47, mid/near hill +34, collar vs cockpit
  opening, spinner/sky −82).

## Drawing notes

- The barrel, wing, fin, canopy, pilot, clouds and hills are each modelled as a
  *tonal ladder* (shadow → base → lit → rim) painted in bands inside a clip.
- Shading boundaries follow the form: the barrel's lit/shade border is a curve, not a
  horizontal edge, so the fuselage reads as a cylinder rather than stacked stripes.
- Paint order matters and is load-bearing. The wing is drawn **before** the fuselage so
  its root tucks behind the hull; the canopy rim is drawn **before** the pilot so his
  scarf is not covered, with a separate front lip drawn **after** him so he reads as
  sitting *inside* the opening (47 % of his area inside a 249 u-wide opening).
- The propeller is a translucent wash plus sweep arcs rather than discrete blades, which
  is what a fast-turning prop actually looks like from the side.

## Accessibility

- `<title>`/`<desc>` describe the scene; the SVG carries `role="img"`.
- `prefers-reduced-motion: reduce` stops the CSS-driven scroll and bob. The SMIL
  animations (propeller, scarf, pilot sway) are **not** affected by that media query —
  SMIL has no such hook. Removing them needs an explicit pause control or a
  `switch`-based alternative; this is a known limitation, not an oversight.

## License

MIT — see [LICENSE](LICENSE).
