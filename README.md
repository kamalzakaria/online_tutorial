# online_tutorial

A small collection of **no-build, static HTML** study sites — interactive notes and daily
practice for Malaysian school subjects (KSSR / KSSM). Everything is plain HTML/CSS/JS with
no dependencies, so each page works by just double-clicking the file or hosting it as-is.

🔗 **Live:** https://kamalzakaria.github.io/online_tutorial/

## Contents

| Folder | Subject | Level | What's inside |
| --- | --- | --- | --- |
| [`bahasa_melayu_tingkatan_1/`](bahasa_melayu_tingkatan_1/) | Bahasa Melayu | Tingkatan 1 | Daily practice app — 1 essay + 10 objective questions a day (ejaan, tatabahasa, peribahasa, kefahaman), streak counter, `localStorage` auto-save. See its own [README](bahasa_melayu_tingkatan_1/README.md). |
| [`asas_komputer_sains_tingkatan_1/`](asas_komputer_sains_tingkatan_1/) | Asas Sains Komputer | Tingkatan 1 | Interactive notes — Bab 1 Pemikiran Komputasional, plus `bab2.html`–`bab4.html`. |
| [`matematik_tahun_1/`](matematik_tahun_1/) | Matematik | Tahun 1 (KSSR) | Notes & activities across 8 chapters (`chapter1.html`–`chapter8.html`); `index.html` is the chapter hub. |

The repo-root [`index.html`](index.html) is a landing page that links to all three.

## Run locally

Double-click any `index.html` — it opens straight from `file://`, nothing to install.

Optional local server (not required):

```bash
python3 -m http.server 8000
# then open http://localhost:8000/
```

## Hosting (GitHub Pages)

Repo → **Settings → Pages → Build from branch → `main` / `/ (root)`**.
The root `index.html` is the home screen; each subject folder has its own `index.html`,
so `…/online_tutorial/<folder>/` resolves automatically.

## Adding content

- New subject → create a folder with an `index.html`, then add a card to the root `index.html` (`.subject` block) and a row to the table above.
- More questions/essays for Bahasa Melayu → see [`bahasa_melayu_tingkatan_1/README.md`](bahasa_melayu_tingkatan_1/README.md).

> Practice items are *modelled on* syllabus topics — study material, not official exam papers.
