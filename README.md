# 🍽️ Swiggy Delivery Time Prediction API

**FastAPI + MLflow + DagsHub powered application to predict food delivery times based on real-world features.**

[![FastAPI](https://img.shields.io/badge/FastAPI-2023-green?style=flat-square\&logo=fastapi)](https://fastapi.tiangolo.com/)
[![MLflow](https://img.shields.io/badge/MLflow-Tracking-blue?style=flat-square\&logo=mlflow)](https://mlflow.org/)
[![DagsHub](https://img.shields.io/badge/DagsHub-Integration-orange?style=flat-square\&logo=dagshub)](https://dagshub.com/)

---

## 🚀 Overview

This repository hosts a FastAPI-based machine learning inference system that predicts delivery times for Swiggy orders. The model uses data such as weather, traffic, delivery person info, and more.

### ✨ Features

* 🔥 **FastAPI Framework**: Interactive REST API documentation via Swagger UI.
* 📦 **MLflow Integration**: Track and retrieve models through MLflow and DagsHub.
* 🧹 **Preprocessing Pipeline**: Clean and transform inputs before prediction.
* 📊 **Live Prediction Endpoint**: `/predict` endpoint accepts user data and returns delivery time.
* ☁️ **Docker-Ready**: Easily containerizable for deployment on any cloud platform.

---

## 📁 Project Structure

```plaintext
.
├── app.py                    # Main FastAPI app
├── run_information.json      # Model metadata info
├── models/
│   └── preprocessor.joblib   # Preprocessing pipeline
├── scripts/
│   └── data_clean_utils.py   # Data cleaning utilities
├── requirements.txt          # Required Python packages
└── README.md                 # Project documentation
```

---

## ⚙️ Getting Started

### ✅ Prerequisites

* Python 3.8 or above
* Access to your DagsHub + MLflow repository

### 📥 Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/jatingyass/swiggydeliverytimeprediction.git
   cd swiggydeliverytimeprediction
   ```

2. **Create a virtual environment**

   ```bash
   python -m venv venv
   source venv/bin/activate     # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Configure MLflow + DagsHub in `app.py`**

   ```python
   from dagshub import dagshub
   import mlflow

   dagshub.init(repo_owner='jatingyass',
                repo_name='swiggydeliverytimeprediction',
                mlflow=True)

   mlflow.set_tracking_uri("https://dagshub.com/jatingyass/swiggydeliverytimeprediction.mlflow")
   ```

---

## ▶️ Running the App

Start the FastAPI server using Uvicorn:

```bash
uvicorn app:app --host 0.0.0.0 --port 8000
```

Visit the interactive API docs at:

```
http://localhost:8000/docs
```

---

## 📬 Prediction Endpoint

Send a POST request to `/predict` with the following JSON format:

```json
{
  "ID": "12345",
  "Delivery_person_ID": "DP001",
  "Delivery_person_Age": "30",
  "Delivery_person_Ratings": "4.5",
  "Restaurant_latitude": 19.0760,
  "Restaurant_longitude": 72.8777,
  "Delivery_location_latitude": 19.2183,
  "Delivery_location_longitude": 72.9781,
  "Order_Date": "2025-01-25",
  "Time_Orderd": "18:30:00",
  "Time_Order_picked": "18:45:00",
  "Weatherconditions": "Sunny",
  "Road_traffic_density": "High",
  "Vehicle_condition": 5,
  "Type_of_order": "Veg",
  "Type_of_vehicle": "Bike",
  "multiple_deliveries": "1",
  "Festival": "No",
  "City": "Mumbai"
}
```

The response will include the predicted delivery time in minutes.

---

## 🧠 Key Components

### 1. Preprocessing

Input data is cleaned and processed using a pipeline stored in `models/preprocessor.joblib`.

### 2. MLflow + DagsHub Integration

* Tracks experiments
* Fetches the latest production-ready model
* Allows reproducible results

### 3. FastAPI Endpoints

| Endpoint   | Description                      |
| ---------- | -------------------------------- |
| `/`        | Welcome route                    |
| `/predict` | Predicts delivery time from data |

---

## 📦 Docker Deployment

### Example `Dockerfile`

```dockerfile
FROM python:3.8-slim

WORKDIR /app

COPY . /app

RUN pip install --no-cache-dir -r requirements.txt

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

Then build and run:

```bash
docker build -t swiggy-predictor .
docker run -p 8000:8000 swiggy-predictor
```


---

## 🙏 Acknowledgements

* [FastAPI Docs](https://fastapi.tiangolo.com/)
* [MLflow Docs](https://www.mlflow.org/)
* [DagsHub Docs](https://dagshub.com/docs/)

---

## 🛠️ Contributing

Want to improve the project?
Feel free to fork, open issues, or submit a pull request.

> Made with ❤️ by [Jatin Gyass](https://github.com/jatingyass)

