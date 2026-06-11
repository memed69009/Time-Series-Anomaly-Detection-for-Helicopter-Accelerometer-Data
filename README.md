
# 🚁 Time Series Anomaly Detection for Helicopter Accelerometer Data

## 📌 Project Overview

This project implements an unsupervised anomaly detection pipeline for helicopter accelerometer time series data in an industrial context (Airbus Helicopters use case).

The objective is to automatically detect abnormal sensor behavior in flight-test data, reducing the need for manual inspection.

---

## 📊 Dataset

* **Training set**: 1677 sequences (normal data only)
* **Validation set**: 594 sequences (unknown distribution of anomalies)
* Each sequence:

  * 1 minute duration
  * Sampling frequency: 1024 Hz
  * 61,440 time steps per signal

---

## ⚙️ Methodology

### 1. Feature Engineering

Extraction of time-domain features:

* Min / Max
* Mean
* Variance
* RMS
* Kurtosis
* Skewness
* Crest Factor (CF)
* Shape Factor (SF)

### 2. Feature Selection

* Correlation matrix used to remove redundant features

### 3. Model

* **Local Outlier Factor (LOF)** (unsupervised)
* Trained only on normal data
* Threshold defined from training distribution

### 4. Optimization

* **Feature Bagging** to improve robustness
* Best parameters selected empirically

---

## 📈 Final Results

### Confusion Matrix

```
[[252   0]
 [ 69 160]]
```

### Metrics

* **Accuracy**: 0.86
* **Precision (Anomaly)**: 1.00
* **Recall (Anomaly)**: 0.70
* **F1-score**: ~0.85
* **False Positive Rate**: 0.00

---

## Interpretation

* ✅ **No false positives** → critical for industrial use (no unnecessary inspections)
* ⚠️ Some anomalies are missed → model is conservative
* 🎯 Strong balance between reliability and detection capability

This behavior is **intentional and desirable** in an industrial context where false alarms are costly.

---

## 🚀 Key Takeaways

* Time-domain features are effective for vibration anomaly detection
* LOF performs well in fully unsupervised settings
* Feature Bagging significantly improves robustness
* The model is suitable for **real-world sensor validation pipelines**

---

## 🔮 Possible Improvements

* Threshold tuning to improve recall
* Comparison with:

  * Isolation Forest
  * One-Class SVM
* Use of frequency-domain features (FFT)

---

## 📌 Conclusion

This project demonstrates that an unsupervised learning approach can effectively detect anomalies in complex industrial time series while maintaining a **very low false positive rate**, making it highly relevant for aerospace applications.
