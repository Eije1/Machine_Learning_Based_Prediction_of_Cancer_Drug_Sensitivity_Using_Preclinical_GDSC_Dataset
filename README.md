# Machine Learning-Based Prediction of Cancer Drug Sensitivity Using Preclinical GDSC Dataset

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.0%2B-orange)
![Pandas](https://img.shields.io/badge/pandas-1.3%2B-green)
![Genomics](https://img.shields.io/badge/Genomics-Pharmacogenomics-ff69b4)
![Google Colab](https://img.shields.io/badge/Colab-F9AB00?style=flat&logo=googlecolab&color=525252)
![License](https://img.shields.io/badge/license-Apache%202.0-blue)
![Status](https://img.shields.io/badge/status-Completed-success)

### Researcher

**EIJE, OLOCHE CELESTINE**


---

## Project Overview

Cancer remains one of the leading causes of death worldwide, with patient responses to drug therapy varying dramatically based on tumor type, genetic background, and molecular pathways. The ability to predict drug sensitivity before treatment could revolutionize personalized oncology, enabling clinicians to select the most effective drugs while avoiding ineffective and toxic therapies. The **Genomics of Drug Sensitivity in Cancer (GDSC)** project provides a comprehensive resource of drug screening data across hundreds of cancer cell lines, offering a unique opportunity to build computational models that connect tumor features with therapeutic response.

### Dataset Description and Importance

The GDSC dataset contains drug sensitivity measurements across multiple cancer types, with features spanning biological information (cancer type, drug name), experimental conditions (drug concentrations), and pathway annotations.

| Attribute of the Dataset | Corresponding Values |
|--------------|-------------|
| **Total Samples** | 240,969 patient samples |
| **Features** | 5 predictive features (cancer_type, drug_name, pathway, min_conc, max_conc) |
| **Target** | ln_IC50 (log-transformed drug sensitivity) |
| **Data Type** | Pharmacogenomic screening data |

### Dataset Statistics

| Feature Category | Features |
|------------------|----------|
| **Biological** | cancer_type, drug_name |
| **Experimental** | min_conc, max_conc |
| **Pathway** | pathway |
| **Target** | ln_IC50 |

### Class Distribution

| Cancer Type | Sample Count |
|------------------|-------------------|
| UNCLASSIFIED | 45,691 |
| LUAD (Lung Adenocarcinoma) | 15,653 |
| SCLC (Small Cell Lung Cancer) | 13,570 |
| BRCA (Breast Cancer) | 13,106 |
| SKCM (Skin Melanoma) | 12,637 |
| COREAD (Colorectal) | 12,538 |
| **Total** | **240,969** |

---

## Aims and Objectives

- **Analyze Drug Sensitivity Patterns:** Investigate how different cancer types and drugs influence IC50 values and identify underlying trends in therapeutic response
- **Supervised Learning:** Develop and compare multiple regression models (Linear Regression, Random Forest, Gradient Boosting) capable of accurately predicting ln_IC50 values
- **Feature Importance Analysis:** Identify which biological and experimental features contribute most significantly to drug sensitivity predictions
- **Therapeutic Insights:** Evaluate whether these predictive patterns can provide insights into drug resistance mechanisms and support precision oncology approaches
- **Model Optimization:** Address the challenges of heterogeneous data types and feature interactions to build robust and generalizable prediction models

---

## Methodology

### Data Preprocessing
We imported the GDSC dataset via Google Colab, removed non-informative columns, and encoded categorical variables including cancer type, drug name, and pathway information using LabelEncoder. We audited the data for consistency and missing values. The target variable, ln_IC50, was retained as a continuous measure of drug sensitivity.

### Exploratory Data Analysis (EDA)
We performed distribution analysis using `df.info()` and `df.describe()` to understand drug sensitivity patterns across different cancer types and drugs. Data visualization was conducted using Matplotlib and Seaborn to identify trends in IC50 values, feature correlations, and the distribution of cancer types and drugs in the dataset.

### Feature Organization
We grouped features into three categories for interpretability:
- **Biological features:** cancer_type, drug_name
- **Experimental features:** min_conc, max_conc
- **Pathway features:** pathway

### Machine Learning Models
We developed three regression models to predict ln_IC50 values:
- **Linear Regression:** Served as our baseline model
- **Gradient Boosting Regressor:** For sequential learning
- **Random Forest Regressor:** For ensemble-based prediction

### Model Evaluation
Performance was measured using:
- **R² Score:** Proportion of variance explained by the model
- **Mean Absolute Error (MAE):** Average prediction error
- **Root Mean Square Error (RMSE):** Penalizes larger errors
- **Accuracy within tolerance:** Predictions within ±1.0 ln_IC50 units

---

## Results and Conclusion

### Model Performance Evolution

| Phase | Model | R² Score | MAE | RMSE | Correct Predictions |
|-------|-------|----------|-----|------|---------------------|
| **1. Baseline** | Linear Regression | 0.070 | 2.047 | 2.669 | 31.7% |
| **2. Non-Linear** | Gradient Boosting | 0.564 | 1.441 | 1.827 | 41.6% |
| **3. Final Model** | Random Forest | **0.769** | **0.994** | **1.331** | **61.2%** |

### Key Findings

**Random Forest emerged as the optimal model**, achieving an R² of 0.769 (explaining 77% of variance), MAE of 0.994, and RMSE of 1.331. It correctly predicted **61.2% of test samples** within ±1.0 ln_IC50 units, misclassifying only 38.8% compared to Gradient Boosting (58.4%) and Linear Regression (68.3%).

### Feature Importance Ranking

| Rank | Feature | Importance | Category |
|------|---------|------------|----------|
| 1 | min_conc | 38.4% | Experimental |
| 2 | drug_name | 23.2% | Biological |
| 3 | max_conc | 16.1% | Experimental |
| 4 | pathway | 13.0% | Pathway |
| 5 | cancer_type | 9.3% | Biological |

### Feature Group Breakdown

| Feature Group | Components | Total Importance |
|--------------|------------|------------------|
| **Experimental Features** | min_conc, max_conc | 54.5% |
| **Biological Features** | drug_name, cancer_type | 32.5% |
| **Pathway Features** | pathway | 13.0% |

### Biological Interpretation

- **Drug Identity Dominance:** The specific compound is the strongest single predictor (23.2%), confirming that drug mechanism and pharmacology are primary drivers of sensitivity
- **Cancer Type Specificity:** Cancer type contributes 9.3% to predictions, with striking differences observed—Dactinomycin showed highly sensitive response in CLL (-6.30) vs. moderately sensitive in LUAD (-3.06)
- **Pathway Importance:** Biological mechanism contributes 13.0%, indicating that drugs targeting similar pathways share sensitivity patterns
- **Experimental Conditions:** Concentration ranges collectively contribute 54.5%, highlighting the critical role of dose-response relationships

---

## Conclusion

This study demonstrates that machine learning, particularly **Random Forest regression**, can effectively predict cancer drug sensitivity using the GDSC dataset. By explaining approximately **77% of the variance** in drug response and correctly predicting within therapeutic range for **61.2% of samples**, our approach shows strong potential for precision oncology applications.

The feature importance analysis revealed that experimental conditions (54.5%) dominate predictions, while biological features (32.5%) and pathway information (13.0%) provide essential context. The striking differences in drug sensitivity across cancer types—exemplified by Dactinomycin's potency in CLL (-6.30) versus LUAD (-3.06)—confirm that **personalized medicine must consider both the patient's tumor type and the specific drug being administered**.

Our findings can help **prioritize drug candidates**, **reduce experimental screening costs**, and ultimately **support personalized treatment decisions** by identifying which patients are most likely to benefit from specific therapies.

---

## License

- This project is licensed under the MIT License 2.0


---

## Acknowledgments

- GDSC Project for providing the pharmacogenomic dataset
- Scikit-learn team for developing machine learning libraries

---

## References

- Yang, W., et al. (2013). Genomics of Drug Sensitivity in Cancer (GDSC): a resource for therapeutic biomarker discovery in cancer cells. *Nucleic Acids Research*, 41(D1), D955-D961.
- Iorio, F., et al. (2016). A landscape of pharmacogenomic interactions in cancer. *Cell*, 166(3), 740-754.
- Costello, J. C., et al. (2014). A community effort to assess and improve drug sensitivity prediction algorithms. *Nature Biotechnology*, 32(12), 1202-1212.
- Geeleher, P., et al. (2014). Discovering novel pharmacogenomic biomarkers by imputing drug response in cancer patients from large genomics studies. *Genome Research*, 24(10), 1740-1751.
