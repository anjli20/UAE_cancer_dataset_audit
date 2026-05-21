# Auditing a UAE Healthcare ML Dataset

A methodology study on the UAE Cancer Patient dataset (10,000 patients, 21 features). An initial model predicting patient 
outcomes reached 63% accuracy. After auditing the pipeline, three flaws were found — target leakage, a time-dependent label, 
and pre-split resampling — that inflated the result. Once corrected, performance dropped to AUC ≈ 0.49, and a permutation test 
(p = 0.875) confirmed the dataset has no extractable predictive signal.

**Tools:** scikit-learn · lifelines · imbalanced-learn · statsmodels · XGBoost

## Summary of findings

| Metric | Original (leaky) | Corrected | Real-data benchmark |
|--------|------------------|-----------|---------------------|
| Accuracy | 63% | 90% (trivial) | — |
| ROC-AUC (mortality) | not reported | 0.487 | 0.65–0.85 |
| Cox concordance | not reported | 0.553 | 0.65–0.75 |
| Permutation test p | not reported | 0.875 | < 0.05 if signal exists |
| Predictors significant after correction | not reported | 0 of 21 | many |

After fixing the leakage and contamination, all models converged to coin-flip performance. The dataset is 
most plausibly synthetic, with outcomes assigned independently of patient features.
