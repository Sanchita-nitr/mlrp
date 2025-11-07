# 🌊 JalTantra: Flood Intelligence & Safe Routing System

## 💡 AI-Powered Flood Severity Classification & Geospatial Route Optimization

### By our Dev Team (e.g., ChaosCoded)


<p align="center">
  <strong>Real-time flood severity assessment + intelligent safe routing = life-saving precision.</strong>
</p>

---

This repository contains the complete source code for **JalTantra**, an integrated, forward-thinking system designed to leverage computer vision for **real-time flood severity assessment** and calculate the optimal **safe route** for navigation by dynamically avoiding clogged road segments. This is a total **game-changer** for emergency routing.

For detailed setup and configuration, refer to the README files inside each module.

---

## 🌟 Key Features

### 🤖 AI/ML Intelligence

- **Real-time Flood Classification**: MobileNetV2 model classifies images into four severity classes (`0_no_flooding` → `3_high_severity`). Built for **speed** and **scalability**.
- **Transfer Learning Pipeline**: Dual-phase training (Head Training + Fine-Tuning) on MobileNetV2 for max efficiency.
- **Inference API**: High-performance **FastAPI** endpoint for production-grade predictions.

### 🧭 Geospatial Routing & Safety

- **Safe Route Algorithm**: Built on **Shapely**, analyzing geometric proximity (~55m buffer) to clogged roads for hyper-accurate route safety.
- **Concurrent Data Fetching**: Uses `asyncio` + `httpx` for concurrent Google Maps + clog data fetches. **Low latency, no excuses.**
- **Dynamic Warnings**: If all paths are compromised, the system still returns the best possible route—transparently.

### ⚙️ System Interoperability

- **Microservice Architecture**: AI inference (`api.py`) and routing logic (`main.py`) separated for clean modular scaling.
- **Environment Parity**: Ready for **Docker** and deployment across any infrastructure.

---

## 🧩 Project Modules

### 🤖 Flood Detection Module

Your **AI backbone** — handles training, prediction, and deployment for flood classification.

- **Model**: MobileNetV2 (Transfer Learning)
- **Libraries**: PyTorch, torchvision, `tqdm`
- **Output**: `best_flood_model.pth` (trained weights)
- **Serving**: via `api.py` (FastAPI @ Port 8080)

📁 Documentation: `/AI/README.md`

---

### 🧭 Route Optimization API

The **logic brain** — integrates geospatial analysis, Google Maps, and AI predictions.

- **Framework**: FastAPI (async-first)
- **Geospatial Tools**: Shapely, Polyline
- **Integration**: Google Maps Directions API + internal Clogged Data Service (`127.0.0.1:5050`)

📁 Documentation: `/API/README.md`

> **Environment Variables:** `.env` file required for configuration.

```env
# Google Maps API Key for Directions Service
GOOGLE_MAPS_API_KEY="your_google_maps_api_key_here"

# The URL for the Clogged Data Service
# CLOGGED_ROADS_URL="http://127.0.0.1:5050/api/cordinates"

## 🚀 Quick Start: Deployment is the Goal

### 🧠 Prerequisites
- Python 3.8+
- Trained model: `best_flood_model.pth`
- Google Maps Directions API Key

---
🚀 Quick Start: Deployment is the Goal
Prerequisites
Python 3.8+
Trained model: best_flood_model.pth
Google Maps Directions API Key
Setup Order: Synergy First!
Clone the Repo & Setup Venv
git clone [repository-link]
cd JalTantra
python -m venv venv
source venv/bin/activate
Install Dependencies
pip install torch torchvision torchaudio
pip install fastapi uvicorn[standard] httpx polyline python-dotenv
pip install pillow shapely
Configure .env
GOOGLE_MAPS_API_KEY="YOUR_API_KEY_HERE"
Start AI Prediction API (Port 8080)
python api.py
# AI Service: http://127.0.0.1:8080
Start Safe Route API (Port 8000)
python main.py
# Route Service: http://127.0.0.1:8000
# Docs: http://127.0.0.1:8000/docs
📊 System Architecture
┌─────────────────┐
│  AI Inference   │  FastAPI / PyTorch
│  (Port 8080)    │  - Flood Severity Prediction
└────────┬────────┘
         │
         ▼
┌────────────────────────┐ 
│  Data Integrator (5050)│  ⟵ CRITICAL MISSING SERVICE
│  - Stores flood coords │
└────────┬───────────────┘
         │
         ▼
┌─────────────────┐    
│ Safe Route API  │  FastAPI / Shapely
│  (Port 8000)    │  - Geospatial Route Check 
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Google Maps API│
└─────────────────┘
🎯 Core Capabilities
1. Flood Severity API
Upload an image → get flood risk instantly.
Classes: No Flooding, Low, Medium, High.
Endpoint: POST /predict
Response Example:
{
  "severity": "Medium Severity",
  "confidence_score": 98.75
}
2. Geometric Route Exclusion
Uses buffer-based spatial checks (route_line.distance(clog_point) < CLOG_BUFFER_DEGREES)
Returns alternate route if any path intersects flooded regions.
3. Asynchronous Workflow
Async calls using httpx ensure no API blocking.
Performance = optimized concurrency.
📈 API Highlights
Flood Prediction
curl -X POST http://127.0.0.1:8080/predict -F "file=@sample.jpg"
# → {"severity": "High Severity", "confidence_score": 96.22}
Safe Route Calculation
POST /api/safe-route
{
  "origin": "Raipur Railway Station",
  "destination": "Swami Vivekananda Airport Raipur"
}
# → {"status": "SAFE_ROUTE_FOUND", "message": "Safe route found via Ring Road No. 3"}
