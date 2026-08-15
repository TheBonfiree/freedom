# Motion recipes — triggered

**Triggered** effects: something enters the viewport and the animation plays on its own clock.
This is STUDIO's default vocabulary. PRECISION's is *scrubbed* — scroll position is the timeline,
and the reader can run a scene backwards; those recipes are in `scroll-scenes.md`.

The opening sequence, before either of those applies — loaders, gates, entry choreography — is in
`entry.md`.

Either register can borrow from the other file, but pick a default and stay with it. A page that
mixes a drag-with-inertia gallery and a scrubbed canvas stage reads as two sites.

Timing defaults for the whole system: **0.75s duration, 0.27s stagger.** Slow enough to read as
deliberate, fast enough not to gate the scroll.

Every effect below lists its `prefers-reduced-motion` fallback. Decide these at build time. The
source site does not honour reduced motion at all — that is a defect, not part of the style.

| Effect | Built with | What it does | Reduced-motion fallback |
| --- | --- | --- | --- |
| Smooth scroll | Lenis + GSAP ScrollSmoother | Substrate for everything else; other effects feel jerky without it | Disable entirely — native scroll |
| Heading reveals | GSAP SplitText | Character-level stagger into place | Plain opacity fade, no stagger |
| Colliding word layers | Two absolutely positioned headings, different faces | Ghost outline behind solid fill; the overlap is the design | Static — keep the overlap, drop any movement |
| Marquees | GSAP timeline, `x` translate on a duplicated track | Horizontal runs of service or client names | Static wrapped list |
| Drag galleries | GSAP Draggable + InertiaPlugin | Throwable image strips with momentum | Native `overflow-x: auto` with scroll snap |
| Morphing mark | GSAP MorphSVGPlugin | Logo mark mutates continuously through scroll | First frame, static |
| Custom cursor | DOM element following pointer, accent dot inside outlined circle | The accent's main home | Hide entirely; ensure nothing was communicated only by it |
| Scroll-triggered video | ScrollTrigger + `<video muted loop playsinline>` | Feature videos start on entry, not on load | Poster frame only, never autoplay |
| Chapter flips | ScrollTrigger background tween | Black/white inversion animates rather than cutting | Hard cut at the section boundary |

## Budget

The source runs 147 ScrollTrigger instances, 20 marquees, 7 Lottie players, 5 AV1 videos, and
210 images across a 15,803px page. That is a real cost in LCP and in build hours, and most
projects cannot carry it.

Set the budget before building. When over it, **cut whole sections** rather than thinning every
effect — a page with five fully-realised sections beats nine half-animated ones.

## Implementation notes

- Load GSAP plugins individually; the full bundle is rarely needed. Draggable and InertiaPlugin
  are the two most often included and never used.
- **The library column is a recipe, not a dependency.** Under a no-CDN or self-contained
  constraint every effect above has a plain path: smooth scroll → native `scroll-behavior` and
  nothing else, character reveals → wrap each character in a `<span>` at build time and stagger
  with `transition-delay`, marquee → duplicated track and one `@keyframes` translate, drag gallery
  → `overflow-x: auto` with `scroll-snap-type`, reveals → `IntersectionObserver` toggling a class.
  The vocabulary survives; only the tooling changes.
- Videos: AV1 in `.mp4` with an H.264 fallback, always `muted loop playsinline`, `preload`
  nothing above the fold except the hero.
- Never autoplay the hero video on load if it is above the LCP element — poster first.
- The morphing mark should be a small inline SVG, not a Lottie. Lottie players are the heaviest
  line item on the source page relative to what they deliver.
