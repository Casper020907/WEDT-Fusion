# WEDT-Fusion

## Wavelet-Enhanced Dual-Branch Temporal Fusion Network for Multivariate Time Series Classification


<p align="center">
<img src="figures/framework.png" width="850">
</p>


## Overview

This repository provides the official implementation of:

> **WEDT-Fusion: Wavelet-Enhanced Dual-Branch Temporal Fusion Network for Multivariate Time Series Classification**

WEDT-Fusion is a neural network framework designed for **multivariate time series classification (MTSC)**, particularly for non-stationary sequences with complex temporal variations and dynamic inter-channel dependencies.

Existing approaches usually learn temporal representations and channel relationships separately, which may weaken the interaction between local events, temporal contexts, and variable dependencies.

To address this issue, WEDT-Fusion introduces a unified temporal-relational modeling framework consisting of:

- **Mask-aware SWT-guided scale proposal**
- **Dual-branch temporal representation learning**
- **Bidirectional cross-branch temporal fusion**
- **Adaptive Kendall-guided inter-channel graph learning**

The proposed framework jointly models:

- transient temporal events,
- multi-scale temporal contexts,
- adaptive channel interactions.


---

# Architecture

The framework contains four main components.


## 1. Mask-aware SWT-guided Scale Proposal

WEDT-Fusion first performs stationary wavelet decomposition to extract multi-scale temporal information.

The scale proposal module:

- adopts Stationary Wavelet Transform (SWT),
- uses `db4` wavelet basis,
- calculates wavelet-domain energy,
- selects informative temporal scales adaptively.


The selected scales provide temporal resolutions for subsequent feature extraction.


---

## 2. Dual-Branch Temporal Encoder


WEDT-Fusion contains two complementary temporal branches.


### Scale-aware Temporal Branch

This branch focuses on:

- long-range temporal dependencies,
- periodic patterns,
- multi-scale temporal structures.


### Transient-aware Temporal Branch

This branch captures:

- local abrupt changes,
- discriminative transient events,
- short-term temporal variations.


The two branches provide complementary temporal representations.


---

## 3. Bidirectional Cross-Branch Fusion


To preserve the interaction between temporal events and contextual information, WEDT-Fusion introduces bidirectional cross attention.

The fusion module enables:

- information exchange between branches,
- adaptive feature alignment,
- contextual enhancement of temporal representations.


---

## 4. Adaptive Kendall-guided Graph Learning


The graph module models dynamic dependencies among variables.

It combines:

1. Training-set Kendall correlation prior

2. Sample-dependent adaptive graph refinement


The learned graph captures:

- dynamic channel relationships,
- structure-aware feature propagation,
- inter-variable dependencies.


---

# Repository Structure


```
WEDT-Fusion/
│
├── data_provider/
│   ├── data_factory.py
│   ├── data_loader.py
│   └── uea.py
│
├── exp/
│   ├── exp_basic.py
│   └── exp_classification.py
│
├── layers/
│   ├── Embed.py
│   ├── Conv_Blocks.py
│   └── graph_modules/
│
├── models/
│   ├── TimeCasper.py
│   └── __init__.py
│
├── scripts/
│   └── experiment configurations
│
├── checkpoints/
│
├── results/
│
├── run.py
│
├── runseeds.py
│
├── requirements.txt
│
├── environment.yml
│
├── LICENSE
│
└── README.md
```


---

# Installation


## Environment

Recommended environment:

```
Python >= 3.9
PyTorch >= 2.0
CUDA >= 11.7
```


Install dependencies:

```bash
pip install -r requirements.txt
```


or using conda:

```bash
conda env create -f environment.yml

conda activate wedt-fusion
```


---

# Dataset Preparation


WEDT-Fusion is evaluated on the:

**UEA Multivariate Time Series Classification Archive**


Download datasets from:

```
https://www.timeseriesclassification.com/
```


Organize datasets as:


```
dataset/
│
└── UEA/
    │
    ├── ArticularyWordRecognition/
    ├── AtrialFibrillation/
    ├── BasicMotions/
    └── ...
```


---

# Training


## Single Experiment


Example:


```bash
python run.py \
--task_name classification \
--is_training 1 \
--model TimeCasper \
--data UEA \
--data_path ArticularyWordRecognition \
--seed 2021
```


---

## Multiple Random Seeds


To reproduce the reported results:


```bash
python runseeds.py
```


The final performance is averaged over multiple random seeds.


---

# Evaluation Metrics


The model is evaluated using:


- Accuracy
- Macro-F1
- Average ranking


Experimental protocol:

- 28 UEA datasets
- multiple random seeds
- dataset-level statistical analysis


---

# Reproducibility


All experimental configurations, training procedures,
and evaluation protocols required to reproduce the results
are provided in this repository.


The implementation follows the experimental settings
described in the corresponding paper.


---

# Citation


If you find this repository useful, please cite:


```bibtex
@article{wedt_fusion2026,
  title={WEDT-Fusion: Wavelet-Enhanced Dual-Branch Temporal Fusion Network for Multivariate Time Series Classification},
  author={Author Name},
  journal={Neural Networks},
  year={2026}
}
```


---

# License


This project is released under the MIT License.


See:

```
LICENSE
```

for details.


---

# Data Availability


The datasets used in this study are publicly available from:

```
UEA Multivariate Time Series Classification Archive

https://www.timeseriesclassification.com/
```


---

# Code Availability


The source code of WEDT-Fusion is publicly available at:


```
https://github.com/yourname/WEDT-Fusion
```


The archived version is available through Zenodo:


```
DOI:
https://doi.org/10.5281/zenodo.xxxxxxx
```


---

# Funding


This research received no external funding.


---

# Acknowledgement


This repository is built upon the open-source framework:

- Time-Series-Library (TSLib)


We sincerely thank the authors of TSLib
for providing an excellent platform for time-series research.


---

# Contact


For questions and discussions:


```
Email:
your_email@example.com
```
