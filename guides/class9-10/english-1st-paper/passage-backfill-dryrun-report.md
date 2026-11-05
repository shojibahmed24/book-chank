# DRY RUN REPORT — English passage TEXT import (Phase 2 step 2.2)

PREPARATION + DRY-RUN ONLY. No database write, no deploy, no zip,
nothing under `bangla/` touched. This report + the mapping below
are built from files only. The write step is a separate parent run
with a transient password (see "What the parent runs").

Counts and row ids only. No passage, question, or answer text is
pasted anywhere in this report, the mapping, or the audit format.

## Deliverables (all under `passage-backfill/`)

- `row_text_mapping.json` — one entry per mapped row (3,995):
  `row_id -> {source_ref, assigned_ref | null, reason, method,
  signal}`. Contains ref keys + reason codes only, never texts.
- `import_passage_texts.py` — the write script (see below).
- `build_row_text_mapping.py` — the reproducible builder that
  produced the mapping from the staging file + row map +
  `merged_units.json` question content. Re-run it to regenerate.
- `import_audit.json` — written by the import script AT WRITE TIME
  (not present yet): outcome, counts, row ids per category,
  starter-differs (hashes only), skipped-non-null-post ids.

## Expected counts (dry-run validated, exit 0)

| Category | Rows |
|---|---|
| Total mapped rows | 3,995 |
| TO WRITE | 3,870 |
| — direct verified ref (rule 1) | 3,291 |
| — split-assigned pooled rows (rule 2) | 578 |
| — relabeled Solitude row (rule 3) | 1 |
| SKIPPED (stimulus_text stays untouched) | 125 |
| — self-contained matching (rule 4) | 60 |
| — self-contained dialogue fragments (rule 4) | 34 |
| — self-contained rearranging (rule 4) | 12 |
| — self-contained writing prompts (rule 4) | 3 |
| — visual-held for image display (rule 5) | 7 |
| — pooled, could not be identified (rule 2) | 8 |
| — generic discussion, unnamed poem (rule 9) | 1 |

Split-assigned by method: keyword (title/character) 336, diagnostic
token 146, quoted-line match 89, 5-word n-gram 5, quoted-title 2.
Split-assigned by target: Merchant of Venice 153, Purple Jar /
Rosamond 134, Two Mothers Remembered 49, Solitude 48, Time You
Old Gipsy Man 46, Stopping by Woods 44, Sands of Dee 38, Books
35, O Me! O Life! 31. Story of an Hour: 0 (no pooled story row
mentions it; its verified text exists but no row needs it here).

## Pooled rows that could NOT be identified (8, NULL + flagged)

No identifying anchor in question content; never guessed:

- `eng1-p182-poem-q8h` (main-20), `eng1-p307-poem-q8h`
  (main-34), `eng1-p383-poem-q8h` (main-42) — the "age" question
  (staging already flags it as a floating item; bare "age" occurs
  in too many texts to anchor it).
- `eng1-p209-poem-q8c` (main-24) — "caregiving lesson" question,
  no poem anchor.
- `eng1-p288-poem-q8g` (main-32) — "recurring questions"
  question, no poem anchor.
- `eng1-p312-story-q9d` (main-35), `eng1-p578-story-q9d`
  (special1-46), `eng1-p601-story-q9d` (special1-56) — motto
  question; the motto wording occurs in no candidate text, so no
  story is assigned rather than guessing.

## Solitude relabel (rule 3)

- Row: `eng1-p122-poem-q8g` (main-13).
- Write sets BOTH `stimulus_text` (O Me! stanza-1 text) AND
  `stimulus_ref` to `textbook poem: O Me! O Life!`.
- Proof on file: the queried words occur together in that stanza
  and not in the certified Solitude text; the identical question
  already sits under the O Me! bank row.
- Consistency check passed: no split-assigned Solitude row asks
  about those words; the 3 pooled rows that do ask about them
  (`eng1-p196-poem-q8h`, `eng1-p312-poem-q8g`,
  `eng1-p580-poem-q8g`) are assigned O Me! text by the same
  word-occurrence signal.

## Small-category skipped ids (full lists are in the mapping)

- Generic discussion (rule 9): `eng1-p118-poem-q8h` (main-12).
- Visual-held (rule 5, 7): `eng1-p145-writing-graph-c`,
  `eng1-p156-mcq-e(a)` … `eng1-p156-mcq-e(e)` (advertisement
  true/false set), `eng1-p157-writing-letter-f`.
- Self-contained writing (rule 4, 3): `eng1-p116-writing-dialogue-e`,
  `eng1-p161-writing-dialogue-q11`, `eng1-p161-writing-story-q10`.

## Rules that could NOT be fully applied from files alone

1. **Starter-differs (rule 8) — authoritative count unknown until
   write time.** The script reads live pre-write `stimulus_text`
   and logs every non-NULL differing row by id + hashes. File-stage
   proxy from `merged_units.json` (NOT write-time truth): among
   direct-verified rows, 25 starters differ from staged text, 267
   match, 2,999 have no starter. Split / relabeled / skipped rows
   have no file-stage starters at all.
2. **Time-addressee signal (20 rows, all to Gipsy Man).** These
   questions address Time as a person (offer / request / personify /
   desire / emotion / "stays for a day"). Within the closed 7-poem
   set only Gipsy Man personifies Time, so they are assigned
   there — but this rests on closed-set reasoning, not a quoted
   line. The 20 ids are queryable in the mapping
   (`signal == "time-addressee"`); spot-check them before commit
   if stricter proof is wanted.
3. **Rule 1 vs rule 4 overlap (8 rows) — resolved for rule 1.**
   These rows have verified refs AND matching/writing sections:
   `eng1-p154-matching-a` … `eng1-p154-matching-f` (Nepal passage),
   `eng1-p128-writing-paragraph-e`,
   `eng1-p380-writing-composition-b`. Their refs ARE real passages,
   so they are written. Rule 4's no-write scope is the
   unverifiable-ref rows of those sections only. If the parent
   disagrees, these 8 ids are the exact set to flip.
4. **O Me! first-stanza rows (rule 7): 74 rows get stanza-1 text**
   (42 direct across 5 ref-key variants + 31 split + 1 relabeled).
   Written exactly as staged; nothing invented for unprinted
   stanzas. Audit note: some of these rows may not be answerable
   from stanza 1 alone.
5. **Merchant set-7 (9 rows) + D2 bundled refs (39 rows, p392 +
   p416)** are written exactly as staged (single copy, bundled
   texts as-is). Merge-flag notes go to the audit log only, never
   into any DB text column.
6. **Split rows keep their original `stimulus_ref` in the DB.**
   Only the Solitude row's ref changes (rule 3). The row's own
   poem/story text is recorded in the mapping's `assigned_ref`
   for audit; the DB keeps the pooled test ref, which is what
   the test actually printed.
7. **Edge surfacing is NOT proven from files alone.** The workspace
   Edge guide-bank select already includes `stimulus_text`, but
   whether the DEPLOYED Edge copy does must be live-probed after
   import (query a known written row id through the Edge function
   and confirm `stimulus_text` returns). If it does not, the
   Phase 3 guide-bank redeploy must include it — the DB write
   alone will not surface texts in the app.

## The write script (`import_passage_texts.py`)

- Password ONLY from environment: `YS_DB_PASSWORD` (or
  `SUPABASE_DB_PASSWORD` fallback). No default, no file, no
  argument, no log. Refuses to run without it.
- Connection: same pattern as `backfill_stimulus_ref.py`
  (db.vvyiwyzredqoulufqgmg.supabase.co:5432, postgres/postgres,
  sslmode require; psycopg2 via `~/workspace/_db-libs`).
- No DDL, so no ACCESS EXCLUSIVE lock like the step-2.1 incident;
  row-level UPDATEs only, in 500-row chunks, one transaction.
- Pre-write guards (any failure -> ROLLBACK with ids, no commit):
  mapping size == map size (3,995) and id sets equal; every
  assigned ref exists in staging with non-empty text; exactly 1
  relabeled row targeting the O Me! key; `stimulus_text` column
  exists; every mapping id resolves in the DB; every live
  `stimulus_ref` still equals the mapped `source_ref` (guards
  against DB drift since the 2.1 backfill).
- Post-write verification (same transaction, before commit):
  every written row non-NULL with hash == staged text hash;
  relabeled row ref == O Me! key; every skipped row byte-identical
  to its pre-write value; sample ids per category recorded.
- COMMIT only if all guards + verifications pass, else ROLLBACK.
  Audit JSON is written in both cases (outcome field says which).

## What the parent runs

```sh
cd ~/workspace/yes-sir-ai-guides/class9-10/talimit/english/_work/redo/passage-backfill
python3 import_passage_texts.py --dry-run   # files only, already green
YS_DB_PASSWORD='<fresh>' python3 import_passage_texts.py
```

Then: read `import_audit.json` (outcome must be `committed`),
live-probe one written row through the Edge guide-bank function
for `stimulus_text`, and run the Phase 3 guide-bank redeploy if
the probe shows the select is missing it.

## Nothing blocking the write except the password

No rule is left unapplied except the write-time items above
(starter-differs count, live-ref drift guard, Edge probe). The
mapping is complete for all 3,995 rows: every row is either
assigned a verified text or null with a reason code; there are no
unclassified rows.
