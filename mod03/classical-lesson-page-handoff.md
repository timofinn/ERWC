## Handoff Spec: Classical Lesson Page (3.04 template)

### Overview
A student-facing lesson page, hosted on GitHub Pages (`timofinn/ERWC`) and embedded in a Canvas assignment with an iframe. Canvas strips `<style>` blocks, so all styling lives on the hosted page. Students open it on Chromebooks to follow the period, from Purpose through the success checklist, while working in a paper notebook. The page is for reading and follows the class in order. Nothing on it is filled in on screen.

Reference build: `mod03/3.04.html`. Reuse it for 3.05 onward.

### Layout
- Single column, centered. `.page` max-width **760px**, padding `40px 24px 64px`.
- Order: Masthead → Purpose (+ notebook image) → numbered sections (I., II., III., IV.) → Success Looks Like → footer ornament.
- Sections are separated by a 1px `--rule` bottom border with 28px vertical padding. The last section has no border.
- Each section header has a meta line underneath: **time · notebook location** (e.g. "7 MIN · LEFT PAGE, TOP").

### Design Tokens Used
| Token | Value | Usage |
|-------|-------|-------|
| `--paper` | #FBF7EE | Page background |
| `--card` | #FFFDF8 | Callout boxes, model answers, page-split cards |
| `--ink` | #2A2724 | Body text, table header rule |
| `--muted` | #6B6358 | Meta lines, tips, captions, table headers |
| `--oxblood` | #7A2E2A | Accent: kicker, roman numerals, STAR letters, fill-in frame border, list markers |
| `--gold` | #B8975A | Ornaments, quote rule |
| `--rule` | #DCD2BF | Hairlines, card borders |
| `--wash` | #F3ECDD | "Steal from yourself" type notes |
| Display font | EB Garamond 600 / 500 italic | h1 44px, h2 30px, h3 22px, STAR letters 32px |
| Body font | Source Serif 4, 400/600 | 18px / 1.6 |
| Label style | Source Serif 4 600, 12–13px, uppercase, tracking .14–.18em | Kicker, meta, table headers, tags |

Fonts load from Google Fonts with Georgia as the fallback. Spacing is ad hoc (4/6/8/12/16/18/24/28px). If this becomes a shared `classical.css`, set them as `--space-xs` through `--space-xl` (4/8/12/18/28).

### Components
| Component | Class | Notes |
|-----------|-------|-------|
| Masthead | `header` | Kicker (module name), h1 `#.## \| Title`, gold ❖ ornament |
| Section header | `h2 > .num` + `.meta` | Roman numeral in oxblood italic. The meta line always gives the time and the notebook page |
| Page-split cards | `.pages` | 2-column grid: Left page / Right page contents |
| Notebook image | `a > img` | Full-width, opens full size in a new tab. Alt text describes both pages |
| Fill-in frame | `.frame` + `.blank` | Sentence frames, oxblood left border, underlined blanks (min 110px) |
| Teacher model | `blockquote > cite` | "Mr. Finn's" label, gold left rule, italic |
| Reference table | `table.star` | Booktabs style: 2px ink header rule, hairline rows. First-column letters in display font |
| Bad vs good model | `.compare > .bad / .good` | Stacked cards. `.bad` is at 85% opacity. `.good` uses oxblood letter labels |
| Steps | `ol.steps` | Oxblood bold markers |
| Note | `.note` | `--wash` background, 16px |
| Question list | `.q` (grid 34px + 1fr) | Italic numeral, bold question, muted tip underneath. `.group` labels split the sets |
| Closer line | `.closer` | Centered Garamond italic, oxblood |
| Checklist | `ul.check` | ☐ glyph markers, display only |

### States and Interactions
| Element | State | Behavior |
|---------|-------|----------|
| Notebook image | Click | Opens the PNG in a new tab |
| Everything else | n/a | Static. No hover states, no JS, no inputs |

The page has no interaction on purpose. The notebook is the workspace, and on-screen inputs invite students to type instead of write.

### Responsive Behavior
| Breakpoint | Changes |
|------------|---------|
| > 560px (Chromebook in Canvas iframe, ~700–900px) | Default layout |
| ≤ 560px (phones) | Body 17px, h1 34px, h2 25px, side padding 16px, page-split cards stack, draft table 14px |

There is no horizontal scroll at any width. Tested at 900px and 380px.

### Canvas Embed
```html
<p><a href="https://timofinn.github.io/ERWC/mod03/3.04.html" target="_blank">Open full screen</a></p>
<iframe src="https://timofinn.github.io/ERWC/mod03/3.04.html" width="100%" height="5600" style="border:0;" title="3.04 Tell Me About a Time"></iframe>
```
- **Height is fixed**, because Canvas strips the script that would resize it. Set it to the page's `scrollHeight` at 900px width plus about 150px. For 3.04 that's 5428px, so the height is 5600.
- **"Open full screen"** is required, as a fallback for iframe trouble and for zooming.

### Edge Cases
- **Stale content:** GitHub Pages caches for about 10 minutes. After a push, the full-screen tab updates on hard refresh (Cmd/Ctrl + Shift + R). The iframe can lag behind.
- **Page grows after an edit:** the iframe height doesn't follow it, and students get a scrollbar inside a scrollbar. Re-measure and update the Canvas height.
- **Image not showing:** check that the HTML and the PNG were both committed and pushed.
- **Fonts fail to load:** the page falls back to Georgia and stays readable.
- **Canvas character limit:** doesn't apply, because the text lives on the hosted page. Still aim for about 5,000 characters or less, for cognitive load reasons, not Canvas ones.

### Animation / Motion
None.

### Accessibility Notes
- One h1 per page, with h2 for sections and h3 for subsections, in order.
- The notebook image needs alt text describing what's on each page.
- The iframe needs a `title` attribute.
- Contrast: `--muted` on `--paper` is 5.5:1, `--oxblood` is 8.7:1 and `--ink` is 13.9:1, both above AA for body text.
- Labels are uppercase through CSS only, so the source text stays in normal case for screen readers.
- Don't use em dashes in student copy (house style).

### Workflow
1. Copy `mod03/3.04.html` to the new page's filename. Swap the content and keep the classes.
2. Build the notebook image from `notebook-models/notebook-model-3.04.html` (edit it, then Export PNG) and save it beside the page.
3. Commit, then push with **GitHub Desktop → Push origin**.
4. In Canvas, paste the embed with the measured height. Create the assignment unpublished.
