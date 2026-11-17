# PROJECT21 — website

One page, four chapters — Work 作品 · Studio 工作室 · Services 服務 · Contact 聯絡 —
plus a project view that opens over it. English first, Traditional Chinese
beside it everywhere; there is no language switch.

No framework, no build step to view. Open `index.html`, or serve the folder.
All paths are relative, so it runs locally, on GitHub Pages, or on any static host.
**Deploy the whole folder**, not just `index.html`.

## Files

    index.html      structure: hero, the four chapters, the project view
    styles.css      the whole design system
    site.js         all content (projects, labels) and all behaviour
    projects/       supplied imagery, untouched — projects/<slug>/01.webp …
    thumbs/         generated 900px covers for the Work index (see below)
    tools/          build-assets.py
    favicon.png, og.png

## Adding things later

### A project
1. Put its images in `projects/<slug>/`, named `01.webp` … `NN.webp`, no gaps.
   One of them is the 4:3 title plate (the one with the logotype).
2. Add an entry to `PROJECTS` in `site.js` — copy an existing one:
   `slug`, `title`, `category`, `cover` (the title plate's number), `accent`
   (one colour sampled from the work), `scope` and `description` (EN + ZH).
3. Run:

       pip install pillow
       python3 tools/build-assets.py

   This writes `thumbs/<slug>.webp` and rewrites the `SIZES` / `SHEETS`
   manifest in `site.js` from the files on disk, so counts and sizes can't
   drift. It refuses to run if numbering has a gap or the cover is missing.

Everything else follows automatically: the Work grid and Flow 流 view, the
filters, the name frame round the hero, Prev / Next inside projects, and the
project's own hung wall and kaleidoscope.

To show it in the hero rotation too, add `[slug, imageNumber, "alt text"]`
to the `HERO` list in `site.js`.

### A category
Add the key to `CATEGORIES` and its EN / ZH name to `L.categories` in
`site.js`. The filter chip appears on its own; empty categories show a note.

### A contact line
In `index.html`, inside `<dl class="contact">`, copy one `<div>` (a `dt`
label in EN + ZH, a `dd` value). The grid makes room.

### A new chapter (e.g. Clients, News, Awards)
There is a commented-out chapter template in `index.html`, just above
Contact. Uncomment it, give it an `id`, and add a matching link to the
header nav: `<a href="#id" data-chapter="id">Name <span lang="zh-Hant">名稱</span></a>`.
The nav highlight, scroll progress and colour background pick it up by
themselves. Keep text small and EN + ZH paired, like the other chapters.

## How the project view is laid out (no per-project setup)
Pieces are derived from each image's real proportions in the manifest:
runs of same-shaped images share a puzzle panel (one big, then 2×2, then
1 + 2); very wide images stand alone. The pieces then hang as a wall in
a fixed rhythm — big · pair · low · high — set by `ROT` in
`sequenceHTML()` in `site.js`. Desktop reads it sideways; phones (≤ 620px)
read it downward. Change `ROT` to change the rhythm everywhere.

## Motion
Every moving layer — name frame, kaleidoscope, colour background, Flow
stage, hung-wall drift, the Contact call — switches off when the visitor's
system asks for reduced motion. Heavy layers draw only while on screen,
and the inner kaleidoscope ring turns itself off on slow devices.

## Before launch
See `NOTES-to-confirm.md` (kept on the Mac, not published) for facts that
still need the client's confirmation.
