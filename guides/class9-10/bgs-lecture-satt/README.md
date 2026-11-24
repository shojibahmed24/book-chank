# বাংলাদেশ ও বিশ্বপরিচয় (bgs) — SSC Lecture Sheets chunking

- **Subject:** বাংলাদেশ ও বিশ্বপরিচয় (slug `bgs`), class 9–10, SSC Chapter Wise
- **Date:** 2026-11-24 (snapshot 2026-11-24 ~20:00; parse runs 1–8; final pass 2026-11-24 ~21:00 — the 48 missing files, all now on disk)
- **Spec:** `~/workspace/lecture-sheets/chunk-spec.md` (v2, decoder v2)
- **Decoder:** ONLY the shared tool `~/workspace/lecture-sheets/tools/decode-pdf.py` (v2).
  No own decoder, no reArrange, no hand-fixed spelling.
- **Snapshot:** 403 files on disk at snapshot time (209 PDFs + 194 .doc/.docx);
  only snapshot files were chunked. Files arriving later (download still running)
  belong to the final pass — **done 2026-11-24 ~21:00 (see § Final pass below)**.
- **No GitHub push** — staging only, approval later.

## Outputs (this directory)

| File | Content |
|---|---|
| `questions-bgs.json` | **8,872 rows**, all types, **37-field schema** (spec schema; `chapter_name` added by the 2026-11-24 normalization — see § Normalization below) |
| `chapter-<NN>-<type>.json` | Per-chapter files (ch 01–15; ch 04–09 lecture-note added by the final pass) |
| `model-test/<set>-<type>.json` | Model-test / board sets (see below) |
| `flagged.json` | 7,020 rows carrying a `flag_note` (79% — read before use) |
| `_backup_pre_norm/` | Pre-normalization backup of `questions-bgs.json` + `flagged.json` (36-field, taken before any change) |
| `dropped-placeholders.json` | Placeholder-drop log: **0 rows dropped** (51 literal candidates reviewed, all kept — they carry real CQ content) |
| `_answer-keys/chapter-<NN>.json` | Answer-key-only `2. MCQ` files: 1,925 keys, 15 chapters (no rows — pairing unresolved, see report) |
| `unparsed-files.json` | 14 files with 0 rows — all `#NEW LECTURE SHEET/01. BGS PDF` M-C files except M-C-39 (ch 3), which parsed 35 CQ rows |
| `parse-stats.json` | Per-file row counts + duplicate-similarity notes |
| `processed-files.txt` | 237 source files actually worked from (233 PDFs + 4 doc-only) |
| `missing-files.txt` | **0 files** (empty — download complete, final pass done) |
| `duplicate-format-files.txt` | 214 .doc/.docx files skipped — PDF twin already chunked (**but see § Normalization 2: 14 of them are NOT duplicates** — `2. MCQ` question banks, listed in `unique-content-pending.txt`) |
| `unique-content-pending.txt` | The 14 `2. MCQ` .doc/.docx files that carry unique content (full MCQ banks) — needs a dedicated chunking pass, do NOT re-skip |
| `_parse_bgs.py` | The parser (audit; decoding stays with the shared tool only) |
| `report-2026-11-24.md` | Full report: counts, validation, problems |

**Accounting:** 237 processed + 0 missing + 214 format-duplicates = **451 = manifest total** ✓

## Row counts by type

| type | rows |
|---|---|
| mcq | 6,130 |
| cq | 1,742 |
| gyanmulok | 519 |
| saq | 469 |
| lecture-note | 12 |
| **total** | **8,872** |

- MCQ with `answer_key`: 2,585 / 6,130 (42%). The rest: null + flag (never guessed).
- CQ with `guide_solution`: 642 / 1,742. CQ with `marks_parts`: 1,288.
- 670 rows have empty `question_text` (mostly board MCQ rows whose stems are
  unconverted Bijoy gibberish — flagged `stem-empty-or-too-short`).
- Board rows: 3,849 (years 2019–2025; board_name/board_year per section header).

## Final pass (2026-11-24 ~21:00) — the 48 missing files

All 48 files (BGS CHAPTER 4–9 `#NEW LECTURE SHEET` sets) chunked with the
same parser (`_parse_bgs.py`, counters seeded from existing max ids — no id
collisions) and merged into the existing chapter files + combined JSON.
**+772 rows** (MCQ 615, CQ 151, lecture-note 6); **+462 flagged rows**.

| File type (per chapter) | Rows |
|---|---|
| `BGS CHAPTER N MCQ.pdf` | 99 each (594 total); 601/615 with `answer_key` (98%); 279 with full 4 options, 552 with any options — the rest have merged/missing option letters, flagged |
| `BGS CHAPTER N CQ.pdf` | 14–28 each (123 total); 132/151 CQ rows with `guide_solution` |
| `BGS CHAPTER N BOOK SOLUTION.pdf` | 4–21 each (49 total) |
| `BGS CHAPTER N BASIC.pdf` | 1 lecture-note row each (6 total; guides 5.3K–13.8K chars) |

- **BOOK SOLUTION duplication — checked, NOT duplicates:** correct text
  similarity vs the matching `1. CQ/chapter-N.pdf` is 0.04–0.35 (Jaccard
  0.27–0.33) — same content family, different text. No duplicate flags.
- **⚠️ Parser bug found during this check:** `sim()` in `_parse_bgs.py`
  `main()` is broken — `norm_text()` collapses all whitespace (incl. `\n`)
  to spaces, so `.split('\n')[3:]` is always `[]` and the ratio is always
  1.0. The first-pass "similarity 1.00" duplicate claims rest on that
  broken metric — BUT a re-check with the corrected metric confirms the
  conclusions anyway: Model Test 1 vs #SSC-2026 pairs present on disk are
  genuinely 1.000; BGS-2024 vs Board-Q 2024 is 0.910; BGS-2025 vs
  Board-2025-Ans is 0.916. (Some pairs couldn't be re-checked — their
  decoded files aren't on disk.)
- **Ch 8 BOOK SOLUTION quirk:** no `প্রশ্ন-` markers, so the parser fell
  back to the `numdot` split and turned a numbered list into 19 fragment
  "CQ" rows (parts-not-found, no answers) — kept + flagged, not real CQ sets.
- Decode quality of the 24 new PDFs: Bengali-line ratio 0.875–0.994.
- `_answer-keys/` sidecar pairing: not applicable here — the new MCQ files
  carry their own inline ● keys; the 1,925 sidecar keys remain unpaired.
- No file had 0 rows; no file is still missing. **BGS is complete vs the
  manifest (451/451).**

## Model-test / board sets (`model-test/`)

`model-test-1` (121 CQ + 450 MCQ), `ssc-2026` (52 CQ + 180 MCQ — **exact
duplicates of Model Test 1**, similarity 1.00, flagged per row),
`ssc-2027-set-1..5` (80 CQ + 150 MCQ), `model-test-2-chapterwise` (93 CQ),
`model-test-2-final-1/2/3` (15 CQ + 89 MCQ), `school` (129 CQ + 33 MCQ),
`sq-mcq-50` (31 MCQ), `test-paper-creative-44` (33 CQ),
`board-2023` (301 MCQ), `board-2024` (633 MCQ — BGS-2024 + Board-Q 2024,
exact duplicates, similarity 1.00), `board-2025` (294 MCQ),
`board-2025-ans` (346 MCQ — same content as BGS-2025, similarity 1.00, but
decoded far better), `board-2018-2020-2023-2024` (237 CQ + 930 MCQ),
`guide-bq-2018-2023` (113 CQ + 486 MCQ), `global-studies-2024` (141 CQ + 368 MCQ).

## Known limitations (see report for detail)

1. **2-column interleave pairing** — measured 8/10 on CHAPTERWISE MCQ ch1
   semantic anchors (Q3/Q16 swapped; answer keys 14/14). Every 2-col MCQ row
   is flagged `option-stem pairing by candidate rule (unverified)`.
2. **M-C mixed guides** — 14 of 15 files yield no extractable question text
   (decode gives only glyphs + answer fragments). M-C-39 (ch 3) gave 35 CQ
   rows; its MCQ bank (~236 items, mixed MCQ + জ্ঞানমূলক) was skipped —
   needs a dedicated pass.
3. **`2. MCQ` answer keys** (1,925 keys) do NOT match the question files'
   counts — stored as sidecars, never force-paired.
4. **Board PDFs are partly unconverted Bijoy** — many stems/options are
   gibberish (6 files still carry >100 gibberish lines). Rows kept + flagged.
5. **Chapter 3 name** kept as decoded: `সৌরজগৎ ও ভূম-ল` (decode artifact;
   textbook name is ভূমণ্ডল). Never hand-fixed per spec.
6. **CQ marks**: printed trailing marks used when present; otherwise the
   standard ক=1, খ=2, গ=3, ঘ=4 scheme with `marks_source` null.

## Verification (all passed 2026-11-24; re-run after normalization, see below)

- All JSON files parse (`json.load`, 0 failures).
- `questions-bgs.json` (8,872) = sum of chapter + model-test files (107 per-file JSONs).
- All 8,872 ids unique; every row has exactly the 37 spec fields.
- 3 decoded files eyeballed before parsing (CHAPTERWISE MCQ ch1, 1. CQ ch1,
  2. MCQ ch1 answer file) + spot-checks of every file type during parsing.

## Normalization (2026-11-24, after the final pass)

Backup first: pre-normalization `questions-bgs.json` + `flagged.json`
copied to `_backup_pre_norm/` before any change. Scripts in
`~/workspace/lecture-sheets/work/bgs/` (`normalize_chapter_name.py`,
`validate_norm.py`, `twin_check.py`, `batch_convert.py`, `batch_compare.py`).
No GitHub push.

### 1. `chapter_name` fix — the main job

BGS rows were 36-field: `chapter` holds the chapter NAME string,
`chapter_number` the number, and there was NO `chapter_name` field.
`chapter_name` = the value already in `chapter` was added to **every row**
(8,872/8,872); `chapter` itself untouched. All rows are now 37-field
(spec schema). `chapter_name` is `null` on the 4,409 model-test/board rows
whose `chapter` is `null` (`chapter_number` 0) — same as before, no
chapter invented. Chapter names (15, ch 01–15): e.g. ch 1
`পূর্ব বাংলার আন্দোলন ও জাতীয়তাবাদের উত্থান (১৯৪৭-১৯৭০)` (361 rows),
ch 3 `সৌরজগৎ ও ভূম-ল` (399; decode artifact kept as-is, see § Known
limitations 5), ch 15 `বাংলাদেশের সামাজিক পরিবর্তন` (145).

### 2. Doc-twin check — DONE (2026-11-24): 200/214 confirmed duplicates, 14 carry unique content

Every `.doc/.docx` in `duplicate-format-files.txt` was converted
(`soffice --headless --norestore --convert-to pdf`, one call per source
directory, 25 dirs) and decoded with the shared tool only, then compared
by token-set Jaccard + difflib head-ratio against its PDF twin's decoded
`.uni.txt` (duplicate ≥ 0.80, review 0.50–0.80, unique < 0.50). All 214
have a PDF twin on disk.

| Verdict | Files |
|---|---|
| Duplicate (Jaccard ≥ 0.80) | 123 |
| Review band, confirmed duplicate by Bengali word-overlap (≥ 0.6 both ways) + side-by-side reading | 64 |
| "Unique" band (Jaccard < 0.50), confirmed duplicate the same way | 13 |
| **Unique content — NOT duplicates** | **14** |
| **Confirmed duplicates total** | **200 / 214** |

Why so many in the review band: the `.docx`→PDF→decode route renders
the same text noisier than the direct PDF decode (unconverted Bijoy
fragments, KLMN option letters instead of কখগঘ, different column
pagination), which depresses Jaccard and verbatim-phrase matches — e.g.
`#SSC-2026/Chapter Wise/MCQ/chapter-3.docx` (Jaccard 0.507) read
side-by-side is the same model test, same questions in the same order
(Q1 "পৃথিবী থেকে শুক্র গ্রহের দূরত্ব কত?" identical incl. options).
Nothing was chunked from the 200 confirmed duplicates; nothing changed
in the row files for them. Full per-file results:
`work/bgs/twin-check/twin-check-final.json` (+ `twin-check-summary.json`,
decoded doc texts in `twin-check/decoded-docs/`).

**The 14 unique files — all `2. MCQ/chapter-N.doc` (ch 1, 2, 4–15; ch 3
is a true duplicate, Jaccard 0.98): the PDF twin is only the ANSWER
sheet (● + letters, 4–10K chars decoded) while the `.doc` holds the full
MCQ question bank (22–67K chars decoded) — ~1,925 questions, exactly
matching the 1,925 sidecar keys in `_answer-keys/` (e.g. ch 1: 178 keys,
doc bank ~178 questions). The original "PDF is primary, .doc is
duplicate" assumption was wrong for these 14. Listed in
`unique-content-pending.txt`. They were NOT chunked in this pass: a
ch-1 pilot with the existing parser (`parse_mcq_2col`) yields only
92/178 rows, options mis-paired (Q1's option গ = another question's
stem), questions 100–178 missing (numbering restarts across sections —
the doc has ~10 `বহুনিবার্চনি` sections), and 0 inline keys (● markers
not picked up for the KLMN variant). Merging those rows would corrupt
the set. Needs a dedicated, section-aware chunking pass with parser
tuning (and the sidecar keys paired in question order as the spec's
cross-check allows). Decoded doc texts are preserved for that pass.

### 3. য+় / য় trap

Checked every row (all fields) for board names built with য+়
(U+09AF+U+09BC) instead of য় (U+09DF). **Board values are clean: 0 rows**
— `board_name` values (`ঢাকা`, `চট্টগ্রাম`, `রাজশাহী`, `যশোর`,
`ময়মনসিংহ`, `সিলেট`, `বরিশাল`, `দিনাজপুর`, `কুমিল-া`) use the correct
U+09DF where applicable (verified codepoint-by-codepoint; `ময়মনসিংহ`
is U+09AE U+09DF …). No board value changed, nothing flagged.
The trap DOES exist elsewhere, as a decode artifact, and was left as-is
per the spec's no-hand-fix rule: `subject` (`বাংলাদেশ ও বিশ্বপরিচয়` —
final char of পরিচয় is য+়) on all 8,872 rows, `chapter`
(`জাতীয়তাবাদের` etc.) on 1,028 rows, `question_text` on 12
lecture-note rows (chapter titles). `guide_solution` / `stimulus`: 0 rows.
Note: `কুমিল-া` is a separate decode artifact (কুমিল্লা), not the য+় trap.

### 4. Empty placeholders — 0 dropped

51 rows match the literal test (empty `question_text` + null `options` +
null `guide_solution`) — all CQ. **None dropped:** every one carries real
content in `marks_parts` (40/51) and/or `stimulus` (27/51), e.g.
`bgs-lec-mt-ssc-2027-set-3-cq-002` has 4 full CQ parts. A truly empty
placeholder (nothing in question_text, options, guide_solution, stimulus,
marks_parts, explanation) does not exist in BGS (0 rows). Full review in
`dropped-placeholders.json`. Exact-duplicate rows: 0 (checked by full-row
JSON comparison). No `answer_key` was guessed or changed anywhere.

### 5. Normalization validation (all passed — `work/bgs/validate_norm.py`)

- All 130 JSON files under staging parse.
- Combined (8,872) = sum of ALL 107 per-file JSONs (chapter + model-test,
  incl. `board-*.json` sets).
- Ids unique (8,872), none null; all rows exactly 37 fields.
- Processed (237) + missing (0) + dup-format (214) = 451 = manifest ✓.
- `flagged.json` (7,020) == rows with non-empty `flag_note`; flagged
  count unchanged by normalization.
- `chapter_name` == `chapter` on every row; **no other field changed**
  vs the backup (verified field-by-field); no rows lost.
- Spot-checks (decoded files re-read): `1. CQ/chapter-1` (readable Q&A,
  e.g. ৬-দফা answers), `CHAPTERWISE MCQ Sheet/1st Chapter` (2-col
  interleave as documented), `6. Board Question 2023-25/Global Studies`
  (partly unconverted Bijoy as flagged; `ঢাকা বোর্ড ২০২৪` header legible).
  3 sample rows' question heads found verbatim in their decoded sources.
