# Marker Quiz — README

**Highlight a photo or PDF of your textbook or notes and get an instant 4-choice quiz.**
A single-file web app that runs offline in any modern browser. No install, no account, and your photos never leave your device.

Marker Quiz ships in two editions that share the same engine:

| Edition | File | UI language | Notes |
|---|---|---|---|
| Japanese (マーカーでクイズ) | `Fマーカーでクイズ_v1.0.html` | Japanese | Photos only (2026-09-20) |
| Japanese (マーカーでクイズ) | `Fマーカーでクイズ_v1.1.html` | Japanese | + PDF import (2026-09-23) |
| English (Marker Quiz) | `FMarkerQuiz_English_v1.1.html` | English | Full English edition: UI, help, sample page, and an English-aware quiz engine (2026-09-23) |
| English (Marker Quiz) | `FMarkerQuiz_English_v1.2.html` | English | + Sample chooser with four subject pages (2026-09-23) |

Older files are kept on purpose; each edition is complete on its own.

---

## 1. Quick start

1. Open the HTML file in a browser — from the Files app on iPhone, Files/Drive on Android, or by double-clicking on a PC.
2. Tap **Take a photo**, **Choose a photo**, or **Choose a PDF**. (New here? Try **Try a sample** or **Watch the demo** first.)
3. Run your finger over the terms you want to remember.
4. Pick a difficulty and tap **Make a quiz**.
5. Optionally type the hidden terms (this turns those questions into text choices), then **Start the quiz**.

Requirements: a current browser (Safari on iOS, Chrome on Android, or Chrome/Edge/Safari/Firefox on desktop). Works from a local file or any web server.

---

## 2. How it works

The app walks you through five steps: **Photo/PDF → Mark → Terms → Quiz → Results**.

### Photo / PDF
* **Take a photo** opens the camera; **Choose a photo** opens your photo library.
* **Choose a PDF** lets you pick pages from a PDF (see §4).
* On a desktop browser you can also drag a photo or PDF onto the home screen.
* Photos are downscaled to a long edge of 1600 px and stored as JPEG; a 240 px thumbnail is kept for the history list.

### Mark
| Tool | What it does |
|---|---|
| **Marker** | Highlight a term. The highlighted area becomes one quiz "spot". Six preset colors plus a custom color; three widths (S / M / L). |
| **Pencil** | Underline a term (the spot extends upward to cover the text) or circle it (the enclosed area becomes the spot). |
| **Eraser** | Removes a single stroke. |
| **Pan** | Move the page; you can also pinch to zoom or pan with two fingers at any time. |
| **Spots** | Shows exactly which areas will be quizzed. |
| **Undo / Redo / Clear all** | Stroke history; Clear all asks for confirmation. |

Marks that overlap or sit close together (within about 1.5 % of the image width) merge into a single spot. Marks are saved automatically; you need **at least two spots** to make a quiz.

### Terms (optional)
Type the term hidden under each spot to get **text choices** for that question. Spots left blank use **image choices** instead. You can skip this step entirely.

### Quiz
Three question types:
* **Fill-in (text)** — which term belongs under the red sheet? Four text options.
* **Fill-in (image)** — which cropped image belongs under the red sheet? Four image options.
* **Reverse (term → spot)** — a term is shown; pick the matching spot A–D on the page (Hard only).

Up to 10 questions per quiz (choose *All (max 10)*, *5*, or *10*). Question format can be *Auto* (text whenever a term was typed), *Image choices*, or *Text choices*. On a keyboard, press **1–4** or **A–D** to answer.

### Results
Score, points, time, and a review list of every question with your answer. From here you can **retry only the ones you missed**, **retry at the same level**, **retry at a harder level**, change the level, or go back and **edit marks**.

---

## 3. Difficulty levels

| | Easy ★ | Medium ★★ | Hard ★★★ |
|---|---|---|---|
| Hidden spots | only the one being asked | only the one being asked | every marked spot |
| Other marks | visible | hidden (plain page) | all hidden |
| Context shown | wide (about 3×) | medium (about 2×) | narrow (about 1.5×) |
| Time limit | none | 20 s per question | 10 s per question |
| Hints | yes | no | no |
| Wrong answers | clearly different | similar length | most confusable (look-alikes, same category) |
| Question format | fill-in | fill-in | fill-in + reverse lookup, mixed |
| Feedback | immediate | immediate | at the end, with a speed bonus |

Wrong answers are drawn first from the other terms on the same page, then from terms you typed in earlier sessions, then from a built-in vocabulary of general school terms. In Hard mode the engine also generates look-alike variants of the correct answer.

**English quiz engine (English edition).** Look-alikes are built from confusable letters (a/e, i/l, m/n, b/d …), vowel substitutions, swapped or doubled letters, suffix and prefix groups (-tion/-sion, -able/-ible, -er/-or, hyper-/hypo-, in-/un- …), plural toggles, swapped word order for two-word terms, and number shifts (±1, ±10, ×2, ÷2, or a few years for dates) that keep units such as °F, °C, or % intact.

**Japanese quiz engine (Japanese edition).** Look-alikes use visually similar kana and kanji, voiced-mark (dakuten) toggles, common technical suffixes, and a Japanese school vocabulary.

---

## 4. PDF import (v1.1 and later)

1. Tap **Choose a PDF** and pick a file.
2. The **page picker** shows thumbnails of every page (rendered as you scroll). Tap pages to select them, use **All** / **None**, or type a range such as `3-5, 8` and tap **Apply**.
3. Tap **Import selected pages**. Each page is rendered at a long edge of 1600 px and saved as its own item titled `<file name> p.3/12`, marked with a **PDF** badge in History. The first page opens immediately; the others are waiting in History.

Details:
* A single-page PDF skips the picker and opens right away.
* Importing more than 30 pages at once asks for confirmation (each page uses roughly 300–600 KB of storage).
* Password-protected PDFs prompt for the password.
* Pages with their own rotation are imported upright.

### About pdf.js and the first-time download
PDF rendering uses **Mozilla pdf.js 3.11.174** (Apache License 2.0). It is **not bundled** in the HTML file; the first time you open a PDF the app downloads it, trying these sources in order and stopping at the first that works:

1. Files placed next to the HTML (`pdf.min.js`, `pdf.worker.min.js`, `cmaps/`, `standard_fonts/`)
2. jsDelivr
3. cdnjs
4. unpkg

Only the library is downloaded. **The PDF itself never leaves your device.** Photo features do not need a network at all.

**Fully offline PDFs:** copy `pdf.min.js` and `pdf.worker.min.js` from `pdfjs-dist@3.11.174` (`legacy/build`) into the same folder as the HTML file. Adding the `cmaps/` and `standard_fonts/` folders helps with PDFs whose fonts are not embedded (these folders are used when the app is served over http(s)). If the library cannot be loaded, the app explains why and everything else keeps working.

---

## 5. Sample pages and the demo

* **Try a sample** creates a fictional textbook page inside the app so you can practice marking.
* **Watch the demo** marks five terms on that page automatically and pre-fills them, so you can go straight to **Make a quiz**.

| Edition | Sample pages |
|---|---|
| Japanese | 光合成のしくみ (photosynthesis and the three states of water) |
| English v1.1 | *Photosynthesis* — how plants make food, and the three states of water |
| English v1.2 | A chooser with four subjects: **Science** — *Photosynthesis*; **History** — *From Workshops to Factories* (the Industrial Revolution); **Math** — *Triangles*; **Civics** — *Three Branches of Government*. Each page has five demo terms, including multi-word terms and a numeric term. |

All sample text is generated inside the app and written as generic school material; no real people appear.

---

## 6. Your data and privacy

* Everything — photos, marks, terms, and scores — is stored **only in your browser** (IndexedDB). Nothing is uploaded.
* The two editions use **separate databases** (`markerQuizDB` for Japanese, `markerQuizDB_en` for English), so you can keep both on one device without mixing their history.
* **Export / Import:** each history item can be exported as a JSON file (image, strokes, spots, terms, and finished quiz results) and imported again on any device or in either edition. Importing an item that already exists creates a copy.
* **Delete:** individual scores or whole items can be deleted from History.
* Clearing the browser's site data removes everything — export anything you want to keep first.
* If the browser blocks IndexedDB (for example inside some sandboxed previews), the app falls back to in-memory storage and warns you that data will be lost when the page closes.

---

## 7. Install it like an app

* **iPhone (Safari):** tap **Share → Add to Home Screen**.
* **Android (Chrome):** open the menu (⋮) → **Add to Home screen** or **Install app**.
* The file also works when saved to the Files app, Google Drive, or any folder — just open it from there.

---

## 8. Under the hood

Each edition is one self-contained HTML file with two clearly separated layers:

* **Backend layer (`LocalBackend`)** — runs entirely on the device: storage (IndexedDB with an in-memory fallback), spot detection from strokes, quiz generation, wrong-answer generation, scoring, history, and export/import. It exposes a small Promise-based, REST-style API: `createSession`, `getSession`, `saveMarks`, `detectRegions`, `saveTerms`, `generateQuiz`, `submitAnswer`, `finishQuiz`, `listHistory`, `deleteSession`, `deleteQuiz`, `exportSession`, `importSession`.
* **Frontend layer** — screens, the canvas marking engine (zoom/pan, strokes, layers), the PDF page picker, and the quiz/results UI. It talks to the backend only through the API above.
* **`RemoteBackend`** — a ready-made skeleton with the same interface that calls a REST server over `fetch`. Set `USE_REMOTE_BACKEND = true` and `REMOTE_BASE_URL` to move to a synced, server-backed version without touching the UI.

Other notes:
* No build step, no frameworks, no external dependencies except pdf.js (loaded on demand).
* Light and dark themes follow the system setting; layouts adapt to small phones and landscape.
* Accessible controls: labeled buttons, live announcements, keyboard shortcuts.
* A testing hook is available in the browser console as `window.__markerQuiz`.

---

## 9. Known limitations

* There is no text recognition (OCR). Terms are typed by hand; untyped spots use image choices.
* Opening a PDF for the first time needs an internet connection unless pdf.js is placed next to the HTML file (§4).
* When opened as a local file (`file://`), pdf.js runs its worker on the main thread; large PDFs may take a moment to render.
* Drag-and-drop import is desktop-only.
* Sample pages are fictional teaching material, not a substitute for a real textbook.

---

## 10. Third-party notices

* **pdf.js** — © Mozilla and contributors, Apache License 2.0. Downloaded at runtime; not modified.
* Interface icons are based on Material Design icon paths (Apache License 2.0).

---

## 11. Version history

| Version | Date | Highlights |
|---|---|---|
| Japanese v1.0 | 2026-09-20 | Photo → mark → 4-choice quiz; three difficulty levels; history; JSON export/import |
| Japanese v1.1 | 2026-09-23 | PDF import with page picker, password support, PDF badge in History; desktop drag-and-drop |
| English v1.1 | 2026-09-23 | Full English edition; English-aware wrong-answer engine; English sample page; separate database |
| English v1.2 | 2026-09-23 | Sample chooser with Science, History, Math, and Civics pages |

---

Created by Dr. HATAYAMA, SHUNSUKE D.C.(ITL) · 2026-09-23
