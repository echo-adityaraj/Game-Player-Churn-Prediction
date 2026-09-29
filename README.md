Game Player Churn Prediction
----------------------------------------------------

Predicting seven-day player inactivity using XGBoost, with SHAP explanations to support retention analysis.
------------------------------------------------------------------------------------------------------------------

Overview
----------------------------

The project uses each player's first 30 days of activity to predict no gameplay during the following 7 days. Players must have played during the final observation week and have complete follow-up coverage.

The workflow includes data checks, 20 behavioural features, baseline comparisons, validation-based model settings and thresholds, and SHAP explanations. The final cohort contains 2,124 players, including 425 held-out test players.

Results
-------------------------------------------------------------------

Model	| ROC-AUC	| Average precision	| F1
Logistic regression	| 0.9484	| 0.8478	| 0.7455
XGBoost	| 0.9549	| 0.8196	| 0.7611

Selecting the highest-risk 20% of test players captured 58 of 65 inactive players (89.2%), achieving 4.46× lift over random targeting.

SHAP identified time since last play and recent activity frequency as the leading prediction factors. Logistic regression had higher average precision; XGBoost had higher test ROC-AUC and F1.


Dataset
--------------------------------------------------

Game Difficulty for DAF (Difficulty-Aware Framework): Anonymised mobile puzzle-game activity from 4,089 players, released by Li et al. (KDD 2021).

Download the original dataset : The authors specify research use only. Download the CSVs from the original source; do not include raw data in this repository. This project uses the dataset, not the original DAF method.

How to run
-------------------------------------------------

1. Place interactions.csv and payment.csv in a data folder alongside the notebook.
2. Set DATA_DIR = Path("data") in the notebook.
3. Install dependencies and launch JupyterLab:
   python -m pip install -r requirements.txt
   python -m jupyterlab
4. Open game_player_churn_prediction.ipynb and run all cells in order. The export cell saves the model and result tables in outputs.


Limitations
----------------------------------------------

Results use one random player holdout, not a future-period test. Scores are uncalibrated, and seven-day inactivity does not imply permanent churn. SHAP explains model predictions rather than causes. No reduction in churn or increase in revenue was measured.

The audit found 124 exact duplicate purchase rows; these were retained because separate transactions could not be distinguished from duplicate logging.

Reference
------------------------------

Li et al. (2021). A Difficulty-Aware Framework for Churn Prediction and Intervention in Games. KDD '21.
