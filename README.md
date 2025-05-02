# Blockhouse_Quant_Research
# Task 1: Order Flow Imbalances (OFI) – Quantitative Research Submission

##  Objective
This repository contains a complete implementation of OFI-based feature construction and modeling for short-term return forecasting. It is based on the assignment provided as part of a quantitative research evaluation, referencing the paper:

> *Cross-Impact of Order Flow Imbalance in Equity Markets*

The goal is to evaluate the candidate’s ability to work with limit order book (LOB) data, construct multiple levels of OFI, and apply predictive modeling techniques such as LASSO regression.

---

##  Contents

| File | Description |
|------|-------------|
| `Trial_Task_Implementation.ipynb` | Modular Python script for OFI feature extraction and LASSO modeling |
| `first_25000_rows.csv` | Provided dataset  |
| `Task_Report.pdf` | LaTeX report in pdf covering modeling, results, and conceptual questions |
| `Trial Task.docx` | Description of the given tasks |

---

##  Implemented Features

###  Constructed OFI Features
- **Best-Level OFI**: Captures net demand at top of book (Level 1).
- **Multi-Level OFI**: Measures OFI at Levels 1 through 10 of the LOB.
- **Integrated OFI**: First principal component of multi-level OFI via PCA.
- **Cross-Asset OFI**: *Not implemented due to single-symbol dataset (`AAPL` only). Code prints explanation.*

###  Forecasting Horizons
Models were built to forecast:
- 1-minute log return
- 5-minute log return
- 10-minute log return

---

##  Modeling Approach

- **LASSO regression** with TimeSeriesSplit (5-fold) CV
- **Lagged OFI features** at 1m, 5m, 10m lags
- **Standardized features** using `StandardScaler`
- Output: R² score, best alpha, top predictive features per horizon

### Sample Output

| Horizon        | R² Score | Top Features |
|----------------|----------|--------------|
| log_return_1m  | 0.0000   | *(None selected — noisy horizon)* |
| log_return_5m  | 0.0101   | `ofi_level_2_lag1`, `ofi_level_9_lag1`, ... |
| log_return_10m | 0.0138   | `ofi_level_2_lag5`, `ofi_level_1_lag5`, ... |

---

##  Conceptual Questions Answered
Answers included in `Task_Report.pdf`:
1. Why measure OFI at multiple depth levels?
2. Why use LASSO over OLS for cross-impact modeling?
3. Why is OFI more predictive than trade volume?

