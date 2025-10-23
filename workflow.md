# Workflow

## 1. General Data preprocessing; not provided in this repository
**Files:** `original_data.csv`
- Apply general data cleaning and time-to-event calculation
- Saves result as `data_clean.csv` with the structure depicted above

### Structure
| Variable | Type | Description |
|-----------|------|-------------|
| name | string | Patient identifier |
| id | numeric | ID number |
| center | string | 1, 2, 3, 4 |
| date v0, v1 | date | yyyy-mm-dd |
| tto v1 | numeric | Days |
| ltfu, transplant, death at visit 1 | logical | TRUE/FALSE |
| date ltfu, transplant, death | date | yyyy-mm-dd |
| tto ltfu, transplant, death | numeric | Days |

| age | numeric | Age in years |
| gender | string | Male/Female |
| dialysis vintage  | numeric | vintage in months |
| dialysis access
| dialysis dose 
| bloodflow
| rkf
| ktv
| bmi
| iPTH | numeric | mg/L |
| noxPTH | numeric | mg/L |
| beta crosslaps | numeric | mg/L |
| opg | numeric | mg/L |
| imanox | numeric | mg/L |
| perox | numeric | mg/L |
| srankl | numeric | mg/L |
| hscrp | numeric | mg/L |
                     
---

## 2. Clusteranalysis— `cluster_generation.Rmd`
- Imports `data_clean.csv`
- Performs Winsorization, z-normalisation and manhattan distance calculation
- Determines optimal clustering solution (Silhouette width)
- Determins cluster stability via bootstrap analysis
- Runs PAM algorithm on the datasets  
- Saves each result as `clusterresults.csv`

---
## 3. Validation — `leaveonecenterout_analysis.Rmd`
Validation is both embedded in earlier steps and performed here:
- **`leaveonecenteryout_analysis.Rmd`** – Runs clustering while excluding one registry at a time  
- **`ECDF_plots.Rmd`** – Plots ECDFs of log-likelihoods for six leave-one-out analyses


## 4. Description & Outcome Analysis — `describe_clusters.Rmd`
- Imports `data_clean.csv` and relabelled cluster data  
- Describes clusters with summary statistics  
- Performs Kaplan-Meier analysis and CIF of outcomes with competing events
- Performs incremental Outcome prediction analysis using a fine grey model


📦 **Output Summary**
