# Climate Data Forecasting with LSTM

## 📌 Project Overview

This project applies **Long Short-Term Memory (LSTM)** neural networks to forecast **temperature** and **pressure** using historical climate data. The dataset comes from the Jena Climate dataset, which contains 7 years of meteorological data (2009–2016).

The pipeline involves:

1. Data Collection & Preprocessing
2. Feature Engineering
3. Train-Test Split
4. Data Standardization
5. LSTM Model Building
6. Training & Evaluation

---

## 📂 Dataset

* **Source**: Jena Climate dataset (2009–2016)
* **Original Size**: ~420,551 rows × 15 columns
* **Processed Size**: ~70,091 rows × 15 columns (after sampling hourly data)

### Key Features

* `T (degC)` → Temperature in Celsius 🌡️
* `p (mbar)` → Pressure in millibar 🌬️
* `Date Time` → Timestamp for each measurement ⏳
* Other meteorological parameters like humidity, dew point, wind velocity, etc.

---

## 🔄 Data Preprocessing

1. **Resampling**: Used only hourly data (`climate_data = climate_data[5::6]`).
2. **Datetime Indexing**: Converted `Date Time` into pandas `datetime` format.
3. **Feature Engineering**:

   * Created **sin** and **cos** transformations for daily and yearly cycles (`Day sin`, `Day cos`, `Year sin`, `Year cos`).
   * Dropped unnecessary columns like `Seconds`.

---

## 📊 Visualization

Time series plots were created for temperature and pressure to analyze seasonal and daily variations.

---

## 🛠️ Feature and Target Preparation

* Defined a function `df_to_X_Y` to generate **input sequences** (7-day windows) and **targets** (temperature and pressure of the next step).
* Shapes:

  * `X`: (70,084, 7, 6)
  * `Y`: (70,084, 2)

---

## ✂️ Train-Test Split

* Training: 60,000 samples
* Validation: 5,000 samples
* Testing: 5,084 samples

---

## ⚖️ Data Standardization

* Normalized **pressure** and **temperature** using training mean and standard deviation.
* Applied same normalization to outputs (`Y_train`, `Y_val`, `Y_test`).

---

## 🤖 Model Architecture (LSTM)

```text
Input Shape: (7, 6)

LSTM Layer: 64 units
Dense Layer: 8 (ReLU)
Output Layer: 2 (Linear, for temperature & pressure)

Total Parameters: 18,714
```

---

## 🏋️ Training

* **Optimizer**: Adam (lr=0.0001)
* **Loss Function**: Mean Squared Error (MSE)
* **Metric**: Root Mean Squared Error (RMSE)
* **Epochs**: 10
* **Callbacks**: ModelCheckpoint (to save best model)

### Training Performance (Sample)

* Epoch 1: RMSE ≈ 72.57 → Val RMSE ≈ 60.07
* Epoch 3: RMSE ≈ 20.59 → Val RMSE ≈ 8.48
* Epoch 4: RMSE ≈ 3.64 → Val RMSE ≈ 1.06 ✅

---

## ✅ Results

The LSTM model achieved strong forecasting performance:

* Rapid loss reduction after a few epochs.
* Validation RMSE decreased significantly, showing the model captured both **daily** and **seasonal trends** effectively.

---

## 🚀 Future Improvements

* Train longer with **early stopping** for optimal performance.
* Include additional meteorological features for multi-variate forecasting.
* Compare with **GRU** and **1D CNN** models.

---

## 📜 License

This project is open-source and available for educational purposes.
