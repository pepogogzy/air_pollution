# Air Pollution in Skopje

Class project on analyzing air pollution in Skopje over the period 2016–2025. The idea is to combine air quality and weather data, clean it up, and try to understand what drives high PM2.5/PM10 days – and maybe predict them.

## Data sources

- **Air quality** – hourly measurements from the [OpenAQ API](https://openaq.org) (PM2.5, PM10, etc.).
- **Weather** – hourly weather from the [Open-Meteo archive](https://open-meteo.com) for Skopje (41.9981, 21.4254).

The `OPENAQ_API_KEY` goes in a `.env` file.

## Project structure

```
data/
  raw/          # downloaded hourly air quality + weather
  interim/      # intermediate stuff
  processed/    # cleaned daily dataset, features, model outputs
notebooks/      # numbered pipeline: collection -> EDA -> modeling
output/figures/ # generated plots
src/            # shared helpers
reports/        # write-ups
```

## Notebooks (run in order)

1. Weather collection (Open-Meteo)
2. Air quality collection (OpenAQ)
3. Build daily dataset (air + weather combined)
4. Missingness and station selection
5. EDA
6. Feature engineering
7. Regression / forecasting
8. Classification of high pollution days
9. Clustering

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
# add your OpenAQ API key to .env (OPENAQ_API_KEY=...)
jupyter lab
```

## Results

Plots are saved to `output/figures/` and model metrics to `data/processed/`. Nothing too fancy – mostly exploring whether weather features help predict pollution days in Skopje.