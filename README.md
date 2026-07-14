# 🚖 Bluebird Taxi Fleet Optimization & Fraud Mitigation Analysis

An end-to-end data analytics project focused on optimizing fleet performance and uncovering B2B revenue leakage for **Bluebird Group**, Indonesia's largest taxi service provider. Utilizing a multi-source relational infrastructure containing 300,000 trip records [source: 2], this project pipelines raw operations data into actionable strategic insights via an optimized **Python-to-BigQuery-to-Looker Studio** architecture [source: 1, 2].

---

## 📊 Business Executive Summary

Based on the unified operational dataset across 7 distinct taxi pools [source: 1]:
* **Total Completed Trips**: 300,000 [source: 1, 2]
* **Total Active Drivers**: 12,000 [source: 1]
* **Total B2B Corporate Clients**: 500 [source: 1, 2]
* **Total Gross Income**: IDR 37.51 Billion [source: 1]
* **Average Driver Rating**: 4.80 / 5.00 [source: 1]

---

## 🛠️ Strategic Business Challenges Solved

### 1. Driver Performance: Potential Cheat Trips (Fraud)
By establishing a strict temporal condition mapping (`meter_start_time < booking_time`), the data layer flagged an anomaly category where drivers manipulated the taximeter setup [source: 2]:
* **Insight**: Roughly **3% (9,000 trips)** of total volume were identified as cheated trips [source: 2]. 
* **Pool Impact**: The cheat distribution is evenly split across regional hubs, heavily led by the **Bluebird Regular** fleet service tier (~70.2%) [source: 1].
* **Statistical Correlation**: A Seaborn scatter plot analysis proved there is **no correlation** between a driver's historical customer rating and their propensity to commit taximeter fraud [source: 2].

### 2. Fleet Optimization: Idle Time & Supply-Demand Mismatch
An analysis of operational efficiency revealed massive driver downtime between completed drop-offs and incoming bookings [source: 1]:
* **The Anomaly**: Around **17.4% of trip sequencing** registered an overlapping anomaly (getting a new booking before closing the previous order) [source: 1].
* **The Downtime Problem**: By isolating regular activity, the median driver wait time between trips sits at a staggering **284.94 minutes (~4.7 hours)** [source: 2]. Drivers are averaging only **1.07 completed trips per day** [source: 1].
* **The Solution**: An optimization framework estimates that by lowering driver wait times, the optimum productivity capacity should reach **5.5 to 5.8 trips/day per driver** [source: 1]. Implementing this allows Bluebird to reduce the active daily driver dispatch requirement from ~220 down to **40–43 drivers per pool**, significantly cutting operational overhead [source: 1].

### 3. B2B Corporate Report: Fraud Mitigation
Corporate accounts using **eVoucher Corporate** payment methods (making up 20.1% of total transaction shares) were heavily audited [source: 1]:
* **Abuse Discovery**: **31.6%** of total corporate fare claims occurred on suspect parameters (weekend travel or late-night trips after 10:00 PM) without verified professional justification [source: 2].
* **Data Leakage**: **15%** of all corporate e-Voucher trips were processed with a **missing Company ID**, representing an immediate billing reconciliation risk [source: 1].
* **Top Offenders**: The audit ranked top leakage sources, exposing multiple client companies in the Mining, Media, and Banking spaces experiencing a **Fraud Percentage over 42%** on employee voucher usage [source: 1].

---

## 💻 Tech Stack & Engineering Pipeline

- **Data Processing & ETL**: `Pandas`, `NumPy`, `PyArrow` (Handling string alignment, converting localized `Asia/Jakarta` timestamp layers, and data restructuring) [source: 2].
- **Data Warehousing Layer**: `Google BigQuery` (`pandas-gbq` and service account API structures utilized to run table formatting and complex window function queries) [source: 2].
- **Exploratory Data Analysis**: `Matplotlib`, `Seaborn` [source: 2].
- **Business Intelligence**: `Looker Studio` (For translating BigQuery matrices into real-time tracking boards) [source: 1, 2].

---

## 📁 Project Repository Structure

```text
bluebird-data-analysis/
│
├── data/
│   ├── bb_corporate_clients.csv  # 500 verified B2B client firms
│   ├── bb_drivers.csv           # 12,000 driver performance indices
│   └── bb_trips.parquet         # 300,000 binary trip records
│
├── notebooks/
│   └── bluebird_capstone.ipynb  # Primary ETL and BigQuery injection notebook
│
├── README.md                    # Project documentation
└── requirements.txt             # Environment dependencies
