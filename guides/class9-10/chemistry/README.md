# Class 9–10 Chemistry Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 chemistry **guide** bank.
The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির রসায়ন
গাইডের প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions (`questions-part*.json`) | 5,784 |
| — MCQ (board-mcq + mcq-bank + model-mcq) | 2,794 |
| — Creative / short / knowledge / other | 2,990 |
| Chapters covered | 3, 4, 5, 6, 7, 11 + board + special model sets |
| Held-out rows (see `chemistry-held-out-2026-11-04.md`) | 24 |

Reconciliation (see `chemistry-import-verification-2026-11-04.md`):
collection 5,808 rows − 24 excluded = 5,784 import-ready rows. The same
5,784 rows are live in the app database. Duplicate ids: 0. MCQ rows with
a null key: 0. Rows with empty question text: 0.

## File formats

- `questions-part1.json`, `questions-part2.json`, `questions-part3.json`
  — each part is a valid JSON array; concatenate the arrays in filename
  order to recover the full 5,784-row list (part files, per the root
  README rule: no single file above ~4 MB).
- Row fields: `id`, `chapter`, `question_number`, `section`, `set_id`,
  `question` (verbatim), `options`, `answer_key`, `guide_solution`,
  plus flags where applicable. Note the field is `question`, not
  `question_text`.
- 490 rows are pointer-only: `guide_solution` is NULL and the pointer is
  kept verbatim in the note — never converted, never guessed.
- 19 part-level out-of-syllabus rows are kept flagged in-row, not split.

## What is NOT in this copy

- The 24 held-out rows (word variants 11, board held-near pointers 4,
  keyless/defective MCQs 7, ch7 activity section 2) — listed with reasons
  in `chemistry-held-out-2026-11-04.md`. They stay in the local collection
  files and wait for owner decisions; the 7 keyless/defective rows fall
  under the permanent drop rule.
- The 148 board out-of-syllabus held entries and the 32-row scan gap
  (printed pages 545–576) plus 95 unreadable rows — held entries, not
  rows; marked for an alternate guide.
- The 114 collection chunks — chunk import is a separate batch step, not
  built here.
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Open owner items

- Word-variant rows (11) and board held-near pointer rows (4): owner
  decides which transcription / target stands.
- Board out-of-syllabus 148: import form (flag vs drop) still open.
- Special model-MCQ sets 07–22 (400 rows): keys are grid-verbatim as
  collected; section 9.18 re-verification for those sets was pending.

## Source & provenance

- Source: a printed Class 9–10 chemistry guide (scan; publisher/edition
  as printed in the guide).
- Pipeline: page rendering → OCR → visual verification against rendered
  pages → grid-audit corrections (section 9.18: 612 verdicts, 88 key
  corrections applied) → import-ready build 2026-11-04.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Generated 2026-11-04 (import-ready build). Rows match the live database
count exactly (5,784).
