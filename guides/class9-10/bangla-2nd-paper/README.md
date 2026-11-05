# Class 9–10 Bangla 2nd Paper Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 Bangla 2nd paper **guide**
bank. The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির বাংলা
২য় পত্র গাইডের প্রশ্নব্যাংক — পাঠ্যবই ফোল্ডার থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Guide questions (`questions.json`) | 2,761 |
| — MCQ (bank + board + model + assessment) | 2,165 |
| — Written (board + model) | 528 |
| — Suggestions (kept as suggestions only) | 68 |
| — Nirmiti (নির্মিতি) | 300 |

The same 2,761 rows are live in the app database. The real exam is
MCQ 30 + written 70, 3 hours, code 102.

## File formats

- `questions.json` — one JSON array, 2,761 rows. Each part of the file
  is a valid JSON array holding a slice of the full list; this file was
  small enough to stay whole (under ~4 MB).
- Row fields: `id`, `book_id`, `question_type` (`mcq`, `written`,
  `suggestion`), `row_kind` (`mcq-bank`, `mcq-board`, `mcq-model`,
  `mcq-assessment`, `written-board`, `written-model`, `nirmiti`,
  `suggestion`), `question_text`, `options`, `answer_key`,
  `guide_solution`, plus flags where applicable.
- Suggestion rows are kept as suggestions and imported as suggestions
  only where an answer exists; answerless suggestions were dropped.
- 17 re-binned rows follow the verified division; writing topics are
  paired with their sample texts.

## What is NOT in this copy

- Answerless directives (23) and 2 chapter-17 suggestion rows — dropped
  entirely under the permanent drop rule.
- The per-chapter collection banks, nirmiti drafts and held rows — local
  collection intermediates, not part of this final package.
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: a printed Class 9–10 Bangla 2nd paper guide (scan; publisher/
  edition as printed in the guide).
- Pipeline: page rendering → OCR → visual verification against rendered
  pages → import-ready build, live in the app database at 2,761 rows.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Generated 2026-11-04 (import-ready build). Rows match the live database
count exactly (2,761).
