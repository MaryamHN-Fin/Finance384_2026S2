# Lecture 9 — Credit Risk: Probability of Default

This lecture introduces probability of default (PD) using funded 36-month LendingClub loans.

The notebook covers:

- defining the borrower population, information date and default horizon;
- dividing loans chronologically into training, validation and test samples;
- preparing numerical and categorical predictors without test-data leakage;
- estimating an L2-regularised logistic-regression PD model;
- selecting the regularisation strength using validation data;
- evaluating discrimination with ROC AUC;
- evaluating probability accuracy with Brier score, log loss and calibration;
- interpreting coefficients and odds multipliers; and
- translating predicted PD into an illustrative lending decision.

## Materials

- `A_credit_risk_PD_and_lending_decisions.ipynb` — the Lecture 9 notebook.
- `data/credit_risk_course_data.csv` — the frozen course dataset.
- `requirements.txt` — the Python packages required to run the notebook.

Keep the notebook, `requirements.txt` and the `data` folder together. If the required packages are not already installed, run this command once from the `Lecture_9` folder:

```bash
python -m pip install -r requirements.txt
```

Open the notebook and choose **Restart Kernel and Run All Cells**.

## Scope

This is a teaching model based on resolved, funded loans. It estimates retrospective lifetime default over a 36-month contract and should not be interpreted as a regulatory, production or real-time lending model.
