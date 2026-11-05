# Class 9–10 Higher Math Guide (Newton) — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 higher mathematics **guide**
bank (Newton edition). The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির
উচ্চতর গণিত গাইডের (নিউটন) প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার থেকে সম্পূর্ণ
আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions (`questions-part*.json`) | 3,795 |
| — MCQ bank | 2,163 |
| — Short | 718 |
| — Creative | 547 |
| — Exercise / activity / other | 367 |
| Prose chunks (`chunks.json`) | 58 |
| Chapters covered | 2, 7, 8, 9, 10, 11, 12, 14 |

The same 3,795 rows and 58 chunks are live in the app database.
This is version 2 of the import rows: the v1 build held 3,797 rows and
was superseded by v2 (3,795 rows). Do not re-run the v1 file.

## File formats

- `questions-part1.json`, `questions-part2.json` — each part is a valid
  JSON array; concatenate the arrays in filename order to recover the
  full 3,795-row list (part files, per the root README rule: no single
  file above ~4 MB).
- `chunks.json` — one JSON array, 58 prose chunks (non-problem material
  only, as fallback grounding).
- Row fields: `id`, `book_id`, `chapter_id`, `chapter_number`,
  `guide_source`, `question_text`, `question_type`, `section`, plus
  options, answer key and solution fields where applicable.
- Keyless MCQs: 0.

## What is NOT in this copy

- The v1 import-rows file (3,797 rows) — superseded, kept local only.
- The per-chapter collection rows and the Panjeree edition collection —
  the Panjeree files are a correction reference only, never imported,
  and live outside this folder.
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: Higher Math Guide, Newton edition, Exam 2026 (printed guide,
  scanned).
- Pipeline: page rendering (500 dpi) → OCR → visual verification against
  rendered pages → import-rows build v2, live in the app database at
  3,795 rows and 58 chunks.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Generated 2026-11-05 (import-rows v2). Rows and chunks match the live
database counts exactly (3,795 / 58).
