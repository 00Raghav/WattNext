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