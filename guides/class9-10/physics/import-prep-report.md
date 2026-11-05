# Physics import-prep report — Yes Sir AI guide pipeline

- **Book:** Newton Physics, code 136, class 10, SSC 2026
- **Proposed book_id:** `class9-physics-bn-guide`, subject `physics`, class_id **9 (proposed, Islam precedent — coordinator confirms pre-live)**
- **Scope:** DRY-RUN ONLY. No database connection was opened, no database write made, no Edge/app file edited, no zip, no download, no user message, no password/token sought or used.
- **Inputs (read-only, unmodified):** `_work/collection/phy-*.json` + `_work/verification/` audits listed in §2.
- **Outputs (all under `_work/import-prep/`):**
  - `normalized/phy-rows-normalized.json` — 6,700 rows
  - `normalized/phy-held-normalized.json` — 369 held
  - `normalized/phy-chunks-normalized.json` — 72 chunks
  - `normalized/phy-sets-normalized.json` — 66 sets
  - `import_physics.py` — guarded dry-run script (exit 0, all guards green)
  - `import_physics_audit.json` — dry-run audit (ids + counts only, no guide text)
  - `no-disc-decisions.json` — the 27 per-row no-disc decisions
  - `build_normalized.py` — the builder that produced the normalized files (kept for reproducibility)

## 1. Counts before → after corrections

| Total | Before | After |
|---|---|---|
| Rows | 6,701 | 6,700 (−1: triage move-to-held, §3.6) |
| Held | 368 | 369 (+1: same move) |
| Chunks | 72 | 72 |
| Sets | 66 | 66 |
| Diagram-dependent rows (counted SEPARATELY, never in completion math) | 824 | 823 in rows + 1 moved to held |
| Countable rows (rows − diagram) | 5,877 | 5,877 (6,700 − 823) |

### Per file

| File | Rows before | Rows after | Held before | Held after |
|---|---|---|---|---|
| phy-board.json | 394 | 394 | 200 | 200 |
| phy-ch1.json | 671 | 671 | 5 | 5 |
| phy-ch2.json | 820 | 820 | 13 | 13 |
| phy-ch3.json | 827 | 827 | 9 | 9 |
| phy-ch4.json | 876 | 876 | 66 | 66 |
| phy-ch7.json | 765 | 765 | 22 | 22 |
| phy-ch8.json | 763 | 762 | 9 | 10 |
| phy-ch10.json | 666 | 666 | 35 | 35 |
| phy-practical.json | 70 | 70 | 0 | 0 |
| phy-special.json | 849 | 849 | 9 | 9 |

Only ch8 changes: `phy-ch8-formula-bank-20` moves rows → held. Every other file is row-count-identical.

### Per section (values KEPT AS COLLECTED — no folding, splitting, or renaming)

| Section | Before | After |
|---|---|---|
| activity | 14 | 14 |
| applied-math | 20 | 20 |
| board-creative | 89 | 89 |
| board-mcq | 305 | 305 |
| comprehension-qa | 111 | 111 |
| conceptual-creative | 11 | 11 |
| creative | 492 | 492 |
| exercise-qa | 97 | 97 |
| formula-math | 647 | 646 |
| knowledge-qa | 290 | 290 |
| mcq-bank | 1889 | 1889 |
| model-creative | 202 | 202 |
| model-mcq | 717 | 717 |
| model-short | 203 | 203 |
| practice-math | 57 | 57 |
| quiz | 709 | 709 |
| short-qa | 734 | 734 |
| type-bank | 44 | 44 |
| viva | 70 | 70 |

Notes on kept-as-collected section shapes (preserved, not decided here):
- `comprehension-qa` (111) is combined knowledge+comprehension in ch1/ch2/ch7/ch10 and split in ch3/ch4/ch8 — kept exactly as collected in each file.
- `knowledge-qa` (290) is the combined section in ch1/ch2/ch7/ch10 and the split section in ch3/ch4/ch8 — kept as collected.
- `applied-math` (20: ch2 13 + ch3 7), `practice-math` (57: ch3 only), `type-bank` (44: ch2 only) kept as collected.
- Creative rows: 492, every one with `marks_parts` `[1,2,3,4]` (kept, verified by the dry-run guard).

## 2. Correction-application log

Sources applied, in order: board-grid-audit (305 rows) → chapter-mcq audits (1,889 rows) → model-grid-audit (717 rows, zero corrections) → ch1-verbatim-pass (354 rows) → flagged-triage-ch4-ch8 (355 rows). All audit ids resolved to collection rows (verified: zero missing ids in any audit file).

### 2.1 Board corrections — 106 (verdict=correct, audit_key applied; every one changed the key)

- phy-board-barishal-2023-board-mcq-3: খ → ঘ
- phy-board-barishal-2023-board-mcq-8: গ → ক
- phy-board-barishal-2023-board-mcq-10: খ → ঘ
- phy-board-barishal-2023-board-mcq-12: খ → গ
- phy-board-barishal-2023-board-mcq-16: খ → গ
- phy-board-barishal-2023-board-mcq-17: ঘ → খ
- phy-board-barishal-2023-board-mcq-19: ঘ → খ
- phy-board-barishal-2023-board-mcq-21: গ → ক
- phy-board-barishal-2023-board-mcq-22: খ → গ
- phy-board-barishal-2023-board-mcq-23: খ → গ
- phy-board-barishal-2023-board-mcq-25: খ → গ
- phy-board-barishal-2024-board-mcq-9: খ → ক
- phy-board-barishal-2024-board-mcq-16: গ → ক
- phy-board-barishal-2024-board-mcq-20: গ → ক
- phy-board-chattogram-2023-board-mcq-10: খ → গ
- phy-board-chattogram-2023-board-mcq-22: ঘ → ক
- phy-board-chattogram-2023-board-mcq-23: খ → গ
- phy-board-chattogram-2023-board-mcq-25: গ → ক
- phy-board-chattogram-2024-board-mcq-2: খ → গ
- phy-board-chattogram-2024-board-mcq-7: গ → খ
- phy-board-chattogram-2024-board-mcq-19: খ → গ
- phy-board-chattogram-2024-board-mcq-25: গ → খ
- phy-board-cumilla-2023-board-mcq-5: গ → ক
- phy-board-cumilla-2023-board-mcq-9: খ → গ
- phy-board-cumilla-2023-board-mcq-23: খ → গ
- phy-board-cumilla-2024-board-mcq-1: খ → গ
- phy-board-cumilla-2024-board-mcq-5: খ → ক
- phy-board-cumilla-2024-board-mcq-6: খ → গ
- phy-board-cumilla-2024-board-mcq-14: খ → গ
- phy-board-cumilla-2024-board-mcq-17: গ → ক
- phy-board-cumilla-2024-board-mcq-21: খ → গ
- phy-board-cumilla-2024-board-mcq-25: গ → খ
- phy-board-dhaka-2023-board-mcq-8: None → গ
- phy-board-dhaka-2024-board-mcq-3: খ → গ
- phy-board-dhaka-2024-board-mcq-6: খ → গ
- phy-board-dhaka-2024-board-mcq-9: গ → খ
- phy-board-dhaka-2024-board-mcq-10: খ → ঘ
- phy-board-dhaka-2024-board-mcq-13: খ → গ
- phy-board-dhaka-2024-board-mcq-14: খ → গ
- phy-board-dhaka-2024-board-mcq-20: খ → গ
- phy-board-dinajpur-2023-board-mcq-3: খ → গ
- phy-board-dinajpur-2023-board-mcq-4: খ → গ
- phy-board-dinajpur-2023-board-mcq-5: খ → গ
- phy-board-dinajpur-2023-board-mcq-7: গ → খ
- phy-board-dinajpur-2023-board-mcq-12: খ → ঘ
- phy-board-dinajpur-2023-board-mcq-16: খ → গ
- phy-board-dinajpur-2023-board-mcq-17: খ → গ
- phy-board-dinajpur-2023-board-mcq-18: খ → গ
- phy-board-dinajpur-2023-board-mcq-19: খ → গ
- phy-board-dinajpur-2023-board-mcq-21: গ → ক
- phy-board-dinajpur-2023-board-mcq-22: গ → খ
- phy-board-dinajpur-2024-board-mcq-5: গ → ক
- phy-board-dinajpur-2024-board-mcq-9: খ → ক
- phy-board-jessore-2023-board-mcq-2: খ → ক
- phy-board-jessore-2023-board-mcq-7: খ → গ
- phy-board-jessore-2023-board-mcq-9: খ → গ
- phy-board-jessore-2023-board-mcq-16: খ → গ
- phy-board-jessore-2023-board-mcq-18: গ → ক
- phy-board-jessore-2023-board-mcq-19: খ → গ
- phy-board-jessore-2023-board-mcq-21: খ → গ
- phy-board-jessore-2023-board-mcq-22: গ → ক
- phy-board-jessore-2023-board-mcq-24: খ → গ
- phy-board-jessore-2024-board-mcq-6: খ → গ
- phy-board-jessore-2024-board-mcq-7: গ → খ
- phy-board-jessore-2024-board-mcq-8: খ → ক
- phy-board-jessore-2024-board-mcq-9: গ → খ
- phy-board-jessore-2024-board-mcq-10: গ → ক
- phy-board-jessore-2024-board-mcq-21: খ → গ
- phy-board-mymensingh-2023-board-mcq-3: গ → ক
- phy-board-mymensingh-2023-board-mcq-4: খ → গ
- phy-board-mymensingh-2023-board-mcq-5: গ → ক
- phy-board-mymensingh-2023-board-mcq-6: গ → ক
- phy-board-mymensingh-2023-board-mcq-10: গ → ক
- phy-board-mymensingh-2023-board-mcq-17: খ → গ
- phy-board-mymensingh-2023-board-mcq-20: গ → ক
- phy-board-mymensingh-2023-board-mcq-21: খ → গ
- phy-board-mymensingh-2024-board-mcq-1: গ → খ
- phy-board-mymensingh-2024-board-mcq-13: গ → ক
- phy-board-mymensingh-2024-board-mcq-16: গ → খ
- phy-board-mymensingh-2024-board-mcq-17: গ → ক
- phy-board-mymensingh-2024-board-mcq-22: গ → খ
- phy-board-rajshahi-2023-board-mcq-1: ঘ → খ
- phy-board-rajshahi-2023-board-mcq-3: ঘ → গ
- phy-board-rajshahi-2023-board-mcq-5: গ → ঘ
- phy-board-rajshahi-2023-board-mcq-8: গ → খ
- phy-board-rajshahi-2024-board-mcq-4: খ → গ
- phy-board-rajshahi-2024-board-mcq-5: গ → ক
- phy-board-rajshahi-2024-board-mcq-6: খ → গ
- phy-board-rajshahi-2024-board-mcq-10: খ → গ
- phy-board-rajshahi-2024-board-mcq-13: গ → ক
- phy-board-rajshahi-2024-board-mcq-16: খ → গ
- phy-board-rajshahi-2024-board-mcq-22: খ → গ
- phy-board-sylhet-2023-board-mcq-3: খ → গ
- phy-board-sylhet-2023-board-mcq-4: গ → ক
- phy-board-sylhet-2023-board-mcq-6: গ → ক
- phy-board-sylhet-2023-board-mcq-8: গ → ক
- phy-board-sylhet-2023-board-mcq-10: খ → গ
- phy-board-sylhet-2023-board-mcq-14: গ → খ
- phy-board-sylhet-2023-board-mcq-16: গ → ক
- phy-board-sylhet-2023-board-mcq-19: গ → ক
- phy-board-sylhet-2023-board-mcq-21: খ → গ
- phy-board-sylhet-2024-board-mcq-11: খ → গ
- phy-board-sylhet-2024-board-mcq-14: খ → গ
- phy-board-sylhet-2024-board-mcq-16: খ → গ
- phy-board-sylhet-2024-board-mcq-19: খ → গ
- phy-board-sylhet-2024-board-mcq-20: গ → খ

- Board agree: 194 unchanged. Board null-confirmed: 5 stay null (see §2.4). Includes Dhaka 2023 Q8 null → গ.

### 2.2 Chapter-bank corrections — 573 (verdict=correct AND audit_key non-null; every one changed the key)

Per chapter: ch1 16, ch2 24, ch3 58, ch4 64, ch7 147, ch8 188, ch10 76. (ch2's 25th `correct` and ch10's 26 `correct` rows are the no-disc nulls of §2.5, not counted here.)

- phy-ch1-mcq-bank-034: ক → খ
- phy-ch1-mcq-bank-122: ঘ → ক
- phy-ch1-mcq-bank-124: ক → খ
- phy-ch1-mcq-bank-127: ঘ → খ
- phy-ch1-mcq-bank-128: খ → গ
- phy-ch1-mcq-bank-129: খ → গ
- phy-ch1-mcq-bank-151: ঘ → খ
- phy-ch1-mcq-bank-156: ক → ঘ
- phy-ch1-mcq-bank-173: গ → ক
- phy-ch1-mcq-bank-203: গ → ক
- phy-ch1-mcq-bank-204: ক → খ
- phy-ch1-mcq-bank-205: খ → গ
- phy-ch1-mcq-bank-207: খ → ক
- phy-ch1-mcq-bank-219: ঘ → গ
- phy-ch1-mcq-bank-226: খ → ঘ
- phy-ch1-mcq-bank-230: খ → ক
- phy-ch2-mcq-bank-55: গ → ঘ
- phy-ch2-mcq-bank-113: গ → খ
- phy-ch2-mcq-bank-116: গ → খ
- phy-ch2-mcq-bank-117: খ → ঘ
- phy-ch2-mcq-bank-121: গ → খ
- phy-ch2-mcq-bank-179: খ → ঘ
- phy-ch2-mcq-bank-189: ঘ → গ
- phy-ch2-mcq-bank-210: গ → ক
- phy-ch2-mcq-bank-233: ক → গ
- phy-ch2-mcq-bank-244: ঘ → খ
- phy-ch2-mcq-bank-268: ঘ → ক
- phy-ch2-mcq-bank-269: ক → গ
- phy-ch2-mcq-bank-271: গ → খ
- phy-ch2-mcq-bank-274: ক → খ
- phy-ch2-mcq-bank-275: ঘ → গ
- phy-ch2-mcq-bank-279: ঘ → গ
- phy-ch2-mcq-bank-280: গ → খ
- phy-ch2-mcq-bank-282: খ → ঘ
- phy-ch2-mcq-bank-287: গ → খ
- phy-ch2-mcq-bank-291: গ → খ
- phy-ch2-mcq-bank-293: গ → খ
- phy-ch2-mcq-bank-295: গ → খ
- phy-ch2-mcq-bank-296: গ → ঘ
- phy-ch2-mcq-bank-298: গ → খ
- phy-ch3-mcq-bank-2: গ → ক
- phy-ch3-mcq-bank-4: ঘ → ক
- phy-ch3-mcq-bank-5: গ → খ
- phy-ch3-mcq-bank-9: খ → ক
- phy-ch3-mcq-bank-20: ঘ → গ
- phy-ch3-mcq-bank-21: ঘ → ক
- phy-ch3-mcq-bank-23: খ → ক
- phy-ch3-mcq-bank-37: গ → খ
- phy-ch3-mcq-bank-38: গ → খ
- phy-ch3-mcq-bank-43: খ → গ
- phy-ch3-mcq-bank-56: গ → খ
- phy-ch3-mcq-bank-83: গ → ক
- phy-ch3-mcq-bank-84: খ → ক
- phy-ch3-mcq-bank-87: ঘ → খ
- phy-ch3-mcq-bank-104: ঘ → খ
- phy-ch3-mcq-bank-117: গ → খ
- phy-ch3-mcq-bank-118: গ → খ
- phy-ch3-mcq-bank-120: গ → ক
- phy-ch3-mcq-bank-125: গ → খ
- phy-ch3-mcq-bank-126: গ → খ
- phy-ch3-mcq-bank-127: গ → খ
- phy-ch3-mcq-bank-128: গ → খ
- phy-ch3-mcq-bank-132: গ → খ
- phy-ch3-mcq-bank-136: গ → খ
- phy-ch3-mcq-bank-144: খ → ক
- phy-ch3-mcq-bank-146: খ → ক
- phy-ch3-mcq-bank-148: গ → খ
- phy-ch3-mcq-bank-150: গ → খ
- phy-ch3-mcq-bank-152: গ → খ
- phy-ch3-mcq-bank-157: গ → খ
- phy-ch3-mcq-bank-161: গ → খ
- phy-ch3-mcq-bank-162: খ → ক
- phy-ch3-mcq-bank-165: গ → খ
- phy-ch3-mcq-bank-168: গ → খ
- phy-ch3-mcq-bank-173: গ → খ
- phy-ch3-mcq-bank-174: খ → ক
- phy-ch3-mcq-bank-175: গ → খ
- phy-ch3-mcq-bank-176: গ → খ
- phy-ch3-mcq-bank-177: খ → ঘ
- phy-ch3-mcq-bank-181: গ → খ
- phy-ch3-mcq-bank-184: গ → খ
- phy-ch3-mcq-bank-187: খ → ক
- phy-ch3-mcq-bank-188: গ → খ
- phy-ch3-mcq-bank-198: খ → ঘ
- phy-ch3-mcq-bank-199: ঘ → খ
- phy-ch3-mcq-bank-200: গ → ক
- phy-ch3-mcq-bank-223: গ → খ
- phy-ch3-mcq-bank-224: গ → খ
- phy-ch3-mcq-bank-235: গ → খ
- phy-ch3-mcq-bank-238: খ → ক
- phy-ch3-mcq-bank-240: খ → ক
- phy-ch3-mcq-bank-241: গ → খ
- phy-ch3-mcq-bank-243: ঘ → ক
- phy-ch3-mcq-bank-244: গ → খ
- phy-ch3-mcq-bank-245: খ → ক
- phy-ch3-mcq-bank-249: খ → ক
- phy-ch3-mcq-bank-252: গ → খ
- phy-ch3-mcq-bank-254: ক → ঘ
- phy-ch4-mcq-bank-13: ঘ → খ
- phy-ch4-mcq-bank-16: ঘ → গ
- phy-ch4-mcq-bank-18: গ → ক
- phy-ch4-mcq-bank-53: ক → খ
- phy-ch4-mcq-bank-58: খ → গ
- phy-ch4-mcq-bank-59: গ → ঘ
- phy-ch4-mcq-bank-66: ক → খ
- phy-ch4-mcq-bank-67: ঘ → খ
- phy-ch4-mcq-bank-95: খ → ক
- phy-ch4-mcq-bank-96: গ → খ
- phy-ch4-mcq-bank-104: ঘ → গ
- phy-ch4-mcq-122: ঘ → গ
- phy-ch4-mcq-123: গ → খ
- phy-ch4-mcq-125: গ → খ
- phy-ch4-mcq-126: গ → খ
- phy-ch4-mcq-130: ঘ → গ
- phy-ch4-mcq-132: খ → ক
- phy-ch4-mcq-134: খ → গ
- phy-ch4-mcq-135: খ → গ
- phy-ch4-mcq-142: গ → খ
- phy-ch4-mcq-150: গ → ক
- phy-ch4-mcq-153: ঘ → খ
- phy-ch4-mcq-158: গ → খ
- phy-ch4-mcq-160: গ → খ
- phy-ch4-mcq-165: গ → খ
- phy-ch4-mcq-171: ক → ঘ
- phy-ch4-mcq-182: ঘ → গ
- phy-ch4-mcq-188: ক → ঘ
- phy-ch4-mcq-190: ঘ → গ
- phy-ch4-mcq-191: খ → ঘ
- phy-ch4-mcq-211: ঘ → খ
- phy-ch4-mcq-222: গ → খ
- phy-ch4-mcq-227: গ → ক
- phy-ch4-mcq-228: ঘ → খ
- phy-ch4-mcq-229: ক → খ
- phy-ch4-mcq-230: ঘ → খ
- phy-ch4-mcq-232: ক → খ
- phy-ch4-mcq-256: ক → খ
- phy-ch4-mcq-258: ক → খ
- phy-ch4-mcq-259: গ → খ
- phy-ch4-mcq-260: ক → খ
- phy-ch4-mcq-263: ক → ঘ
- phy-ch4-mcq-267: ঘ → গ
- phy-ch4-mcq-268: খ → গ
- phy-ch4-mcq-283: ক → গ
- phy-ch4-mcq-284: খ → গ
- phy-ch4-mcq-285: খ → গ
- phy-ch4-mcq-286: ক → গ
- phy-ch4-mcq-287: ক → গ
- phy-ch4-mcq-288: ক → গ
- phy-ch4-mcq-289: খ → ঘ
- phy-ch4-mcq-290: গ → ক
- phy-ch4-mcq-291: খ → গ
- phy-ch4-mcq-292: গ → খ
- phy-ch4-mcq-303: খ → ক
- phy-ch4-mcq-306: খ → ঘ
- phy-ch4-mcq-309: ক → ঘ
- phy-ch4-mcq-314: ক → ঘ
- phy-ch4-mcq-316: ক → ঘ
- phy-ch4-mcq-317: ক → ঘ
- phy-ch4-mcq-321: ঘ → গ
- phy-ch4-mcq-329: খ → গ
- phy-ch4-mcq-330: ঘ → গ
- phy-ch4-mcq-332: ঘ → গ
- phy-ch7-mcq-bank-ex-001: গ → খ
- phy-ch7-mcq-bank-ex-002: ক → গ
- phy-ch7-mcq-bank-006: খ → গ
- phy-ch7-mcq-bank-007: ঘ → খ
- phy-ch7-mcq-bank-008: খ → গ
- phy-ch7-mcq-bank-009: খ → গ
- phy-ch7-mcq-bank-010: খ → গ
- phy-ch7-mcq-bank-011: ক → ঘ
- phy-ch7-mcq-bank-012: ক → ঘ
- phy-ch7-mcq-bank-013: খ → ঘ
- phy-ch7-mcq-bank-015: গ → খ
- phy-ch7-mcq-bank-018: ক → ঘ
- phy-ch7-mcq-bank-019: ক → ঘ
- phy-ch7-mcq-bank-021: ঘ → গ
- phy-ch7-mcq-bank-022: খ → গ
- phy-ch7-mcq-bank-023: ক → ঘ
- phy-ch7-mcq-bank-025: ক → খ
- phy-ch7-mcq-bank-026: ঘ → খ
- phy-ch7-mcq-bank-028: গ → খ
- phy-ch7-mcq-bank-029: গ → খ
- phy-ch7-mcq-bank-031: গ → খ
- phy-ch7-mcq-bank-032: গ → খ
- phy-ch7-mcq-bank-033: গ → খ
- phy-ch7-mcq-bank-037: খ → ঘ
- phy-ch7-mcq-bank-042: ক → ঘ
- phy-ch7-mcq-bank-043: গ → খ
- phy-ch7-mcq-bank-046: ক → ঘ
- phy-ch7-mcq-bank-048: ক → ঘ
- phy-ch7-mcq-bank-050: ক → ঘ
- phy-ch7-mcq-bank-051: গ → খ
- phy-ch7-mcq-bank-052: গ → খ
- phy-ch7-mcq-bank-053: গ → খ
- phy-ch7-mcq-bank-054: গ → খ
- phy-ch7-mcq-bank-057: গ → খ
- phy-ch7-mcq-bank-063: ক → খ
- phy-ch7-mcq-bank-067: ক → গ
- phy-ch7-mcq-bank-068: ঘ → গ
- phy-ch7-mcq-bank-073: ক → ঘ
- phy-ch7-mcq-bank-074: গ → খ
- phy-ch7-mcq-bank-076: ক → ঘ
- phy-ch7-mcq-bank-077: ক → ঘ
- phy-ch7-mcq-bank-078: গ → খ
- phy-ch7-mcq-bank-079: ক → ঘ
- phy-ch7-mcq-bank-080: গ → খ
- phy-ch7-mcq-bank-081: ক → ঘ
- phy-ch7-mcq-bank-084: গ → খ
- phy-ch7-mcq-bank-086: গ → খ
- phy-ch7-mcq-bank-088: গ → খ
- phy-ch7-mcq-bank-093: গ → খ
- phy-ch7-mcq-bank-095: ক → ঘ
- phy-ch7-mcq-bank-100: ক → গ
- phy-ch7-mcq-bank-102: ক → গ
- phy-ch7-mcq-bank-103: খ → গ
- phy-ch7-mcq-bank-104: ক → ঘ
- phy-ch7-mcq-bank-105: খ → ঘ
- phy-ch7-mcq-bank-107: ক → ঘ
- phy-ch7-mcq-bank-108: ক → ঘ
- phy-ch7-mcq-bank-110: গ → খ
- phy-ch7-mcq-bank-113: গ → খ
- phy-ch7-mcq-bank-114: গ → খ
- phy-ch7-mcq-bank-115: খ → ঘ
- phy-ch7-mcq-bank-116: খ → ঘ
- phy-ch7-mcq-bank-117: গ → খ
- phy-ch7-mcq-bank-118: ঘ → খ
- phy-ch7-mcq-bank-120: গ → খ
- phy-ch7-mcq-bank-121: ক → ঘ
- phy-ch7-mcq-bank-122: গ → খ
- phy-ch7-mcq-bank-124: ক → ঘ
- phy-ch7-mcq-bank-125: ঘ → খ
- phy-ch7-mcq-bank-140: ক → ঘ
- phy-ch7-mcq-bank-141: ক → ঘ
- phy-ch7-mcq-bank-143: ঘ → খ
- phy-ch7-mcq-bank-144: ক → ঘ
- phy-ch7-mcq-bank-146: খ → ঘ
- phy-ch7-mcq-bank-147: গ → ঘ
- phy-ch7-mcq-bank-158: None → ক
- phy-ch7-mcq-bank-163: ঘ → গ
- phy-ch7-mcq-bank-164: খ → ঘ
- phy-ch7-mcq-bank-165: গ → খ
- phy-ch7-mcq-bank-166: খ → ঘ
- phy-ch7-mcq-bank-168: ক → ঘ
- phy-ch7-mcq-bank-171: ক → ঘ
- phy-ch7-mcq-bank-172: খ → ঘ
- phy-ch7-mcq-bank-173: ক → ঘ
- phy-ch7-mcq-bank-174: ক → ঘ
- phy-ch7-mcq-bank-179: ঘ → গ
- phy-ch7-mcq-bank-185: গ → খ
- phy-ch7-mcq-bank-186: খ → ঘ
- phy-ch7-mcq-bank-187: None → খ
- phy-ch7-mcq-bank-189: ঘ → খ
- phy-ch7-mcq-bank-191: খ → ঘ
- phy-ch7-mcq-bank-192: ক → ঘ
- phy-ch7-mcq-bank-193: খ → ঘ
- phy-ch7-mcq-bank-194: খ → ঘ
- phy-ch7-mcq-bank-195: গ → খ
- phy-ch7-mcq-bank-205: গ → ঘ
- phy-ch7-mcq-bank-206: খ → ঘ
- phy-ch7-mcq-bank-207: গ → খ
- phy-ch7-mcq-bank-208: ক → ঘ
- phy-ch7-mcq-bank-210: গ → খ
- phy-ch7-mcq-bank-211: খ → ঘ
- phy-ch7-mcq-bank-212: গ → খ
- phy-ch7-mcq-bank-214: গ → খ
- phy-ch7-mcq-bank-215: ক → ঘ
- phy-ch7-mcq-bank-217: ক → ঘ
- phy-ch7-mcq-bank-218: খ → ঘ
- phy-ch7-mcq-bank-219: গ → খ
- phy-ch7-mcq-bank-220: খ → ঘ
- phy-ch7-mcq-bank-221: গ → ঘ
- phy-ch7-mcq-bank-222: গ → খ
- phy-ch7-mcq-bank-223: খ → ঘ
- phy-ch7-mcq-bank-224: ক → গ
- phy-ch7-mcq-bank-225: ক → ঘ
- phy-ch7-mcq-bank-226: খ → ঘ
- phy-ch7-mcq-bank-227: খ → ঘ
- phy-ch7-mcq-bank-228: খ → ঘ
- phy-ch7-mcq-bank-229: ক → ঘ
- phy-ch7-mcq-bank-230: খ → ঘ
- phy-ch7-mcq-bank-231: গ → খ
- phy-ch7-mcq-bank-232: ক → খ
- phy-ch7-mcq-bank-233: খ → ঘ
- phy-ch7-mcq-bank-234: গ → খ
- phy-ch7-mcq-bank-235: খ → ঘ
- phy-ch7-mcq-bank-236: ক → ঘ
- phy-ch7-mcq-bank-237: খ → ঘ
- phy-ch7-mcq-bank-238: খ → ঘ
- phy-ch7-mcq-bank-241: গ → খ
- phy-ch7-mcq-bank-242: ক → খ
- phy-ch7-mcq-bank-245: খ → ঘ
- phy-ch7-mcq-bank-246: গ → ঘ
- phy-ch7-mcq-bank-247: খ → ঘ
- phy-ch7-mcq-bank-248: খ → ঘ
- phy-ch7-mcq-bank-251: ঘ → খ
- phy-ch7-mcq-bank-252: ঘ → খ
- phy-ch7-mcq-bank-254: ক → গ
- phy-ch7-mcq-bank-256: গ → খ
- phy-ch7-mcq-bank-257: গ → খ
- phy-ch7-mcq-bank-263: ক → ঘ
- phy-ch7-mcq-bank-267: গ → খ
- phy-ch7-mcq-bank-268: গ → ঘ
- phy-ch7-mcq-bank-271: ক → ঘ
- phy-ch7-mcq-bank-273: গ → খ
- phy-ch7-mcq-bank-274: খ → ঘ
- phy-ch7-mcq-bank-279: গ → খ
- phy-ch7-mcq-bank-281: গ → খ
- phy-ch7-mcq-bank-282: ক → ঘ
- phy-ch7-mcq-bank-284: খ → ঘ
- phy-ch8-mcq-bank-1: গ → ঘ
- phy-ch8-mcq-bank-2: গ → খ
- phy-ch8-mcq-bank-3: গ → খ
- phy-ch8-mcq-bank-7: ক → গ
- phy-ch8-mcq-bank-9: গ → খ
- phy-ch8-mcq-bank-11: গ → খ
- phy-ch8-mcq-bank-12: None → ঘ
- phy-ch8-mcq-bank-13: ক → খ
- phy-ch8-mcq-bank-18: ক → খ
- phy-ch8-mcq-bank-19: গ → ঘ
- phy-ch8-mcq-bank-20: ঘ → খ
- phy-ch8-mcq-bank-21: গ → খ
- phy-ch8-mcq-bank-22: গ → খ
- phy-ch8-mcq-bank-24: গ → খ
- phy-ch8-mcq-bank-25: খ → ঘ
- phy-ch8-mcq-bank-26: খ → ঘ
- phy-ch8-mcq-bank-31: ক → ঘ
- phy-ch8-mcq-bank-32: গ → খ
- phy-ch8-mcq-bank-33: গ → ঘ
- phy-ch8-mcq-bank-35: খ → ঘ
- phy-ch8-mcq-bank-36: ক → ঘ
- phy-ch8-mcq-bank-38: ক → ঘ
- phy-ch8-mcq-bank-39: খ → ঘ
- phy-ch8-mcq-bank-40: গ → খ
- phy-ch8-mcq-bank-41: গ → খ
- phy-ch8-mcq-bank-42: গ → খ
- phy-ch8-mcq-bank-43: খ → ঘ
- phy-ch8-mcq-bank-44: ক → ঘ
- phy-ch8-mcq-bank-46: গ → খ
- phy-ch8-mcq-bank-47: গ → খ
- phy-ch8-mcq-bank-48: গ → খ
- phy-ch8-mcq-bank-51: ক → ঘ
- phy-ch8-mcq-bank-52: ক → ঘ
- phy-ch8-mcq-bank-53: ক → ঘ
- phy-ch8-mcq-bank-55: গ → খ
- phy-ch8-mcq-bank-57: ক → ঘ
- phy-ch8-mcq-bank-58: গ → খ
- phy-ch8-mcq-bank-60: গ → খ
- phy-ch8-mcq-bank-61: ক → ঘ
- phy-ch8-mcq-bank-62: ক → ঘ
- phy-ch8-mcq-bank-63: ঘ → খ
- phy-ch8-mcq-bank-64: গ → ঘ
- phy-ch8-mcq-bank-65: খ → ঘ
- phy-ch8-mcq-bank-68: খ → ঘ
- phy-ch8-mcq-bank-70: গ → খ
- phy-ch8-mcq-bank-71: খ → ঘ
- phy-ch8-mcq-bank-72: খ → ঘ
- phy-ch8-mcq-bank-73: গ → খ
- phy-ch8-mcq-bank-74: খ → ঘ
- phy-ch8-mcq-bank-75: গ → খ
- phy-ch8-mcq-bank-77: খ → ঘ
- phy-ch8-mcq-bank-78: গ → খ
- phy-ch8-mcq-bank-79: ক → ঘ
- phy-ch8-mcq-bank-80: গ → খ
- phy-ch8-mcq-bank-81: গ → খ
- phy-ch8-mcq-bank-82: গ → খ
- phy-ch8-mcq-bank-84: খ → ঘ
- phy-ch8-mcq-bank-85: ক → ঘ
- phy-ch8-mcq-bank-88: গ → খ
- phy-ch8-mcq-bank-89: খ → ঘ
- phy-ch8-mcq-bank-90: ক → ঘ
- phy-ch8-mcq-bank-91: খ → ঘ
- phy-ch8-mcq-bank-93: ক → ঘ
- phy-ch8-mcq-bank-94: ক → ঘ
- phy-ch8-mcq-bank-95: ক → ঘ
- phy-ch8-mcq-bank-96: গ → খ
- phy-ch8-mcq-bank-97: ক → ঘ
- phy-ch8-mcq-bank-98: ক → ঘ
- phy-ch8-mcq-bank-99: গ → খ
- phy-ch8-mcq-bank-101: খ → ঘ
- phy-ch8-mcq-bank-103: ক → ঘ
- phy-ch8-mcq-bank-105: গ → খ
- phy-ch8-mcq-bank-106: গ → খ
- phy-ch8-mcq-bank-108: গ → খ
- phy-ch8-mcq-bank-109: গ → খ
- phy-ch8-mcq-bank-110: গ → খ
- phy-ch8-mcq-bank-111: খ → ঘ
- phy-ch8-mcq-bank-117: গ → খ
- phy-ch8-mcq-bank-118: খ → ঘ
- phy-ch8-mcq-bank-120: খ → ঘ
- phy-ch8-mcq-bank-121: খ → ঘ
- phy-ch8-mcq-bank-122: গ → খ
- phy-ch8-mcq-bank-123: গ → খ
- phy-ch8-mcq-bank-124: ক → ঘ
- phy-ch8-mcq-bank-125: ক → ঘ
- phy-ch8-mcq-bank-126: গ → খ
- phy-ch8-mcq-bank-127: ক → ঘ
- phy-ch8-mcq-bank-129: ক → ঘ
- phy-ch8-mcq-bank-131: খ → ঘ
- phy-ch8-mcq-bank-132: ক → ঘ
- phy-ch8-mcq-bank-133: ক → ঘ
- phy-ch8-mcq-bank-135: ক → ঘ
- phy-ch8-mcq-bank-136: ক → ঘ
- phy-ch8-mcq-bank-137: গ → খ
- phy-ch8-mcq-bank-138: ক → ঘ
- phy-ch8-mcq-bank-140: ক → ঘ
- phy-ch8-mcq-bank-145: খ → ঘ
- phy-ch8-mcq-bank-146: ঘ → খ
- phy-ch8-mcq-bank-147: গ → খ
- phy-ch8-mcq-bank-149: গ → খ
- phy-ch8-mcq-bank-151: ক → ঘ
- phy-ch8-mcq-bank-152: গ → খ
- phy-ch8-mcq-bank-153: ক → ঘ
- phy-ch8-mcq-bank-154: গ → খ
- phy-ch8-mcq-bank-155: খ → ঘ
- phy-ch8-mcq-bank-156: খ → ঘ
- phy-ch8-mcq-bank-157: খ → ঘ
- phy-ch8-mcq-bank-158: ক → খ
- phy-ch8-mcq-bank-159: ঘ → খ
- phy-ch8-mcq-bank-161: ঘ → খ
- phy-ch8-mcq-bank-162: ঘ → খ
- phy-ch8-mcq-bank-163: ক → ঘ
- phy-ch8-mcq-bank-164: গ → খ
- phy-ch8-mcq-bank-165: গ → খ
- phy-ch8-mcq-bank-171: ক → ঘ
- phy-ch8-mcq-bank-172: গ → খ
- phy-ch8-mcq-bank-173: গ → খ
- phy-ch8-mcq-bank-175: ক → ঘ
- phy-ch8-mcq-bank-176: ক → ঘ
- phy-ch8-mcq-bank-177: গ → খ
- phy-ch8-mcq-bank-180: খ → ঘ
- phy-ch8-mcq-bank-181: গ → খ
- phy-ch8-mcq-bank-183: খ → ঘ
- phy-ch8-mcq-bank-184: খ → ঘ
- phy-ch8-mcq-bank-186: খ → ঘ
- phy-ch8-mcq-bank-188: গ → ঘ
- phy-ch8-mcq-bank-189: ক → ঘ
- phy-ch8-mcq-bank-190: ক → ঘ
- phy-ch8-mcq-bank-195: ক → ঘ
- phy-ch8-mcq-bank-196: ক → ঘ
- phy-ch8-mcq-bank-198: খ → ঘ
- phy-ch8-mcq-bank-199: গ → খ
- phy-ch8-mcq-bank-200: গ → খ
- phy-ch8-mcq-bank-201: খ → ঘ
- phy-ch8-mcq-bank-211: গ → খ
- phy-ch8-mcq-bank-213: গ → খ
- phy-ch8-mcq-bank-214: খ → ঘ
- phy-ch8-mcq-bank-215: ক → ঘ
- phy-ch8-mcq-bank-216: খ → ঘ
- phy-ch8-mcq-bank-217: খ → ঘ
- phy-ch8-mcq-bank-218: গ → ঘ
- phy-ch8-mcq-bank-220: ক → ঘ
- phy-ch8-mcq-bank-221: গ → খ
- phy-ch8-mcq-bank-222: গ → খ
- phy-ch8-mcq-bank-223: ক → ঘ
- phy-ch8-mcq-bank-226: গ → খ
- phy-ch8-mcq-bank-227: ক → ঘ
- phy-ch8-mcq-bank-231: গ → খ
- phy-ch8-mcq-bank-233: খ → ঘ
- phy-ch8-mcq-bank-235: খ → ঘ
- phy-ch8-mcq-bank-236: গ → খ
- phy-ch8-mcq-bank-237: গ → খ
- phy-ch8-mcq-bank-239: খ → ঘ
- phy-ch8-mcq-bank-240: গ → খ
- phy-ch8-mcq-bank-241: গ → খ
- phy-ch8-mcq-bank-242: গ → খ
- phy-ch8-mcq-bank-243: খ → ঘ
- phy-ch8-mcq-bank-244: গ → খ
- phy-ch8-mcq-bank-245: খ → ঘ
- phy-ch8-mcq-bank-246: খ → ঘ
- phy-ch8-mcq-bank-247: ক → ঘ
- phy-ch8-mcq-bank-248: গ → ঘ
- phy-ch8-mcq-bank-249: ক → খ
- phy-ch8-mcq-bank-250: ক → ঘ
- phy-ch8-mcq-bank-251: ঘ → খ
- phy-ch8-mcq-bank-253: গ → খ
- phy-ch8-mcq-bank-256: ক → ঘ
- phy-ch8-mcq-bank-259: গ → খ
- phy-ch8-mcq-bank-262: ক → ঘ
- phy-ch8-mcq-bank-263: খ → ঘ
- phy-ch8-mcq-bank-264: গ → ঘ
- phy-ch8-mcq-bank-265: ঘ → খ
- phy-ch8-mcq-bank-266: খ → ঘ
- phy-ch8-mcq-bank-268: ক → ঘ
- phy-ch8-mcq-bank-269: গ → ঘ
- phy-ch8-mcq-bank-270: খ → ঘ
- phy-ch8-mcq-bank-271: ক → খ
- phy-ch8-mcq-bank-272: খ → ঘ
- phy-ch8-mcq-bank-273: খ → ঘ
- phy-ch8-mcq-bank-276: ক → ঘ
- phy-ch8-mcq-bank-277: খ → ঘ
- phy-ch8-mcq-bank-279: খ → ঘ
- phy-ch8-mcq-bank-280: ক → খ
- phy-ch8-mcq-bank-286: ক → ঘ
- phy-ch8-mcq-bank-290: খ → ঘ
- phy-ch8-mcq-bank-291: খ → ঘ
- phy-ch8-mcq-bank-292: গ → খ
- phy-ch8-mcq-bank-293: ক → ঘ
- phy-ch10-mcq-bank-4: খ → ঘ
- phy-ch10-mcq-bank-7: ক → ঘ
- phy-ch10-mcq-bank-8: গ → খ
- phy-ch10-mcq-bank-9: ক → ঘ
- phy-ch10-mcq-bank-10: গ → খ
- phy-ch10-mcq-bank-11: ক → ঘ
- phy-ch10-mcq-bank-15: গ → খ
- phy-ch10-mcq-bank-17: ক → ঘ
- phy-ch10-mcq-bank-23: গ → খ
- phy-ch10-mcq-bank-24: খ → ঘ
- phy-ch10-mcq-bank-26: খ → ঘ
- phy-ch10-mcq-bank-27: গ → খ
- phy-ch10-mcq-bank-28: গ → ঘ
- phy-ch10-mcq-bank-30: গ → খ
- phy-ch10-mcq-bank-31: গ → ঘ
- phy-ch10-mcq-bank-33: ক → ঘ
- phy-ch10-mcq-bank-34: ক → ঘ
- phy-ch10-mcq-bank-36: None → ক
- phy-ch10-mcq-bank-49: গ → খ
- phy-ch10-mcq-bank-52: গ → খ
- phy-ch10-mcq-bank-55: গ → খ
- phy-ch10-mcq-bank-58: ক → ঘ
- phy-ch10-mcq-bank-61: খ → ঘ
- phy-ch10-mcq-bank-62: খ → ঘ
- phy-ch10-mcq-bank-63: গ → খ
- phy-ch10-mcq-bank-64: ক → ঘ
- phy-ch10-mcq-bank-65: খ → ঘ
- phy-ch10-mcq-bank-82: খ → ঘ
- phy-ch10-mcq-bank-90: খ → ঘ
- phy-ch10-mcq-bank-91: ক → ঘ
- phy-ch10-mcq-bank-92: খ → ঘ
- phy-ch10-mcq-bank-93: ক → ঘ
- phy-ch10-mcq-bank-94: খ → ঘ
- phy-ch10-mcq-bank-97: ঘ → খ
- phy-ch10-mcq-bank-98: গ → খ
- phy-ch10-mcq-bank-99: গ → খ
- phy-ch10-mcq-bank-100: গ → খ
- phy-ch10-mcq-bank-102: গ → ঘ
- phy-ch10-mcq-bank-118: ক → ঘ
- phy-ch10-mcq-bank-121: গ → খ
- phy-ch10-mcq-bank-122: খ → ঘ
- phy-ch10-mcq-bank-123: খ → গ
- phy-ch10-mcq-bank-126: খ → গ
- phy-ch10-mcq-bank-129: খ → ক
- phy-ch10-mcq-bank-134: গ → খ
- phy-ch10-mcq-bank-137: ক → ঘ
- phy-ch10-mcq-bank-144: গ → খ
- phy-ch10-mcq-bank-145: গ → খ
- phy-ch10-mcq-bank-147: গ → খ
- phy-ch10-mcq-bank-148: গ → খ
- phy-ch10-mcq-bank-149: ক → ঘ
- phy-ch10-mcq-bank-152: খ → গ
- phy-ch10-mcq-bank-153: ঘ → খ
- phy-ch10-mcq-bank-168: খ → ক
- phy-ch10-mcq-bank-177: ক → ঘ
- phy-ch10-mcq-bank-179: গ → খ
- phy-ch10-mcq-bank-180: গ → খ
- phy-ch10-mcq-bank-181: ক → ঘ
- phy-ch10-mcq-bank-182: গ → খ
- phy-ch10-mcq-bank-183: খ → ঘ
- phy-ch10-mcq-bank-184: খ → ঘ
- phy-ch10-mcq-bank-186: গ → খ
- phy-ch10-mcq-bank-188: খ → ঘ
- phy-ch10-mcq-bank-189: গ → ঘ
- phy-ch10-mcq-bank-192: গ → ঘ
- phy-ch10-mcq-bank-193: ক → খ
- phy-ch10-mcq-bank-194: ঘ → খ
- phy-ch10-mcq-bank-195: গ → ঘ
- phy-ch10-mcq-bank-196: ঘ → খ
- phy-ch10-mcq-bank-197: গ → ঘ
- phy-ch10-mcq-bank-205: None → খ
- phy-ch10-mcq-bank-207: ঘ → ক
- phy-ch10-mcq-bank-208: খ → ঘ
- phy-ch10-mcq-bank-211: None → খ
- phy-ch10-mcq-bank-212: None → খ
- phy-ch10-mcq-bank-214: ক → ঘ

### 2.3 Conflict-unresolved — 103 kept (collected key kept + flag strengthened)

- phy-ch1-mcq-bank-171 (collected খ kept)
- phy-ch1-mcq-bank-235 (collected ঘ kept)
- phy-ch2-mcq-bank-135 (collected খ kept)
- phy-ch2-mcq-bank-136 (collected ক kept)
- phy-ch2-mcq-bank-137 (collected খ kept)
- phy-ch2-mcq-bank-138 (collected গ kept)
- phy-ch2-mcq-bank-139 (collected ঘ kept)
- phy-ch2-mcq-bank-140 (collected গ kept)
- phy-ch2-mcq-bank-141 (collected খ kept)
- phy-ch2-mcq-bank-142 (collected খ kept)
- phy-ch2-mcq-bank-208 (collected ক kept)
- phy-ch2-mcq-bank-211 (collected ঘ kept)
- phy-ch2-mcq-bank-228 (collected ঘ kept)
- phy-ch2-mcq-bank-230 (collected গ kept)
- phy-ch2-mcq-bank-231 (collected গ kept)
- phy-ch2-mcq-bank-260 (collected ক kept)
- phy-ch2-mcq-bank-261 (collected গ kept)
- phy-ch2-mcq-bank-262 (collected গ kept)
- phy-ch2-mcq-bank-263 (collected ঘ kept)
- phy-ch2-mcq-bank-264 (collected গ kept)
- phy-ch2-mcq-bank-265 (collected খ kept)
- phy-ch2-mcq-bank-266 (collected ক kept)
- phy-ch3-mcq-bank-1 (collected গ kept)
- phy-ch3-mcq-bank-3 (collected খ kept)
- phy-ch3-mcq-bank-6 (collected খ kept)
- phy-ch3-mcq-bank-49 (collected গ kept)
- phy-ch3-mcq-bank-50 (collected গ kept)
- phy-ch3-mcq-bank-51 (collected খ kept)
- phy-ch3-mcq-bank-79 (collected খ kept)
- phy-ch3-mcq-bank-80 (collected গ kept)
- phy-ch3-mcq-bank-81 (collected খ kept)
- phy-ch3-mcq-bank-82 (collected খ kept)
- phy-ch3-mcq-bank-111 (collected ঘ kept)
- phy-ch3-mcq-bank-112 (collected খ kept)
- phy-ch3-mcq-bank-113 (collected খ kept)
- phy-ch3-mcq-bank-139 (collected ঘ kept)
- phy-ch3-mcq-bank-140 (collected ঘ kept)
- phy-ch3-mcq-bank-166 (collected ক kept)
- phy-ch3-mcq-bank-167 (collected গ kept)
- phy-ch3-mcq-bank-185 (collected ঘ kept)
- phy-ch3-mcq-bank-186 (collected ক kept)
- phy-ch3-mcq-bank-212 (collected গ kept)
- phy-ch3-mcq-bank-213 (collected ক kept)
- phy-ch3-mcq-bank-214 (collected ক kept)
- phy-ch3-mcq-bank-215 (collected খ kept)
- phy-ch3-mcq-bank-216 (collected ঘ kept)
- phy-ch3-mcq-bank-217 (collected গ kept)
- phy-ch3-mcq-bank-218 (collected ঘ kept)
- phy-ch3-mcq-bank-219 (collected ক kept)
- phy-ch3-mcq-bank-220 (collected ক kept)
- phy-ch3-mcq-bank-222 (collected ঘ kept)
- phy-ch3-mcq-bank-237 (collected ক kept)
- phy-ch4-mcq-bank-1 (collected ক kept)
- phy-ch4-mcq-bank-2 (collected ঘ kept)
- phy-ch4-mcq-bank-23 (collected গ kept)
- phy-ch4-mcq-bank-24 (collected খ kept)
- phy-ch4-mcq-bank-25 (collected গ kept)
- phy-ch4-mcq-bank-26 (collected ক kept)
- phy-ch4-mcq-bank-51 (collected খ kept)
- phy-ch4-mcq-bank-52 (collected গ kept)
- phy-ch4-mcq-bank-78 (collected ক kept)
- phy-ch4-mcq-bank-79 (collected খ kept)
- phy-ch4-mcq-bank-80 (collected ঘ kept)
- phy-ch4-mcq-bank-81 (collected গ kept)
- phy-ch4-mcq-bank-82 (collected ক kept)
- phy-ch4-mcq-bank-83 (collected ক kept)
- phy-ch4-mcq-bank-84 (collected ক ও ঘ kept)
- phy-ch4-mcq-bank-85 (collected ক kept)
- phy-ch4-mcq-bank-86 (collected ক kept)
- phy-ch4-mcq-112 (collected গ kept)
- phy-ch4-mcq-113 (collected গ kept)
- phy-ch4-mcq-114 (collected খ kept)
- phy-ch4-mcq-115 (collected গ kept)
- phy-ch4-mcq-116 (collected গ kept)
- phy-ch4-mcq-117 (collected ঘ kept)
- phy-ch4-mcq-118 (collected খ kept)
- phy-ch4-mcq-145 (collected গ kept)
- phy-ch4-mcq-146 (collected খ kept)
- phy-ch4-mcq-147 (collected ক kept)
- phy-ch4-mcq-177 (collected খ kept)
- phy-ch4-mcq-178 (collected ক kept)
- phy-ch4-mcq-179 (collected খ kept)
- phy-ch4-mcq-180 (collected খ kept)
- phy-ch4-mcq-181 (collected খ kept)
- phy-ch4-mcq-183 (collected ক kept)
- phy-ch4-mcq-197 (collected গ kept)
- phy-ch4-mcq-198 (collected ঘ kept)
- phy-ch4-mcq-199 (collected ঘ kept)
- phy-ch4-mcq-200 (collected গ kept)
- phy-ch4-mcq-201 (collected ঘ kept)
- phy-ch4-mcq-217 (collected খ kept)
- phy-ch4-mcq-218 (collected খ kept)
- phy-ch4-mcq-219 (collected ক kept)
- phy-ch4-mcq-220 (collected খ kept)
- phy-ch4-mcq-221 (collected ক kept)
- phy-ch4-mcq-237 (collected ঘ kept)
- phy-ch4-mcq-238 (collected ঘ kept)
- phy-ch4-mcq-239 (collected খ kept)
- phy-ch4-mcq-240 (collected ক kept)
- phy-ch4-mcq-241 (collected ক kept)
- phy-ch10-mcq-bank-1 (collected ঘ kept)
- phy-ch10-mcq-bank-2 (collected খ kept)
- phy-ch10-mcq-bank-3 (collected ঘ kept)

Includes ch1 Q171 (collected খ) and Q235 (collected ঘ), whose question blocks are absent from their cited pages (adjacent pages checked) — see open owner decisions, §6.
Includes the single multi-key MCQ row `phy-ch4-mcq-bank-84` (printed multi-correct, kept verbatim; the dry-run allows exactly this one multi-key row).

### 2.4 Null-confirmed — 11 stay null

- phy-board-dhaka-2023-board-mcq-23 (board)
- phy-board-dinajpur-2024-board-mcq-20 (board)
- phy-board-jessore-2023-board-mcq-11 (board)
- phy-board-rajshahi-2024-board-mcq-24 (board)
- phy-board-sylhet-2023-board-mcq-2 (board)
- phy-ch1-mcq-bank-078 (chapter-ch1)
- phy-ch10-mcq-bank-20 (chapter-ch10)
- phy-ch10-mcq-bank-111 (chapter-ch10)
- phy-model-01-model-mcq-13 (model)
- phy-model-01-model-mcq-24 (model)
- phy-model-01-model-mcq-25 (model)

- Board 5, chapter 3 (ch1 Q78; ch10 Q20, Q111), model 3 (model-01 Q13/Q24/Q25).

### 2.5 The 27 NO-DISC rows — semantic rule applied per row (full file: `no-disc-decisions.json`)

Rule: verdict=`correct` with `audit_key`=null means eye-confirmed **NO DISC beside the question** — the label means "collected key unsupported by any margin disc", NOT a replacement. No key was nulled blindly. For each of the 27, the row's own explanation/answer evidence was checked: kept iff the explanation states the collected key as the answer, else nulled. **Result: 25 kept, 2 nulled. This group is flagged for owner awareness.**

- phy-ch10-mcq-bank-104: collected খ → KEPT — Explanation states potential is inversely proportional to capacitance at fixed charge — the collected option's term.
- phy-ch10-mcq-bank-105: collected গ → KEPT — Explanation's computation concludes the collected option's energy value.
- phy-ch10-mcq-bank-106: collected ক → KEPT — Explanation's computation concludes the collected option's energy value.
- phy-ch10-mcq-bank-107: collected খ → KEPT — Explanation's computation concludes the collected option's energy value.
- phy-ch10-mcq-bank-108: collected ক → KEPT — Question asks where static electricity is NOT used; the explanation's use-list omits the collected option, the only option absent from it (support by exclusion).
- phy-ch10-mcq-bank-109: collected গ → NULL — Explanation's concluding causal claim names positive-charge build-up (option ka) as what creates lightning; the collected option (negative charge in clouds) appears only as an intermediate step, not as the stated cause.
- phy-ch10-mcq-bank-110: collected ক → KEPT — Explanation states the air heats to the collected option's temperature range.
- phy-ch10-mcq-bank-18: collected ক → KEPT — Explanation states the glass rod becomes positively charged — the collected option's text.
- phy-ch10-mcq-bank-19: collected গ → KEPT — Explanation states flannel cloth has the least electron affinity — the collected option's text.
- phy-ch10-mcq-bank-21: collected খ → KEPT — Explanation defines the process by the collected option's term.
- phy-ch10-mcq-bank-22: collected ক → KEPT — Explanation describes induction as charging an uncharged object — the collected option's text.
- phy-ch10-mcq-bank-42: collected গ → KEPT — Explanation's computation concludes the force is unchanged — the collected option's text.
- phy-ch10-mcq-bank-43: collected ক → KEPT — Explanation's computation concludes 1 C — the collected option's value.
- phy-ch10-mcq-bank-44: collected ঘ → KEPT — Explanation concludes the force becomes three times — the collected option's text.
- phy-ch10-mcq-bank-45: collected খ → KEPT — Explanation's computation concludes 5 C — the collected option's value.
- phy-ch10-mcq-bank-46: collected খ → KEPT — Explanation's computation concludes the collected option's signed value.
- phy-ch10-mcq-bank-47: collected ঘ → KEPT — Explanation rejects the out-of-range root and keeps the collected option's value.
- phy-ch10-mcq-bank-48: collected গ → KEPT — Explanation's computation concludes the collected option's value.
- phy-ch10-mcq-bank-74: collected ক → KEPT — Explanation names the collected option's figure as the one with equal charges and a neutral point.
- phy-ch10-mcq-bank-75: collected গ → KEPT — Explanation states the potential must change for the field to change — the collected option's text.
- phy-ch10-mcq-bank-76: collected খ → KEPT — Explanation states charge-flow direction is set by electric potential — the collected option's term.
- phy-ch10-mcq-bank-77: collected গ → KEPT — Explanation defines the quantity as scalar — the collected option's term.
- phy-ch10-mcq-bank-78: collected ক → KEPT — Explanation's computation concludes the collected option's unit.
- phy-ch10-mcq-bank-79: collected খ → KEPT — Explanation states positive charge moves from high to low potential — the collected option's text.
- phy-ch10-mcq-bank-80: collected খ → KEPT — Explanation states electrons move from low to high potential; with A=16V, B=12V that yields the collected direction.
- phy-ch10-mcq-bank-81: collected খ → KEPT — Explanation defines the quantity as electric potential — the collected option's term.
- phy-ch2-mcq-bank-36: collected ঘ → NULL — Explanation explicitly concludes there is no correct answer; it does not state the collected key as the answer.

The 2 nulled rows:
- `phy-ch2-mcq-bank-36` — explanation explicitly concludes there is no correct answer. (Its collected flag already documents the tension: a margin-circle key read as ঘ versus an explanation concluding no correct answer.)
- `phy-ch10-mcq-bank-109` — the explanation's concluding causal claim names positive-charge build-up (option ক) as what creates lightning; the collected গ appears only as an intermediate step, not as the stated cause.

### 2.6 Ch1 verbatim replacements — 27 applied (field = the row's section use)

- phy-ch1-short-qa-002 (short-qa → answer)
- phy-ch1-short-qa-007 (short-qa → answer)
- phy-ch1-short-qa-008 (short-qa → answer)
- phy-ch1-short-qa-013 (short-qa → answer)
- phy-ch1-short-qa-014 (short-qa → answer)
- phy-ch1-short-qa-016 (short-qa → answer)
- phy-ch1-short-qa-022 (short-qa → answer)
- phy-ch1-short-qa-039 (short-qa → answer)
- phy-ch1-short-qa-050 (short-qa → answer)
- phy-ch1-short-qa-067 (short-qa → answer)
- phy-ch1-short-qa-077 (short-qa → answer)
- phy-ch1-exercise-qa-g01 (exercise-qa → answer)
- phy-ch1-exercise-qa-g02 (exercise-qa → answer)
- phy-ch1-exercise-qa-g03kha (exercise-qa → answer)
- phy-ch1-exercise-qa-g07 (exercise-qa → answer)
- phy-ch1-mcq-bank-003 (mcq-bank → explanation)
- phy-ch1-mcq-bank-016 (mcq-bank → explanation)
- phy-ch1-mcq-bank-024 (mcq-bank → explanation)
- phy-ch1-mcq-bank-042 (mcq-bank → explanation)
- phy-ch1-mcq-bank-061 (mcq-bank → explanation)
- phy-ch1-mcq-bank-113 (mcq-bank → explanation)
- phy-ch1-mcq-bank-120 (mcq-bank → explanation)
- phy-ch1-creative-002 (creative → answer)
- phy-ch1-creative-016 (creative → answer)
- phy-ch1-creative-022 (creative → answer)
- phy-ch1-creative-036 (creative → answer)
- phy-ch1-creative-044 (creative → answer)

- Short-qa / exercise-qa / creative → `answer` (guide_solution); mcq-bank → `explanation`.
- Confirmed-verbatim rows (326) unchanged. `phy-ch1-short-qa-001` (flagged-unreadable) kept as collected + flag.

### 2.7 Triage — 1 move-to-held applied, 1 correction HELD BACK

- **Applied:** `phy-ch8-formula-bank-20` (formula-math) moved rows → held: question cut at the page bottom edge and no printed answer found; nothing usable as collected and the cut text unverifiable from the scan.
- **HELD BACK (coordinator hold, NOT applied):** `phy-ch4-mcq-bank-36` triage `correct-at-import` (board year '২৭). The '২৭ year is anomalous for an SSC-2026 guide, so the row is kept as collected (source `ঢা. বো.`, no year) + flag, recorded as pending owner confirmation. Question/answer unchanged.
- All other 353 triage rows keep their flags as collected (304 keep-flagged, 35 deferred-to-audit, 14 needs-owner-decision).

### 2.8 Held / out-of-syllabus handling

- Board held ⊗/box rows (199: 125 + 52 + 20 + 2 by reason) stay held, never imported as usable rows. The 200th board held row is the unverifiable washed-out row; it also stays held.
- Part-level OOS rows stay flagged exactly as collected; split-vs-keep is an OWNER decision, not taken here: ch1 creative Q3/Q23/Q34 (ঘ part printed [সিলেবাস বহির্ভূত]), ch7 creative Q30/Q32/Q36/Q39/Q63 (গ part printed '[সিলেবাস বহির্ভূত]' note), ch10 creative Q25 (গ part printed [সিলেবাস বহির্ভূত]). Their `out_of_syllabus` boolean stays false as collected (the note is part-level, not row-level).

## 3. Field mapping (Islam-style, documented — not silent)

| Collected field | Normalized field | Rule |
|---|---|---|
| `question` | `question_text` | verbatim |
| `answer` | `guide_solution` | verbatim, EXCEPT pointer-only rows (below) |
| `answer_pointer` | `answer_pointer` | kept verbatim on pointer-only rows (model-short 203, model-creative 202, board-creative 89): `guide_solution` null + pointer verbatim. On other rows, pointer carried as collected (normally null). |
| `explanation` | `explanation` | kept; ch1 mcq-bank verbatim replacements applied here |
| `answer_key` | `answer_key` | after §2 corrections |
| `options` | `options` | kept (ক/খ/গ/ঘ map) |
| `marks`, `marks_parts` | same | kept; creative `marks_parts` [1,2,3,4] on all 492 creative rows |
| `marks_source` | `marks_source` | kept |
| `lesson`, `textbook_page`, `learning_outcome`, `source`, `source_kind`, `stimulus`, `topic`, `importance`, `out_of_syllabus`, `out_of_syllabus_note`, `flag_note`, `diagram_dependent`, `guide_source`, `key_format` | same | kept |
| `set_id` | `set_id` | kept; dry-run fails if any model/board row's set_id does not resolve to its file's sets list (1,516 model/board rows checked, all resolve) |
| — | `book_id`, `subject`, `class_id` | `class9-physics-bn-guide`, `physics`, 9 (proposed) on every row/chunk/set |
| board rows | `board_name`, `board_year` | derived from the row's set entry (e.g. dhaka / 2023) |
| — | `source_file`, `import_notes` | provenance: which collection file the row came from; which corrections/flags import-prep applied |
| `flag_note` | `flag_note` | kept verbatim EXCEPT conflict-unresolved (103), no-disc (27), and triage-held-back (1) rows, where a standardized `IMPORT:` note is appended (strengthening, not overwriting) |

Chunks (72) and sets (66) are carried through with their ids; sets keep all collected fields plus `book_id`/`source_file`. No part explosion was performed: one normalized row per collected row (unlike Islam's creative part explosion — physics keeps `marks_parts` on the group row per the task's kept-as-collected rule).
No rows were dropped for any other reason: every collected row is either in normalized rows (6,700) or normalized held (369), with zero row/held id overlap and zero duplicate ids (dry-run guards).

## 4. Dry-run result

`python3 import_physics.py` → **exit 0, all 23 guards PASS**: counts, id uniqueness, row/held non-overlap, per-file counts, per-section counts, set resolution (1,516 model/board rows), keyless-MCQ set == documented 13 exactly, single-option keys (+1 documented multi-key), pointer-only solution-null rule, diagram/countable split (823 / 5,877), uniform book/subject/class, chunk/set uniqueness, creative marks_parts.

Two guards initially failed on first run and were corrected in the SCRIPT (not the data), both documented here for honesty:
- Per-file held counts: the counter omitted the zero-held practical file; fixed with zero-fill.
- MCQ key guard: it rejected the genuine printed multi-correct row `phy-ch4-mcq-bank-84` (ক ও ঘ); fixed to allow exactly that documented row.

Final keyless-MCQ list (13): 5 board null-confirmed, ch1 Q78, ch10 Q20/Q111, model-01 Q13/Q24/Q25, and the 2 no-disc nulled rows (ch2 Q36, ch10 Q109). No other MCQ row is keyless.

## 5. Edge allowlist gap (deploy-time, read-only check of `supabase/functions/guide-bank/list.ts` — NOT edited)

The allowlist (`LIST_SECTION_VALUES`, 44 values, exact-match, case-sensitive) does **NOT** contain 6 physics section values. Rows in these sections (875 after import-prep) would fail section-filtered list queries (client error) until the allowlist is extended at deploy time. Section values are kept as collected per the task, so this is a coordinator deploy-time gap, not an import-prep fix:

| Section NOT on allowlist | Rows after | Near-miss warning |
|---|---|---|
| `formula-math` | 646 | no allowlist counterpart |
| `exercise-qa` | 97 | no allowlist counterpart |
| `practice-math` | 57 | distinct from allowlisted `practice_work` |
| `type-bank` | 44 | no allowlist counterpart |
| `applied-math` | 20 | no allowlist counterpart |
| `conceptual-creative` | 11 | distinct from allowlisted `conceptual` — exact-match means these are DIFFERENT sections |

On-allowlist physics sections (5,825 rows): `quiz`, `activity`, `mcq-bank`, `short-qa`, `creative`, `knowledge-qa`, `comprehension-qa`, `model-mcq`, `model-short`, `model-creative`, `board-mcq`, `board-creative`, `viva`.

## 6. Pre-live requirements + owner decisions still open

- **Subjects-table `physics` row MISSING (pre-live requirement):** per the task context, no `physics` row exists in the subjects table yet. This worker performed NO database connection, so this was not re-verified against the live DB — the coordinator must create/confirm the subjects row before any live write. This worker cannot create it.
- **class_id 9 (proposed):** joint class 9 per the Islam precedent; coordinator confirms before live.
- **Open owner decisions (NOT decided by this worker):**
  1. Part-level OOS splits (§2.8): ch1 creative Q3/Q23/Q34, ch7 Q30/Q32/Q36/Q39/Q63, ch10 Q25 — split the OOS part to held, or keep the flagged whole row.
  2. The 27 no-disc group (§2.5) — owner awareness, especially the 2 nulled rows (ch2 Q36, ch10 Q109).
  3. `phy-ch4-mcq-bank-36` board year — triage correction held back; confirm whether the source year is '২৭ or '২২ before restoring it.
  4. Model-01 3 nulls (Q13/Q24/Q25) — stay null, dropped, or resolved another way.
  5. Model-08 grid-vs-computation policy — 16 `GRID CONFLICT` rows: printed grid (currently held, audit-confirmed at 500 dpi) vs independent computation. This audit confirms the grid side only; the policy choice is the owner's.
  6. ch1 Q171 (collected খ) and Q235 (collected ঘ) — question blocks absent from cited pages (adjacent pages checked); rows kept as collected + conflict flag pending owner disposition.
- **Not in scope / not done:** no live write, no Edge deploy, no subjects-table change, no app-tree edit, no zip, no download. The Islam import script's guard pattern was used as a behavioral model only; `import_physics.py` was written fresh for physics (no Islam data or paths copied).

## 7. Self-verification

- Normalized files re-parsed independently of the builder; recounts match the dry-run exactly (rows 6,700 / held 369 / chunks 72 / sets 66 / diagram 823 / countable 5,877 / keyless MCQ 13).
- Spot checks passed: Dhaka 2023 Q8 = গ; ch7 bank ex-001 = খ; ch1 verbatim replacements match their `replacement` texts (short-qa answer, mcq-bank explanation, creative answer); ch1 short-qa-001 unchanged; ch4-36 source unchanged; ch8-20 absent from rows and present in held; pointer-only rows carry solution null + pointer verbatim.
- Collection + verification input files: checksummed before and after; zero modifications (see final report to coordinator).
