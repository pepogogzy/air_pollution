# Air Pollution in Skopje

Class project analyzing air pollution in Skopje over 2016–2025: combine air quality and weather data, clean it, and understand what drives high PM2.5/PM10 days — and predict and cluster them.

## Data

- **Air quality** – hourly measurements from the [OpenAQ API](https://openaq.org) (PM2.5, PM10, CO, NO, etc.), several Skopje stations.
- **Weather** – hourly data from the [Open-Meteo archive](https://open-meteo.com) for Skopje (41.9981, 21.4254).

Your `OPENAQ_API_KEY` goes in a `.env` file. Raw downloads live in `data/raw/`, the cleaned daily air+weather dataset (per station, with PM10<PM2.5 consistency flags) in `data/processed/air_pollution_weather_daily_master.parquet`, engineered features and model metrics/predictions also in `data/processed/`.

## Code organization

```
data/
  raw/          # downloaded hourly air quality + weather
  interim/      # intermediate output (mostly unused)
  processed/    # daily dataset, features, model outputs
notebooks/      # numbered pipeline: collection -> EDA -> modeling
output/figures/ # generated plots
reports/        # write-ups
```

Notebooks (run in order):

1. `01_weather_collection.ipynb` – Open-Meteo download
2. `02_air_quality_collection.ipynb` – OpenAQ download
3. `03_build_daily_dataset.ipynb` – build daily air + weather dataset
4. `04_missingness_and_station_selection.ipynb` – missingness, station selection, PM consistency
5. `05_eda.ipynb` – distributions, seasonal patterns, correlations
6. `06_feature_engineering.ipynb` – lags, rolling stats, calendar encodings, high-day labels
7. `07_forecasting_regression.ipynb` – predict next-day PM2.5/PM10
8. `08_high_pollution_classification.ipynb` – classify high (>25 µg/m³) PM2.5 days
9. `09_clustering.ipynb` – find pollution regimes (KMeans, GMM, DBSCAN)

## Setup & execution

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
# add your OpenAQ API key to .env (OPENAQ_API_KEY=...)
jupyter lab
```

Run notebooks `01`–`09` in order; steps 1–2 can be skipped if `data/raw/` downloads are already present. Plots are saved to `output/figures/`, model outputs to `data/processed/`.