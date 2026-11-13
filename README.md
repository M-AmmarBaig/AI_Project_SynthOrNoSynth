# Two-Stage Hybrid Synthetic Population & Survey Simulation Pipeline

[![Python 3.11](https://img.shields.io/badge/python-3.11-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end AI research project addressing the failure modes of Large Language Models in survey simulation (algorithmic caricature, joint distribution collapse, and behavioral information deficit).

This repository implements **Option D: A Two-Stage Hybrid Architecture**:
1. **Stage 1 (Statistical Population Synthesis):** Rigorous data forensic cleaning, behavioral context validation (Wang et al., 2024), and a multi-paradigm benchmark of generative tabular models (Naive Marginal Sampling, Stratified Contingency / IPF, Gaussian Copula via Sklar's Theorem, Bayesian Networks via BIC DAG learning, and Deep TVAE).
2. **Stage 2 (Behavioral Persona Conditioning & Survey Elicitation):** Compiling rich synthetic personas and extracting survey responses via Semantic Similarity Rating (SSR; Maier et al., 2025).

---

## Repository Structure

```text
├── data/
│   ├── raw/                  # Untouched raw marketing campaign dataset
│   ├── processed/            # Cleaned data and stratified 80/20 train/test splits
│   └── synthetic_stage1/     # Generated populations across candidate models
├── docs/
│   └── ResearchPapers/       # Downloaded foundational papers (Maier 2025, Cheng 2023, Bisbee 2024, etc.)
├── notebooks/
│   ├── 01_DataAudit_Cleaning.ipynb    # Forensic audit, anomaly detection, behavioral ROC proof
│   └── 02_Stage1_Synthesis.ipynb       # 5 generative models, evaluation scorecard, visual comparisons
├── outputs/
│   ├── figures/              # Generated diagnostic plots (ROC curves, correlation heatmaps, cones)
│   ├── tables/               # Quantitative benchmark scorecards
│   └── Interim_Demo_Technical_Report.pdf  # Comprehensive 9-page technical report
├── src/
│   └── build_report_pdf.py   # Automated report compiler
├── .gitignore
└── README.md
```

---

## Quickstart

### 1. Environment Setup
Install required dependencies:
```bash
pip install numpy pandas matplotlib seaborn scipy scikit-learn statsmodels pgmpy copulas torch reportlab
```

### 2. Running the Notebooks
1. **Data Audit & Forensic Cleaning:**
   Open and execute `notebooks/01_DataAudit_Cleaning.ipynb` to audit raw records, apply Tukey extreme fences ($k = 3.0$), and generate clean train/test splits.
2. **Generative Model Benchmark:**
   Open and execute `notebooks/02_Stage1_Synthesis.ipynb` to train all 5 generative models, evaluate the multi-pillar scorecard, and plot comparative distributions.

---

## Stage 1 Interim Benchmark Results

Evaluated on the held-out real test set ($N = 442$, Real Training Ceiling ROC-AUC = $0.874$):

| Generator Model | 1D KS Similarity (↑) | 2D Corr Frobenius Error (↓) | 6-Category Structural Zero % (↓) | Cross-Feature Violations % (↓) | TSTR Test ROC-AUC (↑) | AUC Retention % |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **0. Naive Independent** | 0.985 | 7.18 | 9.75% | 0.06% | 0.434 | 49.6% |
| **1. Stratified Contingency** | 0.986 | 1.72 | 0.34% | 0.00% | 0.714 | 81.6% |
| **2. Gaussian Copula** | 0.980 | 1.86 | 0.57% | 0.11% | **0.811** | **92.7%** |
| **3. Bayesian Network** | 0.984 | 2.12 | 0.28% | 0.00% | 0.746 | 85.3% |
| **4. Deep TVAE (Xu et al.)** | 0.924 | 1.83 | **0.00%** | **0.00%** | 0.793 | 90.6% |

---

## Core References
- **Maier et al. (2025):** *LLMs Reproduce Human Purchase Intent via Semantic Similarity Elicitation of Likert Ratings* (`arXiv:2510.08338v3`).
- **Cheng, Piccardi, & Yang (2023):** *CoMPosT: Characterizing and Evaluating Caricature in LLM Simulations* (`arXiv:2310.11501v1`).
- **Bisbee et al. (2024):** *Synthetic Replacements for Human Survey Data? The Perils of Large Language Models* (`Political Analysis`, 32, 401–416).
- **Wang, Morgenstern, & Dickerson (2024):** *Large Language Models Cannot Replicate Human Consumers Without Behavioral Context* (`arXiv:2402.01908`).
- **Xu et al. (NeurIPS 2019):** *Modeling Tabular data using Conditional GAN* (`arXiv:1907.00503`).
