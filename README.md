# freedom

A Claude Code skill supplying visual direction for marketing sites built on real proof — a client
with eight or more case studies and consistent imagery, benchmark data with a named baseline, or a
catalogue deep enough to browse, whose claims pass legal or procurement review before shipping.
Agency and studio sites, portfolios, product and hardware landing pages, spec pages, work archives.

That tier is the constraint the whole skill is shaped around: footnotes are structural rather than
decorative, uncited superlatives get cut, and a section with nothing real to put in it gets removed
instead of padded.

It is a style direction, not a template. There is no starter code here and no components; the skill
is a set of decisions to make before writing markup, and the reasoning for each.

## The four registers

Every project routes to one register before anything else is decided. The gate picks among the
first three; the fourth is explicit-only.

- **STUDIO** — the subject is a *maker*: an agency, studio, portfolio, capability deck. The work is
  the proof. Four faces in four roles, one rationed accent, hard black-to-white chapter flips.
- **PRECISION** — the subject is a *thing*: a product, hardware, spec-bearing software. The numbers
  are the proof. One family in two optical sizes, no flat accent, a near-white ladder with dark
  tiles floating on it, scroll-scrubbed scenes.
- **CATALOGUE** — the subject is a *volume*: a back catalogue, release list, work archive. The count
  is the proof, and the visitor came to browse. One dark ground, one face at three sizes with no
  display cut, a ruled scaffold deliberately out of phase with the content grid.
- **DIEGETIC** — the page pretends to be an artifact: an operating system, a terminal, a period
  interface. Bevelled chrome, a period display face, an ambient system, and a mandatory escape hatch
  to a plain reading of the same content. **The gate never selects it** — `/freedom diegetic` only.

Mixing them produces a page that reads as none of them. The gate is the first section of `SKILL.md`.

## Layout

```
SKILL.md               decision zero, the command surface, the hard rule, six moves
reference/
  tokens.md            palette, type scale, tracking, layout — STUDIO and PRECISION
  sections.md          nine STUDIO section archetypes, plus borrowing the proof form
  product.md           eight PRECISION section archetypes
  motion.md            STUDIO triggered effects, with reduced-motion fallbacks
  scroll-scenes.md     PRECISION scrubbed scenes, canvas sequences, sticky stages
  catalogue.md         the whole CATALOGUE register — tokens, archetypes, motion, density
  diegetic.md          the whole DIEGETIC register — opens with the case against it
  entry.md             loaders and opening choreography — opens with the case against a loader
  ship.md              the pre-ship pass: non-negotiables, cross-register then per register
  fable-request.md     request blocks for handing a register off for planning, plus
                       audit and feature blocks for improving this skill itself
```

Read one reference file, not all of them. Each archetype carries a swap-in question; a section whose
question the project cannot answer gets cut rather than filled with placeholder.

## Usage

```
/freedom <brief>                    run the register gate, then design
/freedom studio|precision|catalogue <brief>
                                    force the register, skip the gate
/freedom diegetic <brief>           the explicit-only fourth register
/freedom gate <brief>               decide the register and stop
/freedom tokens|sections|motion|scenes|entry|ship|fable <target>
/freedom fable skill                emit the audit / feature request blocks for this skill
```

The register persists for the session once decided or forced, so a mid-build call does not re-derive
it from a fragment that carries no signal.

Pairs with `impeccable`, which owns process — phases, critique, verified passes. Run `freedom` first
to lock the register, then `impeccable` against it. If the two conflict, process wins.

## Provenance

Every value in this skill was measured on a live page via `getComputedStyle` and
`getBoundingClientRect`, never estimated. The STUDIO and PRECISION teardowns are kept privately and
are not part of this repo; the CATALOGUE and DIEGETIC measurements, taken on 2026-08-14, are
summarised inside `catalogue.md` and `diegetic.md` themselves.

Measured facts about a rendered page — a column width, a tracking value, a spacing rhythm — are not
themselves the property of the sites they were observed on, and the techniques described here are
conventions rather than assets. Two things that *are* someone's property and are deliberately absent:
typefaces and imagery. This skill names type by role and by optical relationship, never by file. Any
project using it needs its own font licenses.

The intent is direction, not resemblance. A page built from these registers should not look like the
sites they were derived from.

## Status

Working, in use. The register gate is verified: blind runs on unrelated briefs route correctly,
read only their own register's reference file, and hold the register across chained calls.
