# Chicago Crime Forecasting using LightGBM

This repository contains a Jupyter Notebook (`Chicago_Project.ipynb`) that explores and models Chicago crime data using LightGBM. The goal is to forecast crime counts (or related targets) using historical crime records and engineered features.

## Dataset

The dataset used is the City of Chicago "Crimes - 2001 to present" dataset from the Chicago Data Portal:

- Dataset page: https://data.cityofchicago.org/d/ijzp-q8t2
- Portal: https://data.cityofchicago.org/

Notes:
- If you downloaded the dataset manually, place the CSV (or Parquet) in an accessible `data/` folder next to the notebook and update paths in the notebook accordingly.
- The dataset contains fields such as: `ID`, `Case Number`, `Date`, `Block`, `Primary Type`, `Description`, `Location Description`, `Arrest`, `Domestic`, `Beat`, `District`, `Ward`, `Community Area`, `Latitude`, `Longitude`, etc.

## What this project does

- Loads and performs exploratory data analysis on Chicago crime records.
- Cleans and preprocesses the data (date parsing, missing values, location handling).
- Engineers features (time features from `Date`, aggregated counts, rolling windows, spatial bucketing, etc.).
- Trains a LightGBM model to forecast crime counts (or another target) and evaluates it using appropriate metrics (MAE, RMSE, R2 for regression; AUC/F1 for classification, depending on how you cast the problem).
- Visualizes results and model diagnostics.

## Quick start

1. Clone or open this repository in VS Code (you already have the notebook in the workspace).
2. Create a Python virtual environment and install dependencies.

Mac / zsh example:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

3. Start Jupyter and open the notebook:

```bash
jupyter lab
# or
jupyter notebook
```

Open `Chicago_Project.ipynb` and run the cells in order. Some heavy preprocessing/training cells may take time depending on your machine.

## Requirements

A minimal `requirements.txt` is included with common packages used in the notebook. See `requirements.txt`.

Notes on optional packages:
- Geospatial analysis (if present) may use `geopandas` which often requires system libraries—install it separately if needed.

## Reproducibility tips

- Use a recent Python 3.8+ interpreter.
- If processing the full dataset is slow, sample or filter by year/date range while iterating on features and model choices.
- Save intermediate preprocessed datasets (Parquet/CSV) to speed up experimentation.

## Example notebook sections

- 00_data_load_and_inspect
- 01_preprocessing_and_feature_engineering
- 02_model_training_and_cv
- 03_evaluation_and_visualization

(Actual sections and cell names may differ; open `Chicago_Project.ipynb` to view.)

## Notes on modeling choices

- LightGBM is used for its speed and support for categorical features. Consider tuning: learning rate, num_leaves, max_depth, feature_fraction, bagging_fraction, and number of boosting rounds.
- For time-based forecasting, use time-aware CV (e.g., expanding window) rather than random CV.

## Dataset license & citation

The data comes from the City of Chicago Data Portal. Please cite it as originating from the City of Chicago data portal and respect any terms listed on their site.

Chicago Data Portal: https://data.cityofchicago.org/

## Next steps (ideas)

- Add a script to download the latest data via the Socrata API.
- Add a lightweight evaluation script to reproduce reported metrics automatically.
- Containerize the environment with `Dockerfile` or provide a Binder link for reproducibility.

## Contact

If you want changes or additional sections (example: a short results summary, figures exported, or scripts to run training headlessly), tell me what to include and I can add them.

---

Created for the local notebook: `Chicago_Project.ipynb` in this workspace.
