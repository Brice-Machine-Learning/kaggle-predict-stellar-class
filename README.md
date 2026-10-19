# Predicting Stellar Class

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.12+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![uv](https://img.shields.io/badge/uv-Package_Manager-DE5FE9?style=for-the-badge&logo=uv&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-Data_Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Numerical_Computing-013243?style=for-the-badge&logo=numpy&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Machine_Learning-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C?style=for-the-badge)
![Kaggle](https://img.shields.io/badge/Kaggle-Competition-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white)
![PyCharm](https://img.shields.io/badge/PyCharm-IDE-000000?style=for-the-badge&logo=pycharm&logoColor=white)

**Kaggle Playground Series | Season 6, Episode 6**

A multiclass classification project focused on predicting astronomical object classes using tabular machine learning. The project emphasizes a reproducible workflow, careful exploratory data analysis, appropriate validation, and model comparison.

## Competition

- **Competition:** [Predicting Stellar Class](https://www.kaggle.com/competitions/playground-series-s6e6)
- **Organizer:** Kaggle, Tabular Playground Series
- **Competition period:** June 1–30, 2026 (closed; late submissions)
- **Task:** Predict `class` as `GALAXY`, `STAR`, or `QSO`
- **Primary metric:** Balanced accuracy

## Project Objectives

1. Inspect and understand the training and test datasets.
2. Identify missing values, class imbalance, unusual distributions, and potential data quality issues.
3. Build leakage-resistant preprocessing and validation pipelines.
4. Establish a baseline classifier and evaluate more capable models.
5. Compare models using balanced accuracy and class-level diagnostics.
6. Generate a reproducible Kaggle submission file.

## Machine Learning Problem

This is a **supervised multiclass classification** task with three possible labels:

| Label | Astronomical object |
| --- | --- |
| `GALAXY` | Galaxy |
| `STAR` | Star |
| `QSO` | Quasi-stellar object (quasar) |

The dataset is synthetically generated for Kaggle's Tabular Playground Series. Feature names, distributions, and record counts should be verified against the downloaded competition files rather than assumed.

## Evaluation

Kaggle evaluates submissions using **balanced accuracy**, the mean recall across the three classes:

\[
\text{Balanced Accuracy} = \frac{1}{3}\sum_{c \in \{\text{GALAXY, STAR, QSO}\}} \frac{TP_c}{TP_c + FN_c}
\]

Balanced accuracy prevents a model from appearing strong solely because it predicts the most common class well.

## Workflow

| Stage | Purpose | Status |
| --- | --- | --- |
| Data ingestion | Load and validate competition files | In progress |
| Exploratory data analysis | Examine schema, missingness, target distribution, and features | In progress |
| Preprocessing | Handle missing values, encode or transform features as needed | Planned |
| Baseline modeling | Establish a reproducible reference score | Planned |
| Model development | Compare candidate classification algorithms | Planned |
| Evaluation | Assess balanced accuracy, confusion matrix, and per-class recall | Planned |
| Submission | Produce and validate Kaggle submission CSV | Planned |

*Update the status column as work progresses.*

## Repository Organization

See [project architecture](docs/01_architecture/00_architecture.md) for a detailed description of the repository structure, including directories for raw and processed data, notebooks, scripts, and documentation.

## Getting Started

1. Download the competition data from the [Kaggle Data page](https://www.kaggle.com/competitions/playground-series-s6e6/data).
2. Place the source CSV files in `data/raw/` (or update paths to match the repository).
3. Create and activate a Python environment and install the project's dependencies.
4. Run the ingestion and EDA notebooks before proceeding to modeling.
5. Use a stratified validation split and report balanced accuracy before creating submissions.

The exact environment commands and dependency list should be added once the repository configuration is confirmed.

## Submission Format

The submission must contain one prediction per test-set ID, with the following columns:

```csv
id,class
577347,STAR
577348,GALAXY
577349,STAR
```

Check that the IDs match the test dataset, the row count is correct, and predictions belong to the three allowed classes.

## Documentation

See [project-overview.md](project-overview.md) for the problem definition, validation design, EDA plan, modeling roadmap, and project completion criteria.

## Citation

Yao Yan, Walter Reade, Elizabeth Park. *Predicting Stellar Class*. Kaggle, 2026. https://www.kaggle.com/competitions/playground-series-s6e6
