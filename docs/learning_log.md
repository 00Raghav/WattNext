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