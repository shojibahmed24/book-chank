# Class 9–10 English 1st Paper Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 English 1st paper **guide**
bank (redo build). The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির
ইংরেজি ১ম পত্র গাইডের প্রশ্নব্যাংক (রিডু বিল্ড) — পাঠ্যবই ফোল্ডার থেকে
সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions, redo (`questions-part*.json`) | 4,855 |
| — Import set (live) | 4,697 |
| — Held writing rows (went to Paper-II bank) | 158 |
| — Test rows in 57 sets | 3,299 |
| — Practice rows | 1,556 |
| Passage backfill (`passage-backfill/`) | 3,995 mapped rows |
| Archive, pre-redo split (`archive/`) | 2,934 questions + 76 chunks |

**Note on 15,240:** that number is the guide-questions table total
after the English import (math 10,543 + English 1st paper 4,697). It is
NOT the English 1st paper count. The 1st paper's own live rows are
4,697.

## File formats

- `questions-part1.json`, `questions-part2.json` — each part is a valid
  JSON array; concatenate the arrays in filename order to recover the
  full 4,855-row list (part files, per the root README rule: no single
  file above ~4 MB). Row fields: `id`, `section`, `question_type`,
  `question_text`, `stimulus_text`, `stimulus_ref`, `options`,
  `answer_key`, `answer_text`, `marks`, `marks_parts`, `test_id`,
  `unit_lesson`, `board_tag`, `verified_visual`,
  `verified_second_pass`, plus flags.
- `passage-backfill/row-text-mapping.json` — passage text mapped to
  3,995 rows. `passage-texts-verified.json` — 263 of 318 passage refs
  verified, 55 unverifiable. `import-audit.json` — backfill result:
  3,870 rows written, 125 dropped.
- **Honest limit:** the backfill wrote 3,870 passage rows, but live
  passage rows are reported as 3,875 — a 5-row gap the files do not
  explain.
- `archive/` — the superseded 2026-10-30 split (`questions.json`
  2,934 rows, `chunks.json` 76, `corrections-log.json` 6 entries,
  `flagged.json` 357 items). Archive only: the redo replaced it, and
  the old files were never the live source.

## What is NOT in this copy

- The 158 held writing rows as a separate Paper-I file — they live in
  the Paper-II bank (`../english-2nd-paper/`).
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: a printed Class 9–10 English 1st paper guide (scan;
  publisher/edition as printed in the guide).
- Pipeline: page rendering → OCR → redo re-transcription with second
  visual pass → passage backfill against verified passage texts.
- English Paper-II is ALWAYS a separate subject — see
  `../english-2nd-paper/`. True/false items always stay true/false,
  never converted to MCQ.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Redo build 2026-11-01. Import set 4,697 rows live.
