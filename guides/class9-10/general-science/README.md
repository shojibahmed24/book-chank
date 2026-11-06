# Class 9–10 General Science Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 General Science **guide** bank.
The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির
সাধারণ বিজ্ঞান গাইডের প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions (`questions-part1.json`, `questions-part2.json`, `questions-part3.json`) | 5540 |
| Prose chunks (`chunks.json`) | 101 |

Questions by section:

| Section | Rows |
|---------|------|
| activity | 15 |
| board | 1096 |
| comprehension | 54 |
| creative | 419 |
| knowledge | 58 |
| knowledge-comprehension | 215 |
| mcq-bank | 1571 |
| model | 318 |
| short-qa | 524 |
| special-model | 794 |
| super-quiz | 476 |

## File formats

- `questions-part1.json` (1918 rows) + `questions-part2.json` (1831 rows) + `questions-part3.json` (1791 rows) — each part is a valid JSON array; together they hold all
  5540 import rows (files over ~4 MB are split into parts — repo rule).
- `chunks.json` — one JSON array, 101 chunks.
- `import-audit.json` — the import-preparation audit (decisions, checks,
  held/dropped rows).

## What is NOT in this copy

- Raw guide PDF, page renders, OCR work files — local only, never pushed.
- Held chunks (8) — not imported, not in this copy.

## Source & provenance

- Source: Newton General Science Guide, Lecture Publications Ltd., Feb 2025, SSC 2026 (printed guide, scanned; subject code 127).
- Pipeline: page rendering (500 dpi) → OCR → visual verification
  against rendered pages → import-preparation audit.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Import snapshot 2026-11-06. Live in the Yes Sir AI database since the
2026-11-06 joint batch write (BGS + General Science + Economics).
