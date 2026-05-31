# MetaLLM 🧬⚡

> An end-to-end deep learning framework for protein-to-metal-ion binding site prediction using protein language models.

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square)](https://python.org)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.11.0-orange?style=flat-square)](https://tensorflow.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## Overview

MetaLLM is a research framework that predicts whether a protein binds to metal ions, and where, using pretrained protein language model embeddings combined with deep learning classifiers. Understanding protein–metal interactions is critical to enzymatic catalysis, structural biology, and drug discovery.

This work leverages state-of-the-art transformer-based models — including **ESM (Evolutionary Scale Modeling)**, **ESMFold**, **ProtGPT2**, and **Progen2** — to extract rich sequence and structural representations, which are then fed into a binary classification pipeline.

---

## Repository Structure

```
MetaLLM/
├── notebooks/
│   ├── 01_esm_embeddings.ipynb               # ESM-based sequence embeddings
│   ├── 02_esmfold_positional.ipynb            # ESMFold + positional encoding
│   ├── 03_progen2.ipynb                       # Progen2 embeddings
│   ├── 04_protgpt2.ipynb                      # ProtGPT2 embeddings
│   └── 05_experiments.ipynb                   # Main experiments & evaluation
├── data/
│   └── metal_binding_data.xlsx                # Curated protein–metal binding dataset
├── validation/
│   └── independent_validation.zip             # Independent test set
├── Google_Colab_Setup.txt                     # Colab environment setup guide
├── requirements.txt                           # Python dependencies
└── README.md
```

> **Note:** The pretrained model weights (`metallm_model.h5`) are hosted externally. See [Model Weights](#model-weights) below.

---

## Key Features

- **Multiple protein LM backends** — ESM-1b, ESM-2, ESMFold, ProtGPT2, Progen2
- **Positional encoding integration** — combines structural and sequential information
- **Binary classification pipeline** — TensorFlow-based classifier for metal-binding prediction
- **Independent validation** — held-out test set for unbiased evaluation
- **Google Colab compatible** — reproducible experiments without local GPU requirements

---

## Dependencies

| Library         | Version |
|-----------------|---------|
| TensorFlow      | 2.11.0  |
| NumPy           | 1.23.5  |
| Pandas          | 1.5.3   |
| Scikit-learn    | 1.2.2   |
| Matplotlib      | 3.7.1   |
| Seaborn         | 0.12.2  |
| BioTransformers | 0.1.2   |
| fair-esm        | 0.4.0   |
| transformers    | 4.29.2  |
| Ray             | 2.6.3   |

---

## Quick Start

**1. Clone the repository**
```bash
git clone https://github.com/FairuzShadmaniShishir/MetaLLM.git
cd MetaLLM
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Run on Google Colab**

Open any notebook in `notebooks/` directly in Google Colab. Refer to `Google_Colab_Setup.txt` for the recommended runtime configuration (GPU, package installs).

---

## Model Weights

The trained model file is in the models folder:


---

## Results
 
All results reported as mean ± std over cross-validation folds.
 
### Precision
 
| Model | Calcium | Copper | Iron | Magnesium | Manganese | Zinc |
|-------|---------|--------|------|-----------|-----------|------|
| Raw Input | 0.62 ± 0.08 | 0.62 ± 0.28 | 0.80 ± 0.19 | 0.74 ± 0.09 | 0.72 ± 0.10 | 0.75 ± 0.06 |
| Raw Input + CNN | 0.76 ± 0.07 | 0.78 ± 0.10 | 0.89 ± 0.11 | 0.81 ± 0.08 | 0.82 ± 0.10 | 0.80 ± 0.05 |
| ProtTrans + CNN | 0.91 ± 0.04 | 0.91 ± 0.17 | 0.97 ± 0.02 | 0.94 ± 0.03 | 0.91 ± 0.04 | 0.94 ± 0.02 |
| ProtTrans + Positional (multi-hot) | 0.86 ± 0.03 | 0.78 ± 0.11 | 0.93 ± 0.05 | 0.90 ± 0.06 | 0.87 ± 0.05 | 0.88 ± 0.06 |
| ProtTrans (no positional) | 0.94 ± 0.02 | 0.86 ± 0.08 | 0.97 ± 0.02 | 0.91 ± 0.04 | 0.91 ± 0.05 | 0.90 ± 0.06 |
| ProtTrans + Positional (encoding) | 0.78 ± 0.03 | 0.75 ± 0.12 | 0.85 ± 0.13 | 0.79 ± 0.08 | 0.78 ± 0.06 | 0.80 ± 0.06 |
| ProGen2 + Positional (encoding) | **0.99 ± 0.02** | **1.00 ± 0.08** | **1.00 ± 0.02** | **0.97 ± 0.04** | **0.96 ± 0.05** | **0.99 ± 0.06** |
| ProtGPT2 + Positional (encoding) | 0.92 ± 0.02 | 1.00 ± 0.08 | 0.99 ± 0.02 | 0.92 ± 0.04 | 0.98 ± 0.05 | 0.94 ± 0.06 |
| ESMFold + Positional (encoding) | 0.96 ± 0.02 | 0.79 ± 0.08 | 0.91 ± 0.02 | 0.72 ± 0.04 | 0.75 ± 0.05 | 0.84 ± 0.06 |
| ESMFold + Positional (multi-hot) | 0.88 ± 0.02 | 0.81 ± 0.08 | 0.81 ± 0.02 | 0.72 ± 0.04 | 0.68 ± 0.05 | 0.85 ± 0.06 |
| ESM + Positional (multi-hot) | 0.94 ± 0.06 | 0.95 ± 0.08 | 0.99 ± 0.01 | 0.98 ± 0.01 | 0.96 ± 0.02 | 0.97 ± 0.01 |
| ESM + Positional (encoding) | 0.93 ± 0.02 | 0.94 ± 0.05 | 0.97 ± 0.03 | 0.92 ± 0.08 | 0.91 ± 0.04 | 0.92 ± 0.03 |
 
### Recall
 
| Model | Calcium | Copper | Iron | Magnesium | Manganese | Zinc |
|-------|---------|--------|------|-----------|-----------|------|
| Raw Input | 0.50 ± 0.13 | 0.29 ± 0.11 | 0.76 ± 0.11 | 0.77 ± 0.08 | 0.63 ± 0.12 | 0.74 ± 0.04 |
| Raw Input + CNN | 0.50 ± 0.14 | 0.44 ± 0.17 | 0.79 ± 0.08 | 0.78 ± 0.07 | 0.66 ± 0.14 | 0.75 ± 0.05 |
| ProtTrans + CNN | 0.82 ± 0.05 | 0.79 ± 0.10 | 0.79 ± 0.10 | 0.95 ± 0.01 | 0.82 ± 0.16 | 0.91 ± 0.02 |
| ProtTrans + Positional (multi-hot) | 0.77 ± 0.10 | 0.74 ± 0.06 | 0.89 ± 0.06 | 0.95 ± 0.02 | 0.82 ± 0.11 | 0.91 ± 0.02 |
| ProtTrans (no positional) | 0.87 ± 0.08 | 0.87 ± 0.08 | 0.92 ± 0.05 | 0.93 ± 0.03 | 0.82 ± 0.12 | 0.93 ± 0.04 |
| ProtTrans + Positional (encoding) | 0.70 ± 0.09 | 0.61 ± 0.07 | 0.72 ± 0.09 | 0.75 ± 0.04 | 0.65 ± 0.14 | 0.78 ± 0.03 |
| ProGen2 + Positional (encoding) | **0.99 ± 0.02** | **0.97 ± 0.08** | 0.88 ± 0.02 | 0.92 ± 0.04 | 0.72 ± 0.05 | **0.98 ± 0.06** |
| ProtGPT2 + Positional (encoding) | 0.92 ± 0.02 | 0.85 ± 0.08 | 0.79 ± 0.02 | **0.97 ± 0.04** | **0.96 ± 0.05** | 0.96 ± 0.06 |
| ESMFold + Positional (encoding) | 0.69 ± 0.02 | 0.88 ± 0.08 | 0.85 ± 0.02 | 0.83 ± 0.04 | 0.22 ± 0.05 | 0.93 ± 0.06 |
| ESMFold + Positional (multi-hot) | 0.66 ± 0.02 | 0.87 ± 0.08 | 0.87 ± 0.02 | 0.89 ± 0.04 | 0.42 ± 0.05 | 0.84 ± 0.06 |
| ESM + Positional (multi-hot) | 0.96 ± 0.02 | 0.97 ± 0.03 | **0.96 ± 0.04** | **0.99 ± 0.01** | 0.95 ± 0.03 | **0.98 ± 0.01** |
| ESM + Positional (encoding) | 0.86 ± 0.04 | 0.87 ± 0.03 | 0.88 ± 0.06 | 0.87 ± 0.02 | 0.79 ± 0.15 | 0.92 ± 0.02 |
 
### F1 Score
 
| Model | Calcium | Copper | Iron | Magnesium | Manganese | Zinc |
|-------|---------|--------|------|-----------|-----------|------|
| Raw Input | 0.55 ± 0.11 | 0.37 ± 0.11 | 0.78 ± 0.15 | 0.75 ± 0.08 | 0.66 ± 0.10 | 0.74 ± 0.03 |
| Raw Input + CNN | 0.60 ± 0.12 | 0.55 ± 0.16 | 0.84 ± 0.09 | 0.79 ± 0.07 | 0.72 ± 0.12 | 0.77 ± 0.02 |
| ProtTrans + CNN | 0.86 ± 0.05 | 0.84 ± 0.10 | 0.94 ± 0.03 | 0.94 ± 0.02 | 0.86 ± 0.13 | 0.93 ± 0.01 |
| ProtTrans + Positional (multi-hot) | 0.81 ± 0.05 | 0.75 ± 0.06 | 0.91 ± 0.04 | 0.92 ± 0.03 | 0.83 ± 0.07 | 0.90 ± 0.04 |
| ProtTrans (no positional) | 0.90 ± 0.04 | 0.86 ± 0.09 | 0.94 ± 0.02 | 0.92 ± 0.03 | 0.86 ± 0.08 | 0.91 ± 0.03 |
| ProtTrans + Positional (encoding) | 0.73 ± 0.05 | 0.67 ± 0.06 | 0.78 ± 0.09 | 0.77 ± 0.04 | 0.70 ± 0.11 | 0.79 ± 0.03 |
| ProGen2 + Positional (encoding) | **0.99 ± 0.02** | **0.98 ± 0.08** | 0.94 ± 0.02 | 0.94 ± 0.04 | 0.82 ± 0.05 | **0.99 ± 0.06** |
| ProtGPT2 + Positional (encoding) | 0.92 ± 0.02 | 0.92 ± 0.08 | 0.88 ± 0.02 | 0.94 ± 0.04 | **0.97 ± 0.05** | 0.95 ± 0.06 |
| ESMFold + Positional (encoding) | 0.80 ± 0.02 | 0.83 ± 0.08 | 0.88 ± 0.02 | 0.77 ± 0.04 | 0.34 ± 0.05 | 0.88 ± 0.06 |
| ESMFold + Positional (multi-hot) | 0.76 ± 0.02 | 0.84 ± 0.08 | 0.84 ± 0.02 | 0.80 ± 0.04 | 0.52 ± 0.05 | 0.85 ± 0.06 |
| ESM + Positional (multi-hot) | 0.95 ± 0.03 | 0.96 ± 0.04 | **0.97 ± 0.02** | **0.98 ± 0.01** | 0.96 ± 0.02 | **0.97 ± 0.01** |
| ESM + Positional (encoding) | 0.89 ± 0.02 | 0.90 ± 0.02 | 0.92 ± 0.04 | 0.89 ± 0.04 | 0.84 ± 0.10 | 0.92 ± 0.02 |
 
> **Best results per metal ion are bolded.** ProGen2 + Positional (encoding) achieves the highest precision overall, while ESM + Positional (multi-hot) delivers the most consistent F1 scores across all metal types.

---

## Citation

If you use this work, please cite:

```bibtex
@ARTICLE{11122592,
  author={Shishir, Fairuz Shadmani and Sarker, Bishnu and Rahman, Farzana and Shomaji, Sumaiya},
  journal={IEEE Transactions on Computational Biology and Bioinformatics}, 
  title={A Deep Learning Framework for Protein-to-Metal Binding Prediction Using Protein Language Models}, 
  year={2025},
  volume={22},
  number={6},
  pages={2575-2585},
  keywords={Proteins;Metals;Predictive models;Ions;Databases;Deep learning;Biological system modeling;Transformers;Encoding;Hidden Markov models;Metal binding site;deep learning;large language model;protein language model;transformers;bio-transformers},
  doi={10.1109/TCBBIO.2025.3595446}}
```

---

## Contact

**Fairuz Shadmani Shishir**
- 📧 shishir@ku.edu
- 📧 fsshishir95@gmail.com

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
