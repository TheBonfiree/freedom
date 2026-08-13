# PRECISION section archetypes

Eight patterns for product and spec pages, in the order they work best. Each ends with the
question to answer before reusing it. A section whose question has no good answer should be cut,
not filled with placeholder.

STUDIO's archetypes are in `sections.md`. Do not mix the two sets on one page.

## 1. Hero — scrubbed product reveal

Eyebrow at 24px carrying the product name, over the claim at 80px/700 with −1.20px tracking.
Behind both, a canvas frame sequence of the product turning or assembling, scrubbed by scroll —
not a video, not a still. The claim holds fixed while the scene runs under it. The eyebrow is the
page's `<h1>`; the claim is a `<p>`, because the claim is a headline visually and a slogan
semantically.

Mobile drops the claim to 40px and resets tracking to `normal`.

> Does a rendered or shot 40–90-frame turn of the product exist? If not, this is a still hero —
> which is fine. A looping video pretending to be a scrub is not: the scroll decouples from the
> footage and the whole register falls apart.

## 2. Chapter headline, unaccompanied

96px/700 in the prose column, alone in its chapter, on the alternate ladder value. No subhead, no
image, no CTA. This is what a chapter break looks like in this register — the equivalent of
STUDIO's manifesto flip, at lower amplitude.

> What is the six-word claim for this chapter? If it takes a sentence, it belongs in intro copy
> at 40px instead and this section should be cut.

## 3. Component tout — dark tile on near-white

A `#111` tile with generous rounding, floating on the near-white ground, holding the component
name at 48px and a spec list at 28px/700 filled with `--g-proof` via `background-clip: text`.
This is where the page gets its contrast — the section behind it stays near-white.

Two touts side by side, each in a sticky column, is the pattern for comparing two variants of the
same component. The second column uses bottom-anchored sticky
(`position: sticky; top: auto; z-index: 1`) so it cross-fades in over the first.

> Are there named internal components worth naming? A tout for an unnamed generic part reads as
> filler. Under two named components, use a spec list instead.

## 4. Proof module — bars and figures

The register's centrepiece. Three bars, descending, with the product first. Markup:

```html
<div class="bars-container">
  <div class="bar-content-container">
    <div class="bar-mask" data-bar-width="2.9">
      <hr class="bar" aria-hidden="true">
    </div>
    <span class="bar-caption">Studio with M4&nbsp;Max</span>
  </div>

  <figure class="badge">
    <div class="badge-content">
      <div class="badge-value-container">
        <span class="badge-value">2.9</span><span class="badge-unit">x</span>
      </div>
      <span class="badge-caption"></span>
    </div>
  </figure>
  <!-- repeat: data-bar-width="2.1", "1.8" -->
</div>
```

```css
.bar      { height: 10px; border: 0; margin: 0; border-radius: 5px;
            background-color: transparent; background-image: var(--g-proof); }
.bar-mask { border-radius: 5px; }             /* width driven from data-bar-width */
.badge-value, .badge-unit { font-size: 48px; font-weight: 600; letter-spacing: -0.144px; }
.bar-caption { font-size: 24px; font-weight: 400; letter-spacing: 0.216px; }
```

Four decisions doing the work:

- **`<hr>` as the bar.** A semantic thematic break, `aria-hidden` because the caption and figure
  already carry the meaning. A `<div>` here would be one more meaningless box.
- **The datum lives in `data-bar-width`**, on the mask, not in an inline style. The page stays
  queryable; the mapping from multiplier to width stays in one place.
- **Value and unit are separate spans** inside a `<figure>`, so the `x` can be tracked and
  baselined independently of the numeral.
- **Same gradient as the tout.** Proof and component read as one system.

Where the module has variants (different workloads), put them behind a tab list: `ul[role="tablist"]`
with `a[role="tab"]`, `tabindex="0"` on current and `-1` on the rest, separated by a literal
`<span aria-hidden="true">/</span>` at 32px/600.

> Is there a real benchmark with a stated baseline and a documented method? No baseline, no
> module — an uncited multiplier is the fastest way to look cheap. See archetype 7.

## 5. Sticky spec stage

A viewport-height sticky stage pinning a canvas, with labelled content advancing over it as the
scroll drives the sequence. The source's ports scene: `data-frames="90"`, two labelled
sub-sections ("Back Ports", "Front Ports") at 19px/600, one pinned canvas.

Chain two stages by pulling the second up under the first with `margin-top: -100vh` so the
handoff has no seam. Full mechanics in `scroll-scenes.md`.

> Does the product have a physical surface worth walking across — ports, controls, internals? If
> the "detail" is a feature list, this is archetype 3, not a stage.

## 6. Comparison — grid, not table

**There is no `<table>`.** The comparison is a CSS grid with a dead centre gutter column:

```css
.compare-grid { display: grid; grid-template-columns: 244px 80px 244px; gap: 0; }
@media (max-width: 480px) {
  .compare-grid { grid-template-columns: 1fr 1fr; }  /* gutter column deleted, never a scroller */
}
```

One semantically-classed element per spec row — `.product-processor`, `.product-cpu`,
`.product-gpu`, `.product-memory`, `.product-storage` — so rows align by class rather than by
position, and a missing spec leaves a gap instead of shifting the column. Spec rows are 14px/400
in the **text** cut. Each column ends in its own CTA plus a secondary text link.

Reserve zero-width columns (`244px 80px 244px 0 0`) if a third product is planned — the grid
absorbs it without a rewrite.

> Exactly two products? Three needs a different layout entirely; one needs a spec list, not a
> comparison.

## 7. Footnote apparatus

Every numeric claim on the page carries a marker:

```html
<sup class="footnote">
  <a href="#footnote-6" aria-label="Footnote 6">6</a>
</sup>
```

```css
.footnote     { font-size: inherit; vertical-align: baseline; position: relative; top: 0; }
.footnote a   { text-decoration: none; color: inherit; }
```

Note what is *not* there: no `vertical-align: super`, no size reduction. The marker matches its
parent's size flat, and the raised look comes from the face's superior figures. Markers inherit
colour, so they survive on dark tiles unchanged. Disclaimer paragraphs sit in a `.disclaimer`
block at the foot of the page, each with a matching `id`.

> Can every numeric claim be cited with a real method? If a claim cannot be footnoted, it cannot
> appear as a proof figure — demote it to copy or drop it.

## 8. Router closers

A row of dark tiles at `#000`, one line each, linking outward — adjacent products, the
sustainability page, business and education. Below them, an icon-card row of three values
statements. This is the page's exit, and it is deliberately quiet: no gradient, no motion, one
headline per tile.

> Are there three or more genuine outward destinations? Two tiles read as a stub; use a single
> full-width band instead.

## Repetition rule

One conversion goal, three placements: a sticky local nav at the top (52px, `z-index` above
everything), the CTA inside each comparison column, and the footer. No second competing ask
anywhere on the page. Price appears with the CTA at 19px/600 — never at display size.
