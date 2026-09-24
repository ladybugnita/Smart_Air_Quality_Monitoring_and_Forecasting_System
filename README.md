# 🌍 Smart Air Quality Intelligence and Forecasting System

**Bayumandal** is an AI-powered web platform for real-time air quality monitoring, 24-hour AQI forecasting, and health guidance.

> Final-year project for the Bachelor of Computer Applications (BCA), Nepal College of Information Technology, Pokhara University (2026).

Most air quality apps only show the current AQI, often in technical terms that are hard to act on. This system goes further. It **predicts** air quality for the next 24 hours, gives **smart safety advice** based on a user's age, health condition, and sensitivity, and answers questions through an **AI chatbot**.

---

## ✨ Features

- **Real-time monitoring:** live AQI, pollutant levels (PM2.5, PM10, CO, NO₂, SO₂, O₃), and weather data for **294 cities across 123 countries**, powered by the Open-Meteo API
- **24-hour AQI forecasting:** a multi-output Random Forest model predicts hourly AQI for the next 24 hours, shown as trend charts and an hourly table
- **Smart Safety Guides:** smart safety guidance from a content-based filtering engine that considers current AQI, disease, age, and health sensitivity, downloadable as a PDF
- **AI chatbot:** answers questions about air quality, pollutants, health effects, and precautions using the Gemini API
- **Interactive global map:** color-coded AQI map with the most polluted countries ranked

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React.js |
| Backend | Java, Spring Boot, REST APIs |
| Database | MySQL |
| Machine Learning | Python, scikit-learn (Random Forest), FastAPI |
| External APIs | Open-Meteo (air quality and weather), Gemini (AI chatbot), Google Maps |
| Tools | Git, GitHub, Postman, Figma, Draw.io |

---

## 🏗️ System Architecture

```
            User (Browser)
                  │
                  ▼
          React Frontend
                  │  REST API
                  ▼
        Spring Boot Backend ──────► External APIs (Open-Meteo, Gemini)
          │               │
          ▼               ▼
   MySQL Database   Python ML API (FastAPI)
                          │
                          ▼
                 Random Forest AQI Model
```

The React frontend communicates only with the Spring Boot backend. The backend handles data storage, fetches live data from external APIs, generates safety guidance, and calls the separate Python ML service for AQI predictions.

---

## 🤖 Machine Learning Model

Five models were trained and compared on the same dataset. **Random Forest** was selected for its strong balance of accuracy, speed, and interpretability (feature importance).

**Final model: Multi-Output Random Forest Regressor**

| Metric | Value |
|---|---|
| Test R² Score | 0.886 |
| Training R² Score | 0.933 |
| Mean Absolute Error | 12.28 AQI |
| Root Mean Squared Error | 23.14 AQI |

**Accuracy by forecast horizon:** R² ≈ 0.95 (1 hour ahead), ≈ 0.90 (12 hours ahead), ≈ 0.79 (24 hours ahead)

**Most important features:** current AQI, PM2.5, PM10, carbon monoxide, city, and ozone

The model uses 42 features, including pollutant and weather data, time features (hour, day, month), and lag and rolling statistics.

> **Note:** The ML training code and trained model are not included in this repository due to file size limits.

---

## 👩‍💻 My Contributions (Nita Dangol)

This was a team project built by four students. I was responsible for the **backend development** and also contributed to research, documentation, and integration throughout the project.

### Backend Development (Spring Boot)
- Developed the complete **Spring Boot backend** connecting the React frontend, MySQL database, Python ML service, and external APIs
- Designed the **MySQL database schema** (locations, AQI records, pollutant data, weather data, predictions, and health recommendations) with proper entity relationships
- Built the **RESTful APIs** for live AQI data, pollutant information, AQI rankings, prediction requests, and safety guidance
- Integrated the **Python/FastAPI Random Forest prediction service** with the backend to deliver 24-hour AQI forecasts
- Connected the **React frontend** to the backend APIs for a complete end-to-end workflow

### Smart Safety Guides Recommendation Engine
- Designed and implemented the **content-based filtering engine** that generates smart safety guidance
- Built a **weighted scoring system** that ranks safety guides using four factors: AQI band (weight 3), disease (weight 3), age (weight 2), and health sensitivity (weight 2), with extra weight for condition severity
- Made sure each factor meaningfully changes which guides appear and how they are ranked, so recommendations are genuinely personalized rather than based on AQI alone

### Research, Documentation & Integration
- Participated in the **literature review** of existing air quality monitoring and AQI forecasting research, which shaped our choice of model and features
- Contributed to writing the **project proposal**, **mid-term report**, and **final report**
- Worked with the team to integrate the frontend, backend, database, ML model, AI chatbot, and external APIs into one system

---

## 👥 Team

| Member | Role |
|---|---|
| Biplov Gautam | Machine Learning |
| Deepak Khanal | Data Collection, AI Chatbot & Project Management |
| Jenish Bhattarai | Frontend Development |
| Nita Dangol | Backend Development |

**Supervisor:** Er. Roshan Kumar Sah

**Original repository:** [biplov2061/Smart_Air_Quality_Monitoring_and_Forecasting_System](https://github.com/biplov2061/Smart_Air_Quality_Monitoring_and_Forecasting_System)

---

## 🔮 Future Work

- Mobile apps for iOS and Android
- IoT sensor integration for hyperlocal monitoring
- Multi-day (3 to 7 day) forecasts
- Multilingual chatbot support, including Nepali
