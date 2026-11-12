# Team 4 | SautiByte
**Working Language:** Kiswahili
**Track:** Track A (Intent Classification)

### Team Roles:
* **Omwoyo Leo Kinara:** [Lead Data Contributor & Demo Lead]
* **Daniel Brian Kikuvi:** [ Lead Documentation]
* **Zakariya Mohamed:** [Code Runner & Lead Reviewer ]

###  Our Idea
Our goal was to build a highly accurate Kiswahili intent classification model capable of mapping natural user commands to 10 distinct action labels (e.g., weather queries, setting alarms, managing lists, and playing music). We focused on real-world Kenyan Kiswahili, incorporating natural Sheng and code-mixing (e.g., "playlist", "news") to ensure the model reflects how people actually speak rather than relying on rigid, unnatural translations.

### Our Approach
1. **Data Creation:** We manually authored a 100% original human dataset of 250 Kiswahili sentences (25 per label). 
2. **Strict Review:** Every single test record underwent independent peer review to ensure natural language quality and label accuracy.
3. **Splits:** We strictly adhered to the datathon ratio, splitting every 25-record group into 15 Train, 5 Dev, and 5 Test.
4. **Modeling:** We trained the baseline character TF-IDF and logistic regression model on our curated dataset using the provided starter kit, and served it via a Streamlit UI.

### Results
Our model achieved strong baseline performance on the frozen test set:
* **Test Accuracy:** 0.860 (86.0%)
* **Test Macro-F1:** 0.858
* *Note: As detailed in our Quality Report, errors primarily stemmed from unseen vocabulary (e.g., "hali ya hewa") and overlapping trigger words (e.g., "Weka" used for both alarms and music).*

###  Team Contributions
We divided the sprint equally to ensure a truly collaborative effort:
* **Omwoyo Leo Kinara (T04-L):** Authored 84 Kiswahili records (weather, datetime, alarms, calendar), conducted independent peer reviews, and co-authored the dataset documentation.
* **Daniel Brian Kikuvi (T04-B):** Authored 83 Kiswahili records (calendar, lists), conducted independent peer reviews, and co-authored the quality report and annotation guidelines.
* **Zakariya Mohamed (T04-Z):** Authored 83 Kiswahili records (music, news, definitions), conducted independent peer reviews, executed the model training pipeline, and recorded the Streamlit UI demonstration

## Watch Our Streamlit Demo App Here [https://drive.google.com/file/d/1VNOoZLsmsSufe2ilpT0O2Ab4tLuNjwco/view?usp=sharing]

## Original team Repository [https://github.com/lolkao55/SautiByte-NLP26]
## Final Commit SHA []