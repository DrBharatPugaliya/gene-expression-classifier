# 🧬 Gene Expression Classifier

> A PyTorch-based deep learning pipeline for cancer subtype classification using TCGA RNA-Seq gene expression data. Fully containerised with Docker for reproducibility.

---

## 🎯 Project Overview

This project applies machine learning to bulk RNA-Seq gene expression data from [The Cancer Genome Atlas (TCGA)](https://www.cancer.gov/tcga) to classify cancer subtypes. It demonstrates an end-to-end ML pipeline — from raw count data through preprocessing, model training, evaluation, and Dockerised deployment.

**Why this matters:** Accurate cancer subtype classification from transcriptomic data can guide treatment decisions and improve patient outcomes — a core challenge in computational oncology.

---

## 🏗️ Repository Structure

```
gene-expression-classifier/
│
├── data/
│   ├── raw/                  # Raw TCGA expression matrices (not committed — see Data section)
│   └── processed/            # Normalised, filtered data ready for modelling
│
├── notebooks/
│   ├── 01_data_exploration.ipynb     # EDA, distribution plots, QC
│   ├── 02_preprocessing.ipynb        # Normalisation, feature selection
│   └── 03_model_training.ipynb       # Training loop, metrics, visualisations
│
├── src/
│   ├── data/
│   │   ├── __init__.py
│   │   └── preprocess.py     # Data loading, normalisation, train/val/test split
│   ├── models/
│   │   ├── __init__.py
│   │   └── classifier.py     # PyTorch model architecture
│   └── utils/
│       ├── __init__.py
│       └── metrics.py        # Evaluation metrics, plotting helpers
│
├── tests/
│   ├── test_preprocess.py    # Unit tests for data pipeline
│   └── test_model.py         # Unit tests for model forward pass
│
├── results/
│   └── figures/              # Training curves, confusion matrices, UMAP plots
│
├── Dockerfile                # Containerised environment
├── requirements.txt          # Python dependencies
├── .gitignore
├── LICENSE
└── README.md
```

---

## 🧪 Methods

### Data
- **Source:** TCGA RNA-Seq gene expression data (HTSeq counts) via [GDC Data Portal](https://portal.gdc.cancer.gov/)
- **Target:** Cancer subtype labels per TCGA project
- **Preprocessing:** TMM/TPM normalisation · log2 transform · variance-based feature selection · train/val/test stratified split

### Model
- **Architecture:** Fully-connected neural network (MLP) built in PyTorch
- **Input:** ~2,000 most variable genes per sample
- **Output:** Softmax over cancer subtype classes
- **Training:** Adam optimiser · CrossEntropyLoss · early stopping · dropout regularisation

### Evaluation
- Accuracy · F1-score (macro) · ROC-AUC
- Confusion matrix
- UMAP visualisation of learned embeddings

---

## 🚀 Quickstart

### Option 1: Docker (Recommended)

```bash
# Clone the repo
git clone https://github.com/bharatpugaliya/gene-expression-classifier.git
cd gene-expression-classifier

# Build and run the container
docker build -t gene-classifier .
docker run -v $(pwd)/data:/app/data gene-classifier
```

### Option 2: Local Setup

```bash
# Clone and install dependencies
git clone https://github.com/bharatpugaliya/gene-expression-classifier.git
cd gene-expression-classifier
pip install -r requirements.txt

# Download data (see Data section below)
# Then run notebooks in order:
jupyter notebook notebooks/
```

---

## 📦 Data Access

TCGA data is publicly available but must be downloaded separately due to size.

1. Visit [GDC Data Portal](https://portal.gdc.cancer.gov/)
2. Filter by: Program → TCGA · Data Type → Gene Expression Quantification · Workflow → HTSeq - Counts
3. Download and place files in `data/raw/`

Alternatively, use the [TCGAbiolinks R package](https://bioconductor.org/packages/TCGAbiolinks/) — see `notebooks/01_data_exploration.ipynb` for instructions.

---

## 📊 Results

*Results will be updated as the project progresses.*

| Metric | Value |
|---|---|
| Accuracy | — |
| Macro F1 | — |
| ROC-AUC | — |

---

## 🛠️ Requirements

```
torch>=2.0.0
numpy>=1.24.0
pandas>=2.0.0
scikit-learn>=1.3.0
matplotlib>=3.7.0
seaborn>=0.12.0
umap-learn>=0.5.3
jupyter>=1.0.0
```

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 👤 Author

**Bharat Pugaliya**
MSc Bioinformatics, University of Birmingham
📧 dr.bharatpugaliya@gmail.com
