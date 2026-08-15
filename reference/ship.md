# Ship gates

The pass to run before a page goes out, in any register. Each register's own reduced-motion table
stays in its own file — `motion.md`, `scroll-scenes.md`, `entry.md`, `catalogue.md`, `diegetic.md` —
and this list does not replace them. It catches what falls between files.

## Every register

- **`prefers-reduced-motion` is decided at build time, per effect, not bolted on.** Every effect in
  every register file ships with its fallback named. If the motion lives in JavaScript, branch in
  JavaScript on `matchMedia('(prefers-reduced-motion: reduce)')` — a CSS media query never sees it.
  None of the four source sites got this fully right; do not inherit any of them.
- **Motion has a budget, and it is a number.** Frame count and tier plan (PRECISION), effect count
  and duration ceiling (STUDIO, CATALOGUE), device count (DIEGETIC). Decide it before building and
  cut whole scenes to stay inside rather than thinning everything into mush.
- **A gate needs a timeout, a fallback and real copy in the HTML.** Loaders hang. Ship a
  `<noscript>` block and a path that shows the page anyway. Most pages should have no gate at all —
  `entry.md` opens with that argument.
- **Autoplaying audio needs a visible, keyboard-reachable mute**, and nothing may depend on audio
  to be understood.
- **Anything a custom cursor communicates needs a keyboard-equivalent path.**
- **The document outline is not the type ladder.** One `<h1>`, headings in order, no styled `<div>`
  standing in for a heading — including in registers whose type is deliberately flat.
- **One link per card.** No interactive nodes, and no `tabindex`, nested inside an `<a>`.
- **The page body never scrolls horizontally.** Check it at 1440, 1024 and 390 with a visible
  scrollbar. Full-bleed devices are the usual culprit: `100vw` includes the scrollbar width, so a
  `100vw` element inside a vertically scrolling page overflows by 8–17px. Size full-bleed elements
  to `100%` of a clipping parent instead.
- **Check the count before committing to a section that needs volume.** Case grid, client list and
  team (STUDIO) all look broken under-filled — fewer than eight cases means a different section. In
  PRECISION the same test is the baseline: no stated baseline, no proof module. In CATALOGUE it is
  twelve items with consistent imagery, or the register is wrong.

## STUDIO

- Type running to a 12px gutter breaks below ~380px. Raise the gutter at the small end.
- The accent stays on the cursor and micro-marks. One accent-coloured button undoes the register.

## PRECISION

- **Every scrub scene needs a static frame under reduced motion** — the frame at the scene's
  narrative peak, not frame `0000`, and not a slowed scrub.
- **Scrub scenes cost real bytes.** One sequence at 90 frames across three tiers is a budget line.
- **Footnote markers need `aria-label="Footnote N"` and a real in-page target.** A bare superscript
  numeral is an uncitable citation.
- The prose column never exceeds ~980px, even though media runs full-bleed.

## CATALOGUE

- The scaffold divisor and the column count stay different **at every breakpoint**, including the
  small end, or the two-grid effect collapses into a single grid.
- The sticky duplicate of the filter is `aria-hidden`; exactly one copy sits in the tab order.
- Type does not scale with the viewport. The flat ladder is the register.

## DIEGETIC

- **The escape hatch ships, works in both directions, and is offered inside the fiction.** It is the
  register's entry fee, not a nicety.
- **The concept declares itself** in the first thing the visitor reads.
- Fake windows are `role="dialog"`, move focus on open, return it on close, and trap focus only
  when modal. Escape closes the top one.
- Icon grids are one tab stop with roving `tabindex`, not one stop per icon.
- Bevels, titlebars, taskbars and screensavers are `aria-hidden="true"`.
- No idle screensaver under `prefers-reduced-motion: reduce`, and it never steals focus.
- Prose is readable with JavaScript off, even where the chrome is not.
