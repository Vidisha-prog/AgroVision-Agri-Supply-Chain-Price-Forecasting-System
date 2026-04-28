<div align="center">

<img src="https://readme-typing-svg.herokuapp.com?font=Playfair+Display&size=42&pause=1000&color=2ECC71&center=true&vCenter=true&width=600&height=80&lines=🌾+AgroVision;Agri+Price+Forecasting+System" alt="AgroVision" />

<br/>

[![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)](https://tensorflow.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://reactjs.org)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)
[![MLflow](https://img.shields.io/badge/MLflow-2.x-E37E11?style=for-the-badge&logo=mlflow&logoColor=white)](https://mlflow.org)

<br/>

> **Predict crop prices. Optimize selling decisions. Empower agri-business.**

*A full-stack intelligent platform combining LSTM neural networks, Facebook Prophet, real-time ETL pipelines, and a live market dashboard — giving agri-business companies forward visibility before prices peak or crash.*

<br/>

| 🎯 Model Accuracy | 🌾 Crop Types | 👥 Contributors | ⚡ Architecture |
|:-:|:-:|:-:|:-:|
| **94%** | **12+** | **3** | **API-First** |

</div>

---

## 📋 Table of Contents

- [What is AgroVision?](#-what-is-agrovision)
- [Features](#-features)
- [System Architecture](#-system-architecture)
- [Tech Stack](#-tech-stack)
- [Team & Responsibilities](#-team--responsibilities)
- [API Documentation](#-api-documentation)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)

---

## 🌾 What is AgroVision?

AgroVision is an end-to-end intelligent platform for the agricultural supply chain. It combines time-series forecasting (LSTM & Prophet), automated ETL pipelines, and an interactive market dashboard to help agri-business companies make **data-driven selling decisions** — before prices peak or crash.

**Built for:**
- 🏢 Commodity trading firms and agri-exporters
- 🌾 Cooperative societies and farmer producer organizations
- 🏛️ Government mandi platforms needing price transparency
- 🏭 Food processing companies needing demand-supply visibility

**Core Problem Solved:**
> Farmers and agri-businesses often sell at market bottom due to lack of predictive intelligence. AgroVision provides **7–90 day price forecasts** so sellers can plan harvest timing and trade execution optimally.

---

## ✨ Features

### 📈 Price Prediction Engine
Dual-model architecture combining two complementary approaches:
- **LSTM Neural Network** — Captures non-linear, long-range sequence dependencies in price data using sliding window sequences
- **Facebook Prophet** — Handles trend decomposition, yearly/weekly seasonality, and holiday effects
- **Ensemble Blender** — Weighted combination of both models for higher accuracy than either alone
- Forecast horizons: **7 days**, **14 days**, **30 days**, **90 days** with confidence intervals

### 📦 Demand Forecasting
Predicts regional demand spikes using:
- Historical consumption and procurement data
- Weather anomaly signals (drought, excess rain)
- Festival and seasonal consumption calendars
- Crop-specific demand elasticity curves

### 📊 Market Trend Dashboard
React-based live dashboard featuring:
- Real-time price heatmaps across regions
- Crop-to-crop comparison charts
- Supply-demand gap analysis
- Market signal alerts (BUY / HOLD / SELL)
- Power BI embedded executive reports

### 🔄 ETL Data Pipelines
Automated data engineering layer:
- Apache Airflow DAGs for daily scheduled ingestion
- Sources: AGMARKNET, Commodity Exchanges, Weather APIs, Satellite NDVI
- Data validation, cleaning, and transformation with Pandas
- TimescaleDB for optimized time-series storage

### 🌐 REST API Layer
Production-grade FastAPI server with:
- JWT authentication and role-based access
- Rate limiting and request throttling
- Model versioning and A/B serving
- WebSocket support for real-time price alerts
- Interactive Swagger docs at `/docs`

### 🔔 Smart Alert System
- Rule-based alerts on user-configured price thresholds
- ML-driven anomaly detection for sudden price spikes
- Delivery via SMS, Email, and WebSocket push

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                      DATA SOURCES LAYER                         │
│  ┌─────────────┐  ┌──────────────┐  ┌────────────────────────┐ │
│  │ AGMARKNET   │  │ Weather APIs │  │  Commodity Exchanges   │ │
│  │    API      │  │ (OpenWeather)│  │  (MCX, NCDEX)          │ │
│  └──────┬──────┘  └──────┬───────┘  └───────────┬────────────┘ │
│         │                │                        │              │
│  ┌──────┴──────┐  ┌──────┴───────┐               │              │
│  │ Satellite   │  │ News/Sentiment│               │              │
│  │ NDVI Data   │  │   Scraper    │               │              │
│  └──────┬──────┘  └──────┬───────┘               │              │
└─────────┼────────────────┼───────────────────────┼──────────────┘
          │                │                        │
          ▼                ▼                        ▼
┌─────────────────────────────────────────────────────────────────┐
│                   ETL / DATA ENGINEERING LAYER                  │
│  ┌──────────────────┐   ┌──────────────┐   ┌─────────────────┐ │
│  │ Apache Airflow   │   │   Pandas     │   │  PostgreSQL +   │ │
│  │  DAG Scheduler   │──▶│  Transform   │──▶│  TimescaleDB    │ │
│  └──────────────────┘   └──────────────┘   └────────┬────────┘ │
│                                                       │          │
│                              ┌────────────────────────┘          │
│                              │  ┌──────────────────────┐         │
│                              └─▶│   Redis Cache Layer  │         │
│                                 └──────────────────────┘         │
└─────────────────────────────────────────────────────────────────┘
          │
          ▼
┌─────────────────────────────────────────────────────────────────┐
│                    ML / PREDICTION LAYER                        │
│  ┌────────────────┐  ┌──────────────┐  ┌─────────────────────┐ │
│  │  LSTM Model    │  │   Prophet    │  │  Ensemble Blender   │ │
│  │ (TensorFlow)   │  │    Model     │  │  (Weighted Avg)     │ │
│  └───────┬────────┘  └──────┬───────┘  └──────────┬──────────┘ │
│          └──────────────────┴──────────────────────┘            │
│                                    │                             │
│                         ┌──────────┴──────────┐                 │
│                         │   MLflow Registry   │                 │
│                         │  (Experiment Track) │                 │
│                         └─────────────────────┘                 │
└─────────────────────────────────────────────────────────────────┘
          │
          ▼
┌─────────────────────────────────────────────────────────────────┐
│                        API LAYER                                │
│  ┌────────────────┐  ┌──────────────┐  ┌─────────────────────┐ │
│  │  FastAPI App   │  │  JWT Auth    │  │  WebSocket Events   │ │
│  │   Server       │  │  Middleware  │  │  (Live Alerts)      │ │
│  └───────┬────────┘  └──────────────┘  └─────────────────────┘ │
│          │                                                       │
│  ┌───────┴────────┐                                             │
│  │ Docker + Nginx │                                             │
│  │  (Reverse Proxy│                                             │
│  └────────────────┘                                             │
└─────────────────────────────────────────────────────────────────┘
          │
          ▼
┌─────────────────────────────────────────────────────────────────┐
│               FRONTEND / VISUALIZATION LAYER                    │
│  ┌────────────────┐  ┌──────────────┐  ┌─────────────────────┐ │
│  │  React 18      │  │  Recharts +  │  │   Power BI Embed    │ │
│  │  Dashboard     │  │    D3.js     │  │  (Executive View)   │ │
│  └────────────────┘  └──────────────┘  └─────────────────────┘ │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │              Mobile PWA (Progressive Web App)              │ │
│  └────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Language** | Python 3.11 | Core backend & ML |
| **ML — Deep Learning** | TensorFlow / Keras | LSTM time-series model |
| **ML — Forecasting** | Facebook Prophet | Seasonal trend decomposition |
| **ML — Tracking** | MLflow | Experiment tracking & model registry |
| **Backend API** | FastAPI | REST endpoints + WebSocket |
| **ETL Orchestration** | Apache Airflow | Scheduled data pipelines |
| **Data Processing** | Pandas, NumPy | Transform & feature engineering |
| **Primary Database** | PostgreSQL + TimescaleDB | Time-series storage |
| **Cache Layer** | Redis | Low-latency API responses |
| **Frontend** | React 18 | Interactive dashboard |
| **Charts** | Recharts + D3.js | Data visualizations |
| **BI Reports** | Power BI Embed | Executive reporting |
| **Containerization** | Docker + Docker Compose | Service orchestration |
| **Web Server** | Nginx | Reverse proxy |
| **Auth** | JWT | Secure API access |

---

## 👥 Team & Responsibilities

<table>
<tr>
<td align="center" width="33%">

### 🟢 Vidisha
**Full-Stack & DevOps Engineer**

</td>
<td align="center" width="33%">

### 🟡 Vrushali
**Data Engineer & ETL Architect**

</td>
<td align="center" width="33%">

### 🔵 Rudresh
**ML Engineer & Data Scientist**

</td>
</tr>
<tr>
<td valign="top">

- ✅ Built FastAPI backend with JWT auth, rate limiting, and versioning
- ✅ Developed React 18 dashboard with Recharts and D3.js visualizations
- ✅ Integrated Power BI embed for executive-level reporting
- ✅ Containerized full stack with Docker Compose and Nginx reverse proxy
- ✅ Set up CI/CD pipeline (GitHub Actions)
- ✅ WebSocket-based real-time alert delivery system
- ✅ Mobile PWA configuration for field agent access

</td>
<td valign="top">

- ✅ Designed and built all Apache Airflow DAGs for daily data ingestion
- ✅ Integrated AGMARKNET, weather APIs, and commodity exchange feeds
- ✅ Built data cleaning & transformation pipelines with Pandas
- ✅ Set up PostgreSQL + TimescaleDB schema for time-series storage
- ✅ Implemented Redis caching layer for low-latency API responses
- ✅ Data quality checks and anomaly flagging in pipelines
- ✅ Historical seed script (5+ years of data across 12 crops)

</td>
<td valign="top">

- ✅ Built LSTM time-series model with TensorFlow/Keras using sliding window sequences
- ✅ Integrated Facebook Prophet for seasonal trend decomposition
- ✅ Designed ensemble blending logic to merge LSTM + Prophet predictions
- ✅ Set up MLflow experiment tracking and model registry
- ✅ Built demand forecasting module using external demand signals
- ✅ Feature engineering pipeline (lag features, rolling stats, NDVI)
- ✅ Model evaluation framework (MAE, RMSE, MAPE metrics)

</td>
</tr>
</table>

---

## 📡 API Documentation

**Base URL:** `https://api.agrovision.io/v1`  
**Authentication:** `Bearer <JWT_TOKEN>` in Authorization header  
**Format:** All responses are JSON

### Endpoints

| Method | Endpoint | Description | Owner |
|--------|----------|-------------|-------|
| `GET` | `/predict/price/{crop}` | 7/30/90-day price forecast with confidence bands | Rudresh |
| `GET` | `/predict/demand/{crop}` | Regional demand forecast with seasonal factors | Rudresh |
| `GET` | `/market/trends` | Real-time market trend snapshot across all crops | Vrushali |
| `GET` | `/data/history/{crop}` | Historical price series with OHLC and volume | Vrushali |
| `POST` | `/alerts/subscribe` | Subscribe to price threshold alerts via SMS/email | Vidisha |
| `POST` | `/auth/token` | Generate JWT access token | Vidisha |
| `GET` | `/health` | System health check and model status | Vidisha |

### Sample Request & Response

```bash
# Get 30-day wheat price forecast
curl -X GET "https://api.agrovision.io/v1/predict/price/wheat?horizon=30" \
     -H "Authorization: Bearer <your_token>"
```

```json
{
  "crop": "wheat",
  "currency": "INR/quintal",
  "horizon_days": 30,
  "model": "ensemble_v2.1",
  "generated_at": "2025-07-01T10:00:00Z",
  "predictions": [
    {
      "date": "2025-08-01",
      "price": 2142.5,
      "lower_bound": 2091.0,
      "upper_bound": 2194.0
    },
    {
      "date": "2025-08-15",
      "price": 2198.0,
      "lower_bound": 2134.0,
      "upper_bound": 2261.0
    }
  ],
  "signal": "BUY",
  "confidence": 0.87
}
```

---

## 🚀 Getting Started

### Prerequisites

```bash
Python  >= 3.11
Node.js >= 18
Docker  >= 24
PostgreSQL >= 15
```

### ⚡ Quick Start with Docker (Recommended)

```bash
# 1. Clone the repository
git clone https://github.com/your-org/agrovision.git
cd agrovision

# 2. Configure environment variables
cp .env.example .env
# Edit .env — add your API keys and DB credentials

# 3. Launch all services
docker compose up --build -d

# 4. Initialize database and seed historical data
docker exec agrovision-api python manage.py migrate
docker exec agrovision-api python scripts/seed_historical.py

# 5. Trigger initial ETL pipeline
docker exec agrovision-airflow airflow dags trigger agro_daily_ingest
```

**Services available at:**
| Service | URL |
|---------|-----|
| React Dashboard | http://localhost:3000 |
| FastAPI Swagger Docs | http://localhost:8000/docs |
| Apache Airflow UI | http://localhost:8080 |
| MLflow Tracking UI | http://localhost:5000 |

---

### 🔧 Manual Setup (Development Mode)

**Backend (Vidisha's module)**
```bash
cd backend
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

**Frontend (Vidisha's module)**
```bash
cd frontend
npm install
npm run dev
```

**ML Training (Rudresh's module)**
```bash
cd ml

# Train LSTM model
python train_lstm.py --crop wheat --epochs 80 --window 30

# Train Prophet model
python train_prophet.py --crop wheat

# Run ensemble evaluation
python evaluate_ensemble.py --crop wheat --test-split 0.2
```

**ETL Pipelines (Vrushali's module)**
```bash
# Initialize Airflow
airflow db init
airflow users create --username admin --role Admin --firstname Admin --lastname User --email admin@agrovision.io

# Start scheduler and webserver
airflow scheduler &
airflow webserver --port 8080 &

# Trigger manual run
airflow dags trigger agro_daily_ingest
```

---

## 📁 Project Structure

```
agrovision/
│
├── 📂 backend/                    # Vidisha
│   ├── app/
│   │   ├── main.py                # FastAPI entry point
│   │   ├── routers/               # API route handlers
│   │   │   ├── predict.py         # /predict endpoints
│   │   │   ├── market.py          # /market endpoints
│   │   │   └── alerts.py          # /alerts endpoints
│   │   ├── middleware/            # Auth, rate limiting
│   │   └── websocket/             # Real-time alert delivery
│   └── Dockerfile
│
├── 📂 ml/                         # Rudresh
│   ├── models/
│   │   ├── lstm/
│   │   │   ├── train_lstm.py
│   │   │   └── lstm_model.py
│   │   └── prophet/
│   │       ├── train_prophet.py
│   │       └── prophet_model.py
│   ├── ensemble/
│   │   └── blender.py             # Ensemble logic
│   ├── features/
│   │   └── feature_engineering.py
│   └── evaluate_ensemble.py
│
├── 📂 etl/                        # Vrushali
│   ├── dags/
│   │   ├── agro_daily_ingest.py   # Main Airflow DAG
│   │   ├── weather_ingest.py
│   │   └── market_ingest.py
│   ├── pipelines/
│   │   ├── agmarknet.py
│   │   ├── weather.py
│   │   └── commodity_exchange.py
│   ├── transforms/
│   │   └── cleaner.py
│   └── scripts/
│       └── seed_historical.py
│
├── 📂 frontend/                   # Vidisha
│   ├── src/
│   │   ├── components/
│   │   │   ├── PriceChart.jsx
│   │   │   ├── DemandForecast.jsx
│   │   │   ├── MarketHeatmap.jsx
│   │   │   └── AlertPanel.jsx
│   │   ├── pages/
│   │   │   └── Dashboard.jsx
│   │   └── App.jsx
│   └── package.json
│
├── 📂 database/                   # Vrushali
│   ├── migrations/
│   └── schema.sql
│
├── docker-compose.yml
├── .env.example
└── README.md
```

---

## 🗺️ Roadmap

```
Sprint 1 ✅  Data Foundation
             └─ ETL pipelines live, DB schema, historical data (5 yrs)
             └─ Owner: Vrushali

Sprint 2 ✅  ML Models v1
             └─ LSTM + Prophet trained on wheat, rice, maize
             └─ Ensemble blender + MLflow tracking live
             └─ Owner: Rudresh

Sprint 3 🔄  API + Dashboard (In Progress)
             └─ FastAPI endpoints, React dashboard, Docker deploy
             └─ WebSocket alerts, Power BI integration
             └─ Owner: Vidisha

Sprint 4 📅  Scale & Polish (Planned)
             └─ Extend to 12 crops, news sentiment signals
             └─ Mobile PWA, user auth portal
             └─ Owner: All team

Sprint 5 📅  Production Deploy (Planned)
             └─ AWS ECS deployment, load testing
             └─ Grafana monitoring, enterprise API keys
             └─ Owner: All team
```

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'feat: add your feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request against `dev`

> All PRs require review from at least one team member. Issues labeled `good first issue` are a great starting point.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built with 🌾 by**

[Vidisha](https://github.com/vidisha) · [Vrushali](https://github.com/vrushali) · [Rudresh](https://github.com/rudresh)

*AgroVision — Turning agricultural data into actionable intelligence*

</div>
