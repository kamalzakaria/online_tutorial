# Sains Tingkatan 1 — Makmal Mini 🔬

A no-build, interactive study site for **Sains Tingkatan 1 (KSSM)**, covering **all 9 chapters** across the 5 themes. Plain HTML/CSS/JS, no dependencies — open `index.html` and start experimenting.

## What's inside

`index.html` is the hub: 9 chapter cards grouped by tema, colour-coded, with an overall progress bar. Each `bab<N>.html` is a self-contained chapter with three tabs:

- **📖 Nota** — concise, visual notes in Bahasa Melayu.
- **🎮 Aktiviti** — a *signature* interactive experiment unique to the topic, plus a smaller match/sort game.
- **✏️ Kuiz** — 7 multiple-choice questions, instant feedback + explanation, scored with stars.

### Chapters & signature interactives

| Bab | Tajuk | Tema | Aktiviti utama |
| --- | --- | --- | --- |
| 1 | Penyiasatan Saintifik | Kaedah Saintifik | Density float/sink lab (slider jisim & isipadu) + quantity↔SI-unit match |
| 2 | Sel sebagai Unit Asas Hidupan | Kesinambungan Hidup | Label organelles with animal/plant toggle + cell-organisation ordering |
| 3 | Koordinasi dan Gerak Balas | Kesinambungan Hidup | Sense-organ ↔ stimulus game + plant-tropism match |
| 4 | Pembiakan | Kesinambungan Hidup | Label flower parts + sexual/asexual classifier |
| 5 | Jirim | Penerokaan Unsur | Particle-state simulator (heat/cool to change state) + change-of-state match |
| 6 | Jadual Berkala | Penerokaan Unsur | Mini periodic-table element finder + unsur/sebatian/campuran classifier |
| 7 | Udara | Penerokaan Unsur | Air-composition chart (N₂/O₂/others) + pollution sorter |
| 8 | Cahaya dan Optik | Tenaga dalam Kehidupan | Reflection-law simulator (sudut tuju = sudut pantulan) + phenomenon match |
| 9 | Bumi | Bumi & Sains Angkasa | Label Earth's interior layers + Earth-systems (sfera) match |

## Run it

Double-click `index.html` — it opens from `file://`, nothing to install.
Optional local server: `python3 -m http.server 8000` → `http://localhost:8000/`.

## Progress tracking

Completing a chapter quiz saves to `localStorage` under the **`sains:`** prefix (`sains:bab<N>` → `{done, best, last}`). The hub reads these for per-chapter scores and overall progress. "Set semula kemajuan" clears all `sains:` keys.

## Adding / editing content

Each chapter is one self-contained file. Near the bottom `<script>`:

- **`QUIZ = [...]`** — `{ q, o:[4 options], a:<correct index 0-3>, e:"explanation" }`. Append to add questions.
- The signature activity's data sits in a named array just above the quiz (e.g. `ELS`, `FL`, `LY`, `STIMS`) — edit those to change the game.

> Notes & questions are *modelled on* the KSSM syllabus. Bab 4 covers human reproduction clinically as per the curriculum. Figures (e.g. air composition) are rounded for learning.
