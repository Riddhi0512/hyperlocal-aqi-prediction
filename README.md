# Hyper-Local Air Quality Prediction for Urban Areas
[Open Notebook in Google Colab](https://colab.research.google.com/drive/1NjeJZjhBmTSe8ua1T9bdQxUfgyEX-sSX?usp=sharing)
## Overview

This project develops a machine learning system to predict PM2.5 concentrations at a hyper-local level across major Indian cities.
Due to sparse placement of CPCB monitoring stations (typically one per 50–100 sq. km), large urban regions remain unmonitored.
The system uses real air quality data, weather variables, and spatial features to estimate pollution levels at any location.

The final output is an interactive Streamlit dashboard for exploring pollution patterns, health risks, and sensor placement recommendations.

---

## Problem Statement

Air quality monitoring infrastructure in Indian cities is insufficient for street-level insights.
This project addresses the gap by building a predictive system that generalizes to unseen locations using machine learning.

---

## Dataset

* Source: CPCB air quality data via Kaggle (rohanrao dataset)
* Weather: Open-Meteo historical API
* Cities: Delhi, Chennai, Bengaluru, Hyderabad, Jaipur
* Time Period: January – March 2019
* Stations: 50 (10 per city)
* Total Records: ~105,000 hourly observations

### Features Used

* Spatial: latitude, longitude, road density
* Weather: temperature, humidity, wind speed, wind direction
* Pollutants: NO2, SO2, CO, PM10
* Time: hour of day, day of year
* City: encoded identifier

Target Variable: PM2.5 (µg/m³)

---

## Machine Learning Models

The following models were trained and compared:

* Linear Regression
* Ridge Regression
* Support Vector Regression (RBF Kernel)
* Random Forest
* XGBoost
* IDW (spatial baseline)
* KMeans (clustering for zone detection)

### Best Model

Random Forest achieved the best performance:

* R²: 0.9873
* MAE: 4.25 µg/m³
* RMSE: 6.69 µg/m³

---

## Model Evaluation

Two evaluation strategies were used:

### Standard Train-Test Split

* 80/20 split across all cities
* Used MAE, RMSE, and R²

### Leave-One-Station-Out (LOSO)

* Each station is completely excluded during training
* Tests real-world generalization to unseen locations

Results:

* Average LOSO R²: 0.8766
* Highest: RK Puram, Delhi (~0.986)
* Lowest: Patancheruvu, Hyderabad (~-0.097)

---

## Key Findings

* Delhi is the most polluted city (average ~138 µg/m³)
* All cities exceed WHO safe limits at all locations
* Rush hour significantly increases PM2.5 levels
* Strong seasonal variation (winter to spring improvement in most cities)
* Co-pollutants (PM10, SO2, CO) are the strongest predictors

---

## Features of the System

### 1. Pollution Heatmaps

Machine learning–based spatial prediction across each city.

### 2. Health Risk Mapping

Classification of regions based on WHO air quality thresholds.

### 3. Sensor Placement Recommendation

Suggests optimal new monitoring locations using:

* Pollution severity (60%)
* Distance from existing sensors (40%)

### 4. Model Uncertainty Map

Displays confidence based on variance across Random Forest trees.

### 5. Seasonal Comparison

Analyzes variation between winter and spring pollution levels.

### 6. What-If Simulator

Interactive tool to explore how weather conditions affect pollution.

### 7. Multi-City Comparison

Unified model enabling cross-city pollution analysis.

---

## Technology Stack

* Language: Python 3
* Machine Learning: Scikit-learn, XGBoost
* Data Processing: Pandas, NumPy
* Visualization: Plotly, Matplotlib, Seaborn
* Maps: Folium, streamlit-folium
* Web App: Streamlit
* Model Storage: Joblib

---

## Project Structure

```
├── data/
│   ├── *.csv
│   ├── *.pkl
├── app.py
├── requirements.txt
├── README.md
```

---

## Installation and Setup

### 1. Clone the repository

```
git clone https://github.com/your-username/hyperlocal-aqi-prediction.git
cd hyperlocal-aqi-prediction
```

### 2. Create virtual environment

```
python -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```
pip install -r requirements.txt
```

### 4. Run the application

```
streamlit run app.py
```

---

## Results Summary

* Best Model: Random Forest
* R² Score: 0.9873
* MAE: 4.25 µg/m³
* Cities Covered: 5
* Stations: 50
* Dataset Size: ~105,000 rows

---

## Limitations

* PM2.5 data originally available at city level, expanded to station level using ratios
* PM10 for Chennai estimated using PM2.5 ratio
* Weather applied at city level (not micro-climate level)
* Dataset limited to 2019

---

## Future Improvements

* Use real-time data integration
* Increase spatial resolution with satellite data
* Optimize model size for faster deployment
* Add deep learning models for comparison

---

## Author

Mihika

---

## License

This project is for academic and research purposes.
