# DIEGETIC — the site that pretends to be an artifact

An operating system, a terminal, a magazine spread, a cassette deck, a card catalogue. The page
stops presenting content and starts *being a thing that contains* content.

**The gate never picks this register.** It is reachable only by typing `/freedom diegetic`, because
a costume is never the correct answer to a brief that did not ask for one. Values below were
measured from `robbyyeager.com` — "RobbyOS", a 1996 desktop — at 1440×900 on 2026-08-14. This is the
register's only file: tokens, archetypes and motion together.

## First: the case against it

Two conditions, and **both** must hold. If either fails, build STUDIO or CATALOGUE and put the idea
in a side project.

1. **The artifact says something true about the subject.** RobbyOS works because the client is a
   brand strategist selling taste and systems thinking, and a 1996 desktop is a system with taste —
   the costume argues the case. A law firm as a Game Boy argues nothing.
2. **The audience rewards the detour.** A recruiter browsing twelve portfolios will spend the extra
   thirty seconds. A buyer comparing three vendors under deadline will not, and the concept becomes
   an obstacle between them and a phone number.

A third test, cheap and clarifying: **can the client defend this in two years, to someone who did
not commission it?** A concept has to survive the novelty wearing off.

## The hard rule

Before any markup, write down two things:

1. **The artifact** — precisely which object, from which year, in which condition. "Retro computer"
   is not an answer; "Windows 95 at 800×600 on a CRT, with the sound scheme on" is.
2. **The escape hatch** — how a visitor who does not want the game reads the same content anyway,
   and how they get back. Design it now, not after the chrome is built.

## 1. Chrome tokens

The measured Win95 set. Treat the *roles* as the register and the values as one instance of it:
every artifact has a face colour, a light edge, two shadow depths, a title fill and a selection
colour.

```css
:root {
  --face:  #c0c0c0;   /* panel and window ground */
  --hi:    #ffffff;   /* bevel light — top and left */
  --lt:    #dfdfdf;   /* inner light, one step down */
  --sh:    #808080;   /* bevel shadow — bottom and right */
  --dksh:  #000000;   /* outer bevel shadow */
  --title: #000082;   /* active titlebar, and link colour */
  --title2:#1084d0;   /* titlebar gradient end */
  --sel:   #000082;   /* selection */
  --desk:  #0a8a8a;   /* the desktop itself */
}

.window {
  background: var(--face);
  border-radius: 0;                          /* never round anything in this register */
  box-shadow: 2px 2px 0 rgba(0, 0, 0, .4);   /* hard offset, no blur */
  border-block-start: 1px solid var(--hi);   /* the bevel, drawn not simulated */
  border-inline-start: 1px solid var(--hi);
  border-block-end: 1px solid var(--dksh);
  border-inline-end: 1px solid var(--dksh);
}
.titlebar {
  block-size: 36px;
  background: linear-gradient(90deg, var(--title), var(--title2));
  color: #fff; font: 700 13px/1 var(--ui);
}
```

**The bevel is the whole material.** Light source is top-left, always, on every raised element;
pressed states invert it. One blurred shadow anywhere and the illusion drops — period interfaces had
no blur, and the eye knows it before the mind does.

> What is the material? Bevelled plastic, printed paper, brushed metal, phosphor. Name it once and
> every surface on the site obeys it.

## 2. Four font roles

Different roles from every other register in this skill, because an interface is not a document.

1. **UI face** — the system font of the artifact. Tahoma 13px here, and it sets *everything*
   chrome: titlebars, menus, buttons, labels.
2. **Period display** — a face that could only come from the era. Pixelify Sans at 31px/34.72
   (1.12) with **+0.4px tracking**. Headlines only, and only inside content, never in chrome.
3. **Terminal mono** — VT323 or equivalent, for anything pretending to be output.
4. **Readable prose** — 13px at 1.55 line-height. The one place where legibility beats the costume:
   the actual writing about the actual work.

**Tracking goes positive in this register**, against the negative-above-16px rule that STUDIO and
PRECISION share. Period faces were drawn for low resolution and open up rather than tighten. It is
the clearest signal that you cannot carry another register's type rules across.

Everything is small — 13px chrome, 31px headline. There is no 96px moment anywhere. Scale is the
artifact's, not the brand's.

> Is there a period face that is still readable, or only one that is charming? Charming goes in the
> chrome. Readable carries the prose.

## 3. The escape hatch

**Non-negotiable.** Every diegetic build ships a second, plain reading of the same content, and the
door swings both ways.

RobbyOS does it as a fake system notification — "A newer version of this portfolio is available.
RobbyOS → 2026 Edition" — with an `Install update` button, and the modern layer carries a
`Back to '96` control in its header. The modern layer is a complete second art direction living in
the same document: `#0b0b0c` ground, `#f1efe9` text, an aurora gradient, a custom cursor with a
ripple, `#111` cards at radius 0, Inter for prose and a heavy grotesque for the wordmark.

```html
<div id="shell">…the artifact…</div>
<div id="modern" hidden>…the same content, plainly…</div>
```

Rules that make it work rather than merely exist:

- **Both directions.** A one-way exit tells the visitor the concept was a hazard.
- **Same content, not a summary.** The plain reading is not a stripped consolation; it is the site
  a different client would have got.
- **Offered inside the fiction.** A system update dialogue, a "print view", a "lights on" switch.
  A plain grey button labelled "Accessible version" concedes the whole idea.
- **Sticky.** Remember the choice, and honour it on the next visit.

> If the plain reading were the only thing you shipped, would the client still have a good site? If
> not, the concept is carrying work the content should be doing.

## 4. Self-declaration

The first thing a visitor reads says the concept is deliberate. RobbyOS puts it in the opening
window: *"Yes, it's a 1996 desktop, art-directed in 2026. A deliberate concept: taste, systems
thinking, and interaction design, disguised as nostalgia."*

Without it, a share of visitors spend their first ten seconds deciding whether the site is broken,
old, or a joke at their expense — and that is the share that leaves. One sentence, in the fiction's
own voice, converts confusion into complicity.

## 5. The ambient system

A costume is a skin; an artifact has behaviour when nobody is touching it. This is what separates
the register from a themed template. From the source:

| Device | Behaviour | Budget |
| --- | --- | --- |
| Idle screensaver | Takes over after ~60s idle, more than one variant, wakes on any input | ≤2 variants |
| Rotating notices | A period-flavoured fact toast, new text each appearance | 1 slot, ≥20s apart |
| System clock | Real time, in the taskbar, ticking | 1 |
| Side apps | Openable toys — a paint program, a chat client, a quiz | ≤4, none required |
| Fake update prompt | The escape hatch, dressed as the artifact | 1 |

**Budget the ambience the way PRECISION budgets frames.** Every device is a thing to build, test on
a phone, and keep accessible. Four devices done fully beat twelve half-wired ones, and the side apps
are where the schedule goes.

The desktop itself: 17 icons at 84×56 on an 88px vertical pitch, in a single left column.

> Which device would the client demo first? Build that one properly. Cut anything that only exists
> to prove the theme is thorough.

## 6. Windows, focus, and the keyboard

The dangerous part. A fake window manager is a real one to anyone using a keyboard or a screen
reader.

- Windows are `role="dialog"` with `aria-labelledby` on the titlebar text. Opening moves focus into
  the window; closing returns it to whatever opened it.
- **Focus is trapped only in modals.** A window that is merely on top does not trap — the visitor
  must be able to tab out to the desktop.
- Icon grids are one tab stop with roving `tabindex`, arrow keys to move, Enter to open. Seventeen
  icons must never be seventeen tab stops.
- Bevels, titlebar gradients, the taskbar and the screensaver are decoration: `aria-hidden="true"`.
- Every drag has a keyboard equivalent, or the thing being dragged does not matter. Do not make
  window position load-bearing.
- Escape closes the top window. Visitors will try it.
- The screensaver must not steal focus, and must never fire under
  `prefers-reduced-motion: reduce`.
- Anything genuinely unnavigable in the fiction has one honest fallback: the escape hatch of §3.

## 7. Motion

| Effect | Recipe | Reduced motion |
| --- | --- | --- |
| Window open | Scale 0.98 → 1 and opacity, 0.12s, no easing curve fancier than `ease-out` | Appears instantly |
| Window drag | Position follows pointer, no inertia — period interfaces had none | Unchanged; drag is opt-in |
| Screensaver | Idle timer, 2 variants, wakes on input | Never fires |
| Cursor ripple (modern layer) | Small ripple at click point | Cursor hidden, ripple 0.01s |
| Aurora ground (modern layer) | Slow gradient drift | Static gradient |
| Card reveal (modern layer) | Opacity + rise on scroll | `opacity: 1; transform: none` |

The source honours reduced motion in five scoped blocks, all on the modern layer. Match that, and
add the screensaver rule it lacks — an unrequested full-screen animation is the single most hostile
thing this register can do.

## 8. Delivery

RobbyOS ships as one document with a ~148KB inline script and no third-party runtime — no framework,
no animation library. That is the right shape here: the artifact is one closed world, and a
component tree spread across routes fights the illusion every time a page transition breaks it.

- One document, one script, no router. Windows open and close; the URL may follow with
  `history.pushState` so links are shareable.
- No web fonts for chrome — the system stack (`Tahoma, "MS Sans Serif", Geneva, Verdana`) is both
  free and period-correct. Spend the font budget on the period display face only.
- The costume must not cost the content: prose stays in the HTML, readable with JavaScript off,
  even if the chrome is not.

> Is the whole thing under 200KB of script? If it is heading past that, cut side apps, not
> accessibility.
