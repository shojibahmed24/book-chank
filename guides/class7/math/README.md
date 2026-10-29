# Class 7 Math Guide — Question Bank (separate from textbooks)

Guide data for the **Yes Sir AI** tuition app, kept in its own folder on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 7 mathematics **guide** pilot.
The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। সপ্তম শ্রেণির গণিত
গাইডের প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার (`class6/`, `class7/`) থেকে সম্পূর্ণ
আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions (`questions.json`) | 2,864 |
| — MCQ | 1,594 |
| — Creative | 813 |
| — Problem | 430 |
| — Task | 26 |
| — Matching | 1 |
| Prose chunks, corrected (`chunks_corrected.json`) | 24 |
| Corrections log (`corrections-log.json`) | 77 entries |
| Flagged, still unresolved (`flagged.json`) | 1 |

Chapters 1–11, all covered. Class tests are kept as separate `set_id`
rows (5a: 11, 5b: 18, 7a: 19) and are NOT mixed into the chapter bank.
No importance stars are set anywhere.

## Display policy (baked into every row)

Each question row carries `display_policy`:

- `verbatim` (1,607 rows) — MCQ and short questions: shown verbatim
  (question + options + correct answer), and the app explains why the
  answer is correct.
- `ai_rewrite` (1,257 rows) — creative, long, and problem items: the app
  NEVER shows the guide's worked solution verbatim. It writes a fresh
  step-by-step solution grounded in the guide's worked solution.

## Repo copy vs app display (read this first)

The app still follows the display policy above: it NEVER shows the
guide's worked solution verbatim for `ai_rewrite` items. This repository
copy is different — it is a **personal backup**, not app content, and it
**does include** `guide_solution` (the guide's worked solutions, 1,618
values) so the full pilot data is preserved in one place. The repo will
be made private later; until then, treat this copy as a backup, not as
something the app serves.

## What is NOT in this copy

The raw uncorrected chunks (`chunks.json`) and the OCR/PNG work files
stay local and are not pushed. Everything else from the pilot final
package is here.

## Guide errors — never auto-score these 18

`corrections-log.json` contains 18 entries of kind `guide_error_mcq`
with `never_auto_score: true`: the guide's printed key for these MCQs is
wrong. They keep their printed key in `questions.json` (audit trail) but
must NEVER be auto-scored from it. The log gives the corrected value.
The other 58 log entries are guide notes and 1 is a prose correction.

## Still flagged (1)

One item stays flagged: a chapter-9 problem whose solution is not printed
in the guide at all. It is a guide gap, not an extraction error, and is
recorded in `flagged.json` with its reason.

## File formats

- `questions.json` — one JSON array, 2,864 rows. Fields: `id`,
  `chapter_id`, `question_text` (verbatim), `question_type` (lowercase
  canonical: `mcq`, `creative`, `problem`, `task`, `matching`),
  `answer_key` (MCQ only, 1,594 rows), `marks`, `section`, `source_tag`
  (school/test-paper provenance where printed), `display_policy`,
  `guide_printed_page`, `pdf_page`, `pdf_file`, `verification_note`,
  `verified_visual`.
- `chunks_corrected.json` — 24 prose chunks (non-problem material only,
  as fallback grounding). Math chunking is per-problem: one problem with
  its full details is one chunk unit, never split, never merged.
- `corrections-log.json` — 77 entries: `guide_error_mcq` (18),
  `guide_note` (58), `prose_error` (1).
- `coverage-map.json` — per-chapter coverage of the guide scan.

## Source & provenance

- Source: a printed Class 7 mathematics guide (244 scanned pages,
  image-only; publisher/edition year unknown — the scan has no cover or
  inner pages, and the drive filename's "2025" is not evidence).
- Pipeline: page rendering → OCR → visual verification against rendered
  pages (200dpi re-reads for doubtful dots/glyphs/keys) → correction
  from the printed page, never guessed.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Generated 2026-10-29 (pilot final). Only the Class 7 mathematics guide
is extracted; the other 15 downloaded Class 7 guides are not yet
extracted and are not in this folder.
