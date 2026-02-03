# Sepsis Prediction Project (PhysioNet 2019)  
**Course:** ADEC/ADAN 7430 Midterm Project  
**Project Goal:** Early detection of sepsis — detect whether and when a patient develops sepsis using the PhysioNet 2019 dataset.

---

## Project Overview
![image alt](https://github.com/pineapple-666/Detect-Sepsis-in-Patients-Before-it-Emerges/blob/b6f04d414459526e4b8bf5c4d2dee1739380c61d/Slide2.PNG)

This project uses data from the **PhysioNet Computing in Cardiology Challenge 2019** to build classifiers that detect sepsis. The assignment has two problem formulations; for this midterm you will:

- **Primary objective:** Predict whether and when a patient develops sepsis.
- **Chosen approach for this submission:** *Patient-level classification* (each patient aggregated to one observation; `SepsisLabel = 1` if the patient ever had sepsis, otherwise 0).  
  *You may extend to patient-time modeling later if time permits.*

Link to dataset: https://physionet.org/content/challenge-2019/1.0.0/

---

## Data Description
- **Source file:** `train.csv` (hourly records per patient; located in `data/raw/` locally).
- **Unique identifier (original):** `PatientID` + `Hour` (patient-time).
- **Target (hour-level):** `SepsisLabel` (1 if t ≥ tsepsis−6 for sepsis patients; 0 otherwise).
- **Target (patient-level):** aggregated `SepsisLabel_patient = max(SepsisLabel over patient hours)`.

**Feature groups**
- Vital signs (8): HR, O2Sat, Temp, SBP, MAP, DBP, Resp, EtCO2  
- Laboratory values (26): BaseExcess, HCO3, FiO2, pH, PaCO2, SaO2, AST, BUN, … Platelets  
- Demographics (6): Age, Gender, Unit1, Unit2, HospAdmTime, ICULOS

---

## Required Steps (as per midterm)
### Step 1 — Exploratory Data Analysis (EDA)
1. Load `data/raw/train.csv` (local copy).
2. Explore variable meaning and distributions (vitals, labs, demographics).
3. Handle missing data and produce a clean, aggregated patient-level dataset (`data/processed/patient_level.csv`).
4. Create training/validation (~80%) and test (~20%) splits — **split by patient ID** (no leakage).
   - Use **stratified splitting** to preserve target class ratio.
   - Apply **SMOTE** only on the training split (after split) if needed — do **not** use SMOTE before splitting.
5. Produce a nicely formatted summary statistics table of the final clean data and provide insights.
![image alt](https://github.com/pineapple-666/Detect-Sepsis-in-Patients-Before-it-Emerges/blob/b6f04d414459526e4b8bf5c4d2dee1739380c61d/Slide6.PNG)
![image alt](https://github.com/pineapple-666/Detect-Sepsis-in-Patients-Before-it-Emerges/blob/b6f04d414459526e4b8bf5c4d2dee1739380c61d/Slide8.PNG)
![image alt](https://github.com/pineapple-666/Detect-Sepsis-in-Patients-Before-it-Emerges/blob/b6f04d414459526e4b8bf5c4d2dee1739380c61d/Slide11.PNG)
![image alt](https://github.com/pineapple-666/Detect-Sepsis-in-Patients-Before-it-Emerges/blob/b6f04d414459526e4b8bf5c4d2dee1739380c61d/Slide13.PNG)

### Step 2 — Model building
Train the following classifiers using the training data (with cross-validation):
- **Baseline:** Logistic Regression (with feature selection / regularization — Lasso or Ridge)
- **LDA**, **QDA**
- **Naïve Bayes**
- **K-Nearest Neighbors (KNN)**

Guidance:
- Use 10-fold cross validation (or 5-fold if compute-limited).
- Experiment with full feature set and with a smaller selected set.
- Comment on multicollinearity, feature selection, and how you chose features for each model.

### Step 3 — Model evaluation
Evaluate classifiers using appropriate metrics for imbalanced data:
- Confusion matrix
- Precision, recall, F1-score (focus on F1)
- ROC AUC and Precision-Recall curves
- Explain why one model works better/worse than others
![image alt](https://github.com/pineapple-666/Detect-Sepsis-in-Patients-Before-it-Emerges/blob/b6f04d414459526e4b8bf5c4d2dee1739380c61d/Slide20.PNG)
### Step 4 — Test and reporting
1. Select the best model based on validation metrics.
2. Retrain the selected model on the full training+validation data (no test leakage).
3. Evaluate and report performance on held-out test data.
4. Submit:
   - Jupyter notebook (`.ipynb`) with numbered code cells that run top-to-bottom
   - A concise report (Markdown or PDF) with introduction, methods, results, conclusion, and full names
   - Cleaned processed dataset (if small) or instructions to reproduce it

---

## Deliverables (per rubric)
- EDA and feature understanding
- Missing data handling and transformation
- Train/test split with class balance
- Implementation of Logit (baseline), LDA, QDA, Naïve Bayes, KNN with CV
- Performance comparison and selection of best model
- Final predictions on test set
- Well-written report and runnable notebook

---

## How to run (local environment / VS Code + Jupyter)
1. Clone repository:
```bash
git clone https://github.com/<your-username>/sepsis-prediction-patient.git
cd sepsis-prediction-patient
