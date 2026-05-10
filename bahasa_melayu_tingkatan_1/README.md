# Latihan Harian Bahasa Melayu — Tingkatan 1

A tiny, no-build practice site for ~15–30 minutes of daily Bahasa Melayu drilling,
built around the weaknesses seen in the Pentaksiran Pertengahan Tahun 2026 result
(overall 54%; weakest: **karangan**, then **ejaan**, **tatabahasa**, **peribahasa**, **kefahaman**).

## What it does
- **1 essay a day** — a real-exam-style prompt. A **good model essay** is shown straight away to read; he then writes his own on the same tajuk in the box (live word count + auto-save).
- **10 objective questions a day** — weighted to his weak areas (3 ejaan, 3 tatabahasa, 2 peribahasa/simile, 2 kefahaman) drawn from a bank of 125. Click an option → marked right/wrong instantly with an explanation, then locked.
- **Daily rotation** — questions & essay change each day (deterministic by date). Use ◀ ▶ to browse other days; "Hari ini" jumps back.
- **Streak counter** + progress, stored in the browser's `localStorage` (per device).

## Files
```
practice/
├── index.html   ← the whole app — open this (everything is inside it)
└── README.md
```
That's it. The question bank and essays are inlined inside `index.html`, so there are **no other files to load** — it works by just double-clicking the file.

## Run it on your PC
Double-click `index.html` — opens in your browser straight from `file://`, nothing to install.
(Optional local server, not needed: `cd practice && python3 -m http.server 8000` → `http://localhost:8000`.)

## Host it on GitHub Pages
1. Create a repo and add `index.html` (and this README) at the repo root.
2. Repo → **Settings → Pages → Build from branch → `main` / root**.
3. Open `https://<your-username>.github.io/<repo>/` — all static, nothing else to configure.

## Adding more questions / essays
Open `index.html` in a text editor and find these arrays near the top of the script section:
- **`window.QUESTION_BANK = [ ... ]`** — append objects like:
  ```js
  { id:"ej99", cat:"Ejaan", q:"...", options:["betul","salah1","salah2","salah3"], answer:0, explain:"..." }
  ```
  `cat` must be one of: `"Ejaan"`, `"Tatabahasa"`, `"Peribahasa & Simile"`, `"Kefahaman"`. The correct option goes at index `answer` (0–3). More questions per category = more variety before the daily rotation repeats.
- **`window.ESSAY_BANK = [ ... ]`** — append `{ id, jenis, tajuk, bahan, tips:[...], contoh:[...paragraphs...] }`.

Reset progress / drafts anytime via the "Set semula semua data" link at the bottom of the page.

> Note: questions are *modelled on* the topics that appeared in the mid-year paper (ejaan & spacing rules, penjodoh bilangan, imbuhan, kata sendi/hubung, kata nama am/khas, ayat perintah/majmuk, peribahasa & simile perbandingan, simpulan bahasa, maksud ayat, pantun/sajak) — practice items, not the exact exam paper. Model essays are original samples written for study.
