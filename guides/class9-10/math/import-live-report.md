# Talimit Math — live import, full implementation (2026-10-31)

## User orders implemented
- Both systems: textbook chapter number AND guide chapter number both
  find guide rows (user-confirmed: the names/numbers are the same).
- Import everything EXCEPT rows the assistant judges answer-wrong.
- Third-decision rows: NOT in the app for now (user order 04:31).
- Model test: one set `model-test`, browse-only, never scored.

## What changed (code, all verified locally)
- Edge `guide-bank` (deno check PASS):
  - `list`: filter = (textbook chapter_id for the number) OR
    (guide_questions.chapter_number = the number); setId path =
    book_id + set_id only (sets are chapter-free by design).
  - `sets`: filtered by book_id (was chapterIds — that hid
    chapter-free set rows entirely).
  - NEW action `guideChapters`: bank rows grouped by guide chapter
    number (total + keyed counts), with a textbook-grouping
    fallback for pre-migration servers.
- Migration `011_guide_chapter_number.sql`: adds
  `guide_questions.chapter_number int NULL` (no backfill: old
  class-7 rows keep resolving through textbook chapter_id).
- Client: `guide_bank_service.fetchGuideChapters()`; quiz
  `fetchPool()` falls back to guide-native numbers when the
  textbook list is empty; guide chapters tab falls back to
  server guide chapters when textbook + cache are both empty.
  Analyze clean on all 3 touched files; all files ≤250 lines.
- Import script `math/_work/import_live.py` (dry-run PASS, no DB):
  one guide book row `class9-math-bn-guide` (class 9, math, bn,
  supplied=false — textbook subject stays locked), chapter_id
  NULL, chapter_number from the file chapter_id, set_id
  `model-test` for ch0 rows only, answer_key MCQ-only,
  marks always NULL. Single transaction with pre/post checks;
  rerun-safe (already-imported state detected, partial state
  aborts). `questions_with_options.json` never overwritten.

## Dry-run numbers (exact)
- Source 3720 rows, all ids unique.
- Excluded 10: 1 proven-wrong
  (`class9-10-math-ch2-p30-n201-problem`: printed key kh,
  maths yields gha) + 9 third-decision held rows (exact ids in
  the script; patterns are NOT used — p329-n6 must not exclude
  p329-n60/n62, p383-n4 must not exclude p383-n43/n47/n48).
- Import 3710: bank 3472, model-test set 238.
- By chapter_number: 2:347, 3:474, 7:430, 8:768, 9:319, 11:235,
  16:532, 17:367.
- Quiz pool (full-optioned + keyed bank MCQ): 904.
- guide_chunks (52) NOT imported: OCR text heavily garbled,
  unverified as AI grounding.

## Tagging — honest state
- Mechanism is FULLY live (migration 010 + Edge Mode G v6 +
  client prompt flow): a tagged row's prose is the ONLY fallback.
- Tags placed: 0. A verbatim-proof pass over the live class-7
  guide (2864 questions × 24 chunks, 230 sentences ≥50 chars)
  matched 0 rows — solutions do not quote prose verbatim, so
  tags cannot be auto-proven. Talimit prose chunks are garbled
  OCR and not imported, so Talimit tags cannot be placed at all
  until those chunks are visually transcribed. Tag placement is
  a human/verified curation pass, chapter by chapter; it is NOT
  invented here, because a wrong tag grounds answers in the
  wrong prose (worse than no fallback).

## Tests
- Flutter: guide_chapters_loading (10) + cached_indicator (6) +
  guide_error (4) + weak_revision (2) = 22/22 passed.
- Edge guide-bank: deno check PASS (after a type fix for the
  two-variant query builder).
- Import script dry-run: PASS (3710 / 238 / 904).

## Still blocked (needs the user, once)
- Live import: Postgres password (fresh, never stored).
- Edge deploy (guide-bank v4, with migration 011 applied first
  by the import script): fresh Supabase CLI token.
- Then: fresh APK build from current code → phone test of
  class-9 guide chapters, quiz pool, and model-test set.
