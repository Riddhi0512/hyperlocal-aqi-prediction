# Hyper-Local Air Quality Prediction for Urban Areas

[**Open Notebook in Google Colab**](https://colab.research.google.com/drive/1COmvs-ybVBJl_mdlMZr4BPzIzZ4ub70)

## Overview

This project develops a machine learning system to predict PM2.5 concentrations at a hyper-local level across major Indian cities.

Due to sparse placement of CPCB monitoring stations, typically one per 50–100 sq. km, large urban regions remain unmonitored. The system uses air quality data, weather variables, and spatial features to estimate pollution levels at different locations.

The final output is an interactive Streamlit dashboard for exploring pollution patterns, health risks, and sensor placement recommendations.

## Problem Statement

Air quality monitoring infrastructure in Indian cities is insufficient for street-level insights. This project addresses the gap by building a predictive system designed to generalize to unseen locations using machine learning.

## Dataset

- **Air quality data:** CPCB air quality data via the Kaggle `rohanrao` dataset
- **Weather data:** Open-Meteo historical API
- **Cities:** Delhi, Chennai, Bengaluru, Hyderabad, and Jaipur
- **Time period:** January–March 2019
- **Monitoring stations:** 50 (10 per city)
- **Total records:** Approximately 105,000 hourly observations

### Features Used

- **Spatial:** Latitude, longitude, road density
- **Weather:** Temperature, humidity, wind speed, wind direction
- **Pollutants:** NO2, SO2, CO, PM10
- **Time:** Hour of day, day of year
- **City:** Encoded city identifier

**Target variable:** PM2.5 (µg/m³)

## Machine Learning Models

The following models and methods were trained or evaluated:

- Linear Regression
- Ridge Regression
- Support Vector Regression (RBF kernel)
- Random Forest
- XGBoost
- Inverse Distance Weighting (IDW) spatial baseline
- KMeans clustering for zone detection

### Best Model

Random Forest achieved the best reported performance:

| Metric | Result |
|---|---:|
| R² | 0.9873 |
| MAE | 4.25 µg/m³ |
| RMSE | 6.69 µg/m³ |

## Model Evaluation

### Standard Train-Test Split

- 80/20 split across all cities
- Evaluated using MAE, RMSE, and R²

### Leave-One-Station-Out (LOSO)

Each station is completely excluded during training to evaluate generalization to unseen monitoring locations.

**Reported results:**

- Average LOSO R²: 0.8766
- Highest: RK Puram, Delhi (approximately 0.986)
- Lowest: Patancheruvu, Hyderabad (approximately -0.097)

## Key Findings

- Delhi has the highest reported average PM2.5 concentration, approximately 138 µg/m³.
- All evaluated cities exceed WHO safe limits at the assessed locations.
- Rush hour significantly increases PM2.5 levels.
- Seasonal variation shows improvement from winter to spring in most cities.
- Co-pollutants such as PM10, SO2, and CO are among the strongest predictors.

## Features of the System

### 1. Pollution Heatmaps
Visualize machine-learning-based spatial predictions across each city.

### 2. Health Risk Mapping
Classify locations according to PM2.5 health-risk thresholds.

### 3. Sensor Placement Recommendations
Recommend new monitoring locations using a priority score based on:

- Pollution severity: 60%
- Distance from existing sensors: 40%

### 4. Model Uncertainty Map
Visualize prediction uncertainty using variance across Random Forest trees.

### 5. Seasonal Comparison
Analyze variations in pollution between winter and spring.

### 6. What-If Simulator
Explore how changes in weather conditions may affect predicted pollution levels.

### 7. Multi-City Comparison
Compare pollution predictions across the five cities using a unified model.

## Technology Stack

- **Language:** Python 3
- **Machine learning:** Scikit-learn, XGBoost
- **Data processing:** Pandas, NumPy
- **Visualization:** Plotly, Matplotlib, Seaborn
- **Maps:** Folium, streamlit-folium
- **Web application:** Streamlit
- **Model storage:** Joblib

## Project Structure

```text
hyperlocal-aqi-prediction/
├── app.py
├── requirements.txt
├── README.md
├── AQIcollabfinal.ipynb
├── assets/
│   └── style.css
├── data/
│   ├── *.csv
│   ├── *.json
│   └── *.pkl
└── utils/
    ├── __init__.py
    ├── charts.py
    ├── maps.py
    └── predictions.py
```

## Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Riddhi0512/hyperlocal-aqi-prediction.git
cd hyperlocal-aqi-prediction
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

On macOS or Linux:

```bash
source venv/bin/activate
```

### 3. Install Dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Run the Application

```bash
streamlit run app.py
```

## Results Summary

- **Best model:** Random Forest
- **Reported R²:** 0.9873
- **Reported MAE:** 4.25 µg/m³
- **Cities covered:** 5
- **Monitoring stations:** 50
- **Dataset size:** Approximately 105,000 records

## Limitations

- PM2.5 data originally available at city level was expanded to station level using ratios.
- PM10 values for Chennai were estimated using a PM2.5 ratio.
- Weather variables were applied at city level rather than micro-climate level.
- The dataset is limited to January–March 2019.

## Future Improvements

- Integrate real-time air quality data.
- Improve spatial resolution using satellite data.
- Optimize model size for faster deployment.
- Compare performance with deep learning models.

## Authors

- **Riddhi Poddar**
- **Lakshmi Aneesha Ambati**

## License

This project is intended for academic and research purposes.
