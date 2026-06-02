# GridPredict — AI Renewable Energy Analytics Platform
GridPredict forecasts Texas wind and solar generation hour-by-hour, scores grid stress in real time, and lets operators ask natural language questions — all validated against a real hurricane.
End-to-end renewable energy forecasting platform. Predicts solar & wind generation using XGBoost and Prophet on ERCOT data, computes real-time grid stress scores with ramp-rate alerting, and answers operator queries via a RAG assistant backed by ERCOT reports. Deployed on Streamlit.

## Architecture

    ERCOT API + Open-Meteo API
              │
              ▼
       Feature Engineering
       ┌──────┴──────┐
       ▼             ▼
    XGB Features  Prophet Features
       │             │
       ▼             ▼
    XGBoost       Prophet
    (Primary)     (Baseline)
       │             │
       └──────┬──────┘
              ▼
       Model Evaluation → Best MAPE wins → MLflow
              │
       ┌──────┴──────┐
       ▼             ▼
    Grid Risk     RAG Assistant
    Engine        FAISS + Groq
       └──────┬──────┘
              ▼
      Streamlit Dashboard

## Modules

| Module | Description | Status |
|--------|-------------|--------|
| Data Pipeline | ERCOT + Open-Meteo ingestion, merge, quality report | 🔄 In progress |
| Feature Store | XGBoost features + Prophet features (dual output) | ⏳ Pending |
| XGBoost Model | Point forecast + quantile intervals (p10/p90) + SHAP | ⏳ Pending |
| Prophet Model | Trend + seasonality decomposition baseline | ⏳ Pending |
| Model Evaluation | MAE / RMSE / MAPE — best model auto-selected via MLflow | ⏳ Pending |
| Grid Risk Engine | Stress score + ramp-rate alerts + Beryl validation | ⏳ Pending |
| RAG Assistant | LangChain + FAISS + Groq, source-cited answers | ⏳ Pending |
| Dashboard | Streamlit 3-page app — Forecast / Risk / AI Chat | ⏳ Pending |

## Model Strategy

Three models trained and compared on the same 2024 holdout test set. Winner = lowest MAPE → logged to MLflow → used in dashboard + grid risk engine.

| Model | Role |
|-------|------|
| XGBoost alone | Primary candidate |
| Prophet alone | Baseline |
| XGBoost + Prophet | Ensemble candidate |

## Setup

    git clone https://github.com/jkoonam/GridPredict-AI-Renewable-Energy-Analytics-Platform.git
    cd GridPredict-AI-Renewable-Energy-Analytics-Platform
    python -m venv venv
    venv\Scripts\activate
    pip install -r requirements.txt
    cp .env.example .env

## Dataset

- [ERCOT Hourly Generation](https://www.ercot.com/gridinfo/generation)
- [Open-Meteo Historical Weather](https://open-meteo.com)
- ERCOT CDRs + Seasonal Assessment PDFs (for RAG assistant)

## Tech Stack

| Layer | Tools |
|-------|-------|
| Data | Pandas, NumPy, PyArrow, Requests |
| ML | XGBoost, Prophet, Scikit-learn, Optuna |
| Explainability | SHAP |
| Tracking | MLflow |
| RAG | LangChain, FAISS, Groq (Llama 3) |
| Dashboard | Streamlit, Plotly |
| Deployment | Streamlit Community Cloud |
