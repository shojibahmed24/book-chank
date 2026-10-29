# Class 7 — Final Copy: Consolidation Report (2026-10-29)

**Scope:** all 22 Class 7 subjects, both book rows (bn + en), built from the
CURRENT per-subject files under `supabase/class7/{chapters,questions,
chunks,chunks_corrected}/`. No per-subject source file was modified.
**Row 23 (minority-language book) is EXCLUDED** — not downloaded, pending user
decision; it appears nowhere in the combined files except in this note.
**No DB write, migration, APK, or deploy was done here** — file stage only.

**Parent rulings applied** (see `supabase/class7/_work/parent-rulings-2026-10-29.md`):
1. EFT passage-stimulus handling accepted as-is (rows name the exact lesson
   passage/section; full lesson repetition rejected as infeasible).
2. Chapter-final short chunks accepted as-is (merging would breach the
   600-word cap; Mode A fetches nearest chunks too).
3. English Grammar ch20 ("Sample Question & Guidelines") DROPPED for
   consistency with the EFT sample exclusion and the Class 6 precedent
   (2 chapter rows, 32 question rows, 10 chunks removed; originals backed up
   at `supabase/class7/_work/eg-ch20-drop-backup/`).
4. Science in-text activity boxes transcribed as `boxed_kaj` rows
   (bn +63, en +64; borderless text-subsections excluded by the border rule).

## Grand totals (recomputed from files, not copied from worker reports)

| Measure | Total |
|---|---|
| Chapter rows (44 book rows) | 444 |
| Question rows (44 book rows) | 8,929 |
| Corrected chunks (primary rows only) | 2,619 |
| Corrected chunk words | 1,013,448 |
| Flagged records kept verbatim (see note §4.1) | ≈ 639 |

## Per-subject table (ch = chapters bn/en, q = questions bn/en, c = chunks bn/en)

| Subject | ch | q | c | Words | Flagged |
|---|---|---|---|---|---|
| সপ্তবর্ণা (saptabarna) | 18/18 | 187/187 | 51/0 (mirror) | 16,587 | 33 |
| আনন্দপাঠ (anandopath) | 9/9 | 36/36 | 52/0 (mirror) | 21,226 | 25 |
| ব্যাকরণ (bekoron) | 11/11 | 47/47 | 104/0 (mirror) | 33,634 | 14 |
| English For Today (eft) | 9/9 | 352/352 | 0/51 (en-primary) | 23,873 | 0 |
| English Grammar (english-grammar) | 19/19 | 423/423 | 0/71 (en-primary) | 32,411 | 0 |
| গণিত (math) | 11/11 | 787/799 | 81/99 | 83,016 | 1 |
| তথ্য ও যোগাযোগ প্রযুক্তি (ict) | 5/5 | 77/79 | 42/44 | 41,597 | 28 |
| বাংলাদেশ ও বিশ্বপরিচয় (bgs) | 11/11 | 238/238 | 87/102 | 72,917 | 14 |
| বিজ্ঞান (science) | 14/14 | 293/294 | 146/174 | 102,736 | 223 |
| শারীরিক (physical) | 5/5 | 85/85 | 38/51 | 43,220 | 78 |
| কর্মজীবন (worklife) | 3/3 | 58/57 | 45/52 | 30,663 | 6 |
| কৃষি (agriculture) | 6/6 | 165/165 | 107/133 | 72,593 | 8 |
| গার্হস্থ্য (homescience) | 15/15 | 263/266 | 84/113 | 85,194 | 28 |
| চারু-কারু (arts) | 7/7 | 75/93 | 28/35 | 28,444 | 13 |
| ইসলাম (islam) | 5/5 | 160/158 | 73/88 | 79,107 | 61 |
| হিন্দু (hindu) | 8/8 | 146/149 | 49/60 | 51,421 | 3 |
| খ্রিষ্ট (christian) | 10/10 | 190/190 | 94/109 | 59,701 | 5 |
| বৌদ্ধ (buddhist) | 11/11 | 253/252 | 66/81 | 69,533 | 19 |
| সহজ আরবি (arabic) | 12/12 | 88/88 | 12/0 (mirror) | 3,050 | 12 |
| সংস্কৃত (sanskrit) | 19/19 | 170/170 | 27/0 (mirror) | 11,342 | 6 |
| পালি (pali) | 10/10 | 290/290 | 99/0 (mirror) | 29,861 | 58 |
| সংগীত (music) | 4/4 | 64/64 | 71/0 (mirror) | 21,322 | 4 |

Mirror rule verified: the 9 identical-PDF subjects (saptabarna, anandopath,
bekoron, eft, english-grammar, arabic, sanskrit, pali, music) have exactly
equal question counts per row, byte-identical question text (spot-verified for
all 7 Bangla-content mirrors), and chunks on the primary row only.
Distinct-PDF subjects differ in question counts per row as expected (e.g. Arts
en has 2 extra sets documented in its log).

## Question types (all lowercase canonical, 0 null, 0 ad-hoc)

mcq 1,676 · creative 1,328 · boxed_kaj 1,202 · short 1,020 · problem 851 ·
task 494 · fill_blank 436 · grammar 396 · descriptive 270 · speaking 248 ·
writing 230 · comprehension 128 · matching 118 · exercise 102 · translation 84 ·
practical 80 · vocabulary 56 · listening 48 · paragraph 34 · true_false 32 ·
letter 26 · essay 24 · reading 36 · assignment 10. Total 8,929.
MCQ options are verbatim inside `question_text`; no correct answer key is
stored or guessed (printed keys, where they exist, are log-only).

## Verification pass (all recomputed on the combined outputs)

- Question/chunk/chapter ids: 0 duplicates anywhere.
- Every question and chunk `chapter_id` exists in the chapters files: 0 bad refs.
- Empty `question_text` / `chunk_text`: 0. `word_count` ≤ 0: 0.
- Raw vs corrected chunk counts AND id sets: identical for all 35 primary files.
- Every question and chunk page range lies inside its chapter's printed range.
- Chunk `word_count` vs whitespace-split recount: 0 chunks off by more than 2.
- SQL round-trip: both SQL files were parsed back with a quote-aware parser
  (handles `''` escapes and newlines inside literals — 1,009 question rows
  contain newlines) and every field of all 8,929 + 2,619 rows matches the
  source files exactly. Each SQL file is a single multi-row INSERT with
  `ON CONFLICT (id) DO NOTHING`.
- Combined JSON row count (8,929) equals SQL row count; combined chunks SQL
  row count (2,619) equals corrected-files total.

## §4 — Source problems found (reported, not hidden)

### 4.1 Flagged files use inconsistent shapes
`*-flagged.json` files come in two shapes: plain lists (per-token entries in
some, per-chunk entries in others) and dicts (`flagged_count` /
`total_tokens` / `entries` / `flagged_entries` / `flagged`). The per-subject
flagged counts in the table above therefore count *records as stored*, not a
uniform token count, and the ≈ 639 total mixes those bases. The authoritative
detail lives in each `*-flagged.json` (original text + reason per record;
nothing was guessed). A future cleanup could normalize these files to one
shape, but it was not done here (source files untouched by design).

### 4.2 Chapter files use varying key sets
Chapter JSONs carry `chapter_number` or `number` plus differing extra fields
(`author`, `section`, `unit_label`, `part`, `notes`, …). All carry `id`,
`title`, and printed/pdf start/end pages; the boundaries map normalizes to
`number / title / printed_start_page / pdf_start_page / printed_end_page /
pdf_end_page`. No data was lost.

### 4.3 problem_number: 4,026 rows become NULL in SQL
`problem_number` is non-numeric in 4,026 of 8,929 rows (305 distinct labels:
`কাজ`, `1ক`, `1খ`, `Activity`, `Task`, `দলগত কাজ`, `1a`, `Group Activity`,
…). The DB column is integer, so the SQL uses NULL for these (same rule as
the Class 6 import); the original labels survive in the combined JSON.
If the app needs these labels, it must read them from a future column, not
from this SQL.

### 4.4 Six chapters have 0 questions
Arts ch7 (bn+en — no discrete exercise items extracted; counts 0 in both
rows), English Grammar ch9 (bn+en — rule expositions and example lists only,
documented in the EG log), Sanskrit ch19 (bn+en — `অভিধানিকা` glossary,
documented in the Sanskrit log). All other 438 chapters have ≥ 1 question.

### 4.5 Other known imperfections (kept, not silently fixed)
- EG log honest limit: one joined-word row (`…-ch1-p3-q10`, "Doyouknowthe")
  was left unchanged because its page was outside the rework's verification set.
- Print errors are kept verbatim everywhere (e.g. Science ch9 "৫জন/five
  friends" table with only 2 numbered rows; EN "diuranal mtion").

## Honest limitations (carried into the app, not hidden)

- **Arabic script is NOT in the chunks.** No Arabic OCR data exists, so the 12
  Arabic chunks (3,050 words, one per chapter) hold only Bangla OCR fragments.
  Question rows are unaffected — they were transcribed visually.
- **Music notation is under-captured.** Lyrics are verbatim; notation blocks
  (ch1 তাল tables, ch3 স্বরলিপি, ch4 song notations) survive only as OCR soup
  and were never reconstructed or quoted as notation.
- **Maths notation does not survive OCR.** Equations, stacked fractions, and
  angle symbols (e.g. `∠AOC`) are unreliable in chunk text; the AI must
  re-derive them, never quote from OCR. Same standing limit as Class 6.
- **Bengali conjunct OCR errors** remain in chunk text; flagged tokens are
  kept verbatim with reasons (see §4.1). Image/map/screenshot text is noise;
  running heads leak in.
- **Science box search is heading-scan dependent.** A box whose heading OCR
  completely missed on a non-spot page could still be missed; every observed
  heading word was scanned in both books and one non-candidate page per
  chapter was spot-checked.
- **EFT listening items depend on audio** that text cannot carry; sample
  sections are excluded (EFT printed 108–116; EG ch20 dropped per ruling 3).
- **No stored answers.** Most exercises print no solution; printed answer keys
  are log-only (no `answer_text` column in the DB schema as read).

## Files produced (this folder)

- `class7_questions_combined.json` — all 8,929 question rows, full 10 fields.
- `class7_questions_import.sql` — single INSERT, 6 DB columns only
  (`id, book_id, chapter_id, page_number, problem_number, question_text`),
  `ON CONFLICT (id) DO NOTHING`. 4,026 `problem_number` values are NULL (§4.3).
- `class7_chunks_import.sql` — single INSERT, all 14 `book_chunks` columns,
  corrected files only, `ON CONFLICT (id) DO NOTHING`.
- `class7_chapter_boundaries.json` — 44 book rows, 444 chapters with
  printed/pdf page ranges.
- `CLASS7_FINAL_REPORT.md` — this file.

## Migration note for the parent (not done here)

Insert order: books → chapters → `class7_questions_import.sql` →
`class7_chunks_import.sql`. Books/chapters SQL is NOT part of this package —
the migration runner builds it from the chapters files and the boundaries map
(book titles/subject ids per the Class 6 mapping style; chapter titles need
bn+en pairing where a chapter file carries only its own language's title).
**The 2026-10-29 13:19 partial-migration snapshot is STALE** (EG ch20 dropped,
Science boxes added, Pali/Music completed after it) — never reuse it; any
migration must be built from these current files.
