# GitHub Kaggle Project README - WiDS Datathon 2025 

---

## **👥 Team Members**

* Joy Chang [(@JoyChang10)](https://github.com/JoyChang10) - Performed data preprocessing and feature engineering for categorical, quantitative, and functional MRI data, built XGBoost model.
* Paige Wu [(@pwinnie2026)](https://github.com/pwinnie2026) - Performed data understanding, cleaning, and visualized dataset distributions.
* Fatima Waqar (@524fatima) -  Performed visualization and cleaning for categorical and quantitative data, finetuned XGBoost model with regularization.
* Tanvi Ladha (@tanviladha) - Performed data cleaning, visualized dataset distributions, addressed imbalances, conducted feature analysis and model research.

---

## **🎯 Project Highlights**

* Built an XGBClassifier using FMRI connectome features, quantitative cognitive assessments, and encoded categorical data with regularization and data sampling to predict sex and ADHD diagnosis amongst patients
* Achieved an F1 score of \[insert score\] and a ranking of \[insert ranking out of participating teams\] on the final Kaggle Leaderboard
* Used \[explainability tool\] to interpret model decisions
* Implemented one-hot encoding, feature pruning, missing value replacement, and sampling to optimize results within compute constraints while maintaining performance

🔗 [WiDS Datathon 2025 | Kaggle Competition Page](https://www.kaggle.com/competitions/widsdatathon2025/overview)

---

## **👩🏽‍💻 Setup & Execution**

**Provide step-by-step instructions so someone else can run your code and reproduce your results. Depending on your setup, include:**

* Access the datasets and goals of this project on the above linked Kaggle competition page 
* To install any necessary dependencies, clone this repository and find them in our notebook 
* Make sure you have your Kaggle key set up with your Google drive so you can access the datasets
* Run the notebook in Google Colab, Jupyter Notebook, etc. 

---

## **🏗️ Project Overview**

* This project was completed for the WiDS (Women in Data Science) Datathon Global Challenge, in collaboration with the Break Through Tech AI Program.
* The challenge aimed to build a machine learning model capable of predicting an individual's sex and ADHD diagnosis using fMRI connectome data and demographic/behavioral survey data.
* This work has important real-world applications: early ADHD diagnosis—especially in females, who are historically underdiagnosed—can enable more equitable mental health interventions and support personalized treatment strategies. Understanding sex-specific brain mechanisms also advances the field of women’s brain health.

---

## **📊 Data Exploration**

* We used the dataset provided by the Healthy Brain Network (HBN) and the Reproducible Brain Charts (RBC), which includes: fMRI functional connectivity matrices (representing brain region correlations), quantitative features (e.g., behavioral and cognitive test scores), categorical data (e.g., socio-demographic and emotional health survey responses).
* Challenges included data imbalance, with more male participants and a higher ADHD diagnosis rate among males and Caucasians.
<img src="https://github.com/user-attachments/assets/365bf0d1-74d1-4b1a-889a-51deed34f87c" width="600">

* There is high dimensionality of the FMRI data (~4000+ features), and potential bias in labels due to social factors in ADHD diagnosis. We also found that parental occupation was highly imbalanced across the dataset. The figures below show the distribution of occupation levels for 'Barratt_Barratt_P1_OCC' and 'Barratt_Barratt_P2_Occ':
<div style="display: flex; justify-content: center; gap: 10px;">
    <img src="https://github.com/user-attachments/assets/9f9dc0c3-ee08-45a5-8b3f-8282e15896f2" width="600">
    <img src="https://github.com/user-attachments/assets/b9c84ca4-f5d5-482c-8418-4eb1c117ec11" width="600">
</div>

* Data exploration and preprocessing approaches also included understanding which variables had high correlations in predicting ADHD and sex.
* Furthermore, we proceeded with the following: one-hot encoding categorical variables, standardizing values, reducing feature dimensionality, and undersampling to address data imbalances we found earlier.

---

**Data Visualizations:**

* By visualizing the correlations between quantitative features and the labels (sex and ADHD) in a heatmap, we were able to better observe the spread of correlations and determine which features to retain.
<div style="display: flex; justify-content: center; gap: 10px;">
    <img src="https://github.com/user-attachments/assets/7c47a975-8c2d-4aca-b562-f6874c9f1f49" width="600">
    <img src="https://github.com/user-attachments/assets/d11eea05-e198-4354-9a0a-3c9e2a4bd969" width="600">
</div>

* After performing PCA on the fMRI data, we created a scree plot to identify which fMRI features had high explanatory power for variance and to assess whether there was an increase compared to before PCA.
<img src="https://github.com/user-attachments/assets/b482f272-9725-4891-917c-90fd1485063d" width="600">

---

## **🧠 Model Development**

* Model used: XGBoost Classifier (XGBClassifier) to predict two binary targets: ADHD diagnosis (ADHD_Outcome) and sex (Sex_F) using the aforementioned multimodal data. 
* To address the high dimensionality of the FMRI data and potential overfitting, we applied L1 (reg_alpha) and L2 (reg_lambda) regularization. The model was further optimized using parameters such as: max_depth to control tree complexity, learning rate, n_estimators, and subsampling. 
* Training setup: trained on the Kaggle-provided training set using an 80/20 train-test split. During preprocessing, we ensured consistent feature alignment between train and test sets by adding missing columns and matching column order before inference. Final predictions included both target outputs (Predicted ADHD, Predicted Sex).

---

## **📈 Results & Key Findings**

* Performance metrics (e.g., Kaggle Leaderboard score, F1-score)
* How your model performed overall
* How your model performed across different skin tones (AJL)
* Insights from evaluating model fairness (AJL)

**Potential visualizations to include:**

* Confusion matrix, precision-recall curve, feature importance plot, prediction distribution, outputs from fairness or explainability tools

---

## **🖼️ Impact Narrative**

**WiDS challenge:**

- What brain activity patterns are associated with ADHD; are they different between males and females, and, if so, how?
    - While our model (an XGBoost classifier) did not directly produce interpretable neurobiological insights, it was trained on functional connectivity matrices — where each feature represents the correlation between a pair of brain regions — along with demographic and behavioral data. These features allow the model to learn patterns in brain network interactions that differ between individuals with and without ADHD.
    - Given the performance of the model in predicting ADHD diagnosis, we can infer that there are distinct patterns of functional connectivity that help distinguish ADHD from non-ADHD brains. Prior research supports this, particularly involving regions like the prefrontal cortex, default mode network, and attention-regulation networks.
    - Regarding sex differences, the dataset itself reflected an imbalance in ADHD diagnosis across sexes, which is also consistent with real-world diagnostic patterns.
    - Though we didn’t perform direct interpretability analysis, we recognize that models trained on this data might learn sex-specific connectivity cues, as ADHD often manifests differently in males and females. This could suggest that ADHD-related brain patterns are influenced by sex, supporting the hypothesis that girls may present more subtle or different neurobiological markers of ADHD.


- How could your work help contribute to ADHD research and/or clinical care?
    - Modeling subtle brain-based signals: By training a model on high-dimensional FMRI connectivity data, we demonstrated that machine learning can detect brain-based signatures associated with ADHD, even in the absence of overt behavioral symptoms.
    - Highlighting diagnostic disparities: This work draws attention to the underdiagnosis of ADHD in females, and reinforces the importance of including sex as a consideration in both model evaluation and healthcare diagnostics.
    - Providing a foundation for future interpretability: Although our current model is not interpretable in a neuroanatomical sense, it establishes a baseline for future models that could integrate explainability tools (like SHAP or permutation importance) to reveal the most influential brain regions or connections for diagnosis.
    - Supporting scalable screening tools: In a clinical context, models like this could eventually serve as supplementary screening tools, helping flag individuals who may benefit from closer clinical evaluation—especially in populations historically overlooked by standard diagnostic criteria.

---

## **🚀 Next Steps & Future Improvements**

**Address the following:**

* Model Limitations: Due to time constraints as part of the collaboration with Break Through Tech, the model may perform more accurately on males due to class imbalances. Furthermore, demographic factors such as socioeconomic status may also play a role in higher rates of diagnosis in certain children with ADHD rather than others. 
* Future Work: It might be ideal to train two different models when making predictions that require different patterns for different patients, such as sex differences. 
* Some techniques to explore in further work could be Microsoft's Fair Learn toolkit which offers APIs and tools to help mitigate bias specifically in AI systems. As a field that has a history of underdiagnosis by sex and other demographic factors, techniques like this in model building could provide a greater understanding. 

---

## **📄 References & Additional Resources**

* https://fairlearn.org/
* https://www.nvidia.com/en-us/glossary/xgboost/
* Break Through Tech AI course material 

---

