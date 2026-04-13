# ucb_mids_266_final_project
Predicting Patient Mortality from Clinical Text: A Comparison of Linear and Transformer-Based Models

# Abstract
Predicting patient mortality from clinical text is an important problem in healthcare, as it enables early identification of high-risk patients and supports clinical decision-making. In this project, we use data derived from the MIMIC-IV clinical database, which contains de-identified electronic health records from intensive care unit (ICU) patients. We focus specifically on radiology reports collected within the first 24 hours of ICU admission and formulate mortality prediction as a binary text classification task.

We compare a traditional TF-IDF + Logistic Regression model with a fine-tuned BioClinicalBERT transformer model. Due to class imbalance, we prioritize F1 score and perform threshold tuning to improve performance. Our results show that the TF-IDF model achieves the strongest performance, reaching an F1 score of 0.4230 on the test set, while the transformer model achieves slightly lower performance. Feature analysis further demonstrates that the model captures clinically meaningful patterns. Overall, this work highlights that simpler models can remain competitive for structured clinical text classification tasks.

