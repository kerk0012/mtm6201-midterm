# MTM6201 Midterm — My Coffee House

Responsive landing page built from the `mtm6201 Midterm` Figma file.
Hand-coded HTML5 + CSS. No frameworks, no JavaScript.

**Live:** `https://<your-username>.github.io/mtm6201-midterm/`
**Repo:** `https://github.com/<your-username>/mtm6201-midterm`

---

## Folder structure

```
mtm6201-midterm/
├── index.html
├── css/
│   ├── reset.css
│   └── main.css
└── images/
```

---

## Breakpoints

Taken from the three Figma frames:

| Frame   | Width  | Media query              | Side padding |
|---------|--------|--------------------------|--------------|
| Mobile  | 390px  | *(base — mobile first)*  | 16px         |
| Tablet  | 768px  | `@media (min-width: 768px)`  | 24px     |
| Desktop | 1440px | `@media (min-width: 1440px)` | 0 (1200px wrapper, 120px margins) |

`min-width` only — there is not a single `max-width` media query in the project.

---

## Design tokens

| Token | Value |
|---|---|
| Page background | `#f3f0e9` |
| Black | `#000000` |
| White | `#ffffff` |
| Gold (eyebrows, icons) | `#d69e3d` |
| Gold dark (button hover/focus) | `#966f2c` |
| Headings + nav | Lato (900 / 700) |
| Body + buttons | Karla (400 / 700) |
| Wrapper max width | 1200px |

Type scale (mobile → tablet → desktop): h1 32/48/62 · h2 28/38/48 · h3 22/28/32 · body 16.

All tokens live in `:root` and are **redefined inside the two media queries**, so the
whole page rescales from one block instead of per-component overrides.

---

## Rubric map

| Requirement | Where |
|---|---|
| Semantic HTML5 | `header`, `nav`, `main`, `section`, `figure`/`figcaption`, `blockquote`, `cite`, `footer` |
| Skip to main content | `.skip-link` → `#main` (visible on focus, `main.css` §03) |
| 3+ ARIA attributes | `aria-label` (nav, CTA section), `aria-labelledby` (5 sections → their headings), `aria-current="page"` (logo → current page) |
| Alt text | All 15 images have descriptive alt text |
| Hero `srcset` + `sizes` | `index.html` — 5 widths (480/800/1200/1600/2400), `sizes="100vw"` (hero is full-bleed at every breakpoint) |
| Flexbox | Header bar, nav list, hero centring |
| CSS Grid | Gallery, features, CTA, story, testimonials |
| Custom properties | `main.css` §01, reused throughout and rescaled per breakpoint |
| `@keyframes` | `fade-up` — hero content fades up on load, staggered (§04) |
| Hover + focus transitions | `.btn` — both variants transition to `#966f2c` (§03) |
| Mobile-first, min-width only | Confirmed — see table above |
| 1200px wrapper | `.wrapper` (§03) |

### Complex selectors (all doing necessary work)

| Selector | Type | Job |
|---|---|---|
| `.story__text p + p` | adjacent sibling | Space between the two story paragraphs, no trailing margin |
| `.hero__content > *:nth-child(2 / 3)` | child + `:nth-child` | Staggers the hero load animation |
| `.features__list > .features__item:last-child` | child + `:last-child` | Centres the 3rd feature across both tablet columns |
| `.testimonials__list > li:last-child` | child + `:last-child` | Same, for the 3rd testimonial |
| `.testimonial__body .testimonial__cite` | descendant | Attribution styling inside the caption overlay |

---

## Validation

Both files were checked before submission:

- **HTML** — W3C Nu Html Checker: *Document checking completed. No errors found.* (0 errors, 0 warnings)
- **CSS** — parses clean; no syntax errors.

---

## Notes on the build

- The gallery, story image and section text columns are all built on the same
  **588px** module (half of the 1200px wrapper minus the 24px gap). Constraining
  the section headings to 588px is what reproduces the Figma's two-line headings
  at every breakpoint.
- `reset.css` sets `height: auto` on media. Without it the `width`/`height`
  attributes on the images defeat `aspect-ratio` and the squares render at their
  full intrinsic height.
- Button states come from the Figma "button examples" layer: white → `#966f2c`,
  and black → `#966f2c`, both with white text on hover/focus.
