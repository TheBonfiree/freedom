# Entry sequences

What happens before the page starts: loaders, gates, opening choreography, and delivering a page
whose assets are too heavy to show immediately.

Register-neutral — this applies to STUDIO and PRECISION alike. `motion.md` covers triggered
effects and `scroll-scenes.md` covers scrubbed ones; both assume the page is already running.
This file covers the moment before that.

Values observed on edolus.com, 2026-08-14 at 1440×900. Sourced teardown, including what could not
be measured: the `Edolus-Teardown` note, kept privately.

## First: most pages should not have a gate

A loader is justified only when **both** are true:

1. The page genuinely cannot render without heavy assets — a WebGL scene, a canvas frame
   sequence, an audio bed. Not "the hero image is large". Not "it feels premium".
2. There is an opening worth watching. A gate that shows a spinner is a delay; a gate that shows
   a title sequence is part of the product.

Everything else should stream and show content immediately. A loader added for atmosphere is a
tax the reader pays on every visit, and it is the single easiest way to make a fast site feel
slow. If you cannot answer both points, build the page without one and put the choreography into
the first scroll instead.

If a gate *is* justified, everything in §6 is mandatory, not optional. A gate is a promise that
the payoff arrives; the failure modes are what happens when it doesn't.

## 1. The state-class handoff

Four classes toggled on one wrapper, in order. The loader (or engine) owns the toggling; CSS owns
everything visual. No animation code in the app layer.

| Class | Applied | Means |
| --- | --- | --- |
| `preanim` | first frame, removed after one rAF | suppress all transitions while initial state is set |
| `bands-open` | assets past first meaningful threshold | opening choreography starts |
| `loaded` | payload complete | title and CTA become visible and interactive |
| `clicked` | user enters | overlay dissolves into what is behind it |

This is the pattern worth taking whether or not there is 3D behind it. One addressable state
machine on one element means the whole opening is inspectable in DevTools, switchable by hand,
and testable without waiting for the real payload.

Name scenes, not steps. `bands-open` describes what the page does; `step-2` describes nothing.

## 2. The `.preanim` guard

```css
#splash.preanim,
#splash.preanim * { transition: none !important; }
```

Applied inline on the first frame, removed after one `requestAnimationFrame`. Without it, setting
the initial state animates *from* the browser's defaults — a flash of the end state, then a
transition backwards into the start state. Small, correct, and routinely forgotten.

## 3. Odometer counter

The genuinely reusable component. Per digit column, two stacked digits in an overflow-hidden box,
rolled by `translateY`:

```html
<span class="roll-col"><span class="roll-num">8</span><span class="roll-num">9</span></span>
```

```css
.roll-col { position: relative; width: 1ch; height: 1.35em;
            overflow: hidden; letter-spacing: 0; }
.roll-num { position: absolute; height: 1.35em; }  /* translateY(0) → translateY(-100%) */
```

Two details carry it:

- **`width: 1ch`** is why the columns do not jitter as digits change. It needs a mono face or
  `font-variant-numeric: tabular-nums`; on a proportional face the counter shifts sideways on
  every tick and the effect is worse than plain text.
- **`letter-spacing: 0`** locally, because tracking inside a `1ch` box breaks the alignment. If
  the surrounding type is tracked (both registers track their mono/small type), reset it here.

Works for any counting readout — progress, prices, stat tiles — not just loaders.

## 4. Letterbox band reveal

Two 50%-height black divs above everything, sliding apart:

```css
.band { position: fixed; left: 0; width: 100%; height: 50%; z-index: 3;
        transition: transform 1600ms cubic-bezier(0.65, 0, 0.35, 1); }
.band-top    { top: 0; }
.band-bottom { bottom: 0; }
.bands-open .band-top    { transform: translateY(-100%); }
.bands-open .band-bottom { transform: translateY(100%); }
```

A full cinema-curtain open in two elements and one class, no library. `cubic-bezier(0.65,0,0.35,1)`
is a symmetric in-out — the bands accelerate and settle evenly, which is what makes it read as
mechanical rather than bouncy.

Works on any chapter transition, not only the opening. In STUDIO it substitutes for a hard
black/white chapter flip.

## 5. Corner brackets

Four L-shaped corner slivers on a single pseudo-element, built from stacked solid "gradients" —
no border, no extra markup:

```css
.cta::before {
  content: ""; position: absolute; inset: -6px -8px;
  background-image:
    linear-gradient(#fff, #fff), linear-gradient(#fff, #fff),
    linear-gradient(#fff, #fff), linear-gradient(#fff, #fff);
  background-repeat: no-repeat;
  background-size: 10px 1px, 1px 10px, 10px 1px, 1px 10px;  /* per-corner slivers */
  background-position: left top, left top, right bottom, right bottom;
  transition: inset 0.3s ease;
}
.cta:hover::before { inset: -4px; }
```

Hover animates **only** `inset`, so the brackets tighten toward the button rather than glowing or
filling. It reads as a targeting reticle locking on — an interaction with no colour change at all,
which is why it survives in PRECISION (no flat accent) and STUDIO (accent is rationed) alike.

## 6. The three-tier timing hierarchy

The most transferable idea here, because it is a rule rather than a trick.

| Tier | Duration | Easing | Carries |
| --- | --- | --- | --- |
| Input feedback | 100–200ms | `steps(1)` — hard cut, no interpolation | hover, click acknowledgement |
| Transition | 1.2–1.6s | `cubic-bezier(0.4,0,0.2,1)` or `(0.65,0,0.35,1)` | bands, scrims, exits |
| Atmosphere | 3s, 0.3s delay | `ease` | title and hint fades |

Observed keyframes at the input tier: `ctaLabelBlink 0.1s steps(1)` on hover, `ctaBlink 0.2s
steps(1) forwards` on click. **`steps(1)` means no interpolation at all** — the state flips. That
is the point: everything on the page eases slowly except the button, which is hard-cut digital,
and the contrast between the two *is* the interaction personality.

The rule generalises. Pick three tiers, keep them far apart, and put input feedback in a different
easing family from everything else. STUDIO's 0.75s/0.27s defaults in `motion.md` are the same idea
at lower amplitude — one transition tier plus a stagger.

## 7. Blur exit

```css
.clicked #title-group { opacity: 0; filter: blur(14px);
                        transition: opacity 1.4s cubic-bezier(0.4,0,0.2,1),
                                    filter  1.4s cubic-bezier(0.4,0,0.2,1); }
```

The overlay dissolves into what is behind it rather than cutting. Costs real compositing —
`filter: blur` on a full-screen layer is expensive — which is acceptable exactly once, on exit,
when nothing else is competing for the frame. Do not reach for it mid-page.

## 8. Heavy-asset delivery — the rules

Framed as requirements, because the source breaks all four and the failure is the worked example:
`__game-scripts.js` hung across two full loads, the loader stalled at 80%, and the page was a
black rectangle with an inert button. No recovery, twice.

- **A gate needs a timeout and a fallback path.** If the loader has not completed in N seconds,
  show the content anyway or show a real error with a retry. A loader with no ceiling is a hang.
- **Text content must exist in the HTML.** Real copy in the DOM plus a `<noscript>` block, so a
  failed, blocked, or slow bundle still communicates who you are. 54 nodes and no fallback text
  means a broken build says nothing at all.
- **Do not gate the primary action on the whole payload.** 90+ requests including ~20 `.glb`/
  `.basis` and 16 `.ogg` before the CTA becomes clickable is a single point of failure by design.
  Gate the CTA on the minimum needed to act; stream the rest.
- **`prefers-reduced-motion` is not optional here.** The source has **zero** matching rules across
  all 55 rules in its CSSOM — confirmed readable, not unread — on a page that is 100% motion plus
  audio.
- **Autoplaying audio needs a visible, keyboard-reachable mute**, and nothing may depend on audio
  to be understood. A "experience with headphones" hint is not a control.

## 9. Reduced motion

One row per effect above. Decide at build time.

| Effect | `prefers-reduced-motion: reduce` |
| --- | --- |
| The gate itself | Skip it. Land directly on the loaded state — no opening, no bands. |
| `.preanim` guard | Keep — it suppresses motion, it does not create any. |
| State-class handoff | Keep. The states still apply; only their transitions are removed. |
| Odometer counter | Final value written directly, no roll. |
| Letterbox bands | No slide. Remove the overlay outright once loaded. |
| Corner brackets | Keep the static brackets; drop the `inset` hover transition. |
| `steps(1)` blink | Keep — a hard state change is not motion, and removing it costs the only click feedback. |
| Atmosphere fades | Instant. Opacity applied without transition. |
| Blur exit | Opacity only. Never `filter: blur` — it is the most expensive thing on the page and reads as a smear. |

## 10. Type in a gate

There is no scale to inherit here — a splash has five levels at most. Two families, two voices,
which is the same principle both registers already run on:

- **Statement**, a geometric grotesk at light weight: `clamp(44px, 8.9vw, 96px)`, weight 300,
  line-height 1.04, tracking `+0.01em`, uppercase.
- **Machine voice**, mono at small size: 12px, weight 500, tracking `+0.1em` — the counter, the
  button label, the hint.

Note that the statement tracks *positive* at display size, which contradicts STUDIO's negative
display tracking. Light-weight uppercase display type needs the extra air; STUDIO's rule assumes
weight 900. Match the tracking to the weight, not to the size alone.

Opacity does the tonal work rather than extra colours — a three-value greyscale ramp
(`1` / `0.8` / `0.7`) on pure black, six distinct colours on the whole page. Cheaper than a
palette and impossible to get wrong.
