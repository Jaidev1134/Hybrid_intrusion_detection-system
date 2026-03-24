# 🛡️ CICIDS2017 - Advanced Intrusion Detection System
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-F37626.svg?style=for-the-badge&logo=Jupyter&logoColor=white)](https://jupyter.org/)

An advanced, state-of-the-art anomaly and intrusion detection system built and evaluated on the **CICIDS2017** dataset. This project employs a novel **Two-Stage Hybrid Architecture**, combining robust ensemble methods with modern Graph Neural Networks to accurately distinguish benign network traffic from diverse malicious attacks.

---

## 🚀 Key Features

*   **Two-Stage Classification Architecture**:
    *   **Stage 1 (Binary Classification)**: Utilizes an optimized **Random Forest** classifier to effectively separate normal (BENIGN) traffic from malicious (ATTACK) traffic.
    *   **Stage 2 (Multi-Class Classification)**: Malicious traffic is fed into a **Graph Neural Network (GNN)** augmented with a **Bayesian Output Layer**. By modeling data relationships as a k-NN graph, the model predicts the specific class of an attack while providing uncertainty estimations.
*   **🧠 Dynamic Feature Selection**: Employs both **Boruta** and **PCA**-based metric rankings to dynamically figure out the most impactful predictive features for the model.
*   **⚖️ Advanced Imbalanced Data Handling**: The CICIDS2017 dataset suffers from heavy class imbalance between varied attack types. This project resolves this utilizing intelligent combinations of **SMOTE** (Synthetic Minority Over-sampling Technique) and **Random Under-sampling**.
*   **Explainable AI (XAI)**: Understand model reasoning using **SHAP (SHapley Additive exPlanations)** values, providing global feature importance and interpretability of complex node classifications.

---

## 📂 Project Structure

| File / Folder | Description |
| :--- | :--- |
| `RAW (2).ipynb` | The primary pipeline notebook containing the complete Two-Stage approach: data preparation, model construction (RF + PyG GNN Bayesian layer), pipeline training, and SHAP explainability. |
| `smote (1).ipynb` | Focused module for handling minority class data using SMOTE techniques. |
| `undersampler.ipynb` | Focused module primarily utilizing `RandomUnderSampler` to naturally balance the initial data by reducing majority class footprint. |
| `top_9_balanced_verified.csv` | The pre-processed, meticulously balanced version of the CICIDS2017 dataset containing the critical Top 9 target classes. |
| `CICIDS2017_combined.csv` | Raw aggregated subset data (prior to class-specific filtering). |

---

## 📊 Dataset: CICIDS2017

This project builds heavily upon the **CICIDS2017** dataset, an industry-standard benchmark encompassing benign network traffic alongside prevalent contemporary attacks:
1.  **DDoS** / **DoS** (e.g., Hulk, GoldenEye, Slowloris)
2.  **Brute Force** (FTP, SSH)
3.  **Web Attacks** (XSS, SQL Injection)
4.  **Botnet Activity**
5.  **Infiltration**
6.  *and more.*

*Note: Ensure `top_9_balanced_verified.csv` is locally present in your working space before running the modeling notebooks.*

---

## ⚙️ Installation & Requirements

Ensure you have Python 3.8+ installed. Using a `conda` or virtual environment is heavily recommended. 
The core dependencies include:

```bash
# General Data Science & ML stack
pip install numpy pandas scikit-learn matplotlib seaborn imbalanced-learn

# Advanced feature selection and Interpretability
pip install boruta shap

# PyTorch and Graph Neural Network libraries
pip install torch
# Note: For PyTorch Geometric, please match your CUDA/PyTorch version accordingly.
pip install torch_geometric
```
*(Reference [PyTorch Geometric Install Guide](https://pytorch-geometric.readthedocs.io/en/latest/install/installation.html) for specific platform combinations).*

---

## 💻 Usage

1.  **Preparation**: Make sure all CSV files (`top_9_classes.csv`, `top_9_balanced_verified.csv`) are correctly referenced in the code paths.
2.  **Addressing Imbalance**: Start with `smote (1).ipynb` or `undersampler.ipynb` if you wish to generate new balanced datasets from scratch. 
3.  **Main Pipeline**: Open `RAW (2).ipynb` in Jupyter Notebook, JupyterLab, or Google Colab. Run the cells in order to:
    *   Load and pre-process the data
    *   Initialize feature ranking (Boruta/PCA)
    *   Train the binary Random Forest (Stage 1)
    *   Forward malicious traffic to the PyTorch Geometric Bayesian GNN (Stage 2)
    *   View comprehensive metrics (Precision, Recall, F1, Confusion Matrices) and SHAP impact plots.

---

## 📈 Model Performance & Metrics

The Two-Stage framework ensures high **Accuracy** regarding normal traffic while utilizing the structural reasoning of the GNN to maximize **F1-Scores** across the rare attack classes. Refer to the model outputs inside `RAW (2).ipynb` for specific evaluation numbers, visualized confusion matrices, and model cross-validation states.

---
*Created for advanced research and modeling in robust Intrusion Detection capabilities. 🛡️ By Jaidev Sharma*
