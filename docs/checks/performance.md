# Performance check: frame rate on phones

Checked on 13 November 2026 against `main` at `f90268d`.

## What the code already does

- The canvases are scaled by the screen's pixel ratio, **capped at 2** (`measure()`), so a 3× phone draws at 2×.
- Each of the three layers redraws only when what it shows changes (the `keys` cache in `frame()`); idle frames skip drawing.
- Drawing stops while the eye is scrolled out of view (`IntersectionObserver` on the stage).
- With reduced motion turned on, captions change without animation.

## Measurement

Headless Chromium at phone size (390 × 844, pixel ratio 3) with the CPU slowed down, timing every animation frame for 6 seconds after the page settled. The vsync limit was switched off, so the frame time, not the frames per second, is the figure to read: 16.7 ms per frame is 60 fps.

| Setting | 95% of frames within | Frames over 33 ms |
|---|---|---|
| Phone size, CPU 4× slower (roughly a mid-range phone) | 17.7 ms (about 56–60 fps) | 1 of 1,589 |
| Phone size, CPU 6× slower (a low-end phone) | 23.9 ms (about 42 fps) | 3 of 840 |
| Desktop, normal CPU | 9.4 ms | 0 of 5,960 |

## Result

At the mid-range setting the eye keeps close to 60 fps, above the 50 fps the issue sets, so the pixel ratio and the drawing work are left as they are. Only an emulated low-end phone drops to about 42 fps.

## Not checked

This is CPU emulation in a headless browser, not a real device: GPU speed, thermal throttling and battery drain weren't measured. The numbers should be confirmed on a real mid-range Android phone and an iPhone.
