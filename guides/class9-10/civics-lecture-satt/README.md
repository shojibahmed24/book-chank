# পৌরনীতি (Civics) — SSC Lecture Sheets chunking

- Subject: পৌরনীতি (slug: civics), class 9-10, book_id class9-10-civics-lecture
- Total rows: 5992
- By type: {'cq': 1036, 'gyanmulok': 304, 'lecture-note': 9, 'mcq': 4180, 'saq': 463}
- Rows with question_text: 5959; rows with answer_key: 2226; rows with guide_solution: 1080
- Flagged rows: 4183 (see flagged.json)
- Processed source files: 89; missing (manifest, not on disk): 0
- Schema: 37 fields per spec (see chunk-spec.md). id format:
  chapter rows `civics-lec-ch<NN>-<type>-<NNN>`; model-test
  `civics-lec-mt-<set>-<type>-<NNN>`; board
  `civics-lec-board-<year>-<board>-<type>-<NNN>`.
- Answers are never guessed: answer_key null + flag_note when the key
  is not printed in the source. MCQ options are positional (reading
  order -> ক,খ,গ,ঘ); Board Question.pdf options carry no labels in the
  decode, so unlabeled options are recovered only when unambiguous
  (4 single-word tokens, or the 4 standard 'নিচের কোনটি সঠিক?'
  combinations).
- Chapter Wise Practice/chapter-1..10: the PDF twins are image-based
  (0 rows: MCQ answer-grids only + CQ sections as images; 58-80
  distinct Bengali tokens per decode). The .doc twins are FULL TEXT
  and carry unique content (see Normalization 2026-11-25, Task 4):
  chapter notes + board/best-school MCQs with school tags and ●
  markers + 4 CQ sub-sections per chapter - ~1,751 numbered MCQ
  lines + ~141 CQ lines across the 10 chapters, mostly new vs the
  existing bank. NOT chunked in this pass; needs a dedicated
  chunking pass with column-split tooling (see report).
- Answer Sheet.pdf (Board Question folder) and the TP Answer Sheet are
  key sheets only (0 rows); the TP Answer Sheet supplies the board MCQ
  keys for SSC Civics TP (21-24) and the school keys for TP School
  Question. The Board Question.pdf Answer Sheet has numbers only (no
  letters), so Board Question.pdf MCQ rows have no answer_key.
- Civics-2023/2024/2025 (board compilations): MCQ answers parsed from
  each board's উত্তরমালা key lines; CQ answers chunked 2026-11-25
  from the উত্তরমালা in the reading-order text (215 of 219
  compilation CQ rows now carry guide_solution; the 4 still null are
  2023 Rajshahi Q350 - no such question exists - and 2025
  Rajshahi/Cumilla/Barishal Q11, whose answers the guide does not
  print: 'বি.দ্র. : ২০২৫ সালে প্রদত্ত পাঠ্যবই বহির্ভূত উদ্দীপক ও
  প্রশ্ন।').

## Normalization 2026-11-25

- Baseline (2026-11-24 chunking): 6,015 rows; flagged 3,906;
  processed 89 (88 PDF + 1 doc) + 86 doc duplicates + missing 0 =
  175 manifest. Pre-normalization copies in
  staging/ssc/civics/_backup_pre_norm/.
- After normalization: 5,992 rows; by type {'cq': 1036, 'gyanmulok':
  304, 'lecture-note': 9, 'mcq': 4180, 'saq': 463}; rows with
  question_text 5,959; with answer_key 2,226; with guide_solution
  1,080 (cq 395, saq 372, gyanmulok 304, lecture-note 9); flagged
  4,183. Processed/missing unchanged (89/0); no doc twin was chunked
  in this pass, so processed stays 89.
- Task 1 — mis-attributed TP papers (SSC Civics TP (21-24).pdf):
  root cause: in the column-split reading order each board paper's
  header line falls ~10 questions INTO its own paper, so the
  chunker's header→header spans systematically held paper P's Q11-30
  + paper P+1's Q1-10; the 4 named papers (Sylhet 2023, Barishal
  2022, Dinajpur 2023, Mymensingh 2021) plus a 5th (Cumilla 2021)
  failed header-start detection entirely. Fix: re-parsed the 36
  Q1-delimited segments with the chunker's own parse_mcq and matched
  old→fresh (strict stem+options, then stem+qnum, then stem-only
  unique). 1,063 rows updated (board changed 433, answer_key changed
  160, id changed 503); 10 rows ADDED (Dhaka 2024 Q1-10, never
  chunked before); 44 rows DELETED (verified section-B reprint
  duplicates of section-A Dinajpur/Mymensingh 2021 Q1-30, renumbered
  31-60; log in work/civics/tp_mcq_changes.json); 21 rows had
  board/year cleared to None + flagged (CQ-run fragments mis-parsed
  as MCQ, retained per no-delete rule); 9 reprint rows kept
  unverified + flagged (no conclusive twin: best token Jaccard
  0.57). TP MCQ per paper now: all 2022/2023/2024 papers exactly 30;
  2021: Cumilla 30, Chattogram 27, Dhaka 29, Dinajpur 40 (31 real +
  9 kept-unverified reprints), Barishal 31, Mymensingh 27, Jashore
  30, Rajshahi 29, Sylhet 29; plus 21 board-None fragment rows. TP
  CQ rows (342) were NOT re-attributed: 43 CQ heads vs 36 expected
  board-years, headers mid-paper, overlapping blocks, Mymensingh
  headers missing - proof not conclusive, so all stay board_name
  None + flagged.
- Task 2 — MCQ2 short models: 11 questions recovered (NOT 13 - the
  original '13 missing' count was an arithmetic error; live counts
  are model-3 29, model-4 28, model-6 28, model-7 29, model-8 29,
  model-9 29, model-10 27 = 11 missing, 1+2+2+1+1+1+3). Cause: each
  missing question's number marker sits ALONE on its own
  reading-order line, which the chunker's NUM_START regex (needs
  trailing whitespace) never matched. Recovered: model-3 Q7 (key গ),
  model-4 Q12 (খ), Q16 (খ), model-6 Q15 (ক), Q26 (ঘ), model-7 Q24
  (ক), model-8 Q5 (ক), model-9 Q14 (ঘ), model-10 Q9 (ঘ), Q21 (ঘ),
  Q28 (ক). Keys: the ● marker (U+F050) TRAILS the correct option
  inline - the chunker's own parse_mcq2 convention; doc twins
  corroborate 3 (model-3 Q7, model-7 Q24, model-9 Q14) and
  contradict none. All 10 MCQ2 models now have exactly 30 rows. The
  11 following rows' stale 'numbering gap' flags were cleaned.
  Transcription fix (same pass): the 11 new rows were first typed
  with the y-trap spelling (য U+09AF + ় U+09BC instead of য়
  U+09DF) in 8 rows / 15 places ('কোথায়', 'হয়', 'ময়দানে',
  'জাতীয়তাবাদ' etc.); corrected to the reading-order spelling -
  the MCQ2 reading-order files contain 0 trap occurrences and 38-60
  correct-য় occurrences each - and flagged per row. Data-field
  trap count is now 0; the remaining trap-sequence hits in
  flag_note are documentation quotes (notes describing the trap and
  quoting old values), not data errors.
- Task 3 — compilation CQ answers: 215 of 219 filled from the
  Civics-2023/2024/2025 উত্তরমালা in the reading-order text (9 boards
  x 11 answers per year; assignment by block position, verified by
  content match with each question's parts). Part labels in the decode
  are the single letters h/i/j/k (legacy font) and were normalised to
  ক./খ./গ./ঘ.; labels occasionally land mid-sentence when the
  reading order splits them onto their own line (decode-order
  artifact, content complete). Two markers are misdecoded in the
  source (Jashore 2023 block 8 reads '৩নং', Sylhet 2023 block 1 reads
  '৪নং') - assigned by position and flagged. Still null (4): 2023
  Rajshahi Q350 (no such question); 2025 Rajshahi/Cumilla/Barishal
  Q11 (guide prints no answer - out-of-textbook note).
- Task 4 — doc-twin check (87 skipped docs; similarity = Bengali
  token containment + Jaccard + line-hit vs the PDF twin decode;
  soffice --headless --convert-to pdf + shared decoder):
  53 DUPLICATE (incl. all 1. CQ, 2. SAQ, 4. Gyanmulok, #SSC-2027,
  5. Model Test/MCQ2 models 1-10, Test Paper Old Model/School
  Question docs; the 2 Answer Sheet docs were upgraded from
  LIKELY_DUPLICATE after their doc-unique lines proved to be
  answer-key letter runs only, e.g. '1 M 2 K 3 K ...' - no question
  text, key-only subset of the PDF key sheet, 0 rows either way);
  1 NO_PDF_TWIN - Chapter Wise Practice/Z (Archived).doc (the
  processed doc; its 9 lecture-note rows already exist, no PDF
  twin); 10 NEEDS_REVIEW - Chapter Wise Practice/chapter-1..10.doc:
  UNIQUE CONTENT, not chunked in this pass (see below); 23
  CONVERT_FAILED - retry in progress at report time (pid 30869,
  started 2026-11-24 ~20:00, one file at a time with a dedicated
  LibreOffice profile; on file 1/23, 6. Board Question
  2023-25/Civics-2025.docx; the 23 are 9x 5. Model Test/MCQ
  chapter-1..9.docx, 10x 5. Model Test/CQ chapter-1..10.docx,
  Civics-2025.docx, Board Question.doc, School Question.doc and
  MCQ2/model-5.doc - all expected DUPLICATE by their siblings'
  verdicts, but unverified until the retry finishes; log
  work/civics/doc_twin_retry.log, verdicts
  work/civics/doc_twins.json).
  CWP finding (the 10 unique docs): the PDF twins are image-based
  (58-80 distinct Bengali tokens, 0 rows) while the .docs are full
  text - chapter notes first, then 'বোর্ড ও সেরা স্কুলের
  বহুনির্বাচনি প্রশ্নোত্তর' (board + best-school MCQs with school
  tags like [ম. বো. '১৬] and ● markers), 'সাধারণ বহুনির্বাচনি
  প্রশ্নোত্তর', then 4 CQ sub-sections ('বোর্ড ও সেরা স্কুলের
  সৃজনশীল', 'মাস্টার ট্রেইনার প্রণীত সৃজনশীল', 'অনুশীলনমূলক
  কাজের আলোকে সৃজনশীল', 'অনুশীলনের জন্য সৃজনশীল'). Numbered
  question lines per chapter (raw doc decode): ch1 155, ch2 167,
  ch3 123, ch4 250, ch5 143, ch6 191, ch7 145, ch8 274, ch9 243,
  ch10 201 = 1,892 total (1,751 in MCQ regions, 141 in CQ regions;
  the CQ count is a lower bound - CQ numbers often sit mid-line).
  Overlap sample (ch1, first 40 MCQ stems): 3 exact + 9 near
  matches vs existing rows (~7.5% exact) - most appear new.
  Estimated scale ~1,500-1,750 MCQs + ~150-400 CQs, i.e.
  ~1,700-2,000 new rows. NOT chunked here: the raw decode is
  2-column-interleaved and unusable for direct chunking, and the
  _cols column-split tooling is not in the repo - a dedicated CWP
  chunking pass (build a column splitter, then reuse the chunker's
  parse functions) is the recommended next task.
- Task 5 — য+়/য় trap: the trap sequence (য U+09AF + ় U+09BC)
  appeared in chapter_name only (204 rows, 2 names): ch08
  'বাংলাদেশের স্থানীয় সরকারব্যবস্থা' (99 rows) and ch09 'নাগরিক
  সমস্যা ও আমাদের করণীয়' (105 rows) - both corrected to য়
  (U+09DF) + flagged. board_name itself was clean (0 rows with the
  trap); ময়মনসিংহ in board_name already used correct য়. The trap's
  real damage was in the chunker: BOARD_FIX line 44 held a duplicated
  য+় key pair and BOARD_SLUG's only Mymensingh key was য+়, so the
  reading-order header 'ময়মনসিংহ' (correct য়) missed the lookup and
  164 rows got id slug 'unknown' (all verified board_name ==
  ময়মনসিংহ). Fixed: chunker canonicalised to য় (U+09DF) with the
  য+় spelling kept as an alias key; all 164 ids renamed
  '-unknown-' -> '-mymensingh-' + flagged (no collisions). 5 trap
  occurrences remain in the chunker only as comments/docstrings
  ('অধ্যায়ের', 'শীর্ষস্থানীয়') - no functional effect.
- Placeholders: 7 rows matched the triple-empty screen at baseline;
  0 deleted. 5 carry the full question as marks_parts text; the 2
  dhaka-2024 -2 rows gained a guide_solution from Task 3 and are no
  longer triple-empty. All 7 retained + flagged; see
  staging/ssc/civics/dropped-placeholders.json.
- Remaining limits: TP CQ board attribution unresolved (see Task 1);
  2021 TP papers' column interleave still leaves some mangled
  stems/options (flagged, never guessed); 9 Dinajpur-2021 reprint
  rows kept unverified; 4 comp CQ answers still null (see Task 3);
  the 2024 compilation chunked CQ for only 3 boards (Dhaka q1-4
  dup, Cumilla q11, Dinajpur q1-11) - the other 2024 boards' CQ
  rows were never chunked as compilations (their questions live in
  the Board Question.pdf rows instead); CWP docs not chunked (see
  Task 4); doc-twin retry for 23 files still running at report
  time.
- Validation (2026-11-25): 101 JSON files in staging/ssc/civics,
  all parse; combined 5,992 = chapter-files 4,410 + model-test-files
  1,582; ids unique, none null; all rows 37 fields; processed 89 +
  missing 0 + doc dupes 86 = 175 manifest; flagged.json 4,183 ⊆
  combined and equals rows with non-empty flag_note; per-file ids ==
  combined ids (multiset). Spot-checks (3 decoded files read):
  ch10-cq-001 question_text + guide_solution present in
  decoded/ssc/civics/1. CQ/chapter-10.uni.txt; recovered
  mcq2-model-7-mcq-024 stem + option 'ব্যক্তিত্ব' present in
  decoded/ssc/civics/5. Model Test/MCQ2/model-7.uni.txt;
  comp-2025-dhaka-cq-001 guide_solution verified against the
  Civics-2025 reading-order text (part-ক phrase 'রাষ্ট্রের সর্বোচ্চ
  ক্ষমতা হলো সার্বভৌমত্ব' present; exact-substring check failed
  only on embedded control chars e.g. U+202A in the decode).
