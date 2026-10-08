# Lecture 10 — Credit Risk: LGD, EAD and Expected Loss

This lecture builds on Lecture 9's probability-of-default (PD) model. Using funded 36-month LendingClub loans, we estimate loss given default (LGD) and an exposure-at-default (EAD) proxy, then combine these with PD forecasts to estimate expected credit loss (EL).

## What you will learn

The notebook covers:

- constructing observed LGD and EAD proxies from loan repayments and recoveries;
- selecting origination-time predictors and avoiding test-data leakage;
- estimating conditional LGD and EAD using fractional-logit models trained on historical defaults;
- evaluating LGD and EAD forecasts against simple development-sample benchmarks;
- checking LGD and EAD calibration across forecast groups;
- predicting conditional LGD and EAD for every loan in the 2012 test cohort;
- combining PD, LGD and EAD to estimate loan-level and portfolio expected loss;
- comparing predicted EL with realised loss proxies across forecast groups and PD bands; and
- interpreting model limitations and exploring an optional stress-testing exercise.

## Materials

Keep the following files in this folder structure:

```text
Lecture_10/
├── FINANCE384_Lecture_10_Notebook_B.ipynb
├── README.md
├── requirements.txt
├── data/
│   └── credit_risk_course_data.csv
└── outputs/
    └── pd_test_predictions.csv
```

- `FINANCE384_Lecture_10_Notebook_B_student.ipynb` — Lecture 10 student notebook.
- `data/credit_risk_course_data.csv` — frozen course loan dataset, also used in Lecture 9.
- `outputs/pd_test_predictions.csv` — held-out 2012 PD forecasts from Lecture 9 (Notebook A), required by this notebook.
- `requirements.txt` — Python packages needed to run the notebook.

## Running the notebook

1. Download the Lecture 10 folder and keep its subfolders and filenames unchanged.
2. Open the `Lecture_10` folder in VS Code or Jupyter, so the notebook runs with `Lecture_10` as its working directory.
3. Select a Python environment with the required packages installed. If needed, run this command from the `Lecture_10` folder:

   ```bash
   python -m pip install -r requirements.txt
   ```

4. Open `FINANCE384_Lecture_10_Notebook_B_student.ipynb` and run its cells in order.
5. The notebook writes `outputs/expected_loss_test_results.csv` with loan-level 2012 predictions and outcomes.

**Important:** The notebook reads `data/credit_risk_course_data.csv` and `outputs/pd_test_predictions.csv` using relative paths. If a file-not-found error occurs, check that you opened the correct working folder and that both files are present. The supplied PD predictions allow you to run Lecture 10 without rerunning Lecture 9.

## Scope and limitations

This is a teaching exercise using resolved, funded loans and a held-out 2012 origination cohort. LGD and EAD are conditional-on-default models fitted using 2007–2011 development defaults; their predictions are then applied to all 2012 loans to calculate EL. The EAD and realised-loss measures are constructed proxies rather than directly observed balances at the date of default or fully discounted economic losses. The separate conditional LGD and EAD predictions are combined using a simplifying product approximation.

The notebook is **not** a production credit-risk model, an IFRS 9 implementation, or a regulatory capital model. The stress-testing section is an optional exercise, not an estimated macroeconomic scenario model.
