# CS 598 DLH Final Project - Reproduction Study
This repository contains code for CS598 DL4H reproducibility project in Spring 2023 (Team 80).

## Introduction
The objective of this reproducibility project is to replicate and verify the results presented in the paper [_Benchmarking Deep Learning Architectures for predicting Readmission to the ICU and Describing patients-at-Risk_](https://www.nature.com/articles/s41598-020-58053-z)
by _Sebastiano Barbieri, James Kemp, Oscar Perez-Concha, Sradha Kotwal, Martin Gallagher, Angus Ritchie, Louisa Jorm_
(_Nature Scientific Reports_).


To reproduce the results of the paper’s experiments, we re-used 
3 neural network architectures provided by the authors (https://github.com/sebbarb/time_aware_attention) to predict readmission to the ICU. 
We also added two ablations without timestamped embeddings to examine their impact on the model performance.

## Data descriptions
The MIMIC-III v1.4 (Medical Information Mart for Intensive Care III) dataset contains a diverse and very large population of ICU
patients. The dataset was obtained through the PhysioNet platform:

https://physionet.org/content/mimiciii/1.4

## Instructions

### Dependencies
Use the command below to install the packages according to the configuration file
```
pip install -r requirements.txt

```

### Data download instruction
The [MIMIC-III Clinical Database 1.4](https://physionet.org/content/mimiciii/1.4/) is available via [PhysioNet](https://physionet.org/) by request.
Please follow [this instruction](https://physionet.org/content/mimiciii/1.4/#files) to access the files. 

### Data preprocessing
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

### Training
Use settings in `hyperparameters.py` to specify the model you would like to train and tune hyperparameters.

To train the chosen model, run the following command:

```
python train.py
```

### Evaluation

To evaluate the trained model, run the following command:

```
python test.py
```

## Results

The paper's three models were replicated, and the results are as follows:


| Model                         | Average Precision    | AUROC                | F1-Score             | Sensitivity          | Specificity          |
|-------------------------------| ---------------------- | ---------------------- | ---------------------- | ---------------------- | ---------------------- |
| ODE + Attention               | 0.296 [0.287,0.305] | 0.715 [0.712,0.717] | 0.341 [0.337,0.346] | 0.643 [0.633,0.654] | 0.681 [0.671,0.691] |
| Attention (concatenated time) | 0.286 [0.277,0.295] | 0.707 [0.704,0.71] | 0.327 [0.322,0.331] | 0.724 [0.711,0.737] | 0.594 [0.581,0.606] |
| ODE + RNN + Attention         | 0.275 [0.27,0.279] | 0.718 [0.715,0.72] | 0.342 [0.338,0.346] | 0.707 [0.695,0.718] | 0.632 [0.62,0.644] |


The following results were achieved for the ablated models:

| Name                | Average Precision   | AUROC               | F1-Score             | Sensitivity          | Specificity         |
| --------------------- |---------------------|---------------------| ---------------------- | ---------------------- |---------------------|
| RNN | 0.311 [0.302,0.32]  | 0.734 [0.731,0.737] | 0.356 [0.351,0.36] | 0.693 [0.685,0.701] | 0.680 [0.672,0.688] |
| RNN + Attention | 0.300 [0.292,0.309] | 0.730 [0.727,0.733] | 0.353 [0.349,0.357] | 0.664 [0.658,0.671] | 0.696 [0.691,0.702] |
