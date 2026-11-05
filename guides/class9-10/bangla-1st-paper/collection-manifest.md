# Bangla 1st Paper — Collection MANIFEST

Source: Panjeree SSC 2026 guide, class 10. Spec:
`../BANGLA1ST_PLAN.md` + `collection/README.md`.
Rule: a lesson counts as DONE only when every fragment is
verified and merged; unverified lessons stay open.

## Lesson 1 — প্রত্যুপকার (ঈশ্বরচন্দ্র বিদ্যাসাগর), printed 5–38

**MERGED + DONE (verified by coordinator):**
`lessons/prottupokar.json` — 379 rows, 18 chunks, 2 sets,
13 held. Verified flags: 369 true / 10 false (bank only).

| Fragment | File | Status | Counts |
|---|---|---|---|
| Analysis + quiz | `lessons/prottupokar/analysis.json` | DONE | 18 chunks (analysis 11 + supporting 7) + 32 quiz rows (short-answer, options/key null), held 3 |
| MCQ bank | `lessons/prottupokar/mcq-bank.json` | DONE | 198 total (exercise 2, master-trainer 18, sadharon 140, bohupodi 28, ovinno 10); held [] |
| Short Q&A | `lessons/prottupokar/short-qa.json` | DONE | 90 rows (jnan 60 + anudhabon 30), held [] |
| Creative + bank CQs | `lessons/prottupokar/creative.json` | DONE | 14 lesson CQs (verified) + 10 bank CQs (question-verified, answers NULL — not printed by design), held 10 |
| Model tests | `lessons/prottupokar/model-tests.json` | DONE | 30 model-mcq + 5 model-creative, held [] |

Lesson verified flag = false ONLY because bank CQ answers do
not exist in print (see decision item 1 below). All other
rows eye-checked at 500 dpi.

## Decision items for parent/user (do not assume)

1. **Bank counting:** bank groups are in rows[] with
   verified=false AND in held[]. If counts must mean
   "fully verified only", bank reads 0 (lesson verified
   rows = 369, not 379).
2. **CQ12 photo stimulus:** CQ12's stimulus is a photograph;
   stimulus_text is a bracketed description grounded in the
   photo + the group's own ga/gha answers — not verbatim
   printed text. Confirm acceptable, or rule it held.
3. **Verification resolution (from interim report):** source
   scans are natively ~150–180 ppi; 500-dpi renders are
   upscales. Rule whether native-resolution verification
   counts, or literal 500-dpi stays for all rows.

## Image-wins corrections recorded (evidence over brief)

- MCQ bank numbering is ONE global sequence 1–198, NOT
  restarted per sub-source (brief assumption corrected).
- Filled MCQ key grid is at the foot of printed p. 38, NOT
  p. 37 (p. 37 foot grid is blank student fill-in).
- Model-test MCQ grade bands as printed: D 0–11 / C 12–18 /
  B 19–26 / A 27–30 (plan brief said C 12–19 / B 20–26).
- Short-qa anudhabon ids disambiguated (`-short-qa-anudhabon-N`)
  since numbering restarts at 1.
- Quiz items are short-answer rows (options/key null), NOT MCQ.
- Guide misprints kept verbatim throughout (never "fixed").

## Decision items — RESOLVED 2026-11-02 (plan §11, user decisions)

1. **Bank counting — RESOLVED:** bank groups (question present,
   answer NOT printed) are DROPPED from usable rows/counts.
   Lessons 2–18 record them in held[] only with
   ai_answerable=true (answer NULL, verified=false, excluded
   from verified totals, quiz, scoring) so the app can later
   offer a clearly-labeled AI answer, never as guide text.
   Lesson 1 predates this rule and keeps its original
   structure (bank in rows + held); its verified-only count
   is 369, not 379.
2. **Photo stimuli — RESOLVED:** HELD with reason exactly
   "photo stimulus, image display pending", stimulus_text
   null, answers/essences preserved in the held entry. No
   bracketed description shown either. (Open question to
   parent/user, still unanswered: can image display be
   arranged in the app at all, for Bangla photo stimuli and
   physics/chemistry images?)
3. **Verification resolution — RESOLVED:** use the MAXIMUM
   TRUE DPI the source genuinely supports (native ~150–180
   ppi for these scans; no upscaling to 500). Accurate text
   is the goal; verified_by="native-eye" on lessons 2–18.

## Lessons 2–18 — MERGED + DONE (verified by coordinator)

Grand totals lessons 1–18: 5,033 rows, 232 held, 233 chunks,
34 sets. Lessons 2–18 alone: 4,654 rows, 219 held.
Mechanical gate on every file: JSON parses, row ids unique,
held ids disjoint from rows (except lesson 1 legacy, above),
all set member ids resolve to rows, subsection tags exactly
quiz / mcq-bank / short-qa / creative / model-mcq /
model-creative (descriptive only in ১৯৭১). Counts below are
verified-only rows; held is separate.

| # | Lesson (author, printed pp.) | File | Rows | Held | Chunks | Sets | Verified |
|---|---|---|---|---|---|---|---|
| 2 | সুভা (রবীন্দ্রনাথ ঠাকুর, 39–74) | lessons/subha.json | 334 | 12 (10 bank + 2 scan-gap: CQ8/CQ9, blank p. 62) | 15 | 2 | true |
| 3 | বই পড়া (প্রমথ চৌধুরী, 75–112) | lessons/boi-pora.json | 331 | 12 (10 bank + 1 guide-flagged flawed Q + 1 illegible statements) | 8 | 2 | true |
| 4 | আম-আঁটির ভেঁপু (বিভূতিভূষণ বন্দ্যোপাধ্যায়, 113–144) | lessons/am-antir-bhepu.json | 308 | 13 (10 bank + 1 photo model-creative-3 + 2 blurred answers p. 127) | 10 | 2 | true |
| 5 | মানুষ মুহম্মদ (স.) (মোহাম্মদ ওয়াজেদ আলী, 145–176) | lessons/manush-muhammad.json | 284 | 10 (all bank) | 11 | 2 | true |
| 6 | নিমগাছ (বনফুল, 177–208) | lessons/nimgach.json | 295 | 10 (all bank) | 9 | 2 | true |
| 7 | শিক্ষা ও মনুষ্যত্ব (মোতাহের হোসেন চৌধুরী, 209–242) | lessons/shikkha-o-manushotto.json | 277 | 11 (10 bank + scan-gap: quiz-1 + analysis opening, pp. 210–211 absent) | 14 | 2 | true |
| 8 | প্রবাস বন্ধু (সৈয়দ মুজতবা আলী, 243–272) | lessons/probas-bondhu.json | 295 | 10 (all bank) | 14 | 2 | true |
| 9 | একুশের গল্প (জহির রায়হান, 273–306) | lessons/ekusher-golpo.json | 396 | 26 (10 bank + 1 photo + 15 smeared p. 285, Q170–184) | 21 | 2 | true |
| 10 | কপোতাক্ষ নদ (মাইকেল মধুসূদন দত্ত, 309–344) | lessons/kopotakkho-nod.json | 277 | 14 (10 bank + 1 dual-key + 3 scan-gap pp. 336–337) | 21 | 2 | false* |
| 11 | জীবন বিনিময় (গোলাম মোস্তফা, 345–368) | lessons/jibon-binimoy.json | 208 | 11 (10 bank + 1 photo CQ10) | 19 | 2 | true |
| 12 | উমর ফারুক (কাজী নজরুল ইসলাম, 369–394) | lessons/umor-faruk.json | 256 | 15 (10 bank + 4 illegible quiz stems + 1 illegible margin key) | 10 | 2 | true |
| 13 | সেইদিন এই মাঠ (জীবনানন্দ দাশ, 395–424) | lessons/seidin-ei-math.json | 261 | 22 (10 bank + 10 long answers not verifiable word-for-word + 2 scan-gap pp. 410–411) | 8 | 2 | true |
| 14 | বৃষ্টি (ফররুখ আহমদ, 425–456) | lessons/brishti.json | 272 | 10 (all bank) | 9 | 2 | true |
| 15 | আমি কোনো আগন্তুক নই (আহসান হাবীব, 457–484) | lessons/ami-kono-agontuk-noi.json | 269 | 10 (all bank) | 10 | 2 | true |
| 16 | তোমাকে পাওয়ার জন্যে, হে স্বাধীনতা (শামসুর রাহমান, 485–516) | lessons/tomake-pawar-jonne-he-sadhinota.json | 272 | 11 (10 bank + 1 photo) | 12 | 2 | true |
| 17 | বোশেখ (আল মাহমুদ, 517–542) | lessons/boshekh.json | 251 | 12 (10 bank + 2 photo) | 10 | 2 | true |
| 18 | ১৯৭১ (হুমায়ূন আহমেদ, 544–566) | lessons/1971.json | 68 | 10 (all bank) | 14 | 0 | true |

\* কপোতাক্ষ নদ verified=false SOLELY because exercise MCQ Q2
(p. 314) has no single printed key — the guide's দ্রষ্টব্য
declares BOTH ক and খ correct. The item is held
(ai_answerable=false); every usable row passed the gate.

Subsection detail (verified rows): সুভা 32/143/107/17/30/5;
বই পড়া 32/155/89/20/30/5; আম-আঁটির ভেঁপু 32/149/78/15/30/4;
মানুষ 32/134/69/14/30/5; নিমগাছ 32/150/62/16/30/5;
শিক্ষা 24/129/72/17/30/5 (quiz sets 2–4; set 1 scan-gap);
প্রবাস 32/143/72/13/30/5; একুশের 32/169/150/10/30/5;
কপোতাক্ষ 32/135/59/16/30/5; জীবন 32/88/42/11/30/5;
উমর 28/117/66/10/30/5 (quiz 28 usable + 4 held = 32);
সেইদিন 32/136/47/11/30/5; বৃষ্টি 32/132/53/20/30/5;
আগন্তুক 32/118/72/12/30/5; তোমাকে 32/133/59/13/30/5;
বোশেখ 32/110/63/12/30/4; ১৯৭১ 32 quiz + 12 mcq-bank +
2 creative + 22 descriptive, no model tests.
Order per lesson: quiz / mcq-bank / short-qa / creative /
model-mcq / model-creative.

## Coordinator normalizations (content unchanged, 2026-11-02)

- শিখ্যা: 24 quiz rows retagged subsection None → quiz
  (ids + quiz_set prove it).
- উমর + সেইদিন: merged "model-tests" split by row id into
  model-mcq 30 + model-creative 5; সেইদিন's 32 "analysis"
  rows retagged to quiz (ids prove it). Counts fields
  already matched these splits.
- নিমগাছ + প্রবাস: flag-notes moved OUT of held[] into row
  notes / verification_notes (nothing withheld in them);
  নিমগাছ held 17 → 10, প্রবাস held 14 → 10 (both all bank
  after the move). নিমগাছ p. 178 importance table
  transcribed verbatim by the coordinator from an enlarged
  crop into new field `shikhonfol_importance_p178`
  (grid totals 0/4/3/9/4, chart-matched, ranking note
  ৪, ২, ৫ ও ৩): the p. 177 opener lists 4 outcomes but the
  p. 178 table prints 5 rows, and row 5's outcome text is
  nowhere printed — flagged, never invented. No row depends
  on that table.
- আম-আঁটির ভেঁপু: photo-held model-creative-3 removed from
  the set's usable members, recorded under the set's
  `held_members` (printed set = 5 groups / 50 marks;
  usable = 4 groups).
- তোমাকে / বোশেখ / ১৯৭১ chunks completed (were 1 summary
  each): +11 / +9 / +13 per-section chunks, rows/held/sets
  byte-identical in count. One gap flagged in-text:
  তোমাকে p. 488 শ্রেণি-চরিত্র item ৩ ends mid-sentence,
  continuation absent from the scan.
- প্রবাস model-creative-3 prints only ক/খ parts (p. 272);
  no গ/ঘ invented. Backups of pre-normalization files in
  /tmp/coord-backup/ (ephemeral).

## Pipeline notes

- Scan mapping (goddo): scan n = printed n+1 (verified at
  scans 4, 5, 9, 36).
- Scan mapping (poddo): printed page = PDF page + 308
  (verified from page headers; e.g. printed 486 = PDF 178).
- Scan mapping (uponnas): printed page = PDF page + 543
  (printed 545 = PDF 2).
- Scan-gap offsets exist per lesson and break any global
  rule: শিক্ষা post-gap offset is printed = PDF + 3
  (pp. 210–211 absent); কপোতাক্ষ pp. 336–337 absent;
  সেইদিন pp. 410–411 absent; সুভা p. 62 blank. Always
  verify mapping from page headers per lesson.
- /tmp is a 512 MB tmpfs and filled during work: renders go
  to workspace scratch dirs under `collection/renders-*/`
  and are deleted after verification.
- One creative worker errored (runtime restart drain,
  nothing written); a replacement redid it reusing the
  surviving renders. No data lost.
