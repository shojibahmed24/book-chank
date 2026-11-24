# ভূগোল — SSC Lecture Sheets (chunked)

**Subject:** ভূগোল ও পরিবেশ (Geography), class 9–10 · **slug:** `geography`
**Book:** `class9-10-geography-lecture` · **Chunked:** 2026-11-24 · **Normalized + doc-twins chunked:** 2026-11-25 · **Rows:** 5,036

## Outputs

| File | Rows | What it is |
|---|---|---|
| `questions-geography.json` | 5,036 | All rows, sorted by (chapter, type, set_id, question_number, id) |
| `flagged.json` | 3,137 | Every row with a `flag_note` (needs a visual / human check) |
| `chapter-<NN>-<type>.json` | — | 56 files: per-chapter `saq`, `cq`, `mcq`, `lecture-note` |
| `model-test/*.json` | — | 128 files: model tests, board papers per board-year, test papers |
| `processed-files.txt` | 131 | Sources actually chunked (102 PDFs + `Geography.doc` + 28 `.doc` twins, see below) |
| `missing-files.txt` | 72 | `.doc/.docx` files verified as true duplicates of a PDF twin (chunked from the PDF instead); 0 not on disk |
| `report-2026-11-24.md` | — | Full run report (this folder) |
| `_backup_pre_norm/` | — | Pre-normalization `questions-geography.json` + `flagged.json` (3,999 rows) |
| `dropped-placeholders.json` | — | 0 rows dropped — see normalization section |

## Row counts by type

| type | rows | answer_key | options |
|---|---|---|---|
| saq | 655 | — | — |
| mcq | 1,859 | 631 | 1,315 |
| lecture-note | 202 | — | — |
| cq | 456 | — | — |
| board | 1,864 | 590 | 1,157 |
| **total** | **5,036** | **1,221** | **2,472** |

Board rows by year: 2021: 201 · 2022: 253 · 2023: 492 · 2024: 570 · 2025: 348.
`guide_solution` on 1,266 rows · `stimulus` on 1,233 · `diagram_dependent` on 501 ·
73 rows have no `question_text` (flagged, kept per spec).

## Sources (203 manifest files — all accounted for)

- `2. SAQ` ch1–14 → 472 SAQ rows (28–46/chapter).
- `4. Model Test` Chapter Wise CQ ch1–14 (head CQ + tail short-answer, answers filled from the chapter SAQ file) + Chapter Wise MCQ ch1–10 + Final Model Geo-CQ-1/2 + Geo-MCQ-1/2.
- `#SSC-2027` CQ Model-1..5 + MCQ model-1..5.
- `Lecture sheet` 01–14 → শিখনফল + key-point notes (202) + one flagged MCQ section row per sheet (14) + CQ sections C (board/best), E (practice), F (question bank) (108).
- `5. Board Question 23-25` Gegoraphy-2023/2024 + Geography-2025 → 9 boards × (30 MCQ + ~11 CQ) each; 2025 MCQ answer keys are BLANK in print, so `answer_key` is null there (0 set).
- `Test paper` 01 (BQ CQ 21–24, 300 rows) + 02 (BQ MCQ 21–24, 535 rows) → the only source for 2021/2022 board papers; 2023/2024 rows are flagged as duplicates of the board files. TP03 (school CQ, split per paper) + TP04 (school MCQ, option letters lost — `options` null) are in the model-test files; TP05 (answer-key file, blank grids) → 0 rows.
- `1. CQ` ch1–14 `.doc` → **178 new CQ rows** (2026-11-25, see normalization section — the PDF twins are diagram-only, the `.doc` is the real text).
- `3. MCQ` ch1–14 `.doc` → **859 new MCQ rows** (2026-11-25 — the PDF twins are answer-key grids only, the `.doc` is the question paper).
- `Geography.doc` (doc-only, 46 MB) → converted to PDF and decoded (65% Bengali lines, residual raw Bijoy runs) → **77 rows parsed but DROPPED**: it duplicates the 2024 board MCQ already chunked from Gegoraphy-2024.pdf (same ids, partial/unreliable, no CQ rows parsed).

## How it was parsed

- Decoder: shared tool `tools/decode-pdf.py` **v2** (content-based Bijoy detection). 31 files re-decoded with v2 (board files 0.1% → 88–90% Bengali lines).
- Parser: `_work/parse.py` (stream parser with a memoized constraint solver for the 2-column option interleave) + driver `_work/run_all.py`.
- Normalization (2026-11-25): `work/geography/normalize.py` (log: `work/geography/normalization-log.json`); twin chunking: `work/geography/chunk_twins.py` (draft: `work/geography/chunk-twins-draft.json`).
- Validation: all JSON parse; `questions-geography.json` count = sum of bucket files; all ids unique; processed (131) + dup-format (72) + not-on-disk (0) = 203 manifest files.
- MT-MCQ chapter-1 verified against the printed answer key: **26/26 answers match**.

## Normalization — 2026-11-25 (3,999 → 3,999 rows, then +1,037 twin rows → 5,036)

Backup first: pre-normalization combined + flagged copied to `_backup_pre_norm/` before any change.

1. **Model-test type fix (1,339 rows).** `type="model-test"` → real type, `section` kept as `lecture-model-test`: **mcq 986** (576 with options + 410 from MCQ papers whose options were lost in parse — TP04 SQ-MCQ etc., marks=1, file name + id agree), **cq 170** (164 with `marks_parts` + 6 CQ-set fragments whose parts failed to parse), **saq 183** (109 chapter-wise CQ-tail short answers, marks=2, answers from the chapter SAQ file + 74 SSC-2027 CQ-model rows). The 74 SSC-2027 rows are the file's সংক্ষিপ্ত-উত্তর section, verified against the decoded file (8 CQ sets + 15 short-answer questions; the parser had kept only the 15 short answers, labelled `-cq-`); their ids were re-suffixed `-cq-` → `-saq-` and `marks=2` set from the printed header (`প্রতিটির মান—২`, all 5 files). **gyanmulok 0** — no MT row is a one-line knowledge question distinct from SAQ; no Gyanmulok folder exists for this subject. 0 rows left undeterminable. The 8 CQ sets × 5 SSC-2027 models (40 sets) were never chunked — a re-parse gap, see report.
2. **Section fix (324 rows).** `section="lecture-lecture-sheet"` → `lecture-<type>`: lecture-note 202, cq 108, mcq 14. No `lecture-lecture-sheet` section remains.
3. **য+়/য় trap (237 rows).** `board_name` (and the board-derived `set_id`, e.g. `ময়মনসিংহ-2021`) used decomposed য+় (U+09AF+U+09BC) instead of precomposed য় (U+09DF) — NFC does **not** compose them, so the chunker never caught it. Fixed to precomposed য় on all 237 Mymensingh rows (47 of them newly flagged with the fix note; 190 were already flagged). The same decomposed literal was fixed in the chunker (`_work/parse.py` `BOARD_SLUGS` / `BOARD_NAME_FIX`, 2 lines). Decomposed য় remains in free text (question/stimulus/guide, ~3,458 rows) as decoder output, left as-is per the spec's keep-as-is rule.
4. **Deletions: 0.** No verified exact duplicates (0 groups) and no truly-empty placeholders. The 1 literal-def candidate (`geography-lec-ch00-board-cumilla-2023-mcq-017`, empty stem/options/guide) carries a printed `answer_key` (খ, from the key grid) and was kept, flagged. The other 39 literal-def empties are CQ rows whose stem is diagram-only but whose `marks_parts` carry the questions — kept. See `dropped-placeholders.json`.
5. **Doc-twin check (100 files).** Every `.doc/.docx` listed as a skipped duplicate was verified by decoded-text similarity against its PDF twin (`.docx`: text extracted + Bijoy-converted with the shared decoder's logic; `.doc`: `soffice --headless --convert-to pdf` + shared `decode-pdf.py`). Results: **`.docx` 53/53 duplicates** (median containment 0.978; 5 below 0.85 re-checked with fragment-aware matching, 0.84–0.94, same questions — conversion noise, not new content). **`.doc` Lecture-sheet twins are duplicates** (containment 0.986–0.990). **BUT `1. CQ` (14) and `3. MCQ` (14) `.doc` twins are NOT duplicates**: the PDF twins decode to almost nothing (19–53 tokens: diagram labels / answer-key grids), while the `.doc` files hold the full text (655–2,034 tokens). They were chunked (see below) — the only twin group that carried unique content. Test-paper `.doc` twins (5): all duplicates (containment 0.964–0.992) — left skipped.
6. **Twin chunking (+1,037 rows).** `1. CQ` → 178 CQ rows (239 parsed, 61 skipped as duplicates of existing MT/board/lecture-sheet CQ rows — e.g. the মাসুম set already exists as `geography-lec-mt-chapter-wise-ch01-cq-001`); `3. MCQ` → 859 MCQ rows (895 parsed + ch7 recovered 4 → 89 with an extended Latin-marker conversion, 213 dupes skipped overall). Method: `প্রশ্ন- N` (`proshno`) markers incl. unnumbered headers (numbers reconstructed from file order, flagged); CQ answers attached from the K/L/M/N answer blocks by order (139/178 rows; coherence audit mean 0.60, min 0.27 — ch4/ch10/ch14-board answers not attached, flagged); MCQ keys only where the ● marker survived (46 new keys, never guessed); raw-Bijoy titles Bijoy-decoded for question text (56 → 1 garbage-qt row left, a diagram-only set kept flagged). All new rows are `chapter-<NN>-cq/mcq.json`, ids `geography-lec-ch<NN>-cq/mcq-<NNN>`, `set_id` `chapter-<NN>-cq-book/-board` or `chapter-<NN>-mcq-book`. 820/859 new MCQ rows and all 178 new CQ rows are flagged.

## Known problems (see `report-2026-11-24.md` for detail)

1. **2-column interleave** pollutes some stems/options (fragments of the neighbouring column leak in); 3,137 rows flagged.
2. **i/ii/iii options scrambled** in some MCQ (options set to null, answer kept from the key grid).
3. **Lecture-sheet MCQ grid** is unparseable from text — one flagged section row per sheet, needs a visual pass.
4. **Board MCQ shortfalls**: 2023 Barishal 15/30 MCQ, Jessore 18/30, Sylhet 21/30, Chittagong 23/30; 2025 Dinajpur 18/30 MCQ, Barishal 5/11 CQ.
5. **TP02 2021 MCQ** uses Latin-digit markers (`1.`–`30.`) — converted to Bengali and parsed (135 rows, all flagged); 2021 CQ 66 rows.
6. **Decode artefacts kept as-is** (never hand-fixed): চিন্ত্মা, উলিস্নখিত, বিশেস্নষণ, আন্ত্মজাির্তক, সাতÿীরা, দাশির্নক, গুরম্নত্বপূণর্, বোডর্ — a later fix pass handles them together.
7. **Geography.doc** has residual raw Bijoy runs the v2 marker set misses.
8. **73 rows lack `question_text`** (fragment rows, mostly board/CQ with a diagram-only stem) — flagged, kept.
9. **SSC-2027 CQ models: 40 CQ sets missing** (8 per model × 5) — the parser kept only the 15 short-answer rows per file; the CQ sets need a head-only re-parse.
10. **3. MCQ ch7**: Latin-digit markers (extended conversion 1–200 used); 89 rows recovered, questions beyond ~99 not reached by the parser.
11. **Twin-chunked MCQ**: only 46 new `answer_key`s — the ● markers mostly did not survive the 2-column interleave; the PDF twins are answer grids whose ● positions are not recoverable from text.
