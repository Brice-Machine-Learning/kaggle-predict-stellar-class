# Notebook 03 — Feature Engineering

**Notebook:** `03_feature_engineering.ipynb`
**Objective:** Design and document useful predictors while avoiding data leakage.

> Self-study checklist. No implementation code or preselected modeling solution is provided.

## Checklist

### Plan transformations

- [ ] Review EDA findings and proposed transformations.
- [ ] Identify features that may require scaling.
- [ ] Identify skewed features.
- [ ] Determine whether missing-value treatment is necessary.
- [ ] Consider whether categorical encoding is needed.
- [ ] Identify redundant or potentially uninformative features.

### Engineer and select features

- [ ] Investigate scientifically meaningful feature combinations.
- [ ] Consider photometric color differences where appropriate.
- [ ] Assess whether transformations improve usefulness or interpretability.
- [ ] Evaluate whether certain features should be excluded.
- [ ] Record the reasoning behind each engineered feature.
- [ ] Avoid adding features without a testable rationale.

### Prevent leakage

- [ ] Establish a reproducible stratified validation strategy.
- [ ] Fit learned transformations only on the training portion of each split or fold.
- [ ] Keep the Kaggle test dataset separate from model development.
- [ ] Verify that identifiers and the target are not predictors.
- [ ] Document processing steps needed for inference.

### Deliverables

- [ ] Create a documented feature list.
- [ ] Record engineering decisions and assumptions.
- [ ] Establish a reproducible preprocessing workflow.
- [ ] Document rejected transformations and why.

## Reflection notes

**What did I learn?**


**What decisions did I make, and why?**


**What remains unresolved?**


**What should happen next?**

