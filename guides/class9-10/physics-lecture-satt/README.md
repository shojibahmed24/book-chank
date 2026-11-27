# SSC Physics Lecture Sheets — staging (chunked 2026-11-24, final pass 2026-11-24, normalized 2026-11-25)

Subject: পদার্থবিজ্ঞান (physics) — Class 9-10
Files chunked: 628 (458 first pass + 170 final pass)
Total rows: 5574 (5404 + 170 Mq model-test rows, 2026-11-25)
Schema: 37 fields (34-field board schema + `type`, `subject_slug`, `chapter_name` — normalized 2026-11-25; see "Normalization (2026-11-25)" below)

## Rows by type

- board: 7
- cq: 185
- gyanmulok: 13
- handnote: 41
- lecture-note: 57
- mcq: 4945
- model-test: 174 (4 + 170 Mq Chapter 1–10, 2026-11-25)
- saq: 152

Flagged rows: 4598 (4474 + 124 new Mq flags — see "Model-test Mq Chapter 1–10 chunking (follow-up)" in report-2026-11-24.md)
Answer keys matched from answer sheets (final pass): 0
Repairs applied: 0

## Chapter names (from file headers — sheet-header forms; see normalization notes for book variants)

- Chapter 1: ভৌত রাশি এবং তাদের পরিমাপ
- Chapter 2: গতি
- Chapter 3: বল
- Chapter 4: কাজ, ক্ষমতা ও শক্তি
- Chapter 5: পদার্থের অবস্থা ও চাপ
- Chapter 6: বস্তুর উপর তাপের প্রভাব
- Chapter 7: তরঙ্গ ও শব্দ
- Chapter 8: আলোর প্রতিফলন
- Chapter 9: আলোর প্রতিসরণ
- Chapter 10: স্থির বিদ্যুৎ
- Chapter 11: চল বিদ্যুৎ
- Chapter 12: বিদ্যুতের চৌম্বক ক্রিয়া
- Chapter 13: তেজস্ক্রিয়তা ও ইলেকট্রনিক্স
- Chapter 14: জীবন বাঁচাতে পদার্থবিজ্ঞান

## Normalization (2026-11-25)

- **Schema 34 → 37 fields** on all 5,404 rows: added `type` (from `section`), `subject_slug` = "physics", `chapter_name` (from chapter number via the list above). Row count unchanged (5,404 → 5,404); 0 rows dropped (0 truly-empty placeholders); ids unchanged.
- **Chapter recovery:** 14 Hand Note2 rows (`SSC-Physics-N.pdf`, chapter 0/None) recovered to chapters 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 12, 14 — each file's first in-text "অধ্যায়—N" header matches its filename N. `chapter-00-handnote.json` deleted (now empty); `chapter-14-handnote.json` created (2 rows). Ids still carry `ch00` (stable identifiers, not rewritten).
- **Chapter unknown:** 299 rows stay chapter 0 / `chapter_name` null (SSC-2027 sets, Combined Model sets, board papers, test papers, practice-suggestion files) + flag note each.
- **Board year:** 4 of 7 board rows got `board_year` from the filename (Physics-2023 → 2023, Physics-2024 → 2024, Physics-2025 → 2025, TP_ME 2024 Newton → 2024); `board_name` stays null on all 7 (multi-board papers) + flag note. Per-board split never happened because decoded headers spell "বোর্ড" as "বোডর্" (257× across the 7 board files) so the chunker's `বোর্ড` regex never matched — a future re-chunk pass could split per board with a `বোডর্`-tolerant pattern.
- **Decomposed Bengali composed:** 48,279× য+় → য়, 11,229× ড+় → ড়, 37× ঢ+় → ঢ়, 74× ে+া → ো, 12× ে+ৗ → ৌ, 5× Ω → Ω (509 + 753 rows; 767 + 753 fields). Meaning-preserving (NFD before == NFD after on all 62,259 string fields, verified). NOTE: plain `unicodedata.normalize("NFC")` must never be used here — NFC *decomposes* য়/ড়/ঢ় (Unicode composition exclusions), verified in-session.
- **Duplicates flagged, none deleted:** 48 rows in 24 exact-duplicate groups got a flag note naming the other row's id (includes the same question printed twice as Q13 and Q30 in one ch11 bank file — kept as two printed occurrences, flagged).
- **Math-misfire check:** no v2 decoder damage found — 0× "অ = {", 0× "{ধ/ন/প", only 4 benign Bengali-in-braces matches in decoded files (legit phrases/formulas, e.g. "{ 'গ' হতে প্রাপ্ত}"); 0 files re-decoded. The v2.1 high-byte guard was verified present in `tools/decode-pdf.py` (docstring lines ~13–19, `should_convert` guard).
- **Doc-twin check (STOPPED at 55/290 by SIGTERM — see report):** 55 of 290 skipped duplicates verified before the run was stopped (SIGTERM); 55/55 are doc-richer (doc 10–100× more readable Bengali than the PDF twin), 0 duplicate-confirmed. #Hand note's 13 docs were already the chunk source (known). The .doc holds the same material in readable form while the twin PDF's Bijoy runs barely decode (1–8% Bengali lines) — re-chunking from docs is a separate project-scale decision, not done here; no twin was chunked in this pass.
- **Validation:** all 86 chapter + 59 model-test JSONs parse; combined 5,404 = 4,517 chapter + 887 model-test; ids unique/non-null; all rows 37 fields in spec order; `flagged.json` ⊆ combined and count (4,474) == rows with flag note; `answer_key` non-null count unchanged 1,766 (nothing guessed); manifest 628 = 338 content-processed (322 PDF + 16 doc-only) + 290 skipped duplicates + 0 missing. Backup of pre-normalization files: `_backup_pre_norm/` (md5-verified). Scripts: `_work/normalize_physics.py`, `_work/validate_norm.py`, `_work/doc_verify.py`; logs: `_work/normalize-2026-11-25-log.json` (+ `-run1.json`), `_work/doc-verify/results.jsonl`.

## Files

- chapter-00-board.json
- chapter-00-cq.json
- chapter-00-mcq.json
- chapter-00-model-test.json
- chapter-01-cq.json
- chapter-01-gyanmulok.json
- chapter-01-handnote.json
- chapter-01-lecture-note.json
- chapter-01-mcq.json
- chapter-01-saq.json
- chapter-02-cq.json
- chapter-02-gyanmulok.json
- chapter-02-handnote.json
- chapter-02-lecture-note.json
- chapter-02-mcq.json
- chapter-02-saq.json
- chapter-03-cq.json
- chapter-03-gyanmulok.json
- chapter-03-handnote.json
- chapter-03-lecture-note.json
- chapter-03-mcq.json
- chapter-03-saq.json
- chapter-04-cq.json
- chapter-04-gyanmulok.json
- chapter-04-handnote.json
- chapter-04-lecture-note.json
- chapter-04-mcq.json
- chapter-04-saq.json
- chapter-05-cq.json
- chapter-05-gyanmulok.json
- chapter-05-handnote.json
- chapter-05-lecture-note.json
- chapter-05-mcq.json
- chapter-05-saq.json
- chapter-06-cq.json
- chapter-06-gyanmulok.json
- chapter-06-handnote.json
- chapter-06-lecture-note.json
- chapter-06-mcq.json
- chapter-06-saq.json
- chapter-07-cq.json
- chapter-07-gyanmulok.json
- chapter-07-handnote.json
- chapter-07-lecture-note.json
- chapter-07-mcq.json
- chapter-07-saq.json
- chapter-08-cq.json
- chapter-08-gyanmulok.json
- chapter-08-handnote.json
- chapter-08-lecture-note.json
- chapter-08-mcq.json
- chapter-08-saq.json
- chapter-09-cq.json
- chapter-09-gyanmulok.json
- chapter-09-handnote.json
- chapter-09-lecture-note.json
- chapter-09-mcq.json
- chapter-09-saq.json
- chapter-10-cq.json
- chapter-10-gyanmulok.json
- chapter-10-handnote.json
- chapter-10-lecture-note.json
- chapter-10-mcq.json
- chapter-10-saq.json
- chapter-11-cq.json
- chapter-11-gyanmulok.json
- chapter-11-handnote.json
- chapter-11-lecture-note.json
- chapter-11-mcq.json
- chapter-11-saq.json
- chapter-12-cq.json
- chapter-12-gyanmulok.json
- chapter-12-handnote.json
- chapter-12-lecture-note.json
- chapter-12-mcq.json
- chapter-12-saq.json
- chapter-13-cq.json
- chapter-13-gyanmulok.json
- chapter-13-handnote.json
- chapter-13-lecture-note.json
- chapter-13-mcq.json
- chapter-13-saq.json
- chapter-14-cq.json
- chapter-14-handnote.json
- chapter-14-lecture-note.json
- chapter-14-mcq.json
- mtnew-combined-model-1-set-1-mcq.json
- mtnew-combined-model-2-set-1-mcq.json
- mtnew-combined-model-3-set-1-mcq.json
- mtnew-combined-model-4-set-1-mcq.json
- mtnew-combined-model-5-set-1-mcq.json
- mtnew-cq-ch01-cq.json
- mtnew-cq-ch01-saq.json
- mtnew-cq-ch02-cq.json
- mtnew-cq-ch02-saq.json
- mtnew-cq-ch03-cq.json
- mtnew-cq-ch03-saq.json
- mtnew-cq-ch04-cq.json
- mtnew-cq-ch04-saq.json
- mtnew-cq-ch05-cq.json
- mtnew-cq-ch05-saq.json
- mtnew-cq-ch06-cq.json
- mtnew-cq-ch06-saq.json
- mtnew-cq-ch07-cq.json
- mtnew-cq-ch07-saq.json
- mtnew-cq-ch08-cq.json
- mtnew-cq-ch08-saq.json
- mtnew-cq-ch09-cq.json
- mtnew-cq-ch09-saq.json
- mtnew-cq-ch10-cq.json
- mtnew-cq-ch10-saq.json
- mtnew-cq-ch11-cq.json
- mtnew-cq-ch11-saq.json
- mtnew-cq-ch12-cq.json
- mtnew-cq-ch12-saq.json
- mtnew-cq-ch13-cq.json
- mtnew-cq-ch13-saq.json
- mtnew-mcq-ch01-set-1-mcq.json
- mtnew-mcq-ch02-set-1-mcq.json
- mtnew-mcq-ch03-set-1-mcq.json
- mtnew-mcq-ch04-set-1-mcq.json
- mtnew-mcq-ch05-set-1-mcq.json
- mtnew-mcq-ch06-set-1-mcq.json
- mtnew-mcq-ch07-set-1-mcq.json
- mtnew-mcq-ch08-set-1-mcq.json
- mtnew-mcq-ch09-set-1-mcq.json
- mtnew-mcq-ch10-set-1-mcq.json
- mtnew-mcq-ch11-set-1-mcq.json
- mtnew-mcq-ch12-set-1-mcq.json
- mtnew-mcq-ch13-set-1-mcq.json
- ssc2027-cq-set-1-cq.json
- ssc2027-cq-set-1-saq.json
- ssc2027-cq-set-2-cq.json
- ssc2027-cq-set-2-saq.json
- ssc2027-cq-set-3-cq.json
- ssc2027-cq-set-3-saq.json
- ssc2027-cq-set-4-cq.json
- ssc2027-cq-set-4-saq.json
- ssc2027-cq-set-5-cq.json
- ssc2027-cq-set-5-saq.json
- ssc2027-mcq-set-1-set-1-mcq.json
- ssc2027-mcq-set-2-set-1-mcq.json
- ssc2027-mcq-set-3-set-1-mcq.json
- ssc2027-mcq-set-4-set-1-mcq.json
- ssc2027-mcq-set-5-set-1-mcq.json
- questions-physics.json
- flagged.json
- processed-files.txt
- missing-files.txt

Final pass: the 170 files missing after the first pass (Topicwise MCQ 1/2, Model Test New, #NEW UPDATE 10–14) were chunked after the download completed; see report-2026-11-24.md for details.
