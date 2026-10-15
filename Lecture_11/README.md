# FINANCE 384 — Lecture 11: Financial Text, Sentiment and Market Risk

This student pack uses a **constructed financial-news teaching case** together with historical SPY prices and Cboe VIX levels. The main analysis covers January–November 2025; earlier observations provide the warm-up period needed for the market calculations.

The titles are synthetic. They are not Financial Times articles, newspaper records or evidence about real news coverage. Their mixture was designed to vary with market-stress conditions so that students can learn the workflow. Relationships between the text indicators, SPY volatility and VIX are therefore expected by construction and must not be interpreted as forecasting or causal evidence.

## Student files

Keep the notebook, this README, `requirements.txt` and the `data` folder together:

```text
FINANCE384_Lecture11_Student.ipynb
FINANCE384_Lecture11_Student.html
README.md
requirements.txt
data/
    synthetic_financial_titles_2025_with_warmup.csv
    finbert_scores_synthetic_titles.csv
    lm_dictionary.csv
    spy_daily.csv
    VIX_History.csv
```

| File | Purpose |
|---|---|
| `FINANCE384_Lecture11_Student.ipynb` | Runnable student notebook with code, outputs and discussion questions |
| `FINANCE384_Lecture11_Student.html` | Read-only rendered copy for convenient viewing |
| `data/synthetic_financial_titles_2025_with_warmup.csv` | 4,346 constructed titles, their issue dates, stable IDs and warm-up flags |
| `data/finbert_scores_synthetic_titles.csv` | Frozen FinBERT positive, negative and neutral probabilities for the constructed titles and six short teaching examples |
| `data/lm_dictionary.csv` | Loughran–McDonald word list and positive, negative and uncertainty indicators |
| `data/spy_daily.csv` | Historical SPY closing and adjusted closing prices used in the notebook |
| `data/VIX_History.csv` | Historical Cboe VIX data; the notebook retains the date and closing level |

Only these five CSV files are required. Preparation notebooks, model files and internet access are not needed for the student lesson.

## Set up and run the notebook on Windows

Use Python 3.11 or 3.12. Open PowerShell in the folder containing the notebook, then run:

```powershell
py -3.12 -m venv .venv
.venv\Scripts\python.exe -m pip install --upgrade pip
.venv\Scripts\python.exe -m pip install -r requirements.txt
.venv\Scripts\python.exe -m jupyter lab
```

Open `FINANCE384_Lecture11_Student.ipynb`, select the `.venv` kernel, and choose **Kernel → Restart Kernel and Run All Cells**. Run the notebook from its own folder so that `Path("data")` points to the supplied `data` directory.

After the packages have been installed, the student notebook does not need an API key, GPU, PyTorch, Transformers or a model download. It reads previously calculated FinBERT probabilities from the supplied CSV.

## What the notebook does

1. Loads the constructed titles and the three frozen reference datasets.
2. Selects finance-related titles and assigns each issue date to the next observed SPY trading session.
3. Measures title-level sentiment and uncertainty using the Loughran–McDonald dictionary.
4. Attaches frozen FinBERT class probabilities and calculates `positive - negative` sentiment.
5. Aggregates the title measures into daily news indicators.
6. Calculates rolling and EWMA realised volatility from SPY returns and compares them descriptively with VIX and the text indicators.
7. Uses April 2025 as a teaching case and compares averages before, during and after the stress window.

FinBERT neutral sentiment and Loughran–McDonald uncertainty are different concepts. FinBERT probabilities describe the model's sentiment labels; they are not probabilities that SPY will rise or fall. Correlation describes co-movement and does not establish prediction or causation.

## Data and model notes

- **Constructed titles:** generated locally for this teaching exercise. They contain no Financial Times or ProQuest title data. The generator used market-stress conditions to vary the mixture of headline templates, so the resulting associations are simulated rather than empirical findings.
- **Loughran–McDonald dictionary:** frozen extract from the [official Notre Dame master dictionary](https://sraf.nd.edu/loughranmcdonald-master-dictionary/). Reference: Loughran, T. and McDonald, B. (2011), “When Is a Liability Not a Liability? Textual Analysis, Dictionaries, and 10-Ks,” *Journal of Finance*, 66(1), 35–65.
- **FinBERT:** frozen probabilities generated with [`ProsusAI/finbert`](https://huggingface.co/ProsusAI/finbert), revision `4556d13015211d73dccd3fdd39d39232506f3e43`. Reference: Araci (2019), [*FinBERT: Financial Sentiment Analysis with Pre-trained Language Models*](https://arxiv.org/abs/1908.10063).
- **SPY:** historical adjusted prices obtained from [Yahoo Finance](https://finance.yahoo.com/quote/SPY/history/). Adjusted prices may be revised by the provider.
- **VIX:** historical levels from [Cboe](https://www.cboe.com/tradable_products/vix/vix_historical_data/). VIX is an annualised option-implied volatility measure, not the probability or expected size of a market loss.
- **April 2025 context:** [2 April order](https://www.whitehouse.gov/presidential-actions/2025/04/regulating-imports-with-a-reciprocal-tariff-to-rectify-trade-practices-that-contribute-to-large-and-persistent-annual-united-states-goods-trade-deficits/), [9 April order](https://www.whitehouse.gov/presidential-actions/2025/04/modifying-reciprocal-tariff-rates-to-reflect-trading-partner-retaliation-and-alignment/), and the [Federal Reserve November 2025 Financial Stability Report](https://www.federalreserve.gov/publications/november-2025-financial-stability-report-asset-valuations.htm).

The supplied files are for this course exercise. Do not treat the constructed titles as observed news or use the simulated correlations as research findings.

## Create a fresh HTML copy

After running and saving the notebook, close JupyterLab or open a new PowerShell window in the same folder and run:

```powershell
.venv\Scripts\python.exe -m jupyter nbconvert --to html "FINANCE384_Lecture11_Student.ipynb"
```

This writes `FINANCE384_Lecture11_Student.html` beside the notebook.

