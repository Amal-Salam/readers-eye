# Layout check: tablets and landscape phones

Checked on 13 November 2026 against `main` at `f90268d`, in headless Chromium, in light and dark themes. At each size the check measured whether the page scrolls sideways, whether any block (header, eye, hints, caption, controls) overlaps the next, and whether any block runs off the screen.

| Size | Viewport | Scrolls sideways | Overlaps | Off screen | Eye height |
|---|---|---|---|---|---|
| Tablet, portrait | 768 × 1024 | No | None | None | 484 px |
| Tablet, landscape | 1024 × 768 | No | None | None | 428 px |
| Phone, landscape | 844 × 390 | No | None | None | 418 px |
| Phone, portrait | 390 × 844 | No | None | None | 236 px |
| Desktop | 1280 × 800 | No | None | None | 446 px |

Results were the same in light and dark.

## Result

Text never overlaps the eye or runs off the screen at any of these sizes, so the layout needs no fix.

One thing to decide: on a phone in landscape the eye is 418 px tall on a 390 px screen, so it never fits on screen whole and the reader scrolls to see it all. The size comes from the 420 px minimum in `measure()` (and the matching `.eye` rule in the CSS), which keeps the engraved text legible. Lowering it for short landscape screens would let the eye fit, at the cost of smaller text. That's a design choice, so it is left as it is.

## Screenshots (dark theme)

- [Tablet, portrait](layout/tablet-portrait.png)
- [Tablet, landscape](layout/tablet-landscape.png)
- [Phone, landscape](layout/phone-landscape.png)
