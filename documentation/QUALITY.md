# Quality report
* **Team / language / dataset version:** Team 4 (SautiByte) / Kiswahili (sw-KE) / v1.0.
* **Accepted contributions by source method and intent:** 250 `original_human` records. 25 each for: `weather_query`, `datetime_query`, `alarm_set`, `calendar_set`, `calendar_query`, `lists_createoradd`, `lists_query`, `play_music`, `news_query`, `qa_definition`.
* **Unchanged external training rows (not counted as contributions):** 0.
* **Independent review counts (including every test item):** 50 test items independently reviewed. (100% of the test set).
* **Disagreements and resolutions:** Minor disagreements on whether "Soma ratiba yangu" was `calendar_query` or `lists_query`. Resolved by tying the word "ratiba" (schedule) strictly to `calendar_query` and "orodha/listi" strictly to `lists_query`.
* **Duplicates / exclusions / missing fields:** Removed all trailing commas during preprocessing to prevent CSV parsing errors. Multi-intent queries were excluded.
* **Group creation and split checks:** `validate.py` passed. `group_id` was applied to thematic paraphrases to ensure they stayed within the same split (e.g., `T04-calset-B01`).
* **Baseline and final model; dev and frozen-test metrics:** *(Note: You will need to paste your exact accuracy and macro-F1 scores here after you run `python evaluate.py`)*.
* **Analyse up to five actual errors and explain them. Report all if there are fewer. If there are none, state that and discuss the limits of the test set:**
  1. *(Placeholder: Explain a misclassification between `calendar_set` and `alarm_set` due to vocabulary overlap like "ukumbusho")*.
  2. *(Placeholder: Insert second model error from `test_predictions.csv`)*.
* **Language variety, limits and unresolved issues:** Kenyan code-switching (using English nouns like "clients" or "meeting" with Swahili verbs) reflects natural use but may cause out-of-vocabulary (OOV) issues if tested against formal standard Swahili (Sanifu).[cite: 57, 62]