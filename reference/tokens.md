# Tokens and scale

Two registers. Read the one you picked in decision zero. Use the *rules* verbatim; replace the
brand hue, the gradient, and the faces per project.

STUDIO values observed on hobro.digital, PRECISION values on apple.com/ph/mac-studio, both on
2026-08-13 at 1440×900.

Set every size as a `clamp()` expression rather than fixed px, per the fluid-scale method. The px values
in both tables are the desktop end of each clamp.

---

# STUDIO

## Palette

```css
:root {
  --c-bg-primary:      #000;      /* chapter A */
  --c-bg-secondary:    #fff;      /* chapter B */
  --c-bg-tertiary:     #161616;   /* one off-black, for a single chapter that needs to differ */

  --c-font-primary:    #000;
  --c-font-secondary:  #fff;
  --c-font-error:      #E6B0B0;   /* desaturated — errors do not get to be loud here */

  --c-border-default:  #636262;
  --c-border:          1px solid var(--c-border-default);
  --c-border-grid:     #4141413B;

  --c-brand-primary:   #00FB96;   /* REPLACE. Cursor dot and micro-marks only. */
  --c-brand-secondary: #DBDCCA;   /* REPLACE. Warm neutral, used sparingly. */

  --side-gutters:      0.75rem;   /* 12px — raise to 1.25rem below 380px */
  --header-height:     77px;

  --anim-default-time:  .75s;
  --anim-default-delay: .27s;
}
```

The accent rule, restated because it is the one most often broken: `--c-brand-primary` appears
on the custom cursor and on micro-marks. Not on buttons. Not on headings. Not on links.

## Four font roles

```css
:root {
  --font-title:      /* heavy grotesque, 900 */    'Archivo Black', Arial, sans-serif;
  --font-text:       /* neutral sans, 400/500 */   'Inter Tight', Helvetica, Arial, sans-serif;
  --font-cursive:    /* italic display serif */    'Instrument Serif', Georgia, serif;
  --font-typewriter: /* mono */                    'JetBrains Mono', ui-monospace, monospace;
}
```

Substitutes above are open licence. The source used Kamerik 205, PP Neue Montreal, Freight Big
Pro Light Italic, and Akkurat Mono LL — all commercial.

## Type scale

| Size | Role | Face | Weight | Line-height | Tracking |
| --- | --- | --- | --- | --- | --- |
| 176px | Hero wordmark | title | 900 | 0.84 | −1% |
| 180px | The one serif moment | cursive | 300 | 1.0 | −1% |
| 60px | Service list rows | text | 500 | 0.88 | −1.5% |
| 22px | Manifesto lead, nav | text | 500 | 1.0 | −1.5% |
| 18px | Body | text | 400 | 1.2 | −1.5% |
| 16.5px | Small uppercase label | text | 500 | 1.2 | −1.9% |
| 16px | Hero mono subtitle | typewriter | 500 | 1.1 | normal |
| 14px | Captions, buttons, `(01)` | typewriter | 500 | 1.0 | normal |

Two rules carry the whole scale:

- **Negative tracking above 16px**, about −1% at display sizes and −1.5% at text sizes. The mono
  face keeps normal tracking — it is the only thing that does.
- **Line-height falls as size rises**: 1.2 at body, 0.88 at 60px, 0.84 at the wordmark. Display
  lines should nearly touch.

## Layout

- **No max-width container. No CSS grid.** Sections are full-bleed; content is positioned per
  section. This is deliberate — a centred 1200px column reads as a template.
- 12px side gutters. Type genuinely runs to the viewport edge.
- Fixed header at 77px; its contents invert against whatever chapter is behind it.
- **Section padding is asymmetric and hand-set.** The source runs 167px top against 191px bottom
  on one section. Do not derive it from a spacing scale — the irregularity is what makes the
  rhythm read as art-directed.

---

# PRECISION

## Palette

```css
:root {
  --c-chapter-a:   #fafafa;   /* the ladder — chapters never hard-flip */
  --c-chapter-b:   #ffffff;
  --c-chapter-end: #f5f5f7;   /* closing chapters only */

  --c-tile-dark:   #111111;   /* contrast lives on tiles, not on sections */
  --c-tile-black:  #000000;

  --c-font:        #1d1d1f;   /* one text token, used everywhere */
  --c-font-muted:  #86868b;
  --c-rule:        #d2d2d7;
  --c-link:        #0066cc;

  /* REPLACE — the one ramp that carries every loud moment on the page */
  --g-proof: linear-gradient(90deg, #fac1ff 0%, #b44aff 45%, #674bff 100%);
}
```

This inverts STUDIO's accent rule rather than softening it: **there is no flat accent at all.**
Loud colour exists only as `--g-proof`, and it fills both the proof bars and the component
callout type, so the two read as one system rather than two decorations. Everything else on the
page is `--c-font` on a near-white ground.

Observed usage counts on the source, as a sanity check on ration: text `#1d1d1f` ×185, muted
`#86868b` ×51, rule `#d2d2d7` ×45, white ×33, link `#0066cc` ×14. The gradient hues appear on
29 elements total across a 43,645px document.

A second, wider ramp is worth having for a hero-scale callout — the source runs a six-stop version
whose stops sit at even 13.3% intervals and stop at 76.5%, so the final colour never fully lands:

```css
--g-hero: linear-gradient(90deg, #fff3e5 10%, #f6cfb4 23.3%, #eea4bc 36.6%,
                          #a18cff 49.9%, #64a8ff 63.2%, #c7f8ff 76.5%);
```

## The optical-size pair

```css
:root {
  --font-display: 'SF Pro Display', 'Inter Display', system-ui, sans-serif; /* ≥19px */
  --font-text:    'SF Pro Text',    'Inter',         system-ui, sans-serif; /* ≤17px */
}
```

The threshold **is** the hierarchy. There is no separate heading face — the same voice, cut for
two sizes. The source ships nine woff2 files total and never uses a second family.

Open substitutes: Inter Display / Inter, or a variable face with a real `opsz` axis (Newsreader,
Roboto Flex, Source Serif 4). If only one cut is available, **do not fake it with weight** — fall
back to STUDIO's four-role split, which is honest about being a multi-face system.

## Type scale

| px | Role | Cut | Weight | Line-height | Tracking |
| --- | --- | --- | --- | --- | --- |
| 96 | Section headline | display | 700 | 1.042 | −1.44px |
| 80 | Hero super | display | 700 | 1.05 | −1.20px |
| 64 | Feature headline | display | 700 | 1.063 | −0.576px |
| 56 | Chapter header | display | 600 | 1.071 | −0.28px |
| 48 | Proof figure, reduced headline | display | 600 | 1.083 | −0.144px |
| 40 | Intro copy | display | 600 | 1.20 | normal |
| 32 | Tab nav | display | 600 | 1.125 | **+0.128px** |
| 28 | Body, spec copy | display | 600 | 1.143 | +0.196px |
| 24 | Bar caption, eyebrow | display | 400 | 1.167 | +0.216px |
| 21 | Link label | display | 400 | 1.381 | +0.231px |
| 19 | Tout, price | display | 600 | 1.211 | +0.228px |
| 17 | Inline label | **text** | 400/600 | 1.47 | −0.374px |
| 14 | Spec row | **text** | 400 | 1.43 | −0.224px |

Three rules carry this scale:

- **Tracking changes sign twice.** Negative at display, crossing to **positive between 32px and
  40px**, positive through all mid-size UI type, then negative again in the small text cut. Big
  type tightens, mid type opens, small type tightens. This directly contradicts STUDIO's blanket
  "negative above 16px" — do not carry that rule across registers.
- **Line-height compresses as size rises**, 1.47 at 17px down to 1.042 at 96px. Same principle as
  STUDIO, gentler slope — display lines here breathe rather than touch.
- **Body is 28px.** Not 16, not 18. The register reads large; a 16px body column immediately
  reads as a generic marketing page.

## Layout — two grids

Both exist on the same page, deliberately.

| | Prose | Media |
| --- | --- | --- |
| Width @1440 | **980px**, fixed, centred | full-bleed, **1377px** content |
| Gutter | 222.5px each side | 24px each side |
| Inner grid | 12-col (`10 of 12, offset 1` → 817px; `9 of 12` → 735px) | bento tiles |
| Carries | every headline and paragraph | every image, canvas, video, tile |

Prose never gets wider than 980. Imagery is never boxed. Narrower sub-columns exist for dense
passages — the source runs 820px for gallery and privacy copy.

**Mobile: the gutter migrates onto the children.** At 390px the wrappers go `width: 100%;
padding: 0; margin-left: 0` and the offset moves to the content itself (`left: 24px`, width
`100% − 48px`); the media grid drops its 24px padding to `0` and goes fully bleed.

**Vertical rhythm is hand-set.** Observed consecutive section paddings: 45 / 80 / 90 / 97 / 135 /
137 / 140 / 148 / 150 / 160 / 195 / 200 / 230 / 250.5px. `160/160` is the only symmetric pair on
the page and appears only in boilerplate closing chapters. There is no spacer token — every
editorial chapter is tuned to its own composition.

**Mobile rhythm is re-authored, not scaled.** One block goes `140/250.5` → `75/353`: padding-top
nearly halves while padding-bottom *grows* 40%, because the scene below it needs more runway on a
tall narrow viewport. Never derive the mobile rhythm by multiplying the desktop one.
