# Data Dictionary — Predicting Stellar Class

**Competition:** Kaggle Playground Series, Season 6 Episode 6  
**Task:** Multiclass classification (`GALAXY`, `STAR`, `QSO`)  
**Status:** Provisional, inferred definitions. **Not an official Kaggle data dictionary.**

## Overview

The dataset uses names associated with astronomical sky coordinates, five-band photometry, and spectroscopic measurements. The competition uses synthetically generated data, so values, categories, and relationships may differ from physical survey observations. Confirm units, valid ranges, and category meanings against actual records before relying on these definitions.

## Feature definitions

| Column | Best-guess meaning | Likely data type | Confidence | Notes / checks |
|---|---|---|---|---|
| `id` | Unique row or observation identifier | Integer | High | Check uniqueness; generally exclude from predictors. |
| `alpha` | Right ascension (sky position, analogous to longitude) | Numeric | High | Commonly degrees, 0–360; verify observed range. |
| `delta` | Declination (sky position, analogous to latitude) | Numeric | High | Commonly degrees, −90 to +90; verify range. |
| `u` | Apparent magnitude in the ultraviolet/near-UV *u* filter | Numeric | High | Lower magnitude means brighter; inspect missing/sentinel values. |
| `g` | Apparent magnitude in the blue-green *g* filter | Numeric | High | One of the standard `ugriz` photometric bands. |
| `r` | Apparent magnitude in the red *r* filter | Numeric | High | One of the standard `ugriz` photometric bands. |
| `i` | Apparent magnitude in the far-red/near-IR *i* filter | Numeric | High | One of the standard `ugriz` photometric bands. |
| `z` | Apparent magnitude in the near-infrared *z* filter | Numeric | High | **Not the same as `redshift`**, which is also often symbolized by z. |
| `redshift` | Relative shift in observed spectral wavelengths | Numeric | High | Often defined as (observed wavelength / rest wavelength) − 1; may be spectroscopic, but provenance is unverified. |
| `spectral_type` | Categorical descriptor of an object's spectrum or spectral grouping | Categorical | Low | **Exact categories and generation rules unknown.** Inspect unique values and cross-tabulate with `class`. |
| `galaxy_population` | Categorical grouping or population descriptor associated with galaxies | Categorical | Low | **Exact definition unknown.** May represent a simulated grouping; inspect values, missingness, and relationship with `class`. |
| `class` | Target astronomical object category | Categorical | High | Expected labels: `GALAXY`, `STAR`, `QSO` (quasi-stellar object/quasar). Present in training data, not the competition test features. |

## Astronomical context

### Coordinates

`alpha` and `delta` describe location on the celestial sphere. They may capture survey footprint or selection effects rather than intrinsic object properties. Their physical interpretation does not establish their predictive usefulness.

### Photometric magnitudes

The `u`, `g`, `r`, `i`, and `z` bands measure brightness through different filters. In the astronomical magnitude system, **smaller values correspond to brighter observations**. Differences such as `u − g` and `g − r` are *color indices* and can reflect the shape of an object's measured spectrum. Whether these are useful features is an empirical question.

### Redshift

Redshift is conventionally written as:

$$
 z_{\mathrm{redshift}} = \frac{\lambda_{\mathrm{observed}} - \lambda_{\mathrm{rest}}}{\lambda_{\mathrm{rest}}}
$$

It can be associated with cosmic expansion or line-of-sight motion. Its relationship with the target may be strong, but should be measured rather than assumed.

### Target classes

- **GALAXY:** A gravitationally bound system of stars, gas, dust, and dark matter.
- **STAR:** An individual stellar object.
- **QSO:** A quasi-stellar object, generally a luminous active galactic nucleus (quasar).

## Important unknowns

1. Whether the synthetic features preserve original survey units and realistic ranges.
2. The allowed categories and intended semantics of `spectral_type`.
3. The allowed categories and intended semantics of `galaxy_population`.
4. Whether either categorical feature was derived from the target or would reveal it indirectly.
5. Whether missing values or unusual numerical values encode survey-specific sentinels.
6. Whether `id` is a purely arbitrary identifier or reflects data-generation order.

## EDA verification checklist

- [ ] Record each column's actual dtype and observed range.
- [ ] Check missing counts and percentages for every feature.
- [ ] Verify `id` uniqueness and exclude it from initial modeling.
- [ ] List unique values and frequencies for `spectral_type`.
- [ ] List unique values and frequencies for `galaxy_population`.
- [ ] Compare those categories with `class` to identify possible leakage or label proxies.
- [ ] Check ranges of `alpha` and `delta` against expected coordinate conventions.
- [ ] Inspect photometric magnitude distributions and anomalous values.
- [ ] Compare `redshift` distributions across target classes.
- [ ] Record verified interpretations separately from hypotheses.

## References for background, not confirmation of this dataset

- [Kaggle competition](https://www.kaggle.com/competitions/playground-series-s6e6)
- [Sloan Digital Sky Survey](https://www.sdss.org/)
- [SDSS imaging filters](https://www.sdss.org/instruments/camera/)

> **Documentation policy:** Do not promote an inferred definition to a verified fact without supporting evidence. In particular, `spectral_type` and `galaxy_population` remain provisional until their categories and provenance are established.
