# Class 9–10 Bangla 1st Paper Guide — Question Bank (per-lesson)

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material. The
textbook folders (`class6/`, `class7/`) hold verbatim textbook questions
and chunks; this folder holds the Class 9–10 Bangla 1st paper **guide**
bank, collected lesson by lesson. The two are never mixed.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়। নবম-দশম শ্রেণির বাংলা
১ম পত্র গাইডের প্রশ্নব্যাংক, পাঠ ধরে ধরে সংগ্রহ করা — পাঠ্যবই ফোল্ডার
থেকে সম্পূর্ণ আলাদা।

## Coverage

| Item | Count |
|------|-------|
| Verified lessons (`lessons/*.json`) | 16 of 18 |
| Rows in verified lessons | 4,377 |
| Held lessons (verified=false, NOT included) | 2 |

Verified lessons: 1971, am-antir-bhepu, ami-kono-agontuk-noi,
boi-pora, boshekh, brishti, ekusher-golpo, jibon-binimoy,
manush-muhammad, nimgach, probas-bondhu, seidin-ei-math,
shikkha-o-manushotto, subha, tomake-pawar-jonne-he-sadhinota,
umor-faruk.

Held lessons (not in this folder): kopotakkho-nod (277 rows),
prottupokar (379 rows) — both flagged verified=false in the collection.

## File formats

- `lessons/<lesson-slug>.json` — one JSON object per lesson, the ONLY
  collection output per lesson. Contains lesson metadata (title, author,
  printed page range), `rows`, `sets`, `chunks`, `counts` (counted per
  subsection, never estimated), `held` (unverified rows with reasons),
  and `verified` (true only when the per-lesson gate passed: every row's
  text + key + marks eye-checked at 500 dpi, creative-question groups
  complete, key grids re-read).
- `collection-manifest.md` — the collection manifest for the lesson set.
- A lesson counts as complete only when every part is verified and
  merged. Fragment files inside per-lesson folders are older or partial
  snapshots and are NOT included here; the top-level merged lesson file
  is the reliable output.

## Notes

- `1971.json` is much smaller than the other lessons (68 rows; mcq-bank
  12, model-mcq 0, model-creative 0) — recorded as an anomaly, not
  corrected.
- The `class9/bangla-1st-paper/` download set (goddo, kobita, uponnas)
  is BLOCKED at the source (owner disabled download) and holds no data
  files; this folder's lessons come from the talimit collection instead.

## What is NOT in this copy

- The 2 held lessons (kopotakkho-nod, prottupokar).
- Per-lesson fragment files (older/partial snapshots).
- Raw guide PDF, page renders, OCR work files — local only, never pushed.

## Source & provenance

- Source: Panjeree SSC 2026 guide, Bangla 1st Paper (one book, three
  scan files: goddo, poddo, uponnas).
- Pipeline: page rendering (500 dpi) → OCR → visual verification
  against rendered pages → per-lesson verification gate.
- Guide content is commercial guide-book material. This repository holds
  the extraction built for the Yes Sir AI project; take your own decision
  before redistributing guide content elsewhere.

## Version

Collection snapshot 2026-11-05. 16 verified lessons; 2 held lessons
still open.
