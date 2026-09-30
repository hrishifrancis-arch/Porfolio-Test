# Hrishi Francis — Engineering Portfolio

Static portfolio site for Hrishi Francis, mechanical engineering student at Purdue
University. Dark, drawing-sheet design; plain HTML, CSS and JavaScript, no frameworks
and no runtime dependencies. Hosted free on GitHub Pages.

**Pages:** Home · Projects (3 case studies) · CAD Lab · About · Résumé · Contact · 404

## Structure

```
index.html, about.html, cad-lab.html,        ← built pages (committed, served as-is)
resume.html, contact.html, 404.html
projects/index.html                           ← projects overview
projects/asme-grand-prix.html                 ← case study 01
projects/bravecore-uav.html                   ← case study 02
projects/habitat-can-crusher.html             ← case study 03
assets/css/main.css                           ← all styles (design tokens at the top)
assets/js/main.js                             ← nav, reveals, counters, lightbox, filters, form
assets/img/*.webp                             ← optimized images (generated) + sizes.json
assets/Hrishi-Francis-Resume.pdf              ← the résumé served by the site
src/pages/*.html                              ← page SOURCES — edit these, not the built pages
tools/build.mjs                               ← src/pages → built pages, sitemap.xml, robots.txt
tools/build_images.py                         ← originals → assets/img/*.webp
tools/verify.mjs                              ← static QA (links, anchors, alt text, PDF, pending)
tools/site.json                               ← site URL, email, LinkedIn, résumé filename
```

## Editing

Edit the source in `src/pages/`, then rebuild:

```bash
node tools/build.mjs      # regenerate every page
node tools/verify.mjs     # must print OK
```

The built HTML at the root is committed so GitHub Pages can serve it with no build
step. Edits made directly to a built page are overwritten by the next build.

Page sources start with a JSON front-matter comment (`out`, `title`, `description`,
`nav`, `sheet`) and can use these shortcodes:

| Shortcode | Produces |
|---|---|
| `{{base}}` | relative path to the site root (`""` or `"../"`) |
| `{{img src="name" alt="…" sizes="…" eager}}` | responsive `<img>` with `srcset`, width/height, lazy loading |
| `{{fig src="name" alt="…" cap="…" label="Fig 04.1" group="g" frame="cover\|contain\|paper" ar="3/4"}}` | a `<figure>` that opens in the lightbox, with caption |
| `{{big src="name"}}` | URL of the largest rendition (for hand-built lightbox links) |
| `{{email}}` `{{linkedin}}` `{{resume}}` `{{resumeFile}}` | values from `tools/site.json` |

Attribute values can't contain `"` — use typographic quotes in captions.

`frame="paper"` puts white-background CAD renders on a light panel (multiply blend) so
they don't glare on the dark page.

### Content still to confirm

A few spots are marked on the page with a dashed orange **Content to confirm** box
(`<span class="pending" data-pending="…">`). `node tools/verify.mjs` lists them;
`node tools/verify.mjs --strict` fails while any remain. Replace the span with the real
text, rebuild, and re-verify.

## Images

Originals (HEIC phone photos, PNG screenshots) are not in this repository. To
regenerate `assets/img/` from them:

```bash
python3 tools/build_images.py "/path/to/originals"   # needs Pillow; HEIC via macOS sips
node tools/build.mjs
```

The source folder needs one sub-folder per project (`ASME Grand Prix`, `Bravecore`,
`Habitat for Humanity`). `MANIFEST` in `build_images.py` maps each output name to its
source file and crop; EXIF rotation is baked in, and each image is written as WebP at
640 / 1280 / 1920 px (never upscaled). `gp-kart-negative` is the inverted kart render
used on the home page.

**Adding a CAD Lab item:** add a line to `MANIFEST`, rerun the image build, then copy
an `<article class="cad-card">` block in `src/pages/cad-lab.html`. `data-cats` holds
space-separated categories (`vehicle uav mechanisms product`); to add a new category
such as Personal CAD, add a matching filter button with `data-filter="personal"`.

### Hero turntable video

`assets/video/kart-orbit-1200.mp4` (desktop) and `kart-orbit-720.mp4` (mobile) are
encoded from a ProRes master kept in `_source/` (gitignored — 205 MB, over GitHub's
100 MB limit) by `tools/encode_video.swift` (usage in its header). The encoder crops the
pillarbox to the model, grades black to the page ink, and blends the last 0.6 s into
frame 0 so the orbit ends exactly on the hero still (`gp-kart-negative`).

`main.js` runs the sequence: plot-in → 360° orbit (from ~1.35 s) → still + callout +
edge-scan pass (4 s) → orbit → … It streams the video immediately, picks the size from the
rendered width, pauses
off-screen, and falls back to the CSS-only scan loop if the video can't play
(blocked autoplay, data saver, error). Reduced-motion visitors never get the video.
To remove it, delete the `<video class="vp-video">` element in `src/pages/index.html`
and rebuild — everything else keeps working.

## Site settings

`tools/site.json`:

```json
{
  "url": "https://hrishifrancis.github.io",
  "email": "franc102@purdue.edu",
  "linkedin": "https://www.linkedin.com/in/hrishi-francis-04a938193/",
  "resumeFile": "Hrishi-Francis-Resume.pdf"
}
```

Change a value, run `node tools/build.mjs`, commit. `url` must match the real GitHub
Pages address — it drives canonical links, social previews, `sitemap.xml` and
`robots.txt`.

**Replacing the résumé:** overwrite `assets/Hrishi-Francis-Resume.pdf` with the new PDF
(same filename), run `node tools/build.mjs`, and commit. The build regenerates
`assets/resume-data.js`, the base64 copy that lets the download button force a real
download when the site is opened from disk (`file://`). Over https the PDF itself is
fetched, so a forgotten rebuild only leaves `file://` with a stale copy —
`verify.mjs` flags it. If the filename changes, update `resumeFile` too.

## Contact form

The form posts to [FormSubmit](https://formsubmit.co) — no account, no backend.
**The first submission sends an activation email to the address in `site.json`; the
form doesn't deliver anything until that link is clicked.** After activation FormSubmit
can issue a random alias to use in place of the plain address. Submissions use AJAX
with an inline success/error message, and fall back to a normal POST with JavaScript
off. There's a honeypot field against bots.

## Hosting (GitHub Pages)

1. The repository **must be named `<username>.github.io`**. `404.html` uses
   root-absolute paths, which break if the site lives in a sub-folder.
2. Settings → Pages → *Deploy from a branch* → `main` / `(root)`.
3. `.nojekyll` is present, so files are served untouched.

A plain-English walkthrough for account setup is in [GITHUB-SETUP.md](GITHUB-SETUP.md).

## Running locally

Open `index.html` directly, or serve the folder:

```bash
python3 -m http.server 8000     # then http://localhost:8000
```

Over `file://` everything works except the contact form.

## Design notes

- **Concept:** the engineering drawing sheet. Drafting-grid background, title blocks
  styled on Hrishi's own drawings (PROJECT / TITLE / DRAWN / SHEET), dimension-line
  dividers, monospace readouts, one signal-orange accent (`--signal`).
- **Type:** Barlow Condensed (display), IBM Plex Sans (body), IBM Plex Mono (data),
  via Google Fonts.
- **Case studies** follow Problem → Requirements → My Role → Design → Analysis →
  Manufacturing → Testing → Iteration → Results, with a sticky stage rail (a horizontal
  strip on mobile) that tracks the reader's position.
- **Accessibility:** skip link, visible focus, `aria-current` navigation, labelled
  lightbox `<dialog>`, reduced-motion support (no animation, counters show final
  values), and alt text on every image (enforced by `verify.mjs`).
- **Progressive enhancement:** with JavaScript off every page still reads top to
  bottom, images open as plain links and the form still submits.
