# Class 1–10 Book Chunks & Questions

Textbook-grounded data for the **Yes Sir AI** tuition app (and any later
pipeline that needs the same books): **verbatim textbook questions** and
**corrected text chunks**, organised class-wise so they can be reused without
re-running OCR.

বাংলা সংক্ষেপ: এনসিটিবি বই থেকে তোলা হুবহু প্রশ্ন আর সংশোধিত চাংক — ক্লাস
অনুযায়ী সাজানো, যাতে পরে যেকোনো কাজে সরাসরি ব্যবহার করা যায়, আবার OCR
করতে না হয়।

## Current coverage

| Class | Book rows | Questions | Chunk book rows | Chunks |
|-------|-----------|-----------|-----------------|--------|
| 6     | 44        | 5,815     | 35              | 1,556  |
| 7     | 44        | 8,929     | 35              | 2,619  |

Classes 1–5 and 8–10 are **not yet added**. When a new class lands, it follows
the exact same layout (`class<N>/questions.json`, `questions.sql`,
`chunks.json`, `chunks.sql`, plus `chapters.json` where available).

## Layout

```text
class6/
  books.json       # book metadata (id, subject, language, title, file)
  questions.json   # 5,815 verbatim questions (10 fields each)
  questions.sql    # same rows, DB-ready (6 columns, see below)
  chunks-part*.json  # 1,556 corrected chunks, split into parts (see Part files)
  chunks-part*.sql   # same rows, DB-ready (14 columns), split into parts
class7/
  questions-part*.json  # 8,929 verbatim questions, split into parts (see Part files)
  questions.sql    # same rows, DB-ready (6 columns)
  chunks-part*.json  # 2,619 corrected chunks, split into parts (see Part files)
  chunks-part*.sql   # same rows, DB-ready (14 columns), split into parts
  chapters.json    # chapter boundaries: printed + PDF page ranges, 444 chapters
  final-report.md  # per-subject counts, decisions, and limitations
```

## Part files

Files larger than ~4 MB are stored as parts, because the upload path
rejects single files above that size. The content is identical — only split.
Reassemble in filename order:

- **JSON parts** (`questions-part1.json`, `questions-part2.json`,
  `chunks-part1a.json`, `chunks-part1b.json`, `chunks-part2a.json`,
  `chunks-part2b.json`, `chunks-part3.json` where present): each part is a
  valid JSON array holding a slice of the full list. Concatenate the arrays
  in filename order to recover the complete file.
- **SQL parts** (`chunks-part1a.sql`, `chunks-part1b.sql`,
  `chunks-part2.sql`, …): each part is a complete `INSERT` statement
  (header + a subset of rows + `ON CONFLICT DO NOTHING` footer). Run the
  parts in filename order; re-runs are safe.
- Files that were already small enough are stored whole and are not split:
  `books.json`, `chapters.json`, `questions.sql`, `class6/questions.json`,
  `class6/chunks-part2.sql`, `class7/chunks-part3.json`.

## File formats

### Questions (JSON, 10 fields per row)

`book_id`, `chapter_id`, `id` (page-bearing, e.g.
`class7-science-bn-ch3-p42-q2`), `page_number` (**printed** page),
`pdf_page`, `pdf_file` (filename only), `problem_number`,
`question_text` (verbatim), `question_type` (lowercase canonical:
`mcq`, `creative`, `short`, `problem`, `fill_blank`, `boxed_kaj`, …),
`verified_visual` (true only after a rendered page was visually read).

MCQ options are verbatim inside `question_text`. **No answer keys are
stored or guessed** — printed keys live only in extraction logs, never here.

### Chunks (JSON, 14 fields per row)

`id`, `book_id`, `chapter_id`, `language` (`bn`/`en`), `page_start`,
`page_end` (**printed** pages), `pdf_page_start`, `pdf_page_end`,
`chunk_index`, `chunk_text`, `word_count`, `source_pdf` (filename only),
`ocr_engine`, `ocr_confidence_note`.

Class 7 chunks follow the small-chunk spec (target 300–500 words, max 600,
30-word overlap). Class 6 chunks are larger (sentence-boundary, up to 850
words, 50-word overlap) — the Class 7 spec was deliberately **not** backported.

### SQL files (DB-ready)

- Each SQL file is **one** multi-row `INSERT` ending in
  `ON CONFLICT (id) DO NOTHING` — re-runs are safe, existing rows are never
  overwritten.
- Questions SQL uses only the 6 columns the `book_questions` table has
  (`id`, `book_id`, `chapter_id`, `page_number`, `problem_number`,
  `question_text`). `question_type` / `pdf_file` / `verified_visual` stay
  JSON-only.
- Chunks SQL uses all 14 `book_chunks` columns.
- Import order: **books → chapters → questions.sql → chunks.sql**
  (foreign keys point that way).
- Class 7 note: 4,026 questions have a non-numeric `problem_number` label
  (e.g. `কাজ`, `1ক`, `Activity` — 305 kinds), so those become `NULL` in SQL;
  the original label is preserved in the JSON.

## Rules baked into this data

- **Mirror rule.** 9 subjects per class have byte-identical PDFs in the
  Bangla and English folders. Questions are mirrored to both book rows, but
  chunks exist **only** for the primary row (35 chunk book rows, not 44).
  Never double-index the mirror.
- **Printed vs PDF pages.** Printed page = PDF page − 5 for these books
  (verified per book; see `chapters.json` for Class 7). Always cite printed
  pages to students.
- **Verbatim only.** Nothing is invented. A question or chunk that could not
  be verified was flagged or left out, never guessed.

## Honest limitations (do not hide these from users of this data)

- Bengali OCR still leaves conjunct (যুক্তাক্ষর) errors in some chunks, even
  after correction. Flagged tokens are kept verbatim with reasons in the
  extraction logs.
- **Arabic script is not captured** (no Arabic OCR data) — Arabic books hold
  only their Bangla-prose sections.
- **Maths notation does not survive OCR** — equations, stacked fractions and
  angle symbols must be re-derived, never quoted from chunk text.
- **Music notation is raw OCR soup**, never quotable as notation; lyrics are
  verbatim text.
- Image, map and diagram text is noise in chunks; image-stimulus questions
  carry a bracket description (e.g. `[চিত্র: …]`) instead of the image.
- Class 7 chapters with 0 questions (Arts ch7, English Grammar ch9,
  Sanskrit ch19) have no discrete exercise items — see the final report.

## Source & provenance

- Source: official NCTB textbooks, 2026 school year (nctb.gov.bd).
  Class 6: 22 Bangla + 22 English PDFs. Class 7: 22 + 22 PDFs (row 23,
  the minority-language book, excluded pending a decision).
- Pipeline: official PDF → page rendering → Tesseract OCR → sentence-boundary
  chunking → Bengali conjunct correction → visual verification →
  count verification. No third-party dataset was used as a base.
- Textbooks are © NCTB. This repository holds the extraction built for the
  Yes Sir AI project; reuse it for that project, and take your own decision
  before redistributing verbatim textbook content elsewhere.

## Version

Generated 2026-10-29. Class 7 = final-copy package (post parent rulings:
English Grammar Sample Question ch20 excluded; Science in-text activity boxes
included as `boxed_kaj`). Class 6 = post flagged-pass corrected chunks.
