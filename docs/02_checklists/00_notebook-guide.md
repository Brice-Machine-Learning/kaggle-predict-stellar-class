# Predicting Stellar Class — Notebook Study Guide

Kaggle Playground Series S6E6 · Target: `class` (`GALAXY`, `STAR`, `QSO`) · Primary metric: **balanced accuracy**.

## Learning approach

- [ ] Attempt each task independently before asking for help.
- [ ] Record a hypothesis before investigating a pattern.
- [ ] Explain results in plain language rather than relying only on plots or metrics.
- [ ] Keep raw competition files unchanged.
- [ ] Prevent leakage: fit learned preprocessing on training folds only; do not use the Kaggle test set to make modeling decisions.
- [ ] Complete each notebook with findings, decisions, and open questions.

## Notebook sequence

- [ ] [01 — Data Ingestion](01_data_ingestion.md) — Understand the structure, contents, and integrity of the supplied datasets before analysis.
- [ ] [02 — Exploratory Data Analysis](02_exploratory_data_analysis.md) — Explore the target distribution, feature behavior, relationships, and scientific context.
- [ ] [03 — Feature Engineering](03_feature_engineering.md) — Design and document useful predictors while avoiding data leakage.
- [ ] [04 — Baseline Modeling](04_baseline_modeling.md) — Establish a trustworthy benchmark before tuning sophisticated models.
- [ ] [05 — Model Experiments](05_model_experiments.md) — Test hypotheses systematically and compare candidate models fairly.
- [ ] [06 — Model Evaluation](06_model_evaluation.md) — Evaluate the selected pipeline, generate a valid Kaggle submission, and document conclusions.

## Working agreement

Use AI to explain concepts, critique reasoning, or provide hints when stuck, not to generate the notebook solutions.

## Important validation note

Explore the data, but define validation boundaries before using model results to choose features or transformations. Keep a final holdout untouched if you choose to use one.

## Completion

- [ ] Document the final modeling methodology.
- [ ] Record baseline and final balanced accuracy.
- [ ] Validate submission columns and class labels.
- [ ] Summarize limitations and future experiments.
