# SDN DDoS Detection

Detecting **DDoS attacks on SDN (Software-Defined Networking) based networks** using the *LR-HR DDoS 2024 Dataset for SDN-Based Networks*. The notebook combines classical machine-learning classifiers with a Keras neural network and works through a series of iterative experiments, each adding a regularization or robustness technique.

> **Note on scope:** This is a research/experimental notebook for comparing models and techniques, not a production intrusion-detection system.

## Task & data

- **Dataset:** `LR-HR DDoS 2024 Dataset for SDN-Based Networks.csv`
- **Task:** classifying network flows as benign or DDoS attack (the `Label` column).
- **Preprocessing:** dropping non-contributing / constant flow-flag columns, `VarianceThreshold` feature filtering, `StandardScaler` scaling, and `SMOTE` for class imbalance.

The dataset is **not** included in this repository — place the CSV at the path referenced in the notebook (`/content/` on Colab) or update it.

## Approach

The notebook is organised as progressive experiments (each markdown cell notes what was added):

- **Models** — KNN, Naive Bayes, Decision Tree, and Random Forest combined in a `VotingClassifier`, plus a Keras feedforward neural network.
- **Techniques explored** — dropout, L2 regularization, batch normalization, Gaussian noise injection, cross-validation (`StratifiedKFold`), early stopping, and SMOTE oversampling.
- A final section runs the pipeline on a **random/simulated dataset** as a noise/robustness sanity check.

## Results

On the real dataset, the models reach very high accuracy (test set, single runs):

| Model | Accuracy |
|-------|----------|
| Decision Tree | 0.9997 |
| KNN | 0.9996 |
| Voting ensemble | 0.9996 |
| Naive Bayes | 0.9994 |
| Neural network | ~0.998 |

> Accuracies this high usually mean the classes are very easily separable in this dataset (and/or some leakage-prone features); the later experiments add noise, SMOTE, and regularization partly to probe robustness. The simulated-data section performs near chance by design. Treat the figures as indicative.

## Requirements

Developed in Google Colab. Main dependencies:

- `tensorflow`
- `scikit-learn`
- `imbalanced-learn`
- `pandas`
- `numpy`

Install everything with:

```bash
pip install -r requirements.txt
```

## Getting started

1. Open the notebook in Google Colab or Jupyter.
2. Place `LR-HR DDoS 2024 Dataset for SDN-Based Networks.csv` at the path used in the cells.
3. Run the cells top to bottom; each experiment section is self-contained.

## Repository structure

```
.
├── Code.ipynb
└── README.md
```
