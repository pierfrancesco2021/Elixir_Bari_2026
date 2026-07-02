# Elixir_Bari_2026
# Microbiome ML

This repository contains two Jupyter notebooks for a hands-on teaching activity on machine learning with synthetic microbiome data.

The goal is not only to train a classifier, but to make students reason about the main methodological risks in microbiome ML: compositional data, sparsity, prevalence filtering, batch effects, leakage, validation strategy, model comparison, and interpretability.

## Notebooks

### `synthetic_data_generator.ipynb`

This notebook generates a synthetic microbiome dataset for the exercise.

It creates:

- a student-facing CSV containing microbial count data, `health_status`, and `batch`;
- an instructor-only answer key containing the true health-associated taxa and the true batch-associated taxa.

The dataset is deliberately designed to contain both biological signal and technical structure. The biological signal is modest and distributed across several taxa, while the batch effect is stronger. This allows students to discover that unsupervised methods and machine-learning models may capture batch-related variation instead of, or together with, the biological signal.

Main configurable parameters include:

- number of samples and taxa;
- class imbalance through `CLASS_PROBS`;
- number of batches;
- strength of the health signal;
- strength of the batch effect;
- degree of confounding between `health_status` and `batch`.

Run this notebook first to generate the CSV files used in the main analysis.

### `microbiome_ml.ipynb`

This is the main teaching notebook.

Students load the synthetic microbiome dataset and go through a decision-game workflow covering:

- data inspection and class balance;
- prevalence filtering;
- compositional preprocessing with relative abundance and CLR transformation;
- PCA, PCoA, clustermap, and k-means clustering;
- baseline supervised modelling;
- comparison of accuracy, balanced accuracy, F1-score, ROC-AUC, PR curves, and confusion matrices;
- model comparison under identical preprocessing and cross-validation;
- supervised feature selection and leakage;
- random cross-validation versus batch-grouped cross-validation;
- SHAP-based interpretation of model predictions.

The notebook is structured around short discussion blocks. Students are asked to interpret results before seeing the explanation, so that each methodological issue emerges from the analysis rather than being stated upfront.

## Suggested workflow

1. Open and run `synthetic_data_generator.ipynb`.
2. Save the generated student CSV.
3. Open `microbiome_ml.ipynb`.
4. Load the generated CSV.
5. Work through the notebook section by section.
6. Use the instructor answer key only at the end, if you want to reveal which top SHAP features were true biological signals and which were batch artifacts.

