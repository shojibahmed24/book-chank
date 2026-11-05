# Class 9–10 ICT Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 ICT **guide** bank. The two
are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির ICT
গাইডের প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions (`questions-part*.json`) | 3,575 |
| Prose chunks (`chunks.json`) | 132 |
| Set entries | 71 |
| Held rows (file_held, in audit) | 356 |

The same 3,575 rows and 132 chunks are live in the app database.
Chapter split: ch2 536, ch4 861, ch5 909 (split at import into chapter 5:
470 and chapter 6: 439), practical 115, special 910, board 234,
supplement 10. Keyless MCQs: 0.

## File formats

- `questions-part1.json`, `questions-part2.json` — each part is a valid
  JSON array; concatenate the arrays in filename order to recover the
  full 3,575-row list (part files, per the root README rule: no single
  file above ~4 MB).
- `chunks.json` — one JSON array, 132 chunks.
- `pointer-resolutions.json` — the special pointer resolutions, including
  the 46-entry supplement merged into the main file (320 entries in
  total; 11 overrides of near targets, 9 confirmations, 26 previously
  unmatched now matched). Re-running the ICT import build would
  regenerate the resolutions file and LOSE these content-match
  corrections unless the supplement is re-merged.
- `held-dispositions-2026-11-04.md` — the 26 held rows, decided: 1
  accepted (ch6-179), 1 dropped outright (ch5-007, no printed key),
  13 marked for a future guide, 11 marked picture-dependent.
- Open note: the 2026-11-04 dry-run plan listed ict-ch6-mcq-bank-179
  as a new row to INSERT, but it is still held in the ict-ch5.json
  held array. The file total 3,575 matches live, so whether that row
  actually reached live cannot be verified from the files.

## What is NOT in this copy

- The per-chapter collection files (ict-ch2 … ict-special, ict-board) —
  merged into `questions.json` here.
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: a printed Class 9–10 ICT guide (scan; publisher/edition as
  printed in the guide). Book id `class9-ict-bn-guide`.
- Pipeline: page rendering → OCR → visual verification → pointer
  triage → import audit (`import-audit.json`, dry run).
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Build 2026-11-04. Rows and chunks match the live database counts
exactly (3,575 / 132). Decisions complete.
