# Class 9–10 Bangla 1st Paper (বাংলা ১ম) Guide — Question Bank

Guide data for the **Yes Sir AI** tuition app, kept under `guides/` on
purpose: this is **guide** material, not NCTB textbook material.

বাংলা সংক্ষেপ: এটা গাইডের ডাটা, পাঠ্যবইয়ের নয়।

## Coverage

| Item | Count |
|------|-------|
| Prose chunks (`chunks.json`) | 233 |

## Board MCQs (added 2026-11-23)

Source: user-provided `~/workspace/user/files/upload.pdf` — Satt Academy
Dynamic Print Question Bank, "নবম-দশম শ্রেণি বোর্ড প্রশ্ন ও সমাধান",
বাংলা সাহিত্য, printed 2025-04-02, 81 pages. Text-layer parse (parser:
`/tmp/parse_bangla1st.py`). Staging only — nothing imported to the live DB.

| File | Rows |
|------|------|
| `questions-board-2024.json` | 270 (9 boards × 30) |
| `questions-board-2023.json` | 270 (9 boards × 30) |
| `questions-board-2020.json` | 240 (8 boards × 30) |
| `questions-board-2019.json` | 240 (8 boards × 30) |
| `questions-board-2018.json` | 30 (সকল বোর্ড × 30) |
| **Total** | **1050** |

Schema: standard staging rows (`section: board-mcq`, options as ক/খ/গ/ঘ
dict, `answer_key` Bengali letter, `board_tag` e.g. "ঢাকা বোর্ড ২০২৪").
IDs: `bn1-board-<board-slug>-<year>-mcq-<nn>`. Stimuli: 50 blocks, each
covering exactly the next 2 questions (positional rule — the word
"উদ্দীপক" in a stem is NOT a signal; it over-attached one stale stimulus
to 45 questions). Text transcribed exactly as printed (incl. rendering
quirks like "ময়মনসিংংহ", "বোড"); nothing "fixed".

Defects (kept as printed, flagged here — nothing dropped):
- `bn1-board-mymensingh-2024-mcq-29`: no `ans:` line in the print
  (visually confirmed on PDF p.4); `answer_key` is null.
- `bn1-board-sylhet-2020-mcq-01`: option a) missing in the print
  (visually confirmed on PDF p.49); `options` is null.
- রাজশাহী 2023 set repeats two questions verbatim in the print:
  Q3 = Q22 and Q7 = Q27 (same stem, options, ans); both kept.

## Honest limits

- Live in the app DB: 6721 rows + 233 chunks.
- Guide: Panjeree 2026. Chunks built from the 18 collection lesson files in LESSON_ORDER (same mapping as import_bangla1st.py).
- Note: staging `lessons/` holds 16 of the 18 lessons (194 chunks); `kopotakkho-nod` and `prottupokar` lesson files are not in staging, but their chunks ARE in this `chunks.json` (all 233).