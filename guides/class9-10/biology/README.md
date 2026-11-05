# Class 9–10 Biology Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 biology **guide** bank.
The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির
জীববিজ্ঞান গাইডের প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions (`questions-part*.json`) | 4,297 |
| Prose chunks (`chunks.json`) | 49 |
| Set entries | 67 |
| Held rows (file_held, in audit) | 1,138 |
| Board recollected rows (`board-recollected.json`) | 214 |

Chapters: ch1 473, ch2 586, ch3 320, ch4 520, ch11 351, ch12 565,
ch13 463, practical 111, special-board 908.

**How the counts relate:** the import audit reports `file_rows` 4,297
and `db_rows` 5,584, and the program log reports 5,798 live rows.
The board recollection adds 214 importable rows: 5,584 + 214 = 5,798,
matching live. The file rows (4,297 + 214 = 4,511) are fewer than the
live rows for the same reason as Islam: parts-rows are combined in the
files and split into separate rows in the database. Do not fill the
difference by guessing.
**Open caveat:** the key-grid v4 backfill is a file-only dry run — no
database write was made. The pushed chapter files still carry 650 grid
rows with NULL keys in bio-special-board.json, unlike the live database
keys. The v4 merge is still open.

## File formats

- `questions-part1.json`, `questions-part2.json` — each part is a valid
  JSON array; concatenate the arrays in filename order to recover the
  full 4,297-row list (part files, per the root README rule: no single
  file above ~4 MB).
- `chunks.json` — one JSON array, 49 chunks.
- `board-recollected.json` — board rows recovered after the first pass:
  214 importable (board-mcq 179, board-creative 35), 73 unrecovered,
  3 picture-excluded. Original stub fields preserved verbatim; only the
  listed overlay fields were added.
- Held families in the audit: diagram 686, key-conflict 18, truncation
  68, other-illegible 6, scan-missing 5, occluded 4, illegible-native 60,
  parts-not-printed 1, out-of-syllabus 290.

## What is NOT in this copy

- The per-chapter collection files (bio-ch1 … bio-special-board) —
  merged into `questions.json` here. Fragment files inside the chapter
  folders are intermediate snapshots, not final data.
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: a printed Class 9–10 biology guide (scan; publisher/edition
  as printed in the guide).
- Pipeline: page rendering → OCR → visual verification → board
  recollection → import audit (`import-audit.json`, dry run).
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Build 2026-11-02 (audit). File rows 4,297; audit db_rows 5,584;
live 5,798 (audit + board recollection 214; parts-rows split in the
database). v4 merge still open.
