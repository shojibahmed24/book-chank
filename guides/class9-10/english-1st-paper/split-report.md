# English 1st Paper — Split + Chunk Report (Talimit Class 9–10, Yes Sir AI)

Date: 2026-10-30. Source: `english/english-1st.pdf` (736 pages, CamScanner
image-only scan) + `_work/ocr/english/` (736/736 non-empty page texts, 5.5 MB,
150dpi ben+eng). Worker: `_work/split_english.py` (re-runnable; overwrites
outputs each run). File stage only: no DB import, no options extraction.

## Outputs (all under `english/`)

- `questions.json` — 2934 rows, 16-field Math schema, 0 duplicate IDs,
  0 empty question_text.
- `chunks.json` — 76 prose chunks.
- `corrections-log.json` — 6 page-status entries (re-reviews; 0 question-text
  corrections).
- `flagged.json` — 357 flagged items (see below).
- This report. STATUS.md English row updated to DONE with these counts.

## Book map (verified from TOC + OCR)

- pp1–12: front matter, syllabus, TOC, abbreviations list.
- pp13–390: Paper-I units/lessons + Model Tests 01–43 (interleaved lesson
  texts, lesson practice sets, model tests, answer sheets).
- p391: Supplementary Reading divider.
- pp392–426: Special Unseen Passages 01–30 (Q4 table + Q5 summary each).
- pp427–441: supplementary matching / rearranging sets (questions).
- pp442–480: poem appreciation (7 sets) + story appreciation (10 sets).
  (An earlier scan misread "Answer the questions…" headers as answer pages;
  these pages are questions.)
- p481: Writing Test divider. pp482–570: writing items (story, dialogue,
  graphs/charts, letters/e-mail/application, paragraphs, compositions).
- p571: Special Model Tests divider.
- pp572–603: Special Model Tests Paper-I — 14 tests (questions).
- pp604–620: "Key to Special Model Tests [Paper-I]" (answers, grouped).
- pp621–700: Special Model Tests Paper-II — 55 tests (questions).
- pp701–736: "Key to Special Model Tests [Paper-II]" (answers, grouped).
- Printed page number equals PDF page number throughout (verified from
  running heads); `guide_printed_page` is the PDF page string.
- Test-group detection (final): 110 groups = 41 main + 14 special1 + 55
  special2. Two main Model Tests (TOC: 43) still have no detected Part-A
  header (OCR garbling); their question blocks were still captured, only
  group attribution is affected. One special2 test starting p650 has a
  fully garbled Part-A header and sits in the previous test's span.

## Row counts by type (2934 total)

| type | rows | type | rows |
|---|---|---|---|
| short | 449 | writing_dialogue | 100 |
| mcq | 551 | writing_letter | 106 |
| gapfill | 45 | writing_paragraph | 112 |
| matching | 53 | writing_graph | 1 |
| summary | 77 | writing_composition | 94 |
| table | 124 | writing_story | 76 |
| poem_q | 323 | grammar_gapbox | 53 |
| rearrange | 45 | grammar_suffix | 56 |
| story_q | 300 | grammar_tag | 53 |
| | | grammar_transform | 50 |
| | | grammar_verbs | 52 |
| | | grammar_connector | 56 |
| | | grammar_preposition | 52 |
| | | grammar_punctuation | 55 |
| | | grammar_table | 51 |

Display policy: verbatim 2368 (mcq/short/grammar/gapfill/table/matching/
rearrange), ai_rewrite 566 (summary + all writing_* — question prompt as
reference, guide model text as HIDDEN grounding only, never displayed text).
`verified_visual` is "False" everywhere (OCR-derived only, as with Math's
initial state).

## MCQ keys, answers, links (fail-safe exact-match only)

- MCQ: 551 rows — keyed 87 (73 Paper-I answer sheets + 14 special1),
  unkeyed 464. Keys link ONLY on exact size match between an answer group
  and question set(s) in scope; on any mismatch the group is left unlinked
  and flagged, never guessed.
- Guide-error MCQs: none separately identified. No key was auto-scored as
  a guide error; unkeyed means "key not provably linked" (answer group
  size mismatch, or the question set itself incomplete — see below), NOT
  "key known wrong".
- Short / poem / story answers: 60 of 1072 rows carry a guide_solution
  (47 Paper-I + 13 special1). Story answers 0 linked in Paper-I: guide
  answer lists do not match question-set sizes (selective printing,
  merged lists).
- Whole-Q / grammar answers: 139 of 822 rows (126 Paper-I + 13 special1).
- `depends_on` set on 294 rows (test-group seen/unseen passage links).
  No adjacent/previous chunk was ever used as a fallback link.
- Special2 answers: NOT linked (fail-safe skip). Answer blocks detected:
  59 vs 55 tests; the excess comes from false Q1 splits (abbreviated
  answer fragments and "1.0)"-style misreads splitting one test's answers
  in two). Order-linking would misassign every later test, so nothing
  links for special2 and the mismatch is flagged. Principled follow-up:
  gapbox-word anchoring (match a block's Q1 answer words against each
  test's Q1 box words) instead of order.

## Why link rates are low (honest causes, not bugs)

1. Question sets incomplete: S1 Q1 sets typically yield 3–6 of 7 items
   because option markers are OCR-mangled (e.g. numeric options
   "i. 200 ii. 250" read as "1.200 2250", "(e)" read as "(€)",
   "ii." read as "Ai-"). The splitter rejects segments with <3 provable
   option markers rather than emitting broken items. Only complete
   7-item sets can take 7-key groups.
2. Guide answer lists are selective/merged (e.g. 15 answers vs 5+5+5
   sets), so exact-sum linking fails often by design.
3. Seen-passage phrase detection is weak for main tests (only 2 of 41
   main seen passages found by phrase; special1: 13 of 14). Passage
   chunks therefore under-cover `depends_on` for main-test mcq/short
   rows. Follow-up: span-based seen extraction (test Part-A start →
   first Q1 block) would raise this substantially.

## Chunks (76)

- Seen passages: 15 (2 main + 13 special1).
- Unseen passages: 33 (main tests, Q4/Q5 phrase-detected).
- Special unseen passages: 28 (of 30; passages 12, 15 unrecovered —
  header repeats / translation-marker cuts).
- Lesson-text chunks were NOT built (lesson rows have `depends_on` NULL
  unless a test-group link applies) — recorded limitation, not invention.

## Re-review (200dpi re-read, pdftoppm + tesseract ben+eng)

Re-reviewed 6 pages, all confirmed NON-question pages, so their low 150dpi
char counts are explained, not missing OCR. Zero question-text corrections
resulted; zero still-flagged from this set:

- p0001: book cover. p0011: Part-A Reading Test divider (150dpi 199 chars).
- p0012: abbreviations list (synonym/antonym/…). p0391: Supplementary
  Reading divider. p0481: Writing Test divider. p0571: Special Model Tests
  divider (150dpi 190 chars).
- Renders kept in `_work/rereview-english/`; entries in
  `corrections-log.json`.
- Formula pages: none in this book (English); no 300dpi re-reads needed.

## Flagged (357, in `flagged.json`)

| kind | n | meaning |
|---|---|---|
| mcq_few_options | 142 | MCQ segment with <3 provable option markers; not emitted |
| short_no_question_mark | 75 | short segment without "?" or question-word start; not emitted |
| key_group_mismatch | 32 | MCQ key group matches no exact set-size sum in scope |
| answer_group_mismatch | 31 | short-answer group matches no exact set-size sum |
| special_link_mismatch | 29 | special1/2 group matches no exact set-size sum in its test span |
| writing_no_ans | 18 | writing item with no `Ans.` block found (emitted, solution empty) |
| q11_unclassified | 17 | numbered Q11 prompt not classifiable by keywords |
| unseen_link_unverified | 12 | special-unseen table row without shared-keyword passage link |
| special_block_count_mismatch | 1 | special2: 59 blocks vs 55 tests — linking skipped |

## Known limitations / follow-ups (not done, not hidden)

1. Special2 answer linking skipped (see above); gapbox-word anchoring is
   the proposed fix.
2. Supplementary sets largely unextracted (pp427–480): only 1 row vs an
   estimated 55–70 units — matching sets (≥7), rearranging sets (≥31),
   poem sets (7), story sets (10). Cause: sets are numbered without the
   per-set headers the main parser keys on, and poem/story headers use
   "Answer the questions from the following poem/story" phrasing.
   Follow-up: a numbered-set splitter + those two header patterns +
   matching-key linking.
3. Main seen-passage coverage 2/41 (phrase detection); span-based seen
   extraction proposed.
4. Two main Model Tests lack detected Part-A headers (TOC 43 vs 41
   groups); one special2 test (p650) lacks one entirely. Question blocks
   exist; only group attribution is off.
5. S1 Q1 sets incomplete from option-marker OCR mangling (see above);
   a targeted 200dpi re-read of incomplete Q1 blocks is the path to a
   higher keyed rate. This was NOT done in this pass (re-reads covered
   only the low-char pages).
6. Graphs/charts: only 1 writing_graph row; no graphs/charts subsection
   heading was found in the writing range (only incidental matches inside
   "paragraph"/"graphic"/"photographs"). If this edition has no separate
   graphs section, 0–1 rows is correct — verify against the TOC.
7. `verified_visual` False everywhere: a visual verification pass (as
   with Math) is still the path to higher key/answer coverage.

## Method notes (for the next worker)

- Stream parser over `[[PAGE n]]`-marked OCR text; headers are
  whitespace-flexible; Part-A separator OCR varies (`:`, `2`, `.`, `'`,
  `:-`, `»`) — the pattern must not force a literal colon, and must not
  use `\W` for the separator (a digit `2` is a word char).
- Special answers are GROUPED sections (p604+, p701+), not interleaved:
  never treat special-range Part-A headers or Q lists as questions.
- Q1 answer-list block starts require a Part-A header within the previous
  1200 chars (Q7 preposition lists with `7.` misread as `1.` mimic Q1
  starts mid-text; Bengali-digit openers need a closing bracket or they
  false-match `1.১`-style fragments).
- Lettered splitting labels items SEQUENTIALLY (OCR letter values are
  unreliable: (a)→(9), (b)→(6)/(4)/(8), (c)→(©), (e)→(g)/(¢)/(€)).
- Linking is fail-safe exact-sum scoped linking everywhere; the old
  nearest-rows heuristic was removed because it risked misalignment.
- Special1 links ARE order-paired (14 blocks == 14 tests) and spot-check
  clean (keys match their option lists); special2 is not linked because
  its counts do not match.
