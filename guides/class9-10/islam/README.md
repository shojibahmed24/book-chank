# Class 9–10 Islam Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 Islam **guide** bank. The
two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির ইসলাম
গাইডের প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions, normalized (`questions-part*.json`) | 4,293 |
| Prose chunks (`chunks.json`) | 105 |
| Sets (`sets.json`) | 85 |
| Held, excluded (`held-excluded.json`) | 26 |

**Honest limit:** the import audit reports `db_rows` 5,697 against
`file_rows` 4,293 — a 1,404-row gap the files do not explain. The live
count 5,697 is the program-log figure; this folder holds the 4,293-row
normalized file that the audit itself records. Do not fill the gap by
guessing.

## File formats

- `questions-part1.json` … `questions-part3.json` — each part is a valid
  JSON array; concatenate the arrays in filename order to recover the
  full 4,293-row list (part files, per the root README rule: no single
  file above ~4 MB).
- `chunks.json` — one JSON array, 105 chunks. `sets.json` — 85 sets.
  `held-excluded.json` — 26 held rows, excluded from import.
- Sections in the file: quiz 272, mcq-bank 1,152, short-qa 162,
  knowledge-qa 354, creative 659, qb-creative 112, qb-short 50,
  model-mcq 510, model-creative 166, model-short 230,
  comprehension-qa 35, activity 21, board-mcq 810, board-creative 1,164.
- Exactly one keyless MCQ is kept NULL by owner decision:
  `isl-ch2-mcq-bank-004`.

## What is NOT in this copy

- The per-chapter collection blocks (islam-ch1 … ch5, board, models,
  appendix, suggestions) — merged into the normalized file here.
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: a printed Class 9–10 Islam guide (scan; publisher/edition as
  printed in the guide).
- Pipeline: page rendering → OCR → visual verification → normalization
  (`normalization-log.md`) → import audit (`import-audit.json`).
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Normalized build 2026-11-02. File rows 4,293; audit db_rows 5,697
(gap unexplained — see honest limit above).
