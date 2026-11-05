# English Paper-I Import — Dry-Run Report (PREP ONLY, NOT executed)

প্রস্তুতি: 2026-11-01। এই রানে DB পড়া/লেখা হয়নি, ডেপ্লয় নয়, zip নয়,
git নয়। এক্সিকিউশন করবে প্যারেন্ট (`import_english_paper1.py` চালিয়ে,
তারপর `VERIFY_CHECKLIST.md` অনুযায়ী লাইভ যাচাই)। মালিকের নির্দেশ
(2026-11-01 ~15:03): ১ম পত্র পূর্ণ ইমপোর্ট; ২য় পত্র সব সময় আলাদা
সাবজেক্ট — তাই ১৫৮ সারি এই ইমপোর্টে আসবে না।

## ১. ধরে রাখা ১৫৮ সারির শনাক্তকরণ (প্রমাণসহ)

নিয়ম (DRYRUN-এর held grouping হুবহু): section ∈
{writing-paragraph, writing-email, writing-letter, writing-composition}
AND 481 ≤ source পৃষ্ঠা ≤ 570 — অর্থাৎ W1/W2 অনুশীলন-ব্লক, যাদের বইয়ের
রানিং হেড "[Paper-II]"।

যাচাই (merged_units.json-এর বিরুদ্ধে, দুই পৃষ্ঠা-ফিল্ডে আলাদা করে):
- source_pdf_page দিয়ে: 158 সারি; source_printed_page দিয়ে: 158 সারি;
  দুই সেট হুবহু একই (symmetric diff 0) — শনাক্তকরণ দ্বিমুখী-প্রমাণিত।
- ভাঙন: writing-paragraph 41 (pp511–521) + writing-email 18
  (W1 8, pp523–525 + W2 10, pp526–528) + writing-letter 59 (pp530–553)
  + writing-composition 40 (pp555–570) = 158। PROGRESS-এর W1/W2
  প্রতিবেদনের সংখ্যার সাথে হুবহু মিলেছে।
- 158-ই practice (test_id NULL), 158-ই scored=false, 67-টি flagged।
- বাইরে থাকা লেখা-সারি (Paper-I-তে থাকছে): writing-paragraph 4,
  writing-letter 3, writing-composition 1 (লেসন/টেস্ট-সারি, W-রেঞ্জের
  বাইরে) + writing-story 98 + writing-dialogue 95 (story/dialogue
  Paper-I হেডার)।

## ২. ইমপোর্ট সেট: 4,697 সারি

4,855 (merged) − 158 (held) = 4,697 = টেস্ট সারি 3,299 + অনুশীলন
(ব্যাংক) সারি 1,398। সব id অনন্য, সব `eng1-` উপসর্গ, সব
verified_visual=true, কোনো `paper` ফিল্ড নেই।

### সেকশন-ভিত্তিক (ইমপোর্ট সেট)

| section | সারি | | section | সারি |
|---|---|---|---|---|
| mcq | 846 | | story | 604 |
| true-false | 11 | | summary | 89 |
| short | 616 | | table | 772 |
| gapfill | 370 | | writing-story | 98 |
| matching | 493 | | writing-dialogue | 95 |
| rearranging | 92 | | writing-paragraph | 4 |
| poem | 602 | | writing-letter | 3 |
| writing-composition | 1 | | writing-graph | 1 |

### সেট-ভিত্তিক (টেস্ট সারি; keyed = answer_key খালি নয়)

| সেট | সারি | keyed | সেট | সারি | keyed |
|---|---|---|---|---|---|
| main-01 | 64 | 19 | main-25 | 64 | 14 |
| main-02 | 64 | 14 | main-26 | 94 | 26 |
| main-03 | 93 | 28 | main-27 | 56 | 12 |
| main-04 | 47 | 7 | main-28 | 62 | 14 |
| main-05 | 47 | 7 | main-29 | 59 | 14 |
| main-06 | 64 | 20 | main-30 | 59 | 14 |
| main-07 | 59 | 20 | main-31 | 75 | 25 |
| main-08 | 59 | 20 | main-32 | 71 | 21 |
| main-09 | 68 | 27 | main-33 | 78 | 28 |
| main-10 | 65 | 24 | main-34 | 73 | 24 |
| main-11 | 59 | 20 | main-35 | 65 | 21 |
| main-12 | 47 | 7 | main-36 | 92 | 30 |
| main-13 | 47 | 7 | main-37 | 75 | 21 |
| main-14 | 47 | 7 | main-38 | 65 | 20 |
| main-15 | 47 | 7 | main-39 | 58 | 13 |
| main-16 | 47 | 7 | main-40 | 47 | 7 |
| main-17 | 47 | 7 | main-41 | 47 | 7 |
| main-18 | 59 | 14 | main-42 | 47 | 7 |
| main-19 | 64 | 14 | main-43 | 47 | 7 |
| main-20 | 54 | 11 | special1-44…50 | 47 করে | 7 করে |
| main-21 | 61 | 21 | special1-51…54, 56, 57 | 47 করে | 13 করে |
| main-22 | 64 | 14 | special1-55 | 42 | 13 |
| main-23 | 59 | 14 | অনুশীলন (set_id NULL) | 1,398 | — |
| main-24 | 80 | 25 | **মোট** | **4,697** | **1,605 keyed** |

সারি-সংখ্যা ≠ ক্যানোনিকাল নম্বর: সেটের সারি-সংখ্যা (উপরে) DB-সত্য;
MARKING_SYSTEM-এর ক্যানোনিকাল নম্বর-মোট (100; ব্যতিক্রম main-09=99
[Q3(c) ছাপা নেই], main-27=64 [p230 স্ক্যান-ত্রুটি, 36 নম্বর ঘাটতি],
special1-55=95 [Q3 ছাপা নেই]) choice-সমন্বিত নম্বর — Q8/Q9-এর 8টি
choice সারি সব ডেলিভার করা হয়েছে বলে কাঁচা marks-যোগফল বেশি হয়
(যেমন main-01 কাঁচা যোগ 129)। কোনো সেটকে 100-এ জোর করা হয়নি।

### অন্যান্য মোট

- scored (ফাইল-স্টেজ ধারণা): true 2,515 / false 2,182।
  true = mcq 802 + true-false 11 + gapfill 360 + table 757 +
  matching 493 + rearranging 92।
- flagged (flag_note আছে): 426 সারি → guide_error true 246 /
  false 180 (নিচে §4)। ফ্ল্যাগহীন 4,271 সারি → guide_error false।
- answer_key আছে: 1,605 সারি (mcq 844/846 — চাবিহীন 2টি Test 27 Q1
  Set-1(a),(b); true-false 11/11; matching 267/493; rearranging 48/92;
  table 435/772; বাকি সেকশনে answer_key null — উত্তর guide_solution-এ)।
- pointer-only: 112 সারি (টেস্ট Q10/Q11 writing-story 56 +
  writing-dialogue 56; সব answer_text null, সব flag_note-এ
  pointer-চিহ্ন আছে) → guide_solution NULL + flag_note হুবহু।
- marks: null 382, 1: 2,262, 2: 1,683, 8: 92, 10: 87, 15: 191
  (15 = লেখা-সারি 191 = টেস্ট 112 + অনুশীলন 79)।
- options: null 3,558; array 1,083 (দৈর্ঘ্য 2/4/9/10/12);
  dict 56 (mcq, {i,ii,iii,iv} কী) — Edge optionsToArray দুই রূপই
  সামলায়, তাই JSON হুবহু রাখা হয়েছে।
- question_text: সব সারিতে অ-খালি (NOT NULL নিরাপদ)।
- source_printed_page: সব মান int-রূপান্তরযোগ্য।

## ৩. ম্যাপিং (merged → guide_questions)

| merged ফিল্ড | DB কলাম | নিয়ম |
|---|---|---|
| id | id | হুবহু |
| — | book_id | `class9-english-1st-bn-guide` (নতুন বই-সারি) |
| — | chapter_id / chapter_number | NULL (অধ্যায় নেই) |
| source_pdf_page | guide_source | `english-1st.pdf p<পৃষ্ঠা>` |
| question_text | question_text | হুবহু |
| section | question_type + section | হুবহু (17 মান) |
| options | options | JSON হুবহু (array/dict/null) |
| answer_key | answer_key | হুবহু (verbatim; নিচে ফুটনোট-ভিন্নতা দেখুন) |
| answer_text | guide_solution | হুবহু (null = pointer-only/MCQ/চাবিহীন) |
| marks | marks | হুবহু (int/null) |
| — | marks_parts | সব NULL (সারি আগেই প্রতি-অংশে ভাঙা) |
| — | important | সব false (ছাপা গুরুত্ব নেই) |
| test_id | set_id | টেস্ট সারিতে test_id, অনুশীলনে NULL |
| verified_visual | verified_visual | সব true |
| flag_note → শ্রেণি | guide_error | §4-এর নিয়ম |
| unit_lesson | lesson | যেখানে আছে, নাহলে NULL (1,419 null) |
| — | stimulus_id | NULL (চাঙ্ক-id নেই; উদ্ভাবন নয়) |
| stimulus_text | stimulus_text | হুবহু (297 সারিতে আছে) |
| source_pdf_page / printed | source_*_page | int |
| flag_note | flag_note | হুবহু |
| board_tag | note | হুবহু (পার্সিং করে board_name/year বানানো হয়নি — নিচে দেখুন) |
| — | board_name/board_year, has_diagram/diagram_note, linked_prose_chunk_id, corrected_answer_key/correction_note | NULL |

বাদ পড়েছে (DB কলাম নেই; merged_units.json-ই আর্কাইভ):
question_number, old_id, stimulus_ref, choice_count,
choice_required, verified_second_pass, scored, flagged।

### বই-সারি (প্রস্তাব; title প্রদর্শন-মাত্র, id-ই চাবি)

id `class9-english-1st-bn-guide`, class_id 9, subject_id `english`,
language `bn`, title `English 1st Paper Guide`, supplied false,
source_link NULL। ক্লাস-১০ গণিতের নজিরে class_id 9-এর বই দিয়েই
পরিবেশিত হবে (অ্যাপ/Edge-এর বিদ্যমান নিয়ম; ইমপোর্টের কাজ নয়)।

## ৪. guide_error শ্রেণিবিভাগ (426 flagged সারি, 0 অজানা)

নিয়ম (স্ক্রিপ্টে একই কোড; FALSE-নিয়ম আগে, কারণ pointer/নম্বর/
নম্বরিং-নোটে error-শব্দও থাকে):

FALSE (ত্রুটি নয়): pointer-only (48) / See the Writing Part (64) /
মডেল-অনুপস্থিতি / নম্বর-নোট (14) / চাবি-অনুপস্থিতি (10: Test 46 Q4
5 + Or-সংস্করণ 5) / printed-numbering ও ক্যানোনিকাল (14) /
পুনঃট্যাগ (13) / মার্জ-সংশোধন (1: Test-30 Q8(f) — ছাপা চাবি 500 dpi-তে
যাচাইকৃত, তাই ত্রুটি নয়) / section-সিদ্ধান্ত (essay→composition,
ট্যাগ-নিয়মে ধরা) / বোর্ড-ট্যাগ অমিল (1) / চাবি-ক্রম (5) /
সারি-ক্রম (5) / লেবেল-অনুপস্থিতি (1: (iv) ঘর কী-পেজ থেকে পূরণ) /
ট্যাগ-কাটা (4: শুধু স্কুল-ট্যাগ ছাঁটা, কনটেন্ট ঠিক)।

TRUE (ত্রুটি-শ্রেণি): misprint 42 / key-tension 9 / uncertain-word 3 /
scan-cut (কাটা) 4 / scan-defect (p230 ত্রুটিপূর্ণ স্ক্যান) 4 /
ছাপার ভুল/মুদ্রণ-ত্রুটি 37 / ছাপা চাবি/উত্তর/কী 18 / ছাপা মিলিত বাক্য 1 /
অন্যান্য ছাপা-verbatim নোট 128। মোট TRUE 246।

স্ক্রিপ্টে অজানা নোট পেলে এক্সিকিউশন থেমে যাবে (আগে রোলব্যাক);
এই ফাইলের বিরুদ্ধে যাচাইয়ে অজানা 0।

## ৫. নমুনা সারি (ম্যাপিং-যাচাইয়ের জন্য)

- true-false: `eng1-p245-true-false-d(4)` — section true-false,
  practice, Unit-10 Lesson-06, options [True, False], answer_key ✓,
  answer_text True, scored true (ফাইলে), marks null → DB:
  answer_key ✓, guide_solution "True", guide_error false।
- pointer-only: `eng1-p166-writing-story-q10` — main-18, marks 15,
  answer_key null, answer_text null, flag_note "pointer-only: …
  See the Writing Part" → DB: guide_solution NULL, flag_note হুবহু,
  guide_error false, hasSolution false।
- flagged-true: `eng1-p164-mcq-q1-set1e` — main-18, mcq, answer_key
  "ii", flag_note "misprint: প্রশ্নে 'Kathmundu' ছাপা…" → DB:
  guide_error true (কুইজ-স্কোরিং থেকে বাদ)।
- সাধারণ mcq: `eng1-p019-mcq-q1-set1-a` — main-01, options 4টি,
  answer_key "ii", marks 1 → DB: hasKey true, guide_error false।

## ৬. সৎভাবে জানানো ফাঁক/সিদ্ধান্ত (ইমপোর্টের কাজ নয়)

1. **44টি keyed Additional/alternative MCQ** (সব practice, সব
   marks null, ফাইলে scored=false): DB-তে scored কলাম নেই, তাই
   অ্যাপের বিদ্যমান কুইজ-নিয়ম (mcq + hasKey + guide_error=false)
   এগুলোকে অন্তর্ভুক্ত করবে। ভবিষ্যৎ অ্যাপ-ফিল্টারের সম্ভাব্য
   উপায়: marks IS NOT NULL (44-টিরই marks null)। ইমপোর্টে কিছু
   বাদ দেওয়া হয়নি।
2. **choice_count/choice_required বাদ**: DB কলাম নেই; any-5
   গ্রুপিং অ্যাপকে সারি থেকে derive করতে হবে (আগের dry-runের
   অনুমান অনুযায়ী)।
3. **stimulus_ref বাদ**: চাঙ্ক-id নেই; পূর্ণ stimulus_text যেখানে
   আছে সেখানে রাখা হয়েছে।
4. **answer_key verbatim**: matching/rearranging/table-এ
   T1-এ চাবি নেই, T2-এ আছে — অসঙ্গতি হুবহু রাখা হয়েছে
   (স্বাভাবিকীকরণ নয়; কুইজ-পুল MCQ+scored-এ সীমিত বলে
   স্কোরিং-এ প্রভাব নেই)।
5. **board_tag → note**: "DB '20", স্কুল-নাম, সেট-ট্যাগ মেশানো
   (1,684 সারি) — board_name/year-এ পার্স করা নিরাপদ নয় বলে
   কাঁচা স্ট্রিং note-এ রাখা হয়েছে, পার্সিং উদ্ভাবন করা হয়নি।
6. **বই-শিরোনাম প্রস্তাব**: title প্রদর্শন-মাত্র; প্যারেন্ট
   চাইলে এক্সিকিউশনের সময় বদলাতে পারেন (id অপরিবর্তিত)।
7. **বেসলাইন**: স্ক্রিপ্ট এক্সিকিউশনের সময় লাইভ মোট পড়ে
   প্রত্যাশিত ডেল্টা (+4,697 সারি + 1 বই) ছাপবে — 9,027 ধরে
   নেওয়া হয়নি (অংক-ইমপোর্ট আগে হলে মোট বদলাবে)।

## ৭. এক্সিকিউশন (প্যারেন্টের ধাপ)

1. `SUPABASE_DB_PASSWORD` env-এ ফ্রেশ পাসওয়ার্ড দিয়ে
   `import_english_paper1.py` চালান (এক ট্রানজ্যাকশন; যেকোনো
   ব্যর্থতায় সম্পূর্ণ রোলব্যাক)। প্রত্যাশিত আউটপুট: baseline →
   final ডেল্টা 4,697 + বই-সারি।
2. `VERIFY_CHECKLIST.md` অনুযায়ী লাইভ Edge প্রোব চালান
   (`verify_english_import.py` দিয়ে স্বয়ংক্রিয় যাচাই)।
3. কোনো প্রোব না মিললে রিপোর্ট করুন — DB-তে হাত দিয়ে ঠিক
   করার আগে প্যারেন্টকে জানান।
