# Uber NCR Analysis — EDA

EDA on 160K+ Delhi-NCR ride-hailing bookings — demand, cancellation, and festival/event patterns in 2024.

## Overview

This project is an exploratory data analysis (EDA) of **160,609 ride-hailing bookings** across Delhi-NCR in 2024, examining how time, vehicle type, and Indian festivals/events relate to ride demand, completion, and cancellation behavior.

Full title: **Spatiotemporal Analysis of Ride-Hailing Demand and Cancellation Patterns in Delhi-NCR**

The analysis is exploratory rather than predictive — the goal is to surface genuine statistical patterns (and openly report where assumed patterns *don't* hold up), not to build a forecasting model.

## Dataset

| | |
|---|---|
| **Name** | NCR Uber Ride Data with Festivals and Events 2024 |
| **Source** | [Kaggle — CRAZYELON](https://www.kaggle.com/datasets/crazyelon/ncr-uber-ride-data-with-festivals-and-events-2024) |
| **Size** | 160,609 ride-booking records, 29 variables |
| **Geography** | Delhi-NCR, India |
| **Time period** | January – December 2024 |
| **License** | CC BY-SA 4.0 (attribution required, derivatives shared under same/compatible license) |
| **Type** | Publicly available secondary dataset — not personally collected, not officially provided by Uber |

Key fields: booking date/time, booking status, vehicle type, pickup/drop location, ride distance, booking value, average vehicle arrival time (VTAT), average customer/trip turnaround time (CTAT), driver/customer ratings, payment method, cancellation reasons, and event/festival tags (Diwali, Holi, Eid, Wedding Season, Monsoon, etc.).

## Project Structure

```
├── data/
│   └── ncr_rides_final_event_dataset_2024.csv
├── notebooks/
│   └── ncr_eda.ipynb
├── NCR_Ride_EDA_Report.md      # Full written report with findings
└── README.md
```

## Methodology

1. **Data cleaning** — treating missing values as structural rather than erroneous. Most "missingness" in this dataset directly encodes booking outcome (e.g. a cancelled ride has no fare or distance recorded because no trip occurred).
2. **Feature engineering** — time-of-day buckets, peak-hour flags, weekend indicators, completion flag.
3. **Univariate analysis** — distribution of booking status, vehicle type, payment method, and numeric ride metrics.
4. **Temporal analysis** — ride volume and completion rate by hour, weekday, and month; overlay with festival/event periods.
5. **Cancellation analysis** — customer vs. driver cancellation reasons, and the relationship between wait time (VTAT) and cancellation.
6. **Statistical testing** — chi-square tests (categorical associations) and ANOVA (numeric differences across groups).
7. **Segmentation** — K-Means clustering on ride distance, fare, and timing metrics.

## Key Findings

- **Overall completion rate: 62.06%**, with driver cancellations (17.94%) far outpacing customer cancellations (7.01%).
- **Evening hours (17:00–19:00) see the highest ride volume**, but demand volume does not predict lower completion — cancellation risk is spread across the day, not concentrated at peak hours.
- **Wait time (VTAT) predicts customer cancellations but not driver cancellations.** Customers who cancel wait 12.50 min on average vs. 8.51 min for completed rides — but driver-cancelled rides average just 7.50 min, meaning drivers tend to cancel *quickly*, not after a long wait.
- **Vehicle type and event/festival type show no statistically significant effect on completion likelihood** (chi-square p = 0.183 and p = 0.799 respectively) — though event type *does* significantly affect fare (ANOVA p < 0.001), with festivals like Diwali and Dussehra showing notably higher average booking values than Normal Days.
- **Near-zero correlation across all numeric fields** (distance, fare, wait time, ratings) — an unusual pattern for real-world ride data, discussed openly in the report as a dataset limitation rather than glossed over.
- **K-Means clustering (k=4)** reveals a distinct premium-fare segment (8.8% of rides, avg ₹1,408) that isn't explained by trip distance — segments separate mainly by service-timing characteristics rather than distance.

See [`NCR_Ride_EDA_Report.md`](./NCR_Ride_EDA_Report.md) for the full write-up with all statistics, tables, and reasoning.

## Tools & Libraries

- **Python** — Pandas, NumPy (data processing)
- **Matplotlib, Seaborn** — visualization
- **SciPy** — chi-square and ANOVA testing
- **Scikit-learn** — K-Means clustering
- **Plotly / Power BI** — interactive dashboard

## Getting Started

```bash
git clone https://github.com/aadeeshsanghi/Uber_ncr_analysis-EDA-.git
cd Uber_ncr_analysis-EDA-
pip install -r requirements.txt
jupyter notebook notebooks/ncr_eda.ipynb
```

## Limitations

- Dataset covers only calendar year 2024 — no year-over-year trend analysis possible.
- No geographic coordinates — spatial analysis is limited to named-location frequency counts, not true geospatial mapping.
- No external variables (real-time traffic, weather, driver supply) to explain demand or cancellation fluctuations.
- Near-zero correlation among numeric fields suggests these may be independently/synthetically generated rather than reflecting real-world causal ride mechanics — findings should be read as statistical associations within this dataset, not causal claims about Uber's actual operations.
- Customer and Booking identifiers are treated as anonymized; no attempt is made to re-identify individuals.

## License

This project's code is available under the MIT License. The underlying dataset is licensed CC BY-SA 4.0 by its original provider on Kaggle — attribution required, derivatives must be shared under the same or a compatible license.

## Author

**Aadeesh Sanghi**
CSE (Data Science), VIT Vellore
[LinkedIn](#) · [GitHub](https://github.com/aadeeshsanghi)
