# ⚡ Household Energy Consumption Forecasting using LSTM

## 📌 Project Overview

This project develops a deep learning-based time series forecasting pipeline to predict the **next-hour household energy consumption** using an **LSTM (Long Short-Term Memory)** neural network.

The complete workflow includes data preprocessing, exploratory data analysis (EDA), feature engineering, sequence generation, model training, evaluation, and prediction. The entire implementation is contained in a single Jupyter Notebook (`forecasting_pipeline.ipynb`) for easy reproducibility.

---

# 📂 Dataset

**Dataset:** Individual Household Electric Power Consumption Dataset

This dataset contains minute-level measurements of household electric power consumption collected over several years.

The dataset is **not included** in this repository because it exceeds GitHub's recommended file size limits.

Please download the dataset from the official UCI Machine Learning Repository:

https://archive.ics.uci.edu/dataset/235/individual+household+electric+power+consumption

### Download Instructions

1. Visit the dataset page using the link above.
2. Download the dataset files.
3. Extract the downloaded archive.
4. Copy the file:


### Features

- Global Active Power
- Global Reactive Power
- Voltage
- Global Intensity
- Sub Metering 1
- Sub Metering 2
- Sub Metering 3
- Date
- Time

After preprocessing, the minute-level observations were resampled into hourly averages for forecasting.

---

# 🎯 Project Objective

The objective of this project is to forecast the household's **next-hour Global Active Power consumption** using historical electricity usage patterns.

The project demonstrates an end-to-end machine learning workflow including:

- Data preprocessing
- Feature engineering
- Time series sequence generation
- LSTM model development
- Model evaluation
- Model persistence

---

# 🛠 Data Preprocessing

The following preprocessing steps were performed:

- Loaded raw household power consumption dataset
- Converted Date and Time into a unified datetime index
- Handled missing values using time-based interpolation
- Resampled minute-level data into hourly averages
- Removed invalid observations generated during feature engineering

---

# 📊 Exploratory Data Analysis (EDA)

Several analyses were performed to understand consumption behavior:

- Hourly energy consumption profile
- Weekly consumption pattern
- Monthly consumption pattern
- Seasonality analysis
- Autocorrelation (ACF) analysis
- Distribution of Global Active Power

These analyses helped identify daily and weekly seasonal trends.

---

# ⚙ Feature Engineering

The following features were created to improve forecasting performance.

## Time Features

- Hour
- Day_of_Week
- Month
- Is_Weekend

## Lag Features

- Lag_1
- Lag_24
- Lag_168

## Rolling Statistics

- Rolling_Mean_24
- Rolling_Std_24

---

# 🔄 Data Preparation

The processed dataset was split chronologically:

- Training Data: 80%
- Testing Data: 20%

Scaling was performed using **MinMaxScaler**.

Separate scalers were used for:

- Input Features
- Target Variable

Time-series sequences were then created using a sliding window approach.

**Sequence Length:** 24 hours

Each input sequence contains the previous 24 hourly observations used to predict the next hour.

---

# 🧠 Model Architecture

The forecasting model is based on a Long Short-Term Memory (LSTM) neural network.

Architecture:

```
Input Sequence (24 × Features)
        │
        ▼
LSTM Layer (64 Units)
        │
        ▼
Dropout (20%)
        │
        ▼
Dense Layer (1 Output)
```

### Why LSTM?

Traditional machine learning models cannot effectively capture long-term temporal dependencies in sequential data.

LSTM networks are specifically designed for time series forecasting because they:

- Learn temporal dependencies
- Preserve long-term information
- Handle sequential patterns efficiently
- Perform well on energy demand forecasting tasks

---

# 📈 Model Evaluation

The trained model was evaluated using standard regression metrics.

| Metric | Score |
|---------|-------|
| MAE | **0.3127** |
| RMSE | **0.4589** |
| MAPE | **0.4058** |

---

# 💾 Model Persistence

The trained model and preprocessing objects were saved for future inference.

Saved artifacts include:

- `energy_forecasting_lstm.keras`
- `feature_scaler.pkl`
- `target_scaler.pkl`

---

# 🐳 Running the Project with Docker

## Build Docker Image

```bash
docker build -t forecast-energy-lstm .
```

## Run Docker Container

```bash
docker run -p 8888:8888 forecast-energy-lstm
```

After the container starts, open Jupyter Notebook and execute:

```
forecasting_pipeline.ipynb
```

---

# 📁 Project Structure

```
forecast-energy/
│
├── data/
│   └── household_power_consumption.txt
│
├── models/
│   ├── energy_forecasting_lstm.keras
│   ├── feature_scaler.pkl
│   └── target_scaler.pkl
│
├── notebooks/
│   └── forecasting_pipeline.ipynb
│
├── Dockerfile
├── requirements.txt
└── README.md
```

---

# 🚀 Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- TensorFlow / Keras
- Joblib
- Jupyter Notebook
- Docker

---

# 📌 Results

The LSTM model successfully learned temporal patterns from historical household electricity consumption and produced reliable next-hour forecasts.

The combination of temporal features, lag features, rolling statistics, and sequence-based learning enabled the model to capture daily consumption trends effectively.

---

# 📚 Future Improvements

Possible future enhancements include:

- Multi-step forecasting (24-hour prediction)
- Hyperparameter tuning
- Bidirectional LSTM
- GRU-based forecasting
- Attention-based sequence models
- Deployment using FastAPI
- Interactive Streamlit dashboard

---

# 👨‍💻 Author

**Pavan Teja**

Data Science Student

Machine Learning & AI Enthusiast