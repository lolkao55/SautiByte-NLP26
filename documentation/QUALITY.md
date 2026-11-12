# Quality report

* **Team / language / dataset version:** Team 4 (SautiByte) / Kiswahili (`sw-KE`, Kenyan variety with some natural Sheng and Kiswahili–English code-switching) / v1.
* **Accepted contributions by source method and intent:** 250 `original_human` records, written by the team (`source_dataset = team_authored`). 25 per label: `weather_query`, `datetime_query`, `alarm_set`, `calendar_set`, `calendar_query`, `lists_createoradd`, `lists_query`, `play_music`, `news_query`, `qa_definition`.
* **Contributors:** T04-L: 84 records · T04-B: 83 records · T04-Z: 83 records.
* **Unchanged external training rows (not counted as contributions):** 0.

## Review

* **Independent review counts:** All 50 test records were independently reviewed by a team member who did not write them (`reviewer_code ≠ contributor_code`). Train and dev records were also reviewed by the same cross-check.
* **Review assignments:**
  * T04-L's records reviewed by T04-B (11 Nov 2026).
  * T04-B's records reviewed by T04-Z (12 Nov 2026).
  * T04-Z's records reviewed by T04-L (11 Nov 2026).
* **Corrections made during review (T04-B's records, reviewed by T04-Z):**

| Record | Original | Corrected | Reason |
|---|---|---|---|
| T04-B-021 | Nimepangia mambo magani Ijumaa? | Nimepanga mambo gani Ijumaa? | Spelling and verb form |
| T04-B-028 | …kilichyopangwa… | …kilichopangwa… | Spelling |
| T04-B-042 | Ongeza mkate kwenye orodha yangu ya manunuzi. | Ongeza PS4 kwenye orodha yangu ya zawadi za Krismasi. | Original copied the handbook example verbatim; replaced with a new team-written sentence |
| T04-B-045 | Tia sukari kwenye bidhaa za nyumbani. | Tia sukari kwenye orodha ya bidhaa za nyumbani. | Added "orodha" so the list intent is clear |
| T04-B-054 | Ongeza kuosha gari kwenye majukumu ya leo. | …kwenye orodha ya majukumu ya leo. | Added "orodha" so it is not read as a calendar entry |
| T04-B-060 | Niwekee mayai kwenye orodha ya mapishi kesho. | …kwenye orodha ya mapishi ya kesho. | "kesho" now describes the list, not a reminder time |
| T04-B-064 | Tengeneza maswali nitakayomuuliza daktari. | Tengeneza orodha ya maswali nitakayomuuliza daktari. | No list was mentioned |
| T04-B-079 | Nisomee mambo yote niliyopanga kufanya kabla ya jioni. | Nisomee orodha ya mambo niliyopanga kufanya kabla ya jioni. | Ambiguous with `calendar_query` |
| T04-B-082 | Nionyeshe listi kamili ya wageni watakaokuja. | Je, shati jeupe liko kwenye orodha yangu ya mavazi ninayofaa kununua? | Near-duplicate of T04-B-070; replaced with a new team-written sentence |

* **Reviewed and kept (no change):** T04-B-013 (dinner with guests is a scheduled event → `calendar_set`), T04-B-057 ("dawa za mswaki" is genuine informal usage), T04-B-063 ("kwenye majina ya wageni mashuhuri" clearly implies a list).
* **Other fixes:** Removed one extra `calendar_set` record (T04-L-081, so the label has exactly 25); corrected missing splits on two `qa_definition` records; moved one `news_query` record from train to test to reach 15/5/5; fixed trailing spaces and punctuation; made `source_record_id` match `record_id` for all T04-Z records; corrected one wrong `group_id` (T04-Z-059 changed from G-NEWS-26 to G-QDEF-25).

## Disagreements and resolutions

**Disagreement 1: scope of `datetime_query`**

* **Records affected:** T04-L-028, T04-L-032 to T04-L-038, T04-L-041 to T04-L-050 (18 records, including all 5 `datetime_query` test records).
* **Issue:** These records ask about the time or date of an event or a person (e.g. "Sherehe itakuwa saa ngapi?", "Ndege la baba litatua saa ngapi?") rather than the current time, date or day.
* **View A (T04-L, author):** The classifier's job is to identify the intent of the message, not to know the answer. A "what time" question expresses a time/date intent; answering it is left to downstream components.
* **View B (T04-Z, reviewer):** The handbook defines `datetime_query` as asking for the *current* time, date or day, and says to decide from the requested action, not one shared word. Routed to a clock handler, these would return the current time, which does not answer the request. In MASSIVE such requests belong to other intents (e.g. calendar or transport queries) outside our 10 labels.
* **Decision:** Kept as labelled, by team agreement on 12 Nov 2026. Recorded here as a known limitation.
* **Expected effect:** The model may associate "saa ngapi" with `datetime_query`, so calendar questions containing "saa ngapi" (e.g. T04-B-020, `calendar_query`) may be misclassified. Checked in the error analysis below.

**Disagreement 2: `alarm_set` records that do not request setting an alarm**

* **Records affected:** T04-L-058, T04-L-066, T04-L-068, T04-L-069 (dev/train) and T04-L-072, T04-L-073 (test).
* **Issue:** Some are statements ("Nitalala mpaka saa kumi jioni"), some ask *not* to ring or wake ("King'ora cha saa hakipaswi kulia kesho", "usiniamshe kesho asubuhi"), and one is a reminder, which the handbook assigns to `calendar_set`.
* **View A (T04-L):** Each contains an explicit alarm time and alarm context, so the intent is alarm-related.
* **View B (T04-Z):** The handbook defines `alarm_set` as setting an alarm that will ring at a requested time; statements and cancellations do not request this.
* **Decision:** Kept as labelled, by team agreement on 12 Nov 2026. Recorded here as a known limitation.
* **Expected effect:** Statements and cancellations that mention a time may teach the model that any alarm-related wording means `alarm_set`. Checked in the error analysis below.

## Duplicates, exclusions and missing fields

* No duplicate texts or record IDs (checked with a script on the final CSV).
* No empty required fields.
* Excluded during writing (not in the dataset): multi-intent requests, requests outside the 10 labels (e.g. volume control, contacts lookup, radio stations, song identification) and unclear requests.

## Groups and splits

* Each record has its own `group_id` (e.g. `G-CSET-01`, `G-PMUS-12`), because no records are paraphrases of each other.
* Every label has exactly 15 train / 5 dev / 5 test (150 / 50 / 50 total).
* `validate.py`: [paste result after running it].

## Results

* **Majority baseline (test):** accuracy [ ], macro-F1 [ ].
* **Dev (character TF-IDF + logistic regression):** accuracy [ ], macro-F1 [ ].
* **Final frozen test:** accuracy [ ], macro-F1 [ ]. Test size: 50 (5 per label).

## Error analysis (up to five actual mistakes from `test_predictions.csv`)

1. [record_id] "[text]": true `[label]`, predicted `[label]`. Why: [ ]
2. …

## Language variety, limits and unresolved issues

* Kenyan Kiswahili with natural Sheng (e.g. "ngoma", "chai za mastaa", "nirushie moja") and code-switching (e.g. "news", "playlist", "ku-test speaker"). This reflects real use but may not represent standard (sanifu) or Tanzanian Kiswahili.
* Small dataset written by three authors, so vocabulary and style may be narrow; 5 test records per label make per-label scores very uncertain.
* The `datetime_query` and `alarm_set` disagreements above were kept by team decision and remain a known limitation.
