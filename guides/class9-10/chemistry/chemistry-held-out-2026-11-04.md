# Chemistry held-out buckets — 2026-11-04 (excluded from the import-ready file)

Source collection files untouched. These rows stay in the sources and wait for owner decisions (or, for bucket D, are dropped under the permanent drop rule).

## Bucket A: Word-variant rows (11) — owner decides which transcription stands

- che-ch11-creative-11: adjudication E pair of model-04-creative-4 (PH3/PH4+)
- che-ch3-creative-33: adjudication E pair of ch3-model-creative-006 (lobon/somanu)
- che-ch3-model-creative-006: adjudication E: part-ka 'lobon' vs print 'somanu' (pair with ch3-creative-33)
- che-ch4-knowledge-qa-3: adjudication E: collected form drops a word vs print full form
- che-ch5-short-qa-33: adjudication E pair of model-02-short-7 (NH3/NH4+)
- che-ch7-creative-86: adjudication E: part-ka 'kon' vs bank 'mom' (pair with ch7-knowledge-qa-3)
- che-ch7-knowledge-qa-3: adjudication E pair of ch7-creative-86 (kon/mom)
- che-model-02-model-short-7: adjudication E: NH3 vs bank NH4+ (pair with ch5-short-qa-33)
- che-model-04-model-creative-4: adjudication E: part-kha PH3 vs bank PH4+ ion form (pair with ch11-creative-11)
- che-model-10-model-creative-1: in-row flag: word as printed, probable variant of another word, not silently corrected
- che-model-10-model-short-2: in-row flag: word sense uncertain, possibly a print variant

## Bucket B: Board held-near pointer rows (4) — near-target UNVERIFIED, no remap

- che-board-barishal-2023-board-creative-6: held-near: near-target ch3-creative-11 unverified (+1 pattern)
- che-board-chattogram-2023-board-creative-2: held-near: near-target ch3-creative-10 unverified (+1 pattern)
- che-board-cumilla-2023-board-creative-2: held-near: near-target ch5-creative-17 unverified
- che-board-mymensingh-2024-board-creative-1: held-near: near-target ch3-creative-6 unverified (+1 pattern)

## Bucket D: Keyless / defective MCQs (7) — permanent drop rule (no answer / defect)

- che-board-barishal-2023-board-mcq-3: 9.18 verdict null-confirmed (stray ink dot only); also decided Barishal 2023 Q3 DROP
- che-ch6-mcq-bank-338: printed defect/conflict: no option equals the printed correct value; key null
- che-ch6-mcq-bank-359: printed defect: no explanation printed; key null
- che-ch6-mcq-bank-364: printed defect/conflict: no option carries the computed value; key null
- che-ch6-mcq-bank-382: printed defect: no explanation printed; key null
- che-ch7-mcq-bank-157: key unresolvable at 300 dpi: duplicated options + margin letter cut
- che-ch7-mcq-bank-159: key unresolvable at 300 dpi: duplicated options + margin letter cut

## Bucket E: Ch7 activity section (2) — section keep/drop unconfirmed by owner

- che-ch7-activity-1: flag: parent to confirm whether to keep the activity section at all
- che-ch7-activity-2: same unconfirmed activity section as activity-1

## Bucket C: board out-of-syllabus 148 — ZERO rows excluded

The 148 are held entries in che-board.json (113 MCQ + 35 creative), disjoint from rows. Their import form (flag vs drop) is still an open owner decision, but there is nothing to subtract from the 5,808 rows now.

## Decided drops already satisfied by construction (no subtraction)

- Scan-gap 32 + unreadable 95: held entries, not rows.
- Special 35: verified absent from rows.
- Barishal 2023 creative-3: held entry, not a row.
