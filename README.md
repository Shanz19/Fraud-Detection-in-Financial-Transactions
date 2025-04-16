# Fraud-Detection-in-Financial-Transactions
## Overview

This project tackles the challenge of identifying fraudulent financial transactions in a highly imbalanced dataset. It spans the full data‑mining pipeline—from raw data preprocessing and exploratory analysis, through feature engineering and model training, to hyperparameter tuning and final evaluation—yielding a robust Random Forest classifier with a balanced precision–recall trade‑off.

## Data Preprocessing & Feature Engineering

- **Time Features**  
  Derived transaction hour, day, week, month, year, and categorical periods (e.g., “morning”, “evening”) to capture temporal fraud patterns.  
- **Interaction Features**  
  Combined source, browser, and device type to surface suspicious cross‑category behaviors.  
- **User Proxy**  
  Without explicit customer or transaction IDs, fused customer age and account age to approximate user identity and detect behavioural anomalies.  
- **Risk Indicators**  
  Flagged high‑value transactions from new users and new‑device activity by established accounts.  
- **Outlier Treatment**  
  Rather than dropping extreme values (which often correspond to fraud), binned transaction amounts and age groups to preserve signal.  
- **Encoding & Selection**  
  - Label‑encoded low‑cardinality categoricals.  
  - Target‑encoded high‑cardinality features (>10 unique values).  
  - Removed features with pairwise correlation > 0.7.

## Handling Class Imbalance

- Fraud cases comprised just ~7.8% of all transactions.  
- Applied **SMOTE** to oversample the minority class, mitigating model bias toward non‑fraudulent transactions.

## Model Training & Tuning

- Tested multiple classifiers (Random Forest, LightGBM, XGBoost).  
- **Random Forest** emerged as the optimal choice due to its:
  - Robustness on skewed data
  - Ease of interpretability via feature‑importance scores
  - Lower sensitivity to noisy inputs  
- Conducted grid search for hyperparameter tuning (e.g., tree depth, number of estimators) to maximize F1.

## Evaluation Metrics

| Metric     | Validation Set | Test Set   |
|------------|----------------|------------|
| Precision  | 93%            | 93%        |
| Recall     | 48%            | 47%–49%    |
| F1 Score   | 64%            | 62%        |

> **Note:** High precision minimizes false alarms, protecting genuine customers; moderate recall reflects the trade‑off inherent to fraud detection.

## Alternative Models Considered

- **XGBoost & LightGBM**  
  - Achieved comparable accuracy but required more extensive tuning.  
  - Less interpretable, making it harder to justify predictions in a regulatory context.

## Key Takeaways

1. **Rich Feature Engineering** unlocks temporal and interaction patterns.  
2. **Binning vs. Dropping Outliers** preserves critical fraud signals.  
3. **Target Encoding** for high‑cardinality categoricals avoids the curse of dimensionality.  
4. **SMOTE** effectively addresses class imbalance but must be paired with careful validation.  
5. **Interpretability** is as vital as raw accuracy in real‑world fraud detection.

## Challenges & Future Work

- **Data Identifiers:** Incorporating true Customer/Transaction IDs would enhance behavioural tracking.  
- **Advanced Resampling:** Explore methods like ADASYN or cluster‑based oversampling.  
- **Deep Learning:** Investigate sequence models (RNNs/Transformers) for time‑series transaction data.  
- **Real‑Time Deployment:** Build a streaming pipeline for live transaction scoring and continuous model retraining.

## Conclusion

By integrating comprehensive preprocessing, targeted feature creation, and a carefully tuned Random Forest classifier, this project demonstrates a practical, effective approach to real‑world fraud detection—balancing precision with acceptable recall and offering clear paths for future enhancement.  
