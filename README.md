# European Airport ATFM Delays

Analysis of arrival ATFM (Air Traffic Flow Management) delays at European airports, using EUROCONTROL open data, with unsupervised and supervised machine learning.

**Notebook:** [ATFM_delay_analysis.ipynb](ATFM_delay_analysis.ipynb)

## Data

- **Source:** [EUROCONTROL Aviation Intelligence Unit – Airport arrival ATFM delays](https://ansperformance.eu/data/)
- **Period:** 2022–2024, 301,044 airport-days
- **Content:** daily arrivals and arrival ATFM delay minutes per airport, broken down by delay cause (weather, aerodrome capacity, ATC capacity, ATC staffing etc.)

## Questions

1. Which airports and causes generate the most arrival ATFM delay?
2. Can airports be grouped by their delay-cause profile?
3. Can we predict, one day ahead, whether an airport will have arrival ATFM delay?

## Methods

- Data cleaning and exploratory analysis with **pandas** and **matplotlib**
- **Unsupervised learning:** k-means clustering of airports by delay-cause profile, with a PCA projection for visualisation
- **Supervised learning:** logistic regression, random forest and gradient boosting (**scikit-learn**), compared with a naive baseline, using a time-based train/test split (train 2022–2023, test 2024)

## Key results

- **Weather (41%)** and **aerodrome capacity (26%)** cause two-thirds of airport arrival ATFM delay, followed by ATC capacity (14%) and ATC staffing (8%).
- The highest average delay per arrival is at Lisbon (4.4 min), London Gatwick (3.8), Tel Aviv (3.1), Amsterdam Schiphol (2.9) and Athens (2.9).
- Four airport clusters emerge: **staffing-driven**, **weather and aerodrome capacity-driven**, **ATC capacity-driven** and **airspace management-driven**. Each calls for a different type of mitigation.
- The ML models predict next-day delay with **ROC AUC ≈ 0.88**, against 0.76 for the baseline ("tomorrow will be like today"). The three models perform almost equally well, so a simple, interpretable model is enough.

| Model | ROC AUC | F1 |
|---|---|---|
| Baseline (yesterday) | 0.760 | 0.695 |
| Logistic regression | 0.874 | 0.736 |
| Random forest | 0.876 | 0.742 |
| Gradient boosting | 0.877 | 0.725 |

## Limitations and next steps

The models use only historical airport-level data. A natural next step would be to add meteorological data (METAR/TAF), since weather is the main cause of delay. Other extensions would be to include en-route ATFM delays and to predict delay minutes (regression).

## How to run

Open the notebook in [Google Colab](https://colab.research.google.com/) and run all cells. The data is downloaded directly from EUROCONTROL.

---
*Author: Daniela Șchiopu*
