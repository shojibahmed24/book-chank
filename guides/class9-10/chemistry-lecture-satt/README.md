# SSC রসায়ন (Chemistry) — Lecture Sheets Chunking

**Subject:** রসায়ন (chemistry) · **Class:** 9-10 · **Source:** SSC Chapter Wise lecture sheets
**Chunked:** 2026-11-24 (decoder v2) · **Normalized:** 2026-11-25 · **Status:** COMPLETE — all 530 manifest files on disk, 0 missing.

## Totals

| | |
|---|---|
| Total rows | **18,126** (16,824 at chunking − 24 truly-empty placeholders + 1,326 doc-twin rows, see Normalization) |
| Files processed | **530 / 530** (272 PDF + 258 .doc/.docx, of which 99 docs contributed rows in normalization) |
| Files missing | **0** |
| Rows flagged | 17,497 (97% — mostly answer-only / image-stem rows, see below) |
| Rows with `question_text` | 5,382 (30%) |
| Rows with `answer_key` | 9,659 (53%, all MCQ) |
| Rows with `options` | 11,408 (dict present; 7,350 have ≥1 non-empty option value, 1,394 have all four) |
| Duplicate rows flagged | 238 (same board/year/number/stem appearing in two compilations; 0 new ones from the doc merge) |

## Rows by type

| type | rows | question_text | answer_key |
|---|---|---|---|
| mcq | 11,784 | 671 | 9,659 |
| cq | 2,731 | 1,155 | — (answers in `guide_solution`) |
| board | 2,802 | 2,747 | 0 (not printed in text) |
| gyanmulok | 438 | 438 | — |
| saq | 348 | 348 | — |
| handnote | 12 | 12 | — |
| lecture-note | 11 | 11 | — |

## Output files (staging/ssc/chemistry/)

- `chapter-<NN>-<type>.json` — 74 files, one per (chapter, type). Chapter 00 = no chapter.
- `model-test/<set>-<type>.json` — 53 files (SSC-2027 sets 1–5, Model Test chapters 1–12).
- `questions-chemistry.json` — all 18,126 rows.
- `flagged.json` — the 17,497 rows carrying a `flag_note`.
- `dropped-placeholders.json` — the 24 truly-empty placeholder rows removed in normalization (logged, not silently deleted).
- `_backup_pre_norm/` — pre-normalization `questions-chemistry.json` (16,824 rows) + `flagged.json` (16,192 rows).
- `_work/` — normalization scripts + doc-twin verification work (`doc-twin/`, `fixed-board-ids.txt`, `validate-final.py`, `doc-merge-report.json` in `doc-twin/`).
- `processed-files.txt` — all 530 manifest files (PDFs parsed + .doc/.docx noted as duplicates).
- `missing-files.txt` — empty (0 missing).
- `report-2026-11-24.md` — full report.
- `_chunker.py`, `run_chunk.py` — parser + driver (re-runnable).

## Board / year index (board rows only, 2,802)

| Year | Boards | Rows/board |
|---|---|---|
| 2021 | ঢাকা, রাজশাহী, যশোর, চট্টগ্রাম, সিলেট, বরিশাল, দিনাজপুর, ময়মনসিংহ | ~29–36 |
| 2022 | same 8 | ~54–60 |
| 2023 | + কুমিল্লা (9 boards) | ~85–91 |
| 2024 | 9 boards | ~85–90 |
| 2025 | 9 boards | ~28–30 |

Board MCQ answers are **not** in the source text (the answer grids are blank / hidden in white font) → `answer_key` null + flag. Board CQ solutions ARE extracted and paired by question number from each board's উত্তরমালা section (`guide_solution`).

## What is thin, and why

Most MCQ rows are **answer-only**: the question stems are images in the source PDFs, so only the option markers/values and the ● (correct-answer) marker survive as text. These rows carry `question_text: null` + flag "answer sheet only; question stem not in source". They are kept (never dropped) — full text needs OCR later.

2-column MCQ papers (SSC-2027, Board, Model Test) have `options: null` + flag: the decoded text merges both columns' option lines on shared lines, so per-question option attribution is unreliable (verified: paired questions swap options, e.g. Q2/Q11 in SSC-2027 set-1). Stems and grid answers are kept. Recoverable later via a column-split re-decode.

## Decode (v2)

All 272 PDFs decoded with the shared v2 tool (`tools/decode-pdf.py`). v2 re-decode of the 189-file corpus: 16 files improved >2pt Bengali lines, **0 regressed**, mean 25.7% → 26.0% (chemistry is formula-heavy, so the gain is small; the big gain was #Hand note/7th +22pt). 1 file fixed that v1 crashed on (SAQ ch-11).

Known decode artifacts are kept as-is (never hand-fixed): see `report-2026-11-24.md` for 5 examples.

## Normalization (2026-11-25)

Pre-normalization backup in `_backup_pre_norm/` (16,824 rows / 16,192 flagged). No push to GitHub (coordinator pushes).

### 1. Math-misfire check — NO damage found, 0 files re-decoded
- Shared decoder `tools/decode-pdf.py` verified to carry the v2.1 high-byte guard: docstring lines 13–19 + `should_convert()` lines 74–86 (`len(inds) >= 2 and any(ord(ch) >= 0x80 ...)`).
- Scanned all 272 decoded `.uni.txt` files: 0 occurrences of the v2 misfire signature (`অ = {ধ,ন,প,ফ}`-style, Bengali single letters comma-listed in braces, `অ =` anywhere). 115 lines contain `{`/`}` — all intact Latin chemistry formulas (`{K+(aq)}`, `{63.5 + 32 + (16 × 9) + (1 × 10)}`, polymer `{−OC−(CH2)4−COHN−(CH2)6−NH−}n`).
- 297 decoded lines pair a brace with Bengali on the same line; brace-content audit found only 5 distinct Bengali contents, all genuine source labels (`{বন্ধন ভাঙতে প্রয়োজনীয় শক্তি}`, `{নতুন বন্ধন গঠনে নিগর্ত শক্তি}`, `{তামা(Cu), রূপা(Ag) ও সোনা(Au)}`) — not conversion damage. 79 combined rows carry brace+Bengali for the same reason. **No re-decode, no re-chunk.**

### 2. Doc-twin check — DONE, 1,326 rows added from 99 docs
- Manifest: 258 .doc/.docx skipped as duplicates. 246 have a same-stem PDF twin in the same directory; the other 12 (`#TYPEWISE/TYPEWISE MCQ PRACTICE & SUGGESTION/অধ্যায়-1..12.doc/.docx`) map to `রসায়ন-MCQ-1..12.pdf` in the same directory (per `run_chunk.py:96`). All 258 twins have decoded `.uni.txt` on disk.
- Conversion: `soffice --headless --convert-to pdf` (isolated LibreOffice profile per worker, resume-aware), mirroring the source tree under `_work/doc-twin/pdf/`; each converted PDF decoded with the shared v2.1 tool into `_work/doc-twin/txt/`. Two workers ran in parallel (dirs 0–18 / 19–31); both first-generation workers died ~2026-11-24 19:09 UTC with no traceback (orphaned soffice finished their in-flight dirs) and were relaunched with plain `nohup`. Scripts: `_work/doc-twin/convert.py`, `convert-b.py`, `retry4.py`; logs `convert.log`, `convert-b.log`, `retry4.log`.
- **Converted 256/258. Two genuine failures, both LibreOffice PDF-export aborts (`Area:Io Class:Abort Code:27` at `sfxbasemodel.cxx:3274/1822`) after 3 attempts each — NOT disk space (57 GB free, 100 MB probe write OK):** `01. Chemistry IX-X ( CQ).docx` (10,496,189 bytes) and `Test paper/15-22.doc` (26,432,256 bytes). Secondary method (`_work/doc-twin/alt-extract.py`, results in `doc-twin-alt.json`, texts in `txt-alt/`): stdlib zipfile reads `word/document.xml`, font-aware Bijoy conversion reusing the shared tool's own functions (`should_convert`, `convertBijoyToUnicode`, `post_fix`) — no hand-rolled decoder, shared tool untouched. For `15-22.doc`, soffice `.doc` → `.docx` conversion succeeded (1.3 MB `alt/15-22.docx`) even though PDF export aborts. `python-docx` not installed; `antiword`/`catdoc`/`pandoc` not found.
- Similarity (`_work/doc-twin/similarity.py`, report `doc-twin-report.json`): word-set Jaccard + doc-word coverage vs twin decoded text. Verdicts over 256 docs: REVIEW 244, `duplicate?` 12, clean `duplicate` 0. Coverage histogram: 0–0.05: 11; 0.05–0.15: 100; 0.15–0.3: 42; 0.3–0.5: 23; 0.5–0.7: 22; 0.7–0.85: 46; 0.85–0.95: 12. **158 docs have twin_words < 300** (PDF twin nearly textless / image-based) — low coverage mostly means the twin is image-based, not that the doc is different material.
- Row-coverage (`_work/doc-twin/row-coverage.json`): each doc's words vs the words ALREADY IN ROWS chunked from its twin PDF. Histogram: <0.1: 129; 0.1–0.3: 46; 0.3–0.5: 29; 0.5–0.7: 21; ≥0.7: 33. Decisive example: `1. CQ Practice Sheet/chapter-1.doc` — 1,445 lines / 48,158 chars of real CQ questions+answers (partly garbled Bijoy, e.g. `cÖkœ -1`); twin PDF produced only 18 CQ rows, all with empty `question_text`; 0/15 doc-line fragments found in twin rows. Same sheet in content terms, text form where the PDF has images.
- Dry-run chunk (`_work/doc-twin/dryrun-chunk.py`, report `doc-chunk-dryrun.json`): re-ran the SAME parsers as `run_chunk.py` (classify via the twin PDF rel, dispatch replicated) on every doc's decoded text — 15,808 doc rows total. 156 docs were same-sheet (shared question numbers, close counts) but with NO text gain (doc rows with `question_text` 1,616 vs twin rows 1,643 over the same set) — the parsers extract answers, not stems, from both sources — so same-sheet docs were left skipped. 40 docs parsed to 0 rows (12 answer-only files, parser-found-nothing on garbled text).
- **Merge (`_work/doc-twin/merge-doc-rows.py`, report `doc-merge-report.json`): added only the rows whose (type, set_id, question_number) has NO counterpart among the twin PDF's rows — 1,326 rows from 99 docs.** By type: mcq 678, board 202, gyanmulok 241, saq 159, cq 46. By kind: practice-gyan 241, practice-mcq 262, newupdate-mcq 212, practice-saq 159, topicwise-mcq 64, typewise-mcq-practice 60, typewise-mcq-que 54, typewise-cq-que 31, modeltest-mcq 26, chapterwise-cq2 12, chapterwise-cq 3, board 202. Spot-verified before merging: board extras are per-board qnums 26–50 for 2021 (twin extract found only 1–25 per board); newupdate-02 extras are contiguous qnums 115–170 after the twin's 1–114; practice-mcq ch-5 extras are 298–357 after the twin's 1–297; model-test "Chapter 3 to 6" extras are 23 real MCQ stems with options. The 2 false-alarm "clashes" on (board, year, qnum) were a check bug (`year` is null on board rows; real key is `board_year`) — both rows are genuinely different years/stems. Board dedupe rule (same board/year/number/stem) flagged **0** new rows as duplicates.
- New-row rules: IDs continue per-group maxima, replicating `run_chunk.py` (`chemistry-lec-ch<NN>-<type>-<NNN>` per (chapter_number or 0, type); `chemistry-lec-mt-<set>-<type>-<NNN>` per (set_id, type)). Every new row carries the provenance flag `chunked from .doc/.docx twin (doc-twin normalization 2026-11-25); PDF twin extract lacks this row`, so all 1,326 are in `flagged.json`. `source_file`/`guide_source` point at the `.doc`/`.docx`. 50 chapter/model-test files updated (e.g. `chapter-01-saq.json` 0 → 14, `chapter-01-gyanmulok.json` 0 → 33 — the dropped placeholders' chapters now have real rows). 0 fully-empty extras (all 1,326 carry question_text, options, answer_key or question_number), so no placeholder was re-introduced. The 2 unconvertible docs: `01 ( CQ).docx` contributed 0 rows (all its parsed rows match the twin); `15-22.doc` contributed 1 board row via the alt method.
- NOT done (follow-up): the same-sheet docs' question STEMS exist in raw doc text but no parser extracts them from either source (both parsers are answer-side); a stem-extraction pass over `_work/doc-twin/txt/` could fill empty `question_text` on existing rows. Doc-decoded text is noisier than PDF-decoded (unconverted Bijoy runs like `cÖkœ -1`, `hv cixÿvMvi`).

### 3. য+় / য় trap — FIXED, 294 rows
- `board_name` was spelled with য+় (U+09AF+U+09BC) instead of য় (U+09DF) on all 294 ময়মনসিংহ board rows (the only board name containing য়). Fixed `board_name` + `set_id` (`ময়মনসিংহ-2024-cq` → `ময়মনসিংহ-2024-cq`) + `source` on those rows in `questions-chemistry.json` and `chapter-00-board.json`; appended `normalization: board_name spelling fixed to correct য় (U+09DF)` to each row's `flag_note`. 291 were already flagged; 3 newly flagged → flagged 16,192 → 16,195 at that step. Root cause fixed in `_chunker.py:1118` + `run_chunk.py:330,382`: `.replace(correct-য়, trap-য+়)` normalized correct → trap; now maps trap → correct (regex still matches both spellings).
- Deliberately NOT changed: `source_file`/`guide_source` (they record the real on-disk filename — `রসায়ন-MCQ-1.pdf` itself is spelled য+় on disk, verified by codepoint); `subject`/`chapter_name`/`question_text`/`guide_solution` (the য+় spelling occurs 38,872× across all text — decoder-wide Bijoy artifact, kept as-is per spec's never-hand-fix rule).

### 4. Empty placeholders — 24 DROPPED (logged)
- 80 rows had `question_text` + `options` + `guide_solution` all empty. 56 were KEPT: 52 board rows carry board/year + question_number + marks_parts, 3 MCQ rows carry grid `answer_key`s, 1 CQ row (`chemistry-lec-ch12-cq-203`) carries full `marks_parts`.
- 24 dropped: one per chapter (1–12) from the image-based SAQ + Gyanmulok practice sheets — no question_number, marks, answer_key or stimulus; their own flag_note says "no rows extracted". Logged in `dropped-placeholders.json`. 0 exact-duplicate rows found (content signature excluding `id`), so nothing deleted as a duplicate.

### Validation (after normalization, final)
- All JSON parses (129 files); combined 18,126 = chapter files 17,289 + model-test files 837; ids unique (18,126), none null; all rows 37 fields; flagged.json ⊆ combined and flagged count 17,497 == rows with non-empty `flag_note`; processed 530 + missing 0 = manifest 530.
- Spot-checked 3 decoded files by reading (re-confirmed after the merge): `#Hand note/1ST.uni.txt` (readable Bengali — "রবাটর্ বয়েল (১৬২৭-১৬৯১)" / Robert Boyle passage), `1. CQ Practice Sheet/chapter-6.uni.txt:445–455` (mole-calculation formula intact), `6. Board Question 23-25/Chemistry-2023.uni.txt:1–12` (ঢাকা বোর্ড-২০২৩ header + Q1 readable).

## Red-marker answers (TYPEWISE MCQ)

The 12 `ch-mcq-ans-N.pdf` files mark answers in **red** (no ●). Red letters were read from the PDFs' font colour (`#ff0000` in `pdftohtml -xml` — colour metadata only, no text re-decoding): 60 per chapter (56 for ch-2). They were paired with the `ch-mcq-que-N` question files **only when counts matched**; 11 of 12 chapters did not match (question file grouped into fewer sets than red markers) → `answer_key` left null + flag, per spec. The red counts are recorded in the run notes (`_run-summary.json`).
