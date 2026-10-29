# Air Pollution in Skopje

Class project that looks at air pollution (PM2.5 and PM10) in Skopje from 2016 to 2025. We pull air quality and weather data, clean and combine them, then try to understand what drives high pollution days and whether we can predict them.

## Data sources

- **Air quality** – hourly measurements from the [OpenAQ API](https://openaq.org) (PM2.5, PM10, CO, NO, etc.) across several Skopje stations.
- **Weather** – hourly data from the [Open-Meteo archive](https://open-meteo.com) for Skopje (41.9981, 21.4254).

You need an OpenAQ API key stored in a `.env` file as `OPENAQ_API_KEY=...`. Raw downloads go to `data/raw/`, cleaned data goes to `data/processed/`.

## Notebooks

Run in order. Steps 1–2 can be skipped if `data/raw/` already has the downloads.

1. `01_weather_collection.ipynb` – download weather data from Open-Meteo
2. `02_air_quality_collection.ipynb` – download air quality data from OpenAQ
3. `03_build_daily_dataset.ipynb` – combine into a daily air + weather dataset
4. `04_missingness_and_station_selection.ipynb` – handle missing data, pick stations, flag PM inconsistencies
5. `05_eda.ipynb` – explore distributions, seasonal patterns, correlations
6. `06_feature_engineering.ipynb` – create lag features, rolling stats, calendar encodings, and labels for high-pollution days
7. `07_forecasting_regression.ipynb` – predict next-day PM2.5 and PM10
8. `08_high_pollution_classification.ipynb` – classify whether a day will be high-pollution (>25 µg/m³ for PM2.5)
9. `09_clustering.ipynb` – group days into pollution regimes using KMeans, GMM, DBSCAN, and hierarchical clustering

## Project structure

```
data/
  raw/          # downloaded hourly data
  processed/    # daily dataset, features, model outputs
notebooks/      # the 9 notebooks above
output/figures/ # saved plots
reports/        # project documentation
```

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
# put your OpenAQ API key in a .env file
jupyter lab
```

Model predictions, metrics, and cluster labels are saved as parquet files in `data/processed/`. Plots are saved to `output/figures/`.
