# Class 9–10 BGS (Bangladesh & Global Studies) Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 BGS (Bangladesh & Global Studies) **guide** bank.
The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির
বাংলাদেশ ও বিশ্বপরিচয় গাইডের প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions (`questions.json`, `questions-part2.json`, `questions-part3.json`) | 3410 |
| Prose chunks (`chunks.json`) | 52 |

Questions by section:

| Section | Rows |
|---------|------|
| activity | 59 |
| creative | 333 |
| descriptive | 17 |
| knowledge-comprehension | 562 |
| mcq-bank | 1114 |
| model | 203 |
| short-qa | 327 |
| special-model | 795 |

## File formats

- `questions.json` (1528 rows) + `questions-part2.json` (1632 rows) + `questions-part3.json` (250 rows) — each part is a valid JSON array; together they hold all
  3410 import rows (files over ~4 MB are split into parts — repo rule).
- `chunks.json` — one JSON array, 52 chunks.
- `import-audit.json` — the import-preparation audit (decisions, checks,
  held/dropped rows).

## What is NOT in this copy

- Raw guide PDF, page renders, OCR work files — local only, never pushed.
- Held chunks (7) — not imported, not in this copy.

## Source & provenance

- Source: Newton BGS Guide, SSC 2026 (printed guide, scanned; subject code 150).
- Pipeline: page rendering (500 dpi) → OCR → visual verification
  against rendered pages → import-preparation audit.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Import snapshot 2026-11-06. Live in the Yes Sir AI database since the
2026-11-06 joint batch write (BGS + General Science + Economics).
