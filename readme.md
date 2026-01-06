#  Satellite-Driven Wildfire Impact Analysis

##  Project Overview
Wildfires pose serious environmental, economic, and social challenges. This project investigates whether **spatiotemporal metadata alone**—specifically *location* and *time of occurrence*—can be used to **predict the cause of wildfires** in the United States using machine learning.

The study applies a full end-to-end **data science pipeline** on a large-scale historical wildfire dataset and evaluates multiple advanced models to determine their effectiveness under real-world constraints.

 **Degree**: MSc Data Science  
 **Institution**: University of Hertfordshire  
 **Author**: Shashank Shivakoti  
 **Submission Date**: January 2026  

---

##  Objectives
- Analyze large-scale wildfire records using spatial and temporal data  
- Engineer meaningful geographic and time-based features  
- Address severe class imbalance in wildfire causes  
- Compare multiple ML models for multi-class classification  
- Evaluate feasibility and limitations of metadata-only prediction  

---

##  Research Questions
1. **Exploratory**: Do wildfire causes show distinct spatial or seasonal patterns?
2. **Feasibility**: Can wildfire causes be predicted using only time and location data?
3. **Methodological**: Does geo-clustering (K-Means) improve model performance?

---

##  Dataset
- **Source**: U.S. Forest Service – Fire Program Analysis Fire-Occurrence Database (FPA-FOD)
- **Size**: ~1.88 million wildfire records
- **Years Covered**: 1992–2015
- **Format**: SQLite
- **Target Variable**: `STAT_CAUSE_DESCR` (13 wildfire cause categories)

Key features include:
- Latitude & Longitude  
- Discovery date (Julian format)  
- State  
- Fire year  

📎 Dataset details and preprocessing steps are documented in the project report :contentReference[oaicite:0]{index=0}

---

##  Methodology

### 1. Data Ingestion
- Extracted data using **SQL queries** from SQLite database

### 2. Exploratory Data Analysis (EDA)
- Analyzed class imbalance
- Identified seasonal trends
- Visualized spatial and temporal distributions

### 3. Feature Engineering
- **Temporal Features**: Month, Day of Week, Day of Year, Season  
- **Spatial Features**:  
  - Applied **K-Means clustering (30 clusters)** on latitude & longitude  
  - Converted raw coordinates into regional “Geo-Clusters”

### 4. Handling Class Imbalance
- Used **SMOTE (Synthetic Minority Over-sampling Technique)**  
- Applied **only on training data** to prevent data leakage

---

##  Models Implemented

| Model      | Type              | Purpose |
|------------|-------------------|--------|
| TabNet     | Deep Learning     | Attention-based tabular modeling |
| LightGBM   | Gradient Boosting | Fast, high-accuracy baseline |
| XGBoost  | Gradient Boosting | Final selected model |

###  Hyperparameter Tuning
- Performed using **RandomizedSearchCV**
- Tuned learning rate, tree depth, number of estimators
- GPU acceleration used where available (CUDA)

---

##  Results Summary

| Model      | Test Accuracy | Strengths | Limitations |
|-----------|--------------|-----------|-------------|
| TabNet    | ~53% | Captures nonlinear interactions | High compute cost, unstable across classes |
| LightGBM  | ~59% | Fastest, highest raw accuracy | Biased toward majority classes |
| **XGBoost** | **~50%** | Best class-wise balance, robust | Slightly lower overall accuracy |

- **Random baseline accuracy**: ~7.7%
- **XGBoost** achieved:
  - Weighted F1 ≈ 0.52
  - Macro F1 ≈ 0.39
- Lightning-caused fires were **most predictable**
- Human-caused fires showed **high overlap and ambiguity**

---

##  Key Insights
- Wildfire causes are **not random**—clear spatial and seasonal patterns exist
- **Geo-clustering significantly improves spatial learning**
- Metadata-only models have **performance limits**
- Environmental variables (weather, vegetation, humidity) are likely required for higher accuracy

---

##  Ethical Considerations
- Dataset contains **no personal or sensitive data**
- Risk of **algorithmic bias** when associating geography with human-caused fires
- Model is intended as a **decision-support tool**, not a legal or investigative authority

---

##  Practical Applications
- Early-stage wildfire cause screening
- Resource prioritization for investigation teams
- Analytical dashboards for wildfire agencies

---

##  Technologies Used
- **Python**
- **SQLite**
- **Pandas, NumPy**
- **Scikit-learn**
- **XGBoost, LightGBM**
- **TabNet (PyTorch)**
- **SMOTE (imbalanced-learn)**
- **Matplotlib, Seaborn**



