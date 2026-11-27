# উচ্চতর গণিত — Lecture Sheet চাংক

মোট row: **9327** (chapter: 5911, model-test: 3416)
flag করা row: 7701

## ID সংশোধন (2026-11-24 — ফাইনাল পাসের আগে)

প্রথম পাসে model-test id-তে ত্রুটি ছিল: চাংকারের per-run কাউন্টার (kind, chapter, set_id)-এ 001 থেকে শুরু হতো, আর set_id ছিল শুধু কালেকশনের ফোল্ডার (collection1–4) — ফলে ৪টি কালেকশনের ৭৬টি সোর্স ফাইলের row একই id পেয়েছিল (১৩৪টি duplicate id, ৮৬৮টি অতিরিক্ত row)। ঠিক করা হয়েছে: প্রত্যেক সোর্স ফাইলের নিজের set_id (যেমন collection1-mcq-q01, collection1-mcq-ans-q01, collection2-cq-q01, collection3-cq-q1-1, collection4-mcq-q5-2-20), id প্রতি (নতুন set, kind)-এ 001 থেকে ক্রমিক; model-test ফাইল এখন সেট-প্রতি আলাদা (১০ → ৮২টি)। মোট row আগের মতোই ৯,৩২৭; শুধু id/set_id বদলেছে, প্রশ্ন/উত্তর/flag কিছুই বদলায়নি। স্ক্রিপ্ট: `_fix_mt_ids.py`; আগের ফাইলের ব্যাকআপ: `_backup_pre_id_fix/`।

## type ভাগ

- board: 2154
- cq: 2006
- handnote: 66
- lecture-note: 74
- mcq: 1249
- model-test: 3416
- saq: 362

## chapter ফাইল

- chapter-00-board.json: 2154
- chapter-00-mcq.json: 48
- chapter-00-saq.json: 362
- chapter-01-cq.json: 112
- chapter-01-handnote.json: 4
- chapter-01-lecture-note.json: 6
- chapter-01-mcq.json: 113
- chapter-02-cq.json: 220
- chapter-02-handnote.json: 5
- chapter-02-lecture-note.json: 5
- chapter-02-mcq.json: 78
- chapter-03-cq.json: 117
- chapter-03-handnote.json: 4
- chapter-03-lecture-note.json: 4
- chapter-03-mcq.json: 87
- chapter-04-cq.json: 53
- chapter-04-handnote.json: 3
- chapter-04-lecture-note.json: 4
- chapter-04-mcq.json: 143
- chapter-05-cq.json: 139
- chapter-05-handnote.json: 12
- chapter-05-lecture-note.json: 5
- chapter-05-mcq.json: 196
- chapter-06-cq.json: 48
- chapter-06-handnote.json: 5
- chapter-06-lecture-note.json: 5
- chapter-06-mcq.json: 92
- chapter-07-cq.json: 89
- chapter-07-handnote.json: 2
- chapter-07-lecture-note.json: 4
- chapter-07-mcq.json: 60
- chapter-08-cq.json: 199
- chapter-08-handnote.json: 4
- chapter-08-lecture-note.json: 8
- chapter-08-mcq.json: 54
- chapter-09-cq.json: 184
- chapter-09-handnote.json: 7
- chapter-09-lecture-note.json: 7
- chapter-09-mcq.json: 37
- chapter-10-cq.json: 177
- chapter-10-handnote.json: 4
- chapter-10-lecture-note.json: 5
- chapter-10-mcq.json: 36
- chapter-11-cq.json: 125
- chapter-11-handnote.json: 7
- chapter-11-lecture-note.json: 7
- chapter-11-mcq.json: 143
- chapter-12-cq.json: 161
- chapter-12-handnote.json: 4
- chapter-12-lecture-note.json: 5
- chapter-12-mcq.json: 57
- chapter-13-cq.json: 171
- chapter-13-handnote.json: 3
- chapter-13-lecture-note.json: 5
- chapter-13-mcq.json: 70
- chapter-14-cq.json: 211
- chapter-14-handnote.json: 2
- chapter-14-lecture-note.json: 4
- chapter-14-mcq.json: 35

## model-test ফাইল (৮২টি — ID সংশোধনের পর, 2026-11-24)

- collection1-mcq-ans-q01-model-test.json: 30
- collection1-mcq-ans-q02-model-test.json: 30
- collection1-mcq-ans-q03-model-test.json: 30
- collection1-mcq-ans-q04-model-test.json: 55
- collection1-mcq-ans-q05-model-test.json: 30
- collection1-mcq-ans-q06-model-test.json: 23
- collection1-mcq-ans-q07-model-test.json: 30
- collection1-mcq-ans-q08-model-test.json: 30
- collection1-mcq-ans-q09-model-test.json: 30
- collection1-mcq-ans-q10-model-test.json: 30
- collection1-mcq-ans-q11-model-test.json: 30
- collection1-mcq-ans-q12-model-test.json: 29
- collection1-mcq-ans-q13-model-test.json: 30
- collection1-mcq-ans-q14-model-test.json: 30
- collection1-mcq-q01-model-test.json: 22
- collection1-mcq-q03-model-test.json: 28
- collection1-mcq-q04-model-test.json: 22
- collection1-mcq-q05-model-test.json: 25
- collection1-mcq-q06-model-test.json: 21
- collection1-mcq-q07-model-test.json: 1
- collection1-mcq-q08-model-test.json: 2
- collection1-mcq-q09-model-test.json: 2
- collection1-mcq-q10-model-test.json: 2
- collection1-mcq-q12-model-test.json: 14
- collection1-mcq-q13-model-test.json: 25
- collection1-mcq-q14-model-test.json: 1
- collection2-cq-ans-q01-model-test.json: 6
- collection2-cq-ans-q02-model-test.json: 6
- collection2-cq-ans-q03-model-test.json: 5
- collection2-cq-ans-q04-model-test.json: 1
- collection2-cq-ans-q05-model-test.json: 4
- collection2-cq-ans-q06-model-test.json: 5
- collection2-cq-ans-q07-model-test.json: 5
- collection2-cq-ans-q08-model-test.json: 3
- collection2-cq-ans-q09-model-test.json: 5
- collection2-cq-ans-q10-model-test.json: 5
- collection2-cq-ans-q11-model-test.json: 5
- collection2-cq-ans-q12-model-test.json: 5
- collection2-cq-ans-q13-model-test.json: 5
- collection2-cq-ans-q14-model-test.json: 6
- collection2-cq-q01-model-test.json: 1
- collection2-cq-q02-model-test.json: 3
- collection2-cq-q03-model-test.json: 1
- collection2-cq-q06-model-test.json: 3
- collection2-cq-q07-model-test.json: 1
- collection2-cq-q08-model-test.json: 1
- collection2-cq-q09-model-test.json: 3
- collection2-cq-q11-model-test.json: 2
- collection2-cq-q12-model-test.json: 1
- collection3-cq-q02-model-test.json: 3
- collection3-cq-q07-model-test.json: 3
- collection3-cq-q1-1-model-test.json: 3
- collection3-cq-q1-2-model-test.json: 3
- collection3-cq-q10-2-model-test.json: 3
- collection3-cq-q11-1-model-test.json: 3
- collection3-cq-q11-3-model-test.json: 3
- collection3-cq-q11-4-model-test.json: 2
- collection3-cq-q5-1-model-test.json: 3
- collection3-cq-q5-3-model-test.json: 3
- collection3-cq-q5-7-model-test.json: 3
- collection3-cq-q8-1-model-test.json: 3
- collection3-cq-q8-2-model-test.json: 3
- collection3-cq-q9-2-model-test.json: 3
- collection4-mcq-q02-model-test.json: 11
- collection4-mcq-q07-model-test.json: 26
- collection4-mcq-q1-1-model-test.json: 31
- collection4-mcq-q1-2-model-test.json: 27
- collection4-mcq-q11-1-model-test.json: 15
- collection4-mcq-q11-3-model-test.json: 32
- collection4-mcq-q12-model-test.json: 15
- collection4-mcq-q13-model-test.json: 33
- collection4-mcq-q3-1-model-test.json: 27
- collection4-mcq-q5-1-model-test.json: 29
- collection4-mcq-q5-2-20-model-test.json: 18
- collection4-mcq-q5-3-model-test.json: 22
- collection4-mcq-q6-1-model-test.json: 26
- test-paper-15-22-model-test.json: 201
- test-paper-18-23-model-test.json: 1377
- test-paper-bq-cq-21-24-model-test.json: 8
- test-paper-bq-mcq-21-24-model-test.json: 760
- test-paper-school-cq-model-test.json: 8
- test-paper-school-mcq-model-test.json: 25

## ফাইল নোট

- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-1.pdf` — stem অপ্রাপ্য (CID, 0/6 readable) — উত্তরপত্র ফাইলে একই প্রশ্ন আছে; fragmented rows বাদ দেওয়া হয়েছে
- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-10.pdf` — stem অপ্রাপ্য (CID, 0/4 readable) — উত্তরপত্র ফাইলে একই প্রশ্ন আছে; fragmented rows বাদ দেওয়া হয়েছে
- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-11.pdf` — stem অপ্রাপ্য (CID, 1/9 readable) — উত্তরপত্র ফাইলে একই প্রশ্ন আছে; fragmented rows বাদ দেওয়া হয়েছে
- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-12.pdf` — parse issue: no-mcq-numbers
- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-13.pdf` — stem অপ্রাপ্য (CID, 0/2 readable) — উত্তরপত্র ফাইলে একই প্রশ্ন আছে; fragmented rows বাদ দেওয়া হয়েছে
- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-14.pdf` — stem অপ্রাপ্য (CID, 0/4 readable) — উত্তরপত্র ফাইলে একই প্রশ্ন আছে; fragmented rows বাদ দেওয়া হয়েছে
- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-2.pdf` — stem অপ্রাপ্য (CID, 0/4 readable) — উত্তরপত্র ফাইলে একই প্রশ্ন আছে; fragmented rows বাদ দেওয়া হয়েছে
- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-3.pdf` — stem অপ্রাপ্য (CID, 0/2 readable) — উত্তরপত্র ফাইলে একই প্রশ্ন আছে; fragmented rows বাদ দেওয়া হয়েছে
- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-5.pdf` — stem অপ্রাপ্য (CID, 0/12 readable) — উত্তরপত্র ফাইলে একই প্রশ্ন আছে; fragmented rows বাদ দেওয়া হয়েছে
- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-6.pdf` — stem অপ্রাপ্য (CID, 0/7 readable) — উত্তরপত্র ফাইলে একই প্রশ্ন আছে; fragmented rows বাদ দেওয়া হয়েছে
- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-8.pdf` — stem অপ্রাপ্য (CID, 0/2 readable) — উত্তরপত্র ফাইলে একই প্রশ্ন আছে; fragmented rows বাদ দেওয়া হয়েছে
- `#TYPEWISE/CHAPTERWISE & TYPEWISE MCQ PRACTICE & SUGGESTION/H.Math-MCQ-9.pdf` — stem অপ্রাপ্য (CID, 0/5 readable) — উত্তরপত্র ফাইলে একই প্রশ্ন আছে; fragmented rows বাদ দেওয়া হয়েছে
- `#TYPEWISE/MODEL TYPEWISE & CHAPTERWISE CQ/10.pdf` — parse issue: no-cq-markers-or-numbers
- `#TYPEWISE/MODEL TYPEWISE & CHAPTERWISE CQ/13.pdf` — parse issue: no-cq-markers-or-numbers
- `#TYPEWISE/MODEL TYPEWISE & CHAPTERWISE CQ/14.pdf` — parse issue: no-cq-markers-or-numbers
- `#TYPEWISE/MODEL TYPEWISE & CHAPTERWISE CQ/4.pdf` — parse issue: no-cq-markers-or-numbers
- `#TYPEWISE/MODEL TYPEWISE & CHAPTERWISE CQ/5.pdf` — parse issue: no-cq-markers-or-numbers
- `Chapterwise MCQ1 Sheet/12TH.pdf` — parse issue: no-mcq-numbers
- `Model Test/Collection2 Chapterwise CQ model/10.pdf` — parse issue: no-cq-markers
- `Model Test/Collection2 Chapterwise CQ model/13.pdf` — parse issue: no-cq-markers
- `Model Test/Collection2 Chapterwise CQ model/14.pdf` — parse issue: no-cq-markers
- `Model Test/Collection2 Chapterwise CQ model/4.pdf` — parse issue: no-cq-markers
- `Model Test/Collection2 Chapterwise CQ model/5.pdf` — parse issue: no-cq-markers
- `Test paper/05. High Math (MCQ Ans).doc.pdf` — parse issue: no-mcq-numbers

## Normalization (2026-11-24/25 — ফাইনাল পাস)

মোট row আগে/পরে: **৯,৩২৭ → ৯,৩২৭** (কোনো row ডিলিট হয়নি)। flag row আগে/পরে:
**৭,৭০১ → ৭,৭০১**। স্কিমা: সব row ঠিক ৩৭ ফিল্ড (validate.py PASS)।
ব্যাকআপ: `_backup_pre_norm/` (আসল pre-norm অবস্থা — যাচাই করা: chapter_name-এ
৫৫৬টি trap, বর্তমান ফাইলে ০) ও `_backup_pre_trapsweep/` (trap-sweep-এর আগের অবস্থা)।

### য+়/য় trap — full-field sweep (পাস ২)

- ডিকোড করা টেক্সটে (৩২৪টি .uni.txt) GOOD য় ৪৩,৯৮৩টি বনাম BAD য+় মাত্র ২টি —
  ডিকোডার GOOD দেয়; JSON-এর BAD চাংকিং পাইপলাইন থেকে এসেছে। পাস ১ শুধু
  chapter_name ঠিক করেছিল (২৭৮ row); পাস ২-তে বাকি সব ফিল্ড sweep করা হয়েছে:
  **৫,৯২৬ row-তে ৮,৪৫২টি বদল** — flag_note ৭,৮৯৪ / chapter ৫৫৬ / guide_solution ২।
  question_text / options / stimulus / board_name-এ trap ছিল ০।
- chapter ফিল্ডে ২৭৮টি ch09 row-র লেবেল trap-সহ ছিল, অথচ chapter_name তখনই
  canonical ছিল — sweep-এর পর ২৭৮টি row-তেই chapter == chapter_name।
- ২টি guide_solution row (ch12-handnote-002 "হয়", ch03-handnote-002 "নির্ণয়")-র
  BAD ডিকোড-সোর্সেও একই জায়গায় আছে — দুটোই নিঃসন্দেহে য়; JSON ঠিক করা হয়েছে,
  ডিকোড-ফাইল ছোঁয়া হয়নি। স্ক্রিপ্ট: `work/higher-math/normalize_trap_sweep.py`
  (শুধু \u escape ব্যবহার করে — ফাইলে একটিও raw য় নেই); লগ:
  `work/higher-math/trap-sweep-log.json`। sweep-এর পর সব ১৪৩ ফাইলে BAD ০।
- সিদ্ধান্ত: canonicalization লগ করা হয়েছে, flag_note-এ marker যোগ করা হয়নি —
  তাই flagged সেট অপরিবর্তিত (৭,৭০১)।

### Doc-twin যাচাই (২৯১টি skip করা .doc/.docx)

- পদ্ধতি: soffice → PDF → shared decode-pdf.py → twin PDF-র decoded টেক্সটের সাথে
  token containment; ≥0.60 = DUPLICATE। ফল: **২৮৯ DUPLICATE** (containment
  ০.৫৮৬–১.০০), ২টি NO-DOC-DECODE (নিচে)।
- Twin PDF ০ row দিয়েছে এমন ৩৬টি doc-এর extra coverage যাচাই: combined-এর সাথে
  distinctive-token coverage **০.৭৭–১.০০** — সবগুলোর কনটেন্ট combined-এ আছে।
- ২টি বাকি ছিল — ১টি শেষ: Board Question 23-25/HM-2025.docx single-file
  soffice convert + shared decode → twin HM-2025.pdf-র সাথে containment
  **০.৯১২**, jaccard ০.৭৯৬ → **DUPLICATE** (twin PDF থেকে ২৬৬ row আছেই;
  unique content নেই, chunk লাগেনি)। ১টি **UNVERIFIED**: Test paper/Higher Math
  15-22.doc (১৬ MB) — ৩টি soffice চেষ্টা ব্যর্থ (whole-dir batch 1500 s timeout;
  single-file 3300 s — export মেসেজের পরেও PDF ডিস্কে আসেনি; 7200 s চেষ্টা
  VM restart-এ ~৩৭ মিনিটে মারা গেছে; আরেকটি 7200 s চেষ্টা ১২০ মিনিটে timeout,
  ৫৬:০৪ CPU, তবু PDF নেই)। twin PDF থেকে ২০১ row আছেই — কভারেজের ভিত্তি
  দাঁড়িয়ে আছে; doc-টি "unpushed unique content: UNVERIFIED" হিসেবে তালিকাভুক্ত
  (duplicate প্রমাণিত নয়, unique-ও প্রমাণিত নয়)। শান্ত মেশিনে বা অন্য
  কনভার্টারে আবার চেষ্টা করা যেতে পারে।
- স্ক্রিপ্ট: `work/higher-math/doc-twin/` (`doc_twin_resume.py`,
  `doc_twin_resume_rev.py`, `doc_twin_score.py`, `doc_twin_coverage2.py`)।

### অন্যান্য সিদ্ধান্ত

- Exact duplicate (marks_parts-সহ full key): ৪ গ্রুপ, ৪টি অতিরিক্ত row — সবাই
  flagged, ভিন্ন set-এর কভারেজ বলে দুটো কপিই রাখা হয়েছে (ডিলিট নয়)।
- খালি placeholder ১২টি (question_text + options + guide_solution খালি) —
  সবগুলোতে marks_parts-এ আসল কনটেন্ট আছে বলে সব রাখা হয়েছে; ০টি ড্রপ।
- Math-misfire: `{a,b,c}` → বাংলা ক্ষতি পাওয়া যায়নি (0 hits); সেট-বিল্ডার
  নোটেশনে বাংলা বৈধ (`{x : x মৌলিক সংখ্যা}`)। re-decode/re-chunk লাগেনি।

### বাকি সীমা

- ৩৬টি twin-র coverage ০.৭৭–০.৯৯ (১.০০ নয়) — token-ভিত্তিক মিল, অক্ষরে-অক্ষরে নয়।
- ২টি doc-র twin verdict বাকি (উপরে)।
- Decoded টেক্সটের private-use গ্লিফ (\uf0ce = ∈ ইত্যাদি) ও CID-ক্ষতিগ্রস্ত
  ফাইলের fragment সীমা আগের মতোই আছে; flagged row flagged-ই আছে।
- GitHub push coordinator-এর কাজ — এই পাসে push করা হয়নি।
