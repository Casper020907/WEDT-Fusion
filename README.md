# WEDT-Fusion
Code For WEDT-Fusion
WEDT-Fusion
Wavelet-Enhanced Dual-Branch Temporal Fusion Network for Multivariate Time Series Classification

Overview

This repository provides the official implementation of:

WEDT-Fusion: Wavelet-Enhanced Dual-Branch Temporal Fusion Network for Multivariate Time Series Classification

WEDT-Fusion is a neural architecture designed for multivariate time series classification (MTSC) under non-stationary conditions.

Different from existing approaches that separately model temporal representations and inter-channel dependencies, WEDT-Fusion aims to preserve the interaction among:

local transient events,
surrounding temporal contexts,
adaptive channel relationships.

The framework integrates:

Mask-aware SWT-guided scale proposal
Dual-branch temporal representation learning
Bidirectional cross-branch temporal fusion
Adaptive Kendall-guided inter-channel graph learning

to jointly capture multi-scale temporal patterns and dynamic variable dependencies.

Architecture

The overall architecture consists of four major components:

1. SWT-guided Scale Proposal

The model first performs stationary wavelet decomposition:

Wavelet basis: db4
Decomposition: SWT
Scale selection based on wavelet energy

The selected scales provide adaptive temporal resolutions for subsequent feature extraction.

2. Dual Temporal Branch Encoder

WEDT-Fusion contains two complementary branches:

Scale-aware Branch

Captures:

long-range temporal structures
multi-resolution patterns
periodic behaviors
Transient-aware Branch

Captures:

local fluctuations
short-term discriminative events
abrupt temporal changes
3. Bidirectional Temporal Fusion

The two branches exchange information through:

multi-head cross attention
bidirectional feature interaction

This allows temporal events to retain their contextual information during fusion.

4. Adaptive Kendall-guided Graph Learning

A graph module is introduced to model dynamic channel dependencies.

The graph construction combines:

training-set Kendall correlation prior
sample-dependent adaptive edge weighting

The learned graph enables:

adaptive inter-variable reasoning
structure-aware classification
Repository Structure
WEDT-Fusion/
│
├── data_provider/
│   ├── data_factory.py
│   ├── data_loader.py
│   └── uea.py
│
├── exp/
│   ├── exp_basic.py
│   ├── exp_classification.py
│
├── layers/
│   ├── Embed.py
│   ├── Conv_Blocks.py
│   └── graph related modules
│
├── models/
│   ├── TimeCasper.py
│   └── __init__.py
│
├── scripts/
│   └── experiment scripts
│
├── checkpoints/
│
├── run.py
│
├── runseeds.py
│
├── requirements.txt
│
├── README.md
│
└── LICENSE
Requirements

Python:

Python >= 3.9

Main dependencies:

torch
torch-geometric
numpy
scipy
scikit-learn
pandas
pywavelets
sktime
einops

Install:

pip install -r requirements.txt
Dataset Preparation

WEDT-Fusion is evaluated on:

UEA Multivariate Time Series Classification Archive

Download datasets and organize them as:

dataset/
└── UEA/
    ├── ArticularyWordRecognition/
    ├── AtrialFibrillation/
    ├── ...
Training

Example:

python run.py \
--task_name classification \
--is_training 1 \
--model TimeCasper \
--data UEA \
--data_path ArticularyWordRecognition \
--seed 2021
Multiple Seeds Evaluation

Run:

python runseeds.py

The default evaluation averages results across multiple random seeds.

Experimental Results

The model is evaluated using:

Accuracy
Macro-F1
Average ranking

Evaluation protocol:

28 UEA datasets
multiple random seeds
dataset-level statistical analysis
Citation


This project is released under the MIT License.

See LICENSE for details.

Acknowledgement

This repository is built upon:

Time-Series-Library (TSLib)

We sincerely thank the authors of TSLib for providing an excellent open-source framework for time-series research.
