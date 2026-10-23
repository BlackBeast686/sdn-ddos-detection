# SDN DDoS Detection

Detecting **DDoS attacks on SDN (Software-Defined Networking) based networks** with machine learning. The repository applies the same model family — a voting ensemble of classical classifiers, plus (in one notebook) a Keras neural network — across three different SDN DDoS datasets.

> **Note on scope:** These are research/experimental notebooks for comparing models and techniques, not a production intrusion-detection system.

## Notebooks & datasets

| Notebook | Dataset(s) | Models | Ensemble accuracy |
|----------|-----------|--------|-------------------|
| `SDN_DDoS_Detection.ipynb` | LR-HR DDoS 2024 Dataset for SDN-Based Networks | KNN, Naive Bayes, Decision Tree, Random Forest voting ensemble + Keras NN | ~0.999 |
| `SDN_DDOS_Dataset.ipynb` | `SDN_DDOS_dataset.csv` | KNN, NB, DT, SVM, RF, LogReg + voting ensemble (+ 5-fold CV) | 0.960 |
| `ICMP_SDN_DDOS_UDP_Datasets.ipynb` | `SDN_DDOS_dataset.csv` + `ICMP.csv` + `udp.csv` combined (~119k rows) | same six + voting ensemble (+ CV) | 0.943 |

Common pipeline: numeric-feature selection, Gaussian-noise injection, mean imputation, `StandardScaler` scaling, a stratified train/test split, per-model metrics (accuracy, precision, recall, F1), and a `VotingClassifier` ensemble. The two dataset-specific notebooks add stratified 5-fold cross-validation; `SDN_DDoS_Detection.ipynb` additionally works through a series of neural-network experiments (dropout, L2 regularization, batch norm, SMOTE, Gaussian noise, early stopping).

None of the datasets are included in this repository — place the relevant CSV(s) at the paths referenced in each notebook (`/content/` on Colab) or update them.

## Results

Voting-ensemble test accuracy per dataset (single runs, cross-validated where noted):

| Dataset | Ensemble accuracy |
|---------|-------------------|
| LR-HR DDoS 2024 | ~0.999 |
| `SDN_DDOS_dataset.csv` | 0.960 |
| `SDN_DDOS` + `ICMP` + `udp` combined | 0.943 |

> Figures are single runs (cross-validated where indicated). Treat them as indicative rather than definitive.

## Requirements

Developed in Google Colab. Main dependencies:

- `scikit-learn`
- `tensorflow`
- `imbalanced-learn`
- `pandas`
- `numpy`

Install everything with:

```bash
pip install -r requirements.txt
```

## Getting started

1. Open the notebook you want in Google Colab or Jupyter.
2. Place the dataset CSV(s) that the notebook expects at the referenced paths.
3. Run the cells top to bottom; each notebook is self-contained.

## Repository structure

```
.
├── SDN_DDoS_Detection.ipynb            # LR-HR DDoS 2024 dataset (ML ensemble + Keras NN)
├── SDN_DDOS_Dataset.ipynb              # SDN_DDOS_dataset.csv
├── ICMP_SDN_DDOS_UDP_Datasets.ipynb    # SDN_DDOS + ICMP + udp combined
└── README.md
```
