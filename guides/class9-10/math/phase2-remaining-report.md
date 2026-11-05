# Phase 2 remaining prep — steps 2.4–2.9 (Yes Sir AI)

File-only verification + guarded scripts + dry-runs. NO database writes, NO
deploy, NO zip. No password was received by this task; every write step is
for the parent's run. No password, token, or secret appears in any file
here. This report carries counts + ids only — no question, answer, or
solution texts.

Deliverables in this directory (`math/_work/phase2-remaining/`):

| File | Purpose |
|---|---|
| `update_class7_guide_error.py` | 2.4 write script (8 ids) |
| `apply_class7_corrected_keys.py` | OPTIONAL 10-key script (adjacent gap, Gate-2-gated) |
| `reimport_ch2_p30.py` | 2.5 write script |
| `backfill_class7_chapter_number.py` | 2.8 write script (2,864 ids) |
| `update_math_corrections.py` | 2.6 script (empty update set + live verification) |
| `class7_chapter_map.json` | 2.8 mapping (2,864 ids) |
| `math_corrections_mapping.json` | 2.6 mapping (619 already-correct, 0 updates, 826 unjoinable) |
| `audit_2_*.json` | Dry-run audits (ids + counts only) |

Dry-run results (all exit 0, no DB touched):
`update_class7_guide_error` 8 ids planned; `apply_class7_corrected_keys`
10 ids planned; `reimport_ch2_p30` pilot source verified, logic planned;
`backfill_class7_chapter_number` 2,864 ids mapped, counts match;
`update_math_corrections` already_correct 619, update_pairs 0, unjoinable
826.

---

## 2.4 — Class-7 8 uncorrected guide-error MCQs: VERDICT = keep guide_error, NO corrected key

Source: guide `class7/06-Math-Guide.pdf` (244 pages, 143 MB); file
`class7/math/questions.json` (2,864 rows); log `class7/math/corrections-log.json`
(77 entries). All 8 rows carry `correct_value: null, never_auto_score:
true, kind: guide_error_mcq` in the log; file answer_keys are the printed
keys stored verbatim; `verified_visual=true` for all 8; display policy
verbatim.

**Method note, stated plainly:** a fresh eye-read was ATTEMPTED (200-dpi
renders of PDF pages 78, 95, 135, 161, 185, 194, 218 produced at
`/tmp/c7/`), but this environment did not return perceivable image
content to this agent from the file reads, and tesseract is not installed
(no OCR cross-check possible). The verdicts below therefore rest on (a)
two agreeing prior reads — the file verification_notes (200-dpi crops,
recording dotted keys, option values, and error analyses) and the
corrections-log entries — and (b) this agent's INDEPENDENT recomputation
of every item's mathematics from the recorded stem facts. In each case
the conclusion follows from the mathematics, not from trusting a dot.
A visual pass by the parent (renders at `/tmp/c7/`) can still close the
eye-read item; it is listed under "genuinely undecidable / still open"
below. Native resolution of the guide PDF is ~100 dpi (embedded images
1979×2800 px on 1399.68×2016 pt pages), so 200-dpi renders are upscales
for viewing comfort — no detail exists beyond ~100 dpi.

Per-row verdicts (ids in the file's id scheme; printed page = guide folio):

1. `class7-math-bn-guide-ch3-p87-mcq51` (printed p87, PDF p78, printed
   key ক). Unit conversion recomputed: 1 acre = 4046.86 sq m. Neither
   printed option equals it (the dotted option is the nearest value
   only, never exact). NO correct option exists. Keep guide_error.
2. `class7-math-bn-guide-ch4-p107-mcq13` (printed p107, PDF p95, printed
   key খ). Stimulus confirmed by the two neighbouring items (their
   dotted keys fix the three expressions). Recomputed result of
   (first−second)+third is absent from the option set; two options are
   duplicates of each other and neither equals the recomputed result.
   NO correct option exists. Keep guide_error.
3. `class7-math-bn-guide-ch6-p153-ex61mcq9` (printed p153, PDF p135,
   printed key খ). Algebraic simplification recomputed: the simplified
   form is absent from the option set, and the dotted option is
   algebraically wrong. NO correct option exists. Keep guide_error.
4. `class7-math-bn-guide-ch7-p182-ex72mcq10` (printed p182, PDF p161,
   printed key ঘ) and 5. `class7-math-bn-guide-ch7-p182-ex72mcq11`
   (same page, printed key গ). The printed stimulus is self-contradictory
   (sentence 1 gives a relation between the two unknowns; sentence 2
   forces them equal, contradicting sentence 1). The printed keys
   require an unstated relation that is NOT in the printed stimulus.
   No consistent solution exists as printed; inventing the missing
   relation is forbidden. NO correct key. Keep guide_error (both).
5. `class7-math-bn-guide-ch9-p211-ex91smcq61` (printed p211, PDF p185,
   printed key খ). Geometry recomputed: right isosceles triangle with
   the right angle at B gives base angles 45° each; one listed statement
   is false (60° claim), another is impossible (a leg equalling the
   hypotenuse), leaving only the first statement true — and no
   "first-only" option exists. NO correct option exists. Keep guide_error.
6. `class7-math-bn-guide-ch9-p221-ex92smcq32` (printed p221, PDF p194,
   printed key ঘ). MULTIPLE valid answers: the triangle inequality
   admits more than one listed value. The printed key is valid but NOT
   unique. Keep guide_error + flag multi-valid; never auto-score as a
   single key. (Scoring interpretation is the same undecided multi-key
   item as Paper-II's 134 rows — see below.)
7. `class7-math-bn-guide-ch10-p249-ex102smcq26` (printed p249, PDF p218,
   printed key ক). Cosine-rule recomputation from the recorded figure
   measures: the asked angle is ≈32°, while every listed option is a
   different angle (≈48°, 90°, ≈42°, ≈21° — all four independently
   recomputed and consistent with the figure). NO correct option
   exists. Keep guide_error.

**Write step:** `update_class7_guide_error.py` — env-only password,
`--dry-run` file-only; live run SELECTs current
guide_error/flag_note/answer_key first (old values into
`audit_2_4_guide_error.json`), UPDATEs only rows not already correct
(SET guide_error=TRUE + per-row verdict-only flag_note; answer_key
untouched), post-check requires all 8 guide_error=true else ROLLBACK.
Idempotent. Note: the Class-7 import script already flags all 18
guide-error MCQs (see 2.8), so IF the live import used that script the
DB flags are already set and this run is a no-op confirmation — the
script is safe either way.

**Adjacent gap (NOT 2.4 scope, flagged, optional script provided):** the
other 10 guide-error MCQs DO have correct values in the log, but
questions.json still carries the printed keys and the Class-7 import
script does NOT apply correct_value — so whether the live DB carries
corrected keys is UNVERIFIED from files. Ids (file scheme):
ch2-p44-ex21-mcq18, ch2-p56-ex22b-mcq17, ch3-p86-mcq26, ch5-p125-mcq34,
ch8-p200-ex8mcq2, ch8-p201-ex8smcq31, ch9-p211-ex91smcq59,
ch10-p242-ex101smcq12, ch10-p242-ex101smcq30, ch11-p274-ex11mcq2.
`apply_class7_corrected_keys.py` is header-marked OPTIONAL and must run
ONLY if the Gate-2 live check shows DB keys still printed: it SETs
corrected_answer_key = log correct_value VERBATIM (printed answer_key
untouched, guide_error stays true), following the English corrected
pattern. Some correct_values are descriptive values, not bare option
letters — stored verbatim; how the app scores them is a display/scoring
matter, not decided here. Dry-run green (10 ids planned).

---

## 2.5 — ch2 p30 corrected re-import: correct key PROVEN; pilot row already carries it

Old row: `class9-10-math-ch2-p30-n201-problem` (old file: answer_key খ,
printed p30, PDF p54, question_type corrected problem→mcq per printed
p30). The old verification_note is truncated in the file but the
mathematics is unambiguous: the stem defines a set of integers whose
squares are ≤ 9, i.e. exactly {-3,-2,-1,0,1,2,3}. The printed key খ
omits ±3 and is WRONG. The correct option is ঘ.

Pilot counterpart found: `pilot21-mcq_bank-201` (pilot-2.1
transcribed_units.json; kind mcq, section mcq_bank, printed p30, PDF p54,
lesson 2.1, question_number ২০১, marks 1) — SAME stem (with proper minus
signs) and SAME options, and its answer_key is ALREADY ঘ. Its flagged
field notes no worked explanation is printed (solution null) and the key
comes from the margin marker only; `verified_visual=false`.

**Dot-reading discrepancy, flagged:** the old extraction records the
margin disc as খ; the pilot extraction records the margin marker as ঘ.
The mathematics settles the correct answer as ঘ regardless of which
dot-reading is right. The pilot row's key was not visually verified, but
this agent's mathematical verification confirms ঘ.

**Write step:** `reimport_ch2_p30.py` — NEVER inserts the old id while
the pilot row exists (that would duplicate the question). Five outcomes
in order: (1) pilot exists with key ঘ → no-op; (2) pilot exists with
wrong/missing key → UPDATE to the corrected pattern (printed key kept
in answer_key, corrected_answer_key=ঘ, guide_error=true,
correction_note); (3) pilot absent but old id exists → same UPDATE on
the old id; (4) neither exists → INSERT the pilot row from the pilot
source file (key ঘ, guide_error=false, flag_note recording that the
printed guide key খ was proven wrong; book class9-math-bn-guide,
chapter_id NULL, chapter_number 2, section mcq_bank, marks from pilot
unit); (5) both exist → ABORT with report (unexpected duplication;
never silently merge). Post-check requires the surviving row to carry
key ঘ (answer_key or corrected_answer_key) else ROLLBACK. Dry-run green
(pilot source verified, key ঘ, logic planned).

---

## 2.6 — 1,445 question-text corrections UPDATE: VERDICT = obsolete for live data; NO bulk update

File-stage: `math/_work/cleanup/corrected_merged.json` = 1,445 rows
(union of corrected_w1..w6; only 2 pdf_page fixes in MERGE_NOTES.md).
Worker method: creative rows = full unit (stimulus + all sub-parts)
where unambiguous, sub-part rows = stimulus + that sub-part; MCQ rows =
stem only (options/keys untouched); guide misprints transcribed
verbatim, not repaired. **221 flagged rows are SEPARATE**
(`cleanup/flagged_list.md`) — they NEED RE-SPLIT and stay OUT of this
round; they are NOT inside the 1,445. Folio-offset caveat (does NOT
affect an id-joined text update, but DOES affect page-based joins):
offset (pdf − printed) varies by chapter: ch2/ch3/ch7/ch9 = 24,
ch0/ch11/ch16/ch17 = 23, ch8 = 22; ~50 ch16 rows may have pdf_page off
by one (two-column spread wobble). Do not blindly shift pdf_pages.
Open question carried from MERGE_NOTES (moot now, since the update set
is empty): exact scope for creative rows was never parent-confirmed.

**Join finding (the hard result):** all 1,445 corrections join EXACTLY
(1,445/1,445, 0 missing) to the OLD 3,720-row file (ids
`class9-10-math-chX-pY-nZ-type`). By chapter: ch0 30, ch2 164, ch3 243,
ch7 74, ch8 261, ch9 141, ch11 92, ch16 267, ch17 173. By old type: mcq
1,145, problem 150, creative 150. But **live DB rows use PILOT ids, not
old-scheme ids**, so no id join to live rows exists. Pilot sources
(total 7,366 units): pilot-0 690, pilot-2.1+2.2 862, pilot-3 1,411,
pilot-7 443, pilot-8 952, pilot-9 787, pilot-11 441, pilot-16 1,067,
pilot-17 713 — vs 10,543 live rows; live DB composition is NOT provable
from files (difference 3,177 unexplained by files alone; do not guess).
The Talimit import stores question_text VERBATIM from units, so
compare-before-write against pilot texts is valid.

**Four join attempts (all file-side, same chapter + kind-compatible):**
1. (chapter, printed_page, number): FAILED — numbers restart per
   section (same page+number collides across textbook_exercise /
   mcq_bank / creative); old page attribution is off by 2–3 pages for
   ch8 bank items. 1,038 unmatched, 354 diverged, 53 ambiguous, 0
   already-correct, 0 still-garbled.
2. Text similarity, threshold 0.95, option-set tiebreak: pilot texts
   ALREADY EQUAL corrected texts in matched cases. Kind mapping: old
   mcq → pilot {mcq, mcq_bank}; old problem → {short, task,
   textbook_exercise, practice_work}; old creative → {creative,
   sub_part}. Note: pilot `question_kind` ≠ id prefix (e.g. some
   pilot8-textbook_exercise units have kind mcq); pilot8 mcq numbers are
   NOT unique (320 units vs 101 distinct numbers) — number is a weak
   feature, never a key. Result before the number-strip fix: 92
   already-correct, 1,284 no-high-similarity, 65 matched-diverged, 4
   ambiguous ties. Root cause found: corrected texts KEEP the leading
   question number while pilot texts STRIP it (one-token penalty
   capping similarity at ~0.92).
3. v2 normalization (strip leading numbers + board tags + triangle
   glyphs △/▲→Δ + units সে.মি./সেমি→cm, মি.→m): 519 already-correct,
   95 matched-diverged (pilot stands), 19 ambiguous ties, 812
   no-high-similarity, **0 update candidates**. Remaining failure
   modes: (a) pilot texts add trailing school/board attributions the
   corrected texts strip; (b) corrected texts sometimes TRUNCATED
   mid-sentence while the pilot text is fuller (pilot is MORE complete,
   pilot stands); (c) board-tag-only differences (metadata, not
   question text; the pilot's eye-verified tag wins); (d) glyph-only
   differences (same question).
4. v3 (strip ALL `[...]` bracket blocks + prefix rule — corrected stem
   is a prefix of pilot stem or vice versa, length ≥10 chars, counts
   as a match): **619 already-correct, 0 update candidates, 826
   unjoinable**. Stratification of the 619: 617 EXACTLY equal after
   normalization, 2 prefix matches (pilot text fuller; pilot stands).
   Caveat: 135 of the 619 are short stems (<30 chars, mostly
   diagram-dependent MCQs) — matched on stem + option tiebreak where
   available; "already correct" means the pilot text equals the
   corrected text, with identification resting on the tiebreak. Since
   no write follows from a match, this caveat affects confidence
   wording only, not safety.

**Why 0 updates is the right call, not a failure:** NOT ONE pilot text
still resembles the old garbled text. The old garble came from OCR of
the printed pages; the pilot transcriptions are fresh eye
transcriptions of the same pages and cannot reproduce OCR artifacts.
For the 826 unjoinable items, the live pilot text (if the item exists
live) is a clean transcription, not the old garble — overwriting it
with an older correction would be wrong or redundant. The only case
where an update would be needed — a live row whose text is BOTH
different from the correction AND wrong — cannot be established from
files; it needs a targeted re-read of that item's printed page.

**Unjoinable 826 by (chapter, old type):** ch0 mcq 11 / problem 8;
ch2 creative 19 / mcq 53 / problem 3; ch3 creative 24 / mcq 93 /
problem 17; ch7 creative 8 / mcq 28 / problem 3; ch8 creative 19 / mcq
138 / problem 34; ch9 creative 30 / mcq 27 / problem 13; ch11 creative
6 / mcq 38 / problem 11; ch16 creative 19 / mcq 45 / problem 33; ch17
creative 25 / mcq 106 / problem 15.

**Script:** `update_math_corrections.py` + `math_corrections_mapping.json`
(619 already-correct pairs with old id → pilot id; 0 update_pairs; 826
unjoinable with chapter/type/reason). `--dry-run` validates mapping
integrity (total 1,445) file-only, exit 0. Live mode is READ-ONLY
verification of the 619 (live text must match pilot-source or corrected
text after normalization; anything else reported as drift, never
auto-fixed) and writes NOTHING while the update set is empty. If a
future review supplies individually verified (pilot_id → corrected
text) pairs, the same script applies them with compare-before-write
guards (missing → skip + report, never error; text == pilot text →
update; text == corrected text → no-op; anything else → ABORT whole
transaction with ROLLBACK; post-check requires every updated row to
carry the new text). Audit JSONs carry ids + counts + match status
only — never question/answer texts; if an update ever runs, pre-update
texts go to a separate revert file (marked as such) with only hashes in
the audit.

**What 2.6 must NEVER do:** join on old ids directly against live rows
(live rows don't carry old ids); join on (page + number) alone
(collides across sections; old page attribution wobbles 2–3 pages);
overwrite a clean pilot text with an older correction when they differ
only in board tags, glyphs, unit renderings, or attributions (pilot
wins); apply the 221 flagged re-split rows (stay out); invent a
correct value anywhere.

---

## 2.7 — ch8 9 held MCQs: HOLD STANDS, ids confirmed, no script

Exact ids from `math/_work/import_live.py` EXCLUDED dict (exact ids
only, NEVER prefix patterns — p329-n6 must not exclude p329-n60/n62,
p383-n4 must not exclude p383-n43/n47/n48; header comment: "5 ch8
candidates + 5 caveated keys, overlapping at p411-n4" = 9 distinct
rows; "Held rows stay in the file for a later reviewed import; they are
NOT deleted"):

1. `class9-10-math-ch8-p328-n1-mcq` (third-decision held; printed 328)
2. `class9-10-math-ch8-p329-n6-mcq` (third-decision held; printed 329)
3. `class9-10-math-ch8-p380-n23-mcq` (third-decision held; printed 380)
4. `class9-10-math-ch8-p383-n4-mcq` (third-decision held; printed 383)
5. `class9-10-math-ch8-p411-n4-mcq` (third-decision held+caveated; printed 411)
6. `class9-10-math-ch8-p407-n9-mcq` (third-decision caveated; printed 407)
7. `class9-10-math-ch8-p431-n4-mcq` (third-decision caveated; printed 431)
8. `class9-10-math-ch8-p462-n18-mcq` (third-decision caveated; printed 462)
9. `class9-10-math-ch8-p463-n21-mcq` (third-decision caveated; printed 463)

All 9 FOUND in `math/questions_with_options.json`. Class-7 ch8 is NOT
the source: class7 chapter-8 pilot file shows 93/93 verified (200-dpi
re-read of PDF 176–177 pending solutions; 2 guide-error-flagged MCQs
ex8mcq2 + ex8smcq31 — those are among the 10 corrected, not held; 1
non-MCQ guide note; 0 flagged; MCQ keyed 71/71; rows 93 = creative 21 +
mcq 71 + task 1; guide folio range 195–202, PDF range 171–178).

**Gate-2 live-check item:** whether these 9 ids are present in the live
DB is UNVERIFIABLE from files. If present, removal needs an EXPLICIT
user order (deletion is destructive; do NOT auto-delete). Report only;
do NOT import them.

---

## 2.8 — Class-7 chapter_number backfill: mapping fully derivable from file

Why NULL: the Class-7 import script
`class7/math/_work/import_to_guide_tables.py` DOES compute
chapter_number from chapter_id (function `chapter_number()`: regex
`ch(\d+)$` → int) and DOES flag all 18 guide-error MCQs (function
`flagged_ids()`: kind == guide_error_mcq AND never_auto_score is True;
raises if never_auto_score rows exist outside that kind) — but its
INSERT maps chapter_number → a chapter_id UUID and has NO chapter_number
column. Hence guide_questions.chapter_number was never written for
Class-7 rows. (Its INSERT also sets guide_error via FLAG_COLUMN =
"guide_error" — so IF the live import used this script, DB already has
guide_error=true for all 18; the open 2.4 item is the CORRECT VALUE, not
the flag. Gate-2 must confirm the flag state; the 2.4 script is
idempotent either way.)

Mapping (`class7_chapter_map.json`, 2,864 ids, all file rows have
chapter_id, 0 NULL in file): ch1 310, ch2 394, ch3 182, ch4 286, ch5 407,
ch6 212, ch7 271, ch8 93, ch9 301, ch10 191, ch11 217.

**Write step:** `backfill_class7_chapter_number.py` — env-only password,
`--dry-run` validates mapping + counts (no DB); live run idempotent
(UPDATE ... WHERE chapter_number IS DISTINCT FROM N), captures old
values into `audit_2_8_chapter_backfill.json`, post-check requires all
2,864 mapped + per-chapter counts else ROLLBACK. Any id whose chapter
is not derivable would be left untouched — none exist in this file.
Dry-run green.

---

## 2.9 — Pointer-only rule verdict: English precedent, ALREADY APPLIED, no remaining rows, no script

The live Talimit import already applied it (IMPORT_DRYRUN.md, ch0
section): "Pointer-only: 384 inserted (389 − 5 dropped short/creative
pointer rows) — guide_solution NULL + the printed pointer in `note`
verbatim, nothing invented. (All 668 inserted rows are solution-null:
ch0 prints no worked solutions at all.)" The 9-10 flagged-merged.json
(1,948 entries; kinds unverified 928, unkeyed 676, no_solution 205,
unreliable 105, table_key_held 29, caveated_key 5) is a general flagged
list, not a pointer list.

File search for remaining pointer-only rows: class7 questions.json — 12
pattern candidates were FALSE positives (worked solutions using
"অনুরূপ" = corresponding angles, a geometry term, or "পূর্বের" =
previous-step references inside worked solutions); class7
guide_solution empty = 1,246 rows (mostly MCQs — normal, key suffices,
not pointer-only); 9-10 questions_with_options.json — 0 pointer
candidates. **Finding: 0 true pointer-only rows remain unhandled in
files.**

**Verdict (standing rule for any future pointer rows):** solution NULL
+ pointer note verbatim, rows stay, never invented text — the same as
the English precedent (solution NULL + pointer note, 112 such rows in
the English Paper-I import). No script needed.

---

## What the parent's write run does (in order)

1. `update_class7_guide_error.py` (live) — 8 ids, guide_error=true +
   verdict flag_notes; answer_key untouched; audit old values.
2. `reimport_ch2_p30.py` (live) — expected outcome (1): pilot row
   exists with key ঘ → no-op; any other outcome follows the script's
   five-branch logic; never inserts a duplicate.
3. `backfill_class7_chapter_number.py` (live) — 2,864 chapter_numbers;
   per-chapter counts must match the mapping or ROLLBACK.
4. `update_math_corrections.py` (live) — verification only (update set
   empty): confirms the 619 live texts match pilot-source/corrected
   texts; reports drift/missing; writes nothing.
5. OPTIONAL, Gate-2-gated only: `apply_class7_corrected_keys.py` (live)
   — only if Gate-2 shows the 10 log-corrected keys are still printed
   in DB.

All scripts: env-only password (`YS_DB_PASSWORD` or
`SUPABASE_DB_PASSWORD`), refuse without it, single transaction, ROLLBACK
on any guard failure, audit JSON written on success.

**Gate-2 live checks (parent, read-only):** 8 guide_error flags true;
ch2 p30 surviving row carries key ঘ; 2,864 chapter_numbers with the
per-chapter counts above; 9 held ch8 ids absent-or-reported (removal
only on explicit user order); 384 pointer rows intact; 18 Class-7
guide_error flags state (confirms whether the import script already
flagged them); 10 log-corrected keys state (decides the optional
script); 619 already-correct live texts match (via the 2.6 script's
verification mode).

---

## Genuinely undecidable from files alone (flagged, none silently decided)

- **Live DB composition:** 7,366 pilot units vs 10,543 live rows
  (difference 3,177 unexplained by files). No file proves which live
  rows correspond to which pilot units beyond the 619 verified joins.
- **Whether the 10 log-corrected Class-7 keys are already in DB.**
  (Optional script exists for the "still printed" case only.)
- **Whether the 9 held ch8 ids are in the live DB.** (Removal needs an
  explicit user order if present.)
- **Multi-key scoring:** still UNDECIDED (Paper-II 134 rows +
  class-7 ex92smcq32 multi-valid case await it). Collection/import do
  not need it; auto-scoring display does. Do NOT decide it silently.
- **Fresh eye-read of the 8 Class-7 pages:** renders exist at
  `/tmp/c7/` (200 dpi, native ~100 dpi) for a visual pass; this agent's
  verdicts rest on prior 200-dpi crop notes + corrections-log +
  independent recomputation (see 2.4 method note). If a visual pass
  contradicts a note, the visual pass wins and the 2.4 verdict +
  flag_note for that row must be corrected before the write run.
- **826 unjoinable corrections:** no confident live-row join exists
  from files alone; they stay as-is (pilot texts stand) unless a future
  targeted re-read of an individual printed page joins one.
- **221 flagged re-split entries:** stay out of this round entirely.
- **Carried (not this task's):** ch13 bank-MCQ importance normalisation
  and tile re-verification for ch4-early + special-board (Biology prep
  open items).
