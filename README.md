# Predictive Maintenance RUL Estimation

This repository implements a predictive maintenance pipeline for estimating Remaining Useful Life (RUL) of aircraft engines using the NASA C-MAPSS FD001 dataset. It includes data ingestion, exploratory data analysis (EDA), feature engineering, baseline modeling with Random Forest and XGBoost, and evaluation on a held-out test set.

---

## 📂 Dataset

    NASA Turbofan Jet Engine Data Set: FD001 

All files follow the format:

```
unit, time, op_set_1, op_set_2, op_set_3, s1, s2, ..., s21
```

Download and place these files in the project root or the `data/` folder.

---

---

## 📑 Project Structure

```
├── data/                      # Optional data directory
│   ├── train_FD001.txt
│   ├── test_FD001.txt
│   └── RUL_FD001.txt
├── notebooks/
│   ├── 001_data_inspection&train_model.ipynb
├── requirements.txt
└── README.md
```

---

## 🚀 Usage

1. **Data Inspection & EDA**

   ```bash
   jupyter notebook notebooks/01_data_inspection.ipynb
   ```
2. **Feature Engineering**

   ```bash
   jupyter notebook notebooks/02_feature_engineering.ipynb
   ```
3. **Model Training & Evaluation**

   ```bash
   jupyter notebook notebooks/03_modeling.ipynb
   ```

Each notebook is self-contained, with code cells and explanations.

---

## 🔧 Key Steps

1. **Compute RUL** for training set:

   ```python
   train_df['RUL'] = train_df.groupby('unit')['time'].transform('max') - train_df['time']
   ```
2. **Feature Engineering**: rolling mean, std, and slope over a 20-cycle window for sensors `s3, s4, s7, s9, s17`.
3. **Baseline Models**:

   * Random Forest: RMSE ≈ 34.24 on validation, 33.41 on test
   * XGBoost: comparable performance, tuneable hyperparameters

---

## 📈 Results

| Model         | Validation RMSE | Test RMSE |
| ------------- | --------------- | --------- |
| Random Forest | 34.24 cycles    | 33.41     |
| XGBoost       | 32    cycles    | 32        |
