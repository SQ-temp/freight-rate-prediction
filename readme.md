# Freight Rate Prediction

Predict `posted_rate` for freight loads. Column descriptions are in `docs/DataDictionary.md`.

## Project structure
```
data/                     raw csv files
data/processed/           cleaned files (created by preprocessing.ipynb)
notebooks/eda.ipynb       data exploration and findings
notebooks/preprocessing.ipynb   cleaning + features
notebooks/model.ipynb     split, baseline, model, final predictions
src/score.py              provided scorer
final_deliverables/       validation_predictions.csv, december_predictions.csv, candidate_december.png, report.pdf
```

## Setup
```bash
python -m venv ML
ML\Scripts\activate        # Windows
source ML/bin/activate      # Mac / Linux
pip install -r requirements.txt
pip install ipykernel
```

## How to run
1. Run `notebooks/preprocessing.ipynb`
2. Run `notebooks/model.ipynb` (creates `validation_predictions.csv` and `december_predictions.csv` in `final_deliverables/`)
3. Run the scorer:
```bash
python src/score.py --predictions final_deliverables/validation_predictions.csv --december-predictions final_deliverables/december_predictions.csv --output-dir final_deliverables
```

## Main decisions
- Removed 677 loads with wrong prices (rate per mile outside 1.4 - 4 $/mile)
- Fixed negative weights with abs (same distribution as positive weights)
- Dropped `quote_signal` (leaks the target in some months) and `market_index` (made the test error worse, missing in December file)
- Used lat/lon instead of city names (validation has new cities)
- Time split: train Jan-Aug, test Sep-Oct
- Model: HistGradientBoostingRegressor on rate per mile

## Results (test Sep-Oct)
| Model | MAE | MAPE |
|---|---|---|
| Baseline (median $/mile per equipment) | $175 | 8.1% |
| Model | $51 | 2.2% |