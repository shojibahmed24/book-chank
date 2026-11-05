# Chemistry import verification — 2026-11-04 (file work only)

Source files untouched. This file reports the built import-ready set.

## Reconciliation

- Collection rows total: 5,808 (board 443 + ch3 863 + ch4 706 + ch5 813 + ch6 967 + ch7 653 + ch11 461 + practical 79 + special 823)
- Collection held total: 281 (board 151 + ch3 19 + ch4 49 + ch5 9 + ch6 1 + ch7 18 + ch11 28 + frontmatter 6); held entries are disjoint from rows (0 row/held overlap, verified)
- Collection chunks total: 114 (not rows; chunk import is a separate batch step, not built here)
- Excluded rows: 24 (A 11 + B 4 + D 7 + E 2)
- Import-ready rows: 5784
- Check: 5,808 - 24 = 5784; built file holds 5784 rows -> MATCH

## Breakdown by source file (import-ready rows)

- che-board.json: 438
- che-ch3.json: 861
- che-ch4.json: 705
- che-ch5.json: 812
- che-ch6.json: 963
- che-ch7.json: 647
- che-ch11.json: 460
- che-practical.json: 79
- che-special.json: 819

## Breakdown by file + section (import-ready rows)

- che-board.json / board-creative: 102
- che-board.json / board-mcq: 336
- che-ch11.json / applied-math: 8
- che-ch11.json / conceptual-creative: 2
- che-ch11.json / creative: 124
- che-ch11.json / knowledge-qa: 30
- che-ch11.json / mcq-bank: 133
- che-ch11.json / model-creative: 7
- che-ch11.json / model-mcq: 25
- che-ch11.json / model-short: 7
- che-ch11.json / short-qa: 97
- che-ch11.json / topic-math: 4
- che-ch11.json / understanding-qa: 23
- che-ch3.json / activity: 3
- che-ch3.json / applied-math: 21
- che-ch3.json / conceptual-creative: 2
- che-ch3.json / creative: 48
- che-ch3.json / knowledge-qa: 86
- che-ch3.json / mcq-bank: 350
- che-ch3.json / model-creative: 6
- che-ch3.json / model-mcq: 25
- che-ch3.json / model-short: 7
- che-ch3.json / quiz: 185
- che-ch3.json / short-qa: 72
- che-ch3.json / topic-math: 56
- che-ch4.json / activity: 6
- che-ch4.json / applied-math: 3
- che-ch4.json / comprehension-qa: 23
- che-ch4.json / conceptual-creative: 2
- che-ch4.json / creative: 69
- che-ch4.json / knowledge-qa: 27
- che-ch4.json / mcq-bank: 306
- che-ch4.json / model-creative: 7
- che-ch4.json / model-mcq: 25
- che-ch4.json / model-short: 7
- che-ch4.json / quiz: 132
- che-ch4.json / short-qa: 98
- che-ch5.json / activity: 3
- che-ch5.json / conceptual-creative: 2
- che-ch5.json / creative: 112
- che-ch5.json / knowledge-qa: 63
- che-ch5.json / mcq-bank: 337
- che-ch5.json / model-creative: 7
- che-ch5.json / model-mcq: 25
- che-ch5.json / model-short: 7
- che-ch5.json / quiz: 149
- che-ch5.json / short-qa: 107
- che-ch6.json / activity: 10
- che-ch6.json / comprehension-qa: 26
- che-ch6.json / conceptual-creative: 2
- che-ch6.json / creative: 85
- che-ch6.json / knowledge-qa: 29
- che-ch6.json / mcq-bank: 391
- che-ch6.json / model-creative: 7
- che-ch6.json / model-mcq: 25
- che-ch6.json / model-short: 7
- che-ch6.json / quiz: 99
- che-ch6.json / short-qa: 88
- che-ch6.json / topic-math: 156
- che-ch6.json / topic-math-bank: 38
- che-ch7.json / conceptual-creative: 2
- che-ch7.json / creative: 86
- che-ch7.json / knowledge-qa: 19
- che-ch7.json / mcq-bank: 301
- che-ch7.json / quiz: 143
- che-ch7.json / short-qa: 96
- che-practical.json / practical-chunk: 28
- che-practical.json / viva: 51
- che-special.json / model-creative: 152
- che-special.json / model-mcq: 515
- che-special.json / model-short: 152

## Verification checks

- JSON parses, all lines: yes (5784 lines)
- Duplicate ids in output: 0
- MCQ rows in output: 2794; MCQ null keys in output: 0 []
- Pointer-only rows in output (solution NULL + verbatim pointer, kept as-is, never converted): 490 (collection total 500 minus 4 held-near pointer rows minus 6 variant-bucket pointer rows)
- Part-level out-of-syllabus rows in output (flagged, NOT split): 19
- Empty question text in output: 0
- Rows without class_id 9: 0

## Section 9.18 grid-audit corrections applied (in the new file only)

- Verdicts file: 612 entries (agree 520, correct 91, null-confirmed 1); all verdict ids exist as rows
- 'correct' verdicts applied: 88 (old -> grid-verbatim new); the other 3 'correct' verdicts needed no change (collected key already equals grid reading); 'agree' needed no change; no correction applied to any excluded row
- che-board-barishal-2024-board-mcq-14: 'খ' -> 'ক'
- che-board-barishal-2024-board-mcq-2: 'খ' -> 'গ'
- che-board-barishal-2024-board-mcq-7: 'খ' -> 'ঘ'
- che-board-barishal-2024-board-mcq-8: 'খ' -> 'ক'
- che-board-chattogram-2023-board-mcq-11: 'খ' -> 'ঘ'
- che-board-chattogram-2023-board-mcq-12: 'খ' -> 'গ'
- che-board-chattogram-2023-board-mcq-19: 'খ' -> 'ঘ'
- che-board-chattogram-2023-board-mcq-20: 'খ' -> 'গ'
- che-board-chattogram-2023-board-mcq-22: 'খ' -> 'গ'
- che-board-chattogram-2023-board-mcq-25: 'গ' -> 'ক'
- che-board-chattogram-2023-board-mcq-4: 'খ' -> 'ঘ'
- che-board-chattogram-2023-board-mcq-6: 'খ' -> 'ক'
- che-board-chattogram-2023-board-mcq-9: 'গ' -> 'ক'
- che-board-chattogram-2024-board-mcq-1: 'খ' -> 'ঘ'
- che-board-chattogram-2024-board-mcq-10: 'খ' -> 'ক'
- che-board-chattogram-2024-board-mcq-11: 'খ' -> 'ক'
- che-board-chattogram-2024-board-mcq-18: 'খ' -> 'ক'
- che-board-chattogram-2024-board-mcq-2: 'খ' -> 'ক'
- che-board-chattogram-2024-board-mcq-4: 'খ' -> 'ঘ'
- che-board-chattogram-2024-board-mcq-7: 'খ' -> 'ক'
- che-board-cumilla-2023-board-mcq-6: 'খ' -> 'ক'
- che-board-cumilla-2024-board-mcq-16: 'গ' -> 'ঘ'
- che-board-cumilla-2024-board-mcq-19: 'খ' -> 'ক'
- che-board-cumilla-2024-board-mcq-2: 'খ' -> 'ঘ'
- che-board-cumilla-2024-board-mcq-8: 'খ' -> 'গ'
- che-board-dhaka-2023-board-mcq-1: None -> 'খ'
- che-board-dhaka-2023-board-mcq-14: None -> 'খ'
- che-board-dhaka-2023-board-mcq-16: None -> 'খ'
- che-board-dhaka-2023-board-mcq-18: None -> 'খ'
- che-board-dhaka-2023-board-mcq-20: 'খ' -> 'ক'
- che-board-dhaka-2023-board-mcq-22: 'খ' -> 'ক'
- che-board-dhaka-2023-board-mcq-3: None -> 'ক'
- che-board-dhaka-2023-board-mcq-9: 'খ' -> 'ক'
- che-board-dhaka-2024-board-mcq-10: 'খ' -> 'গ'
- che-board-dhaka-2024-board-mcq-9: 'খ' -> 'ঘ'
- che-board-dinajpur-2023-board-mcq-15: 'খ' -> 'ঘ'
- che-board-dinajpur-2023-board-mcq-7: 'গ' -> 'খ'
- che-board-dinajpur-2024-board-mcq-13: 'খ' -> 'গ'
- che-board-dinajpur-2024-board-mcq-15: 'খ' -> 'ক'
- che-board-dinajpur-2024-board-mcq-16: 'খ' -> 'ক'
- che-board-dinajpur-2024-board-mcq-2: 'খ' -> 'গ'
- che-board-dinajpur-2024-board-mcq-8: 'খ' -> 'ঘ'
- che-board-jashore-2023-board-mcq-19: 'খ' -> 'গ'
- che-board-jashore-2023-board-mcq-2: 'খ' -> 'গ'
- che-board-jashore-2023-board-mcq-21: 'খ' -> 'গ'
- che-board-jashore-2023-board-mcq-25: 'খ' -> 'গ'
- che-board-jashore-2023-board-mcq-3: 'খ' -> 'গ'
- che-board-jashore-2024-board-mcq-13: 'খ' -> 'গ'
- che-board-mymensingh-2023-board-mcq-6: 'খ' -> 'ঘ'
- che-board-mymensingh-2023-board-mcq-8: 'খ' -> 'ঘ'
- che-board-mymensingh-2024-board-mcq-16: 'ঘ' -> 'খ'
- che-board-mymensingh-2024-board-mcq-20: 'ঘ' -> 'খ'
- che-board-rajshahi-2023-board-mcq-10: 'খ' -> 'গ'
- che-board-rajshahi-2023-board-mcq-21: 'খ' -> 'ঘ'
- che-board-rajshahi-2023-board-mcq-25: 'খ' -> 'ঘ'
- che-board-rajshahi-2023-board-mcq-6: 'খ' -> 'গ'
- che-board-rajshahi-2023-board-mcq-7: 'খ' -> 'গ'
- che-board-rajshahi-2023-board-mcq-8: 'খ' -> 'ঘ'
- che-board-rajshahi-2024-board-mcq-18: 'খ' -> 'ঘ'
- che-board-rajshahi-2024-board-mcq-3: 'খ' -> 'ঘ'
- che-board-sylhet-2023-board-mcq-14: 'খ' -> 'গ'
- che-board-sylhet-2023-board-mcq-20: 'খ' -> 'ক'
- che-board-sylhet-2023-board-mcq-23: 'খ' -> 'ক'
- che-board-sylhet-2023-board-mcq-5: 'খ' -> 'ঘ'
- che-board-sylhet-2023-board-mcq-6: 'খ' -> 'ঘ'
- che-board-sylhet-2024-board-mcq-17: 'খ' -> 'ক'
- che-board-sylhet-2024-board-mcq-20: 'খ' -> 'ক'
- che-board-sylhet-2024-board-mcq-3: 'খ' -> 'ক'
- che-board-sylhet-2024-board-mcq-4: 'গ' -> 'ঘ'
- che-board-sylhet-2024-board-mcq-6: 'খ' -> 'ক'
- che-board-sylhet-2024-board-mcq-9: 'খ' -> 'ক'
- che-ch5-model-mcq-5: 'গ' -> 'ঘ'
- che-model-01-model-mcq-10: 'খ' -> 'ঘ'
- che-model-01-model-mcq-13: 'ক' -> 'গ'
- che-model-01-model-mcq-16: 'ক' -> 'খ'
- che-model-01-model-mcq-22: 'খ' -> 'ঘ'
- che-model-01-model-mcq-23: 'খ' -> 'ঘ'
- che-model-01-model-mcq-7: 'খ' -> 'ঘ'
- che-model-03-model-mcq-14: 'গ' -> 'ক'
- che-model-03-model-mcq-19: 'ঘ' -> 'খ'
- che-model-03-model-mcq-20: 'গ' -> 'ক'
- che-model-03-model-mcq-21: 'গ' -> 'ক'
- che-model-03-model-mcq-24: 'ঘ' -> 'খ'
- che-model-03-model-mcq-7: 'গ' -> 'ক'
- che-model-03-model-mcq-8: 'গ' -> 'ক'
- che-model-05-model-mcq-12: 'গ' -> 'ঘ'
- che-model-05-model-mcq-15: 'ঘ' -> 'খ'
- che-model-05-model-mcq-17: 'ঘ' -> 'খ'

## Buckets that subtract ZERO rows (held entries, not rows)

- Board out-of-syllabus 148 (113 MCQ + 35 creative, incl. 16 creative wording variants): held entries in che-board.json, disjoint from the 443 board rows. Import form still OPEN (flag vs drop) for if/when they ever become rows; nothing to subtract now.
- Scan-gap 32 (printed 545-576) + unreadable 95: held entries, disjoint from rows; dropped from import and marked for an alternate guide per decided disposition.
- Special 35 drops (set 09 MCQ 1-25, set 16 MCQ 15/16/17, set 19 MCQ 14, set 22 MCQ 1/2/3/10/11/23): verified ABSENT from che-special.json rows (0 present); no subtraction.
- Barishal 2023 creative-3 (keyless): held entry, not a row; the decided DROP is satisfied by construction. (Barishal 2023 MCQ-3 is a separate row and IS excluded under bucket D.)

## Kept with caveats (in the file, flagged in-row; parent may pull)

- ch11-creative-120: partial row, printed gha sub-answer absent from the present range; kept as collected with its flag.
- Special model-MCQ sets 07-22 (400 rows): keys are grid-verbatim as collected, but section 9.18 re-verification for those sets was noted pending in prior work; no verdicts exist for them. Keys are present, not null.
- A small number of rows carry 'tile-check pending' wording-only flags with keys confirmed; kept as collected.
- Diagram-flagged rows are kept flagged in the file (separate bucket for counting purposes only, per standing rule).

## Output files

- Import-ready: /home/hatch/workspace/yes-sir-ai-guides/class9-10/talimit/chemistry/_work/import-prep-2026-11-04/chemistry-import-ready.jsonl
- Held-out buckets: /home/hatch/workspace/yes-sir-ai-guides/class9-10/talimit/chemistry/_work/import-prep-2026-11-04/chemistry-held-out-2026-11-04.md
- This report: /home/hatch/workspace/yes-sir-ai-guides/class9-10/talimit/chemistry/_work/import-prep-2026-11-04/chemistry-import-verification-2026-11-04.md
