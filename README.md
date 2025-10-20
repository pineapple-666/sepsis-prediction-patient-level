# Sepsis Prediction Project (PhysioNet 2019)

## 🧠 Project Overview
This project explores patient data from the PhysioNet Challenge 2019 to predict whether a patient **ever develops sepsis** during their ICU stay.  
We use the `train.csv` dataset, where each row represents a **patient at a specific time**. For this project, we **aggregate data to the patient level**, so that each patient has one observation:
- `SepsisLabel = 1` if the patient ever had sepsis  
- `SepsisLabel = 0` otherwise  

The goal is to perform **Exploratory Data Analysis (EDA)** and prepare data for further modeling.

---

## 📂 Data Description
### Data Source
[PhysioNet Sepsis Prediction Challenge 2019](https://physionet.org/content/challenge-2019/1.0.0/)

### Data Categories
- **Vital Signs (8 features):** HR, O2Sat, Temp, SBP, MAP, DBP, Resp, EtCO2  
- **Laboratory Values (26 features):** BaseExcess, HCO3, FiO2, pH, PaCO2, etc.  
- **Demographics (6 features):** Age, Gender, Unit1, Unit2, HospAdmTime, ICULOS  
- **Outcome (1 feature):** SepsisLabel  

---

## ⚙️ Workflow
### 1. Data Loading
Load the provided `train.csv` file and inspect its structure.  
Each patient’s data includes multiple time points (ICU hours).

### 2. Data Transformation
Aggregate the data to create one record per patient:
- `PatientID` is the unique identifier.
- `SepsisLabel` = 1 if the patient ever had sepsis, otherwise 0.
- Aggregate continuous variables (e.g., mean, median, last recorded value).

### 3. Data Cleaning
- Handle missing values (e.g., mean/median imputation).
- Drop features with excessive missingness.
- Convert categorical variables (e.g., Gender, Unit1, Unit2) into numeric.

### 4. Exploratory Data Analysis
- Visualize variable distributions (histograms, boxplots).
- Explore correlations between variables and SepsisLabel.
- Summarize insights in tables and charts.

### 5. Output
Produce:
- Cleaned aggregated dataset (`clean_train_patient.csv`)
- Summary statistics table
- Visual EDA outputs

---

## 💻 Environment Setup
You can run this project in **VS Code** using **Jupyter Notebook**.

### Installation
Clone the repository and install dependencies:
```bash
git clone https://github.com/<your-username>/sepsis-prediction-patient.git
cd sepsis-prediction-patient
pip install -r requirements.txt
