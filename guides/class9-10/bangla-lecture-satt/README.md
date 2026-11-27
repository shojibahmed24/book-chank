# বাংলা (SSC Lecture Sheets) — Chunking README

**সাবজেক্ট:** বাংলা (slug: `bangla`) · **ক্লাস:** ৯–১০ · **সোর্স:** SSC Lecture Sheets (Google Drive)
**প্রথম পাস:** 2026-11-24 · **মেরামত + ফাইনাল পাস:** 2026-11-24 · **নরমালাইজেশন:** 2026-11-25 (পাস ২ — য+়/য় ফুল সুইপসহ) · **মোট row:** 22326 · **flag করা row:** 21233 (95%)
**প্রসেস করা ফাইল:** 926 · **মিসিং ফাইল:** 0 · **মোট ম্যানিফেস্ট:** 926

## আউটপুট ফাইল

| ফাইল | বর্ণনা |
|---|---|
| `questions-bangla.json` | সব row (22326), combined |
| `chapter-<NN>-<type>.json` | অধ্যায় × টাইপ ভাগে row (215 ফাইল) |
| `model-test/<set>.json` | মডেল টেস্ট সেট ভাগে row (24 সেট, 3325 row) |
| `flagged.json` | flag করা সব row (21233) |
| `stats.json` | সংখ্যা-সারাংশ (নরমালাইজেশন ব্লকসহ) |
| `dropped-placeholders.json` | বাদ দেওয়া row: 0 (কারণসহ) |
| `_backup_pre_norm/` | নরমালাইজেশনের আগের `questions-bangla.json` + `flagged.json` |
| `_backup_pre_trapsweep/` | পাস-২ (ফুল ট্র্যাপ সুইপ)-এর আগের `questions-bangla.json` + `flagged.json` |
| `processed-files.txt` / `missing-files.txt` | 926 + 0 = 926 |
| `report-2026-11-24.md` | এই রানের রিপোর্ট |
| `_work/answer-sheets/` | Chapterwise model q-র Anss উত্তর-তালিকা (sidecar, 0 row) |

## Row স্কিমা

স্পেসের ৩৭-ফিল্ড তালিকা অনুযায়ী:
`id, book_id, subject, subject_slug, class_id, chapter, chapter_number, chapter_name, section, type, set_id, question_text, question_number, stimulus, options, answer_key, answer_pointer, guide_solution, explanation, marks, marks_parts, marks_source, lesson, textbook_page, learning_outcome, source, source_kind, importance, out_of_syllabus, diagram_dependent, flag_note, guide_source, key_format, source_file, board_name, board_year, verified_visual`

- `book_id` = `class9-10-bangla-lecture`
- `chapter` = অধ্যায়ের বাংলা নাম (string); `chapter_number` = int; `chapter_name` = chapter-এর সমান
- `section` = `lecture-<type>` (বোর্ড row-র 1,529টি-তে `lecture-mcq` ছিল — 2026-11-25 নরমালাইজেশনে `lecture-board` করা হয়েছে; এখন বোর্ড row 2,795টি-ই `lecture-board`)
- `id` = `<slug>-lec-ch<NN>-<type>-<NNN>`; মডেল টেস্ট = `<slug>-lec-mt-<set>-<type>-<NNN>` (সব row-তে বসানো, combined-এ ইউনিক)
- `key_format`: `printed-marker` (●), `printed-letter` (trailing চ/ছ/জ/ঝ), `answer-key-table` (উত্তরমালা / Answer Sheet)
- উত্তর/মান কখনো আন্দাজ করা হয়নি — না জানলে `null` + flag

## অধ্যায় নম্বরিং (১ম পত্র ch01 ও ২য় পত্র ch01 যাতে না মেশে)

| রেঞ্জ | অর্থ |
|---|---|
| 01–16 | গদ্য (প্রত্যুপকার … শিক্ষা ও মনুষ্যত্ব) |
| 17–31 | পদ্য (বন্দনা … বসেখ) |
| 32 | সহপাঠ — কাকতাড়ুয়া |
| 33 | সহপাঠ — বহিপীর |
| 34 | সহপাঠ — ১৯৭১ |
| 51–93 | ২য় পত্র পরিচ্ছেদ N → 50+N (পরিচ্ছেদ ১–৪৩) |
| 00 | অজানা / পুরনো সিলেবাস / বোর্ড / লেখা অংশ (chapter_name-এ নাম থাকে, flag করা) |

## মেরামত (প্রথম পাসের ৩টি গঠনগত ত্রুটি) — 2026-11-24

1. **id null (18,983 row)** — সব row-তে spec-মাফিক id বসানো; combined-এ ইউনিক যাচাই করা।
2. **chapter_number 0 (11,837 row, 62%)** — source_file থেকে আবার বের করা: Grammar MCQ Sheet-এর `Chapter N` ফাইলগুলো `50+N` (প্রথম পাসে leading-digit বাগে সব 50 হয়েছিল — 2,069 row, 43 ফাইল); Topicwise টপিক ফাইলগুলো রোমানাইজড TOPIC2POR দিয়ে পরিচ্ছেদে ম্যাপ করা (parse.py-র TOPIC2POR বাংলা-কী দিয়ে রোমানাইজড ফাইলনাম মেলাতে পারত না); stem-ভিত্তিক ম্যাপে ১৪টি অনুপস্থিত রোমানাইজড কী যোগ করা (ovagirshorgo, pollishahitto, akattorerdingulo, amarporicoy, sahosijononi, jibonsonggit, manushmsw, amatirbhenpu, kaktarua, bohipir, kopotakkhonod, ondobodu, jornargan, bristy, tomakepawyarjonne, tomakpaoarjonne, amikonoaguntoknoi, sahitterruporiti)। Bakaron-IX-এর 33 সেকশন (1,630 row) আগের মতোই ch00-তে আছে।
3. **model-test দুই জায়গায়** — chapter-00-model-test.json-এর 1,643 row (83টি null-set row-সহ: 30টি ssc-2027-writing, 53টি model-test-combined-cq) model-test/<set>.json-এ সরানো; mt ফোল্ডারের 1,560টি row ছিল ওগুলোরই ডুপ্লিকেট; chapter-00-model-test.json মুছে ফেলা হয়েছে। এখন combined = chapter যোগফল + model-test যোগফল।
4. **same-content row (88 গ্রুপ, 480 row)** — full-row তুলনা: 112টি হুবহু ডুপ্লিকেট + 10টি fragment row (অপশন/উত্তর ছাড়া কাটা stem) বাদ দেওয়া; 36টি গ্রুপে আলাদা অপশন/উত্তর থাকায় সব row রাখা হয়েছে (বোর্ড CQ-র generic শিরোনাম `সৃজনশীল প্রশ্ন ১` ×18 — marks_parts আলাদা, আলাদা প্রশ্ন)।

## নরমালাইজেশন — 2026-11-25 (প্রি-পুশ)

ব্যাকআপ: `_backup_pre_norm/` (নরমালাইজেশনের আগের combined + flagged) · স্ক্রিপ্ট: `~/workspace/lecture-sheets/work/bangla/normalize.py` · লগ: `~/workspace/lecture-sheets/work/bangla/normalization-log.json` · যাচাই: `~/workspace/lecture-sheets/work/bangla/validate.py` (সব PASS) · কোনো row বাদ দেওয়া হয়নি (22,326 → 22,326)।

| কাজ | আগে | পরে |
|---|---|---|
| **1. বোর্ড section** | type=board + section=`lecture-mcq`: 1,529 | সব `lecture-board`; বোর্ড row 2,795টি-ই `lecture-board`, `lecture-mcq` 0 |
| **2. অধ্যায়ের নাম** | `chapter_name` null: 1,868 (সব ch00, 31টি সোর্স ফাইল) | 1,868-ই ভরা, null 0; `chapter_number` 0-ই আছে |
| **5. য+়/য় ট্র্যাপ** | সব ফিল্ডে য+় (U+09AF+U+09BC): ১,৪৯,১০৮টি occurrence, ১৬,৯১৭ row | **সব ফিল্ডে য+় 0** — পাস ২ ফুল সুইপ: question_text ৩৪,৭২২ + options ২৯,২৪৭ + guide_solution ২৯,৮০৬ + stimulus ১৫,২৩৬ + marks_parts ৩২,০৯৮ + flag_note ৭,৯৯৯ occurrence ঠিক; `board_name`-এ ট্র্যাপ 0 (সব রোমানাইজড) |
| **flag** | 16,914 (76%) | 21,233 (95%) — পাস ১-এ +৫১১, পাস ২-এ +৩,৮০৮টি আগে-আনফ্ল্যাগড trap row-তে flag যোগ হয়েছে |

**অধ্যায় ৪০–৫০ প্রসঙ্গে (গুরুত্বপূর্ণ সংশোধন):** নম্বর ৪০–৫০-এর কোনো row-ই নেই — নম্বরিং ৩৪ থেকে ৫১-এ লাফ দেয় (৩৫–৫০ ফাঁকা, ডিজাইন অনুযায়ী: ১–৩৪ প্রথম পত্র, ৫১–৯৩ দ্বিতীয় পত্রের পরিচ্ছেদ ১–৪৩)। null নামের আসল জনসংখ্যা ch00-এর ১,৮৬৮ row — পুরনো সিলেবাসের টপিক (Sheet / CHAPTERWISE MCQ Sheet / Chapterwise MCQ Sheet 2 ফাইল)। নাম ডিকোড করা সোর্সের হেডার/ফাইলনাম থেকে নেওয়া (যেমন `13. Ekattorer Dingulo OK.uni.txt`-এর হেডারে "একাত্তরের দিনগুলি / জাহানারা ইমাম")। পুরনো অধ্যায়-ক্রম (ত্রয়োদশ, পঞ্চদশ ইত্যাদি) বর্তমান ১–৩৪-এর সঙ্গে মেলে না বলে `chapter_number` 0-ই রাখা হয়েছে — নম্বর আন্দাজ করা হয়নি। ভরা নাম: আমার পরিচয় ২৮৩, একাত্তরের দিনগুলি ১৭০, সাহিত্যের রূপ ও রীতি ১৫৫, নিয়তি ১৫২, পয়লা বৈশাখ ১৪৪, জুতা আবিষ্কার ১৪০, বঙ্গবাণী ১৩৬, স্বাধীনতা এ শব্দটি কীভাবে আমাদের হলো ১২৮, আশা ১০৯, সাহসী জননী বাংলা ১০৬, পল্লিজননী ১০৫, জীবন-সঙ্গীত ৯৯, দেনাপাওনা ৯২, বাঙলা শব্দ ৪৭, পাখি ২। "পাখি" শুধু ফাইলনাম + উদ্দীপকের পাখি-প্রসঙ্গ থেকে (২ row)।

**য+় ট্র্যাপ — পাস ১-এর সিদ্ধান্ত সংশোধন (পাস ২, 2026-11-25):** পাস ১ শুধু নাম-ফিল্ড ঠিক করে প্রশ্ন/উত্তরের ট্র্যাপ "ডিকোড-ত্রুটি" বলে রেখে দিয়েছিল — সেটা ভুল ছিল। প্রমাণ: ডিকোড করা ৪৭৩টি `.uni.txt`-এ য+় **০টি** বনাম য় (U+09DF) **১,৮১,৬৩৬টি**; চাংকার `parse.py`-র `clean()`/`read_txt()` সব লেখায় plain `unicodedata.normalize('NFC', …)` চালাত, আর NFC U+09DF-কে য+়-এ ভেঙে দেয় (Python-এ যাচাই করা) — অর্থাৎ JSON-এর সব ট্র্যাপ চাংকারের তৈরি, ডিকোডের নয়। পাস ২-এ সব ফিল্ডে (question_text, options, guide_solution, stimulus, marks_parts, flag_note-সহ, nested dict/list-ও) য+় → য় করা হয়েছে: মোট ১,৪৯,১০৮ occurrence, ১৬,৯১৭ row; পরে য+় ০। চাংকার স্ক্রিপ্টও ঠিক করা হয়েছে — `parse.py`/`repair_final.py`/`extract_anss.py`-তে safe-NFC (NFC-র পর য+় → য় ফিরিয়ে আনা) + ম্যাপ/রেজেক্স লিটারালে থাকা ১২২টি কাঁচা য+় (parse.py ২১, repair_final.py ৯৪, extract_anss.py ৫, test_mcq2.py ১, twocol_v6.py ১) য়-তে বদলানো; সব `.py`-তে কাঁচা য+় এখন ০, `py_compile` OK, `read_txt()` এন্ড-টু-এন্ড যাচাইয়ে ডিকোড লেখা ট্র্যাপ-মুক্ত থাকে (Ekattorer Dingulo ফাইলে BAD ০, GOOD ৬২৪)। পাস ১-এর flag মার্কার নিজেই ট্র্যাপ-লিটারাল বহন করত বলে flag_note-র ট্র্যাপ ৫,৪৮৪ → ৭,৯৯৯ হয়েছিল; সেই পুরনো মার্কার ১,৪২৫ + ৫১১ row থেকে সরিয়ে ASCII-শুধু মার্কার (`trap-fixed: U+09AF U+09BC -> U+09DF in <fields>`) বসানো হয়েছে। আসল ডিকোড-ত্রুটি (যেমন `সূযার্স্ত্ম`, `বিশেস্নষণ`, `বণর্নামূলক`) হাত দেওয়া হয়নি — যেমন ডিকোডে আছে তেমনই আছে। `board_name`-এ কোনো বাংলা নাম নেই (dhaka, rajshahi… রোমানাইজড), তাই বোর্ড-নামে ফিক্স ০। নরমালাইজেশন স্ক্রিপ্টের প্রথম রানে NAME_MAP-এর ৩টি লিটারাল (পয়লা বৈশাখ, আমার পরিচয়, নিয়তি) ভুলবশত ট্র্যাপ-রূপে লেখা হয়েছিল (৫৭৯ row); দ্বিতীয় রানের trap পাস সেগুলো য়-তে ঠিক করেছে — চূড়ান্ত অবস্থা কোডপয়েন্ট দিয়ে যাচাই করা (সব ফিল্ডে য+় ০)।

**বাদ দেওয়া হয়নি:** `question_text`+`options`+`guide_solution` খালি এমন ১৪৪টি row পরীক্ষা করা হয়েছে — ১২৬টির `question_number` আছে, ৯টির `answer_key` আছে, ১৪৪টি-ই flag করা (no-stem/image-only/no-options) — এগুলো নথিভুক্ত আংশিক row (stem ছবিতে বা তিন-কলামে হারিয়েছে), স্পেসের "কোনো প্রশ্ন বাদ নয়" নিয়মে রাখা হয়েছে। হুবহু ডুপ্লিকেট 0।

**ছোঁয়া হয়নি (যাচাই করা):** জ্ঞানমূলক উত্তর-অমীমাংসিত ১,৩৫২ row (টাস্কে বলা ৭৮৮ পুরনো সংখ্যা — যাচাই করা বর্তমান সংখ্যা ১,৩৫২; সবগুলোর `guide_solution` null), তিন-কলাম stem-only ২৯৮ row, Bakaron-IX ch00 ১,৬৩০ row (source_file-এ `Bakaron` থাকা মোট ১,৭৫৮ row-র মধ্যে) — এগুলোর প্রশ্ন/উত্তর/উৎসের বিষয়বস্তু অপরিবর্তিত; পাস ২-এ শুধু য+় → য় trap ফিক্স (ডিকোডের লেখায় ফেরানো) + flag মার্কার যোগ হয়েছে যেখানে প্রযোজ্য (detrap-সচেতন যাচাইয়ে প্রমাণিত — `validate.py` ALL PASS)।

**ডক-টুইন যাচাই (টাস্ক ৪, চূড়ান্ত):** ৪৫৩টি .doc/.docx-র সবগুলো যাচাই করা — **DUPLICATE ৪২৭** (বাংলা containment ০.৯০১২–১.০০০, গড় ০.৯৮৮৬; skip সঠিক), **REVIEW ২৬** (ছবি-টুইন ১৭টি unique content — আলাদা chunking পাস লাগবে, তালিকা `~/workspace/lecture-sheets/work/bangla/doc-twin/review-image-twin-docs.txt`; borderline ৯টি আলাদা সংস্করণ/ডিকোড-ভেদ), **ERROR ০** (Bangla-1-2025.docx-এর প্রথম timeout-এর পর ১৭০০s retry সফল — REVIEW ০.৬৭ হিসেবে নথিভুক্ত)। বিস্তারিত রিপোর্টে (টাস্ক ৪)।

## ফাইনাল পাস — 2026-11-24

- মিসিং 261টি এন্ট্রির সবগুলো ডিস্কে পাওয়া গেছে: 130টি PDF ডিকোড + চাংক, 2টি Anss PDF উত্তর-তালিকা sidecar হিসেবে (`_work/answer-sheets/`, 0 row — Chapter-N row-র সঙ্গে positional pairing ভবিষ্যতের কাজ), 1টি doc-only ফাইল (Poddo 5. Model Test chapterwise/CQ/14. Tomake Paoar Jonne.docx) soffice-এ কনভার্ট করে চাংক, 130টি .docx twin processed-duplicate-doc।
- নতুন মডেল-টেস্ট সেট: `model-test-goddo-cq`, `model-test-goddo-mcq`, `model-test-poddo-cq`, `model-test-poddo-mcq`, `chapterwise-model-goodo`, `chapterwise-model-poodo` (Chapter-1..15 — অধ্যায় নম্বর source_file-এ আছে, mt row chapter_number 0-ই থাকে)।
- `Rochona July Rev.pdf` আসল লেখা (জুলাই বিপ্লব-২০২৪ রচনা) — writing-part হিসেবে চাংক করা হয়েছে, image-row নয়।
- মিসিং ফাইল এখন 0; processed + missing = 926।

## টাইপ ম্যাপিং (স্পেস + এক্সটেনশন)

- স্পেসের ম্যাপিং হুবহু; এক্সটেনশন: `writing-part` (Writing Part Sheet1/2), Sohopath BQ ফাইল → `board`, Sheet ফাইল → মিশ্র (lecture-note + mcq + cq, সেকশন ভাগে), NEW Bakaron → `mcq` (+ লেখা অংশ writing-part)
- `বর্ণনামূলক` প্রশ্ন = CQ-র মতো, তবে ২টি উপ-প্রশ্ন (ক/খ), ৪টি নয়; ডিকোডে `বণর্নামূলক` বানানও আছে

## ডিকোড (v2)

- সব PDF শেয়ার্ড টুল `decode-pdf.py` (v2) দিয়ে ডিকোড; 342 + 131টি `.uni.txt`
- v2 = কনটেন্ট-ভিত্তিক Bijoy শনাক্তকরণ (যেকোনো WinAnsi ফন্ট); 50%-এর নিচে বাংলা-লাইনের 21টি ফাইল v2 দিয়ে আবার ডিকোড করা হয়েছে — অনুপাত বদলায়নি (কাঠামোগত কারণ, ডিকোড ত্রুটি নয়)
- 20টি ফাইল 50%-এর নিচে: 11টি MCQ OLD (প্রশ্ন রাস্টার ছবি — OCR লাগবে), Writing Part Sheet1-এর 4টি (manpotro/abedon/Letter/rochona — ছবি/টেমপ্লেট), Answer Sheet, Amar Porichoy (দুই-কলামে ছোট লাইন বলে মেট্রিক কম দেখায়), Dhonitto.
- ডিকোড-ত্রুটির উদাহরণ (হাত দিয়ে ঠিক করা হয়নি): `চিন্তা→চিন্ত্মা`, `উল্লিখিত→উলিস্নখিত`, `বিশ্লেষণ→বিশেস্নষণ`, `আন্তর্জাতিক→আন্ত্মজাির্তক`, `গুরুত্বপূর্ণ→গুরম্নত্বপূণর্`, `বোর্ড→বোডর্`, `বর্ণনামূলক→বণর্নামূলক`

## উত্তর-উৎস (যাচাই করা)

- **● মার্কার** = সঠিক অপশনের অক্ষর (Grammar MCQ 43টি, Goddo/Poddo MCQ NEW-র বেশিরভাগ)
- **Trailing letter** চ=ক, ছ=খ, জ=গ, ঝ=ঘ — ● ground truth দিয়ে ৫ বার যাচাই করা (Bakaron-IX / NEW CHAPTERWISE MCQ)
- **উত্তরমালা টেবিল** (সংখ্যা-সারি + অক্ষর-সারি) — Goddo/Poddo MCQ-র একাংশ, মডেল টেস্ট
- **Answer Sheet** (K/L/M/N = ক/খ/গ/ঘ) — MCQ Board Question ফাইলের সঙ্গে (board, year, number) মিলিয়ে; 24টি board-year জোড়া
- **কোনো উত্তর-উৎস নেই** — CHAPTERWISE MCQ Sheet (11), Topicwise MCQ Sheet (24), MCQ-Model-Ans (সংখ্যা-গ্রিড আছে, অক্ষর নেই) → answer_key null + flag

## জানা সীমাবদ্ধতা (সব flag করা)

1. **জ্ঞানমূলক উত্তর মেলানো যায় না** — দুই-কলামে Q/A জোড়া পরস্পর-বিরোধীভাবে মিশে যায়; stem সঠিক, guide_solution null + `answer-unresolved-two-column` (788 row)
2. **তিন-কলাম লেআউট** (MCQ-Model 10 টেস্ট, বোর্ড MCQ) — দুই-কলাম ইঞ্জিন কলাম আলাদা করতে পারে না; MCQ-Model-এর 298টি stem নম্বর-মার্কার দিয়ে তোলা, অপশন/উত্তর null + `three-column-layout`; বোর্ড MCQ-র অপশন বেশিরভাগ অসম্পূর্ণ (raw-options সংরক্ষিত)
3. **বোর্ড MCQ অপশন** — অক্ষর ছাড়া শব্দ-তালিকা; line-based segmentation শুধু 4-লাইন অপশন-সেটে কাজ করে; বাকিগুলো `options-incomplete` + raw-options
4. **Bakaron-IX সেকশন-অধ্যায় ম্যাপ হয় না** — বইটি আলাদা/পুরনো বই (33 সেকশন); সব row ch00 + `section-chapter-unmapped` (1,630 row)
5. **MCQ OLD (14 ফাইল) + Writing Part Sheet1-এর 4টি** — প্রশ্ন ছবিতে; একটি করে flag-row, OCR লাগবে
6. **ছবি-ভিত্তিক PDF** — কিছু প্রশ্নের stem ছবিতে থাকায় 166টি row-এ question_text নেই (flag করা)
7. **দ্বিতীয় সেট** (Chapterwise MCQ Sheet 2-এর ০১।–২৫। মডেল টেস্ট অংশ) — আলাদা part হিসেবে পার্স করা, set_id + `-extra`, প্রথম সেটের key উত্তরাধিকার পায় না
8. **ডুপ্লিকেট প্রশ্ন** — একই প্রশ্ন-ব্যাংক একাধিক ফাইলে আছে; possible-duplicate flag (cross-file, আসল id দিয়ে)
9. **Final objecitve "2."-এর Q1** — stem-এ দুটি প্রশ্ন মিশে আছে (দ্বিতীয় প্রশ্নের stem আলাদা করা যায়নি — 1,516টি stem-এ 2+ `?` আছে, বেশিরভাগ বৈধ follow-up যেমন "নিচের কোনটি সঠিক?")
10. **Chapterwise model q-র উত্তর** — Anss.pdf-তে আছে কিন্তু Chapter-N row-র সঙ্গে positional pairing করা হয়নি (ভবিষ্যতের কাজ); sidecar `_work/answer-sheets/`-এ আছে

## ডুপ্লিকেট ফাইল (md5 যাচাই করা — একবার চাংক, বাকিগুলো processed-duplicate)

- `Bakaron-IX` == `Topicwise MCQ NEW UPDATE/NEW CHAPTERWISE MCQ1`
- `Board Question 2023-25/Bangla-1-2025` == `Test Paper/01.-SSC-Bangla-1st & 2nd-2025`
- `Goddo/3. Gyanmulok Sheet/Library` == `Goddo/4. Anudhaban Sheet/Library`

## যাচাই (ডেলিভারির আগে)

- সব JSON parse হয়; `questions-bangla.json` (22326) = chapter ফাইলগুলোর যোগফল (19001) + model-test ফাইলগুলোর যোগফল (3325) ✓
- id সব ইউনিক, null নেই ✓
- processed (926) + missing (0) = 926 = ম্যানিফেস্ট ✓
- সব row 37 ফিল্ড ✓
- 3টি ডিকোড ফাইল চোখে দেখা (ফাইনাল পাস): নিচে রিপোর্টে ✓
- GitHub-এ push করা হয়নি (অনুমোদন পরে)

