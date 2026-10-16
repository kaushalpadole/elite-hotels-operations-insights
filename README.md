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

# Basic EDA — 10 Questions

## 1. What is the average lead time for bookings?

**Answer:** The average lead time is **79.89 days**.

**Insight:** On average, bookings were made about 80 days before arrival. Lead time can help hotels understand advance-booking behavior and plan demand.

## 2. What is the distribution of bookings by hotel type?

| Hotel Type | Bookings | Share |
|---|---:|---:|
| City Hotel | 53,428 | 61.13% |
| Resort Hotel | 33,968 | 38.87% |
| **Total** | **87,396** | **100%** |

**Answer:** City Hotel accounts for the larger share of records, at **61.13%**.

**Insight:** City Hotel is more represented in this cleaned dataset. Hotel-specific demand and operational plans should take this difference into account.

## 3. How many bookings were canceled?

- Total booking records: **87,396**
- Canceled bookings: **24,025**
- Cancellation rate: **27.49%**
- Non-canceled bookings: **63,371**

**Answer:** There were **24,025 canceled bookings**, representing **27.49%** of the cleaned records.

**Insight:** Cancellation behavior is an important factor in occupancy forecasting and booking management.

## 4. What is the most common arrival month for bookings?

**Answer:** **August**, with **11,257 booking records**.

**Insight:** August is the most frequently represented arrival month in this dataset. Monthly demand patterns can inform staffing and resource planning.

## 5. What is the average number of special requests per booking?

**Answer:** **0.70 special requests per booking** on average.

**Insight:** Special requests provide a measure of guest requirements that can help with service planning. This average does not directly measure guest satisfaction.

## 6. Which country has the highest number of bookings?

**Answer:** **Portugal (PRT)**, with **27,453 booking records**.

**Insight:** Portugal is the leading country by booking count in the cleaned dataset. Country-level patterns may help describe the geographic mix of guests.

## 7. What is the average daily rate (ADR) for each hotel type?

| Hotel Type | Average ADR |
|---|---:|
| City Hotel | 110.99 |
| Resort Hotel | 99.03 |

**Answer:** City Hotel has the higher average ADR, at **110.99**, compared with **99.03** for Resort Hotel.

**Insight:** Average rates differ by hotel type. The dataset's currency is not specified in this analysis, so no currency symbol is applied.

## 8. What percentage of bookings required car parking spaces?

- Bookings requiring at least one parking space: **7,313**
- Total booking records: **87,396**
- Percentage: **8.37%**

**Answer:** **8.37%** of booking records indicate a parking-space requirement.

**Insight:** Parking demand appears in a minority of booking records. This metric can support parking-capacity planning.

## 9. What is the average stay duration in week nights and weekend nights?

| Stay Measure | Average Nights |
|---|---:|
| Week nights | 2.63 |
| Weekend nights | 1.01 |
| Total stay | 3.63 |

**Answer:** Guests stayed for an average of **2.63 week nights** and **1.01 weekend nights**, or approximately **3.63 nights in total**.

**Insight:** Stay duration can inform room-availability planning and demand analysis.

## 10. How many bookings were made through travel agents?

The notebook counted non-null values in the `agent` column.

- Booking records with an agent ID: **75,203**
- Share of all cleaned records: **86.05%**

**Answer:** **75,203 records (86.05%)** have a non-null agent ID.

**Insight:** Agent IDs are present for most booking records. A non-null ID indicates recorded agent information, but does not by itself explain the full booking journey.

---

# Medium EDA — 10 Questions

## 1. What is the cancellation rate for each hotel type?

| Hotel Type | Cancellation Rate |
|---|---:|
| City Hotel | 30.04% |
| Resort Hotel | 23.48% |

**Answer:** City Hotel has a cancellation rate of **30.04%**, compared with **23.48%** for Resort Hotel—a difference of **6.56 percentage points**.

**Insight:** Cancellation rates differ by hotel type. Further analysis could examine whether lead time, market segment, deposit type, or other characteristics help explain the difference.

## 2. What is the average ADR per market segment?

| Market Segment | Average ADR |
|---|---:|
| Online TA | 118.17 |
| Direct | 116.58 |
| Aviation | 100.17 |
| Offline TA/TO | 81.76 |
| Groups | 74.86 |
| Corporate | 68.15 |
| Undefined | 15.00 |
| Complementary | 3.05 |

**Answer:** **Online TA** has the highest average ADR (**118.17**), while **Complementary** has the lowest (**3.05**).

**Insight:** Average ADR varies substantially by market segment. These differences may reflect distinct booking and pricing arrangements; the lowest averages should be interpreted in light of what each segment represents. The currency is not specified.

## 3. What is the relationship between lead time and cancellation rate?

The notebook compared average lead time by cancellation status:

| Booking Status | Average Lead Time |
|---|---:|
| Not canceled (`is_canceled = 0`) | 70.10 days |
| Canceled (`is_canceled = 1`) | 105.72 days |

**Answer:** Canceled bookings had an average lead time **35.62 days longer** than non-canceled bookings.

**Insight:** Longer lead time is associated with cancellations in this descriptive comparison. This result alone does not prove that longer lead time causes cancellation.

## 4. Which distribution channel has the highest number of bookings?

| Distribution Channel | Booking Records |
|---|---:|
| TA/TO | 69,141 |
| Direct | 12,988 |
| Corporate | 5,081 |
| GDS | 181 |
| Undefined | 5 |

**Answer:** **TA/TO** has the most booking records, with **69,141**—approximately **79.11%** of all cleaned records.

**Insight:** TA/TO is the dominant distribution channel in this dataset. The channel mix may be useful when reviewing channel strategy and partner relationships.

## 5. What is the average number of previous cancellations by hotel type?

| Hotel Type | Average Previous Cancellations |
|---|---:|
| City Hotel | 0.04 |
| Resort Hotel | 0.02 |

**Answer:** City Hotel booking records have a higher mean number of previous cancellations (**0.04**) than Resort Hotel records (**0.02**).

**Insight:** The averages are low for both hotel types. This comparison describes previous cancellation history recorded for customers and does not explain the causes of those cancellations.

## 6. What is the trend of ADR over the years?

| Arrival Year | Average ADR |
|---|---:|
| 2015 | 92.16 |
| 2016 | 101.54 |
| 2017 | 118.71 |

**Answer:** Average ADR increased from **92.16 in 2015** to **118.71 in 2017**, an increase of approximately **28.8%** over that period.

**Insight:** The dataset shows an upward trend in average ADR across these arrival years. Further analysis would be needed to separate pricing changes from differences in hotel, month, and guest mix.

## 7. Which month has the highest revenue?

The notebook followed the project hint by summing `adr` for each arrival month.

| Month | Sum of ADR Values |
|---|---:|
| August | 1,698,412.48 |
| July | 1,363,146.03 |
| June | 929,859.68 |
| May | 929,040.10 |
| April | 819,368.35 |
| September | 749,823.65 |
| October | 625,117.56 |
| March | 613,132.35 |
| February | 455,472.02 |
| December | 417,921.11 |
| November | 363,408.53 |
| January | 328,748.13 |

**Answer according to the requested calculation:** **August** has the highest summed ADR value (**1,698,412.48**).

**Important limitation:** Summing ADR values is not the same as calculating actual total revenue. ADR is a rate metric; a proper revenue calculation would require an appropriate revenue measure, such as rate multiplied by relevant occupied nights, with the necessary booking and stay details.

## 8. What is the impact of special requests on ADR?

| Number of Special Requests | Average ADR |
|---:|---:|
| 0 | 99.67 |
| 1 | 109.65 |
| 2 | 118.57 |
| 3 | 125.07 |
| 4 | 131.09 |
| 5 | 129.98 |

**Answer:** Average ADR generally increases as the number of special requests rises from zero to four. The highest average is **131.09** for bookings with four requests; the average for five requests is **129.98**.

**Insight:** Special-request count has a positive descriptive association with ADR across most of these groups, but the pattern is not perfectly increasing. This does not establish that special requests cause higher rates.

## 9. What is the average stay duration for repeated guests versus new guests?

| Guest Group | Average Total Stay |
|---|---:|
| Not recorded as repeated (`0`) | 3.70 nights |
| Repeated guest (`1`) | 1.93 nights |

**Answer:** Guests not recorded as repeated guests stayed **3.70 nights** on average, compared with **1.93 nights** for repeated guests—a difference of **1.77 nights**.

**Insight:** In this dataset, the non-repeated-guest group has a longer average stay. This may help inform further investigation of guest behavior and loyalty, but does not establish why the difference exists.

## 10. Which room type has the highest number of bookings?

| Reserved Room Type | Booking Records |
|---|---:|
| A | 56,552 |
| D | 17,398 |
| E | 6,049 |
| F | 2,823 |
| G | 2,052 |
| B | 999 |
| C | 915 |
| H | 596 |
| L | 6 |
| P | 6 |

**Answer:** Reserved room type **A** is the most common, with **56,552 records**—approximately **64.71%** of cleaned records.

**Insight:** Room type A dominates the recorded reservations. The room-type codes are categorical labels; their specific features should not be inferred without a separate data dictionary.

---

# Advanced EDA — 5 Questions

## 1. What factors significantly impact the cancellation rate?

A logistic regression model was fitted using:
- `lead_time`
- `booking_changes`
- `total_of_special_requests`

The target variable was `is_canceled` (0 = not canceled, 1 = canceled).

| Predictor | Coefficient | P-value | Direction of Association |
|---|---:|---:|---|
| Lead time | +0.0050 | < 0.001 | Positive |
| Booking changes | -0.4944 | < 0.001 | Negative |
| Special requests | -0.3852 | < 0.001 | Negative |

**Model results:**
- Observations: **87,396**
- Pseudo R-squared: **0.0548**
- Model converged successfully.
- Likelihood-ratio test p-value: **< 0.001**

**Answer:** All three predictors were statistically significant in this model. Longer lead time was associated with higher cancellation odds, while booking changes and special requests were associated with lower cancellation odds, holding the other included predictors constant.

**Insight:** Lead time, booking changes, and special requests may help characterize cancellation risk. However, statistical association is not causation, and the pseudo R-squared indicates modest explanatory improvement over the intercept-only model. The model's predictive performance was not evaluated with a holdout set in this analysis.

## 2. How does ADR vary with the number of adults, children, and babies?

A multiple linear regression model was fitted with ADR as the outcome and `adults`, `children`, and `babies` as predictors.

| Predictor | Coefficient | P-value |
|---|---:|---:|
| Adults | +21.1778 | < 0.001 |
| Children | +38.6573 | < 0.001 |
| Babies | +6.7081 | < 0.001 |

**Model results:**
- Observations: **87,396**
- R-squared: **0.165**
- Adjusted R-squared: **0.165**
- Overall model F-statistic: **5,752**

**Answer:** All three guest-count variables had positive, statistically significant coefficients. Holding the other guest-count variables constant, one additional adult was associated with **21.18 ADR units** higher ADR; one additional child with **38.66 units** higher ADR; and one additional baby with **6.71 units** higher ADR.

**Insight:** Guest composition is associated with ADR in this model, but the model explains **16.5%** of observed ADR variation. Other variables—such as hotel type, season, market segment, and room characteristics—may also matter. The results describe associations rather than causal effects.

## 3. What is the impact of booking changes on guest satisfaction as indicated by special requests?

The notebook calculated the Pearson correlation between `booking_changes` and `total_of_special_requests`.

**Result:** **0.0161**

**Answer:** The correlation is positive but extremely weak, indicating almost no linear relationship between booking changes and the number of special requests in this dataset.

**Insight:** Booking changes alone are not a useful linear proxy for the number of special requests. Special requests are also only an indirect indicator of guest needs—not a direct measure of satisfaction—so this analysis cannot determine the effect on satisfaction.

## 4. What is the seasonal impact on booking cancellations?

| Arrival Month | Cancellation Rate |
|---|---:|
| January | 22.12% |
| February | 23.20% |
| March | 24.36% |
| April | 30.46% |
| May | 29.23% |
| June | 30.32% |
| July | 31.80% |
| August | 32.18% |
| September | 24.54% |
| October | 23.68% |
| November | 21.10% |
| December | 26.86% |

**Answer:**
- Highest cancellation rate: **August (32.18%)**
- Second-highest: **July (31.80%)**
- Lowest cancellation rate: **November (21.10%)**
- Difference between highest and lowest: **11.08 percentage points**

**Insight:** Cancellation rates vary by arrival month. Hotels could investigate higher-rate months when planning occupancy and cancellation policies. These descriptive results identify monthly differences but do not prove that seasonality itself causes cancellations.

## 5. How does the booking lead-time distribution vary between different market segments?

A box plot compared `lead_time` across market segments.

**Findings from the visualization:**
- **Groups** has a relatively high median lead time and a wide distribution.
- **Offline TA/TO** also shows relatively high lead times.
- **Online TA** has a moderate median and a wide spread.
- **Direct** and **Corporate** show relatively low median lead times, with some long-lead-time outliers.
- **Complementary** and **Aviation** have comparatively low median lead times.
- Several segments have outliers representing bookings made far in advance.

**Answer:** Lead-time distributions differ across market segments. Groups and Offline TA/TO appear to have relatively high median lead times, while several other segments have lower medians.

**Insight:** Different segments may have different booking windows. Hotels can use this information to investigate segment-specific booking behavior and improve demand forecasting and marketing plans. The `Undefined` segment should be interpreted cautiously because it may contain very few observations.

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
