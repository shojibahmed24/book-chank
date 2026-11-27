# ইসলাম শিক্ষা — SSC Lecture Sheets (chunked)

- **Subject:** ইসলাম শিক্ষা (`islam`), Class 9–10
- **Book ID:** `class9-10-islam-lecture`
- **Total rows:** 9,269 (`questions-islam.json`) — first pass 3,974 + final pass 2,534 + normalization 2,761 (2. MCQ .doc banks, 2026-11-25)
- **By type:** board 2,161 · mcq 5,843 · saq 438 · cq 471 · gyanmulok 304 · lecture-note 52
- **Flagged rows:** 3,924 (`flagged.json` — rows whose `flag_note` is set)
- **Processed / missing / twins / duplicates:** 86 processed · 2 missing (TP05, keys unrecoverable) · 70 doc/docx twins (PDF used) · 14 duplicate-content skips = 172 manifest files
- **No GitHub push** (approval later). Decoded text in `~/workspace/lecture-sheets/decoded/ssc/islam/`.

## Files

| File | Rows | Notes |
|---|---|---|
| `chapter-00-board.json` | 2,161 | Board papers + TP board/school CQ + TP02/TP04 MCQ (see board index) |
| `chapter-01-cq.json` | 73 | ch1 আকাইদ ও নৈতিক জীবন |
| `chapter-01-gyanmulok.json` | 68 | |
| `chapter-01-lecture-note.json` | 10 | NEW UPDATE definitions (final pass) |
| `chapter-01-mcq.json` | 1,106 | answer-only sheets (287) + Chapterwise MCQ Sheet (190) + 2. MCQ .doc bank (629, normalization) |
| `chapter-01-saq.json` | 75 | |
| `chapter-02-cq.json` | 64 | ch2 শরিয়তের উৎস |
| `chapter-02-gyanmulok.json` | 54 | |
| `chapter-02-lecture-note.json` | 12 | NEW UPDATE definitions (final pass) |
| `chapter-02-mcq.json` | 1,035 | answer-only sheets (258) + Chapterwise MCQ Sheet (229) + 2. MCQ .doc bank (548, normalization) |
| `chapter-02-saq.json` | 86 | |
| `chapter-03-cq.json` | 64 | ch3 ইবাদত |
| `chapter-03-gyanmulok.json` | 67 | |
| `chapter-03-lecture-note.json` | 10 | NEW UPDATE definitions (final pass) |
| `chapter-03-mcq.json` | 856 | answer-only sheets (196) + Chapterwise MCQ Sheet (233) + 2. MCQ .doc bank (427, normalization) |
| `chapter-03-saq.json` | 58 | |
| `chapter-04-cq.json` | 87 | ch4 আখলাক |
| `chapter-04-gyanmulok.json` | 64 | |
| `chapter-04-lecture-note.json` | 15 | NEW UPDATE definitions (final pass) |
| `chapter-04-mcq.json` | 1,095 | answer-only sheets (270) + Chapterwise MCQ Sheet (240) + 2. MCQ .doc bank (585, normalization) |
| `chapter-04-saq.json` | 67 | |
| `chapter-05-cq.json` | 60 | ch5 আদর্শ জীবনচরিত |
| `chapter-05-gyanmulok.json` | 51 | |
| `chapter-05-lecture-note.json` | 5 | NEW UPDATE definitions (final pass) |
| `chapter-05-mcq.json` | 1,123 | answer-only sheets (265) + Chapterwise MCQ Sheet (286) + 2. MCQ .doc bank (572, normalization) |
| `chapter-05-saq.json` | 23 | |
| `model-test/` | 880 | first pass 507 + final pass 373 (see below) |
| `flagged.json` | 3,696 | all rows with a `flag_note` (subset view, ids match the chapter files) |
| `questions-islam.json` | 6,508 | combined (board first, then chapters/model-tests) |
| `processed-files.txt` / `missing-files.txt` | 81 / 2 | snapshot accounting (see `disk-snapshot-2026-11-24.txt`) |

### Model-test files added in the final pass

| File | Rows | Notes |
|---|---|---|
| `model-test/model-test-mcq-ch1..5.json` | 30 each | 5. Model Test/MCQ — 30 MCQs each, keys from the printed key table |
| `model-test/chapterwise-cq-model-mcq-ch1..5.json` | 20 each | cq MODEL MCQ section — no printed keys (null + flag) |
| `model-test/final-sub-1.json` | 11 | Final 1.Sub — 11 CQ sets, no printed answers |
| `model-test/final-sub-2.json` | 11 | Final 2.Sub — 11 CQ sets (Q1 is a science/antibiotics topic — flagged) |
| `model-test/final-sub-4.json` | 11 | Final 4.Sub — 11 CQ sets |
| `model-test/final-obj-1.json` | 30 | Final 1.objecitve — 30 MCQs, keys from inline pairs |
| `model-test/final-obj-2.json` | 30 | Final 2.objecitve — 30 MCQs, keys from inline pairs |
| `model-test/final-obj-3.json` | 30 | Final 3.objecitve — 30 MCQs, keys from inline pairs |

## Board index (chapter-00-board.json)

| Source | Rows | MCQ | CQ | Answer keys | CQ solutions |
|---|---|---|---|---|---|
| Islam-2023.pdf (9 boards) | 369 | 270 (30×9) | 99 (11×9) | 270/270 | 99/99 |
| Islam-2024.pdf (9 boards) | 360 | 262 | 98 | 123/262 | 97/98 |
| Islam-2025.pdf (9 boards) | 355 | 256 | 99 | 0/256 | 99/99 |
| 01. SSC Islam TP. [BQ CQ] | 165 | — | 165 | — | — |
| 03. SSC Islam TP. [School CQ] | 176 | — | 176 | — | — |
| 02. SSC Islam TP. [BQ MCQ] — 2020/2019/2018 only | 330 | 330 | — | 0/330 (TP05 has numbers only) | — |
| 04. SSC Islam TP. [School MCQ] — 19 schools | 406 | 406 | — | 0/406 (TP05 has numbers only) | — |

Boards per year: ঢাকা, রাজশাহী, কুমিল্লা, যশোর, চট্টগ্রাম, বরিশাল, সিলেট, দিনাজপুর, ময়মনসিংহ.
TP 01 covers 2023 + 2020 board papers; TP 03 is school papers (no board/year).
TP02 2023 papers (9 boards × 30 = 270) are duplicates of Islam-2023 rows — NOT re-chunked.

## Known gaps (see report-2026-11-24.md)

- 2024 board MCQ: 8 questions missing (scattered Q18/22/23/27/28/30); keys only 123/262 — the key table's second half (Q8–15, Q23–30) is not in the text layer.
- 2025 board MCQ: 14 questions missing (scattered Q13/14/21–30); keys 0/256 — the key letters are not in the PDF text layer at all (numbers only).
- 2024 Cumilla board CQ Q6 missing.
- TP05 (`05. SSC Islam TP MCQ Solution`) is UNRECOVERABLE as a key source — the file has numbers only, no answer letters in the text layer (verified by reading the full file). TP02/TP04 answer_key therefore stays null + flagged. The 3 deferred files from the first pass are resolved: TP02 and TP04 decoded fine from the PDFs (92–97% Bengali) and are chunked; only TP05 remains missing.
- Model-test shortfalls: #SSC-2027 set-2 SAQ 14/15; #SSC-2027 MCQ model-2 24/30; #SSC-2026 MCQ-1/2/6 29/28/29 vs 30.
- Final-pass data-quality finding (FIXED in normalization, 2026-11-25 — see below): the existing Islam-2023 board rows' question_numbers were scrambled vs TP02 (same exam, same questions — e.g. TP02 Dhaka Q1 = existing Q24) and some existing options were misaligned. All 270 rows renumbered/re-optioned to TP02 order; keys kept (verified correct against TP02 content).
- Decode artifacts are kept as-is, never hand-fixed (see report for examples).

## Rebuild notes (VM replacement 2026-11-24 ~21:09 Dhaka wiped /tmp)

The board rows were regenerated after the wipe by `~/workspace/lecture-sheets/work/islam/board_chunk.py`
(colsplit at `~/workspace/lecture-sheets/work/islam/colsplit.py` + `colsplit/Islam-YYYY.{L,R,RO}.txt`).
Non-board rows are the run-2 outputs (verified correct before the wipe).
Final-pass scripts live in `~/workspace/lecture-sheets/work/islam/finalpass/` (never /tmp):
`chunk_finalpass.py` (Stage A MCQ), `stage_b.py` (Stage B CQ/TOPICWISE), `stage_c.py` +
`colsplit3.py` (Stage C 3-column TP02/TP04), `parse_final.py` (Stage F Final Sub/objecitve),
`parse_nu.py` (Stage D NU definitions), `run_all.py` (runner), `merge.py` (Stage E merge).

## Normalization (2026-11-24/25)

Scripts: `~/workspace/lecture-sheets/work/islam/norm/` (`fix_scramble.py`, `manual_trims.py`,
`post_audit.py`, `validate.py`, `twin_convert.py`, `twin_convert_rest.py`, `twin_similarity.py`,
`chunk_2mcq.py`, `apply_2mcq_chunk.py`, `parse_2mcq.py`, `analyze_2mcq.py`, `txt_convert_2mcq.py`).
Pre-normalization backup (combined + flagged): `staging/ssc/islam/_backup_pre_norm/` (md5
`7d6ff8ab064cd5fbd826fd1d26db2cb8` for `questions-islam.json`). No rows deleted; no
placeholders dropped. Validation: `work/islam/norm/validate.py` — ALL PASS.

### 1. 2023 board scramble — FIXED (270 rows, TP02 as reference)
- 6 boards fully scrambled vs TP02 (barishal, chattogram, cumilla, dhaka, dinajpur, sylhet);
  3 already correct (jessore, mymensingh, rajshahi). **180 question_numbers fixed, 0 left uncertain.**
- Options: 138 replaced with TP02 values, 71 kept (same content modulo decode artifacts),
  59 kept (TP02 options defective), 41 confirmed no-change, 2 manual-confirm no-change.
  14 stems trimmed (leaked option text removed). 227 rows changed; flagged 3,696 → 3,904.
- **Keys were NOT permuted.** 10/10 hand-checked questions prove the current key letter points
  at the correct answer in TP02's options, while naive key-permutation would be WRONG in 7/10
  (e.g. Dinajpur 'ইলম' Q7→TP30: current ক=জ্ঞান correct, permuted ঘ=পরিশুদ্ধতা wrong;
  Dhaka প্রধান ওহি লেখক Q6→TP13: current ঘ=যায়েদ ইবনে সাবিত correct, permuted ক=আবু বকর wrong).
  TP02 option order == book option order (70/70 clean pairs). Sole exception: Mymensingh Q8
  key set to null (was খ) — TP02 mis-split that block and the 4th book-title option is missing
  from both sources; never guessed.
- ⚠️ PREMISE TENSION (parent/coordinator to judge): the book's own numbering looks
  self-consistent — decoded `Islam-2023.uni.txt` line 9 shows Dhaka Q1 = the মনীষীগণ question
  (TP02 Dhaka Q8), and line 4887 shows the same question as Q11 in another board. So the
  "scramble" is a question-ORDER difference between two books, both internally consistent
  (the book's উত্তরমালা key table proves it). The task explicitly ordered TP02 as reference,
  so rows were renumbered to TP02 order as instructed and keys kept valid; revert is possible
  from `_backup_pre_norm/`.

### 2. Doc-twin check — DONE (89 pairs, 0 unresolved)
- Method: every skipped .doc/.docx converted via `soffice --headless --convert-to pdf` +
  shared decoder, compared against its PDF twin by clean-Bengali-word containment
  (wrong-pair baseline median 0.212). **84 confirmed duplicates** (incl. TP05 Board .doc:
  word-set identical to the TP05 PDF — both numbers-only, no keys recoverable from either;
  and Islam-2025.docx, verified by direct `word/document.xml` + bijoy2unicode decode,
  cosine 0.891, after soffice conversion timed out twice on the 3.8 MB file).
- **5 twins carried unique content and were CHUNKED** (see §3): `2. MCQ/chapter-1..5.doc`.
  Their PDF twins are answer-only sheets (● letters, no stems); the .docs hold the full
  questions. **2,761 new rows** (`islam-lec-ch01-mcq-478..1106`, `ch02-488..1035`,
  `ch03-430..856`, `ch04-511..1095`, `ch05-552..1123`; `set_id` `ch0N-mcq-doc`).
- The 1,276 old answer-sheet rows were NOT deleted and their keys were NOT changed (their
  key extraction is unreliable — keys agree with the .doc ● keys at chance level, 25% on
  ch1; SequenceMatcher ratio 0.253, no long matching blocks). Each old row's `flag_note`
  gained a SUPERSEDED note pointing at the new bank. Processed 81 → 86; twins 75 → 70.
- Spec tension: chunk-spec.md says a same-chapter .doc is a duplicate ("PDF-ই প্রধান ...
  পড়বে না") — that rule assumed the PDF holds the content. Here the PDF is answer-only
  and the .doc is the only source of the questions, so the parent task's "chunk unique
  content" instruction governed.

### 3. 2. MCQ .doc chunk (the unique-content twin)
- Decode: `soffice --convert-to txt` + bijoy2unicode per tab-segment/token
  (bn_ratio 1.0 on all 5 files). The shared PDF decoder only reaches 55–67% Bengali on
  these files (LibreOffice splits Bijoy text into per-word runs); the txt export preserves
  logical reading order and the ● key marker (PUA `\uf098`, sometimes raw byte `\x98`).
  Two converter traps found: bijoy2unicode CRASHES (IndexError) on already-Bengali input
  and on short `‡`-final tokens at string end (fixed by per-token conversion with a
  trailing-space pad); it also CORRUPTS Bengali passed through it (ফিরদাউস→ফরিদাউস), so
  Bengali tokens are never fed to it.
- Parser: numbered stems, options by ordinal position (printed labels are sometimes
  typo'd — e.g. two 'গ's — so labels are assigned 1st→ক, 2nd→খ, 3rd→গ, 4th→ঘ and the
  typo is recorded, which keeps the ●-key attached to its value). Counts match the PDF
  ● totals exactly (ch1 629, ch2 548, ch3 427 vs 425 ● + 2 keyless, ch4 585, ch5 572).
- Quality: all 2,761 rows have 4 options; 2,759 have keys. 20 rows flagged: 2 with no ●
  in the source (ch3 Q19 `islam-lec-ch03-mcq-448`, Q37 `islam-lec-ch03-mcq-466` —
  `answer_key` null, never guessed), 14 printed-label typos, 4 glued option labels
  repaired by position. 15 true/false statements (ch1 7, ch2 8) excluded — not MCQs.
- Overlap check: only 44/636 ch1 .doc stems match an existing ch1 MCQ stem (≥0.8) — the
  bank is genuinely new content, not a re-chunk of Chapterwise/Model-Test rows.

### 4. য+়/য় trap — DONE, nothing to fix
- All `board_name` values are ASCII slugs; zero occurrences of য+় (U+09AF+U+09BC) in
  `source`/`set_id`/`guide_source`. The 856 য+় hits elsewhere are pre-existing
  decomposed-য় decode artifacts in ordinary text — kept as-is per spec.

### Remaining limits
- 2023 board: TP02-order premise (see tension above) + Mymensingh Q8 key null.
- 2. MCQ old rows (1,276) still carry unreliable keys — flagged SUPERSEDED, kept for audit;
  a future pass may delete them once the .doc bank is accepted as canonical.
- ch3 Q19/Q37 have no key (no ● in either source). Decode artifacts kept as-is.
