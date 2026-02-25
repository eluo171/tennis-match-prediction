# 🎾 Predicting ATP Tennis Match Winners

A machine learning project that predicts the outcomes of professional ATP tennis matches using player performance metrics and historical data. Two models — **Logistic Regression** and **Random Forest** — are compared using a walk-forward (time-series) validation strategy.

---

## 📊 Results

| Model | Average Accuracy (1990–2024) |
|---|---|
| Logistic Regression | ~70.5% |
| Random Forest | ~69.6% |

Logistic Regression slightly outperforms Random Forest, suggesting the underlying relationships between features and match outcomes are largely linear.

---

## 🔍 Features

| Feature | Description |
|---|---|
| `age_diff` | Age difference between P1 and P2 |
| `rank_diff_pct` | ATP ranking difference (as % of P2's rank) |
| `rank_points_diff_pct` | Ranking points difference (as %) |
| `serve_diff` | Serve rating difference |
| `return_diff` | Return rating difference |
| `pressure_diff` | Pressure/clutch performance difference |
| `p1_win_streak` | P1's current win streak entering the match |
| `p2_win_streak` | P2's current win streak entering the match |
| `h2h` | Head-to-head win differential (P1 − P2) |

---

## 🧠 Key Findings

- **Serve and return ratings** are the strongest predictors of match outcomes
- **ATP ranking** is a powerful baseline predictor
- **Win streaks and age** were not statistically significant (p > 0.05) in logistic regression
- Prediction accuracy fluctuates year-to-year (~65–75%), consistent with tennis prediction literature
- Walk-forward validation is used to prevent data leakage — each year's model is trained only on prior years

---

## 📁 Project Structure

```
tennis-match-prediction/
│
├── predicting_tennis_match_winner.ipynb   # Main notebook
├── atp_matches.csv                         # Dataset (not tracked by git)
├── requirements.txt                        # Python dependencies
├── .gitignore
└── README.md
```

---

## ⚙️ Setup & Usage

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/tennis-match-prediction.git
cd tennis-match-prediction
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Add the dataset
Place your `atp_matches.csv` file in the root directory.

### 4. Run the notebook
```bash
jupyter notebook predicting_tennis_match_winner.ipynb
```

---

## 📦 Dataset

The dataset (`atp_matches.csv`) contains ATP match records with player stats including serve ratings, return ratings, pressure ratings, ATP rankings, and match results. Due to file size, it is not included in this repository.

> The data can be sourced from [Jeff Sackmann's Tennis Abstract dataset](https://github.com/JeffSackmann/tennis_atp) with additional player ratings derived separately.

---

## 🛠 Methods

### Walk-Forward Validation
To simulate real-world prediction, models are trained on all matches **before** year *t* and tested on year *t*. This prevents data leakage and reflects how a model would actually perform when deployed.

### Models
- **Logistic Regression** — scikit-learn, standardized features, 1000 max iterations
- **Random Forest** — 150 estimators, max depth 20, min samples split 5

### Feature Engineering
- Performance differences computed as P1 − P2
- Rankings expressed as percentage differences
- Win streaks computed chronologically to prevent lookahead bias
- H2H records computed chronologically to prevent lookahead bias

---

## 📈 Visualizations

The notebook generates:
- Logistic Regression accuracy over time (1990–2024)
- Random Forest accuracy over time (1990–2024)
- Side-by-side model comparison
- Average feature importance bar chart
- Logistic regression coefficients with p-values

---

## 🔮 Future Improvements

- Include **surface type** (clay, grass, hard court) — a major missing predictor
- Add **tournament level** (Grand Slam vs. ATP 250)
- Use a **rolling window** of recent form rather than just win streaks
- Incorporate **fatigue metrics** (days since last match, rounds played)
- Try **gradient boosting** (XGBoost, LightGBM)
- Add **Elo-based ratings** as features

---

## 🧰 Tech Stack

- Python 3.x
- pandas, numpy
- scikit-learn
- statsmodels
- matplotlib, seaborn
- Jupyter Notebook
