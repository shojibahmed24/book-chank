# Class 9–10 Economics Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 Economics **guide** bank.
The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির
অর্থনীতি গাইডের প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions (`questions-part1.json`, `questions-part2.json`, `questions-part3.json`) | 4360 |
| Prose chunks (`chunks.json`) | 81 |

Questions by section:

| Section | Rows |
|---------|------|
| activity | 39 |
| board | 678 |
| creative | 461 |
| descriptive | 24 |
| knowledge-comprehension | 358 |
| mcq-bank | 1227 |
| model | 318 |
| short-qa | 354 |
| special-model | 901 |

## File formats

- `questions-part1.json` (1503 rows) + `questions-part2.json` (1852 rows) + `questions-part3.json` (1005 rows) — each part is a valid JSON array; together they hold all
  4360 import rows (files over ~4 MB are split into parts — repo rule).
- `chunks.json` — one JSON array, 81 chunks.
- `import-audit.json` — the import-preparation audit (decisions, checks,
  held/dropped rows).

## What is NOT in this copy

- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: Lecture SSC Economics Guide Exam 2026 (printed guide, scanned; subject code 141).
- Pipeline: page rendering (500 dpi) → OCR → visual verification
  against rendered pages → import-preparation audit.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Import snapshot 2026-11-06. Live in the Yes Sir AI database since the
2026-11-06 joint batch write (BGS + General Science + Economics).
