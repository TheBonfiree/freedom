# freedom

A Claude Code skill supplying visual direction for marketing sites that must read as expensive —
agency and studio sites, portfolios, product and hardware landing pages, spec pages.

It is a style direction, not a template. There is no starter code here and no components; the skill
is a set of decisions to make before writing markup, and the reasoning for each.

## The two registers

Every project routes to one of two registers before anything else is decided:

- **STUDIO** — the subject is a *maker*: an agency, studio, portfolio, capability deck. The work is
  the proof. Four faces in four roles, one rationed accent, hard black-to-white chapter flips.
- **PRECISION** — the subject is a *thing*: a product, hardware, spec-bearing software. The numbers
  are the proof. One family in two optical sizes, no flat accent, a near-white ladder with dark
  tiles floating on it, scroll-scrubbed scenes.

Mixing them produces a page that reads as neither. The gate that routes a brief to one or the other
is the first section of `SKILL.md`.

## Layout

```
SKILL.md               decision zero, the command surface, the hard rule, six moves, ship gates
reference/
  tokens.md            palette, type scale, tracking, layout — split by register
  sections.md          nine STUDIO section archetypes
  product.md           eight PRECISION section archetypes
  motion.md            STUDIO triggered effects, with reduced-motion fallbacks
  scroll-scenes.md     PRECISION scrubbed scenes, canvas sequences, sticky stages
  entry.md             loaders and opening choreography — opens with the case against a loader
  fable-request.md     request blocks for handing either register off for planning
```

Read one reference file, not all of them. Each archetype carries a swap-in question; a section whose
question the project cannot answer gets cut rather than filled with placeholder.

## Usage

```
/freedom <brief>                    run the register gate, then design
/freedom studio|precision <brief>   force the register, skip the gate
/freedom gate <brief>               decide the register and stop
/freedom tokens|sections|motion|scenes|entry|fable <target>
```

The register persists for the session once decided or forced, so a mid-build call does not re-derive
it from a fragment that carries no signal.

Pairs with `impeccable`, which owns process — phases, critique, verified passes. Run `freedom` first
to lock the register, then `impeccable` against it. If the two conflict, process wins.

## Provenance

Every value in this skill was measured on a live page via `getComputedStyle` and
`getBoundingClientRect`, never estimated. The teardowns backing it are kept privately and are not
part of this repo.

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
