# Machine Learning-based network intrusion detection

## Project overview

This project develops a machine learning-based approach for network intrusion detection using the UNSW-NB15 dataset.

The objective is to develop models capable of distinguishing between normal and malicious network traffic and to evaluate their ability to generalize to previously unseen network traffic.

The project follows a complete machine learning workflow, including data understanding, exploratory data analysis, preprocessing, feature engineering, model development, evaluation, explainability and critical reflection in a cybersecurity context.

## Problem and cybersecurity context

Network intrusion detection is a cybersecurity task in which network traffic is classified as either normal or malicious.

The project addresses a supervised binary classification problem using machine learning to distinguish between these two classes.

The main challenge is not simply to maximise overall accuracy. In a cybersecurity context, missed malicious traffic can remain undetected, while legitimate traffic classified as malicious can generate unnecessary alerts and increase the workload of security analysts.

The modelling approach therefore considers both detection performance and false-alert burden when evaluating the models.

## Dataset

The project uses the [UNSW-NB15 dataset](https://research.unsw.edu.au/projects/unsw-nb15-dataset), provided by UNSW Canberra for supervised binary classification of network traffic.

The target variable distinguishes between normal and malicious observations.

The dataset is used to develop and evaluate machine learning models while keeping an independent testing dataset separate from the model development process.

The raw dataset is not redistributed in this repository. Please obtain the dataset from the official source before reproducing the analysis.

## Methodology

The project follows a structured machine learning workflow:

- Problem understanding and framing
- Data collection and understanding
- Data preprocessing, exploratory data analysis and feature engineering
- Model development, evaluation and selection
- Reproducibility
- Critical thinking, ethical AI and cybersecurity analysis

The modelling process includes preprocessing, feature engineering, feature selection, model development and evaluation using several classification algorithms.

The evaluated models include:

- Logistic Regression
- Decision Tree
- Random Forest
- XGBoost

Model performance is evaluated using several complementary metrics, including Recall, Precision, F1-score, PR-AUC, ROC-AUC and False Positive Rate.

Recall is particularly relevant in this cybersecurity context because false negatives represent malicious traffic that is not detected.

Cross-validation is used during model development, while the independent testing dataset is kept separate for the final evaluation.

## Final model and results

The final selected model is a shallow Decision Tree configured with:

- `max_depth = 3`
- Classification threshold = `0.50`

The final model was evaluated once on the independent testing dataset.

### Independent test results

| Metric | Result |
|---|---:|
| Accuracy | 76.70% |
| Recall | 100.00% |
| Precision | 70.27% |
| F1-score | 82.54% |
| PR-AUC | 92.28% |
| ROC-AUC | 93.28% |
| False Positive Rate | 51.84% |

The model detected all malicious observations in the independent test set. However, this high detection rate was associated with a substantial False Positive Rate.

The independent test results also show a decrease in several metrics compared with the cross-validation results obtained during model development. This highlights the importance of evaluating the final configuration on previously unseen data.

The independent test results were not used to perform further model or threshold adjustments.

## Explainability and critical reflection

Explainability is considered as part of the cybersecurity analysis because intrusion detection models should provide interpretable evidence about their predictions.

SHAP is used to examine model behaviour and feature contributions at both global and local levels.

The analysis also discusses important limitations and risks, including:

- dataset representativeness;
- generalisation to different network environments;
- dependence on labelled historical data;
- potential data leakage;
- model reliability;
- subgroup robustness;
- operational consequences of false positives and false negatives.

The analysis shows that `sttl` is the most influential feature in the final Decision Tree, accounting for approximately 88.26% of the impurity-based feature importance. `ct_srv_dst` and `bytes_ratio` also contribute to the model.

This strong concentration on a single feature raises a robustness consideration: if the relationship learned from the UNSW-NB15 dataset changes in another network environment, model performance may be affected.

The ethical analysis recognises that the UNSW-NB15 dataset does not contain the demographic attributes normally used for traditional demographic fairness analysis. The assessment therefore focuses on representativeness, subgroup robustness and cybersecurity-specific sources of bias.

## Reproducibility

The final modelling workflow is documented in the notebook, including the preprocessing, feature engineering, model configuration, evaluation procedure and final independent test evaluation.

The project also defines the final model configuration and classification threshold used for the independent test evaluation.

## Repository Structure

```text
unsw-nb15-intrusion-detection/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   └── Valerie_Andoulsi_Capstone_Machine_learning_based_network_intrusion_detection.ipynb
│
├── models/
│   ├── final_decision_tree.joblib
│   └── final_configuration.json
│
└── data/
    └── README.md
