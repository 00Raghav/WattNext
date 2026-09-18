# WattNext Learning Log

## Day 1 — Project Setup and Dataset Exploration

### Completed

- Renamed the project to WattNext
- Created the project directory structure
- Created a Jupyter notebook
- Loaded the smart meter dataset using Pandas
- Inspected the first rows
- Checked the dataset shape
- Checked column names
- Checked data types
- Checked missing values

### Dataset Initial Findings

- Approximately 3.95 million rows
- 6 columns
- No missing values detected in the initial check
- Timestamp column: `x_Timestamp`
- Consumption column: `t_kWh`
- Consumer identifier: `meter`

### Concepts Learned

- DataFrame
- Rows and columns
- Dataset shape
- Data types
- Missing values
- Jupyter notebooks
- Relative file paths

### Questions to Investigate

- What does each column represent?
- What is the time interval between readings?
- Does `t_kWh` represent energy per interval or cumulative energy?
- How many unique consumers are present?
- Are there duplicate timestamps?

## Milestone: Sensor Anomaly Investigation

### Findings
- Suspicious voltage readings: 349,793 (8.86%).
- Suspicious frequency readings: 344,622 (8.73%).
- Maximum voltage: 654.5 V.
- Maximum frequency: 177.3 Hz.
- Zero-energy readings with nonzero current: 103,675 (2.63%).
- BR46 and BR52 have high zero-energy/nonzero-current percentages.

### Decision
- Original raw data will be preserved.
- No readings have been deleted.
- Suspicious values will be considered during feature engineering and modeling.
- Further investigation may be performed if necessary.


## Milestone: First K-Means Clustering Experiment

### Features Used
- 24 hourly average energy consumption values per meter.
- Each row represents one meter.
- Hourly profiles were normalized by each meter's average consumption.

### Model
- Algorithm: K-Means Clustering
- Tested K values: 2 to 8
- Selected initial K: 2
- Random state: 42
- Silhouette score for K=2: 0.2265

### Results
- Cluster 0: 15 meters
- Cluster 1: 23 meters
- Cluster 0 total energy: 19,414.132 kWh
- Cluster 1 total energy: 57,217.438 kWh

### Initial Interpretation
- Cluster 0 shows a stronger daytime consumption pattern.
- Cluster 1 shows relatively stronger nighttime consumption.
- The clusters are preliminary because the silhouette score is relatively low.

### Output
- Saved meter-level clustering results to:
  `data/processed/meter_clusters.csv`

  ## Milestone: Reliability-Filtered Clustering

### Filtering
- Original meters: 38
- Excluded meters: 5
- Reliable meters: 33
- Exclusion threshold: More than 50% zero-energy readings

### Model Comparison
- Original K=2 silhouette score: 0.2265
- Reliable K=2 silhouette score: 0.2895
- Reliable K=3 silhouette score: 0.2462

### Working Baseline
- Algorithm: K-Means
- Number of clusters: 2
- Cluster 0: 23 meters
- Cluster 1: 10 meters
- Features: 24 normalized hourly consumption values

### Interpretation
- Reliability filtering improved the silhouette score in this experiment.
- The two clusters are preliminary behavioral groupings.
- Cluster meanings require further profile analysis.
- Raw data and excluded meters are preserved.

### Output
- Saved to:
  `data/processed/reliable_meter_clusters.csv`

  ## Milestone: Cluster Behavioral Interpretation

### Cluster 0: Night-Oriented Profile
- Higher normalized consumption during midnight and early morning.
- Consumption decreases during the daytime.
- Consumption increases again during evening and late night.
- Peak occurs approximately around 23:00.

### Cluster 1: Day-Oriented Profile
- Lower consumption during midnight and early morning.
- Strong increase begins around 07:00.
- Main peak occurs approximately around 09:00.
- Relatively higher daytime consumption.
- Consumption decreases during late evening.

### Interpretation
- The clustering experiment identified two distinct average hourly consumption profiles.
- Cluster 0 has relatively stronger nighttime consumption.
- Cluster 1 has relatively stronger daytime and morning consumption.
- Cluster labels are behavioral groupings, not confirmed consumer categories.
- Further validation is required before assigning real-world consumer types.

## Milestone: Cluster Comparison

### Cluster Statistics

| Metric | Cluster 0 | Cluster 1 |
|---|---:|---:|
| Number of meters | 23 | 10 |
| Total energy (kWh) | 58190.790 | 17351.886 |
| Average energy (kWh) | 0.0197 | 0.0213 |
| Average voltage (V) | 217.7315 | 228.0942 |
| Average current (A) | 1.8253 | 2.0297 |
| Average frequency (Hz) | 45.3828 | 47.1010 |
| Zero-energy percentage | 14.0599 | 10.0630 |

### Interpretation

- Cluster 0 contains more meters than Cluster 1.
- Cluster 1 has slightly higher average energy per reading.
- Cluster 1 has higher average voltage, current, and frequency.
- Cluster 0 has a higher zero-energy percentage.
- Total energy is affected by the different number of meters in each cluster.
- These clusters represent preliminary behavioral groupings, not confirmed consumer categories.