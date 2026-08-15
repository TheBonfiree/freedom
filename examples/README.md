# Examples

Four single-file pages built with this skill. Each one is self-contained: open it in a browser,
no build step, no dependencies, no network requests. They exist so a register can be read as a
finished page rather than as a description of one.

Every page invents its client. The companies, addresses, phone numbers and job records are
fictional, and the email domains are `.example`.

| File | Register | Built by | State |
|---|---|---|---|
| `bellwether.html` | STUDIO | authored, then audited | Layout pass and scroll work applied |
| `cold-storage.html` | DIEGETIC | authored, then audited | Layout pass and CRT work applied |
| `korero.html` | CATALOGUE | cold test run — an agent given only a client brief | As produced |
| `ilves.html` | STUDIO | cold test run — an agent given only a client brief | As produced |

The two cold-run pages are kept as they came out of the test, not polished afterwards. They are
evidence about what the skill produces without a human steering it, which is only useful if they
stay unedited.

## What the two audited pages demonstrate

**`bellwether.html`** — STUDIO. Four faces, chapters that flip black to white, no container, 12px
gutters. Scroll drives one continuous idea: the bench field recedes as the hero leaves, each
chapter's ink arrives as a wipe rather than a cut, and case panels morph out of the card that
opened them via View Transitions. All of it sits behind `@supports (animation-timeline: view())`
and `prefers-reduced-motion: no-preference`; without either, the page renders as static chapters.

**`cold-storage.html`** — DIEGETIC. The page presents itself as a 1988 amber-phosphor file browser.
A WebGL2 fragment shader draws the shadow mask, aperture grille, drifting bar and phosphor grain,
and composites them *over* the live DOM — the page is never rasterised to a texture, so text stays
selectable, findable and readable by assistive technology. Power-on opens the raster; the boot
line arrives at a plausible baud rate as a CSS clip, with the full string in the DOM from the first
frame; switching to the plain reading layer collapses the beam to a line first.

Both pages carry the register's escape hatch. DIEGETIC's is explicit — `F9` or the status-bar key
swaps the artifact for an ordinary document containing the same information, and that document is
the more structured of the two, not the less.

## Fallbacks

Nothing here is required for the page to work.

- No WebGL2: the tube never lights and the flat amber screen remains.
- No View Transitions: the panel swap simply happens.
- No scroll-timeline support: the `@supports` block never applies.
- `prefers-reduced-motion: reduce`: one still shader frame, no boot, no type-on, no beam collapse,
  no scroll-driven movement, no marquee.
- No JavaScript: every document is already in the HTML and all of it is shown.
