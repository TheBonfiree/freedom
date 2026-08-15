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

## Skill-maintenance request block

For asking Fable to improve this skill rather than plan a client build. Two requests, sent in
order — the audit finds what is wrong, the feature request decides what to add. Same no-repo-access
assumption: the file list has to be pasted, with line counts, or the plan comes back proposing
files that already exist.

```
PROJECT:     freedom — a Claude Code skill that supplies visual direction for premium
             marketing sites. Not a template, no starter code. Four mutually exclusive
             registers: STUDIO (loud, four fonts, black/white chapters, triggered
             motion), PRECISION (quiet, one family in two optical cuts, near-white
             ladder, scrubbed canvas scenes), CATALOGUE (dark ruled scaffold, flat
             three-size type ladder, imagery carries the volume) and DIEGETIC (the page
             as artifact — an OS or period interface; the gate never selects it).
CLIENT TIER: Single user, no approval chain. Skill is invoked by an agent that reads
             one reference file per task, so every file must stand alone.
GOAL:        Audit for gaps and inconsistencies, ranked by how much each one costs a
             build. Nothing else this request.
WHAT I HAVE: Structure (pasted — no repo access):
             - SKILL.md, <n> lines: register gate, routing table, the hard rule, the
               six moves
             - reference/<file>.md <n> lines — <register>: <what it covers>
               <one line per reference file, with its line count and register>
             Asymmetries I already see: <the ones you can name, so the audit spends its
             attention elsewhere>
CONSTRAINTS: Files stay independently readable — an agent loads one, never all. No
             reference file past ~210 lines, except a register whose single file carries
             its tokens, archetypes and motion together. The registers must not blur into
             a single house style. No starter code, no component library, no named
             typefaces.
DELIVERABLE: audit
```

```
PROJECT:     freedom — Claude Code skill, visual direction for premium marketing sites,
             two registers: STUDIO (loud editorial) and PRECISION (quiet spec page).
             Structure as pasted in my previous request.
CLIENT TIER: Single user, no approval chain. One reference file read per task.
GOAL:        Propose new capabilities, ranked, with the cost of each in lines and in new
             concepts an agent must hold. Nothing else this request.
WHAT I HAVE: The audit findings from the previous request, plus the file list above.
             Candidate directions I have already considered, so you can rank them
             against your own rather than repeat them: <list them>
CONSTRAINTS: Every addition names what it replaces or shrinks — the skill does not grow
             past ~<n> lines. New reference files must be readable alone. Nothing that
             turns direction into a template. No dependency on a specific framework.
DELIVERABLE: feature proposals
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
- **Maintenance: audit and features are two requests, not one.** Same rule as architecture and
  copy — asked together, the audit degenerates into a wishlist and the features arrive unmotivated.
  Send the audit first and feed its findings into the second request.
- **Maintenance: paste the file list with line counts.** Without them the plan proposes files that
  already exist, and it cannot tell which register is under-served or where the skill is heaviest.
- **PRECISION: state whether real benchmark data with a named baseline exists.** Without it the
  proof module cannot be planned, and it is the register's centrepiece — better to learn that from
  the plan than after building the bars.
