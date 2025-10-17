# Cybersecurity Attack Prediction (Data Engineering Focus)

This repository implements a pipeline for predicting cybersecurity attacks from raw, “dirty” logs. It emphasizes end-to-end **data engineering**: ingestion, preprocessing, feature engineering, and deployment.

---

##  Project Structure
<pre>
.
├── Data Engineering.ipynb # Notebook: full data pipeline (cleaning, feature engineering)
├── Modelling.ipynb # Experiments with neural, tree, and ensemble models
├── preprocessing.py # Scripted preprocessing logic used in notebooks and app
├── app.py # Simple API / script to run predictions on new logs
├── cybersecurity_attacks.csv # Raw log data of attack events
├── Processed_Samples.csv # Features + labels prepared for modeling
├── best_nn_model.pth # Best neural network model
├── best_rf_model.pkl # Best random forest model
├── best_xgb_model.pkl # Best XGBoost model
├── pca.pkl # Saved PCA transformer for dimensionality reduction
├── predictions.csv # Resulting predictions on test dataset
├── nn_classification_report.txt # Classification report for neural network model
└── gpu_check.py # Utility to check GPU availability
  </pre>
---

##  Data Pipeline

1. **Ingestion & Exploration**  
   - Raw logs (e.g. `cybersecurity_attacks.csv`) are loaded and initially explored.  
   - Missing values, inconsistent types, and anomalies are handled.

2. **Preprocessing & Feature Engineering**  
   - Transform categorical fields, encode timestamps, scale/normalize features.  
   - Dimensionality reduction using PCA (`pca.pkl`) to reduce noise and overfitting.  
   - Save the resulting feature matrix and labels into `Processed_Samples.csv`.

3. **Model Training & Selection**  
   - Run multiple models (Neural Network, Random Forest, XGBoost) in `Modelling.ipynb`.  
   - Select best models and save their checkpoints/weights.

4. **Predictions & Deployment**  
   - `app.py` serves as an interface to load a chosen model and perform predictions on new data.  
   - Outputs are saved to `predictions.csv` for downstream evaluation.

5. **Evaluation & Reporting**  
   - Classification metrics (precision, recall, F1, etc.) are logged in `nn_classification_report.txt`.  
   - Visual and tabular results are reviewed to compare model performance.

---

##  Performance Summary

- The notebooks demonstrate comparative performance among model types.  
- The data pipeline is modular: preprocessing logic is shared across notebooks and deployment.  
- GPU support is detected via `gpu_check.py`, enabling faster model training where available.

---

##  Usage
1. Run data pipeline (in notebook or via script):
   `python preprocessing.py`.
2. Train an evaluate models via Modelling.ipynb.
3.  Use app.py to run predictions directly on logs files:
   `python app.py --input new_logs.csv --model best_xgb_model.pkl`.
---
## Caveats & Limitations

- Imbalanced or noisy logs may degrade predictive performance.
- PCA reduction is not sufficient to generate patterns from features engineered in the set.
