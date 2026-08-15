---
name: freedom
description: Use when building or redesigning a marketing site that should read as premium — agency and studio sites, portfolios, product and hardware landing pages, spec pages, back catalogues and work archives, capability decks made into pages. Trigger on "make it feel premium", "bold editorial site", "brutalist type", "agency site", "studio landing page", "big type hero", "HOBRO style", "Apple-style product page", "spec page", "scroll-scrub", "portfolio index", "filterable work grid", "release catalogue", "premium product marketing", or any brief asking for a site that must not look templated. Supplies four concrete style registers — STUDIO (loud, four-font, black/white chapters), PRECISION (quiet, optical-size pair, near-white ladder, scrubbed scenes), CATALOGUE (dark ruled scaffold, flat type ladder, imagery carries the volume) and DIEGETIC (the page as artifact — an OS, a terminal, a period interface; explicit request only) — each with tokens, section archetypes, and motion with reduced-motion fallbacks.
user-invocable: true
argument-hint: "[studio|precision|catalogue|diegetic|gate · tokens|sections|motion|scenes|entry|ship|fable|fable skill] [brief or target]"
allowed-tools:
  - Read
---

# Freedom

Style direction for a client who has enough real proof to fill a page — eight or more case studies
with consistent imagery, benchmark data with a named baseline, or a catalogue deep enough to browse
— and whose claims pass legal or procurement review before they ship. That tier is the whole brief:
footnotes are mandatory rather than decorative, uncited superlatives get cut, and no section can be
filled with placeholder to hold its shape.

Four registers, each from a live teardown of a site that solves the problem a different way, sourced
value by value in the vault:

- STUDIO — the `Hobro-Digital-Teardown` note
- PRECISION — the `Apple-Mac-Studio-Teardown` note
- CATALOGUE — measured from `denmu.com/portfolio`, 2026-08-14
- DIEGETIC — measured from `robbyyeager.com`, 2026-08-14

The older teardowns are kept privately and are not distributed with this skill; the two 2026 ones
are summarised inside `catalogue.md` and `diegetic.md` themselves.

**Relationship to `impeccable`:** impeccable supplies the process — phases, critique, verified
passes; this skill supplies the visual direction those phases execute. Run both. On conflict,
impeccable's process wins and these aesthetics fill the gaps it leaves open.

## Decision zero — pick the register

Before anything else, including the font decision, decide which register the project is in. The
question is what the page is *for*: is the subject the **maker**, the **thing**, or the **volume**?

| | STUDIO | PRECISION | CATALOGUE |
| --- | --- | --- | --- |
| Subject | a **maker** — agency, studio, portfolio, capability deck | a **thing** — product, hardware, spec-bearing software | a **volume** — a back catalogue, release list, archive |
| What proves it | the work | the numbers | the count |
| Visitor's job | be convinced | be persuaded by evidence | browse and filter |
| Chapters | hard `#000` ↔ `#fff` | near-white ladder `#fafafa` ↔ `#fff` → `#f5f5f7` | none — one dark ground throughout |
| Type | four faces, four jobs | one family, two optical sizes | one face, three sizes, no display cut |
| Colour | one accent, cursor only | no flat accent — gradients on proof marks | monochrome, one blend-mode moment |
| Layout | no container, 12px gutters | two grids: 980px prose, full-bleed media | ruled scaffold out of phase with the content grid |
| Motion | triggered reveals | scrubbed scenes | four effects, none over 0.4s |
| Sections | `reference/sections.md` | `reference/product.md` | `reference/catalogue.md` |

Mixing them produces a page that reads as none of them — a spec table in STUDIO looks unfinished, a
drag gallery in PRECISION looks like a different site, a 176px headline in CATALOGUE kills the flat
ladder the register is built on. If the brief spans two (a studio launching its own product), build
PRECISION and borrow only STUDIO's mono metadata layer.

**CATALOGUE against STUDIO** is the close call. STUDIO argues; CATALOGUE lists. Eight to a dozen
cases, as evidence for hiring the maker, is STUDIO with a case grid. Twelve or more items where the
visitor arrives intending to *find one* is CATALOGUE. The question is what the page is **for**, not
what the client treasures most — a label with 200 releases and a beloved essay about its history is
CATALOGUE with an essay in it.

**A maker with fewer than twelve pieces whose visitor still arrives to browse** — a photographer
wanting a contact sheet — is STUDIO with CATALOGUE's grid discipline: the flat type ladder and the
uniform tile, without the dark ground or the filter. The one sanctioned borrow between these two,
because the count rule and the maker-or-volume rule are independent and a brief can fail one.

**There is a fourth register, DIEGETIC — the page that pretends to be an artifact.** Decision zero
never selects it, because a costume is never the right answer to a brief that did not ask for one,
and it demands a concept the client can still defend two years from now. See
`reference/diegetic.md`, which opens with the case against it.

**When the brief itself names the artifact** — the client asked for the 1996 desktop, the tape
machine, the ledger — the gate still does not select it, but you do not silently build something
else either. Run decision zero, report the register it yields, then **stop and put the choice to
whoever asked you**: name that the client's concept is DIEGETIC, quote `diegetic.md`'s two
conditions, and say which of them this client meets. Build only after an answer. A brief where the
client has already accepted the cost is exactly the case the register exists for; quietly delivering
the safe register instead is a worse failure than picking the costume would have been.

## Commands

**Register:** `/freedom <studio|precision|catalogue> [brief]` forces the register, skips the gate,
and locks it for the session. `/freedom diegetic [brief]` does the same for the explicit-only fourth
register. `/freedom gate [brief]` runs decision zero and stops — it reports the register and the
reason, and builds nothing.

Everything below routes to exactly one reference file. The argument after the token is the target.

| Token | Reads |
| --- | --- |
| `tokens` | `reference/tokens.md`, the locked register's half only — STUDIO and PRECISION. CATALOGUE and DIEGETIC carry their tokens in their own files |
| `sections` | `reference/sections.md` (STUDIO), `reference/product.md` (PRECISION), `reference/catalogue.md` (CATALOGUE), `reference/diegetic.md` (DIEGETIC) — one token, the locked register picks the file |
| `motion` | `reference/motion.md` — STUDIO triggered effects |
| `scenes` | `reference/scroll-scenes.md` — PRECISION scrubbed scenes |
| `entry` | `reference/entry.md` — its argument against a loader comes first |
| `ship` | `reference/ship.md` — the pre-ship pass: the non-negotiables, cross-register and per-register |
| `fable` | `reference/fable-request.md`, emitting the locked register's request block |
| `fable skill` | `reference/fable-request.md`, emitting the skill-maintenance blocks instead — an audit or feature request about this skill, not about a client build. Register-independent; it does not run decision zero or lock a register |

Routing:

- **No token:** treat the whole argument as the brief and run decision zero. The default path.
- **Leading token matches the register block or the table:** act on it; the rest is the target.
- **Out-of-register tokens** — `motion` under PRECISION, `scenes` under STUDIO, either one under
  CATALOGUE or DIEGETIC: say so and redirect to the in-register file instead of reading the one
  asked for. An explicit verb must not become a way to smuggle in a cross-register effect.
- **Ambiguous first word:** prefer the brief reading and say which was taken. A client named "Studio
  Mono" is a brief, not a register switch.
- **A brief that describes a concept** — a 90s desktop, a terminal, a fake magazine — still runs
  decision zero and gets a real register. If the concept is the *client's own stated request*, stop
  after reporting the register and ask, per decision zero above. Never build past a register
  conflict without surfacing it.
- **`fable skill`:** the only path that is about this skill rather than a page. It needs no register,
  so do not run decision zero for it, and do not let it change a register already locked.

**The register persists once decided.** Later calls assume it rather than re-deriving it from a thin
fragment — `motion hero` carries no maker-or-thing-or-volume signal and must not re-open the
question. Only an explicit `studio`, `precision`, `catalogue` or `diegetic` token switches it, and a
mid-build switch invalidates decisions already made, so say so out loud when it happens. Nothing
enforces this but the instruction: restate the register whenever acting on it, and if it has been
lost, ask rather than guess.

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

**In CATALOGUE —**

1. **The scaffold pitch** — the divisor that rules the page, which must differ from the number of
   content columns at every breakpoint.
2. **The one type size** everything structural shares. There is no display cut in this register;
   deciding the small size *is* deciding the hierarchy.

**In DIEGETIC —**

1. **The artifact** — which object, which year, which condition. "Retro computer" is not an answer.
2. **The escape hatch** — how a visitor who does not want the game reads the same content, and how
   they get back.

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
*CATALOGUE:* the inverse — one face, three sizes, no display cut at all, and the imagery carries
what type would have. A face used for two jobs is what fails in the first two; a headline is what
fails in the third.

**2. Loud colour is rationed.**
*STUDIO:* one hue, living on the custom cursor and a few micro-marks. It never fills a button,
never sets a heading. Scarcity is the whole effect — an accent-coloured hero CTA collapses this
register into a template instantly.
*PRECISION:* there is no flat accent at all. Colour arrives only as the gradient, only on proof
marks and component callouts. *CATALOGUE:* monochrome, with one `mix-blend-mode: difference` label
standing in for the accent.

**3. Chapters alternate; the inversion replaces dividers.** Full-bleed sections flip, which is
what lets the page drop eyebrow headings and rules entirely. STUDIO flips hard, near-black to
white. PRECISION runs the same device at low amplitude — a three-value near-white ladder with no
visible seam — and gets its drama from dark tiles floating on that ground. CATALOGUE has no
chapters at all: one ground, and the ruled scaffold does the dividing.

**4. Numerals are structure.** Caption every image in mono or the small cut. Number sections
`(01)`, items `[1]`, years `23-26`; in PRECISION, footnote every claim. **Not in CATALOGUE**, where
the order changes under the visitor's hand at the filter and a stable ID code replaces the index.

**5. Motion is the product, and it has a budget.** STUDIO: smooth scroll, character-level heading
reveals, marquees, drag galleries — `reference/motion.md`. PRECISION: canvas frame sequences,
sticky stages, scrubbed transforms — `reference/scroll-scenes.md`. CATALOGUE: four effects, none
over 0.4s. DIEGETIC: window behaviour and an ambient system with a device count. Decide the budget
up front and cut whole scenes to stay inside it rather than thinning every effect into mush.

**6. Proof has a form.** Numbers are designed objects, not sentences. The multiplier splits value
from unit into separate elements so the unit can be tracked and baselined on its own; the raw
datum lives in a `data-` attribute on the mask, not in an inline style; the bar is an `<hr>` with
`aria-hidden`, doing decorative work while staying semantic. A page that renders "2.9x faster" as
body copy has thrown away its strongest visual. PRECISION-native — `product.md` §4 for the markup,
`sections.md` for what changes when a STUDIO page borrows it.

## Non-negotiables

They live in `reference/ship.md` — cross-register rules first, then a short list per register.
Read it before shipping, and read it again if a build has drifted. Three that decide the shape of
the work rather than its finish, so they belong here too:

- **`prefers-reduced-motion` for every effect, decided at build time**, not retrofitted. None of the
  four source sites got this fully right; do not inherit any of them.
- **Motion has a budget and it is a number** — frames and tiers, or effects and durations, or
  ambient devices. Cut whole scenes to stay inside it rather than thinning every effect into mush.
- **Check the count before committing to a section that needs volume.** Eight cases for a STUDIO
  case grid, a named baseline for a PRECISION proof module, twelve items for CATALOGUE at all.

## References

Read the one you need; do not load them all.

- `reference/tokens.md` — palette, type scale, tracking and layout rules for STUDIO and PRECISION.
- `reference/sections.md` — nine STUDIO archetypes, each with its swap-in question, plus borrowing
  the proof form.
- `reference/product.md` — eight PRECISION archetypes, each with its swap-in question.
- `reference/motion.md` — triggered-effect recipes with reduced-motion fallbacks (STUDIO).
- `reference/scroll-scenes.md` — scrubbed scenes, canvas sequences, sticky stages (PRECISION).
- `reference/catalogue.md` — the whole CATALOGUE register: tokens, archetypes, motion, density.
- `reference/diegetic.md` — the whole DIEGETIC register, opening with the case against it.
- `reference/entry.md` — loaders, gates, opening choreography, heavy-asset delivery. Every
  register. Read it before adding a loader — its first section is the argument against one.
- `reference/ship.md` — the pre-ship pass. Cross-register non-negotiables, then per register.
- `reference/fable-request.md` — request blocks for handing a register to Fable for planning, and
  for auditing this skill.
