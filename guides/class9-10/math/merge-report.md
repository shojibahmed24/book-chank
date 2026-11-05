# MATH MERGE REPORT — Talimit Class 9–10 (Yes Sir AI)

Worker: MATH MERGE (subagent), 2026-10-30. Scope: `math/` only. No other subject,
app, APK, or Supabase folder touched. Nothing deleted. No DB import, no options
extraction (both still pending — see §9). Originals untouched:
`questions.json` still 3,680 rows, `chunks.json` still 52 chunks, `_complete/`
files unmodified. Merge script (re-runnable, pure function of the inputs):
`_complete/_merge_2026-10-30.py`. This report carries structure and counts
only — no guide question/answer text is pasted anywhere in it.

## 1. Totals

- **Merged rows: 3,720** (exactly the expected total — no forcing needed).
  Start 3,680 + 40 recovered rows = 3,720. **Duplicate ids: 0** (3,720 unique ids).
- **Schema check: PASS.** Every merged row has exactly the original 16 fields
  (`answer_key, chapter_id, display_policy, guide_printed_page, guide_solution,
  id, marks, pdf_file, pdf_page, question_text, question_type, section,
  source_tag, verification_note, verified_visual, depends_on`). No `options`
  field exists anywhere (see §9). The chapter files' extra field
  `recovered_from_flagged` (present on all 40 recovered rows) was stripped and
  its value appended to each row's `verification_note`, so the schema is restored
  without losing provenance.
- **Row order in `questions_merged.json`:** sorted by `guide_printed_page`,
  then `chapter_id`, then `id` (guide page order).
- **MCQ rows: 1,676 — keyed 939, unkeyed 737.** Problem/creative rows carrying
  a printed MCQ key: 85 (after the §4 strips; 95 before). Total keyed rows: 1,024.
- **verified_visual overall: 2,084 / 3,720 = 56.0%.** `depends_on`: null on all
  3,720 rows (see §7f).

## 2. Per-chapter counts

Family-file counts (rows as they arrived in the latest `_complete` file):

| family | latest file | rows | verified | % |
|---|---|---|---|---|
| ch0 (model tests) | ch0.json | 238 | 114 | 47.9% |
| ch2 | ch2.json | 348 | 258 | 74.1% |
| ch3 | ch3r3.json | 474 | 323 | 68.1% |
| ch7 | ch7r.json | 430 | 379 | 88.1% |
| ch8a | ch8a.json | 387 | 84 | 21.7% |
| ch8b | ch8br.json | 390 | 360 | 92.3% |
| ch9 | ch9r.json | 319 | 46 | 14.4% |
| ch11 | ch11r.json | 235 | 85 | 36.2% |
| ch16a | ch16ar.json | 262 | 184 | 70.2% |
| ch16b | ch16br4.json | 271 | 98 | 36.2% |
| ch17 | ch17r.json | 366 | 153 | 41.8% |

Merged counts by `chapter_id` (after the single §7d transfer):

| chapter_id | rows | verified | % |
|---|---|---|---|
| class9-10-math-ch0 | 238 | 114 | 47.9% |
| class9-10-math-ch2 | 348 | 258 | 74.1% |
| class9-10-math-ch3 | 474 | 323 | 68.1% |
| class9-10-math-ch7 | 430 | 379 | 88.1% |
| class9-10-math-ch8 (8a+8b) | 777 | 444 | 57.1% |
| class9-10-math-ch9 | 319 | 46 | 14.4% |
| class9-10-math-ch11 | 235 | 85 | 36.2% |
| class9-10-math-ch16 (16a+16b) | 532 | 282 | 53.0% |
| class9-10-math-ch17 (incl. transferred p788 row) | 367 | 153 | 41.7% |

Weak areas CONFIRMED (not assumed): ch9 14.4%, ch8a 21.7% (the "first half"
figure), ch16b 36.2%, ch11 36.2%. Honest meaning of `verified_visual` here:
page viewed, numbered item confirmed present, and the row contains that item's
stimulus/solution core (segment standard — ch3 worker notes state this
explicitly, and the same standard is visible in the other families' notes).
**Clean verbatim text is NOT claimed** for any chapter: rows remain
fragment-heavy OCR in places, and verification is segment-based. ch9's worker
notes record labels 487–576 as page-checked (PDF 511–600); ch8b's work-state
records all its pages rendered + verified. Those page-coverage claims are the
workers', carried here without re-verifying every page at merge.

Recovered rows (present in a latest `_complete` file, absent from the original
3,680) — 40 total: ch2 1, ch3 5, ch7 1, ch8a 4, ch9 1, ch11 2, ch16b 17,
ch17 9. ch0 and ch16a recovered 0. Every original row was replaced by its
family's latest file (0 original rows left unreplaced; no id appears in two
families). Note on the task brief: it said `chapter_id` is null in the original
file — it is not; the original file carries populated `chapter_id` values and
the family mapping was verified from those values plus the row-id prefixes.

## 3. Flags and corrections — merged totals (not sums)

- **`flagged-merged.json`: 1,948 entries, 1,685 unique ids.**
  By kind: `unverified` 928, `unkeyed` 676, `no_solution` 205, `unreliable` 105,
  `table_key_held` 29 (merge-created, §4), `caveated_key` 5 (merge-created, §5).
  By chapter (id prefix): ch8 479, ch0 357, ch16 307, ch9 277, ch3 163, ch2 99,
  ch11 93, ch7 92, ch17 75, marker/other pseudo-ids 5. 33 flag entries refer to
  rowless marker/segment items with no merged row (listed in §8).
- How 1,947 is built (so it is auditable, not a sum): latest per-family flag
  files 1,813 entries + still-open carry-overs from immediate predecessors 101
  (ch3 r2: 100, ch16b br3: 1 — see §7e) − 2 resolved by merge decisions (§5)
  + 5 caveated-key flags + 29 table-held flags + 1 original-flagged carry-over
  (ch2 p35-n3, §8) + 1 work-state content-mismatch flag (ch8b p414-n16, §5)
  = 1,948. Deduplicated by full (id, kind, reason) triple.
- **`corrections-log-merged.json`: 1,222 entries** (unique (id, field) pairs),
  each tagged with `source_file`. Construction: union over ALL revision
  correction files per family, latest revision winning per (id, field) = 1,197
  (raw total across revision files 1,601; latest-only files alone sum to 724 —
  the union is used because some latest files are round-delta logs, e.g.
  ch3r3 lists only 5 round-4 corrections while its 474 rows embody ~242
  documented corrections from rounds 1–4), + 34 merge entries, of which 9
  overwrote an earlier entry for the same (id, field) and 25 were new
  (1,197 − 9 + 34 = 1,222). Merge entries are tagged `source_file: MERGE`.
  Superseded ROW files were not merged in; superseded CORRECTION files were
  read for decisions and consolidated as above, never double-counted.

## 4. Rule (a) — table keys (the largest merge judgement)

No unverified table key remains in any `answer_key`:

- **ch0: 300 keys held, 0 applied.** `ch0-answertables.json` holds 10 tests ×
  30 keys. ch0 merged rows have 0 keyed rows (128 MCQs all unkeyed, all flagged
  `unkeyed` in ch0-flags). Nothing was taken from the tables.
- **ch3 PDF 268 table: NOT used.** Confirmed by ch3r2 + ch3r3 notes (disc-only
  rule; the model-test uttormala on PDF 268 was explicitly not used for keys)
  and by scan: 0 ch3 keyed rows cite PDF 268 / a table in their notes.
- **ch7 PART 04: 21 keys STRIPPED at merge.** The 21 ch7 rows whose notes cite
  "key from printed uttormala table on PDF 338 (450dpi crop read)" had their
  keys set to null, with a merge note on each row and a `table_key_held` flag
  carrying the letter + source (list in §4 table below). `verified_visual`
  was left unchanged (text verification is separate from key provenance).
  The 7 further PART 04 gap readings for printed 313 (items with no PDF 337 row)
  were never in rows and remain in the gap-notes appendix (§10).
- **ch11 grid: NOT applied.** 0 ch11 keyed rows cite a grid/table; the only grid
  mention in ch11 files is a flag noting a page "shows … the model-test answer
  grid only" with no key taken from it.
- **ch8b PDF 488: table-only keys STRIPPED (8 rows); math/disc-proven keys KEPT
  (2 rows).** PDF 487 (model-test page) has no margin marks, so its keys rest
  on the PDF 488 table unless independently proven. Stripped to null + held as
  `table_key_held` flags: p463-n3 (ক), p463-n5 (গ), p463-n7 (ঘ), p463-n8 (ঘ),
  p463-n10 (ক), p463-n25 (গ), p463-n29 (খ), p463-n30 (ক). KEPT: p462-n18 (খ —
  table + math x=60 agree, §5) and p463-n21 (গ — table + math agree, §5).
- **Boundary NOT extended (parent question, §11):** model-test table keys in
  other families were left untouched because task rule (a) lists only the five
  sources above: ch2 printed-91 table keys (12 rows), ch16b printed-786 table
  keys (14 rows), ch17 printed-796 table key (1 row). If the parent wants the
  same rule applied there, those 27 keys strip the same way.

Stripped ch7 PART 04 keys (id → held letter):

| id | letter | id | letter |
|---|---|---|---|
| class9-10-math-ch7-p313-n1-problem | খ | class9-10-math-ch7-p313-n22-problem | ঘ |
| class9-10-math-ch7-p313-n3-problem | ক | class9-10-math-ch7-p313-n25-problem | ঘ |
| class9-10-math-ch7-p313-n6-mcq | ঘ | class9-10-math-ch7-p313-n26-mcq | ক |
| class9-10-math-ch7-p313-n7-problem | খ | class9-10-math-ch7-p313-n27-problem | ক |
| class9-10-math-ch7-p313-n8-mcq | গ | class9-10-math-ch7-p313-n28-problem | খ |
| class9-10-math-ch7-p313-n10-problem | খ | class9-10-math-ch7-p313-n30-mcq | খ |
| class9-10-math-ch7-p313-n11-problem | ঘ | class9-10-math-ch7-p313-n12-mcq | ক |
| class9-10-math-ch7-p313-n13-mcq | খ | class9-10-math-ch7-p313-n14-mcq | গ |
| class9-10-math-ch7-p313-n15-problem | খ | class9-10-math-ch7-p313-n16-mcq | গ |
| class9-10-math-ch7-p313-n18-mcq | গ | class9-10-math-ch7-p313-n19-mcq | ঘ |
| class9-10-math-ch7-p313-n20-mcq | গ | | |

## 5. Rule (c) — caveated keys and content (each case resolved explicitly)

- **ch8b 4 caveated keys — ALL KEPT, caveat flags retained** (keys are
  disc/math-proven, not table-only; the caveat is about number/label lag, so
  the flag survives in `flagged-merged.json` as kind `caveated_key`):
  - p411-n4-mcq → ঘ: filled margin mark on page image, stem/options matched;
    caveat: row n4 vs printed Q47.
  - p407-n9-mcq → গ: filled margin mark, stem/options matched, explanation agrees;
    caveat retained (label vs header lag).
  - p431-n4-mcq → ঘ: filled margin mark, stem/options matched, explanation
    (120°) agrees; caveat: row n4 vs printed Q6.
  - p462-n18-mcq → খ: PDF 488 table খ + math cross-check (x+80=2(x+10), x=60)
    agree; caveat retained for parent decision. Its `pdf_page` correction
    (486→487) is already in the latest row.
  - Plus a 5th caveated key found in the work-state (not in the task's list of
    4): p463-n21-mcq → গ, table + math agree, mixed-text caveat; key kept,
    caveat flag added the same way.
- **ch16a 5 disc-vs-explanation mismatches — NOTHING injected into any row.**
  All five are rowless disc observations in `ch16ar-state.json` notes (no
  matching clean row exists), so there was no row key to change:
  - printed 677 item 8: disc reads গ, explanation concludes 17 (= খ) — conflict,
    no key recorded.
  - printed 677 item 17: disc ambiguous খ/ক vs explanation value (ক) — no key.
  - printed 680 item 51: disc ক, printed explanation concludes 128 — **guide
    error**: correct rhombus area for diagonals 8 and 16 is (8×16)/2 = **64**,
    not 128. Recorded here only; no row exists for printed-680 item 51, so no
    row carries 128 or 64 as a key.
  - printed 684 item 96: disc not captured; computation gives square area 72
    (from diagonal 12) — recorded as a computation note only, not a key.
  - printed 687 item 129: disc reads গ vs geometric diagonal √2a (= ঘ) —
    apparent conflict, no key recorded, re-read requested by the worker.
  Other ch16a number/content mismatches (e.g. row content matching a different
  printed item number) were likewise left unkeyed in the chapter files and are
  carried in the merged flags unchanged.
- **ch16b p756 item 90 → key corrected ঘ→খ, plus label corrected 755→756.**
  Evidence: br4 flag records stem + number match to row p755-n90-mcq, margin
  disc খ on PDF 779, options including 16, and math 6a²=96 → a²=16 = খ; the
  prior row key ঘ contradicted both disc and math. The br4 corrections entry
  for this row said "evidence only, no change — identity still unproven", which
  conflicts with its own flag's stem+number match; the merge follows the flag's
  positive match + two independent proofs (disc, math) and corrects the key.
  Two cautions preserved: the row text still contains a neighbouring-fragment
  contamination (per the br4 flag), so `verified_visual` stays False and the
  row must NOT be scored until its text is re-split clean; and the br4 flag
  also called the printed label 755 stale — corrected to 756 (PDF 779 = printed
  756 under the ch16 PDF−23 pattern, §6). The flag entry itself was removed
  from the merged flags as resolved, and both changes are logged as MERGE
  corrections entries.
- **ch8b 2 content mismatches:**
  - p414-n16-problem: stored descriptor differs from the page image for short
    question 16 (PDF 438); number + numbers match. **NOT corrected** — worker
    left it for parent decision; row kept as-is. It appeared ONLY in the
    ch8br work-state (`content_mismatches`), in no flags file, so the merge
    added it to `flagged-merged.json` as kind `unreliable` rather than losing
    it. Its `verified_visual` is True in the chapter file (item confirmed) —
    that flag-vs-verified tension is preserved, not papered over.
  - p415-n20-problem: work-state text correction (image reads 8/6 diameters;
    the row's own solution bleed gives diameter 8). **APPLIED at merge:**
    the row's single occurrence of the digit ৪ (diameter position) was changed
    to ৮, with a merge note and a MERGE corrections entry. (The chapter file
    had not applied this correction — its text still carried ৪.)
- **ch2 same-question two printings with different keys — NOT LOCATED as two
  keyed rows.** Searched: keyed-row stem similarity across ch2, and all ch2
  flags/corrections for reprint/duplicate-printing language. No pair of keyed
  rows with the same stem and different keys exists in the merged set. The
  closest flagged cases were all left exactly as the worker left them, with no
  silent pick:
  - p30-n201 (id suffix `-problem`, type `mcq`): printed stem's arithmetic
    yields ঘ but the printed margin disc is clearly খ; key kept as printed খ,
    flagged `unreliable` ("possible guide error … never auto-score, needs
    parent decision"). Note the tension: this row's `verified_visual` is True
    in the chapter file despite the unreliable flag.
  - p91-n17-mcq: model-test item whose answer-table cell is not clearly
    distinguishable AND whose stem set is infinite, so no listed option is
    mathematically valid (possible guide error); key left null, never guessed.
  - p29-n80 duplicate-number pair (p29-n80-problem + p29-n80-mcq): both garbled,
    neither certainly matched to a printed item; both unkeyed and flagged.
  If the parent's "two printings" case is a different pair, it is not in the
  chapter files under that description — please point at the two row ids.
- **ch9 Q115 → key assigned ক by identity computation (merge decision).**
  Row p530-n115-mcq (PDF 554, printed 530): margin disc reads গ (tight-crop
  verified, per ch9r page-notes), no printed explanation on p.530/p.531
  arbitrates. Identity computation, verified at merge: sin5B = cos5B →
  tan5B = 1 → 5B = 45° → B = 9°, which is option ক. Under the formula-pass
  policy (mathematically-correct value wins over a print/disc error) the key
  is set to ক and the case is recorded as a guide-disc error. The row's
  `verified_visual` stays False (its text is still garbled); the flag entry was
  removed as resolved and a MERGE corrections entry was added. (The other
  Q115 row, p486-n115-mcq, is a merged Q115+Q120 fragment on PDF 510 and
  remains unkeyed/flagged for re-split; the printed-486 disc reading খ for
  item 115 in the page-notes belongs to that fragment context, not to the
  p.530 item — the two Q115 printings are not conflated.)
- **ch16br4's 2 documented key changes — BOTH APPLIED (they are already in
  ch16br4.json and are carried into the merged rows unchanged):**
  - p723-n14-mcq: খ→গ. Basis: printed 724 image (PDF 747), disc গ + explanation
    value 42.02; prior key খ (= 21.01, the radius value) contradicted both.
    This page was also independently sampled at merge (§6).
  - p786-n15-mcq: খ→ঘ. Basis: printed 788 official model-test answer table
    (item 15 = ঘ) + printed 787 item-15 stem/options (breadth 5 = ঘ); prior key
    খ (= 13, the diagonal value) contradicted the official answer. The row
    remains unverified (solution contaminated) per the worker note.

## 6. Rule (b) — ch16b 40 label changes (br3 → br4)

**ACCEPTED in full.** Every one of the 40 `guide_printed_page` changes in
ch16br4.json carries an individual documented basis in ch16br4-corrections.json
(item found on the named printed page image, usually with disc + explanation
agreement), and the systematic pattern is PDF page − 23 (the old labels were
PDF − 24-based). At merge, 5 PDF pages were freshly rendered from
`math-general.pdf` at 150dpi and their header folios read:
- PDF 747 → header 724 (new label for the p723→724 group; item 14 present with
  explanation concluding 42.02).
- PDF 756 → header 733 (new label for the p732→733 group).
- PDF 780 → header 757 (new label for the p756→757 group).
- PDF 783 → header 760 (new label for the p759→760 / p758→760 group).
- PDF 784 → header 761 (new label for the p759→761 group).
All five sampled headers match the br4 labels exactly. No label was accepted on
a guess: the 40 changes are (old → new, all with `pdf_page` unchanged except
the 9 noted in the diff where the PDF page itself was also corrected):
723→724 (4 rows), 724→725 (2), 725→726 (1), 730→731 (1), 732→733 (3), 733→734 (4),
733→735 (2), 734→735 (1), 748→749 (1), 750→751 (1), 756→757 (4), 756→758 (1),
757→759 (2), 758→759 (3), 758→760 (2), 759→760 (6), 759→761 (2). Row ids were
NOT renamed (ids still embed the old label numbers, e.g. p723-n14-mcq now
carries `guide_printed_page` 724) — ids are stable keys, labels are fields.
Full per-row list: the 40 rows are exactly those differing in
`guide_printed_page` between ch16br3.json and ch16br4.json; the merged rows
carry the br4 values.

## 7. Rules (d)–(h)

- **(d) Transfers.**
  - p788 ch16→ch17: APPLIED. Row class9-10-math-ch16-p788-n4-mcq now carries
    `chapter_id` class9-10-math-ch17 and section অধ্যায় ১৭ (MERGE corrections
    entry added). Its id, `guide_printed_page` (788) and `pdf_page` (812) are
    unchanged for traceability. Consequence to know: grouping by id prefix
    still shows this row under ch16; grouping by `chapter_id` shows it under
    ch17 (hence ch16 532 / ch17 367 in §2 vs family files 533 / 366).
  - PDF 339 ch7→ch8 bleed: HONOURED WITHOUT DELETION OR DUPLICATION. Row
    class9-10-math-ch7-p315-n389-mcq (PDF 339 = the chapter-8 opener) is flagged
    `unkeyed` in ch7r-flags ("row text is ch8 contents-table bleed … no MCQ
    marker exists, never keyed") and is carried in the merged flags as such.
    Its chapter_id/id were NOT rewritten to ch8, because ch8a already covers
    PDF 339 with its own 3 rows (p339-n12-creative, p339-n5-problem,
    p339-n5-problem-90) — moving the bleed row would duplicate ch8 content.
    The row stays unkeyed and unverified.
  - ch8b p462-n2-problem: true page UNKNOWN — left exactly as in ch8br.json
    (`guide_printed_page` 462, `pdf_page` 486, unverified); its `unverified`
    flag is carried in the merged flags. No page was assigned by guess.
- **(e) Gap/disc notes preserved (not dropped).** Full appendix in §10:
  ch9 page-notes (discs with no clean row + 4 unresolved discs), ch7 58
  gap-notes, ch17 74 gap-notes, ch16b disc-read-but-rowless items, ch11
  duplicate pairs, ch0 PDF 922 exclusion (below). The source files themselves
  are untouched, so nothing is lost even where this report summarises.
  - ch11 duplicate pairs (PDF 629/630/639/640 in the task's shorthand = PDF
    pages, i.e. printed 605/606/615/616): KEPT BOTH, cross-noted, NOT deduped.
    Pairs in the merged flags: p605-n1-problem vs p605-n13-creative (identical
    stimulus text; solution lives on the creative row), and p615-n1-problem vs
    p615-n24-creative (identical text; one is a splitter duplicate, neither is
    clean). Both members of each pair remain as merged rows AND as flags.
    Related duplicates also kept flagged: p599-n7-problem (duplicates
    p599-n2-creative / p599-n3-creative fragments) and p623-n9-problem-188
    (duplicate of p623-n9-problem).
  - ch0 PDF 922 test-01 MCQ page: EXCLUDED — no merged row references PDF 922
    or printed 922 (ch0 rows span printed 899–917 only), and no test-01 key was
    applied to any row. See the ambiguity note in §11 (the task's page
    reference does not match any file entry found).
- **(f) `depends_on`: null on all 3,720 rows.** No genuine linked prose was
  found by any chapter worker, and none was invented at merge. This matches the
  brief's expectation (all null is an acceptable result, not a gap to fill).
  The 52 prose chunks in `chunks_merged.json` are carried over byte-identical
  from `chunks.json` (same ids, same page ranges); no chunk was altered by the
  merge, because the merge changes rows, not prose — but note the consequence:
  no chunk is linked from any row, so chunk-based retrieval still has no
  row→chunk edges. The p788 transfer does not affect any chunk (chunks are
  prose units, not rows).
- **(g) Problem-type rows carrying printed MCQ keys: unified at merge by
  keeping the key + its in-note source.** 85 such rows remain keyed in the
  merged file (31 ch7, 8 ch8a, 1 ch11, 29 ch16a, 2 ch16b, 24 ch17 — minus the 10
  ch7 PART 04 strips in §4, which were problem-typed). Every one of these
  rows' `verification_note` already documents the key source (margin disc /
  printed disc, with "question_type left unchanged" where the printed item is
  an MCQ but the row is typed problem/creative) — verified by scan at merge,
  so no note was rewritten for these rows. Their keys are traceable through
  the merged corrections log where a corrections entry exists, and through
  the chapter worker notes/updates files otherwise (ch17 keys live in
  `ch17r-updates.json`, ch8b keys in `ch8br-work-state.json`).
  `question_type` was never changed on any row.
- **(h) Original flagged 56 — fully accounted for.**
  - Id-bearing entries (22): 7 resolved, 15 still flagged.
    - Resolved (7): p117-n7-problem, p136-n4-problem (recovered under a problem
      id from flagged p136-n4-mcq, since the printed item is a worked problem),
      p150-n8-problem, p219-n27-mcq, p286-n49-mcq, p348-n28-mcq, p531-n134-mcq.
    - Still flagged (15): 11 never recovered and flagged (p36-n4, p63-n34,
      p64-n4, p90-n36, p111-n90, p120-n4, p153-n4, p261-n8, p388-n1-problem-374,
      p543-n4, p619-n32); 3 recovered as rows but still flagged (p326-n26,
      p355-n92, p382-n28 — unverified/unkeyed in their latest flags); 1
      (p35-n3-mcq) found in NEITHER ch2.json NOR ch2-flags.json, so the merge
      carried it into `flagged-merged.json` from the original `flagged.json`
      reason rather than dropping it silently.
  - Marker/segment entries (34 runaway segments, no row id): these were never
    rows, so they cannot map 1:1 to merged rows. Their dispositions are: (i)
    recovered where a worker proved an item (the 40 recovered rows include
    marker recoveries, e.g. ch3 p210-n11-mcq and the resolved ids above);
    (ii) carried as 33 rowless flag entries in `flagged-merged.json` (§8);
    (iii) checked-and-not-recovered notes in the chapter notes files (ch3
    notes: PDF 206 Q54/Q55, PDF 221, PDF 231 duplicate, PDF 233, PDF 262 items
    checked, not recovered; ch9r page-notes recovery attempts: 6 attempted, 1
    recovered, 5 kept flagged). No marker segment was forced into a row.

## 8. Cases left flagged and why (summary — full list is flagged-merged.json)

- All `unverified` (928) / `no_solution` (205) rows: page/item not yet visually
  confirmed or no printed solution found; solutions never invented. Includes
  ch8a's 303 unverified rows (the 21.7% verified figure's complement) and
  ch9's 273 unverified rows.
- All `unkeyed` (676): MCQ dot not yet visually read, or row is a merged /
  mislabelled fragment with no single attributable key (e.g. ch9 p475-n7/n8
  merged fragments with two different discs; ch3 problem-typed rows holding
  MCQ disc readings for re-split only).
- All `unreliable` (104): garbled / duplicate / mis-split fragments, guide-error
  suspects (ch2 p30-n201, p91-n17), content/number mismatches, and the 33
  rowless marker/segment items:
  ch11 p607-marker17-creative, p619-n32-problem; ch16 p661-flagged-40,
  p663-flagged-3, p667-flagged-10, p672-flagged-6, p693-flagged-1, p696-flagged-6,
  p700-flagged-8; ch2 p35-n3-mcq, p36-n4-problem, p63-n34-problem, p64-n4-problem,
  p90-n36-problem; ch3 p111-n90-mcq, p120-n4-problem, p153-n4-problem,
  p182-marker2-item, p197-marker13-item, p207-marker8-creative,
  p238-marker4-creative; ch7 p261-n8-problem; ch8 p388-n1-problem-374; ch9
  p497-flagged-3, p510-flagged-26, p538-flagged-2, p543-n4-problem,
  p569-flagged-7; ch17 flagged-marker-1-remainder-p847,
  flagged-marker-25-remainder-p844, flagged-marker-50-remainder-p859,
  ch2 flagged-marker1-p41, flagged-marker29-p13.
- `table_key_held` (29) and `caveated_key` (5): §4 and §5.
- ch8b observed gaps NOT added (work-state, preserved here): marks were read
  but no stored rows exist, so nothing was invented — PDF 431 Q3; PDF 432
  Q4–Q7, Q11–Q13; PDF 433 Q17, Q19–Q27; PDF 434 Q29, Q30, Q32, Q35, Q37, Q38,
  Q40, Q41; PDF 435 Q42–Q45, Q48, Q49; PDF 454 MCQ Q1, Q2; PDF 455 MCQ Q4, Q5,
  Q7, Q8; PDF 459 MCQ Q1, Q4, Q5, Q8; PDF 460 MCQ Q9, Q11, Q12, Q16, Q17, Q19;
  PDF 461 MCQ Q21, Q22, Q23, Q25, Q26, Q27, Q32, Q33.

## 9. Pending items (NOT done by this merge)

1. **Options extraction — BLOCKS class 9–10 Math quiz-readiness.** 0 of 1,676
   MCQ rows carry options (the schema has no options field at all). Until
   options are extracted and joined by row id, no MCQ row is quiz-usable as a
   scored item, keyed or not. This merge deliberately did not invent options.
2. **DB import — NOT done.** No Supabase/app write was attempted, per brief.
3. **Re-split work** for the 1,948 flag entries (merged fragments, mislabelled
   rows, duplicate pairs, garbled rows, rowless markers).
4. **Verification completion** for ch9 (85.6% unverified), ch8a (78.3%
   unverified), ch16b (63.8% unverified), ch11 (63.8% unverified), ch17
   (58.3% unverified), ch0 (52.1% unverified) — and clean-transcription work
   where rows are verified only under the segment standard.
5. **Parent decisions** listed in §11.

## 10. Preserved notes appendix (gap/disc notes not dropped)

### ch7 gap-notes (58 entries, from ch7r-gap-notes.json)

| printed | number | letter | source |
|---|---|---|---|
| 284 | 12 | গ | disc-read |
| 284 | 13 | ঘ | disc-read |
| 284 | 17 | গ | disc-read |
| 284 | 18 | ঘ | disc-read |
| 284 | 19 | গ | disc-read |
| 284 | 21 | ঘ | disc-read |
| 284 | 24 | খ | disc-read |
| 284 | 26 | খ | disc-read |
| 284 | 28 | ঘ | disc-read |
| 284 | 29 | খ | disc-read |
| 285 | 33 | ঘ | disc-read |
| 285 | 38 | ক | disc-read |
| 285 | 40 | ঘ | disc-read |
| 285 | 41 | খ | disc-read |
| 285 | 43 | ক | disc-read |
| 285 | 44 | ঘ | disc-read |
| 278 | 1 | — | prior-worker-carryforward-no-letter-recorded |
| 278 | 5 | — | prior-worker-carryforward-no-letter-recorded |
| 278 | 7 | — | prior-worker-carryforward-no-letter-recorded |
| 279 | 14 | — | prior-worker-carryforward-no-letter-recorded |
| 280 | 22 | — | prior-worker-carryforward-no-letter-recorded |
| 280 | 23 | — | prior-worker-carryforward-no-letter-recorded |
| 280 | 26 | — | prior-worker-carryforward-no-letter-recorded |
| 280 | 27 | — | prior-worker-carryforward-no-letter-recorded |
| 280 | 28 | — | prior-worker-carryforward-no-letter-recorded |
| 280 | 32 | — | prior-worker-carryforward-no-letter-recorded |
| 280 | 34 | — | prior-worker-carryforward-no-letter-recorded |
| 280 | 35 | — | prior-worker-carryforward-no-letter-recorded |
| 280 | 36 | — | prior-worker-carryforward-no-letter-recorded |
| 282 | 50 | — | prior-worker-carryforward-no-letter-recorded |
| 282 | 51 | — | prior-worker-carryforward-no-letter-recorded |
| 282 | 54 | — | prior-worker-carryforward-no-letter-recorded |
| 282 | 55 | — | prior-worker-carryforward-no-letter-recorded |
| 282 | 57 | — | prior-worker-carryforward-no-letter-recorded |
| 282 | 58 | — | prior-worker-carryforward-no-letter-recorded |
| 282 | 60 | — | prior-worker-carryforward-no-letter-recorded |
| 282 | 61 | — | prior-worker-carryforward-no-letter-recorded |
| 282 | 63 | — | prior-worker-carryforward-no-letter-recorded |
| 300 | 4 | — | prior-worker-carryforward-no-letter-recorded |
| 301 | 6 | — | prior-worker-carryforward-no-letter-recorded |
| 301 | 7 | — | prior-worker-carryforward-no-letter-recorded |
| 307 | 1 | — | prior-worker-carryforward-no-letter-recorded |
| 307 | 4 | — | prior-worker-carryforward-no-letter-recorded |
| 307 | 7 | — | prior-worker-carryforward-no-letter-recorded |
| 307 | 11 | — | prior-worker-carryforward-no-letter-recorded |
| 310 | 47 | — | prior-worker-carryforward-no-letter-recorded |
| 310 | 48 | — | prior-worker-carryforward-no-letter-recorded |
| 310 | 50 | — | prior-worker-carryforward-no-letter-recorded |
| 310 | 54 | — | prior-worker-carryforward-no-letter-recorded |
| 310 | 57 | — | prior-worker-carryforward-no-letter-recorded |
| 310 | 59 | — | prior-worker-carryforward-no-letter-recorded |
| 313 | 4 | ক | PART04-model-test-uttormala-PDF338-no-pdf337-row; same-stem bank items exist separately for 17 (file 258 Q64, key গ) and 21 (file 283 Q6, key ঘ) — different instances, not conflated |
| 313 | 5 | ক | PART04-model-test-uttormala-PDF338-no-pdf337-row; same-stem bank items exist separately for 17 (file 258 Q64, key গ) and 21 (file 283 Q6, key ঘ) — different instances, not conflated |
| 313 | 17 | খ | PART04-model-test-uttormala-PDF338-no-pdf337-row; same-stem bank items exist separately for 17 (file 258 Q64, key গ) and 21 (file 283 Q6, key ঘ) — different instances, not conflated |
| 313 | 21 | ক | PART04-model-test-uttormala-PDF338-no-pdf337-row; same-stem bank items exist separately for 17 (file 258 Q64, key গ) and 21 (file 283 Q6, key ঘ) — different instances, not conflated |
| 313 | 23 | গ | PART04-model-test-uttormala-PDF338-no-pdf337-row; same-stem bank items exist separately for 17 (file 258 Q64, key গ) and 21 (file 283 Q6, key ঘ) — different instances, not conflated |
| 313 | 24 | গ | PART04-model-test-uttormala-PDF338-no-pdf337-row; same-stem bank items exist separately for 17 (file 258 Q64, key গ) and 21 (file 283 Q6, key ঘ) — different instances, not conflated |
| 313 | 29 | ক | PART04-model-test-uttormala-PDF338-no-pdf337-row; same-stem bank items exist separately for 17 (file 258 Q64, key গ) and 21 (file 283 Q6, key ঘ) — different instances, not conflated |

Reading: 16 entries carry a disc letter with no source tag (printed 284/285
items); 35 entries are prior-worker carryforwards with NO letter recorded
(printed 278–282, 300, 301, 307, 310 items — gaps, not keys); 7 entries are the
PART 04 table readings for printed 313 (no PDF 337 row) quoted in full above.
These letters were NOT copied onto any row by this merge (the 21 PART 04 row
keys that did exist were stripped per §4).

### ch17 gap-notes (74 entries, from ch17r-updates.json `gaps`)

74 entries; sections: {'general MCQ': 74}; PDF pages 827–842; margin_disc values: {'ক': 18, 'খ': 20, 'ঘ': 16, 'গ': 20}.

| pdf_page | label_printed | visible_folio | section | printed_no | margin_disc |
|---|---|---|---|---|---|
| 827 | 803 | 804 | general MCQ | 50 | ক |
| 827 | 803 | 804 | general MCQ | 53 | খ |
| 828 | 804 | 805 | general MCQ | 62 | ক |
| 828 | 804 | 805 | general MCQ | 63 | খ |
| 828 | 804 | 805 | general MCQ | 68 | ঘ |
| 828 | 804 | 805 | general MCQ | 69 | গ |
| 828 | 804 | 805 | general MCQ | 70 | খ |
| 828 | 804 | 805 | general MCQ | 71 | গ |
| 828 | 804 | 805 | general MCQ | 74 | গ |
| 828 | 804 | 805 | general MCQ | 75 | খ |
| 829 | 805 | 806 | general MCQ | 76 | ঘ |
| 829 | 805 | 806 | general MCQ | 77 | খ |
| 829 | 805 | 806 | general MCQ | 78 | খ |
| 829 | 805 | 806 | general MCQ | 79 | গ |
| 829 | 805 | 806 | general MCQ | 80 | ঘ |
| 829 | 805 | 806 | general MCQ | 81 | ঘ |
| 829 | 805 | 806 | general MCQ | 83 | খ |
| 829 | 805 | 806 | general MCQ | 84 | খ |
| 829 | 805 | 806 | general MCQ | 85 | ক |
| 829 | 805 | 806 | general MCQ | 86 | খ |
| 829 | 805 | 806 | general MCQ | 87 | ক |
| 829 | 805 | 806 | general MCQ | 88 | ক |
| 830 | 806 | 807 | general MCQ | 90 | ক |
| 830 | 806 | 807 | general MCQ | 91 | ঘ |
| 830 | 806 | 807 | general MCQ | 94 | ক |
| 830 | 806 | 807 | general MCQ | 95 | ক |
| 830 | 806 | 807 | general MCQ | 96 | ঘ |
| 831 | 807 | 808 | general MCQ | 99 | ক |
| 831 | 807 | 808 | general MCQ | 101 | খ |
| 831 | 807 | 808 | general MCQ | 102 | ঘ |
| 831 | 807 | 808 | general MCQ | 105 | ক |
| 831 | 807 | 808 | general MCQ | 107 | ঘ |
| 832 | 808 | 809 | general MCQ | 109 | গ |
| 832 | 808 | 809 | general MCQ | 110 | ঘ |
| 832 | 808 | 809 | general MCQ | 112 | ক |
| 832 | 808 | 809 | general MCQ | 113 | খ |
| 832 | 808 | 809 | general MCQ | 116 | ঘ |
| 832 | 808 | 809 | general MCQ | 117 | খ |
| 833 | 809 | 810 | general MCQ | 118 | ক |
| 833 | 809 | 810 | general MCQ | 121 | গ |
| 833 | 809 | 810 | general MCQ | 122 | গ |
| 833 | 809 | 810 | general MCQ | 123 | ঘ |
| 833 | 809 | 810 | general MCQ | 124 | গ |
| 833 | 809 | 810 | general MCQ | 126 | ক |
| 834 | 810 | 811 | general MCQ | 129 | ঘ |
| 837 | 813 | 814 | general MCQ | 163 | খ |
| 837 | 813 | 814 | general MCQ | 165 | খ |
| 838 | 814 | 815 | general MCQ | 169 | গ |
| 838 | 814 | 815 | general MCQ | 170 | খ |
| 838 | 814 | 815 | general MCQ | 172 | গ |
| 838 | 814 | 815 | general MCQ | 176 | গ |
| 838 | 814 | 815 | general MCQ | 180 | ঘ |
| 839 | 815 | 816 | general MCQ | 182 | গ |
| 839 | 815 | 816 | general MCQ | 184 | ক |
| 839 | 815 | 816 | general MCQ | 186 | গ |
| 840 | 816 | 817 | general MCQ | 193 | ক |
| 840 | 816 | 817 | general MCQ | 195 | খ |
| 840 | 816 | 817 | general MCQ | 196 | গ |
| 840 | 816 | 817 | general MCQ | 198 | গ |
| 840 | 816 | 817 | general MCQ | 202 | গ |
| 840 | 816 | 817 | general MCQ | 203 | খ |
| 841 | 817 | 818 | general MCQ | 209 | ঘ |
| 841 | 817 | 818 | general MCQ | 210 | ক |
| 841 | 817 | 818 | general MCQ | 212 | গ |
| 841 | 817 | 818 | general MCQ | 221 | খ |
| 841 | 817 | 818 | general MCQ | 222 | ঘ |
| 842 | 818 | 819 | general MCQ | 224 | গ |
| 842 | 818 | 819 | general MCQ | 225 | ক |
| 842 | 818 | 819 | general MCQ | 226 | খ |
| 842 | 818 | 819 | general MCQ | 227 | গ |
| 842 | 818 | 819 | general MCQ | 228 | খ |
| 842 | 818 | 819 | general MCQ | 229 | ঘ |
| 842 | 818 | 819 | general MCQ | 230 | ক |
| 842 | 818 | 819 | general MCQ | 237 | গ |

Note the ch17 calibration visible in these gaps: visible folio = label + 1
(PDF = label + 24). The 3 `new_flags` in ch17r-updates.json (p804-n4-problem,
p799-n4-problem, p810-n4-problem — garbled fragments, not standalone items)
are included in the merged flags via ch17r-flags.json.

### ch9 page-notes (from ch9r-page-notes.json)

- Pages checked: 102 (labels 487–576; visual pass recorded complete for labels
  487–576, PDF 511–600; label 576 / PDF 600 is the chapter-11 title page, so
  ch9 content ends at label 575).
- Discs with no clean row (disc letter observed, deliberately NOT copied onto
  any merged row): per printed page — 475: 6, 476: 9, 477: 7, 478: 10, 479: 6, 480: 10, 481: 9, 482: 10, 483: 6, 484: 8, 485: 6, 486: 7, 488: 5, 489: 8, 490: 10, 513: 8, 519: 12, 520: 11, 521: 14, 522: 12, 523: 13, 524: 12, 525: 12, 526: 8, 527: 11, 528: 12, 529: 12, 530: 14, 531: 16, 574: 2.
  Full per-item disc table remains in ch9r-page-notes.json
  (`discs_no_clean_row`); only the per-page counts are repeated here.
- Unresolved discs (4, no letter asserted anywhere): (1) printed-475
  left-column duplicate sin A − cos C item — disc not cleanly read (the
  right-column printing of the same item reads ক); (2) printed-477 Q23 — disc
  not cleanly resolved, printed explanation gives খ, crop check needed;
  (3) printed-478 Q34 — disc glyph ambiguous ক/গ even in crops, printed
  explanation gives ক, higher-contrast crop needed, and no clean row exists
  for Q34 in any case; (4) printed-530 Q115 — resolved at merge to ক by
  identity computation (§5), disc গ recorded as a guide-disc error.
- Folio calibration (ch9r): PDF 511 header 489 vs label 487; PDF 521 header 499
  vs label 497; then headers run label + 2 (PDF 536 header 514 vs label 512,
  etc.) — i.e. ch9 row labels lag the visible header by 2 in the later range.
  Labels were NOT rewritten by the worker or by this merge.
- Flagged-recovery outcome (ch9r): 6 attempted, 1 recovered (p531-n134-mcq),
  5 kept flagged (p497-flagged-3, p510-flagged-26, and three further
  flagged pseudo-ids in the merged flags).

### ch16b disc-read-but-rowless items

Round-1 (ch16br) flag entries for items checked on page images but with no
stored row — preserved, not added as rows: p716-creative-39 (printed 716/717
boundary), p738-creative-8 (not on printed 738), p744-item-7 (not a stored
row), p760-problem-40 (not on printed 760), p777-item-2, p779-creative-34.
Of these, the last two WERE later recovered in round 4 as merged rows
(p777-item-2 → p778-n30/n31-creative companions; p779-creative-34 → p780-n33/
n34-creative companions, with source_tag provenance on those rows). The other
four remain rowless and flagged in the round-1 files; they are not separate
entries in the merged flags because the merged flags use the latest (br4)
file + still-open carry-overs, and these four items' round-1 entries were
superseded by the round-4 row set — their evidence lives in ch16br-flags.json
and is recorded here so it is not lost.

### ch16a disc notes with no row (see also §5)

The ch16ar-state.json notes record, per PDF page, printed items with clear
discs but no matching scope row (dozens of items, e.g. PDF 671 items 14/19/22,
PDF 674 items 50–60, PDF 677 items 79–85, PDF 703 items 51/55/57, PDF 710 items
121/122/129/134/136). NONE of those disc letters was copied onto any merged
row. The five conflict/error cases among them are listed in §5.

## 11. Ambiguities and questions for the parent (merge did not guess)

1. **ch7/ch8b table strips (§4):** 29 keys were stripped on the brief's rule
   (a) even though workers had read them (450dpi crop for ch7, table-agreement
   re-check for ch8b). If the parent considers those reads verified, restore
   is mechanical: take the letters from `flagged-merged.json`
   (`table_key_held` entries) back into `answer_key` and delete the flags.
2. **ch9 Q115 (§5):** key set to ক by computation against disc গ. If the
   parent trusts the disc over the computation, revert p530-n115-mcq to null
   (or to গ) and re-add its `unkeyed` flag; the computation is documented in
   the row note and in §5 for audit.
3. **ch16b p755-n90 (§5):** key corrected against the br4 corrections entry's
   "identity still unproven" caution, on the strength of the br4 flag's own
   stem+number match + disc + math. The row stays unverified and must not be
   scored until re-split; if the parent disagrees with the identity match,
   revert the key to ঘ and restore the flag.
4. **ch0 PDF 922:** the brief says the PDF 922 test-01 MCQ page is out of scope
   and excluded. No file entry matching PDF 922 (or printed 922) was found:
   ch0 rows span printed 899–917, and the answertables test01 entry cites
   source PDF 923 / printed label 900 with a note that its MCQ question page
   (printed 899) is outside the rendered range. The merge therefore excluded
   "PDF 922" as "no row, no key applied" — please confirm which page was meant
   (scan PDF 922 = printed 898 by the +24 calibration, which is outside ch0's
   row range either way).
5. **Table-rule boundary (§4):** ch2 (12), ch16b (14) and ch17 (1) model-test
   table keys were NOT stripped because rule (a) names only five sources.
   Confirm whether the same rule should extend to them.
6. **ch2 two printings (§5):** no two-keyed-row pair was found; if the case
   exists under different ids, please supply them.
7. **p788 transfer (§7d):** id prefix still says ch16 while `chapter_id` says
   ch17. If downstream code groups by id prefix, it will mis-group this one
   row; renaming the id would break traceability to the chapter files, so the
   id was kept — confirm this trade-off is acceptable.
8. **ch8b p414-n16 (§5) and ch2 p30-n201 (§5):** both left exactly as workers
   left them (content conflict / math-vs-disc conflict) for parent decision;
   both rows carry `verified_visual` True alongside an unresolved flag — the
   tension is real and is not resolved by this merge.

## 12. Files written

- `math/questions_merged.json` — 3,720 rows, 16-field schema, 0 duplicate ids.
- `math/chunks_merged.json` — 52 prose chunks, byte-identical to `chunks.json`.
- `math/corrections-log-merged.json` — 1,222 entries, each with `source_file`.
- `math/flagged-merged.json` — 1,948 entries, 1,685 unique ids.
- `math/_complete/MERGE-REPORT.md` — this file.
- `math/_complete/_merge_2026-10-30.py` — the merge script (re-runnable).

## 13. What was NOT done (explicitly out of scope)

No DB import, no options extraction, no row deletion, no id renaming (except
no id was renamed at all), no new rows invented, no `depends_on` links
invented, no unverified table key left in any `answer_key`, no chunk text
changed, no file outside `math/` touched.
