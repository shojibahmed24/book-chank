# Talimit Class 9-10 Math — import DRY RUN report (2026-10-31)

No DB contact, no writes. Source: `questions_with_options.json` (3,720 rows,
same order as `questions_merged.json`) + `flagged-merged.json`.
Script: `_work/dry_run_import.py` (re-runnable).

## Counts (verified from file)

- Total: 3,720 rows, 3,720 unique ids, 0 duplicate ids.
- By chapter: ch0 238, ch2 348, ch3 474, ch7 430, ch8 777, ch9 319,
  ch11 235, ch16 532, ch17 367.
- By type: mcq 1,676, problem 1,700, creative 344.
- Marks: 0 non-null (never invented — stays NULL on import).
- guide_solution non-empty: 1,841 (preserved on import).
- Problem rows carrying an answer_key: 85 (answer_key MUST be nulled
  on import — answer_key is MCQ-only).
- ch0 (model tests): 238 rows, 128 MCQ, 0 keyed → single
  `set_id='model-test'`, browse-only, never auto-scored.
- MCQ: total 1,676, full options 1,170, keyed 939, full+keyed 909.
  ch0 contributes 0 keyed, so bank full+keyed is also 909.
- MCQ–MCQ content duplicates: 0 groups (cross-type stem sharing
  exists and is kept deliberately per the merge report, not scored).

## Quiz pool after holds (first import, if it ran)

- Start: 909 bank full+keyed MCQ.
- Hold 1 unreliable full+keyed row: `class9-10-math-ch2-p30-n201-problem`
  (type field mcq after correction; printed key খ, stem math yields ঘ;
  flag says "never auto-score, needs parent decision").
- Hold 4 caveated full+keyed rows (keys kept in file, but flagged
  "parent confirmation required before auto-scoring"):
  ch8-p407-n9 (গ), ch8-p431-n4 (ঘ), ch8-p462-n18 (খ), ch8-p463-n21 (গ).
- 5 ch8 candidates (p328-n1, p329-n6, p380-n23, p383-n4, p411-n4):
  NONE is full-optioned, so holding them changes the pool by 0 —
  but they must still be imported keyless (or held out) pending
  review, because 4 of them carry a key that could become scorable
  if options are ever completed. Note p411-n4 is also a caveated row.
- p380 twin `p380-n23-mcq-334`: MCQ, unkeyed — unscored either way.
- Table-key-held (29): already key-NULL in file. Caveated (5): all
  keyed in file (see above).
- **Pool after holds: 904.** Of those, 4 carry an `unverified`
  flag (segment-verified only, not proven wrong) and 0 carry any
  other unreliable flag. "Unverified" is not "wrong" — those 4 stay
  in the pool unless the user orders otherwise.

## Import mapping (for the live script, once unblocked)

- Target: `guide_questions` (008) only. No textbook-table writes.
- answer_key: MCQ rows only; problem/creative rows → NULL (85 nulled).
- options: MCQ rows only (dict ক/খ/গ/ঘ); non-MCQ → NULL.
- marks: always NULL. guide_solution: preserved where present.
- verified_visual: preserved. set_id: ch0 → 'model-test', else NULL.
- Held-from-scoring rows above: answer_key withheld on import
  (NOT guide_error=true — none is proven wrong except the ch2
  p30 row, where the math itself contradicts the printed key;
  even there, the flag says parent decision, so the live script
  will NOT set guide_error without that decision).

## BLOCKERS — live import must NOT run until the user decides

- **B1 book_id:** `guide_questions.book_id` is NOT NULL and references
  `books(id)`. Live DB books = 88 (class 6+7 only, verified
  2026-10-30). There is NO class-9 math book row to bind to.
- **B2 chapter_id:** Talimit chapter_ids (`class9-10-math-ch*`) do
  not exist in the `chapters` table, and the guide-bank Edge
  list/sets actions filter by textbook chapter_ids. Rows imported
  with chapter_id NULL (or a Talimit id the Edge never queries)
  would be INVISIBLE in the app — imported but unreachable.
  Guessing a mapping to class-6/7 chapters would be wrong.

## Decisions needed (user)

1. Binding route: (a) migrate class-9 textbooks first, then bind
   guides to real textbook chapters (cleanest, matches the class-7
   design, but textbook migration is large un-ordered work);
   (b) redesign the guide-bank Edge to serve guide-native chapters
   (needs a book-row decision + Edge + client change);
   (c) any other route the user names. No route is chosen here.
2. ch2 p30 row: import keyless, or hold out of import, or import
   with guide_error=true (math contradicts the printed key)?
3. 5 ch8 candidates + 4 caveated rows: import keyless, or hold
   out of the first import entirely?
4. After (1)–(3): live import script (single transaction, abort on
   any count mismatch) + live verification + Edge deploy if (b).
   That step needs the password again (not stored) and, for (b),
   a fresh deploy token.
