# Elite Hotels: Insights for Optimized Operations

## Project Overview

This project analyzes hotel booking data to understand booking patterns, cancellations, guest behavior, pricing, and market-segment differences. The analysis follows the **25 Basic, Medium, and Advanced EDA questions** in the *Elite Hotels : Insights for Optimized Operations* project brief.

The business objective is to turn booking data into practical insights that can support occupancy planning, cancellation management, pricing analysis, and guest-service decisions.

## Business Questions

The project explores:
- When and how far in advance guests book.
- Which hotel types, arrival months, countries, channels, and room types are most represented.
- How cancellation rates differ across hotel types and months.
- How ADR varies by hotel type, market segment, year, and guest composition.
- Whether booking changes, special requests, and lead time are associated with cancellation behavior.

## Dataset

- **Dataset:** Hotel Booking Demand
- **Source:** [Kaggle — Hotel Booking Demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand)
- **Original shape:** 119,390 rows × 32 columns
- **Shape after cleaning:** 87,396 rows × 32 columns

The dataset contains booking information for City Hotels and Resort Hotels, including arrival dates, lead time, cancellation status, guest counts, market segment, distribution channel, room type, ADR, parking requirements, and special requests.

## Tools and Technologies

- Python
- Pandas
- Matplotlib
- Seaborn
- Statsmodels
- Kaggle Notebook

## Data Cleaning and Preparation

The notebook applied the following steps:

1. **Handled missing children values:** Filled the four missing values in `children` with `0`. This is an assumption that missing values represent no children; the source data does not confirm the true values.
2. **Checked duplicate rows:** Found 31,994 exact duplicate rows.
3. **Removed exact duplicates:** Dropped those rows, leaving 87,396 rows and no remaining exact duplicates.
4. **Converted the reservation status date:** Converted `reservation_status_date` to a datetime type.
5. **Retained other missing values:** Missing values in `agent`, `company`, and `country` were not removed or imputed in this notebook.

**Data-cleaning note:** Removing 31,994 exact duplicates is a substantial reduction. The results below describe the cleaned dataset used in the notebook. For a production analysis, it would be worth validating whether every repeated row is truly a duplicate rather than a legitimate repeated booking record.

---



# Overall Findings

1. **City Hotel is more represented:** It accounts for **61.13%** of cleaned booking records.
2. **Cancellations are substantial:** **27.49%** of cleaned booking records were canceled.
3. **Cancellation rates vary by hotel type:** City Hotel's rate (**30.04%**) is higher than Resort Hotel's (**23.48%**).
4. **August is a key month in the analysis:** It has the most arrival records and the highest monthly cancellation rate (**32.18%**).
5. **Booking channel mix is concentrated:** TA/TO accounts for approximately **79.11%** of cleaned records.
6. **ADR varies across groups:** City Hotel has higher average ADR than Resort Hotel, and Online TA has the highest average ADR among the listed market segments.
7. **Lead time is associated with cancellations:** Canceled bookings have a longer average lead time than non-canceled bookings, and lead time has a positive coefficient in the logistic regression.
8. **Guest composition is associated with ADR:** Adults, children, and babies all have positive coefficients in the multiple regression model.
9. **Booking changes and special requests have almost no linear correlation:** Pearson's correlation is **0.0161**.
10. **Market segments differ in booking windows:** The box plot shows variation in lead-time distributions across segments.

## Business Recommendations

- **Improve cancellation monitoring:** Track cancellation rates by hotel type, arrival month, and lead time.
- **Plan for monthly variation:** Use arrival patterns and cancellation rates to support staffing and occupancy forecasting.
- **Review distribution channels:** TA/TO is the dominant channel in this dataset; evaluate channel performance alongside ADR, cancellation rates, and acquisition costs where available.
- **Investigate pricing variation:** Compare ADR across hotel types, market segments, and years while accounting for differences in season and guest composition.
- **Plan operational resources:** Use parking requirements, stay duration, and special-request frequency to inform service and capacity planning.
- **Improve future modeling:** Evaluate models on held-out data and consider additional predictors before using them for operational decisions.

## Limitations

- The results describe the cleaned dataset and should not automatically be generalized to all hotels or current booking patterns.
- Four missing `children` values were filled with zero as an assumption.
- Removing 31,994 exact duplicate rows materially changed the dataset size; duplicate handling should be validated for any production use.
- Missing values in `agent`, `company`, and `country` were retained.
- ADR sums are not equivalent to actual total revenue.
- Correlation and regression coefficients identify associations, not causal effects.
- The logistic regression was not evaluated using a separate test set, and its pseudo R-squared is modest.
- The linear regression explains 16.5% of ADR variation and shows highly non-normal residual diagnostics in the notebook output.
- The dataset's currency was not specified in this analysis.

## Conclusion

This project used exploratory analysis, visualization, logistic regression, multiple linear regression, and correlation analysis to answer the 25 questions in the Elite Hotels brief. The results highlight differences in booking volume, cancellation behavior, ADR, seasonal patterns, and lead time across hotel types and market segments.

The findings can support further investigation into cancellation management, demand planning, pricing, and channel strategy. Before operational use, the analysis should be strengthened by validating duplicate handling, adding relevant predictors, and testing model performance on unseen data.
