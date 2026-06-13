# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A collection of **no-build, static HTML** study sites for Malaysian school subjects (KSSR / KSSM syllabus). There is no package manager, no build step, no dependencies, and no tests/lint. Every page is plain HTML/CSS/JS that runs by opening the file directly.

Content is in **Bahasa Melayu** (`<html lang="ms">`) — keep new UI text, questions, and notes in Malay to match.

## Running

- **Locally:** open any `index.html` directly — it works from `file://`, nothing to install.
- **Optional server:** `python3 -m http.server 8000` then `http://localhost:8000/`.
- **Hosting:** GitHub Pages, built from `main` / root. Root `index.html` is the home page; each subject folder has its own `index.html` so `…/online_tutorial/<folder>/` resolves automatically. Live at https://kamalzakaria.github.io/online_tutorial/.

## Critical convention: everything is self-contained

Each `.html` file inlines **all** of its CSS (in `<style>`), JS (in `<script>`), and content data (in JS arrays/markup). There are no shared stylesheets, no shared scripts, and no fetch/import of external files. A page is meant to load with zero network requests. When editing, stay within the single file — do not extract shared assets or add CDN/library links.

Because nothing is shared, the three subjects each evolved their own styling and patterns; match the conventions of the file/folder you're editing rather than imposing a global style.

## Layout

- `index.html` — root landing page; `.subject` cards link to each folder (each card needs a `.c-<colour>` class defined in the page's `<style>`). Add a card here when adding a new subject.
- `bahasa_melayu_tingkatan_1/` — daily-practice **app** (see below).
- `asas_komputer_sains_tingkatan_1/` — interactive notes, multi-page.
- `matematik_tahun_1/` — chapter hub + per-chapter pages.
- `geografi_tingkatan_1/` — chapter hub + 14 per-chapter pages with `localStorage` progress (see below).
- `sains_tingkatan_1/` — chapter hub + 9 per-chapter pages; same shell as geografi (see below).

## Per-subject architecture

### bahasa_melayu_tingkatan_1/index.html (the most app-like)
A daily Bahasa Melayu drilling tool. Three `<script>` blocks: two define data, one runs the app.
- `window.QUESTION_BANK = [...]` — objects `{ id, cat, q, options:[4], answer:<0-3>, explain }`. `cat` ∈ `"Ejaan"`, `"Tatabahasa"`, `"Peribahasa & Simile"`, `"Kefahaman"`.
- `window.ESSAY_BANK = [...]` — `{ id, jenis, tajuk, bahan, tips:[...], contoh:[...paragraphs] }`.
- **Daily rotation is deterministic by date**: a day index (`dayIndexOf`) seeds a LCG shuffle (`seed = di*2654435761 ...`), so the same day always yields the same 10 questions + essay. Don't replace with `Math.random()` — it must stay reproducible across reloads/devices.
- State persists in `localStorage` under the **`bm:`** prefix (e.g. `bm:doneDates` for the streak). The "Set semula semua data" link clears all `bm:` keys.
- To extend: append to the bank arrays only. See `bahasa_melayu_tingkatan_1/README.md` for the full add-content guide.

### asas_komputer_sains_tingkatan_1/ (interactive notes)
- `index.html` is **Bab 1**; `bab2.html`–`bab4.html` are the other chapters.
- A top `<nav>` links the bab pages to each other; the current page's link is highlighted. When adding a bab, add its file **and** the nav link in every page.

### matematik_tahun_1/ (chapter hub + chapters)
- `index.html` is a hub of `.chapter-btn` buttons that `window.location.href` to `chapter1.html`–`chapter8.html`.
- Each chapter page uses a tabbed layout driven by `showContent(id)` over sections: Tutorial, Latihan, Exam, Keputusan (results).
- Answer-checking helpers per chapter: `checkAnswer(qId)` (multiple-choice), `checkFillBlank(qId, correct)`, `checkCompare(qId, '<'|'>'|'=')`; scoring via `updateScore`/`updateResults`/`getStars`. `resetAll()` clears progress. Reuse these helpers when adding questions instead of writing new logic.

### geografi_tingkatan_1/ (chapter hub + chapters, with progress)
- `index.html` is a hub of 14 cards grouped by 6 tema; chapter pages are `bab1.html`–`bab14.html` (note: `bab<N>`, **not** `chapter<N>`). The hub's `TEMAS` array drives the cards and the overall progress bar.
- Every chapter shares the **same self-contained shell**: a sticky tab bar switching three `.panel`s (Nota / Aktiviti / Kuiz) via `tab(id, el)`, plus an identical quiz engine. The quiz is a `QUIZ = [{q, o:[…], a, e}]` array rendered by `pick(qi, oi)` and graded by `submitQuiz()`. The CSS is duplicated per file with only the `--c`/`--c2` theme colour changing per tema — when restyling, edit the file you're in, don't try to share a stylesheet.
- **Progress** persists in `localStorage` under the **`geo:`** prefix: `saveProgress(bab, pct)` writes `geo:bab<N>` = `{done, best, last}`; the hub reads these and "Set semula kemajuan" clears all `geo:` keys. Keep this contract if you add chapters.
- Each chapter's **signature interactive** is bespoke (compass, clickable states map, SVG landform/river scenes with `.hot` hotspots, recycling-bin sorter, step-ordering, etc.). Its data lives in a named array right above the `QUIZ` (e.g. `STATES`, `RV`, `ITEMS`, `STEPS`). Interactions are **click/tap-based, not HTML5 drag-and-drop**, so they work on touch devices — follow that pattern for new games.

### sains_tingkatan_1/ (same shell, science topics)
- Built as a **copy of the geografi pattern**: same tab/quiz shell and `.hot` hotspot labelling games, 9 chapters (`bab1.html`–`bab9.html`) across 5 tema. The only structural differences: progress is stored under the **`sains:`** prefix (`sains:bab<N>`), and the hub counts out of 9.
- Signature interactives lean on small simulations (density float/sink lab, particle-state simulator, reflection-law SVG, label-the-cell with an animal/plant toggle, mini periodic table). The reusable label-on-SVG game (`.hot` dots + a `*Done` map + `new*/pick*` functions) is the same idiom as geografi's landform/river scenes — reuse it for new diagram-labelling chapters.

## Notes

- `.gitignore` excludes `asas_komputer_sains_tingkatan_1/dhng.pdf` (source PDF) and `asas_komputer_sains_tingkatan_1/.claude`.
- Practice items are *modelled on* syllabus topics — study material, not official exam papers; keep that framing in content and READMEs.
