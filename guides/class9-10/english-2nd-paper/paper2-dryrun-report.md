# English Paper-II — Collection Complete + Import Dry-Run Report

Prepared 2026-11-02. Collection only: no database writes, no deploy, no
zip were made by this task. The live import is run by the parent with
`paper2_import.py` (password from environment only).

Source: `english-1st.pdf` (736 pp). Paper-II = Special Model Tests
58–117 (60 tests). Questions pp. 621–700, answer keys pp. 701–736
(printed page = PDF page). Every row was verified at 500 dpi (render,
view image, read; image wins over text layer; OCR/text layer alone
never trusted). This report contains structure and counts only — no
question, answer, solution, or passage texts.

## Deliverables (all under `.../talimit/english/_work/paper2/`)

- `paper2_rows.json` — 3,508 merged usable test rows (one per item).
- `paper2_held.json` — 32 held rows (not imported as usable rows).
- `tests/paper2-58.json` … `tests/paper2-117.json` — per-test files.
- `merge_paper2.py` — merge + normalization script (re-runnable).
- `MERGE_STATS.json` — merge counts (ids + counts only).
- `paper2_import.py` — guarded import script (Paper-I pattern).
- `paper2_dryrun_audit.json` — dry-run audit (ids + counts only).
- `PAPER2_DRY_RUN_REPORT.md` — this file.

## Totals vs expected 3,540

| | Count |
|---|---|
| Template items (60 tests × 59) | 3,540 |
| Usable test rows collected | 3,508 |
| Held rows (not usable) | 32 |
| Rows + held | 3,540 ✓ |
| Marks, usable rows | 5,608 |
| Marks, held rows | 392 |
| Marks total | 6,000 (60 × 100) ✓ |
| Bank rows (158 Paper-I-held writing rows, set_id NULL) | 158 |
| **Import set (test rows + bank rows)** | **3,666** |
| Keyed rows (answer_key present) | 3,358 |
| Multi-answer rows (variants verbatim, scoring deferred) | 134 |
| guide_error = true | 6 |

Dry-run result: `python3 paper2_import.py --dry-run` → all guards
green, exit 0, no DB touched.

## Per-section counts (test rows / bank rows / import total)

| Section | Test | Bank | Import |
|---|---|---|---|
| gapbox | 600 | 0 | 600 |
| table | 300 | 0 | 300 |
| verbs | 599 | 0 | 599 |
| transform | 599 | 0 | 599 |
| tag | 300 | 0 | 300 |
| suffix | 233 | 0 | 233 |
| prefix | 67 | 0 | 67 |
| preposition | 300 | 0 | 300 |
| connector | 300 | 0 | 300 |
| punctuation | 60 | 0 | 60 |
| writing-paragraph | 48 | 41 | 89 |
| writing-email | 19 | 18 | 37 |
| writing-letter | 20 | 59 | 79 |
| writing-application | 12 | 0 | 12 |
| writing-composition | 51 | 40 | 91 |

Shortfalls vs the 60-test template are exactly the held rows: verbs
−1 (t113 Q3j, key omitted), transform −1 (t60 Q4h, key unmatched),
writing-paragraph −12 (of 60 Q10 slots), writing-composition −9 (of
60 Q12 slots), and Q11 −9 (of 60 Q11 slots: 7 application + 2 email
held; all 20 letter slots linked). Q11 subtypes per test: email 21
slots, letter 20, application 19 (subtype varies per test; see the
per-test table).

## Per-test completion (rows / held / usable-row marks / Q11 / linked Q10–12 / multi)

| Test | Rows | Held | Marks | Q11 | Linked | Multi |
|---|---|---|---|---|---|---|
| 58 | 59 | 0 | 100 | email | 3 | 2 |
| 59 | 59 | 0 | 100 | letter | 3 | 3 |
| 60 | 58 | 1 | 99 | application | 3 | 1 |
| 61 | 59 | 0 | 100 | email | 3 | 1 |
| 62 | 59 | 0 | 100 | letter | 3 | 2 |
| 63 | 59 | 0 | 100 | application | 3 | 0 |
| 64 | 59 | 0 | 100 | email | 3 | 3 |
| 65 | 59 | 0 | 100 | letter | 3 | 1 |
| 66 | 59 | 0 | 100 | application | 3 | 1 |
| 67 | 59 | 0 | 100 | email | 3 | 4 |
| 68 | 59 | 0 | 100 | letter | 3 | 1 |
| 69 | 59 | 0 | 100 | application | 3 | 2 |
| 70 | 59 | 0 | 100 | email | 3 | 2 |
| 71 | 59 | 0 | 100 | letter | 3 | 2 |
| 72 | 58 | 1 | 90 | — (held) | 2 | 10 |
| 73 | 59 | 0 | 100 | email | 3 | 5 |
| 74 | 59 | 0 | 100 | letter | 3 | 1 |
| 75 | 59 | 0 | 100 | application | 3 | 2 |
| 76 | 59 | 0 | 100 | email | 3 | 3 |
| 77 | 59 | 0 | 100 | letter | 3 | 5 |
| 78 | 59 | 0 | 100 | application | 3 | 3 |
| 79 | 59 | 0 | 100 | email | 3 | 1 |
| 80 | 59 | 0 | 100 | letter | 3 | 0 |
| 81 | 58 | 1 | 90 | application | 2 | 2 |
| 82 | 59 | 0 | 100 | email | 3 | 3 |
| 83 | 59 | 0 | 100 | letter | 3 | 0 |
| 84 | 59 | 0 | 100 | application | 3 | 3 |
| 85 | 59 | 0 | 100 | email | 3 | 4 |
| 86 | 59 | 0 | 100 | letter | 3 | 4 |
| 87 | 59 | 0 | 100 | application | 3 | 0 |
| 88 | 59 | 0 | 100 | email | 3 | 3 |
| 89 | 59 | 0 | 100 | letter | 3 | 5 |
| 90 | 59 | 0 | 100 | application | 3 | 5 |
| 91 | 59 | 0 | 100 | email | 3 | 6 |
| 92 | 59 | 0 | 100 | letter | 3 | 6 |
| 93 | 57 | 2 | 70 | — (held) | 1 | 3 |
| 94 | 58 | 1 | 90 | email | 2 | 2 |
| 95 | 59 | 0 | 100 | letter | 3 | 2 |
| 96 | 58 | 1 | 90 | — (held) | 2 | 0 |
| 97 | 58 | 1 | 90 | email | 2 | 1 |
| 98 | 57 | 2 | 70 | letter | 1 | 1 |
| 99 | 57 | 2 | 80 | — (held) | 1 | 1 |
| 100 | 59 | 0 | 100 | email | 3 | 0 |
| 101 | 59 | 0 | 100 | letter | 3 | 1 |
| 102 | 59 | 0 | 100 | application | 3 | 2 |
| 103 | 58 | 1 | 90 | — (held) | 2 | 2 |
| 104 | 59 | 0 | 100 | letter | 3 | 0 |
| 105 | 57 | 2 | 70 | — (held) | 1 | 1 |
| 106 | 58 | 1 | 90 | email | 2 | 1 |
| 107 | 57 | 2 | 70 | letter | 1 | 3 |
| 108 | 58 | 1 | 90 | — (held) | 2 | 1 |
| 109 | 58 | 1 | 90 | email | 2 | 0 |
| 110 | 57 | 2 | 70 | letter | 1 | 2 |
| 111 | 59 | 0 | 100 | application | 3 | 0 |
| 112 | 57 | 2 | 70 | email | 1 | 5 |
| 113 | 56 | 3 | 69 | letter | 1 | 2 |
| 114 | 58 | 1 | 90 | — (held) | 2 | 1 |
| 115 | 59 | 0 | 100 | email | 3 | 2 |
| 116 | 58 | 1 | 80 | letter | 2 | 2 |
| 117 | 56 | 3 | 60 | — (held) | 0 | 3 |

Every test's header sequence was verified (58→117, no missing or
duplicated headers); test 108 starts at the foot of p687, confirming
the 107 boundary. Tests 95/96/97 start at the foot of the previous
test's last page, so question-page ranges overlap by design.

## Held rows (32) — ids + reason class only

Model-not-located (30; answer_text NULL, never invented):

- `eng2-p640-writing-application-q11-t72`
- `eng2-p651-writing-paragraph-q10-t81`
- `eng2-p667-writing-application-q11-t93`
- `eng2-p667-writing-composition-q12-t93`
- `eng2-p669-writing-paragraph-q10-t94`
- `eng2-p672-writing-application-q11-t96`
- `eng2-p673-writing-paragraph-q10-t97`
- `eng2-p674-writing-paragraph-q10-t98`
- `eng2-p674-writing-composition-q12-t98`
- `eng2-p676-writing-paragraph-q10-t99`
- `eng2-p676-writing-application-q11-t99`
- `eng2-p682-writing-email-q11-t103`
- `eng2-p684-writing-application-q11-t105`
- `eng2-p684-writing-composition-q12-t105`
- `eng2-p686-writing-paragraph-q10-t106` (test offers two paragraph
  topics; neither located — single row held, not split, not guessed)
- `eng2-p687-writing-paragraph-q10-t107`
- `eng2-p687-writing-composition-q12-t107`
- `eng2-p688-writing-application-q11-t108`
- `eng2-p690-writing-paragraph-q10-t109`
- `eng2-p691-writing-paragraph-q10-t110`
- `eng2-p691-writing-composition-q12-t110`
- `eng2-p695-writing-paragraph-q10-t112`
- `eng2-p695-writing-composition-q12-t112`
- `eng2-p694-writing-paragraph-q10-t113`
- `eng2-p694-writing-composition-q12-t113`
- `eng2-p696-writing-email-q11-t114`
- `eng2-p699-writing-composition-q12-t116`
- `eng2-p700-writing-paragraph-q10-t117`
- `eng2-p700-writing-application-q11-t117`
- `eng2-p700-writing-composition-q12-t117`

Key problems (2):

- `eng2-p624-transform-q4h-t60` — key-block labels shifted vs items;
  one entry content-matches a different item (carried there, flagged),
  one entry matches no item, so Q4h has no key.
- `eng2-p695-verbs-q3j-t113` — printed key ends at "(j)" with no word
  (zoom-verified at 500 dpi).

Held rows are NOT imported. No row was guessed to fill a gap; every
shortfall is reported, never forced to 59/100.

## The 158 Paper-I-held writing rows — placement (no duplication)

- All 158 are imported as BANK rows (`set_id` NULL) in the new
  Paper-II subject: paragraph 41, email 18, letter 59, composition 40.
  Identification rule (same proven rule as Paper-I): writing sections
  with 481 ≤ source_pdf_page ≤ 570; pdf-page set == printed-page set.
- Test Q10–12 linkage: 150 test writing rows carry a model link
  (`model_source`) to a bank row id; every referenced id resolves to
  the bank set (0 dangling refs). 85 distinct bank models are
  referenced; the other 73 bank rows are practice-only (imported as
  bank rows, not referenced by any test row).
- No duplication: bank rows keep their `eng1-` ids, test rows their
  `eng2-` ids; the two id sets are disjoint (guard-enforced).
- One prior correction carried: one test-61 Q11 link was corrected to
  the printed page form (the held transcription differed from the
  printed page); the held source row was left untouched.

## Deferred multi-key scoring note (NOT decided here)

134 rows have `multi_answer=true` with every key variant recorded
verbatim (slash variants and `Or,` variants). Whether every variant
counts correct in automatic scoring is DEFERRED to the scoring step by
owner rule. Storage: a list key is JSON-encoded into the text
`answer_key` column (see assumption below). The 78–87 batch worker
reported 21 multi-answer rows for its range; the files contain 20 —
the file-verified total 134 governs (import guard bakes 134).

## Judgment calls (documented, not re-asked)

- Q6 both-operation gaps → section `suffix` + `affix_kind='both'` +
  flag (18 rows). One row arrived with section `'both'` and was
  normalized at merge to this rule: `eng2-p659-both-q6b-t87`
  (now section suffix, affix_kind both).
- `affix_kind='other'` (3 rows) where the key word is not a regular
  derivation of the printed root, keys verbatim, flagged:
  `eng2-p638-suffix-q6c-t71`, `eng2-p645-suffix-q6b-t76`,
  `eng2-p645-suffix-q6d-t76`.
- Prefix = its own section (67 rows); suffix section 233 rows
  (212 affix suffix + 18 both + 3 other).
- Q2 serial story order is canonical (key order); `table_order`
  recorded where determinable; Q2 key-vs-table wording differences
  kept verbatim with flags, never harmonized.
- Q9: all 60 rows `partial_credit=true`. Q10–12: all 150 rows
  `scored=false`, total marks only, no breakdown.
- Q10/Q12 word counts recorded only where printed (25 rows carry a
  word_count); never defaulted, never copied from a linked model.
- Q10 with guide sub-questions (a)–(e) stays 1 row.
- board_tag kept verbatim, never split (incl. multi-board lists).
- Test 117 key swap (p736) applied by content: under "8." is Q9's
  corrected paragraph, under "9." is Q8's connector list; test 116's
  key on the same page is correctly labeled and was NOT swapped.
- Key-page trap (p724/p725): the block at the head of p725 is test
  98's continuation (Q4–Q9), NOT test 97's — test 97's block ends on
  p724. Re-verified at 500 dpi; no correction was needed.
- PDF pp. 694/695 are swapped upside-down leaves (PDF p694 bears
  printed 695 and vice versa); rows record `source_pdf_page` and
  `source_printed_page` truthfully and differently; PDF = printed
  resumes at p696.
- No separate Composition Part exists beyond pp. 482–570 (p571 is a
  section divider, confirmed by probe).

## Cross-batch second pass on unlinked models (0 new links)

After all 6 batches, every unlinked Q10–12 topic was re-checked
programmatically against all 158 bank titles and all linked models.
No new link met the confidence bar, so all 30 stay held:

- The strongest candidate (flood-relief application topics in tests
  108 and 117 vs bank model `eng1-p553-writing-letter-31`) was
  spot-checked at 500 dpi (p553, prompt + answer head + tail). The
  model letter is addressed to the UNO; test 75's application prompt
  matches it exactly (same scenario, UNO addressee) and is already
  linked. Tests 108 (Deputy Commissioner) and 117 (Upazilla Chairman)
  differ on addressee — a substantive difference in a formal
  application, not a pronoun/title variant — so neither was linked.
- All other candidates were generic boilerplate overlaps (common
  prompt words only) already rejected by the batch workers on
  substance, or empty.

## Flagged topic matches (linked, with flags for parent review)

Test Q10–12 rows linked on topic (not exact title) or with a
type mismatch, all 500-dpi eye-verified and flagged in-file:

- Application prompts linked to letter-form models (guide's only
  model for the request): t69 Q11, t75 Q11.
- Title-variant links (same topic, guide title differs in form):
  t90 Q11, t93 Q10, t94 Q12, t100 Q10/Q11/Q12, t101 Q12, t102 Q11/Q12,
  t103 Q12, t104 Q12, t105 Q10, t107 Q11 (word-for-word prompt match
  incl. board tag), t108 Q12, t114 Q12 (changed held count 15→14
  in its batch: prompt-keyword search had missed the model on a
  pronoun shift), t116 Q10.
- t61 Q11: one letter corrected to the printed page form (see above).

## guide_error = true (6 rows — stored keys not trustworthy for scoring)

- `eng2-p692-preposition-q7c-t111` — key misprint ('form' for 'from').
- `eng2-p694-table-q2d-t114` — key misprint ('are' vs table 'save').
- `eng2-p647-suffix-q6d-t78` — key not derivable from printed root.
- `eng2-p648-prefix-q6a-t79` — key not derivable from printed root.
- `eng2-p653-transform-q4f-t83` — key answers a different question.
- `eng2-p664-transform-q4a-t91` — key answers a different question
  (boat journey vs train-journey question; guide misprint).

All other flagged rows (sic spellings, duplicated labels, box-count
quirks, word-count variants, key-vs-question wording differences that
do not change the answer) have guide_error = false: their keys are
correct as printed. Keys are kept verbatim everywhere, never corrected.

## Model-verification depth difference (stated honestly, not flattened)

- Batches 58–77, 88–117: each model page rendered at 500 dpi and
  viewed; title/prompt and body verified by eye (band crops for long
  models, not downscaled halves — two early downscaled-half readings
  in the 68–77 batch produced plausible-but-wrong text and were caught
  and corrected by band crops).
- Batch 78–87: each model page rendered at 500 dpi and viewed;
  prompt/title/board tag and body opening confirmed by eye, and the
  full model text then taken verbatim from the Paper-I-verified held
  row (`verified_visual=true` in `merged_units.json`), NOT
  re-transcribed in full from the scan. Model linkage for 78–87 is
  therefore match-confirmed, while other batches claim fuller page
  verification. One test-103 model text initially typed from memory
  was caught by the held-row audit and corrected to the held row
  verbatim; all 99–107 model texts were then re-audited
  programmatically against their held rows (exact match).

## Merge normalizations (files govern over worker reports)

1. The 88–97 batch kept its 5 unlinked Q10–12 rows inside `rows[]`
   (answer_text NULL) AND listed them in `held[]` (key `row_id`).
   At merge those 5 rows were REMOVED from `rows[]` so held means
   held-only everywhere: `eng2-p667-writing-application-q11-t93`,
   `eng2-p667-writing-composition-q12-t93`,
   `eng2-p669-writing-paragraph-q10-t94`,
   `eng2-p672-writing-application-q11-t96`,
   `eng2-p673-writing-paragraph-q10-t97`.
2. The 88–97 held entries carry no `marks`; marks were inferred from
   the fixed template (Q10=10, Q11=10, Q12=20) — this reconciles held
   marks to 392 and total marks to 6,000.
3. Section `'both'` → suffix + affix_kind both (t87 Q6b, above).
4. Multi-answer count: files say 134 (78–87 contributes 20, not the
   21 its worker reported).

## Import script notes for the parent (live run)

- Book/subject: `class9-english-2nd-bn-guide` / `english-2nd`
  (separate subject per owner rule; distinct from Paper-I
  `class9-english-1st-bn-guide` / `english`).
- `--dry-run` needs no password and touches no DB. Live run requires
  `SUPABASE_DB_PASSWORD` from the environment only; pre-import rows
  with the new book_id must be 0; post-insert verification covers
  total 3,666, per-section counts, guide_error 6, bank 158, with
  rollback on any mismatch. Success writes
  `paper2_import_audit.json` (ids + counts only).
- ASSUMPTION TO CHECK BEFORE THE LIVE RUN: `answer_key` is a text
  column (as Paper-I's raw-string usage implies). The 134 list keys
  are JSON-encoded to text by `paper2_import.py`; if the column is
  jsonb or text[], pass the list through instead (one line, marked
  in the script).
- DB-column gaps (same as Paper-I, documented not hidden): `scored`
  and `partial_credit` have no `guide_questions` columns — Q10–12
  rows are naturally unkeyed (no answer_key), and Q9 partial scoring
  must be derived by the app from section `punctuation`;
  `multi_answer` semantics are deferred to the scoring step;
  `affix_kind`, `word_count`, and model-link provenance live in the
  JSON archive and this report, not in DB columns.

## What could not be collected from files alone

Nothing for collection: all 60 tests are collected and verified, and
every gap is a held row above. The only items awaiting the parent are
the live-run steps (password, the answer_key column-type check, and
the pre-import 0 check) — all enforced as guards in the script.

## Live-run fix 2026-11-02 (batch write)

- First live attempt rolled back on a foreign key: the subjects table had no
  `english-2nd` row, so the new book row could not insert. Fixed by adding
  subject rows `english-2nd` and `biology` (biology was missing too and
  would have blocked its own write the same way). Nothing was written by
  the failed attempt (full rollback).
- Second live attempt rolled back on JSON: `marks_parts` (jsonb) received
  the raw string `1×10=10`, which is not valid JSON. Fixed in
  `paper2_import.py`, both test and bank branches: `marks_parts` is now
  sent as `Json(...)` when not None, the same pattern already used for
  `options`. Docstring updated; compile check passed.
- Third live attempt committed: 3,666 rows, live-verified (per-section
  counts, guide_error 6, bank 158, sets 60, list-encoded keys 134).
