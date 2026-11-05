# Class 9–10 English 2nd Paper (Paper-II) Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. English
Paper-II is ALWAYS a separate subject, never folded into Paper-I — see
`../english-1st-paper/`. The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির
ইংরেজি ২য় পত্র (Paper-II) গাইডের প্রশ্নব্যাংক — ১ম পত্র থেকে সম্পূর্ণ
আলাদা বিষয়।

## Coverage

| Item | Count |
|------|-------|
| Paper-II test questions (`questions.json`) | 3,508 |
| — Tests | 60 (paper2-58 … paper2-117) |
| — Rows per test | 59 |
| Held rows (`held.json`) | 32 |
| Import set (live) | 3,666 (3,508 test + 158 bank) |

The 158 bank rows are the writing rows held back from Paper-I
(paragraph 41, email 18, letter 59, composition 40). The exam is
3 hours. Q9 carries partial credit for however much is correct; Q10–12
carry total marks only, with no breakdown. Every true/false item stays
true/false, never converted to MCQ.

## File formats

- `questions.json` — one JSON array, 3,508 rows. Row fields: `id`,
  `test_id`, `section`, `question_text`, `stimulus`, `options`,
  `answer_key`, `answer_text`, `marks`, `marks_parts`, `scored`,
  `board_tag`, `source_pdf_page`, `source_printed_page`, `flag_note`.
- `held.json` — 32 held rows (`id`, `section`, `test_id`, `marks`,
  `reason`). These were NOT imported as usable rows.
- `merge-stats.json` — tests 60, rows 3,508, held 32, total 3,540,
  marks 6,000, held158 158.
- `paper2-dryrun-report.md` — the dry-run report; the third live
  attempt committed 3,666 rows, verified per-section.

## What is NOT in this copy

- The per-test files (`tests/paper2-58.json` … `tests/paper2-117.json`)
  — merged into `questions.json` here.
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: a printed Class 9–10 English 2nd paper guide (scan;
  publisher/edition as printed in the guide). Book id
  `class9-english-2nd-bn-guide`, separate subject `english-2nd`.
- Pipeline: page rendering → OCR → per-test build → merge → dry run →
  live commit.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Build 2026-11. Import set 3,666 rows live.
