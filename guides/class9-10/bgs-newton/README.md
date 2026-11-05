# Class 9–10 BGS (Bangladesh & Global Studies) Guide, Newton — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 BGS **guide** bank (Newton
edition). The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির
বাংলাদেশ ও বিশ্বপরিচয় গাইডের (নিউটন) প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার
থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions (`questions.json`) | 1,255 |
| — Chapter 2, verified complete | 313 |
| — Chapter 3, verification claimed (see note) | 561 |
| — Chapter 6, verified complete | 381 |
| Prose chunks (`chunks.json`) | 23 |

Chapters 10, 11 and 13 are still being collected and are NOT in this
folder. Chapters 1, 4, 5, 7, 8, 9, 12, 14, 15, 16 have no collection
files yet.

## Verification note — chapter 3

Chapter 3's PROGRESS file (`ch3-progress.md`) claims final verification:
561 lines, all valid JSON, unique ids, no HELD rows, model MCQ keys
checked against the answer grid. An earlier coordinator note called the
chapter still in progress while joined-JSON line errors were being
fixed. During push preparation every one of the 561 lines was
independently validated as JSON. The chapter is included on the strength
of the PROGRESS claim plus that validation. Open items recorded in the
PROGRESS file: model written section HELD, folio 118 missing.

Chapter 2 open items: model written section HELD, folio 42 missing.
Chapter 6 open items: 3 HELD parts, folios 132, 133, 178.

## File formats

- `questions.json` — one JSON array, 1,255 rows (small enough to stay
  whole, under ~4 MB). Row fields: `id`, `chapter_number`, `lesson`,
  `section`, `subtype`, `question_text`, `options`, `answer_key`,
  plus `guide_solution`, `flag_note`, `held_reason` where applicable.
- `chunks.json` — one JSON array, 23 chunks.
- `ch2-progress.md`, `ch3-progress.md`, `ch6-progress.md` — the
  per-chapter verification notes. `marking-tagging.md` — the
  marking/tagging verification for the Newton guide.

## What is NOT in this copy

- Chapters 10, 11, 13 (in progress) and all uncollected chapters.
- The Panjeree edition of the BGS guide — correction reference only,
  never imported.
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: SSC BGS Guide Exam 2026, Newton edition (printed guide,
  scanned).
- Pipeline: page rendering (500 dpi) → OCR → visual verification
  against rendered pages → per-chapter PROGRESS verification.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Collection snapshot 2026-11-05. Chapters 2, 3, 6 only; the rest are
still being collected.
