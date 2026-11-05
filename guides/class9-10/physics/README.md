# Class 9–10 Physics Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 physics **guide** bank.
The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির
পদার্থবিজ্ঞান গাইডের প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions, normalized (`questions-part*.json`) | 6,700 |
| Prose chunks (`chunks.json`) | 72 |
| Sets (`sets.json`) | 66 |
| Held rows (`held.json`) | 369 |

The same 6,700 rows and 72 chunks are live in the app database.
Keyless MCQs: exactly 13. Chapters: ch1 671, ch2 820, ch3 827,
ch4 876, ch7 765, ch8 762, ch10 666, practical 70, special 849,
board 394 (rows before held). Chapters 5, 6 and 9 have no collection
files. Note: the collection file for ch8 holds 763 rows, but the
normalized file holds 762 — one row was moved to held during the
correction pass (6,701 rows before correction, 6,700 after).

## File formats

- `questions-part1.json` … `questions-part4.json` — each part is a valid
  JSON array; concatenate the arrays in filename order to recover the
  full 6,700-row list (part files, per the root README rule: no single
  file above ~4 MB).
- `chunks.json` — one JSON array, 72 chunks. `sets.json` — 66 sets.
  `held.json` — 368 held rows.
- Row fields follow the normalized schema (`id`, `book_id`,
  `chapter_id`, `section`, `question_text`, `options`, `answer_key`,
  plus solution and flag fields where applicable).

## What is NOT in this copy

- The per-chapter collection files (phy-ch1 … phy-special, phy-board)
  — merged into the normalized file here.
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: a printed Class 9–10 physics guide (scan; publisher/edition
  as printed in the guide). Book id `class9-physics-bn-guide`.
- Pipeline: page rendering → OCR → visual verification → normalization
  → import prep (`import-prep-report.md`, `import-audit.json`).
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Normalized build 2026-11-03. Rows and chunks match the live database
counts exactly (6,700 / 72).
