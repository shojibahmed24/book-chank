# কৃষি শিক্ষা (SSC) — Lecture Sheets চাংকিং

- **সাবজেক্ট:** কৃষি শিক্ষা (slug: `agriculture`)
- **ক্লাস:** ৯–১০ (SSC)
- **সোর্স:** `1. SSC Common Subjects/8. SSC Aggriculture` (ফোল্ডারের বানান "Aggriculture")
- **স্পেস:** `~/workspace/lecture-sheets/chunk-spec.md` (v1 + v2 ডিকোডার নিয়ম)
- **তারিখ:** ২০২৬-১১-২৪

## মোট

| ধরন | row | flag করা |
|---|---|---|
| board (বোর্ড প্রশ্ন ২০২৩/২০২৪/২০২৫) | ৮৯১ (MCQ ৬৭৫ + CQ ২১৬) | ৮৯১ |
| cq (মডেল টেস্ট ৮৬ + Chapter Wise Sheet ২১৪) | ৩০০ | ৮৪ |
| mcq (মডেল টেস্ট ২২৫ + Chapter Wise Sheet ২,৭৫৪) | ২,৯৭৯ | ১৫৯ |
| saq (সংক্ষিপ্ত প্রশ্ন ৩৩৯ + Practical মৌখিক প্রশ্নোত্তর ৪১৫) | ৭৫৪ | ৪০ |
| lecture-note (১০টি পরীক্ষণ + ২টি ব্যবহারিক নির্দেশনা) | ১২ | ৫ |
| **মোট** | **৪,৯৩৬** | **১,১৭৯ (২৪%)** |

- **প্রসেস করা PDF:** ৪২টি (সব)
- **মিসিং:** ০
- **.doc/.docx twin:** ৪০টি — ৩১টি যাচাইকৃত ডুপ্লিকেট (বাদ), ৯টি unique (Chapter Wise Sheet ch1–7 + Combined + Practical — চাংক করা হয়েছে, নিচে দেখুন)

## ফাইল

- `chapter-01..07-saq.json` — অধ্যায়ভিত্তিক সংক্ষিপ্ত প্রশ্ন (১৪৩/১৫১/১২০/১৬৮/৬৬/৪১/৩০ — আগের ৫৫/৫৩/৫২/৭৬/৩৪/১৯/১৫ + Practical মৌখিক প্রশ্নোত্তর ৮৮/৯৮/৬৮/৯২/৩২/২২/১৫)
- `chapter-01..07-cq.json` — Model Test CQ (প্রতিটায় ৫) + Chapter Wise Sheet CQ (৩০/৩০/৩০/৪৬/৩০/১৪/২২) — মোট ৩৫/৩৫/৩৫/৫১/৩৫/১৯/২৭
- `chapter-00-cq.json` — Combined.doc-এর ১২টি CQ সেট
- `chapter-01..07-mcq.json` — Chapter Wise Sheet MCQ (৪০৮/৪৭৫/৩৮২/৮৪৪/২৭১/১৭৬/১৯৮; ২,৭৪২টি keyed)
- `chapter-01/02/04/05-lecture-note.json` — Practical.doc-এর ১০টি পরীক্ষণ (পূর্ণ বিবরণ; ch1 ৩টি, ch2 ৩টি, ch4 ২টি, ch5 ২টি) — আগে PDF-খণ্ড practical row ছিল, .doc row দিয়ে বদলানো হয়েছে
- `chapter-00-board.json` — বোর্ড প্রশ্ন ২০২৩/২০২৪/২০২৫ (৯ বোর্ড × ৩ বছর)
- `chapter-00-lecture-note.json` — ২টি নির্দেশনা row (ব্যবহারিক নির্দেশনা + মৌখিক নির্দেশাবলি)
- `model-test/2026-mcq-1..7-mcq.json` — MCQ ২০২৬ (প্রতিটায় ২৫)
- `model-test/2027-mcq-model-1/2-mcq.json` — MCQ ২০২৭ (প্রতিটায় ২৫)
- `model-test/2026-cq-1/2-cq.json` — CQ ২০২৬ (প্রতিটায় ৮ সেট)
- `model-test/2027-cq-model-1..5-cq.json` — CQ ২০২৭ (প্রতিটায় ৭ সেট)
- `model-test/2027-cq-model-1..5-saq.json` — সংক্ষিপ্ত প্রশ্ন ২০২৭ (প্রতিটায় ৭)
- `questions-agriculture.json` — সব row একসাথে (৪,৯৩৬)
- `flagged.json` — flag করা row (১,১৭৯)
- `dropped-placeholders.json` — নরমালাইজেশনে বাদ দেওয়া placeholder-এর লগ (০টি — কোনো row-ই খালি placeholder শর্ত মেলেনি)
- `processed-files.txt` / `missing-files.txt` — ৪২ / ০
- `_work/` — পার্সার স্ক্রিপ্ট (অডিটের জন্য; push-এর বাইরে)
- `_work/normalization-2026-11-24.json` — নরমালাইজেশনের প্রতি-row সিদ্ধান্তের লগ
- `_work/integration-2026-11-24.json` — doc-twin চাংক ইন্টিগ্রেশনের লগ (বাদ/বদল id-সহ)
- `_work/validation-2026-11-24.json` — ইন্টিগ্রেশন-পরবর্তী যাচাইয়ের ফলাফল
- `_work/twin_check/` — .doc/.docx twin-যাচাইয়ের ফলাফল (`results.json`, `results-v2.json`) ও কনভার্ট করা PDF/ডিকোড করা টেক্সট
- `_work/chunk-doc/` — unique ৯টি doc-এর চাংকিং স্ক্রিপ্ট ও নতুন row (`new-rows-ch00..07.json`, `new-rows-practical.json`)
- `_backup_pre_norm/` — নরমালাইজেশনের আগের `questions-agriculture.json` + `flagged.json`
- `_work/_backup_pre_integration/` — ইন্টিগ্রেশনের আগের per-file JSON স্ন্যাপশট

## নরমালাইজেশন (২০২৬-১১-২৪)

- **মোট row: ১,৫৫৯ → ৪,৯৩৬** (নরমালাইজেশনে অপরিবর্তিত ১,৫৫৯; তারপর doc-twin চাংকে +৩,৩৯৫, বাদ ১৮ — নিচে দেখুন)।
- **type ম্যাপিং (১৮টি row):** `practical` ১০টি + `chapter-wise-sheet` ৮টি → `lecture-note` (section `lecture-lecture-note`)। কোনোটিই `saq` নয় — practical row-গুলো পরীক্ষণের শিরোনাম + আংশিক বিবরণ/"নমুনা চিত্র" খণ্ড (উত্তর নেই, diagram-নির্ভর), chapter-wise-sheet row-গুলো শিরোনাম + MCQ উত্তর-অক্ষরের গ্রিড/বিষয়-সংক্ষেপ নোট-ব্লক (প্রশ্ন নয়) — দুটোই স্পেসের lecture-note আকৃতির (এক শিরোনাম-সেকশনে এক row; question_text=শিরোনাম, guide_solution=সেকশনের লেখা)। প্রতি-row যুক্তি `_work/normalization-2026-11-24.json`-এ। row id অপরিবর্তিত রাখা হয়েছে — নাম বদলালে সংঘর্ষ হতো (অধ্যায় ১-এ practical-001..003 ও chapter-wise-sheet-001 দুটোই `lecture-note-001` হতো)।
- **ফাইল নাম:** স্পেসের `chapter-<NN>-<type>.json` নিয়মে `chapter-01..07-chapter-wise-sheet.json` → `chapter-01..07-lecture-note.json`; `chapter-00-practical.json` (১০) + `chapter-00-chapter-wise-sheet.json` (১) একত্রিত হয়ে `chapter-00-lecture-note.json` (১১)।
- **য+়/য় trap (৪,৮০৯টি প্রতিস্থাপন):** সব row-তে য+় (U+09AF+U+09BC) → য় (U+09DF) — শুধু codepoint ঠিক করা, দেখতে একই লেখা। ভাগ: flag_note ৪,৪৭১, chapter_name ১২৩, board_name ৯৯, source ৯৯, question_text ১৭। `board_name` "ময়মনসিংহ" (ভুল) → "ময়মনসিংহ" (সঠিক) — ৯৯টি board row (৩ বছর × ৩৩); chapter_name "কৃষি ও জলবায়ু" ও "বনায়ন"-ও ঠিক হয়েছে। মূল কারণ চাংকারে: `_work/agri_board.py:50`-এ `norm_board_name()` উল্টো ম্যাপ করছিল (সঠিক → ভুল); ঠিক করা হয়েছে (ভুল → সঠিক)। চাংকারের আরো ৮৪টি হাতে-লেখা flag-স্ট্রিং লিটারেল ঠিক করা হয়েছে (agri_board.py ২৪, agri_build.py ৫০, agri_parse5.py ৭, agri_saq.py ৩)। `BOARD_HDR_RE` রেগেক্সে ভুল রূপটি ইচ্ছাকৃত রাখা হয়েছে (ডিকোড করা সোর্স-টেক্সটে ভুল রূপ থাকলে ম্যাচ করবে বলে) — তবে যাচাইয়ে দেখা গেছে ৪২টি ডিকোড করা `.uni.txt`-এর কোনোটিতেই য+় নেই (সব য় সঠিক), অর্থাৎ trap-টি পুরোপুরি চাংকারের হাতে-লেখা লিটারেল থেকে এসেছিল, ডিকোডার থেকে নয়।
- **flag অপরিবর্তিত:** ১,০৬৫টি row-ই flag-সহ আছে (১৮টি ম্যাপ করা row-সহ); কোনো flag মুছে ফেলা হয়নি।
- **ডিকোড-ত্রুটি হুবহু রাখা হয়েছে** — হাতে বানান ঠিক করা হয়নি (যেমন "চিন্ত্মা", "শিÿা", "বোডর্")।

## Doc-twin চাংকিং + ইন্টিগ্রেশন (২০২৬-১১-২৪)

- **Twin যাচাই (৪০টি .doc/.docx):** soffice PDF-রূপান্তর + শেয়ার্ড ডিকোডার, বাংলা-স্ক্রিপ্ট টোকেন metric (raw Jaccard ভুল দেখায় — একই শিটেরও ০.৪১–০.৫১)। **DUPLICATE ৩১টি** (সব .docx — CQ+MCQ/Model Test/SAQ; overlap ০.৯৬–১.০০) — বাদ। **UNIQUE ৯টি** (Chapter Wise Sheet ch1–7 + Combined + Practical; বাংলা-টোকেন coverage ~০.০১–০.০২, দৈর্ঘ্য ১২–৬৮×) — চাংক করা হয়েছে।
- **চাংকিং:** `soffice --convert-to txt` + bijoy2unicode (PDF-রাউন্ড-ট্রিপ নয় — ● চিহ্ন ও পড়ার ক্রম অক্ষত থাকে)। নতুন row **৩,৩৯৫টি**: MCQ ২,৭৫৪ (২,৭৪২ keyed, ৯৯.৬%), CQ ২১৪, SAQ ৪১৫ (Practical মৌখিক প্রশ্নোত্তর — আগের SAQ-র সাথে ০ overlap), lecture-note ১২। স্ক্রিপ্ট: `_work/chunk-doc/chunk_doc.py`, `_work/chunk-doc/chunk_practical.py`, `_work/chunk-doc/bijoy_convert.py`।
- **ইন্টিগ্রেশন:** নতুন `chapter-01..07-mcq.json` + `chapter-00-cq.json`; CQ/SAQ append; **বাদ ১৮টি row** (৮ chapter-wise-sheet placeholder + ১০ PDF-খণ্ড practical row — পূর্ণ .doc row দিয়ে বদল)। Practical পরীক্ষণ ৭–১০-এর অধ্যায় সংশোধন (আগের id ch02 দেখাত; আসলে ch04/ch05)। হিসাব: ১,৫৫৯ + ৩,৩৯৫ − ১৮ = **৪,৯৩৬**; flag ১,০৬৫ − ১৮ + ১৩২ = **১,১৭৯**। লগ: `_work/integration-2026-11-24.json`; ইন্টিগ্রেশন-আগের স্ন্যাপশট: `_work/_backup_pre_integration/`।
- **নিজের চাংকারে trap ফিরে আসা (ধরা + ঠিক):** নতুন row-তে প্রথমে য+় পাওয়া গেছে — আমার হাতে-লেখা বাংলা লিটারেল থেকে (CHAPTERS dict, flag-স্ট্রিং)। ঠিক: dump-সময়ে `detrap()` (য+় → য়) + রেগেক্সে `\u09df` escape। যাচাই: combined-এ trap **০টি**। শিক্ষা: কোডে বাংলা য় সরাসরি টাইপ নয়।
- **ইন্টিগ্রেশন-পরবর্তী যাচাই (সব পাস, `_work/validate.py`):** ৫১টি JSON parse; combined ৪,৯৩৬ = chapter ৪,৬২৫ + model-test ৩১১; id unique, সব row ৩৭ ফিল্ড; flagged ১,১৭৯ ⊆ combined; trap ০; স্পট-চেক ৩টি (ch3 MCQ-001, ch1 CQ-006, ch1 oral SAQ-056) সোর্সের সাথে মেলে।
- **অবশিষ্ট সীমা:** chapter-doc-এর SAQ/রচনামূলক সেকশন চাংক হয়নি; ৫৯টি CQ সেটে ছাপা উত্তর নেই; চিত্র/ছক-নির্ভর item (CQ ৪ সেট + পরীক্ষণ ৫টি); ch7-এ CQ নম্বর ১২ দুবার; ●-বিহীন ১০টি MCQ-তে answer_key null; board answer_key ০/৮৯১। বিস্তারিত report-2026-11-24.md §৩ ও §৫-এ।

## অধ্যায়

| # | নাম |
|---|---|
| ১ | কৃষি প্রযুক্তি |
| ২ | কৃষি উপকরণ |
| ৩ | কৃষি ও জলবায়ু |
| ৪ | কৃষিজ উৎপাদন |
| ৫ | বনায়ন |
| ৬ | কৃষি সমবায় |
| ৭ | পারিবারিক খামার |

## নিয়ম (সিদ্ধান্ত)

- **উত্তর/মান কখনো আন্দাজ নয়** — না জানলে `null` + flag। বোর্ড MCQ-র `answer_key` সব `null` (উত্তরমালায় শুধু নম্বর, অক্ষর নেই)।
- **বোর্ড MCQ অপশন:** অক্ষর-চিহ্ন ছাড়া ছাপা। সমান-শব্দ ভাগে বিভক্ত করা হয়েছে শুধু যখন টোকেন সংখ্যা ৪ দিয়ে ভাগ যায়; না হলে `options=null` + raw টেক্সট `guide_solution`-এ + flag। পুনরুদ্ধার ২৫৩/৬৭৫ (৩৭%)।
- **মডেল-টেস্ট MCQ `answer_key`:** শুধু পরিষ্কার row-তে (৪ অপশন, অপশন-ত্রুটির flag নেই)। ১৫১/২২৫-এ আছে।
- **CQ marks:** প্রতি part ১/২/৩/৪ (SSC নিয়ম); ২০২৬-এ ছাপা নয় বলে `marks_source=null`, ২০২৭/MT-CQ-তে "প্রতিটির মান—১০" ছাপা আছে বলে `marks_source="printed"`।
- **ডিকোড ত্রুটি হুবহু রাখা হয়েছে** — হাতে বানান ঠিক করা হয়নি (যেমন "চিন্ত্মা", "শিÿা", "বোডর্")।
- **row id:** `<slug>-lec-ch<NN>-<type>-<NNN>`; মডেল টেস্ট `<slug>-lec-mt-<set>-<type>-<NNN>`; বোর্ড `<slug>-lec-ch00-board-<year>-<NNN>`।
- **৩৭ ফিল্ড** (স্পেসের "৩৪ ফিল্ড" লেবেলটি ভুল — ফিল্ড তালিকায় ৩৭টি আছে)।

## বড় সমস্যা (বিস্তারিত report-2026-11-24.md-এ)

1. বোর্ড MCQ-র উত্তর অক্ষর ডিকোডে নেই — ৬৭৫টির `answer_key` সব `null`।
2. Chapter Wise Sheet (৮ ফাইল) — প্রশ্নের stem ডিকোড হয়নি, শুধু উত্তরের অক্ষরের গ্রিড; OCR লাগবে।
3. MCQ দুই-কলাম মিশ্রণ — ১১৬টি row flag; ১২টি যাচাই করা সংশোধন প্রয়োগ করা হয়েছে।
4. বোর্ড ২০২৫ যশোর MCQ পেপারের হেডারে "জীববিজ্ঞান (বিষয় কোড ১৩৮)" লেখা — ভুল লেবেল, প্রশ্ন কৃষির; flag করা হয়েছে।
5. CQ ২০২৬-২-এ সমাধানের নম্বর ভুল ছাপা (দুটি "৫নম্বর", "৪নম্বর" নেই) — ক্রম অনুযায়ী বসানো হয়েছে।
