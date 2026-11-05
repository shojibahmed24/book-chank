# Class 9–10 Mathematics Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 mathematics **guide** bank.
The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির গণিত
গাইডের প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions, consolidated (`questions-part*.json`) | 3,720 |
| — MCQ | 1,676 (1,170 with full options) |
| Redo pilot units (`pilot/*/transcribed_units.json`) | 7,366 |
| Prose chunks, reference only (`chunks.json`) | 52 |
| Corrections log (`corrections-log.json`) | 1,222 |
| Flagged items (`flagged.json`) | 1,948 |

## Two layers — read this first

1. **Consolidated package** (`questions-part*.json`): the merged final
   file with options. It was the source of the FIRST live import
   (3,710 rows imported after 10 rows were dropped: 1 proven error,
   9 held on third-decision). Chapters: ch0 model tests 238, ch2 348,
   ch3 474, ch7 430, ch8 777, ch9 319, ch11 235, ch16 532, ch17 367.
2. **Redo pilots** (`pilot/`): per-chapter re-transcribed units that are
   the source of the CURRENT live content — pilot-0 (model tests, 690),
   pilot-2.1 + pilot-2.2 (ch2, 862), pilot-3 (ch3, 1,411), pilot-7
   (ch7, 443), pilot-8 (ch8, 952), pilot-9 (ch9, 787), pilot-11
   (ch11, 441), pilot-16 (ch16, 1,067), pilot-17 (ch17, 713).

**Honest limit:** the live database holds 10,543 math rows, and the
files here do NOT fully reconstruct it. Pilot units total 7,366 against
7,679 live Class 9 rows (a 313-row gap), and only 619 pilot-to-live
links are verified. Do not fill the gap by guessing. See
`phase2-remaining-report.md` and `import-dryrun-2026-11-01.md`.
(The often-quoted 15,240 is the guide-questions table total after the
English import: math 10,543 + English 1st paper 4,697.)

## File formats

- `questions-part1.json` … `questions-part3.json` — each part is a valid
  JSON array; concatenate the arrays in filename order to recover the
  full 3,720-row list (part files, per the root README rule: no single
  file above ~4 MB). Row fields: `id`, `chapter_id`, `question_text`,
  `question_type`, `options` (MCQ only), `answer_key`,
  `guide_solution`, `display_policy`, `marks`, `section`, `source_tag`,
  `verification_note`, `verified_visual`, plus `depends_on`.
- `pilot/<name>/transcribed_units.json` — one JSON array per pilot
  (25 fields per unit). Each file was small enough to stay whole.
- `chunks.json` — 52 prose chunks. **Reference only:** the chunk text
  is heavily garbled OCR and was never imported live.
- `corrections-log.json` — 1,222 entries (`id`, `field`, `basis`,
  `source_file`). `flagged.json` — 1,948 entries (`id`, `kind`,
  `reason`).

## What is NOT in this copy

- The older per-chapter `_part` files (fully merged into the
  consolidated package) and the superseded `_complete` revision chain
  (only the merged result is kept) — local history only.
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: a printed Class 9–10 mathematics guide (scan; publisher/
  edition as printed in the guide).
- Pipeline: page rendering → OCR → visual verification against rendered
  pages → merged consolidation → redo pilot re-transcription.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Consolidated package generated 2026-11-01 (first live import). Pilot
files are the redo source of the current live content. Live row count
10,543 is NOT fully reproducible from these files — see the honest limit
above.
