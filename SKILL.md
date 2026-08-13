---
name: freedom
description: Use when building or redesigning a marketing site that should read as premium — agency and studio sites, portfolios, product and hardware landing pages, spec pages, capability decks made into pages. Trigger on "make it feel premium", "bold editorial site", "brutalist type", "agency site", "studio landing page", "big type hero", "HOBRO style", "Apple-style product page", "spec page", "scroll-scrub", "premium product marketing", or any brief asking for a site that must not look templated. Supplies two concrete style registers — STUDIO (loud, four-font, black/white chapters) and PRECISION (quiet, optical-size pair, near-white ladder, scrubbed scenes) — each with tokens, section archetypes, and motion with reduced-motion fallbacks.
user-invocable: true
argument-hint: "[studio|precision|gate · tokens|sections|motion|scenes|entry|fable] [brief or target]"
allowed-tools:
  - Read
---

# Freedom

Style direction for sites that must read as expensive. Two registers, derived from live teardowns
of two sites that solve that problem from opposite ends. Both teardowns are sourced, value by
value, in the vault:

- STUDIO — the `Hobro-Digital-Teardown` note
- PRECISION — the `Apple-Mac-Studio-Teardown` note

Those teardowns are kept privately and are not distributed with this skill.

**Relationship to `impeccable`:** impeccable supplies the process — phases, critique, verified
passes. This skill supplies the visual direction those phases execute. Run both. If they
conflict, impeccable's process wins; this skill's aesthetics fill the gaps it leaves open.

## Decision zero — pick the register

Before anything else, including the font decision, decide which register the project is in.

| | STUDIO | PRECISION |
| --- | --- | --- |
| Subject | a **maker** — agency, studio, portfolio, capability deck | a **thing** — product, hardware, spec-bearing software |
| What proves it | the work | the numbers |
| Chapters | hard `#000` ↔ `#fff` | near-white ladder `#fafafa` ↔ `#fff` → `#f5f5f7` |
| Contrast | the section is dark | dark **tiles** float on near-white |
| Type | four faces, four jobs | one family, two optical sizes |
| Colour | one accent, cursor only | no flat accent — gradients on proof marks |
| Layout | no container, 12px gutters | two grids: 980px prose, full-bleed media |
| Motion | triggered reveals | scrubbed scenes |
| Sections | `reference/sections.md` | `reference/product.md` |

Mixing them produces a page that reads as neither — a spec table in STUDIO looks unfinished, a
drag-with-inertia gallery in PRECISION looks like a different site. If the brief genuinely spans
both (a studio launching its own product), build PRECISION and borrow only STUDIO's mono metadata
layer.

## Commands

**Register:** `/freedom <studio|precision> [brief]` forces the register, skips the gate, and locks
it for the session. `/freedom gate [brief]` runs decision zero and stops — it reports the register
and the reason, and builds nothing.

Everything below routes to exactly one reference file. The argument after the token is the target.

| Token | Reads |
| --- | --- |
| `tokens` | `reference/tokens.md`, the locked register's half only |
| `sections` | `reference/sections.md` (STUDIO) or `reference/product.md` (PRECISION) — one token, the locked register picks the file |
| `motion` | `reference/motion.md` — STUDIO triggered effects |
| `scenes` | `reference/scroll-scenes.md` — PRECISION scrubbed scenes |
| `entry` | `reference/entry.md` — its argument against a loader comes first |
| `fable` | `reference/fable-request.md`, emitting the locked register's request block |

Routing:

- **No token:** treat the whole argument as the brief and run decision zero. This is the default and
  the most common path.
- **Leading token matches the register block or the table:** act on it; everything after it is the
  target.
- **`motion` under PRECISION, or `scenes` under STUDIO:** say so and redirect to the in-register
  file instead of reading the one asked for. An explicit verb must not become a way to smuggle in a
  cross-register effect.
- **Ambiguous first word:** prefer the brief reading and say which was taken. A client named "Studio
  Mono" is a brief, not a register switch.

**The register persists once decided.** After decision zero has run or a register has been forced,
later calls assume it rather than re-deriving it from a thin fragment — `motion hero` carries no
maker-or-thing signal and must not re-open the question. Only an explicit `studio` or `precision`
token switches it, and a mid-build switch invalidates decisions already made, so say so out loud
when it happens.

Nothing enforces this but the instruction, so restate the register whenever acting on it. If it has
been lost, ask rather than guess — a visible re-ask is cheap, a silent flip mid-page is not.

## The hard rule

Before writing a single line of markup, decide and write down:

**In STUDIO —**

1. **The four font roles** — which face is display, which is body, which is the one italic
   display moment, which is mono. Four faces, four jobs, no overlap.
2. **The one accent** — a single hue that will appear only on the cursor and micro-marks.

**In PRECISION —**

1. **The optical-size pair** — one family with two real cuts (display above ~19px, text below
   ~17px), or two faces drawn from the same skeleton. Not one face at two weights.
2. **The gradient** — the single multi-stop ramp that carries every loud moment on the page, and
   which appears on both the proof bars and the callout type so they read as one system.

Skipping this and choosing type while building is what makes a site look templated. Nothing else
in this skill works without those decisions locked first.

## The six moves

**1. Type carries the hierarchy, not decoration.**
*STUDIO:* a heavy grotesque at 900 for wordmarks only, a neutral sans for everything read, an
italic display serif used *exactly once* in the whole page, a monospace carrying every label,
numeral, caption, and button. Each face owns one job, so the page reads as designed rather than
decorated. Two fonts plus size variation does not achieve this.
*PRECISION:* the same effect from one family, because the **optical size is the hierarchy** —
a display cut above the threshold, a text cut below it, nothing else. No separate heading face.
Both routes work; a face used for two jobs is what fails.

**2. Loud colour is rationed.**
*STUDIO:* one hue, living on the custom cursor and a few micro-marks. It never fills a button,
never sets a heading. Scarcity is the whole effect — an accent-coloured hero CTA collapses this
register into a template instantly.
*PRECISION:* there is no flat accent at all. Colour arrives only as the gradient, only on proof
marks and component callouts. Everything else is one text token on a near-white ground.

**3. Chapters alternate; the inversion replaces dividers.** Full-bleed sections flip, which is
what lets the page drop eyebrow headings and rules entirely. STUDIO flips hard, near-black to
white. PRECISION runs the same device at low amplitude — a three-value near-white ladder with no
visible seam — and gets its drama from dark tiles floating on that ground, never from a dark
section.

**4. Numerals are structure.** Caption every image in mono or the small cut. Number sections
`(01)`, items `[1]`, years `23-26`; in PRECISION, footnote every claim. Numerals used as
structure make a page feel like a system rather than a layout.

**5. Motion is the product, and it has a budget.** STUDIO: smooth scroll, character-level heading
reveals, marquees, drag-with-inertia galleries — see `reference/motion.md`. PRECISION: canvas
frame sequences, sticky stages, scroll-scrubbed transforms — see `reference/scroll-scenes.md`.
Decide the budget up front and cut whole sections or whole scenes to stay inside it, rather than
thinning every effect into mush.

**6. Proof has a form.** Numbers are designed objects, not sentences. The multiplier splits value
from unit into separate elements so the unit can be tracked and baselined on its own; the raw
datum lives in a `data-` attribute on the mask, not in an inline style; the bar is an `<hr>` with
`aria-hidden`, doing decorative work while staying semantic. A page that renders "2.9x faster" as
body copy has thrown away its strongest visual. PRECISION-native — but any STUDIO page with real
metrics should steal it.

## Non-negotiables

- **`prefers-reduced-motion` for every effect**, decided at build time. Fallbacks per effect are
  in `reference/motion.md` and `reference/scroll-scenes.md`. Neither source site honours it; do
  not inherit that.
- **Every scrub scene needs a static frame under reduced motion** — the frame at the scene's
  narrative peak, not frame `0000`, and not a slowed scrub.
- **Scrub scenes cost real bytes.** One canvas sequence at 90 frames across three resolution
  tiers is a budget line item. Name the frame count and tier plan before building.
- **Footnote markers need `aria-label="Footnote N"` and a real in-page target.** A bare
  superscript numeral is an uncitable citation.
- **Type running to a 12px gutter breaks below ~380px** (STUDIO). Raise the gutter at the small
  end.
- **PRECISION's prose column never exceeds ~980px** even though its media runs full-bleed. One
  page, two grids, deliberately.
- **A gate needs a timeout and a fallback.** If a loader can hang, it will. Real copy in the HTML,
  a `<noscript>` block, and a path that shows the page anyway. Most pages should have no gate at
  all — see `reference/entry.md` for the test.
- **Autoplaying audio needs a visible, keyboard-reachable mute**, and nothing on the page may
  depend on audio to be understood.
- **A custom cursor needs a keyboard-equivalent path** for anything it communicates.
- **Check the imagery count before committing to the case grid, client list, or team section**
  (STUDIO). All three look broken when under-filled. Fewer than eight cases means a different
  section. In PRECISION the same test applies to benchmarks: no stated baseline, no proof module.

## References

Read the one you need; do not load them all.

- `reference/tokens.md` — palette, type scale, tracking and layout rules for both registers.
- `reference/sections.md` — nine STUDIO archetypes, each with its swap-in question.
- `reference/product.md` — eight PRECISION archetypes, each with its swap-in question.
- `reference/motion.md` — triggered-effect recipes with reduced-motion fallbacks (STUDIO).
- `reference/scroll-scenes.md` — scrubbed scenes, canvas sequences, sticky stages (PRECISION).
- `reference/entry.md` — loaders, gates, opening choreography, heavy-asset delivery. Both
  registers. Read it before adding a loader — its first section is the argument against one.
- `reference/fable-request.md` — request blocks for handing either register to Fable for planning.
