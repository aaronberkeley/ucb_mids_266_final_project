# Clinical NLP Mortality Prediction

This project explores whether early clinical text can be used to predict in-hospital mortality for ICU patients. Using the MIMIC-IV dataset, I constructed an ICU cohort and extracted radiology reports from the first 24 hours of admission to evaluate how much predictive signal is available from limited early clinical documentation.

The task is framed as a binary classification problem: predicting whether a patient experiences in-hospital mortality based only on early radiology notes.

> This project is intended for research and educational purposes only. It is not a diagnostic tool or clinical decision-making system.

## Abstract

This project investigates whether early clinical text can be used to predict in-hospital mortality for ICU patients. Using the MIMIC-IV dataset, I constructed a cohort of ICU stays and extracted radiology reports from the first 24 hours of admission to evaluate how much predictive signal is available from limited early clinical documentation.

The task was framed as a binary classification problem, where the model predicts whether a patient will experience in-hospital mortality. I developed and compared multiple NLP modeling approaches, including a TF-IDF + Logistic Regression baseline and a fine-tuned BioClinicalBERT model. Because the outcome was imbalanced, model evaluation emphasized precision, recall, F1 score, ROC AUC, PR AUC, and threshold tuning rather than accuracy alone.

The results show that early radiology text contains meaningful but limited predictive signal. The interpretable TF-IDF baseline achieved strong discrimination while highlighting clinically relevant terms associated with mortality risk, such as references to shock, cardiac arrest, metastatic disease, and ECMO. BioClinicalBERT provided a transformer-based comparison, but performance remained constrained by the limited information available in early radiology reports and the class imbalance of the task.

Overall, this project demonstrates the potential and limitations of using early clinical notes for patient risk prediction. The work is intended as a research and educational analysis of clinical NLP methods, not as a diagnostic or clinical decision-making system.

## Research Question

Can radiology reports from the first 24 hours of ICU admission provide enough clinical signal to predict in-hospital mortality?

This question is important because early risk prediction could help identify high-risk patients sooner. However, early clinical notes are limited, incomplete, and often focused on specific findings rather than the full patient condition. This makes the task challenging and clinically realistic.

## Dataset

This project uses the MIMIC-IV dataset, a large de-identified critical care database containing hospital admissions, ICU stays, clinical notes, and patient outcomes.

The raw MIMIC-IV data is **not included** in this repository due to data use restrictions. Access to the dataset requires completion of the required training and approval through PhysioNet.

### Data sources used

The project uses the following types of data:

- Hospital admissions
- ICU stay records
- Radiology notes
- In-hospital mortality labels

The final modeling dataset was created by linking ICU stays with early radiology reports and patient outcomes.

## Cohort Construction

The cohort was constructed by identifying ICU stays and linking them to radiology notes written within the first 24 hours of admission. Each patient stay was assigned a binary mortality label based on whether the patient died during the hospital admission.

High-level cohort construction steps:

1. Load admissions, ICU stays, and radiology notes
2. Link ICU stays to hospital admissions
3. Filter radiology notes to the first 24 hours of admission
4. Aggregate early radiology text at the ICU stay level
5. Create the binary in-hospital mortality label
6. Split data into training, validation, and test sets
7. Train and evaluate NLP models

## Modeling Approach

This project compares both traditional and transformer-based NLP methods.

### 1. TF-IDF + Logistic Regression Baseline

The first model uses TF-IDF vectorization to convert radiology text into sparse numerical features. A Logistic Regression classifier is then trained to predict in-hospital mortality.

This baseline is useful because it is:

- Fast to train
- Interpretable
- Strong for text classification tasks
- Easy to evaluate using feature coefficients

The model also allows inspection of terms most associated with mortality risk.

### 2. BioClinicalBERT

A transformer-based model was also evaluated using BioClinicalBERT, a BERT model pretrained on biomedical and clinical text. This approach was used to test whether contextual clinical language representations could improve performance beyond the TF-IDF baseline.

The transformer model was fine-tuned on the mortality prediction task and evaluated using the same classification metrics.

### 3. Threshold Tuning

Because the mortality outcome is imbalanced, default classification thresholds are not always appropriate. The project evaluates different decision thresholds to better understand the tradeoff between precision and recall.

Threshold tuning was used to optimize F1 score and better reflect performance on the minority mortality class.

## Evaluation Metrics

Because the dataset is imbalanced, accuracy alone is not sufficient. The project evaluates models using:

- Precision
- Recall
- F1 score
- ROC AUC
- PR AUC
- Confusion matrix
- Threshold sweep analysis

These metrics provide a more complete picture of model performance, especially for the positive mortality class.

## Results

The models showed that early radiology reports contain meaningful but limited predictive signal for in-hospital mortality.

The TF-IDF + Logistic Regression baseline achieved strong discrimination and provided interpretable feature weights. Terms associated with higher predicted mortality risk included references to severe clinical conditions such as shock, cardiac arrest, metastatic disease, and ECMO.

BioClinicalBERT provided a transformer-based comparison, but performance remained constrained by the limited information available in early radiology reports and the class imbalance of the prediction task.

### Key takeaway

Early radiology notes can help identify elevated mortality risk, but they do not contain the full clinical context needed for highly reliable prediction on their own.

## Model Interpretation

One advantage of the TF-IDF + Logistic Regression baseline is interpretability. By examining model coefficients, the project identifies terms that are positively or negatively associated with predicted mortality risk.

Examples of terms associated with higher risk included:

- cardiac arrest
- shock
- metastatic
- ECMO
- ascites

Examples of terms associated with lower risk included more routine or less severe clinical language, such as references to normal findings or postoperative context.

These results suggest that the model learned clinically meaningful patterns, although the predictions should not be interpreted as causal or diagnostic.

## Repository Structure

```text
clinical-nlp-mortality-prediction/
├── README.md
├── clinical_nlp_mortality_prediction.ipynb
├── final_report.pdf
