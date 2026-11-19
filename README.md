# Ensemble Learning for Breast Cancer Detection: A High-Accuracy Model Integrating Clinical Insights

[![DOI](https://img.shields.io/badge/DOI-10.1109%2FICIC63915.2024.11116335-blue)](https://doi.org/10.1109/ICIC63915.2024.11116335)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

**Muhammad Abdullah, Tanzila Kehkashan, Muhammad Zaman, Faheem Akbar, Raja Adil Riaz, Muhammad Hamza**

*2024 5th International Conference on Innovative Computing (ICIC), IEEE, 2024*

[Paper (IEEE Xplore)](https://ieeexplore.ieee.org/document/11116335) | [Author's accepted version (PDF)](paper/ensemble_breast_cancer_icic2024.pdf)

This repository contains the official code for the paper.

## Summary

The paper presents a breast cancer detection model that uses tabular clinical features rather than raw images. It combines three classical classifiers (Logistic Regression, Decision Tree, and Random Forest) in a soft-voting ensemble, which averages the predicted probability of malignancy from each model. Each model is tuned with grid search using 5-fold cross-validation and AUC-ROC as the scoring metric. Features are selected by combining correlation analysis with Random Forest feature importance. Feature importance and SHAP analysis are used to explain the model's decisions.

On the Breast Cancer Wisconsin (Diagnostic) dataset, the paper reports 98.82% accuracy and an AUC-ROC of 0.994 for the ensemble. The most important predictors are mean concave points and worst radius.

## Repository structure

```
ensemble-breast-cancer-detection/
├── notebooks/
│   └── ensemble_breast_cancer_detection.ipynb   # main entry point: full pipeline
├── paper/
│   └── ensemble_breast_cancer_icic2024.pdf      # author's accepted version
├── requirements.txt
├── CITATION.cff
├── LICENSE
└── README.md
```

## Installation

Python 3.11 was used to test the environment.

```bash
git clone https://github.com/vlcmatrix-lab/ensemble-breast-cancer-detection.git
cd ensemble-breast-cancer-detection
python -m venv .venv
# Windows: .venv\Scripts\activate
# Linux/macOS: source .venv/bin/activate
pip install -r requirements.txt
```

## Dataset

The paper uses the **Breast Cancer Wisconsin (Diagnostic)** dataset (Wolberg, Street and Mangasarian, University of Wisconsin). It contains 569 fine needle aspirate (FNA) samples (357 benign, 212 malignant), each with 30 numeric features describing cell nuclei.

- Official source: [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic)

No data files are included in this repository. The notebook loads the dataset through scikit-learn's built-in copy (`sklearn.datasets.load_breast_cancer`), so you do not need to download anything.

## Usage

```bash
jupyter notebook notebooks/ensemble_breast_cancer_detection.ipynb
```

Run all cells in order. The notebook covers:

1. Data loading and exploratory analysis
2. Stratified 70 / 15 / 15 train / validation / test split
3. Feature selection (correlation and preliminary Random Forest importance)
4. Hyperparameter tuning with grid search (5-fold CV, AUC-ROC), using the grids in Table I of the paper
5. The soft-voting ensemble
6. Evaluation on the validation and test sets, ROC curves, feature importance, SHAP, nested cross-validation, threshold sensitivity analysis, and learning curves

Figures are saved to `results/` (created automatically). The nested cross-validation step takes a few minutes.

The notebook is distributed without saved outputs.

## Results

All values below are reported in the paper.

**Performance of the individual models and the ensemble (Table II)**

| Model | Accuracy | Sensitivity | Specificity | AUC-ROC |
|---|---|---|---|---|
| Logistic Regression | 95.3% | 96.2% | 94.7% | 0.987 |
| Decision Tree | 93.8% | 94.3% | 93.5% | 0.939 |
| Random Forest | 96.8% | 97.6% | 96.2% | 0.991 |
| **Ensemble (Proposed)** | **98.82%** | **98.1%** | **96.5%** | **0.994** |

**Top 5 features by Random Forest importance (Table III)**

| Feature | Importance |
|---|---|
| Mean concave points | 0.162 |
| Worst radius | 0.134 |
| Worst perimeter | 0.115 |
| Worst concave points | 0.108 |
| Mean radius | 0.089 |

**Comparison with other studies (Table IV)**

| Method | Accuracy | AUC-ROC |
|---|---|---|
| LR + DT + RF (ours) | 98.82% | 0.994 |
| Deep CNN (baseline) | - | 0.910 |
| Random Forest | 98% | 0.98 |
| Graph Neural Network | 97.1% | 0.989 |

**Nested cross-validation (Table V)**

| Metric | Value |
|---|---|
| Mean Accuracy | 98.82% |
| Mean AUC-ROC | 0.994 |

**Threshold sensitivity analysis (Table VI)**

| Metric | Value |
|---|---|
| Maximum F1-score | 0.973 (threshold = 0.48) |
| Balanced Accuracy | 98.8% (threshold = 0.55) |

## Citation

If you use this code, please cite:

```bibtex
@inproceedings{abdullah2024ensemble,
  author    = {Abdullah, Muhammad and Kehkashan, Tanzila and Zaman, Muhammad and Akbar, Faheem and Riaz, Raja Adil and Hamza, Muhammad},
  title     = {Ensemble Learning for Breast Cancer Detection: A High-Accuracy Model Integrating Clinical Insights},
  booktitle = {2024 5th International Conference on Innovative Computing (ICIC)},
  publisher = {IEEE},
  year      = {2024},
  doi       = {10.1109/ICIC63915.2024.11116335}
}
```

## Copyright notice

© 2024 IEEE. Personal use of this material is permitted. Permission from IEEE must be obtained for all other uses. The final version is published at DOI: [10.1109/ICIC63915.2024.11116335](https://doi.org/10.1109/ICIC63915.2024.11116335).

The PDF in `paper/` is the authors' accepted version, not the publisher's typeset version.

## License

The code in this repository is released under the [MIT License](LICENSE). The copyright notice above applies to the paper.
