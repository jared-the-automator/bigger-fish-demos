# Bigger Fish — Demo Gallery

### ▶ [Open the live gallery](https://jared-the-automator.github.io/bigger-fish-demos/)

Every demo below is a working page you can open and click, not a code listing.

A cold-email hook for business advisors and coaches: three working demos of small automation
systems Bigger Fish builds for small operators (restaurants, trades, clinics, local services).
Each demo runs entirely in the browser against simulated data — no signup, no backend, nothing
to install — so an advisor can click through one and then hand the same link straight to a
client.

## Demos

- [Missed-call textback](https://jared-the-automator.github.io/bigger-fish-demos/missed-call-textback/) —
  a call rings out unanswered and an automatic text goes to the caller before they give up.
  Toggle "with" and "without" to see the counterfactual side by side.
- [Review routing](https://jared-the-automator.github.io/bigger-fish-demos/review-routing/) — mirrors the
  real Outcome Engineer system. A happy post-visit response routes to a public Google review; an
  unhappy one routes to a private form and a GM alert. Watch the public star average react (or
  not react) depending on the path.
- [Automated intake](https://jared-the-automator.github.io/bigger-fish-demos/automated-intake/) — a short
  client intake form gets validated, filed, booked into an open slot, and confirmed by email and
  text, with the operator's dashboard updating live at each step.

## Technical notes

**Stack.** Plain HTML/CSS/JS, no build step, no framework, no external requests of any kind — no
CDNs, no third-party fonts (system font stack only), no analytics, no trackers. Every page works
opened directly as a `file://` URL and from GitHub Pages with zero configuration. One shared
stylesheet (`assets/style.css`) holds the common layout/component styles; each demo carries its
own page-scoped `<style>` and `<script>` for its specific widgets and state machine.

**Structure**

```
bigger-fish-demos/
├── index.html                    # root gallery, framed for advisors
├── assets/
│   └── style.css                 # shared layout, components, focus states
├── missed-call-textback/index.html
├── review-routing/index.html
└── automated-intake/index.html
```

This mirrors the pattern used in `redesign-portfolio`: a root index links out to
self-contained per-item directories, each with its own `index.html`, so the whole thing serves
as a static site with no routing logic needed.

**Accessibility.** Semantic HTML throughout (`header`/`main`/`footer`/`section`, real `<button>`
and `<label>` elements, `fieldset`/`legend` where it applies), a skip-to-content link on every
page, visible focus outlines on every interactive element (3px outline, not just a color shift),
`aria-live` regions announcing state changes for screen reader users, inline field errors tied to
inputs via `aria-describedby` plus an `aria-invalid` flag and a `role="alert"` error summary on
the intake form, and `prefers-reduced-motion` support that collapses all animation/transition
durations to near-zero. Layout is a single responsive column below ~800px with full-width
touch-sized controls.

**Contrast ratios.** Colors were computed against the WCAG 2.x relative-luminance formula (not
eyeballed) via a small Python script using each color's actual sRGB values. Every text/background
pairing used anywhere on the site clears WCAG AA (4.5:1 normal text, 3:1 large text/UI
components):

| Pairing | Foreground | Background | Ratio |
| --- | --- | --- | --- |
| Primary text on page background | `#f4f6f8` | `#0b0d10` | 17.96:1 |
| Primary text on panel | `#f4f6f8` | `#161a20` | 16.12:1 |
| Primary text on nested panel | `#f4f6f8` | `#1f242c` | 14.39:1 |
| Muted text on page background | `#a9b2bc` | `#0b0d10` | 9.06:1 |
| Muted text on panel | `#a9b2bc` | `#161a20` | 8.13:1 |
| Footer/secondary text on page background | `#7c8792` | `#0b0d10` | 5.32:1 |
| Accent (links, focus ring) on page background | `#7fc4ff` | `#0b0d10` | 10.42:1 |
| Accent on panel | `#7fc4ff` | `#161a20` | 9.35:1 |
| Success accent on page background | `#7fe0a0` | `#0b0d10` | 12.11:1 |
| Danger accent on page background | `#ff8f8f` | `#0b0d10` | 8.87:1 |
| Amber accent on page background | `#ffc266` | `#0b0d10` | 12.19:1 |
| Solid primary button text on button fill | `#ffffff` | `#2f6fb0` | 5.22:1 |

The full set of variables and this table (kept in sync) live at the top of
`assets/style.css`.

**No invented claims.** Nothing on this site names a real client, quotes a testimonial, or cites
a statistic. Every name, phone number, and review shown is placeholder demo data generated
client-side. The "how it's built" note at the bottom of each demo names the real moving parts
(webhook, scheduler, SMS gateway, CRM row, email API) that a production version uses — the demo
itself simulates all of them locally; nothing is actually called, texted, booked, or posted
anywhere.
