# SSC শারীরিক শিক্ষা — Lecture Sheets (chunked)

সাবজেক্ট: শারীরিক শিক্ষা (`saririk-shikkha`), Class 9-10, বই: `class9-10-saririk-shikkha-lecture`
মোট row: **2365** (flagged: 2071)

## Type ভাগ

- cq: 181
- lecture-note: 10
- mcq: 1728
- saq: 446

## অধ্যায় ভাগ

- অধ্যায় 1 (সুস্থজীবনের জন্য শারীরিক শিÿা): 213 rows {'lecture-note': 1, 'mcq': 154, 'saq': 40, 'cq': 18}; MCQ 154 (options 64, answer_key 64); flagged 189
- অধ্যায় 2 (শারীরিক সÿমতা): 203 rows {'lecture-note': 1, 'mcq': 149, 'saq': 37, 'cq': 16}; MCQ 149 (options 109, answer_key 109); flagged 183
- অধ্যায় 3 (মানসিক স্বাস্থ্য ও অবসাদ): 179 rows {'lecture-note': 1, 'mcq': 126, 'saq': 37, 'cq': 15}; MCQ 126 (options 101, answer_key 101); flagged 154
- অধ্যায় 4 (স্বাস্থ্যবিজ্ঞান ও স্বাস্থ্যসেবা): 205 rows {'lecture-note': 1, 'mcq': 149, 'saq': 38, 'cq': 17}; MCQ 149 (options 109, answer_key 109); flagged 177
- অধ্যায় 5 (স্বাস্থ্যের জন্য পুষ্টি): 195 rows {'lecture-note': 1, 'mcq': 136, 'saq': 42, 'cq': 16}; MCQ 136 (options 111, answer_key 111); flagged 181
- অধ্যায় 6 (মাদকাসক্তি ও এইডস): 286 rows {'lecture-note': 1, 'mcq': 205, 'saq': 54, 'cq': 26}; MCQ 205 (options 156, answer_key 156); flagged 250
- অধ্যায় 7 (বয়ঃসন্ধিকাল ও প্রজনন স্বাস্থ্য): 192 rows {'lecture-note': 1, 'mcq': 137, 'saq': 39, 'cq': 15}; MCQ 137 (options 94, answer_key 94); flagged 161
- অধ্যায় 8 (দলগত খেলা): 388 rows {'lecture-note': 1, 'mcq': 298, 'saq': 69, 'cq': 20}; MCQ 298 (options 271, answer_key 271); flagged 338
- অধ্যায় 9 (অ্যাথলেটিকস ও সাঁতার): 292 rows {'lecture-note': 1, 'mcq': 222, 'saq': 49, 'cq': 20}; MCQ 222 (options 175, answer_key 175); flagged 251
- অধ্যায় 10 (খেলাধুলার দুঘর্টনা): 212 rows {'lecture-note': 1, 'mcq': 152, 'saq': 41, 'cq': 18}; MCQ 152 (options 114, answer_key 114); flagged 187

## ফাইল তালিকা

প্রতি (অধ্যায়, type) এক ফাইল: `chapter-<NN>-<type>.json`।
Model-test ফাইল নেই — ১০টা ফাইলই চ্যাপ্টার শিট।
`.doc` ডুপ্লিকেট ১০টা (PDF-ই প্রধান, doc পড়া হয়নি)।

## বোর্ড/সাল ইনডেক্স

প্রযোজ্য নয় — লেকচার শিটে বোর্ড/সাল নেই (সব `board_name`/`board_year` null)।

## নোট

- ডিকোড: শেয়ার্ড টুল decode-pdf.py v2.1 (content-based Bijoy detection)।
- MCQ answer_key শুধু strict clean-run নিয়মে (এক লাইনে ৪ অপশন-টোকেন, ঠিক ১টা ●);
  বাকিগুলো null + flag — কখনো আন্দাজ করা হয়নি।
- ২-কলাম ইন্টারলিভের কারণে অনেক অপশন/উত্তর null + flag (বিস্তারিত report-এ)।

## নরমালাইজেশন (2026-11-24/25 পাস; বিস্তারিত report-এর শেষ সেকশনে)

- Schema sweep: সব row ৩৭ ফিল্ড, section = `lecture-<type>`, id প্যাটার্ন ও
  সব spec-ধ্রুবক (book_id, class_id 9, source_kind, verified_visual false)
  ঠিক আছে — কোনো section/type ফিক্স লাগেনি।
- য+় trap: ৪টা row-র flag_note-এ `ভূমিকায়` ভুলভাবে য+় (U+09AF+U+09BC) দিয়ে
  লেখা ছিল — য় (U+09DF) দিয়ে ঠিক করা হয়েছে (ch01/03/05/07 lecture-note-001);
  বোর্ড নাম সব null, তাই বোর্ড-ট্র্যাপ ফিক্স নেই। চাংকার parse-saririk.py-তেও
  একই ৫৪টা occurrence ঠিক করা হয়েছে।
- ১টা সত্যিকারের খালি placeholder বাদ দেওয়া হয়েছে:
  `saririk-shikkha-lec-ch05-mcq-129` (question_text, options, guide_solution
  তিনটাই null) — পুরো row `dropped-placeholders.json`-এ লগ করা আছে।
  ফলে মোট 2366 → 2365, flagged 2072 → 2071।
- Doc-twin যাচাই: ১০টা .doc-ই PDF twin-এর ডুপ্লিকেট প্রমাণিত (soffice-তে PDF-এ
  কনভার্ট + শেয়ার্ড টুলে ডিকোড + তুলনা) — কোনো unique কনটেন্ট নেই, chunk করা
  হয়নি, skipped-ই আছে। ব্যাকআপ: `_backup_pre_norm/`।
