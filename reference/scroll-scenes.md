# Scrubbed scenes

PRECISION's motion vocabulary. `motion.md` covers *triggered* effects — something enters the
viewport and an animation plays on its own clock. This file covers *scrubbed* ones, where scroll
position **is** the timeline: scroll back and the scene runs backwards, stop mid-scene and the
frame holds.

The difference is not cosmetic. A triggered reveal is decoration on a page; a scrubbed scene is
the page — the reader is operating it. That is also why it is expensive.

## 1. Canvas frame sequences

Frames as numbered images, drawn to a `<canvas>` at a frame index derived from scroll progress.

```
anim/<scene>/small/0000.jpg  … 0089.jpg
anim/<scene>/medium/0000.jpg …
anim/<scene>/large/0000.jpg  …
anim/<scene>/sequence_manifest.json   ->  {"name":"","numFrames":"43"}
```

- **Four-digit zero-padded JPGs.** Sequential filenames mean the loader builds URLs by index and
  never ships a manifest of paths.
- **The manifest carries the count**, so the player never hardcodes it and a re-render with a
  different frame count needs no code change.
- **Three resolution tiers** selected by breakpoint. Observed canvas intrinsic sizes:
  `1080×416`, `1440×900`, `1660×644` at the large tier; `730×284`, `370×540`, `704×276` at small.
- Observed scene lengths: 43, 90, and 139+ frames. **43 is enough** for a product turn; 90 is a
  walk across a surface. Beyond ~120 the marginal smoothness is not worth the bytes.

**Why canvas rather than a `<video>` you seek:** browsers cannot seek video frame-accurately in
both directions at scroll speed — you get keyframe snapping and stalls. Canvas costs more bytes
and buys exact, reversible control. If the scene does not need reversibility, use a video with a
scroll-driven `currentTime` and accept the snapping, or just use a triggered video.

**Producing the frames:** render or shoot at the largest tier, then use the `ffmpeg` skill to cut
the sequence and the smaller tiers in one pass. Crush near-black backgrounds so the frames
composite onto the near-white ground without a visible plate.

## 2. The anchor-expression keyframe DSL

Timing authored as strings in the markup, over named anchor elements, rather than in JS:

```html
<div
  data-frames="90"
  data-anchors=".subsection-ports"
  data-sections=".ports-section-front,.ports-section-back"
  data-canvas=".canvas-wrap"
  data-keyframe='{"start": "a0t + a1h - 200vh",
                  "end":   "a0t + a1h + 200h + 200vh",
                  "anchors": [".bento-grid", ".section-chip-intro"],
                  "disabledWhen": "no-enhance"}'>
```

Grammar:

| Token | Means |
| --- | --- |
| `t` | anchor top, in document coordinates |
| `b` | anchor bottom |
| `h` | anchor height |
| `a0t`, `a1h`, `a2h` | indexed into the `anchors` array — anchor 0's top, anchor 1's height |
| `vh`, `px` | units, combined with `+` / `-` arithmetic |
| `disabledWhen` | capability flag that switches the whole scene off |

Observed values, verbatim, as a calibration set:

```
{"start": "t - 70vh",  "end": "t"}                    /* short lead-in */
{"start": "t - 75vh",  "end": "b"}                    /* runs the length of the anchor */
{"start": "t - 90vh",  "end": "b"}                    /* play-once scene */
{"start": "a0t + a1h - 100vh", "end": "a0t + a1h + 200h + 100vh"}
```

**Why this is worth copying:** retiming a scene is a one-attribute edit — no CSS, no JS, no
rebuild. A designer can tune the runway on a live page. It also keeps every scene's timing
readable in one place instead of scattered through a timeline file.

**Building it over GSAP ScrollTrigger.** Parse the expression into `{ trigger, start, end }`:
resolve each anchor selector to an element, read `offsetTop` / `offsetHeight`, evaluate the
arithmetic to a pixel offset, and hand ScrollTrigger `start: () => px` / `end: () => px` as
functions so they re-resolve on resize. Bind the scene to `scrub: true` — never a duration. One
~60-line parser buys the whole authoring model.

## 3. Sticky stages and their handoff

- **The stage** is `position: sticky; top: 0; height: 100vh` wrapping the canvas, inside a tall
  parent whose height defines the scene's scroll runway.
- **The handoff**: give the next chapter `margin-top: -100vh` — exactly one viewport height — so
  its stage pulls up underneath the previous one and two full-screen scenes join with no seam and
  no flash of page background between them.
- **The cross-fade**: a bottom-anchored sticky (`position: sticky; top: auto; z-index: 1`) on a
  parallel column lets a second element rise over the first as the reader scrolls, without either
  leaving the flow.

The source runs 14 sticky elements at once, including the 52px local nav at `z-index: 9997`.
Sticky is cheap; the canvases inside them are not.

## 4. Scrub, don't trigger

The transforms themselves are scrubbed, not transitioned. Observed live inline state on a
headline mid-scene:

```
transform: matrix(1.8, 0, 0, 1.8, 0, 210); opacity: 0;
```

— scale 1.8 → 1 with translateY 210 → 0, driven continuously by scroll position. There are **no**
`.reveal` / `.in-view` / `.animate-in` classes anywhere on the page; scrolling the full document
adds exactly one class (`paused`, on the video controls). Everything visual is inline style
written each frame.

Scenes are named in the markup with `data-anim-scroll-group` — `"Section - Performance"`,
`"Subsection chips"`, `"Processing StatsGallery"` — so a scene is a single addressable unit for
debugging and for switching off.

Practical rule: **if the reader can scroll it backwards, scrub it.** If the effect only ever
plays forwards and once (a counter, a play-once glow), trigger it — see `motion.md`.

## 5. Two decorative devices worth the trouble

**Faux corner notch.** A concave rounded corner where a sticky tile meets the page ground —
impossible with `border-radius`. Four absolutely positioned divs, one per corner:

```css
.corner-top-right { background-image:
  radial-gradient(circle at 100% 100%, rgba(255,255,255,0) 30px, #fff 31px); }
/* other corners: `at 100% 0%`, `at 0% 100%`, `at 0% 0%` */
```

The 30px → 31px hard stop is a deliberate 1px antialias band; a wider ramp reads as a smudge.
Recolour the opaque stop to whichever chapter value the tile sits on.

**Image-clipped gradient text.** A photographic fill in display type, with grain and non-linear
colour that CSS stops cannot produce:

```css
.gradient-text {
  color: #1d1d1f;                              /* fallback, and it must be legible */
  background-image: url("gradient.jpg");
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
```

Use it once, at 96px/700. Below ~48px the texture reads as noise. Keep the pure-CSS `--g-proof`
ramp for everything else so the page has one loud device, not two.

## 6. Reduced motion

One row per effect above. Decide these at build time; the source honours none of them.

| Effect | `prefers-reduced-motion: reduce` fallback |
| --- | --- |
| Canvas frame sequence | Single static frame at the scene's **narrative peak** — the frame that shows what the scene is about, not `0000`. Load that one image; never fetch the sequence. |
| Anchor-expression keyframes | Do not register the ScrollTrigger. Elements sit at their end state. |
| Sticky stage | Unpin. `position: static`, natural height, chapter scrolls normally. |
| Stage handoff (`margin-top: -100vh`) | Remove the negative margin — chapters abut instead of overlapping. Removing the pin without removing this leaves a viewport-tall hole. |
| Bottom-anchored cross-fade | Both columns static and stacked in document order. |
| Scrubbed transform | Final state applied immediately. No transition, no scaled-down version. |
| Faux corner notch | Keep — it is static geometry, not motion. |
| Image-clipped gradient text | Keep — static fill. |
| Scroll-driven video | Poster frame only. Never autoplay. |

## 7. Budget

What the source actually spends across a 43,645px document:

- 49 sequence assets requested at first paint
- 3 canvases, sequences of 43 / 90 / 139+ frames, at 3 resolution tiers each
- 14 sticky elements
- 6 videos, all `muted playsinline preload="none"` with `src` injected by JS — no `autoplay`
  attribute, no `poster` attribute, two carrying `data-alpha` for alpha-channel compositing
- 19 named scroll groups

Most projects cannot carry a fraction of that. **Set the frame count and tier plan before
building.** A single 43-frame hero sequence at two tiers is a realistic first budget and already
buys the register.

When over budget, **cut whole scenes** — one fully-realised scrubbed scene beats three
half-resolution ones, and a page with one scene plus static chapters still reads as PRECISION.
Thinning every scene reads as a slow site.
