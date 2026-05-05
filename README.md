# EEG-MLP-IRPSO: An Interpretable, Lightweight Framework for Early Parkinson's Disease Detection via Adaptive Feature Selection and Generative Augmentation

[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://www.python.org/)
[![TensorFlow 2.10](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)](https://www.tensorflow.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## Overview

This repository contains the complete source code for the paper:

> **EEG-MLP-IRPSO: An Interpretable, Lightweight Framework for Early Parkinson's Disease Detection via Adaptive Feature Selection and Generative Augmentation**  
> Kamyab Karimi, Ali Ghodratnama, Reza Tavakkoli-Moghaddam, Sara GhasemiRad, Niaz Wassan  
> *Cluster Computing, 2026*

We introduce **EEG-MLP-IRPSO**, a novel framework that synergizes multi-domain EEG feature extraction, a pioneering **Intelligent Relative Particle Swarm Optimization (IRPSO)** algorithm for optimal feature selection, and an optimized **Multilayer Perceptron (MLP)** classifier for early, non-invasive Parkinson's disease (PD) detection from EEG signals. The framework addresses critical challenges in EEG-based diagnosis, including high-dimensional feature spaces, class imbalance, data scarcity, and clinical interpretability.

### Key Contributions

- **IRPSO Algorithm**: A novel feature selection method featuring adaptive intelligence and dimension learning optimization (DLO), designed to overcome conventional challenges in high-dimensional EEG data.
- **Hybrid Data Augmentation**: A combined CTGAN + SMOTE strategy to address data scarcity and class imbalance.
- **Optimized MLP Classifier**: Hyperparameter-tuned via Keras Tuner, achieving **96.84% accuracy**, **97.87% precision**, and **99.52% AUC-ROC**.
- **SHAP-based Interpretability**: SHapley Additive exPlanations analysis confirming the clinical relevance of selected features.

---

## Repository Structure

```
EEG-MLP-IRPSO/
│
├── README.md
├── LICENSE
├── requirements.txt
│
├── notebooks/
│   ├── Part_1_Preprocessing_Feature_Extraction.ipynb
│   ├── Part_2_CTGAN_Augmentation_IRPSO_Selection.ipynb
│   ├── Part_3a_MLP_Classification_with_IRPSO.ipynb
│   └── Part_3b_MLP_Classification_without_IRPSO.ipynb
│
├── results/                 
└── data/
    └── README.md             
```

| Notebook | Description |
|----------|-------------|
| **Part 1** | EEG signal preprocessing, multi-domain feature extraction, and dimensionality reduction. |
| **Part 2** | CTGAN-based synthetic data generation, SMOTE oversampling, IRPSO feature selection with adaptive intelligence and DLO, and baseline evaluation with Gradient Boosting. |
| **Part 3a** | MLP classifier training and evaluation on IRPSO-selected features, Keras Tuner hyperparameter optimization, KS-test validation of synthetic data, SHAP analysis, and multi-model comparison. |
| **Part 3b** | Ablation study — identical MLP pipeline executed without IRPSO feature selection to quantify the contribution of the proposed feature selection stage. |

---

## Installation

```bash
git clone https://github.com/<your-username>/EEG-MLP-IRPSO.git
cd EEG-MLP-IRPSO
pip install -r requirements.txt
```

### Dependencies

- Python ≥ 3.9
- NumPy, Pandas, SciPy
- MNE (EEG signal processing)
- scikit-learn
- TensorFlow / Keras
- Keras Tuner
- CTGAN (`ctgan`)
- imbalanced-learn (`imblearn`)
- SHAP
- XGBoost
- Matplotlib, Seaborn

A complete list is provided in `requirements.txt`.

---

## Dataset

This study uses a publicly available resting-state EEG dataset of Parkinson's disease patients and healthy controls. Due to data redistribution policies, the raw dataset is not included in this repository.

**Access instructions:**  
> The dataset can be obtained from https://openneuro.org/datasets/ds002778/versions/1.0.5

After downloading, place the raw `.edf` / `.set` files in the `data/` directory before running Part 1.

---

## Reproducing Results

Execute the notebooks sequentially:

1. **Part 1** — Preprocesses raw EEG data and extracts multi-domain features → outputs `reduced_features_and_labels.csv`.
2. **Part 2** — Performs CTGAN + SMOTE augmentation and IRPSO feature selection → outputs `selected_features_irpso.npy` and `final_selected_data_irpso.csv`.
3. **Part 3a** — Trains and evaluates the optimized MLP on IRPSO-selected features with full SHAP analysis.
4. **Part 3b** — Runs the ablation study without IRPSO for comparative evaluation.

> **Note:** Random seeds are set (`random_state=42`) throughout the pipeline to ensure reproducibility. Minor numerical variations may occur across different hardware/GPU configurations.

---

## Results Summary

| Metric | With IRPSO | Without IRPSO |
|--------|-------------------------:|----------------------------:|
| Accuracy | **96.84%** | 90.25%* |
| Precision | **97.87%** | 91.73%* |
| AUC-ROC | **99.52%** | 96.65%* |

*\*Averaged across 5 runs; see Part 3b for full details.*

---

## Citation

If you use this code or find our work useful, please cite:

```bibtex
@article{karimi2025eegmlpirpso,
  title     = {EEG-MLP-IRPSO: An Interpretable, Lightweight Framework for Early 
               Parkinson's Disease Detection via Adaptive Feature Selection and 
               Generative Augmentation},
  author    = {Karimi, Kamyab and Ghodratnama, Ali and Tavakkoli-Moghaddam, Reza 
               and GhasemiRad, Sara and Wassan, Niaz},
  journal   = {[Journal Name]},
  year      = {[Year]},
  volume    = {[Volume]},
  pages     = {[Pages]},
  doi       = {[DOI]}
}
```

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## Contact

For questions or collaboration inquiries:

- **Kamyab Karimi** — [k.karimi@student.utwente.nl](mailto:k.karimi@student.utwente.nl)  
  Department of Electrical Engineering, Mathematics and Computer Science, University of Twente, Netherlands  

---

## Acknowledgments

We gratefully acknowledge the data providers and the open-source communities behind MNE, TensorFlow, SHAP, and CTGAN.
