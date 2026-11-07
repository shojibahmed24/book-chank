# Class 9–10 Civics (পৌরনীতি ও নাগরিকতা) Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির
পৌরনীতি ও নাগরিকতা (Panjeree) গাইডের চাংক।

## Coverage

| Item | Count |
|------|-------|
| Prose chunks (`chunks.json`) | 64 |

## Honest limits

- Live in the app DB since 2026-11-07: 3,838 rows + 64 chunks; 529
  keyless MCQs written with answer_key NULL (Part B MCQ key rate 23.6%).
- Chapters in the printed 2026 rearranged syllabus: 1, 3, 4, 6, 7, 8
  only — chapters 2 and 5 do not exist in the syllabus, not a
  collection gap.
- App-visibility caveat: chapters 1/3/4 return 0 in the Edge chapter
  list because their rows carry set_id; chapters 6/7/8 show fine.
  Phase-5 app-QA item, no DB change.
- One chunk's guide_error flag was lost (no such column in
  guide_chunks, no migration).
