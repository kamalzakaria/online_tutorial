# Geografi Tingkatan 1 — Jelajah Dunia 🌍

A no-build, interactive study site for **Geografi Tingkatan 1 (KSSM)**, covering **all 14 chapters** across the 6 themes. Every page is plain HTML/CSS/JS with no dependencies — open `index.html` and start learning.

## What's inside

`index.html` is the hub: 14 chapter cards grouped by tema, colour-coded, with an overall progress bar. Each `bab<N>.html` is a self-contained chapter with three tabs:

- **📖 Nota** — concise, visual notes in Bahasa Melayu.
- **🎮 Aktiviti** — a *signature* interactive exercise unique to the topic, plus a smaller match/sort game.
- **✏️ Kuiz** — 7 multiple-choice questions, instant feedback + explanation, scored with stars.

### Chapters & signature interactives

| Bab | Tajuk | Tema | Aktiviti utama |
| --- | --- | --- | --- |
| 1 | Arah | Kemahiran Geografi | Spin-the-compass + drive-the-robot grid |
| 2 | Kedudukan | Kemahiran Geografi | Grid-reference treasure hunt + lat/long lines |
| 3 | Peta Lakar | Kemahiran Geografi | Map-symbol game + read-the-sketch-map |
| 4 | Lakaran Peta Malaysia | Kemahiran Geografi | Clickable states map + capitals match |
| 5 | Bumi | Geografi Fizikal | Day/night rotation slider + latitude lines |
| 6 | Bentuk Muka Bumi | Geografi Fizikal | Label-the-landform scene |
| 7 | Saliran | Geografi Fizikal | Label-the-river-system (hulu→delta) |
| 8 | Penduduk di Malaysia | Geografi Manusia | Density generator + factor sorter |
| 9 | Petempatan di Malaysia | Geografi Manusia | Settlement-pattern classifier + function match |
| 10 | Muka Bumi & Saliran Asia Tenggara | Geografi Kawasan | SEA features map + country match |
| 11 | Penduduk & Petempatan Asia Tenggara | Geografi Kawasan | Interactive population bar chart + city match |
| 12 | Sumber Air | Alam Sekitar | Water-cycle labelling + save/waste sorter |
| 13 | Sisa Domestik | Alam Sekitar | **Recycling-bin sorting game (3R)** + 3R match |
| 14 | Panduan Kerja Lapangan | Kerja Lapangan | Order-the-steps game + method match |

## Run it

Double-click `index.html` — it opens from `file://`, nothing to install.
Optional local server (not required): `python3 -m http.server 8000` → `http://localhost:8000/`.

## Progress tracking

Completing a chapter quiz saves to the browser's `localStorage` under the **`geo:`** prefix (`geo:bab<N>` → `{done, best, last}`). The hub reads these to show per-chapter scores and overall progress. "Set semula kemajuan" on the hub clears all `geo:` keys.

## Adding / editing content

Each chapter is one self-contained file. The bits you'll usually touch are near the bottom `<script>`:

- **`QUIZ = [...]`** — array of `{ q, o:[4 options], a:<correct index 0-3>, e:"explanation" }`. Append objects to add questions (the quiz auto-renders and scores out of `QUIZ.length`).
- The **signature activity** data lives in a clearly-named array just above the quiz (e.g. `STATES`, `RV`, `ITEMS`, `STEPS`) — edit those to change the game content.

> Practice items & notes are *modelled on* the KSSM syllabus topics — study material, not official exam papers. Population/area figures are rounded for learning.
