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