# Class 9–10 Higher Math Guide (Panjeree) — CORRECTION REFERENCE ONLY

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material.

**This folder is a correction reference only. It is NEVER imported.**
The Higher Math Newton edition is the imported guide (see
`../higher-math-newton/`). When a Newton item is unclear, the matching
Panjeree item here is the correction reference. Nothing in this folder
goes into the app database.

বাংলা সংক্ষেপ: এটা শুধু কারেকশন রেফারেন্স। নিউটন গাইডের কোনো আইটেম
অস্পষ্ট হলে এখান থেকে কারেকশন করা হয়। এই ফোল্ডারের কিছুই অ্যাপের
ডেটাবেসে যায় না, কখনো import হয় না।

## Coverage

| Item | Count |
|------|-------|
| Guide questions (`questions.json`) | 2,651 |
| — Chapter 2 | 422 |
| — Chapter 7 | 411 |
| — Chapter 8 | 617 |
| — Chapter 9 | 671 |
| — Chapter 10 | 530 |
| Prose chunks (`chunks.json`) | 59 |

Chapter 11 is partial (292 rows, no chunks file, no PROGRESS file) and
is NOT in this folder. Chapters other than 2, 7, 8, 9, 10 were never
collected.

## File formats

- `questions.json` — one JSON array, 2,651 rows (small enough to stay
  whole, under ~4 MB). Row fields: `id`, `chapter_number`, `section`,
  `question`, `options`, `answer_key`, `solution`, plus `flag_note`
  and `diagram_dependent` where applicable.
- `chunks.json` — one JSON array, 59 chunks.
- `marking-tagging.md` — the marking/tagging verification for the
  Panjeree guide.

## Notes

- Chapter 8: one p,q creative question was not found in the guide, so
  no row was written for it.
- Chapter 11 (held): the last id uses a Bangla digit 8
  (`hm-pan-ch11-quiz6-৮`) while all other ids use English digits.
- Chapter 9 and 10 rows carry `diagram_dependent` flags where the
  question depends on a diagram.

## What is NOT in this copy

- Chapter 11 (partial) and all uncollected chapters.
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: SSC Higher Math Solution Exam 2026, Panjeree edition
  (printed guide, scanned).
- Pipeline: page rendering (500 dpi) → OCR → visual verification
  against rendered pages → per-chapter PROGRESS verification.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Collection snapshot 2026-11-05. Chapters 2, 7, 8, 9, 10 only.
Correction reference only — never import.
