# STUDIO section archetypes

For the agency / studio / portfolio register. The PRECISION set — product, spec, proof,
comparison — is in `product.md`. Do not mix the two sets on one page.

Nine patterns, in the order they work best. Each ends with the question to answer before reusing
it. A section whose question has no good answer should be cut, not filled with placeholder.

## 1. Hero — video plus wordmark

Full-viewport muted looping video, heavily blurred or colour-graded so it reads as a colour
field rather than as footage. The company name across it at display size in white. Under the
name, a three-line mono block of bare facts.

> What three facts about this client belong in the mono block? (Category, founding year, and
> place is the default triad.)

## 2. Manifesto — first chapter flip

Black background. One uppercase statement, around 25 words at 22px, of what the company makes
and why. Nothing else in the section.

> What is the one sentence the client would defend in a meeting?

## 3. Capability list

Heading built from two colliding word layers — a ghost outlined word behind a solid one, offset
so they overlap. Below it, a long unbroken run of specific service names in uppercase. No icons,
no cards, no grouping.

> Can the client name fifteen concrete services? Under ten, this section looks thin and should
> become a four-item version of section 4 instead.

## 4. Numbered features

Four rows, `(01)` through `(04)`. Each row: the service name at 60px, two or three mono keywords
beside it, and an autoplaying muted video that starts when the row enters view. Hairline rules
between rows.

> Which four things does the client want to be hired for? Exactly four — three looks sparse,
> five breaks the rhythm.

## 5. Case grid

Three-up image grid, 14px mono caption under each image, filter counts in the heading
(`BRANDING (7) WEB (13) PRODUCT (5)`). Clicking a case opens a detail panel; pre-render the
panels in the DOM and reveal them rather than fetching.

> Are there at least eight cases with real, consistent imagery? Below that, use a single
> featured case instead of a grid. Above about twelve, with the visitor arriving to *find* one
> rather than be convinced, the grid is straining — that is CATALOGUE, `catalogue.md`.

If the count stays under twelve but the visitor still arrives to browse — a photographer's series, a
maker's shelf — this grid takes CATALOGUE's discipline: every tile the same size and crop, captions
flat at one size, no featured item. It keeps STUDIO's ground, chapters and accent. That borrow is
sanctioned in `SKILL.md`'s gate; going further and importing the dark ground or the filter is the
mixing the gate forbids.

## 6. Full-bleed CTA

Black. A soft question in the italic serif over a hard command at display size. Two thin arc
strokes flanking it.

> What is the two-beat CTA? Question then command — "Got Project?" over "LET'S TALK".

## 7. Clients

Sector-grouped list with counts. Set as text rather than logo images wherever the name is
recognisable — mixed-quality logo files are the fastest way to cheapen this section.

> Does the client have names worth listing? An under-filled version is worse than no section.

## 8. Team

Stacked display-size caps for the heading, with one outlined letterform overlapping its solid
twin. Portraits numbered `[1]` onward, greyscale, on one neutral plate.

> Are the photos shot on a single background? Mixed-source headshots destroy this section — if
> they are mixed, crop hard to greyscale squares or drop the section.

**The solo practitioner.** A one-person consultancy has no team section and usually no client list
worth setting. Both get cut, and what replaces them is a single portrait chapter — one full-bleed
image, the display-size caps treatment from this section applied to the person's own name, and the
practice's terms beside it. A solo portfolio runs about six sections, not nine; that is the normal
shape, not a thin version of the agency page.

## 9. Footer

Two columns. Left: the year range as a single hyphenated numeral pair at display size
(`23-26`), over `© CLIENT` and a privacy link, with a looping video beneath. Right: address,
phone, email — all mono, all uppercase, separated by bullet marks — plus a repeat of the primary
CTA and social icons.

> Founding year to current year, hyphenated. Update it annually.

## Proof, when the numbers are real

SKILL.md's sixth move tells a STUDIO page with real metrics to steal PRECISION's proof form. The
form itself is not duplicated here — read `product.md` §4 for the markup: an `<hr>` bar carrying
its datum in `data-bar-width`, a `<figure>` splitting value from unit into separate spans, and a
footnote marker on every claim.

Three things change on the way across:

- **The gradient does not come with it.** STUDIO has no gradient. The bar is the accent, hairline
  weight, on the chapter's own ground — black on white, white on black.
- **The figures take the display face, the units and footnotes take mono.** Value at 60px or
  larger, unit and marker at 14px. PRECISION's split into two optical cuts has no equivalent here.
- **It is a chapter, not a band.** Full-bleed, alternating with its neighbours like every other
  STUDIO section, 12px gutters. Do not centre it in a column.

> Are there at least three metrics with a stated source or baseline? Two reads as a boast, not a
> proof — cut to a single figure in a headline instead.

## When the content is audio, or the assets do not exist yet

Five of the nine archetypes above assume video or photography. Two cases come up constantly and
neither is a reason to abandon the register.

**Audio as the payload** — a composer, a sound designer, a podcast. The clip player is a mono
transport strip, not a rounded media widget: a play control, a hand-drawn waveform or level bar in
the accent, the duration as a numeral, all at the mono size on the chapter's own ground. It is a
label that plays. Audio does not count against the motion budget, but its transport still needs a
visible focus ring and a keyboard path, and nothing on the page may depend on hearing it.

**No assets yet.** Drawn substitutes are legitimate where placeholders are not: a graded field, a
rendered bar, a type-only plate. The rule against filling a section with placeholder is about
*claims* — invented cases, fake clients, imaginary metrics — not about a colour field standing in
for a photograph that is genuinely being shot next week. Say which is which in the handover.

## Repetition rule

One conversion goal, three placements: a dismissible corner card in the hero, a full-width band
mid-page, and a button in the footer. No second competing ask anywhere on the page. If the
client wants two CTAs, make one of them the only one and demote the other to the footer.
