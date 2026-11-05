# Class 9 Math imports — DRY-RUN report (ch16 redo, ch17 redo, ch0 model tests)

> **PREPARED ONLY — NO database contact was made during preparation, no
> password was asked, used, or embedded anywhere.** The parent executes
> `import_math_16_17_0.py` (dry-run by default; `--live` with
> `SUPABASE_DB_PASSWORD` from the environment) and verifies with
> `VERIFICATION_CHECKLIST.md`. Live baselines below are the parent's
> Edge-verified figures (2026-11-01 ~14:57), reused here without a DB read.

## 0. Live baselines used (parent-verified, not re-read here)

| Scope | Rows |
|---|---|
| `guide_questions` grand total | 9,027 |
| Class-9 math chapters: ch2 / ch3 / ch7 / ch8 / ch9 / ch11 / ch16 / ch17 | 889 / 1,430 / 479 / 969 / 799 / 460 / **532** / **367** |
| Class-9 math chapters subtotal | 5,925 |
| Old model-test set `model-test` | 238 (keyed 0) |
| Class-7 math (untouched by this import) | 2,864 |
| Reconciliation: 5,925 + 238 + 2,864 | **9,027 ✓** |

Chapters 2/3/7/8/9/11 and class 7 are **never touched** by these scripts.

## 1. Mapping (2026-11-01 ch3/7/8/9/11 pattern, parent log 2026-11-01)

- Book `class9-math-bn-guide`; `chapter_id` NULL always; guide-native
  `chapter_number` (16 / 17 / 0).
- `section` = file section verbatim (chapters); ch0 `testNN_mcq` →
  `mcq_bank`, `testNN_short` → `short`, `testNN_creative` → `creative`.
- `question_type`: `mcq_bank`→`mcq`, `short`→`short`,
  `creative`→`creative`, `practice_work`→`task`,
  `textbook_exercise`→`mcq` if kind is `mcq`, else `problem`.
- `options` + `answer_key`: MCQ-kind rows only (jsonb object keyed
  ক/খ/গ/ঘ, verbatim). All other rows: both NULL. Verified: no
  non-MCQ-kind row carries an answer_key in these files, so the
  nulling rule changes 0 rows.
- `guide_solution` = file `solution_text` verbatim (NULL when absent).
- `marks` = file `marks` verbatim (mcq 1, short 2, everything else
  NULL). Creative part marks live in `marks_parts` jsonb verbatim
  ({ক:2, খ:4, গ:4, মোট:10}) and are NOT copied into `marks`
  (pilot-17 convention: `marks_parts` is authoritative).
- `flag_note` = file `flagged` text + (` | ` + file `flag_note` when
  present); NULL when neither exists.
- `guide_error` = **false for every KEPT row in this batch**;
  `corrected_answer_key` / `correction_note` = NULL throughout.
  DROP RULE (user decision 2026-11-01 ~15:12): rows whose printed
  content is WRONG are dropped from the import entirely — neither
  `guide_error=true` nor `false` for them, they simply never enter
  the DB. The script classifies every unit (flagged + flag_note,
  case-insensitive) and asserts the exact per-class drop counts;
  ambiguous rows are kept + listed, never guessed. Full rule +
  audit in the script docstring. Pointer-only rows are NOT wrong
  (solution merely not printed) and are kept; the keyless MCQ
  `pilot16-textbook_exercise-046` is MISSING-key, not wrong-key,
  and is kept with NULL key + flag_note.
- `stimulus_id` = file `stimulus_id` or `group_id`;
  `stimulus_text`, `note`, `diagram_note`, `has_diagram`,
  `verified_visual`, `source_pdf_page`, `source_printed_page`
  (printed may be NULL — ch0 folio-less title page, PDF 922),
  `board_name`/`board_year` (from file `board` dict) — all verbatim.
- `lesson` verbatim (`16.1`–`16.4` / `17` / `0`).
- `guide_source`: display-only string, **never read by any Edge
  function or app query** (verified: zero references in
  `supabase/functions` + `lib`). Format used:
  `Talimit গাইড, মুদ্রিত পৃষ্ঠা {printed}` (or `Talimit গাইড, PDF
  পৃষ্ঠা {pdf} (মুদ্রিত ফলিও নেই)` when printed is NULL). The
  deleted 11-01 script's exact format string could NOT be recovered;
  the parent may adjust this ONE format string before execution —
  it affects display only, never filtering.
- File-only fields NEVER inserted (no such DB columns):
  `question_number`, `topic`, `worker_id`. `linked_prose_chunk_id`
  + `created_at` omitted from INSERT (NULL / default now()).

## 2. Item A — ch16 redo (পরিমিতি)

- Source: `_work/pilot-16/transcribed_units.json` — **1,067 units**,
  ids unique, `verified_visual` 1,067/1,067, 0 empty texts.
- By section: practice_work 5, textbook_exercise 69, mcq_bank 451,
  short 170, creative 372.
- By question_type: mcq 458 (451 + 7 textbook-mcq), short 170,
  creative 372, task 5, problem 62.
- Flag classes (from `flagged_list.md`): A (unclear) 3, B (no printed
  explanation) 77, C (no printed answer/solution) 54, Contradictions
  / print quirks (with solution) 24, S2S note-only 9 (+1 S2S overlap
  counted under B) → **DB `flag_note` on 143 KEPT rows** (167 flagged
  − 24 dropped).
- Solution-null: **126 rows** (was 131; 5 dropped rows were
  solution-null).
- Keyless MCQ (by print, kept with options + NULL key + flag_note):
  **1 row** — `pilot16-textbook_exercise-046` (16.4 Q06; the guide
  itself prints '[বি: দ্র: সঠিক তথ্য নেই]', no margin circle).
  Pool-eligible MCQ added: **446** (457 − 11 dropped keyed MCQs).
- **DROPPED: 24 rows** (error class, user decision 2026-11-01
  ~15:12 — they never enter the DB):

| Drop class | Rows |
|---|---|
| contradiction | 12 |
| value-mismatch | 2 |
| print-inconsistency | 2 |
| wrong-pointer | 1 |
| scan-cut | 3 |
| misprint | 4 |

- **Ambiguous KEPT + listed (not dropped, not guessed): 3 rows** —
  `pilot16-creative-075`, `pilot16-creative-081` (note-scope
  mismatch: comment says only area computed, solution also computes
  a diagonal; no math value disputed) and `pilot16-mcq_bank-343`
  (unit typo in a key option: number correct, unit wrong).
- **DELETE: 532 rows** (book + chapter 16 + `set_id IS NULL`).
  Script ABORTS before any delete unless the pre-delete count is
  exactly 532. **INSERT: 1,043 rows** (1,067 − 24).
  **Post: ch16 = 1,043.** By section: practice_work 5,
  textbook_exercise 68, mcq_bank 440, short 168, creative 362.

## 3. Item B — ch17 redo (পরিসংখ্যান)

- Source: `_work/pilot-17/transcribed_units.json` — **713 units**,
  ids unique, `verified_visual` 713/713, 0 empty texts.
- By section: practice_work 9, textbook_exercise 23, mcq_bank 240,
  short 111, creative 330.
- By question_type: mcq 249 (240 + 9 textbook-mcq), short 111,
  creative 330, task 9, problem 14.
- Flag classes: A 11, B 57, C 18, Contradictions/structural 11,
  S2S note-only 6 → **DB `flag_note` on 94 KEPT rows** (103 flagged
  − 9 dropped).
- Solution-null: **75 rows** (unchanged — all 9 dropped rows carried
  solution text).
- Keyless MCQ: **0**. Pool-eligible MCQ added: **245** (249 − 4
  dropped keyed MCQs).
- **DROPPED: 9 rows** (error class, user decision 2026-11-01
  ~15:12 — they never enter the DB):

| Drop class | Rows |
|---|---|
| misprint | 3 |
| duplicate-option | 1 |
| contradiction | 3 |
| missing-question | 1 |
| print-inconsistency | 1 |

  Note: the 3 misprint drops carry 'উত্তর অপ্রভাবিত' (answer
  certified unaffected) in their flags — they are dropped under
  the strict rule because the printed solution text itself is
  wrong, even though the answer is right. The 4 board-tag rows
  (157/158/187/188) and the 2 marks-banner rows (076/078) are
  KEPT: their 'মেলে না' is about metadata (abbreviation matching /
  parts-sum vs banner total), not about the row's own
  question/answer.
- **Ambiguous kept: none.**
- **DELETE: 367 rows** (book + chapter 17 + `set_id IS NULL`).
  Script ABORTS before any delete unless the pre-delete count is
  exactly 367. **INSERT: 704 rows** (713 − 9).
  **Post: ch17 = 704.** By section: practice_work 9,
  textbook_exercise 23, mcq_bank 236, short 110, creative 326.

## 4. Item C — ch0 model tests (10 tests, full-book SSC-style)

- Source: `_work/pilot-0/units/transcribed_units.json` — **690 units**
  (ids unique, `verified_visual` 690/690, 0 empty texts).
- Per test: MCQ 30 (all keyed) + short 15 + creative parts 24 = 69.
- **DELETE: 0.** Only new `set_id`s are added.
- **Hold-out (stays OUT, exact id): `pilot0-test04_short-004`**
  (Test 04 short 4; fraction exponents illegible; re-verify target
  printed p205 Q8). It is present in the source file and asserted
  absent from the insert set.
- **INSERT: 668 rows** (690 − 1 hold-out − 21 dropped) — sets:

| set_id | rows | keyed (MCQ) |
|---|---|---|
| model-test-01 | 67 | 29 |
| model-test-02 | 66 | 27 |
| model-test-03 | 68 | 29 |
| model-test-04 | **66** (hold-out + 2 drops) | 29 |
| model-test-05 | 68 | 29 |
| model-test-06 | 67 | 29 |
| model-test-07 | 66 | 28 |
| model-test-08 | 66 | 28 |
| model-test-09 | 67 | 28 |
| model-test-10 | 67 | 28 |
| **Total** | **668** | **284** |

- By section: mcq_bank 284, short 148, creative 236. By
  question_type: mcq 284, short 148, creative 236.
- Pointer-only: **384 inserted** (389 − 5 dropped short/creative
  pointer rows) — `guide_solution` NULL + the printed pointer in
  `note` verbatim, nothing invented. (All 668 inserted rows are
  solution-null: ch0 prints no worked solutions at all.)
- **DROPPED: 21 rows** (error class, user decision 2026-11-01
  ~15:12 — they never enter the DB):

| Drop class | Rows |
|---|---|
| key-tension | 14 |
| misprint | 3 |
| underdetermined | 3 |
| count-mismatch | 1 |

  Key-tension ids (14): test01_mcq-002, test02_mcq-024,
  test02_mcq-027, test02_mcq-028, test03_mcq-029, test04_mcq-015,
  test06_mcq-015, test07_mcq-013, test07_mcq-030, test08_mcq-007,
  test08_mcq-030, test09_mcq-030, test10_mcq-003, test10_mcq-020.
  (The old dry-run's "15 key tensions" counted test05_mcq-010
  among them; it is underdetermined, not a tension — see below.)
  Misprint ids (3): test01_creative-002, test07_creative-006,
  test09_mcq-027. Underdetermined ids (3): test04_creative-013,
  test05_mcq-010, test08_creative-013. Count-mismatch id (1):
  test06_short-014.
- **Ambiguous kept: none.**
- Flagged inserted: **384** (405 − 21 drops); unflagged: 284 (all MCQ).
- Quiz-pool addition: **0** (set rows are never pool rows).
- **Old set `model-test` (238 rows) is KEPT, untouched.**
  The script checks its count (238) before every item and after the
  run. Follow-up cleanup option for the user (separate order, NOT
  done here): once the new sets are verified in the app, the old
  238 rows may be deleted — they are the pre-redo model-test data
  and will otherwise show alongside the new sets.

## 5. Expected post-import totals

| Scope | Before | Change | After |
|---|---|---|---|
| ch16 | 532 | −532 +1,043 | 1,043 |
| ch17 | 367 | −367 +704 | 704 |
| ch0 sets (new) | 0 | +668 | 668 |
| Old set `model-test` | 238 | 0 | 238 |
| Other class-9 chapters (2/3/7/8/9/11) | 5,026 | 0 | 5,026 |
| Class-9 chapters subtotal | 5,925 | +848 | 6,773 |
| Class-9 sets subtotal | 238 | +668 | 906 |
| Class-9 math total | 6,163 | +1,516 | 7,679 |
| Class-7 (untouched) | 2,864 | 0 | 2,864 |
| **Grand total** | **9,027** | **−899 +2,415** | **10,543** |

The script asserts the arithmetic identity
(post = pre − deletes + inserts) at runtime; it does NOT hard-assert
9,027, because other approved work (e.g. the English import) may
land first. Expected 10,543 holds on the 9,027 baseline.

## 6. Confirm at execution (parent decisions, NOT preparation blockers)

1. `guide_source` format string (§1) — display-only; adjust if wanted.
2. `marks` column = file marks verbatim; creative part marks live
   ONLY in `marks_parts` (not copied to `marks`). If the parent
   wants creative part marks (2/4/4) in the `marks` column instead,
   it is a one-line change before `--live`.
3. Wrong rows are DROPPED (user decision 2026-11-01 ~15:12), not
   flagged: 54 rows total (ch16 24, ch17 9, ch0 21) never enter the
   DB. Kept rows all carry `guide_error=false`. The 3 ambiguous
   ch16 rows (creative-075, creative-081, mcq_bank-343) are kept +
   listed in §2 — if the parent wants any of them dropped instead,
   it is a one-line change to the script's EXPECTED_AMBIG/EXPECTED_DROPS
   before `--live`.
4. Old `model-test` set kept (locked). Deleting it later needs a
   separate order (see §4).

## 7. What was verified without DB contact / what was not

Verified from files only: source counts (1,067 / 713 / 690), id
uniqueness, section + question_type breakdowns, hold-out presence +
exclusion, drop classification (54 rows across 13 classes, asserted
per class per item), ambiguous-kept list (3 ch16 rows), per-set
post-drop counts (668), MCQ full-option sets (451/240/300 +
7/9 textbook-mcq), keyless-MCQ single case (kept), flag/note/
solution-null counts, `guide_source` non-use by Edge/app.
NOT verified here (parent verifies at execution): live pre-counts
(532/367/238) — the script re-checks them with abort gates before
any write; live post-counts and Mode G behaviour — see
`VERIFICATION_CHECKLIST.md`.

## 8. Execution

```bash
cd ~/workspace/yes-sir-ai-guides/class9-10/talimit/math/_work/import-2026-11-01
python3 import_math_16_17_0.py                 # dry-run (re-run after drop adjustment, PASS, exit 0)
SUPABASE_DB_PASSWORD=... python3 import_math_16_17_0.py --live
```

One transaction per item, in order ch16 → ch17 → ch0. Any item
failure rolls back that item and STOPS the run (later items are not
attempted). Rerun is safe: an already-imported item is detected and
skipped without changes. No Edge deploy, no zip, no git commands.
Source JSON files are never modified.
