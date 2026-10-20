# Project Overview: Predicting Stellar Class

## 1. Project Summary

**Predicting Stellar Class** is a supervised machine learning project based on Kaggle's **Playground Series, Season 6 Episode 6**. The objective is to classify astronomical observations into one of three categories: `GALAXY`, `STAR`, or `QSO`.

The competition uses a synthetically generated tabular dataset and evaluates predictions with **balanced accuracy**. The competition closed June 30, 2026; the project can continue as a learning and experimentation exercise, with late submissions where supported.

**Competition:** https://www.kaggle.com/competitions/playground-series-s6e6

## 2. Problem Definition

### Objective

Given the available predictor columns for an observation, estimate its stellar class.

- **Learning type:** Supervised learning
- **Task:** Multiclass classification
- **Target:** `class`
- **Allowed labels:** `GALAXY`, `STAR`, `QSO`
- **Evaluation metric:** Balanced accuracy
- **Submission key:** `id`

The `id` column is used to identify submission rows and should not automatically be treated as a predictive feature. Inspect the actual dataset schema before selecting features.

### Success Criteria

A successful project should deliver:

1. A documented and reproducible data ingestion process.
2. EDA findings that explain relevant data characteristics and quality issues.
3. A valid baseline and at least one additional model for comparison.
4. A validation procedure designed to avoid target leakage.
5. Balanced accuracy results with per-class recall and confusion-matrix analysis.
6. A correctly formatted submission file.
7. Clear documentation of decisions, experiments, limitations, and results.

## 3. Data Source and Characteristics

The data originates from Kaggle's Tabular Playground Series, which provides synthetic datasets inspired by real-world data. Synthetic generation can preserve useful statistical patterns but does not guarantee that all distributions and relationships match actual astronomical observations.

Expected competition artifacts commonly include:

| File | Role |
| --- | --- |
| `train.csv` | Labeled observations used for training and validation |
| `test.csv` | Unlabeled observations requiring predictions |
| `sample_submission.csv` | Expected output structure |

**Important:** Confirm filenames, column types, feature definitions, dataset dimensions, and missing-value behavior from the downloaded files. These are not established by the competition description alone.

### Data Handling Principles

- Preserve the original downloaded files unchanged.
- Keep raw data separate from processed data.
- Avoid committing large or restricted competition datasets to Git.
- Fit imputation, scaling, encoding, and feature selection on training folds only.
- Track the random seed and validation strategy for reproducibility.

## 4. Exploratory Data Analysis

EDA should answer specific questions before modeling begins.

### Dataset Structure

- Record the shapes of training and test datasets.
- Review feature names, types, sample rows, and descriptive statistics.
- Check duplicate rows and duplicate identifiers.
- Compare train and test schemas and distributions.

### Missing Data

Calculate missing counts and proportions per feature:

```python
missing_summary = pd.DataFrame({
    "Missing Count": df.isna().sum(),
    "Missing Percentage": df.isna().mean() * 100,
})

missing_summary = (
    missing_summary[missing_summary["Missing Count"] > 0]
    .sort_values("Missing Percentage", ascending=False)
)
```

`isna()` returns Boolean values. Because Python and pandas treat `True` as 1 and `False` as 0 for this aggregation, `.mean()` returns the missing fraction; multiplying by 100 expresses it as a percentage.

### Target Analysis

- Measure the frequency and percentage of each target class.
- Assess whether class imbalance makes ordinary accuracy misleading.
- Check class-conditional feature distributions for potentially informative patterns.

### Feature Analysis

- Inspect numeric ranges, skew, and outliers.
- Review categorical levels if categorical columns are present.
- Examine relationships among predictors.
- Identify candidate transformations and features, documenting why each might help.

**EDA deliverable:** A concise findings section listing observed issues, relevant plots, and implications for preprocessing and modeling.

## 5. Preprocessing Strategy

Determine preprocessing from the actual dataset rather than assuming every step is necessary.

Potential operations include:

- Remove identifiers from model features unless there is a validated reason to retain them.
- Impute missing values when the selected algorithm requires it.
- Encode categorical predictors if present and required by the algorithm.
- Scale numeric variables for algorithms sensitive to feature magnitude.
- Consider class weighting or sampling only when validation evidence supports it.
- Use scikit-learn pipelines to prevent preprocessing leakage.

Do not fit preprocessing on the full labeled dataset before splitting into training and validation sets.

## 6. Validation and Evaluation

### Primary Metric: Balanced Accuracy

For three classes, balanced accuracy is the arithmetic mean of class-specific recall:

$$
BA = \frac{1}{3}(R_{GALAXY} + R_{STAR} + R_{QSO})
$$

where:

$$
R_c = \frac{TP_c}{TP_c + FN_c}
$$

This metric gives equal weight to each class, regardless of its frequency.

### Recommended Validation Design

1. Establish a **stratified train/validation split** as an initial baseline.
2. Keep the same split when comparing early model candidates.
3. Consider **Stratified K-Fold cross-validation** for more reliable model selection.
4. Apply all learned preprocessing within each training fold.
5. Avoid repeated manual tuning against a final holdout set.

### Diagnostics

Alongside balanced accuracy, examine:

- Confusion matrix
- Per-class recall
- Classification report
- Cross-validation mean and variability
- Training versus validation performance where relevant

These diagnostics help identify whether the model systematically misses one astronomical class.

## 7. Modeling Roadmap

| Phase | Candidate approach | Purpose |
| --- | --- | --- |
| Baseline | Dummy classifier | Establish a simple reference |
| Initial model | Logistic regression | Provide an interpretable benchmark |
| Nonlinear model | Random forest or histogram gradient boosting | Capture nonlinear relationships |
| Additional experiments | Gradient boosting libraries, if available | Explore further performance improvements |
| Final selection | Best validated pipeline | Generate test predictions |

These are **proposed experiments**, not completed results. Model selection should reflect the actual feature types, computational resources, and cross-validation evidence.

Track experiments using a consistent record:

| Experiment | Features / preprocessing | Model | Validation balanced accuracy | Notes |
| --- | --- | --- | --- | --- |
| Baseline | To be determined | Dummy classifier | Pending | Reference score |
| Model 1 | To be determined | Logistic regression | Pending | Initial benchmark |
| Model 2 | To be determined | Tree-based classifier | Pending | Nonlinear comparison |

## 8. Submission Workflow

Once a final pipeline is selected:

1. Refit the selected pipeline on the full labeled training dataset.
2. Generate predictions for the competition test dataset.
3. Construct a CSV with columns `id` and `class` in that order.
4. Verify row count, ID alignment, null predictions, and permitted labels.
5. Save the submission and document the model version used.

Example:

```csv
id,class
577347,STAR
577348,GALAXY
577349,STAR
```

A late submission may be possible through Kaggle, but competition availability and scoring should be confirmed on the competition page.

## 9. Reproducibility and Documentation

Document the following as the project develops:

- Python and package versions
- Environment setup and execution commands
- Dataset provenance and local storage conventions
- Random seeds and validation folds
- Preprocessing and feature engineering decisions
- Model configurations and experiment results
- Submission filename and corresponding experiment

Keep exploratory work in notebooks and move reusable transformations or modeling logic into Python modules when it becomes stable.

## 10. Current Status and Next Steps

**Current focus:** Data ingestion and exploratory data analysis. No completed modeling results are assumed in this overview.

Suggested immediate sequence:

1. Finish schema, missingness, duplicates, and target-distribution checks.
2. Summarize findings that influence preprocessing.
3. Establish the stratified validation procedure.
4. Train and evaluate a dummy baseline.
5. Compare initial candidate models against that baseline.

## 11. Scope and Limitations

- This is a competition-oriented classification exercise, not a validated scientific astronomy classifier.
- Synthetic training data may differ from real telescope observations.
- A strong leaderboard result does not establish out-of-distribution reliability.
- Model interpretations should be presented cautiously and grounded in observed features.

## 12. Reference

Yao Yan, Walter Reade, Elizabeth Park. *Predicting Stellar Class*. Kaggle, 2026. https://www.kaggle.com/competitions/playground-series-s6e6

Metric reference: https://scikit-learn.org/stable/modules/generated/sklearn.metrics.balanced_accuracy_score.html
