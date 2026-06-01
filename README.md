# Renewable Energy Grid Intelligence Platform

End-to-end renewable energy forecasting platform. Predicts solar & wind 
generation using XGBoost on ERCOT data, computes real-time grid stress 
scores with ramp-rate alerting, and answers operator queries via a RAG 
assistant backed by ERCOT reports. Deployed on Streamlit.

## Architecture
Data Pipeline → Feature Store → XGBoost Forecast → Grid Risk Engine → Streamlit Dashboard
                                                                      ↑
                                          ERCOT PDFs → FAISS → RAG Assistant

## Modules
| Module | Description | Status |
|--------|-------------|--------|
| Data Pipeline | ERCOT + Open-Meteo ingestion | 🔄 In progress |
| Forecasting | XGBoost solar & wind models | ⏳ Pending |
| Grid Risk | Stress score + ramp alerts | ⏳ Pending |
| RAG Assistant | LangChain + FAISS + Groq | ⏳ Pending |
| Dashboard | Streamlit 3-page app | ⏳ Pending |

## Setup
\```bash
git clone https://github.com/YOUR_USERNAME/renewable-energy-grid-intelligence.git
cd renewable-energy-grid-intelligence
pip install -r requirements.txt
cp .env.example .env   # add your Groq API key
\```

## Dataset
- [ERCOT Hourly Generation](https://www.ercot.com/gridinfo/generation)
- [Open-Meteo Historical Weather](https://open-meteo.com)
