# Fable request template

For handing this direction to Fable as a planning request. Fable plans; Claude Code builds.
Workflow constraints assumed here: a small daily request budget, one goal per request, and no disk
access on Fable's side — so the language block has to be pasted every time.

```
PROJECT:     <client>, <one line on what it is>
CLIENT TIER: <n> case studies with consistent imagery / claims need legal signoff:
             <yes|no> / approval chain includes procurement or brand review:
             <yes|no> / <n> named clients worth listing
GOAL:        Architecture and section plan for a <n>-section marketing site in the
             STUDIO register (client tier above)
WHAT I HAVE: Design language (pasted — no repo access):
             - Four fonts, four jobs: display 900 for wordmarks only / neutral sans for
               all readable copy / one italic display serif used exactly once / mono for
               every label, numeral and button
             - Palette: #000, #fff, one off-black, ONE accent used only on the cursor and
               micro-marks — never a button, never a heading
             - Full-bleed sections, no max-width container, no grid, 12px side gutters
             - Chapters alternate black and white as the only section divider
             - Type scale 176 / 60 / 22 / 18 / 16.5 / 14; negative tracking above 16px,
               line-height 0.84 at display rising to 1.2 at body
             - Motion: smooth scroll under everything, character-level heading reveals,
               marquees, drag-with-inertia galleries; 0.75s duration, 0.27s stagger
             - Copy: uppercase, declarative, numerals as structure — (01), [1], 23-26
             Client material: <brand assets, copy, imagery count, existing stack>
             Target stack: <e.g. Astro + GSAP, or Next.js + Lenis>
CONSTRAINTS: Performance budget: <LCP target>. prefers-reduced-motion must be honoured
             for every effect. <deadline, CMS requirement, anything that cannot change>
DELIVERABLE: architecture
```

## PRECISION request block

```
PROJECT:     <client>, <one line on what the product is>
CLIENT TIER: benchmark data with a named baseline: <yes|no — name it> / claims
             requiring footnote or disclaimer: <n> / regulatory or legal review in
             the approval chain: <yes|no> / spec depth expected: <headline figures
             only | full spec table | both>
GOAL:        Architecture and section plan for a <n>-section product page in the
             PRECISION register (client tier above)
WHAT I HAVE: Design language (pasted — no repo access):
             - One family, two optical cuts: display above 19px, text below 17px.
               No separate heading face — the optical size IS the hierarchy
             - Palette: near-white ladder #fafafa / #ffffff / #f5f5f7, one text
               token #1d1d1f, dark TILES (#111, #000) floating on near-white for
               contrast — never a dark section. NO flat accent anywhere
             - One gradient carries every loud moment, and it fills both the proof
               bars and the component callout type so they read as one system
             - Two grids on one page: 980px centred prose column, full-bleed media
               grid at 24px gutters. Prose never exceeds 980
             - Type scale 96 / 80 / 64 / 56 / 48 / 40 / 32 / 28 / 24 / 19 / 17 / 14.
               Body is 28px. Tracking is NEGATIVE at display, crosses to POSITIVE
               between 32 and 40px, negative again in the small text cut
             - Section padding hand-set, never from a spacing scale; mobile rhythm
               re-authored rather than scaled
             - Motion: scrubbed, not triggered — canvas frame sequences over sticky
               viewport stages, chained with margin-top: -100vh. Scroll position is
               the timeline
             - Proof: <hr> bars with the datum in data-bar-width, figure splitting
               value and unit into separate spans, every claim footnoted
             Product material: <specs, benchmark data + baseline, render/frame
               assets, imagery count, existing stack>
             Target stack: <e.g. Astro + GSAP ScrollTrigger, or Next.js>
CONSTRAINTS: Performance budget: <LCP target> and <n> canvas sequences at <n>
             frames, <n> tiers. prefers-reduced-motion honoured for every effect.
             <deadline, CMS requirement, anything that cannot change>
DELIVERABLE: architecture
```

## Field notes

- **Name the tier, not the vibe.** "Premium", "high-end" and "expensive" resolve to nothing in a
  block where every other line is a number, and Fable reads this cold with no repo access. State
  what the tier forces onto the page — the case-study count, the footnote requirement, who signs
  off — and the plan can act on it. Same rule as `entry.md`'s test for describing an entry sequence.
- **One goal.** Asking for architecture and copy in the same request produces a shallow plan on
  both. Split across days.
- **Always name a performance budget.** Without one, the plan will assume the source site's
  15.8k-pixel, 210-image page and come back unbuildable at the client's budget.
- **State how much real imagery exists.** The case grid, client list, and team sections all
  collapse without it — cheaper to learn that from the plan than from a half-built page.
- **Follow up with a `review` request** on what got built, inside the same 30-minute thread
  window if possible.
- **PRECISION: name the frame count and tier plan up front.** "One 43-frame hero sequence at two
  tiers" is a constraint the plan can build around; leaving it open produces a plan assuming three
  scenes and 49 first-paint assets, which is unbuildable at most budgets.
- **PRECISION: state whether real benchmark data with a named baseline exists.** Without it the
  proof module cannot be planned, and it is the register's centrepiece — better to learn that from
  the plan than after building the bars.
