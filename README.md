# Trading Strategies with Machine Learning (DNN on AAPL)

This repository contains a Jupyter notebook for a machine learning trading strategy project using **Apple (AAPL)** historical price data. The notebook downloads data with `yfinance`, builds engineered features, trains a **deep neural network** using scikit-learn's `MLPClassifier`, converts predictions into buy/sell actions, simulates a trading portfolio, and compares the strategy against a **buy-and-hold benchmark**.

## File in this repository

- `Project2_DNN_Trading.ipynb` — main notebook
- `README.md` — setup and run instructions

## What the notebook does

The notebook is organized into these sections:

1. **Data Preparation**
   - Downloads AAPL daily closing prices from **2016-02-01** to **2026-02-01**
   - Cleans the data
   - Plots the 10-year price series
   - Builds features such as:
     - log returns
     - 5 lagged returns
     - short/long moving averages
     - SMA ratio
     - 10-day momentum
   - Splits the data into **80% train / 20% test**

2. **Strategy Design and Implementation**
   - Trains a deep neural network with `MLPClassifier`
   - Predicts price direction on the test set
   - Converts predictions into trading signals:
     - `1` = buy
     - `-1` = sell
     - `0` = hold
   - Plots buy/sell signals on the test-period price chart

3. **Trading Log**
   - Simulates a portfolio starting with **$10,000**
   - Tracks cash, shares held, stock value, and total portfolio value

4. **Performance Evaluation**
   - Computes final portfolio value
   - Computes total return

5. **Benchmark Evaluation**
   - Runs a buy-and-hold strategy on the same test period

6. **Benchmark Comparison**
   - Compares the DNN strategy against buy-and-hold
   - Reports outperformance in percentage points

## Requirements

The notebook was created with **Python 3.12.1**.

Install these packages before running it:

```bash
pip install notebook numpy pandas matplotlib scikit-learn yfinance
```

If you prefer JupyterLab, you can use this instead:

```bash
pip install jupyterlab numpy pandas matplotlib scikit-learn yfinance
```

## How to run

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd <your-repo-folder>
```

### 2. Create and activate a virtual environment

#### macOS / Linux
```bash
python -m venv .venv
source .venv/bin/activate
```

#### Windows (PowerShell)
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
pip install notebook numpy pandas matplotlib scikit-learn yfinance
```

### 4. Launch Jupyter

```bash
jupyter notebook
```

Then open:

```text
Project2_DNN_Trading.ipynb
```

### 5. Run the notebook

In Jupyter, use **Kernel → Restart & Run All** so the notebook executes from top to bottom in the correct order.

## Important notes

- **Internet connection is required** because the notebook downloads market data from Yahoo Finance through `yfinance`.
- Results may vary slightly over time if Yahoo Finance adjusts historical data.
- The notebook is intended to run **from start to finish without manual intervention**.
- The first transaction is constrained to be a **buy**, and the final position is fully liquidated by the end of the test period.
- The portfolio simulation assumes:
  - initial capital = **$10,000**
  - **no short-selling**
  - **whole shares only**
  - buy using all available cash
  - sell the entire position when a sell action occurs
  - no transaction costs or slippage

## Expected outputs

When the notebook runs successfully, it should produce:

- a raw 10-year AAPL price chart
- a test-set trade signal chart with buy/sell markers
- a daily trading log
- DNN strategy performance summary
- buy-and-hold benchmark summary
- a final comparison table and return comparison chart

## Customization

To test another stock or date range, edit the configuration cell near the top of the notebook:

```python
TICKER = 'AAPL'
START  = '2016-02-01'
END    = '2026-02-01'
```

You can also experiment with:

- neural network architecture (`hidden_layer_sizes`)
- moving-average windows
- additional technical indicators
- different feature sets
- alternative train/test periods

## Troubleshooting

### `ModuleNotFoundError`
Install the missing package with `pip install <package_name>`.

### Jupyter command not found
Try:

```bash
python -m notebook
```

or

```bash
python -m jupyter lab
```

### Yahoo Finance download fails
This is usually caused by:
- no internet connection
- temporary Yahoo Finance/API issues
- firewall or network restrictions

Try rerunning the notebook after a short delay.

## Repository suggestion

A simple repository structure would look like this:

```text
your-repo/
├── Project2_DNN_Trading.ipynb
└── README.md
```

## Acknowledgment

This notebook was prepared as a machine learning trading strategy project for academic use. Please review and understand the code before reusing or modifying it.
