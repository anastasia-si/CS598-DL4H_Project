# CS 598 DLH Final Project - Reproduction Study
This repository contains code for CS598 DL4H reproducibility project.

## Introduction
The reproduction study is based on the publication:

_Benchmarking Deep Learning Architectures for predicting Readmission to the ICU and Describing patients-at-Risk_

by _Sebastiano Barbieri, James Kemp, Oscar Perez-Concha, Sradha Kotwal, Martin Gallagher, Angus Ritchie, Louisa Jorm_

_Nature Scientific Reports_


To reproduce the results of the paper’s experiments, we re-used 
3 (TODO: update number) neural network architectures provided by the authors (https://github.com/sebbarb/time_aware_attention) to predict readmission to the ICU. 
We also added two ablations without timestamped embeddings to examine their impact on the model performance.

## Data descriptions
The MIMIC-III v1.4 (Medical Information Mart for Intensive Care III) dataset contains a diverse and very large population of ICU
patients. The dataset was obtained through the PhysioNet platform:

https://physionet.org/content/mimiciii/1.4

## Instructions

Install requirements by running: 
```
pip install -r requirements.txt

```

Unzip the downloaded MIMIC-III dataset and pre-process it by running the following scripts:

```
python preprocessing_reduce_charts.py
python preprocessing_reduce_outputs.py
python preprocessing_merge_charts_outputs.py
python preprocessing_ICU_PAT_ADMIT.py
python preprocessing_CHARTS_PRESCRIPTIONS.py
python preprocessing_DIAGNOSES_PROCEDURES.py
python preprocessing_create_arrays.py
```

Use settings in `hyperparameters.py` to specify the model you would like to train and tune hyperparameters.

To train and evaluate the chosen model, run the following commands:

```
python train.py
```

and

```
python test.py
```