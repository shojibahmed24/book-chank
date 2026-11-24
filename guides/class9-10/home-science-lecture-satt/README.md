# গার্হস্থ্য বিজ্ঞান — SSC Lecture Sheets চাংক

- বিষয়: গার্হস্থ্য বিজ্ঞান (slug: `home-science`)
- বই: `class9-10-home-science-lecture`, শ্রেণি ৯
- তারিখ: ২০২৬-১১-২৪
- উৎস: `1. SSC Common Subjects/9. SSC Home Science` (ড্রাইভ ফোল্ডার)
- ম্যানিফেস্ট: `~/workspace/lecture-sheets/inventory/subjects/home-science.json`
- ডিকোড করা টেক্সট: `~/workspace/lecture-sheets/decoded/ssc/home-science/`

## মোট

| ধরন | রো |
|---|---|
| বোর্ড (board) | ১২৩ |
| সৃজনশীল (cq) | ৫৪ |
| বহুনির্বাচনি (mcq) | ১০০ |
| সংক্ষিপ্ত-উত্তর (saq) | ২১ |
| ব্যবহারিক (practical) | ২৪ |
| **মোট** | **৩২২** |

- flag করা রো: ১৯৪ (`flagged.json` দেখো) — আগের ১০৪ + ৯০টি বোর্ড রো যাতে শুধু
  `board-kind: mcq/cq` নোট আছে (নিচে নরমালাইজেশন দেখো)
- প্রসেস করা PDF: ৩৪টি (১৫টি থেকে রো বেরিয়েছে; ১৯টি ছবি-কনটেন্ট, OCR দরকার — `image-only-files.txt`)
- মিসিং ফাইল: ০ (ম্যানিফেস্ট ৬৬ = ডিস্ক ৬৬)
- .doc/.docx: ৩২টি — সবগুলো যাচাই করা হয়েছে (নিচে নরমালাইজেশন দেখো):
  ১৪টি সত্যিকারের ডুপ্লিকেট (PDF-র একই লেখা), **১৮টি অধ্যায়-doc-এ নতুন লেখা আছে**
  (অধ্যায় ১–১৮, ~২,৫৫০টি প্রশ্ন) — চাংক করা বাকি, আলাদা পাস লাগবে

## নরমালাইজেশন (২০২৬-১১-২৪ ~১৯:০০)

- **বোর্ড সেকশন ঠিক করা:** ১২৩টি বোর্ড রো `board-mcq` (৭৫) / `board-cq` (৪৮)
  থেকে `type="board"` + `section="lecture-board"` হয়েছে (agriculture/biology-র
  কনভেনশন অনুযায়ী); প্রশ্নের ধরন `flag_note`-এ `board-kind: mcq/cq` হিসেবে রাখা
  হয়েছে — ৯০টি রো-তে নতুন flag, ৩৩টি আগের-flag রো-তে append। রো সংখ্যা অপরিবর্তিত (৩২২)।
- **য়-ট্র্যাপ ঠিক করা:** decomposed য+় (U+09AF+U+09BC) → য় (U+09DF), ২৬৯টি
  occurrence, ১৬০টি ফিল্ড, ৮৪টি রো (শুধু `source`/`chapter_name`/`answer_pointer`/
  `flag_note` ফিল্ডে ছিল; `board_name` লাতিন-অক্ষরে লেখা বলে সেখানে ট্র্যাপ ছিল না)।
  NFC দিয়ে হয় না (যাচাই করা) — সরাসরি প্রতিস্থাপন করা হয়েছে; পার্সার স্ক্রিপ্ট
  (`parse-home-science.py`, `build-home-science.py`)-এর ১৭+১৫টি literal-ও ঠিক করা হয়েছে।
- **ব্যাকআপ:** নরমালাইজেশনের আগের combined + flagged
  `_backup_pre_norm/`-এ রাখা আছে। কোনো রো মোছা/যোগ করা হয়নি; `answer_key` ০টি বদল।
- যাচাই: সব JSON parse হয়; per-file যোগফল ৩২২ = combined ৩২২; ০ duplicate id;
  সব রো ৩৭ ফিল্ড; flagged.json ⊆ combined, flagged ১৯৪ = flag_note আছে এমন রো।

## ফাইল তালিকা

| ফাইল | রো | বিবরণ |
|---|---|---|
| `model-test/ssc-2026-mt1-cq.json` | ৮ | SSC-2026 মডেল টেস্ট ১, সৃজনশীল, ছাপা উত্তরসহ |
| `model-test/ssc-2026-mt2-cq.json` | ৮ | SSC-2026 মডেল টেস্ট ২, সৃজনশীল, ছাপা উত্তরসহ |
| `model-test/ssc-2026-mt1-mcq.json` | ২৫ | SSC-2026 মডেল টেস্ট ১, MCQ, উত্তরমালা থেকে key |
| `model-test/ssc-2026-mt2-mcq.json` | ২৫ | SSC-2026 মডেল টেস্ট ২, MCQ, উত্তরমালা থেকে key |
| `model-test/ssc-2027-set-1-cq.json` | ৭ | SSC-2027 সেট ১, সৃজনশীল — ছাপা উত্তর নেই, শুধু অধ্যায়-নির্দেশ |
| `model-test/ssc-2027-set-1-saq.json` | ৭ | SSC-2027 সেট ১, সংক্ষিপ্ত-উত্তর — ছাপা উত্তর নেই |
| `model-test/ssc-2027-set-2-cq.json` | ৭ | SSC-2027 সেট ২, সৃজনশীল — ছাপা উত্তর নেই |
| `model-test/ssc-2027-set-2-saq.json` | ৭ | SSC-2027 সেট ২, সংক্ষিপ্ত-উত্তর — ছাপা উত্তর নেই |
| `model-test/ssc-2027-set-3-cq.json` | ৭ | SSC-2027 সেট ৩, সৃজনশীল — ছাপা উত্তর নেই |
| `model-test/ssc-2027-set-3-saq.json` | ৭ | SSC-2027 সেট ৩, সংক্ষিপ্ত-উত্তর — ছাপা উত্তর নেই |
| `model-test/ssc-2027-model-1-mcq.json` | ২৫ | SSC-2027 মডেল ১, MCQ, উত্তরমালা থেকে key |
| `model-test/ssc-2027-model-2-mcq.json` | ২৫ | SSC-2027 মডেল ২, MCQ, উত্তরমালা থেকে key |
| `board-2023-mcq.json` | ২৫ | বোর্ড ২০২৩, সকল বোর্ড, MCQ — key ২৫/২৫ |
| `board-2023-cq.json` | ১৬ | বোর্ড ২০২৩, Paper A (৮) + Paper B (৮), ছাপা উত্তরসহ |
| `board-2024-mcq.json` | ২৫ | বোর্ড ২০২৪, সকল বোর্ড, MCQ — key ২৫/২৫ |
| `board-2024-cq.json` | ১৬ | বোর্ড ২০২৪, Paper A (৮) + Paper B (৮), ছাপা উত্তরসহ |
| `board-2025-mcq.json` | ২৫ | বোর্ড ২০২৫, সকল বোর্ড, MCQ — **উত্তরমালা খালি ঘর, key নেই** |
| `board-2025-cq.json` | ১৬ | বোর্ড ২০২৫, Paper A (৮) + Paper B (৮); ৮টি সিলেবাস-বহির্ভূত |
| `chapter-00-cq.json` | ১৭ | সমন্বিত অধ্যায়ের সৃজনশীল (ফাইল ১৯), ছাপা উত্তরসহ |
| `chapter-00-practical.json` | ২৪ | ব্যবহারিক পরীক্ষণ ১–১২ × ২ ফাইল (২য় ফাইল প্রতিলিপি-flag) |
| `questions-home-science.json` | ৩২২ | সব রো একত্রে |
| `flagged.json` | ১০৪ | flag_note আছে এমন সব রো |

## বোর্ড/সাল সূচি (board প্রশ্ন)

| সাল | Paper | বোর্ড | রো |
|---|---|---|---|
| ২০২৩ | A (সকল বোর্ড) | dhaka, jashore, sylhet, mymensingh | MCQ ২৫ + CQ ৮ |
| ২০২৩ | B | rajshahi, cumilla, chattogram, dinajpur | CQ ৮ |
| ২০২৪ | A (সকল বোর্ড) | dhaka, rajshahi, chattogram, jashore, sylhet, barishal, dinajpur, mymensingh | MCQ ২৫ + CQ ৮ |
| ২০২৪ | B | cumilla | CQ ৮ |
| ২০২৫ | A (সকল বোর্ড) | dhaka, chattogram, cumilla, barishal, mymensingh | MCQ ২৫ + CQ ৮ |
| ২০২৫ | B | rajshahi, jashore, sylhet, dinajpur | CQ ৮ |

## কী করা হয়নি (বাকি)

- অধ্যায় ১–১৮-র **PDF** ১৮টি + `Practical/Combined CQ.pdf` — প্রশ্নের মূলপাঠ ছবি
  হিসেবে এমবেড করা; টেক্সট লেয়ারে শুধু শিরোনাম + অপশন অক্ষর + ● চিহ্ন আছে।
  **তবে অধ্যায় ১–১৮-র .doc টুইনগুলোতে আসল লেখা আছে** (নরমালাইজেশন পাসে যাচাই
  করা) — তাই OCR-এর বদলে doc-থেকে চাংক করাই পরের ধাপ। `image-only-files.txt`-এ তালিকা আছে।
- বোর্ড ২০২৫ MCQ-র উত্তরমালা ছাপায় খালি ঘর (শিক্ষার্থী নিজে লিখবে) — ২৫টি রো-তে `answer_key` null।
- ফাইল ১৯-এর কিছু অংশের পাঠ কলাম-বিভাজনে কাটা পড়েছে (৮টি রো flag করা) — চোখে দেখে যাচাই করলে পূর্ণ করা যাবে।
- **অধ্যায়-doc চাংকিং (নতুন):** অধ্যায় ১–১৮-র .doc থেকে ~২,৫৫০টি প্রশ্ন চাংক করা
  বাকি — ২-কলাম interleaved লেখা, নতুন পার্সার + প্রতি-অধ্যায় যাচাই লাগবে;
  ডিকোড করা লেখা `~/workspace/lecture-sheets/work/home-science/docdecoded/`-এ
  রাখা আছে, যাচাই-তালিকা `_work/doc-twin-verification.md`-এ।

## যাচাই

- সব JSON parse হয়; per-file রো-র যোগফল = combined ৩২২।
- ০ duplicate id; সব রো ৩৭ ফিল্ড; `question_text` খালি ০টি।
- MCQ-ধরন (type=mcq ১০০ + board-kind mcq ৭৫ = ১৭৫)-এ ৪টি করে অপশন পূর্ণ;
  answer_key ১৫০/১৭৫ (বোর্ড ২০২৩/২০২৪ + মডেল ১০০% যাচাই করা key-র সাথে মিলেছে)।
- CQ-ধরন (type=cq ৫৪ + board-kind cq ৪৮ = ১০২)-এ ৪টি করে অংশ পূর্ণ; ছাপা উত্তর আছে
  ৮১/১০২-তে (২১টি সেট-CQ-তে শুধু অধ্যায়-নির্দেশ)।
- ডিকোডার: শেয়ার্ড টুল v2; বোর্ড ফাইল ০% → ৮৯–৯৭% বাংলা লাইন; অধ্যায় ফাইলগুলো ছবি বলে v2-তেও বদলায়নি।
- পার্সার: `parse-home-science.py`, ড্রাইভার: `build-home-science.py` (এই ডিরে, অডিটের জন্য রাখা)।
