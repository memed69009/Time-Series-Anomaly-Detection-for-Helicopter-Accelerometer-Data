# Time Series Anomaly Detection for Helicopter Sensor Data

## Overview

This project focuses on detecting anomalies in helicopter accelerometer time series using unsupervised machine learning.

The goal is to automate the validation of flight-test sensor data by identifying abnormal vibration patterns in accelerometer signals.

## Business Context

Flight tests generate large volumes of sensor data. Manual validation is time-consuming and difficult to scale.

Anomaly detection can help engineering teams identify abnormal sensors or signals earlier and reduce manual inspection effort.

## Dataset

The project uses helicopter accelerometer time series data from an Airbus AI Gym challenge.

The data includes:

- **Training set**: 1,677 normal one-minute sequences
- **Validation set**: 594 one-minute sequences
- **Sampling frequency**: 1,024 Hz
- **Time steps per sequence**: 61,440
- **Ground truth**: anomaly labels for validation sequences

## Methodology

The project follows this workflow:

1. Data loading from HDF5 files
2. Data cleaning
   - duplicate removal
   - missing value checks
   - low-variance sensor removal
3. Time series visualization
4. Feature engineering in the time domain
5. Feature selection based on correlation
6. Anomaly detection with Local Outlier Factor
7. Hyperparameter tuning with feature bagging
8. Evaluation against ground truth labels

## Feature Engineering

Extracted statistical and signal-based features include:

- minimum
- maximum
- mean
- variance
- RMS
- kurtosis
- skewness
- crest factor
- impulse factor
- shape factor
- clearance factor

## Model

The final approach uses:

- Local Outlier Factor (LOF)
- Feature Bagging
- thresholding based on training-set anomaly scores

The selected parameters are:

- `n_neighbors = 3`
- `n_estimators = 250`

## Results

The final model achieves:

- **Weighted F1-score: ~90%**
- **False Positive Rate: ~0.4%**

This is important in a flight-test context, where false alarms should be minimized.

## Key Insights

- Time-domain statistical features are effective for detecting abnormal vibration behavior.
- LOF is well-suited to this use case because training data contains only normal sequences.
- Feature bagging improves robustness by combining multiple LOF estimators.
- The low false positive rate makes the approach relevant for operational anomaly detection.

## Repository Structure

```text
.
├── data/
│   └── README.md
├── notebooks/
│   └── helicopter_anomaly_detection.ipynb
├── reports/
│   └── anomaly_detection_report.pdf
├── images/
│   ├── time_series_examples.png
│   ├── correlation_matrix.png
│   ├── lof_scores.png
│   └── confusion_matrix.png
├── requirements.txt
├── .gitignore
└── README.md
```

## Tech Stack

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- PyOD
- h5py

## How to Run

Install dependencies:

```bash
pip install -r requirements.txt
```

Open the notebook:

```bash
jupyter notebook notebooks/helicopter_anomaly_detection.ipynb
```

> Note: the raw data files are not included in this repository if they are too large or subject to sharing restrictions.

## Future Improvements

- Convert the notebook into a reusable Python pipeline
- Add automated tests for feature extraction
- Compare LOF with Isolation Forest and One-Class SVM
- Evaluate model stability with cross-validation or bootstrapping
- Add a Streamlit dashboard for anomaly score exploration

## Author

Mohammed Mokeddem
