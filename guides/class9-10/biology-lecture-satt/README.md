# জীববিজ্ঞান (biology) — SSC Lecture Sheets chunking

- সোর্স: `ssc-chapter-wise/2. SSC Science/SSC Biology`
- ম্যানিফেস্ট: `inventory/subjects/biology.json` — ৫৩৮ ফাইল
- ডিকোড: `decoded/ssc/biology/` (শেয়ার্ড টুল `tools/decode-pdf.py` দিয়েই)
- স্টেজিং: `staging/ssc/biology/` (এই ডিরেক্টরি)
- তারিখ: 2026-11-24

## সংখ্যা

| মাপ | সংখ্যা |
|---|---|
| মোট row | **28,069** (first pass 21,653 + final pass 6,416) |
| mcq | 19,683 (+2,321) |
| board | 6,683 (+3,850) |
| cq | 1,337 (+198) |
| saq | 161 |
| lecture-note | 142 (+47) |
| handnote | 63 |
| question_text আছে | 9,092 (first pass 4,659 + final pass 4,433) |
| answer_key আছে | 21,892 (final pass-এ নতুন 5,518) |
| flag করা row | 28,069 (সবগুলোতেই অন্তত একটা সতর্কতা আছে — নিচে দেখুন) |
| ডিকোড করা PDF | 236 + 41 = 277 (final pass-এ 41টা নতুন PDF; 1টা scanned, ডিকোড হয়নি) |
| processed-files.txt | 537 (456 + 81 নতুন: 41 PDF + 40 doc/docx ইনভেন্টরি) |
| missing-files.txt | 1 — শুধু `Test paper/Biology16-22.pdf` (scanned image-only, ~210 MB, OCR লাগবে) |
| processed + missing | 537 + 1 = **538 = ম্যানিফেস্ট** ✓ |

## Final pass (2026-11-24 রাত, chunker `tools/chunk-biology-final.py`)

missing-files.txt-এর 82টা ফাইলের মধ্যে 81টা চাংক করা হয়েছে (42 PDF-এর 41টা;
`Biology16-22.pdf` scanned, টেক্সট লেয়ার নেই — OCR ছাড়া হবে না)।
নতুন row 6,416টা — board 3,850 / mcq 2,321 / cq 198 / lecture-note 47।
এর মধ্যে আসল প্রশ্ন-টেক্সট আছে 4,433টায়, number+key-only 1,983টায়
(ছবি-ভিত্তিক NEW UPDATE MCQ + কী-টেবিল থেকে ভরা প্রশ্ন),
answer_key আছে 5,518টায়। সব নতুন row-ই flagged।

কী চাংক হয়েছে:
- **NEW UPDATE ch8–14** (BASIC/CQ/MCQ): 1,852 row — MCQ 1,651 (●-গুনতি হুবহু মিলেছে),
  CQ 154, lecture-note 47। MCQ/BASIC ছবি-ভিত্তিক (বাংলা লাইন 4–10%)।
- **5. Model Test MCQ ch1–14**: 420 row (14×30), **সব 420টায় key** — উত্তরমালা থেকে।
- **Test paper/1. BQ 21-24** (বোর্ড 2021–2024): 1,096 row — MCQ 900/900 (36 পেপার × 25),
  key 899টা (দিনাজপুর 2022 Q11 = `*`, key নেই); CQ 196 row (36 পেপার)।
  2023-এর 7 বোর্ডের প্রশ্ন ছাপা 26–50 নম্বরে — key position-এ মিলিয়ে বসানো হয়েছে
  (Biology 18-23-এর 1–25 পেপারের সাথে stem মিলিয়ে যাচাই করা)।
- **Test paper/3. School CQ + 4. School MCQ** (Ans School থেকে key): CQ 117 row
  (19 পেপার), MCQ 500/500 (20 পেপার), key 500টায়।
- **Test paper/Biology 18-23** (বোর্ড 2017–2023 + স্কুল + এক্সক্লুসিভ MT): 2,431 row —
  বোর্ড MCQ 1,300/1,300 (52 পেপার), বোর্ড CQ 228 (44 পেপার), স্কুল MCQ 500/500
  (20 পেপার), স্কুল CQ 109 (20 পেপার), এক্সক্লুসিভ MT MCQ 250/250 (10 পেপার),
  MT CQ 44 (10 পেপার)। 2018-এর কোনো বোর্ড পেপার নেই (ফাইলের নাম "18-23" হলেও)।

চাংকারে ধরা পড়া পার্সার-বাগ (final pass-এ ঠিক করা):
- **`বিদ্যালয়` ম্যাচ হতো না**: `SCHOOL_PAT_NORM`-এর `বিদ্যালয়` লেখা ছিল য+়
  (দুই কোডপয়েন্ট) দিয়ে, আর ডিকোড করা টেক্সটে য় (U+09DF, এক কোডপয়েন্ট) —
  ফলে "বিদ্যালয়"-এ শেষ হওয়া 12টা স্কুল পেপার (B18-23: MCQ 7টা + CQ 5টা) প্রথমে
  মিস হয়েছিল; প্যাটার্নে `\u09df` বসিয়ে ঠিক করা হয়েছে।
- **"প্রশ্নের মান ১।" Q1 হয়ে যেত**: MCQ পেপারের নির্দেশনার "মান ১।" Q-মার্কার
  হিসেবে ধরা পড়ত — first pass-এর বোর্ড MCQ Q1 row-গুলো তাই নির্দেশনার টেক্সট
  (যেমন "প্রশ্নপত্রে কোনো প্রকার দাগ/চিহ্ন দেওয়া যাবে না।")। final pass-এ
  "মান"-এর পরের ১ বাদ দেওয়া হয়েছে — নতুন Q1 row-গুলো আসল প্রশ্ন।
- **CQ set-মার্কার নোংরা**: BQ/B18-23 বইয়ে "N", "N ", লাইন-ভাঙা "৭ −/",
  খালি "N" লাইন, মাঝ-লাইনের মার্কার — v2 স্প্লিটার দিয়ে CQ 155 → 196 (file 1)।
  তবু ~338টা CQ সেট টেক্সট লেয়ারে পাওয়া যায়নি (ছবি/মার্কার পড়া যায়নি) —
  কোন সেটগুলো মিসিং, সেটা sibling row-এর flag-এ লেখা আছে।
- **MCQ number+key-only fill**: key টেবিলে 25টা key আছে কিন্তু টেক্সটে মার্কার
  কম — সেই নম্বরগুলো key-সহ row হিসেবে রাখা হয়েছে (B18-23 বোর্ড MCQ 108টা,
  file 1-এ 2টা)। CQ-তে এমন fill করা হয়নি — key ছাড়া খালি নম্বরের row-এর
  মূল্য নেই, শুধু missing-set flag দেওয়া হয়েছে।
- **Duplicate flag**: নতুন বোর্ড row-এর 264টা existing row-এর সম্ভাব্য duplicate
  হিসেবে flag করা (board+year+qnum+text-prefix মিল); 26–50 নম্বরের row-এর
  জন্য qnum−25 দিয়েও মিলানো হয়েছে। কোনো row ডিলিট করা হয়নি।

সীমা (flag-এ লেখা আছে):
- CQ সেট মিসিং: file 1-এ 92, B18-23 বোর্ডে 124, B18-23 স্কুলে 51, MT-তে 36,
  file 3-এ 35 — মোট ~338 সেট; শুধু OCR/ভিজ্যুয়াল চেকেই উদ্ধার সম্ভব।
- দিনাজপুর 2022 Q11-এর key `*` (Ans BQ + B18-23 দুই জায়গাতেই) আর দিনাজপুর
  2020 Q6-এর key পড়া যায় না (PUA চিহ্ন) — দুটোই null।
- file 4-এর key order-মিলিয়ে বসানো (Ans School-এর 20 টেবিলের order = file 4-এর
  20 পেপারের order); নাম-চেকের 3টা mismatch শুধু কসমেটিক ("সেট : ক " prefix,
  "(হাসনাহেনা)" suffix)।

## ডিকোডার v2 (2026-11-24 ~20:08)

v1 দিয়ে ডিকোড করা 236 ফাইলের প্রতিটায় বাংলা-লাইনের অনুপাত মাপা হয়েছে
(৫+ বাংলা অক্ষরওয়ালা লাইন)। 51টা ফাইল ≥50% ছিল (v1 আউটপুট রাখা হয়েছে),
**185টা ফাইল <50% ছিল — সবগুলো v2 টুলে আবার ডিকোড করা হয়েছে**
(185/185 exit 0, লগ `/tmp/biology-v2-log.tsv`)। v2-তে মাত্র ৩টা ফাইল
নাটকীয়ভাবে ভালো হয়েছে — `Biology-2023/2024/2025` (Saroda ফন্ট):
0.5% → 80–93% বাংলা লাইন। বাকি 182টা ছবি-ভিত্তিক (image-based) ফাইল —
টেক্সট লেয়ারে বাংলা লেখা নেই বলে v2-ও বদলাতে পারেনি।

## কীভাবে চাংক করা হয়েছে (সোর্স গ্রুপ অনুযায়ী)

- **3. MCQ Practice / Chaperwise MCQ1 / TYPEWISE MCQ PRACTICE / NEW UPDATE MCQ /
  Sheet-এর MCQ অংশ** — প্রশ্নের stem ছবি; প্রতি ● = ১টা প্রশ্ন (মোট 15,949টা
  row-তে answer_key আছে, ●-র অবস্থান থেকে; অপশন-অক্ষর বাংলা ক/খ/গ/ঘ বা
  K/L/M/N দুটোই চেনে)। question_text null + flag।
- **Chaperwise MCQ2 / SSC 27 MCQ / Board MCQ** — পুরো টেক্সট আছে, ২-কলাম
  interleave; প্রথম-উপস্থিতি (first-occurrence) অনুযায়ী অপশন বসানো হয়েছে —
  গ/ঘ অপশন মাঝে মাঝে অন্য কলামের প্রশ্নের সাথে বদলে যেতে পারে, সব row flag করা।
  SSC 27-এর উত্তরমালা থেকে key মিলিয়ে যাচাই করা হয়েছে (set-1: 25/25 মিলেছে)।
- **Board suggestion books (Biology-2023/2024/2025)** — প্রতি বোর্ডে MCQ পেপার
  (২৫টা) + CQ পেপার + উত্তরমালা। উত্তরমালার MCQ key K/L/M/N আকারে আছে —
  2023: 225/225, 2024: 200/200 key পাওয়া গেছে; **2025-এর key-র অক্ষরগুলো
  ছবি, তাই answer_key null**। CQ পেপারগুলোও পার্স করা হয়েছে (2023: 52,
  2024: 55, 2025: 59)।
- **TP 01/02, CQ/MCQ Board Question** — বোর্ড-স্প্যান ভাগ করে পার্স করা।
  TP 02-এর কিছু সেটে ২৫-এর বেশি প্রশ্ন আছে (২৬–৩৩ নম্বর আসল প্রশ্ন)।
- **TP 03/04, CQ/MCQ School Question** — স্কুল পেপারের সংকলন; "বিষয় কোড"
  লাইন দিয়ে পেপার ভাগ করে পার্স করা (TP03: 19 পেপার/118 row, TP04: 19/475,
  CQ School: 13/81, MCQ School: 18/450)। board_name/year null + flag
  (স্কুল পেপার, বোর্ড নয়)।
- **1. CQ Practice / TOPIC WISE CQ / NEW UPDATE CQ / Sheet-এর CQ অংশ** —
  "Nনং প্রশ্নের উত্তর/সমাধান" হেডার প্রতি ১ row; stimulus + বাংলা উত্তর ছবি,
  শুধু fragment রাখা হয়েছে।
- **5. Model Test/CQ + #SSC 27/CQ** — CQ সেট (সৃজনশীল—N ও ১. মার্কার) +
  SAQ অংশ ("উত্তর অংশ", প্রতি ফাইলে ৭–৮টা, ২ নম্বর করে)। মডেল টেস্ট: 14
  ফাইলে 4 CQ সেট করে (ch4-এ 3টা) + 8 SAQ; SSC27: 5 সেটে 7 CQ + 7 SAQ করে।
- **#TYPEWISE CQ/MCQ que+ans (28+28 ফাইল)** — প্রশ্ন/উত্তর দুটোই ছবি; গণনাযোগ্য
  মার্কার নেই বলে প্রতি ফাইলে ১টা flag row (মোট 56)।
- **2. SAQ Practice Sheet** — প্রশ্ন+উত্তর ছবি; প্রতি ফাইলে ১টা flag row (14)।
- **Sheet / #Hand Note / NEW UPDATE BASIC** — হেডিং-সেকশন প্রতি 1 row
  (lecture-note/handnote); বাংলা prose ছবি বলে শুধু হেডিং + fragment।
- **TP Ans / Answer Sheet (2 ফাইল)** — শুধু নম্বর-গ্রিড, উত্তর-অক্ষর ছবি;
  কোনো row হয়নি (key-source হিসেবে পরীক্ষা করা হয়েছে, README-তে নোট আছে)।

## জানা ডিকোড-ত্রুটি (হাত দিয়ে ঠিক করা হয়নি — যেমন আছে তেমনই রাখা হয়েছে)

"বহুনিবার্চনি" (954×), "বিশেস্নষণ" (576×), "বোডর্" (259×),
"উলিস্নখিত" (217×), "গুরম্নত্বপূণর্" (167×), "সম্পকের্" (46×),
"উলেস্নখিত" (45×), "প্রেশ্নর" (42×), "পযর্ন্ত্ম" (23×),
"চূড়ান্ত্ম" (9×), "চিন্ত্মা" (4×), "দাশির্নক" (2×)।

## বড় সমস্যা (ফাইনাল পাসের কাজ)

1. **বেশিরভাগ PDF-র বাংলা লেখা ছবি** — stem/উত্তর টেক্সট লেয়ারে নেই।
   OCR ছাড়া পূর্ণাঙ্গ প্রশ্ন/উত্তর পাওয়া যাবে না।
2. **২-কলাম interleave** — MCQ/CQ অপশন ও পার্ট মাঝে মাঝে অন্য কলামের
   প্রশ্নের সাথে মিশে যায়; সব ২-কলাম row flag করা আছে।
3. **উত্তর-key** — TYPEWISE/Chaperwise MCQ2/বোর্ড পেপারের বেশিরভাগে key
   ছবি বা নেই (board MCQ: 425/2,269-এ key আছে)।
4. **মিসিং 42টা PDF** (ডাউনলোড চলছে) — ফাইনাল পাসে চাংক করতে হবে।

## যাচাই (ডেলিভারির আগে)

- সব JSON parse হয় ✓
- chapter + model-test ফাইলের row-এর যোগফল (21,653) = questions-biology.json ✓
- সব id unique (21,653) ✓
- processed (456) + missing (82) = manifest (538) ✓
- চোখে পড়ে যাচাই করা ডিকোড ফাইল: MCQ que-1, MCQ Practice ch1, SSC27 CQ
  set-1 + MCQ set-1, TP BQ Sub, Chaperwise MCQ2 ch1, Hand Note ch1, Sheet ch1,
  Biology-2025 পৃষ্ঠা ১, Biology-2023 উত্তরমালা, TP03 স্কুল পেপার।
- SSC27 MCQ set-1-এর 25টা উত্তর উত্তরমালার সাথে 100% মিলেছে।
- per-● row-সংখ্যা প্রতিটা ফাইলে ●-সংখ্যার সাথে মিলেছে (যেমন জীব-MCQ: 2,274/2,274)।

## ID নিয়ম

- chapter row: `biology-lec-ch<NN>-<type>-<NNN>` (ch00 = অধ্যায় অজানা/whole-paper)
- model-test row: `biology-lec-mt-<set>-<type>-<NNN>`
- chapter_name ফাইল-হেডার থেকে নেওয়া হয়েছে (১৪টা অধ্যায়ই মিলেছে)।

## Normalization pass — 2026-11-25 (staging only, no push)

- ব্যাকআপ: `staging/ssc/biology/_backup_pre_norm/` — `questions-biology.json` + `flagged.json`
  (pre-normalization, md5-verified)। স্ক্রিপ্ট: `work/biology/normalize.py`,
  `dup_notes.py`, `rebuild.py` (+ `key_grid_check3.py`, `doc_twin_convert_all.py`)।
- মোট row: **28,069 → 28,069** (0টা ডিলিট, 0টা নতুন)। type ভাগ অপরিবর্তিত
  (board 6,683 / mcq 19,683 / cq 1,337 / saq 161 / lecture-note 142 / handnote 63)।
  flag করা row: 28,069 → 28,069 (সবগুলোই flagged আছে)।

### 1. Section fix — 10,394 row
- `বহুপদী সমাপ্তিসূচক` 3,510 + `অভিন্ন তথ্যভিত্তিক` 6,884 (সব type=mcq)
  → `section="lecture-mcq"`; subtype `flag_note`-এ রাখা হয়েছে
  (`subtype: বহুপদী সমাপ্তিসূচক` / `subtype: অভিন্ন তথ্যভিত্তিক`)।
- আগে: lecture-mcq 9,289; পরে: **lecture-mcq 19,683**। non-spec section এখন **0**।

### 2. Board-mislabel fix — 234 row relabel + 100 key + 2 stem
মূল কারণ: চাংকারের বোর্ড-হেডার প্যাটার্নে `ময়মনসিংহ` লেখা ছিল য+় (দুই কোডপয়েন্ট)
দিয়ে, আর ডিকোড করা টেক্সটে য় (U+09DF, এক কোডপয়েন্ট) — ফলে ময়মনসিংহের
হেডার কখনো মেলেনি, পুরো সেকশন আগের বোর্ডের নামে গেছে। কুমিল্লার হেডার ডিকোডে
`কুমিল-া` (হাইফেন-আর্টিফ্যাক্ট; TP02-তে `কুমিলস্না`) বলে সেটাও মেলেনি।
একই কারণে merged সেকশনের key-table-ও ভুল বোর্ডেরটা বসেছে (নিচে)।
প্রতিটা relabel ডিকোড করা সোর্সের হেডার-লাইন + stem মিলিয়ে যাচাই করা।
- **Biology-2023.pdf (62):** Rajshahi-লেবেলের `ska` MCQ 25 + `s1` CQ 5 → **কুমিল্লা 2023**
  (ids 1308-1337); Dinajpur-লেবেলের run-B MCQ 25 + CQ 7 → **ময়মনসিংহ 2023** (ids 1491-1522)।
- **Biology-2024.pdf (62):** Jessore-লেবেলের run-1 MCQ 25 + CQ 7 → **কুমিল্লা 2024**
  (ids 1680-1711); Dinajpur-লেবেলের run-1 MCQ 25 + CQ 5 → **ময়মনসিংহ 2024** (ids 1748-1777)।
- **Biology-2025.pdf (61):** Jessore-লেবেলের run-1 MCQ 25 + CQ 6 → **কুমিল্লা 2025**
  (ids 1933-1963); Dinajpur-লেবেলের run-1 MCQ 25 + CQ 5 → **ময়মনসিংহ 2025** (ids 2029-2058)।
- **TP02 2021 bank (49):** Jessore-লেবেলের q76-100 (25) → **কুমিল্লা 2021**
  (ids 501-525, set `board-cumilla-2021-sgha`); Dinajpur-লেবেলের q2-25 run (24)
  → **ময়মনসিংহ 2021** (ids 604-627, set `board-mymensingh-2021-sga`)।
- **Key পুনঃবণ্টন (100 key):** merged সেকশনে ভুল বোর্ডের উত্তরমালা বসেছিল — প্রমাণ:
  প্রতিটা run-এর 25টা key-ই ডোনার বোর্ডের ছাপা গ্রিডের সাথে 25/25 মিলেছে, নিজের
  বোর্ডের গ্রিডের সাথে 1-7/25। ঠিক করা হয়েছে: B23 Rajshahi sga (ids 1277-1301)
  ও Dinajpur run-A (1459-1483); B24 Jessore run-0 (1648-1672) ও Dinajpur run-0
  (1717-1741) — ছাপা উত্তরমালা (K/L/M/N) থেকে, নিজের বোর্ডের গ্রিড অনুযায়ী।
  Relabel হওয়া run-গুলোর key আগেই সঠিক বোর্ডের ছিল (25/25 যাচাই করা) — বদলানো হয়নি।
  B25-এর key নেই (ছবি) — কিছু করার নেই।
- **Stem fix (2):** Q1-stem fix-এ আগের পেপারের Q1 stem বসে গিয়েছিল — row 1308
  (Cumilla 2023 MCQ Q1 → `প্রতি কিউবিক মিলিমিটারে রক্তে লোহিত রক্তকণিকা থাকে−`)
  ও row 1491 (Mymensingh 2023 MCQ Q1 → `সাধারণত কত সপ্তাহ গভার্বস্থা বিদ্যমান থাকে?`) —
  দুটোই নিজের ডিকোড করা ফাইল থেকে verbatim (artefact সহ); key গ দুটোই যাচাই করে
  রাখা হয়েছে (নিজের বোর্ডের গ্রিড Q1=M=গ)।
- **নামা 4 row-র সিদ্ধান্ত (পুরোনো রিপোর্টের "Q5" দাবি ভুল — আসলে Q1):**
  1773 → ময়মনসিংহ 2024 CQ Q1 (আর্কিগোনিয়াম/শ্রেণিবিন্যাস/রাজ্য; ডিকোড লাইন 4873+,
  উত্তরমালা "প্রশ্ন ০১" নিশ্চিত করে); 1958 → কুমিল্লা 2025 CQ Q1 (হিস্টোলজি/
  পরিবহণ টিস্যু/চিত্র E/F/G; তবে question_text-এর বাবুল-উদ্দীপকটা আসলে কুমিল্লা Q5-এর —
  flag-এ লেখা আছে, টেক্সট মুছে ফেলা হয়নি); 2054 → ময়মনসিংহ 2025 CQ Q1 (ভৌত
  জীববিজ্ঞান/চিত্র Q/R; part গ Q5-এর spillover); 5928 → question_number 1→4
  (Dinajpur 2022 set-04 CQ Q4, ডিকোডে "৪ নিচের চিত্রটি লক্ষ কর — চিত্র: A, চিত্র: B";
  part ক `ফিটাস কী?` (1 নম্বর) একই block থেকে উদ্ধার করা হয়েছে)।
- **TP 2021 bank:** রিপোর্টের বর্ণনা উল্টো ছিল — বেশিরভাগ row-তেই ছাপা নম্বরই আছে
  (26-50, 51-100, 101-125, 126-150, 151-175, 176-200); শুধু 6টা chunk-start
  প্রশ্ন (ছাপা 26/51/101/126/151/176) দুবার চাংক হয়েছে — একবার qnum=1 (row 449,
  475, 526, 552, 578, 603) আর একবার ছাপা নম্বরে (row 450, 476, 527, 553, 579, 628)।
  6টা qnum=1 row-ই possible-duplicate হিসেবে flag করা হয়েছে — ডিলিট করা হয়নি
  (stem/flag আলাদা, verified exact duplicate নয়) আর renumber করা হয়নি
  (ছাপা নম্বরে ইতিমধ্যে row আছে — collide করত)। বরিশাল 2021 Q155-এর কোনো row নেই,
  ডিকোড টেক্সটেও `১৫৫.` মার্কার নেই — শুধু ভিজ্যুয়াল চেকেই উদ্ধার সম্ভব।

### 3. য+়/য় trap — 325 row
- `board_name`-এ 239 row + `source`-এ 325 row (union 325)-এ `ময়মনসিংহ`-র য+়
  (U+09AF+U+09BC) → য় (U+09DF) করা হয়েছে। এখন board_name/source-এ য+় **0**।
  question_text/stimulus-এর ডিকোড-আর্টিফ্যাক্ট ছোঁয়া হয়নি (spec অনুযায়ী verbatim)।

### 4. Doc-twin check — 260 .doc/.docx, সবগুলোর PDF twin আছে
- প্রসেস: `soffice --headless --convert-to pdf` + শেয়ার্ড ডিকোড টুল দিয়ে decoded-text
  similarity যাচাই (`work/biology/doc_twin_convert_all.py`)।
- স্ট্যাটাস: **সম্পূর্ণ** — 260/260 PDF রূপান্তরিত, 260/260 similarity যাচাই করা
  হয়েছে; ফলাফল নিচে "Doc-twin check — ফলাফল (2026-11-25)" সেকশনে।

### 5. ডিলিট — 0 row
- Exact duplicate row: **0** (সব ফিল্ড হুবহু মিলিয়ে যাচাই)।
- Truly-empty placeholder: **0 ডিলিট** — content-খালি 477 row (qtext/options/guide/
  parts/stimulus/key/explanation সব খালি) পরীক্ষা করে রাখা হয়েছে: 407টা image-only
  CQ সেটের per-number রেকর্ড (question_number আছে) আর 70টা per-file audit row
  (TYPEWISE CQ/MCQ que+ans ও SAQ — প্রতি চ্যাপ্টারে ১টা করে, image-only ফাইলের
  বিবরণসহ)। এগুলো মুছলে ওই প্রশ্ন/ফাইলের একমাত্র রেকর্ড মুছে যেত — spec-এর
  "কোনো প্রশ্ন বাদ দেবে না" নিয়মের বিরুদ্ধে। সিদ্ধান্ত + 477টার id:
  `staging/ssc/biology/dropped-placeholders.json`। 587টা qtext+options+guide-খালি
  row-এর মধ্যে 110টায় verified answer_key আর 517টায় question_number আছে — রাখা হয়েছে।
- Relabel হওয়া 234 row-এর মধ্যে 20টায় possible-duplicate নোট যোগ করা হয়েছে
  (একই বোর্ড/সাল/নম্বর + একই stem, অন্য সোর্স ফাইলে) — flag-মাত্র, ডিলিট নয়।

### 6. যাচাই (normalization-এর পর)
- সব JSON parse হয় ✓; combined 28,069 = chapter ফাইল 27,018 + model-test ফাইল 1,051 ✓
- সব id unique, null নেই ✓; সব row 37 ফিল্ড ✓
- processed 537 (277 PDF + 260 doc) + missing 1 = **538 = ম্যানিফেস্ট** ✓
  (277 + 260 + 1 = 538); missing এখনো শুধু `Test paper/Biology16-22.pdf` (scanned, OCR লাগবে)
- flagged.json ⊆ combined, flagged count 28,069 = non-empty flag_note-ওয়ালা row ✓
- section সব spec-মাফিক (non-spec 0) ✓; board_name/source-এ য+় 0 ✓
- Spot-check (ডিকোড ফাইল চোখে পড়ে): Chaperwise MCQ2 ch1 Q1 (`আমাদের জাতীয় ফুলের
  প্রজাতির নাম কী?`), Model Test MCQ ch5 Q1, NEW UPDATE BASIC ch1 (`প্রথম অধ্যায়`) —
  তিনটাই decoded টেক্সটের সাথে মিলেছে ✓
- Per-file JSON 146টা আবার লেখা হয়েছে (id-membership অনুযায়ী, count অপরিবর্তিত) ✓

### বাকি সীমা
- B24 সিলেট 2024 MCQ (25 প্রশ্ন ডিকোড টেক্সটে আছে, লাইন 3647-3739) — Biology-2024.pdf
  থেকে কোনো row হয়নি (হেডারে `পদার্থবিজ্ঞান` ছাপা — বইয়ের ভুল); প্রশ্নগুলো
  `MCQ Board Question.pdf` থেকে আছে, তাই তথ্য হারায়নি — re-chunk দরকার।
- ডান-কলামের CQ সেট (Q5/Q6/Q8) অনেক পেপারে row হয়নি — chunker শুধু বাম-কলাম নিয়েছে
  (যেমন Mymensingh 2024 CQ Q5 খাদ্য-পিরামিড, Q6, Q8; Cumilla 2025 CQ Q5-এর
  উদ্দীপক row 1958-এ আটকে আছে) — re-chunk/OCR ছাড়া উদ্ধার হবে না।
- Chimeric CQ row (2-কলাম interleave): 1958 (Q1 parts + Q5 stimulus), 1961 (Q4
  stimulus + Q8 parts), 1962 (Q6 ক + Q2 parts), 1963/2056/2058 (fragment) — flag সহ রাখা হয়েছে।
- TP02: Mymensingh 2021 Q1-এর কোনো row নেই; Barishal 2021 Q155-এর row/marker নেই।
- Doc-twin: 14টা true duplicate যাচাই করা হয়েছে (skipped-ই থাকবে); 194টা twin-এ
  unique content আছে — 18,731 stemless row-এর stem ভরাট করা বাকি (নিচে
  "Doc-twin check — ফলাফল" সেকশন + `work/biology/doc-twin-stemfill-plan.md` দেখুন)।

## Doc-twin check — ফলাফল (2026-11-25)

- 260টা .doc/.docx-ই PDF-এ রূপান্তরিত হয়েছে (soffice, isolated profile) আর
  শেয়ার্ড ডিকোড টুল দিয়ে decoded-text similarity যাচাই করা হয়েছে
  (`work/biology/doc_twin_similarity.json`; ডিকোড টেক্সট:
  `work/biology/doc-twins-txt/`)।

| ফল | ডক | Twin PDF থেকে row | তার মধ্যে stemless |
|---|---|---|---|
| duplicate (যাচাই করা) | 14 | 172 | 0 |
| partial-overlap (twin-ই যথেষ্ট) | 52 | 5,984 | 72 |
| unique-content (stem ভরাট দরকার) | 194 | 18,936 | **18,731** |

- **14 duplicate:** Model Test CQ ch1,3,5–14 ও SSC27 CQ set-2, set-4 — দুই দিকেই
  পুরো টেক্সট আছে (jac 0.71–0.83) — skipped-ই থাকবে।
- **52 partial:** twin PDF ভালোভাবে chunk হয়েছে (5,912 row-তে stem আছে) —
  jac 0.35–0.69 শুধু ডিকোড-নয়েজ (Bijoy/layout পার্থক্য); আবার chunk করার দরকার নেই।
  এর মধ্যে 3টা answer sheet (TP Ans, Answer Sheet, Ans School) — 0 row, স্বাভাবিক।
- **194 unique:** twin PDF-র ডিকোড খুবই lossy (মিডিয়ান 2,146 অক্ষর, doc-এর
  মিডিয়ান 13,452) — লেকচার-গদ্য আর বেশিরভাগ MCQ stem twin-এ ওঠেনি, তাই
  18,731 row শুধু নম্বর+key নিয়ে আছে (17,500-এ key আছে)। উদাহরণ: Sheet ch5-এর
  twin থেকে 558 row (521 MCQ key-only + 34 CQ খালি), অথচ doc-এ পুরো stem আছে।
- **এই পাসে chunk করা হয়নি:** সরাসরি chunk করলে 18,731 key-only row ডুপ্লিকেট
  হতো — সঠিক কাজ stem-fill merge (doc থেকে stem নিয়ে existing row-তে ভরাট করা)।
  সেটা আলাদা ফলো-আপ কাজ; ডিজাইন + ফাইল-তালিকা:
  `work/biology/doc-twin-stemfill-plan.md`।
- রূপান্তর-ঘটনা: default LibreOffice profile-এ sibling subject-দের soffice-র
  সাথে ধাক্কা খেয়ে 40টা fail হয়েছিল; isolated profile-এ retry করে 36/39,
  বাকি 3টা (Board Question 23-25) আলাদা 900s রানে হয়েছে। VM replacement দুবার
  রান মেরেছে — স্ক্রিপ্ট resume-aware বলে ক্ষতি হয়নি।
