# SSC হিন্দুধর্ম ও নৈতিক শিক্ষা — লেকচার শিট চাংক

**সাবজেক্ট:** হিন্দুধর্ম ও নৈতিক শিক্ষা (slug: `hindu`)
**তারিখ:** 2026-11-24
**মোট row:** 5,583 (সব JSON parse হয়; ID অনন্য)
**ফ্ল্যাগ করা row:** 5,201 (93% — বেশিরভাগই ডিকোড-ত্রুটি / উত্তর না থাকার ফ্ল্যাগ, ডেটা বাদ দেওয়া হয়নি)

## Row ভাগ (type অনুযায়ী)

| type | সংখ্যা | মন্তব্য |
|---|---|---|
| mcq | 4,279 | উত্তর আছে 2,150টিতে (50%) |
| cq | 688 | গাইড-সমাধান আছে 169টিতে (25%) |
| gyanmulok | 604 | জ্ঞানমূলক + অনুধাবনমূলক/প্রয়োগ/উচ্চতর দক্ষতা Q&A |
| lecture-note | 12 | প্রতি অধ্যায়ে ১টি বিষয়-সংক্ষেপ |

## Row ভাগ (section অনুযায়ী)

| section | সংখ্যা | উৎস |
|---|---|---|
| lecture-mcq | 4,279 | সব MCQ (অধ্যায় + বোর্ড + স্কুল + মডেল টেস্ট) |
| lecture-cq | 688 | সব সৃজনশীল (অধ্যায় + বোর্ড + স্কুল + মডেল টেস্ট) |
| lecture-gyanmulok | 604 | Chapter Wise দক্ষতাস্তরের Q&A |
| lecture-lecture-note | 12 | Chapter Wise বিষয়-সংক্ষেপ |

> Normalization 2026-11-24-এ section স্পেসিফিকেশনের `lecture-<type>` সূত্রে আনা হয়েছে
> (আগে বোর্ড/স্কুল/মডেল row-তে `lecture-board` / `lecture-school` / `lecture-model-test`
> ছিল — বিস্তারিত নিচের Normalization সেকশনে)।

## ফাইল গঠন

- `questions-hindu.json` — সব 5,583 row-এর combined ফাইল
- `flagged.json` — 5,201টি ফ্ল্যাগ করা row (flag_note-সহ)
- `chapter-<NN>-<type>.json` — অধ্যায়ভিত্তিক (01–10; 1.1/1.2 একত্রে অধ্যায় ০১, 2.1/2.2 একত্রে অধ্যায় ০২)
- `board-<board>-<year>-<type>.json` — বোর্ড প্রশ্ন 2024/2025 (h25 + bq24)
- `board-<board>-<year>-tp-<type>.json` — Test paper/Board Question.pdf-এর বোর্ড প্রশ্ন (2023/2024)
- `school-<slug>-<type>.json` — স্কুল প্রশ্নপত্র
- `model-test/model-<NN>-<type>.json` — ১০টি মডেল টেস্ট (০১–০৫ MCQ, ০৬–১০ CQ)
- `processed-files.txt` / `missing-files.txt` — 18 PDF প্রসেস, 0 মিসিং
- `report-2026-11-24.md` — বিস্তারিত রিপোর্ট (ডিকোড-ত্রুটি, সীমাবদ্ধতা, যাচাই)
- `_work/` — চাংকার স্ক্রিপ্ট (`chunk-hindu.py`) ও chunk-report.json

## ID নিয়ম

- অধ্যায়: `hindu-lec-ch<NN>-<type>-<NNN>` (অধ্যায় ০১/০২-এর দুই অংশের ID ধারাবাহিক)
- বোর্ড: `hindu-lec-board-<board>-<year>-<type>-<NNN>` (tp ফাইলের row-তে `-tp-` যোগ)
- স্কুল: `hindu-lec-school-<slug>-<type>-<NNN>`
- মডেল: `hindu-lec-mt-model-<NN>-<type>-<NNN>`

## উত্তর-নীতি (কখনো আন্দাজ নয়)

- MCQ উত্তর: ● চিহ্ন (printed-marker) → Answer Sheet ক্রস-চেক (tp-board) → bq24 ইনলাইন উত্তরমালা (K/L/M/N) → না পেলে null + flag
- h25 (2025) MCQ: উত্তরমালার অক্ষর ছাপায় টেক্সট হিসেবে নেই — সব 270টির answer_key null + flag
- School/Model MCQ: ফাইলে উত্তর ছাপা নেই — সবগুলোর answer_key null + flag
- CQ সমাধান: ছাপা উত্তর থাকলে guide_solution; না থাকলে Answer Sheet-এর পৃষ্ঠা-নির্দেশ answer_pointer-এ + flag ("উত্তর ছাপা নেই")

## জানা সীমাবদ্ধতা (বিস্তারিত report-2026-11-24.md-এ)

1. **ডিকোডার v2-র অবশিষ্ট গার্বল:** ছোট MCQ অপশন-টেক্সটে Bijoy-অবশেষ থাকে (যেমন "K‚g©", "eivn") — ফ্ল্যাগ করা, আন্দাজ করা হয়নি।
2. **2-কলাম ইন্টারলিভ দূষণ:** কিছু CQ উদ্দীপক/সমাধানে পাশের কলামের লেখা মিশে যায়; কিছু MCQ অপশনে অতিরিক্ত লেখা ঢোকে।
3. **বগুড়া জিলা স্কুল MCQ 60টি:** সোর্সেই দুই সেট প্রশ্ন ছাপা আছে (ASCII-সংখ্যাযুক্ত pp.4–5 ও বাংলা-সংখ্যাযুক্ত p.6) — দুটোই রাখা হয়েছে, নম্বর ১–৩০ দুইবার।
4. **অধ্যায় ৫-এ 171 orphan সেগমেন্ট:** ৩-কলাম CQ লেআউট (pp.20, 26) — কিছু CQ সমাধান যুক্ত হয়নি; প্রশ্নগুলো ধরা আছে।
5. **tp-board CQ 190 (প্রত্যাশিত ~198):** ৮টি সেট ধরা পড়েনি।
6. **bq24-এ চট্টগ্রাম বোর্ড আছে:** আগের ধারণা (৮ বোর্ড, চট্টগ্রাম নেই) ভুল ছিল — p.37-এ আসল চট্টগ্রাম ২০২৪ পেপার আছে; মোট ৯ বোর্ড × ৩০ MCQ + ১১ CQ = 270 + 99।
7. অধ্যায় ১.১/১.২ ও ২.১/২.২-এর প্রশ্ন নম্বর দুই অংশেই ১ থেকে শুরু হয় — `source_file` দিয়ে অংশ চেনা যায়।
8. 15টি row-তে question_text নেই (ফ্ল্যাগ করা; normalization-এ 2টি সম্পূর্ণ খালি placeholder বাদ দেওয়া হয়েছে — নিচে দেখুন)।




## Normalization — 2026-11-24

Pre-normalization backup: `_backup_pre_norm/` (combined + flagged, 5,585 row)।
Coordinator GitHub-এ push করবে — এই পাসে push করা হয়নি।

### আগে / পরে

| মাপ | আগে | পরে |
|---|---|---|
| মোট row | 5,585 | 5,583 (−2 placeholder) |
| flagged row | 4,640 (83%) | 5,201 (93%) |
| section = `lecture-<type>` | 3,531 | 5,583 (সব) |
| type ভাগ | mcq 4,281 / cq 688 / gyanmulok 604 / lecture-note 12 | mcq 4,279 / cq 688 / gyanmulok 604 / lecture-note 12 |

### কী ঠিক করা হয়েছে

1. **Section (2,052 row):** স্পেসিফিকেশনের সূত্র `section = "lecture-<type>"` মেনে
   `lecture-board` / `lecture-school` / `lecture-model-test` / `lecture-note`
   বদলে `lecture-mcq` / `lecture-cq` / `lecture-lecture-note` করা হয়েছে।
   ভাগ: board→mcq 1,079; board→cq 388; school→mcq 299; school→cq 72;
   model-test→mcq 150; model-test→cq 52; lecture-note→lecture-lecture-note 12।
   প্রতিটি row-তে flag note যোগ করা হয়েছে। সিদ্ধান্তের ভিত্তি: স্পেসিফিকেশনের
   সূত্র + economics সাবজেক্টে একই আক্ষরিক নিয়ম (0 ব্যতিক্রম, `lecture-lecture-note`-সহ);
   islam / general-science-এ `type=board` ব্যবহার করা হয়েছে, bangla-তে মিশ্র নিয়ম —
   hindu-তে type অপরিবর্তিত (board প্রশ্ন mcq/cq-ই থাকে, স্পেসিফিকেশনের board অনুচ্ছেদ অনুযায়ী)।
2. **য+়/য় trap — metadata (437 + 87 + 1,209 row):** chunker-লেখা metadata-তে
   ভুল ক্রম U+09AF+U+09BC ঠিক করা হয়েছে — chapter_name-এ `ধর্মীয়` 437 row
   (আচার-অনুষ্ঠান 237, উপাখ্যান 200), lesson-এ `প্রযোগ`-এর য-এর ভুল nukta 87 row,
   flag_note-এর 5টি template-শব্দ (যায়নি, পাওয়া, ছাপায়, উত্তরমালায়, লেখায়) 1,209 row।
   board_name/board_year-এ trap নেই (সব ASCII slug: barishal, chattogram, …)।
   ডিকোড-করা source text (question_text/stimulus/guide_solution) ছোঁয়া হয়নি —
   স্পেসিফিকেশনের নিয়ম অনুযায়ী ডিকোড-ত্রুটি যেমন আছে তেমনই রাখা হয়েছে।
3. **খালি placeholder বাদ (2 row):** question_text + options + guide_solution
   তিনটিই খালি ছিল — `hindu-lec-board-cumilla-2025-mcq-028`
   (Board Question 2025/Hindu-2025.pdf p16, Q28) এবং
   `hindu-lec-school-nawab-faizunnessa-mcq-019`
   (Test paper/School Question.pdf p7, Q19)। সম্পূর্ণ row `_work/dropped-placeholders.json`-এ রাখা আছে।
4. **marks_parts নোট (281 row):** CQ row-তে parts `[ক,খ,গ,ঘ]` নয় — 150 row-তে
   বাস্তব নোট যোগ করা হয়েছে (অংশের সংখ্যা ও তালিকাসহ); 131 row-তে আগে থেকেই
   অংশ-সংক্রান্ত নোট ছিল। content বদলানো হয়নি — দুটি সেট মিশে থাকা row আলাদা করা হয়নি।
5. **Doc-twin যাচাই (17/17 duplicate):** 17টি .doc/.docx-ই PDF twin-এর duplicate
   প্রমাণিত (soffice convert + shared decode + token-similarity; বিস্তারিত
   `work/hindu/doc-twins/verification-2026-11-24.md` ও `compare.json`-এ) —
   কিছুই chunk করা হয়নি, skipped-ই আছে।

### যাচাই (সব পাস)

- সব JSON parse হয়; combined 5,583 = 138টি per-file JSON-এর যোগফল
- ID অনন্য, null নেই; সব row 37 field; section সব row-তে সূত্র মেনে চলে
- flagged.json ⊆ combined; flagged 5,201 = flag_note-আছে এমন row-এর সংখ্যা
- processed 18 PDF + missing 0 + doc-duplicate 17 = ম্যানিফেস্ট 35
- 3টি ডিকোড ফাইল চোখে যাচাই (অধ্যায় ৩, Hindu-2025, School Question)

### বাকি সীমা

- 281টি CQ row-তে marks_parts অস্বাভাবিক (দুটি সেট মিশে যাওয়া / অংশ কম) — re-chunk ছাড়া ঠিক করা যাবে না।
- Source text-এ য+় trap রয়ে গেছে (question_text-এ 2,533 row; ড+় 370 row) — decoder-স্তরের পাসের কাজ।
- 15টি row-তে এখনো question_text নেই (ফ্ল্যাগ করা)।
