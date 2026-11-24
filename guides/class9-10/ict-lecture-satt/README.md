# তথ্য ও যোগাযোগ প্রযুক্তি (ICT) — SSC লেকচার শিট চাংকিং

- **বিষয়:** তথ্য ও যোগাযোগ প্রযুক্তি (slug: `ict`, class 9–10)
- **স্পেসিফিকেশন:** `~/workspace/lecture-sheets/chunk-spec.md`
- **ম্যানিফেস্ট:** `~/workspace/lecture-sheets/inventory/subjects/ict.json` — **১৬৫ ফাইল**
- **সোর্স:** `~/workspace/lecture-sheets/ssc-chapter-wise/1. SSC Common Subjects/5. SSC ICT/`
- **ডিকোড:** `~/workspace/lecture-sheets/decoded/ssc/ict/` (+ `_doc-twins/` — .doc/.docx থেকে soffice-কনভার্ট করা কপি)
- **আউটপুট:** এই ডিরেক্টরি (`staging/ssc/ict/`) — `questions-ict.json`, `flagged.json`, `chapter-*.json`, `model-test/*.json`
- **স্ট্যাটাস:** সম্পূর্ণ (first pass + final pass, ২০২৬-১১-২৪; নর্মালাইজেশন ২০২৬-১১-২৫ — নিচে দেখুন)। GitHub-এ push করা হয়েছে (guides/class9-10/ict-lecture-satt/)।

## চূড়ান্ত ফল (যাচাই করা, ডিস্কে — নর্মালাইজেশন-পরবর্তী)

| মাপ | সংখ্যা |
|---|---|
| মোট row | **৭,৭২৬** (আগে ৭,৭২৭; ১টি খালি placeholder বাদ) |
| MCQ | ৬,৯৮৬ |
| SAQ | ৩১৮ |
| Board | ২৬০ |
| CQ | ৮৯ |
| Lecture-note | ৪৮ |
| Handnote | ২৫ |
| Flagged row | ৬,৮৭৩ (আগে ৬,৮৭৪; বাদ পড়া row-টি flagged ছিল) |
| question_text নেই | ১২ → ১১ (বাদ পড়া row-টির question_text ছিল না) |
| answer_key আছে | ৩,১৪৮ (সব MCQ; printed-marker ২,৭৮০ + answer-key-table ৩৬৮) |
| ৪টি অপশন পূর্ণ MCQ | ২,৭০০ / ৬,৯৮৬ |
| stimulus আছে | ৩৯৫ |
| guide_solution আছে | ২৩৬ |
| id unique | হ্যাঁ (০ duplicate) |
| সব row ৩৭ field | হ্যাঁ |

অধ্যায়ভিত্তিক: ch1 ১,৪২৮ · ch2 ৮১৫ · ch3 ৮৬২ · ch4 ১,১৪১ (আগে ১,১৪২; খালি placeholder বাদ) · ch5 ১,৪৪৬ · ch6 ১,০৬৬; অধ্যায়-নম্বর নেই ৯৬৮টি (বোর্ড ২৬০ + মডেল-টেস্ট সেট MCQ ৭০৮)।
বোর্ড row বছরভিত্তিক: ২০১৭: ১, ২০১৮: ২, ২০১৯: ৩, ২০২০: ২, ২০২৩: ১০, ২০২৪: ১৭, ২০২৫: ২২৫ (৯ বোর্ড × ২৫)। বোর্ড row-এ উত্তর নেই (উত্তরমালায় শুধু নম্বর, অক্ষর নেই) — কখনো অনুমান করা হয়নি।

## ফাইল হিসাব (ম্যানিফেস্টের সাথে মিল)

- processed-files.txt: **১৩৭** (৭৬ PDF first pass + ৬১ doc/docx final pass)
- missing-files.txt: **০**
- _duplicates.txt: **২৮** (২০ doc/docx + ৮ PDF) — যাচাই করা ডুপ্লিকেট
- **১৩৭ + ০ + ২৮ = ১৬৫ = ম্যানিফেস্ট** ✓

## কী কী ফাইল আছে

- `questions-ict.json` — সব row (৭,৭২৬)
- `flagged.json` — flag_note আছে এমন সব row (৬,৮৭৩) — flagged ⊆ combined
- `chapter-01-mcq.json` … `chapter-06-*.json` (২৮টি) + `model-test/*.json` (৩৭টি) — যোগফল = combined
- `processed-files.txt`, `missing-files.txt`, `_duplicates.txt`, `_file-flags.json` (০-row / ছবি-ভিত্তিক ফাইলের কারণ)
- `_answer-keys/` — PDF answer-grid থেকে তোলা sidecar (সতর্কতা: এগুলো **অক্ষর-অবস্থান** অনুযায়ী index করা, প্রশ্ন-নম্বর অনুযায়ী নয় — key ভরতে ব্যবহার করা যাবে না)
- `chunk.py` (৬৯০ লাইন) + `parse.py` (৭২৭ লাইন) — first-pass chunker/parser; `parse.py`-তে ২০২৬-১১-২৪-এর ●-dot ফিক্স আছে (নিচে দেখুন)
- `_work_final/` — final-pass স্ক্রিপ্ট, লগ, ব্যাকআপ, ভ্যালিডেশন স্ক্রিপ্ট

## First pass (ব্যাহত, কিন্তু staging ভালো ছিল)

- ৩,৩৮৭ row (MCQ ২,৮৮৭, SAQ ১৫০, Board ২৬০, Lecture-note ৩১, CQ ৫৯), flagged ২,৯২৮, answer_key ৭৬১।
- ৭৬টি PDF প্রসেস করা; ৩৩টি PDF থেকে ০ row — বড় ছবি-ভিত্তিক MCQ ব্যাংক (Practice MCQ ch1–6, Hand Note, CQ/MCQ মডেল Q + Answer PDF) — এগুলোর প্রশ্ন .doc কপিতে ছিল।
- ৮৯টি এন্ট্রি ডুপ্লিকেট হিসেবে রাখা (৮১টি .doc/.docx + ৮টি PDF)।

## Final pass (২০২৬-১১-২৪) — কী যোগ হলো

মোট নতুন row ৪,৩৪০টি (gross ৪,৫৪০ − বোর্ড-২০২৫ dedupe-এ বাদ ২০০ PDF row)।

| উৎস | নতুন row |
|---|---|
| 2. Chapter Wise Practice MCQ ch1–6.doc (আসল প্রশ্ন ব্যাংক; PDF শুধু উত্তর-গ্রিড) | ১,৮৯৪ |
| NEW LECTURESHEET ৬টি .doc (লেকচার শিটের ভেতরের MCQ ব্যাংক) | ১,১৪০ |
| CHAPTERWISE MCQ MODEL Q ch1–5.doc | ৪৯২ |
| #SSC-2026 ICT-MCQ-1–10.docx + #SSC-2027 set-1–5.docx | ৩১৬ |
| 4. Model Test New Update chapter-1–5.docx + Model-6.docx | ২০৭ |
| Chapterwise model MCQ Chapter-1–6.doc | ৫৪ |
| Hand Note ch1–5.doc (গ্লসারি + সংক্ষিপ্ত প্রশ্নোত্তর) | ৬০ |
| CHAPTERWISE CQ MODEL Q ch1–5.doc | ৩০ |
| ICT-2025.docx (বোর্ড ২০২৫; PDF row-এর বদলে — নিচে দেখুন) | ২০০ (net ০, dedupe) |

**উত্তর ভরা (Answer-doc থেকে):** MCQ MODEL Q — ch1 ৮০/৯৭, ch2 ৩৮/৯৯, ch3 ৭৯/৯৮, ch4 ৬৬/৯৯, ch5 ৮২/৯৯; CQ সমাধান ৩০/৩০। ch2-তে same-number মিল মাত্র ৩/৯৯ — কারণ Q-doc আর Answer-doc-এর নম্বর +৬ অফসেটে আছে (A7=Q13, sim ১.০০) — best-match fill (sim ≥ ০.৮৫) দিয়ে আরও ৩৫টি ভরা হয়েছে।

**যাচাই করা ডুপ্লিকেট (০ row = স্কিপ):** ১. Chapter Wise Practise ch1–6.docx, ICT-2025.docx-এর বাইরে বাকি Board/TEST PAPER doc, Chapterwise mcq & saq.docx, NEW LECTURESHEET-এর কিছু — parse-and-compare করে ০ নতুন row পাওয়া গেছে বলেই ডুপ্লিকেট ধরা হয়েছে (শুধু নাম মিলিয়ে নয়)।

**বাদ পড়া / স্কিপ:** Hand Note ch6.docx — PDF ও docx দুটোতেই গার্বেজ (visual/OCR দরকার)। ICT-2024.pdf — স্ক্যান করা ছবি-PDF (decode rc=2), OCR দরকার।

## জানা সীমা (pre-push-এ দেখতে হবে)

1. **Practice MCQ ব্যাংক (১,৮৯৪ row):** দ্বি-কলাম মিশ্রণে stem-এ অন্য কলামের টুকরো ঢুকতে পারে; মাত্র ৪৪৪/১,৮৯৪-এর ৪টি অপশন পূর্ণ; key ১,২৯৮/১,৮৯৪ (৬৯%)। row-গুলোতে flag আছে।
2. **বোর্ড row-এ অপশন নেই (০/২৬০):** positional parse — stem + নম্বর আছে, অপশন লেবেল নেই। বোর্ড ২০২৫-এর ২০০টি PDF row বাদ দেওয়া হয়েছে — একই (board, year, number) স্লটে DOCX parse-এর stem পরিষ্কার (PDF stem-এ অন্য প্রশ্নের টুকরো জোড়া; প্রমাণ: stem গড় দৈর্ঘ্য PDF ১৩৯ বনাম DOCX ৪৬ অক্ষর; `?`/`।`-তে শেষ DOCX ১০৯/২০০ বনাম PDF ৩১/২০০)। প্রশ্ন হারায়নি — পরিষ্কার DOCX কপি আছে।
3. **১১১টি exact-text ডুপ্লিকেট গ্রুপ (২২৬ row):** একই প্রশ্ন ভিন্ন সেটে (যেমন SAQ অধ্যায়-ফাইল + মডেল-টেস্ট ফাইল) — dedupe_key সেট/অধ্যায়-ভিত্তিক বলে ডিজাইন অনুযায়ী রাখা হয়েছে; নতুন row-এ near-dup flag আছে (৮৩২টি)।
4. **MCQ MODEL Q ch2:** Answer-doc-এর ৬টি প্রশ্নের (Q94–99) Q-doc-এ কোনো counterpart নেই; Q-doc-এর Q7–Q12 (stimulus সেট) Answer-doc-এ নেই — ৬১টি row-এর key এখনো null + flagged।
5. **Sidecar key JSON-গুলো ভুল index-এ আছে:** `_answer-keys/`-এর key-গুলো অক্ষর-অবস্থান (letter position) অনুযায়ী, প্রশ্ন-নম্বর অনুযায়ী নয় — positional fill করলে ভুল key বসত; তাই ব্যবহার করা হয়নি (শুধু doc-এর নিজের ● marker ব্যবহার করা হয়েছে)।
6. **parse.py-তে dot-ফিক্স (২০২৬-১১-২৪):** ● যখন অপশন লেবেলের জায়গা নেয় (যেমন `● 1991`), তখন আগের parser key ধরতে পারত না — `body[li][pos-2:pos+1]` স্লাইসে ঠিক করা হয়েছে। Practice ch1-এর key ১৬৫ → ৩১২ হয়েছে এই ফিক্সে।
7. **near-dup pass-এর পারফরম্যান্স:** naive all-pairs difflib ৮+ মিনিটেও শেষ হয়নি — length + token-Jaccard pre-filter দিয়ে <১ মিনিটে নামানো হয়েছে (`finalpass.py`)।
8. **১১টি row-এ question_text নেই** (flagged; নর্মালাইজেশনে ১টি খালি placeholder বাদ — নিচে দেখুন)।

## নর্মালাইজেশন (২০২৬-১১-২৫)

ব্যাকআপ: `_backup_pre_norm/` — `questions-ict.json` + `flagged.json`-এর pre-norm কপি (md5 মিলিয়ে যাচাই করা)। স্ক্রিপ্ট: `~/workspace/lecture-sheets/work/ict/` (`sweep1.py`, `twin_check.py`, `normalize.py`, `validate_norm.py`); লগ: `_norm-log.json`, `dropped-placeholders.json`। shared decoder ছোঁয়া হয়নি; GitHub push হয়নি।

| মাপ | আগে | পরে |
|---|---|---|
| মোট row | ৭,৭২৭ | **৭,৭২৬** |
| MCQ | ৬,৯৮৭ | ৬,৯৮৬ |
| Flagged row | ৬,৮৭৪ | ৬,৮৭৩ |
| question_text নেই | ১২ | ১১ |
| বাকি type | অপরিবর্তিত | — |

### ১. স্কিমা/কনসিস্টেন্সি সুইপ — ক্লিন, কোনো section/type ফিক্স লাগেনি
- সব ৭,৭২৭ row ৩৭ field, spec-এর field set হুবহু; `section == lecture-<type>` সব row-এ; type সব allowed set-এ (`mcq/cq/saq/board/lecture-note/handnote`); id unique, null নেই।
- Chapter (২৮টি) + model-test (৩৭টি) ফাইলের যোগফল = combined; flagged ⊆ combined, সংখ্যা মিলেছে।
- CQ ৫৯টি row-এ `marks_parts`/`stimulus` নেই — যাচাই করে দেখা গেছে এগুলো NEW LECTURESHEET-এর সত্যিকারের সৃজনশীল সেট (উদ্দীপক `question_text`-এ, ক–ঘ অংশ টেক্সটে অসম্পূর্ণ); type `cq` সঠিক, আগে থেকেই flagged — বদলানো হয়নি।
- MCQ ৯৯৭টি row-এ options নেই — Practice MCQ ব্যাংকের জানা সীমা, সব flagged — type সঠিক।
- Exact duplicate row ০টি (সব field মিলিয়ে); ১১১টি exact-text গ্রুপ (২২৬ row) ভিন্ন সেটে একই প্রশ্ন — ডিজাইন অনুযায়ী রাখা হয়েছে, মোছা হয়নি।

### ২. ড্রপ — ১টি সত্যিকারের খালি placeholder
- `ict-lec-ch04-mcq-391` (ch4, question_number 85, source: `2. Chapter Wise Practice MCQ/chapter-4.doc`) — question_text + options + guide_solution সব null; শুধু নম্বর ৮৫ টিকে ছিল, ওই সোর্সে ৮৫ নম্বরের আর কোনো row নেই (parser shell row)। `dropped-placeholders.json`-এ লগ করা হয়েছে; `questions-ict.json`, `chapter-04-mcq.json`, `flagged.json` — তিন জায়গা থেকেই বাদ গেছে।

### ৩. য+়/য় ট্র্যাপ — বোর্ড নাম + মেটাডেটা ঠিক করা হয়েছে
- `board_name`-এ ২৮টি row-এ `ময়মনসিংহ` লেখা ছিল য+় (U+09AF U+09BC) দিয়ে — সবগুলো য় (U+09DF)-এ ঠিক করা হয়েছে; প্রতিটি row-এ flag_note-এ নর্মালাইজেশন নোট যোগ করা হয়েছে (২৮টি row-ই আগে থেকে flagged ছিল, তাই flagged সংখ্যা বাড়েনি)।
- একই trap চাংকার-তৈরি মেটাডেটায় আরও ছিল — `chapter`/`chapter_name` ৩,৩৭৪ row (মূলত "প্রোগ্রামিংয়ের মাধ্যমে সমস্যা সমাধান"), `source` ৩টি, `flag_note` ৮৭৭টি (মূলত "পাওয়া যায়নি"-তে "যায়নি"), আর চাংকার-তৈরি ৩টি বোর্ড সেকশন-হেডার `question_text` — সব একইভাবে ঠিক করা হয়েছে। সোর্স-টেক্সট field (`question_text` সাধারণভাবে, `guide_solution`, `stimulus`, `options`) ছোঁয়া হয়নি — ডিকোড-ত্রুটি যেমন আছে তেমনই রাখার নিয়মে।
- নোট: প্রথম রানে flag suffix-এই ভুল করে য+় টাইপ হয়ে গিয়েছিল — validation ধরে ফেলেছে (২৮টি flag_note-এ অবশিষ্ট), সাথে সাথে ঠিক করা হয়েছে; `_norm-log.json`-এ `post_fix_2026_11_25` হিসেবে লগ করা আছে।

### ৪. ডক-টুইন যাচাই (২০টি .doc/.docx + ৮টি PDF — সব skip বহাল)
- **Chapterwise mcq & saq .docx ×৬ + .pdf ×৬:** md5-তে byte-identical — `4. Model Test New Update/`-এর ইতিমধ্যে-চাংক করা ফাইলের কপি (প্রতিটা PDF থেকে ২৯–৩৮ row আছে)। skip নিশ্চিত।
- **TEST PAPER main file .doc ×২ + ICT.doc + TP-21-24 .pdf:** md5-তে byte-identical; chunk করা twin `TEST PAPER/ICT main file.pdf` processed-files-এ আছে, তা থেকে ১১টি header row এসেছে। doc-এর ডিকোড করা টেক্সটে ০টি বাংলা প্রশ্ন-মার্কার, ০টি ক)/খ)/গ)/ঘ) অপশন-মার্কার, কাঁচা Bijoy টুকরো — টেক্সট থেকে chunk করা যায় না (PDF twin-ও একই অবস্থা)।
- **Board-Que.-Solution-2025-PDFCP.pdf:** ডিকোড করা টেক্সট ICT-2025.pdf-এর সাথে difflib ১.০০ / Jaccard ১.০০ — একই কনটেন্ট, ইতিমধ্যে chunk করা। skip নিশ্চিত।
- **CQ/MCQ Answer .doc ×১০:** PDF twin-এ টেক্সট প্রায় নেই (ছবি-ভিত্তিক: MCQ Answer ch1-এ doc ১,৪৮৯ বনাম PDF ২৫৬ বাংলা লাইন) — doc-গুলো উত্তর-সোর্স হিসেবে ব্যবহৃত হয়েছে, প্রশ্ন-সোর্স হিসেবে নয়। খরচ যাচাই: MCQ MODEL Q ৩৪৫/৪৯২ key ভরা, CQ MODEL Q ৩০/৩০ সমাধান ভরা। নতুন প্রশ্ন-row chunk করার কিছু নেই।
- **Hand Note ch6.docx:** doc ও PDF দুটোতেই গার্বেজ — চোখে পড়ে দেখা হয়েছে (অক্ষর ছড়ানো, `%` artifact: "৬ষ্ঠ অধ্যা য়: প্রো গ্রা মিং য়েয়র…")। visual/OCR ছাড়া chunk করা যাবে না; skip বহাল।
- **ফল:** কোনো twin থেকে নতুন row chunk করা হয়নি — সব skip যাচাই করে সঠিক পাওয়া গেছে।

### ৫. যাচাই (validation — ২৩/২৩ PASS)
- সব ৬৭টি JSON parse হয়; combined (৭,৭২৬) = chapter ফাইল যোগফল (৫,৯৩৩) + model-test যোগফল (১,৭৯৩); id unique, null নেই; সব row ৩৭ field; processed (১৩৭) + missing (০) + duplicate (২৮) = ১৬৫ ✓; flagged.json ⊆ combined এবং flagged সংখ্যা (৬,৮৭৩) = non-empty flag_note-ওয়ালা row; part-ফাইলের row combined-এর row-এর সাথে হুবহু মিলেছে; pre-norm flagged row সব এখনো flagged; ব্যাকআপ অক্ষত (৭,৭২৭ row, বাদ পড়া row-সহ)।
- ৩টি decoded ফাইল চোখে পড়ে যাচাই: Practice MCQ ch1 .doc-এর Q9 ("একুশ শতকে এসে…") → row `ict-lec-ch01-mcq-511`, key ক; NEW LECTURESHEET T-34 PDF-এর "ই-লানির্ং" → ৮টি lecture-note row; ICT-2025.docx-এর "ঢাকা বোর্ড-২০২৫" হেডার → Dhaka Q1 row `ict-lec-ch00-board-302`।

### নর্মালাইজেশন-পরবর্তী জানা সীমা
1. **২০২৩/২০২৪ বোর্ড প্রশ্ন নেই:** ২০২৫-এর আগের ৩৫টি বোর্ড row সবই সেকশন-হেডার (question_number/options নেই); ২০২৫-এর ২২৫টি row-ই আসল প্রশ্ন। TEST PAPER/ICT.doc twin-ও টেক্সট থেকে উদ্ধার করা যায় না (উপরে দেখুন) — ২০১৮–২০২৪ পেপারের প্রশ্ন পেতে visual/OCR পাস লাগবে।
2. **Practice MCQ ব্যাংক, বোর্ড-২০২৫ dedupe, MODEL Q ch2** — আগের সীমাগুলো অপরিবর্তিত (উপরে "জানা সীমা" দেখুন)।
