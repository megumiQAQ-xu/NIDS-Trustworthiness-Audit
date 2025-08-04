# NIDS-Trustworthiness-Audit
n XAI-driven audit of shortcut learning in Network Intrusion Detection Systems.


# NIDS Trustworthiness Audit: An XAI-Driven Analysis of Shortcut Learning

This repository contains the complete experimental code and dissertation for the project titled "An XAI-Driven Audit of Shortcut Learning in Network Intrusion Detection Systems."

##  Abstract

This project addresses a critical trustworthiness gap in Machine Learning-based Network Intrusion Detection Systems (ML-NIDS). While many ML-NIDS report near-perfect accuracy on benchmark datasets like CIC-IDS2017, this performance is often predicated on "shortcut learning"—exploiting dataset-specific artifacts rather than learning generalizable attack patterns. The deployment of such models creates a false sense of security.

This research first replicates these state-of-the-art results by training high-performance classifiers (XGBoost and RandomForest) on the CIC-IDS2017 dataset. Subsequently, it subjects the models to a rigorous post-hoc audit using SHAP (SHapley Additive exPlanations) to prove that their success is indeed based on shortcuts. Finally, the project demonstrates the fragility of these models through adversarial testing and explores potential remediation by retraining on a sanitized feature set.

##  Key Features

- **End-to-End Pipeline**: From data preprocessing and EDA to advanced model analysis in a single Google Colab notebook.
- **Shortcut Learning Demonstration**: Empirically shows how high-performance models achieve near-perfect scores by exploiting dataset flaws.
- **XAI-Driven Audit**: Uses SHAP to provide concrete, visual evidence of the model's flawed decision-making logic.
- **Robustness Testing**: Includes adversarial tests to prove the fragility of the model and feature ablation experiments to explore remediation.
- **Kaggle Best Practices**: Incorporates high-quality coding practices, including feature selection and clear visualizations.

##  Methodology

The experiment follows a structured, multi-stage pipeline:

1.  **Data Preprocessing**: The eight CSV files from the CIC-IDS2017 dataset are loaded, cleaned, and preprocessed.
2.  **Exploratory Data Analysis (EDA)**: The class distribution and feature correlations are analyzed.
3.  **Feature Selection**: A baseline RandomForest model is used to identify the top 30 most important features for efficient and robust modeling.
4.  **Model Training**: RandomForest and XGBoost models are trained on the selected feature set.
5.  **Performance Evaluation**: The models are evaluated, achieving near-perfect F1-scores, thus replicating the "illusion of security."
6.  **XAI Analysis (SHAP)**: The internal logic of the trained XGBoost model is audited to identify reliance on shortcut features.
7.  **Adversarial & Ablation Tests**: The model's fragility is proven, and a potential remediation path is explored.

##  How to Run the Experiment

This project is designed to be run in **Google Colab**.

1.  **Get the Data**
    * Download the dataset from the official source: [CIC-IDS2017 Dataset](https://www.unb.ca/cic/datasets/ids-2017.html).
    * You need the **`MachineLearningCSV.zip`** file.
    * Unzip the file and upload the entire folder (containing all 8 `.csv` files) to your Google Drive.

2.  **Setup the Notebook**
    * Open the `.ipynb` file from this repository in Google Colab.
    * In **Cell 4**, update the `path_to_csv_folder` variable to point to the correct location of your dataset in Google Drive.
    * In the Colab menu, go to **Runtime -> Change runtime type** and select **T4 GPU** to enable GPU acceleration for XGBoost.

3.  **Run the Experiment**
    * Run the cells sequentially from top to bottom.

##  Key Findings

The experiment successfully confirmed the dissertation's core hypothesis:

- The models achieved near-perfect F1-scores (>0.99), demonstrating the "illusion of security."
- The SHAP analysis provided definitive evidence that this performance was based on shortcut learning. Specifically, the model heavily relied on simple, non-robust features like `Average Packet Size`, learning a rule that "low average packet size equals an attack."
- The adversarial test proved the model's fragility, with its accuracy collapsing after a minor modification to the shortcut feature.
- The feature ablation experiment showed that by removing these shortcuts, a new model could be trained that relied on a more diverse set of features, albeit with a slightly lower (but more honest) F1-score.
