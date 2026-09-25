# Customer Segmentation – Amazing International Airlines (AIAI)

Data Mining project developed at NOVA IMS (Master's in Data Science and Advanced Analytics, Fall 2025).

## Business Problem
AIAI operates in a highly competitive market and wanted to understand its loyalty programme members better, in order to replace generic marketing with personalised campaigns and improve retention. The goal was to identify distinct customer segments based on who the customers are and how they travel.

## Data
- **Customer database:** 16,9K loyalty programme members with demographic, financial and loyalty information (income, customer lifetime value, loyalty status, enrolment and cancellation dates).
- **Flights database:** 608,4K monthly records of flight activity (flights, companions, distance, points accumulated and redeemed).

## Approach (CRISP-DM)

### 1. Exploratory Data Analysis
- Data quality assessment: duplicate IDs, missing values and inconsistent enrolment/cancellation dates (a systematic ~850-day offset was detected and corrected).
- Aggregation of monthly flight records into customer-level features.
- Analysis of seasonality, loyalty points behaviour and customer value by loyalty tier.
- Rule-based classification of traveller types (Frequent, Regular, Seasonal, Occasional, Yearly).

### 2. Preprocessing
- Winsorising at the 1st and 99th percentiles for univariate outliers.
- **DBSCAN** for multivariate outlier detection, with epsilon chosen from a k-distance graph.
- Feature engineering (e.g. `ProgramDaysDuration`, `SoloFlightRatio`, seasonal flight counts), StandardScaler and removal of redundant or highly correlated features.

### 3. Segmentation Perspectives
- **Demographic / value:** Income, Customer Lifetime Value, ProgramDaysDuration, TotalFlights, TotalPointsRedeemed.
- **Behavioural:** seasonal flights, flights with companions, solo flight ratio, points ratio, monthly peaks of flights and points.

### 4. Clustering
- **K-Means** with the elbow method.
- **Hierarchical clustering**, comparing Ward, Complete, Average and Single linkage with R² (Ward performed best), plus dendrograms.
- **Self-Organising Maps**, with component planes, U-matrix and hit maps. Topographic error dropped by 76–81% after training.
- **Merging perspectives:** a cross-tabulation of demographic and behavioural clusters, followed by hierarchical clustering on their centroids, gave the final solution.

## Results – 4 Customer Personas

| Persona | Share | Profile | Strategy |
|---|---|---|---|
| **Consistent Loyalists** | 62.4% | Frequent flyers across all seasons, often with companions | Retention, companion rewards, exclusive tier |
| **Low-Engagement Users** | 21.4% | Newer members with minimal activity | Re-activation offers and double-points kickstart |
| **Solo Travellers** | 10.6% | Travel alone, low seasonal activity and redemption | Solo-focused perks and lower redemption thresholds |
| **High-Value Potential** | 5.6% | Steady participation and high potential for premium services | Premium upgrades and personalised high-end services |
