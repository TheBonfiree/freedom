# CATALOGUE — the register where volume is the proof

For a client whose work is a *list*: a studio with forty shipped titles, a label with a release
history, a press with a backlist, an archive. The visitor did not come to read an argument. They
came to browse, filter, and leave with one thing they wanted to find.

**The hard rule for this register, before any markup:** write down the scaffold pitch and the one
type size everything shares. Both are single numbers, and every other decision hangs off them.

**If the client has fewer than about twelve items with consistent imagery, this is the wrong
register.** Build STUDIO and use its case grid — `sections.md` §5. A catalogue with eight things in
it reads as a shop that just opened. Values below were measured from `denmu.com/portfolio` at
1440×900 on 2026-08-14.

This is the register's only file — tokens, archetypes and motion together — so it runs longer than
the STUDIO and PRECISION files, which split the same material three ways.

## 1. Tokens

```css
:root {
  /* ground and marks — monochrome, no chromatic accent exists in this register */
  --ink: #ffffff;
  --ink-2: #ffffff99;                 /* 60% — secondary labels */
  --ground: #0e1217;                  /* near-black with a blue cast, over flat #000 */
  --rule: #ffffff4d;                  /* 30% — the scaffold and every hairline */
  --veil-1: #ffffff1a;                /* 10% */
  --veil-2: #ffffff33;                /* 20% */
  --veil-3: #ffffff59;                /* 35% */
  --plate: rgba(255, 255, 255, 0.08); /* hover ground under nav and chips */

  /* one neutral grotesque, one weight for structure, one for prose */
  --face: "Helvetica Now Display", "Inter", system-ui, sans-serif;
  --w-ui: 500;
  --w-body: 400;

  /* the flat scale — three sizes, and that is the whole ladder */
  --t-ui: 12px;     /* labels, nav, captions, chips, the filter — uppercase */
  --t-cap: 14px;    /* item titles */
  --t-body: 16px;   /* the only running prose on the site */
  --lh-ui: 1;
  --lh-body: 1.2;
  --ls-ui: 0.28px;  /* positive, small, uppercase only */

  /* measure */
  --margin: 40px;   /* side margin, and the inset of anything pinned to a corner */
  --top: 150px;     /* the index opens on air, not on a headline */
  --pitch: 224px;   /* scaffold column */
  --gap: 22px;      /* content grid gutter */
}
```

**Three sizes and no display cut.** This is the register's argument with STUDIO: **loudness comes
from the imagery and the scaffold, not from a type ladder.** The moment the page owns a display
size, the small type reads as subordinate rather than uniform, and the effect is gone.

Be precise about what was measured, though: the source *brand* does own a display line — a
95 / 109 / 171 / 197px cluster across breakpoints — and spends none of it on the index. **The flat
ladder belongs to the catalogue page, not to the company.** It comes back on the item detail page.
Sizes are fixed per breakpoint, never fluid; no `clamp()` in this register.

> Can the client's work carry a page on its own, with no headline helping it? If the imagery is
> weak or inconsistent, the type ladder is the only thing left — build STUDIO instead.

## 2. The ruled scaffold

Full-height 1px verticals in `--rule`, running the entire scroll height behind everything.

```css
.scaffold {
  position: fixed; inset: 0; pointer-events: none; z-index: 0;
  padding-inline: var(--margin);
}
.scaffold::before {
  content: ""; display: block; height: 100%;
  background-image: repeating-linear-gradient(
    to right, var(--rule) 0 1px, transparent 1px var(--pitch));
  background-size: calc(100% + 1px) 100%;
}
```

At 1440 this lands seven rules — 40, 264, 488, 712, 936, 1160, 1384 — dividing a 1344px measure into
six. **The scaffold is not the layout grid, and must not become one.** The content grid divides the
*same measure* into four:

```css
.grid { display: grid; grid-template-columns: repeat(4, minmax(50px, 1fr)); gap: var(--gap);
        margin-inline: var(--margin); position: relative; z-index: 1; }
```

Six against four over one measure: the two systems agree at the outer margins and nowhere between.
That disagreement is the effect. Snap the cards to the rules and the page becomes a spreadsheet.
The one exception is the nav, which sits **on** the scaffold, each item one scaffold column wide —
so the top of the page reads as ruled and everything below reads as placed.

> How many columns does the imagery want? Set the content grid from the images, set the scaffold to
> a different divisor of the same measure, and never reconcile them.

## 3. The clipped wordmark

One full-bleed raster or SVG wordmark at the very top, wider than the viewport and cut off at both
edges, roughly 12% of the viewport width in height.

```css
.wordmark { inline-size: 100%; overflow: hidden; }        /* not 100vw — see below */
.wordmark img, .wordmark svg { display: block; inline-size: 118%; margin-inline-start: -9%; }
```

**The clip is load-bearing and `100vw` breaks it.** `100vw` includes the scrollbar, so the wrapper
is wider than the page and the overflow escapes as a horizontal scrollbar — the one thing this
layout must never do. Size the wrapper to `100%` of a full-bleed parent and let `overflow: hidden`
do the cutting.

The register's one loud moment. Because it is an image rather than type, it carries no weight in the
type system and the ladder stays flat. Letters cut by the viewport edge promise that the page runs
past the frame, which is the right promise for a catalogue.

**With no logo file**, set the wordmark as inline SVG `<text>` rather than as an HTML heading. It is
still type in the document, but it sits outside the CSS type scale, so the flat ladder survives —
which is the whole reason the device works. Give the `<svg>` `role="img"` and a `<title>`.

**The `<h1>` in a register that refuses headlines** is the page title — the catalogue's own name and
count, *"Kōrero Press — backlist, 34 titles in print"* — set at `--t-cap` like every other label.
It is a real heading doing real outline work at label size. The wordmark is not the `<h1>`, and the
answer is never a styled `<div>`; §11 is about exactly that failure.

> Is there a wordmark worth 12% of the screen? If the logo is a small legible mark, do not stretch
> it — run the nav against the top margin and let the first row of work be the opening image.

## 4. The item card

Caption **above** the image, not below. The eye meets the name, then the picture, then the
metadata — a card that reads as a catalogue entry rather than a poster.

```html
<a class="item" href="/work/hundred-line">
  <h2 class="item-title">The Hundred Line<br>Last Defense Academy</h2>
  <img src="/img/hundred-line.jpg" alt="" width="320" height="187" loading="lazy">
  <ul class="item-meta">
    <li class="chip chip-id">DJVN-F15-9658</li>
    <li class="chip">Visual Novel</li>
    <li class="chip">Apr. 23, 2025</li>
  </ul>
</a>
```

```css
.item-title { font: var(--w-ui) var(--t-cap)/1 var(--face); text-transform: uppercase;
              letter-spacing: var(--ls-ui); margin-block-end: 12px; }
.item img   { width: 100%; aspect-ratio: 320 / 187; object-fit: cover; border-radius: 0; }
.item-meta  { display: flex; flex-wrap: wrap; gap: 6px; margin-block-start: 12px;
              list-style: none; padding: 0; }
.chip       { font: var(--w-ui) var(--t-ui)/var(--lh-ui) var(--face); text-transform: uppercase;
              letter-spacing: var(--ls-ui); padding: 3px 11px; border: 1px solid var(--rule); }
.chip-id    { border-color: transparent; padding-inline: 0; }  /* the code is not a tag */
```

Images are `cover`, square corners, no shadow. **The ratio comes from the artifact, not from this
file** — 1.71 landscape was measured on a games catalogue; a book publisher is portrait, a record
label is square. What the register requires is that *every item uses the same one*, declared once
as `aspect-ratio` so the grid stays even before the images load. Mixed ratios are what make a
catalogue look like a spreadsheet of assets.

The ID code is set like the tags but without the box — an identifier, not a filter value, and that
distinction is real: tags are clickable, the code is not.

**Card hover is part of the plate effect, not a fifth item in the budget:** the same
`--plate` ground the nav uses, plus the image lifting from 0.94 to 1 opacity. Nothing moves. The
card is the page's primary interactive element and needs a state; it does not need an animation.

> Does every item have an ID, a type and a date? Invent none of them. A catalogue whose metadata is
> partly fabricated is worse than one with two fields.

## 5. The filter, as an affordance

Not a sidebar, not a row of pills across the top — a single control pinned to the bottom-right at
the same `--margin` as the scaffold, reading `FILTER +`, that opens the tag list on demand.

```css
.filter {
  position: fixed; inset-inline-end: var(--margin); inset-block-end: var(--margin); z-index: 2;
  font: var(--w-ui) var(--t-ui)/var(--lh-ui) var(--face); text-transform: uppercase;
  letter-spacing: var(--ls-ui); background: none; border: 0; color: var(--ink);
}
```

One control, fixed to the corner, is the recipe. The source instead ships **two** elements that
read as one: an in-flow copy sitting where it belongs in the layout, and a `position: sticky;
top: 0` copy that takes over once the first scrolls past. If you copy that, the second is
`aria-hidden="true"` **and** `inert` — `aria-hidden` alone leaves a focusable button in the tab
order announcing nothing, which is worse than the duplicate it was meant to fix. One control is
simpler and loses nothing; take the pair only if the design needs the filter visible in both
places at once.

The grid is the page; the filter is a tool that visits it. Permanent filter chrome tells the visitor
the catalogue is too big to browse, which is the opposite of what a catalogue is for.

**Filtering needs somewhere to land.** Ship a live count in a `role="status"` region — *"12 of 34
titles shown"* — and a zero-result state that says which filter is responsible and offers one click
back. A catalogue that can filter to nothing and says nothing is the register's most common failure.

> Are there enough tags to be worth filtering — five or more, each with at least three items? Below
> that, drop the control and let the grid stand. **If the client requires filtering anyway**, keep
> it and show the count against each tag, with empty tags disabled rather than hidden — the count
> is what tells the visitor the catalogue is shallower than the control implies.

## 6. Nav on the scaffold

Each nav item is exactly one scaffold column wide, so the row is measured by the rules rather than
by its own text. The current item gets a blurred plate rather than a colour.

```css
.nav a { inline-size: var(--pitch); padding: 3px 11px;
         font: var(--w-ui) var(--t-ui)/var(--lh-ui) var(--face);
         text-transform: uppercase; letter-spacing: var(--ls-ui); }
.nav a[aria-current="page"], .nav a:hover, .nav a:focus-visible {
  background: var(--plate); backdrop-filter: blur(8px); }
```

`backdrop-filter` needs something behind it to blur — over flat black it does nothing. Let the first
row of imagery run up under the nav, or accept the plate as a flat tint and drop the filter.

> Does the nav have four to six items? A catalogue nav with nine entries needs a different structure
> — the scaffold cannot absorb it.

## 7. Two devices that carry the rest

**The footer as a fixed stage.** Not the end of the scroll — a fixed layer the grid scrolls *over*,
revealed as the last cards clear it. In the source it holds live clocks for four office cities, the
address in three lines, and the mailing-list field. It works because a catalogue has no closing
argument to build to: the page runs out of items and the standing thing underneath appears.

```css
.footer { position: fixed; inset-inline: 0; bottom: 0; z-index: 0; }
.grid-wrap { position: relative; z-index: 1; background: var(--ground);
             margin-block-end: 100vh; }  /* the footer's own height */
```

**`mix-blend-mode: difference` on one label.** Exactly one element — a nav item or caption crossing
imagery — inverts against what is behind it instead of taking a plate. It is this register's answer
to STUDIO's accent: one moment of contrast that costs no colour. Used twice it is a gimmick, and it
fails over mid-grey imagery, so check the crossing.

> Which single element crosses the imagery? That one blends. Everything else takes a plate.

## 8. Motion

| Effect | Recipe | Reduced motion |
| --- | --- | --- |
| Nav / chip plate | Opacity and backdrop-filter, 0.18s ease | Instant plate, no transition |
| Filter reflow | FLIP on the grid, 0.32s, stagger 0.02s | Items reposition with no tween |
| Image reveal on scroll | Opacity 0 → 1 and 12px rise, 0.4s, once | Rendered visible from first paint |
| Wordmark drift | 2–3% horizontal drift on scroll, scrubbed | Static, no transform |
| Cursor | None. This register has no custom cursor | — |

Budget: four effects, none over 0.4s. The scaffold never animates — it is the fixed thing everything
else moves against.

## 9. Density and the small end

Density is the register, and density is what breaks first on a phone.

- The content grid drops to two columns, then one; the **scaffold drops to three rules, not six**.
  Keep the divisor different from the column count at every breakpoint or the effect collapses.
- `--margin` goes to 20px below 700px — 40px on a 390px screen eats a fifth of the width.
- 12px uppercase at `--ls-ui` holds down to 320px. Do not scale type with the viewport; a fluid
  `clamp()` would undo the flat ladder.

## 10. Copy, and one move this register does not inherit

Titles are the real names of the things, uppercase, one to six words, never rewritten into a
headline. Nav items are single words.

**Numerals are *not* structure here.** SKILL.md's fourth move — `(01)`, `[1]` — belongs to STUDIO
and PRECISION. Catalogue rows are unnumbered because the order changes under the visitor's hand at
the filter. The ID code in the chip row replaces the index numeral: an identifier that stays true in
any order.

## 11. What the source got wrong

- **No `<h1>`–`<h6>` anywhere** — every heading is a styled `<div>`. A flat type ladder must not
  become a flat document outline: page title, then one heading per item.
- **`tabindex` on elements nested inside `<a>`** — one link per card, everything else inert.
- **Zero `prefers-reduced-motion` rules**, with all motion in JavaScript where the CSS query never
  sees it. If motion lives in JS, branch in JS on
  `matchMedia('(prefers-reduced-motion: reduce)')`.

## Repetition rule

A catalogue has one call to action and it is not "get in touch" — it is *open an item*. Every card
is the CTA. Add at most one contact line, in the footer, at `--t-ui`. A mid-page contact band in
this register reads as an interruption of a list the visitor is still reading.
