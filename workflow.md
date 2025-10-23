# Workflow

This is the structure of the main file:

### Structure
| **Variable** |---------------|
| **Type** |-----------|
| **Information** |-----------------|

|---------------|-----------|-----------------|
| name, id, center | string, numeric, string | Patient identifier, ID number, and center code (1–4) |
| date_v0, date_v1, tto_v1 | date, numeric | Baseline and follow-up dates (yyyy-mm-dd) and time to visit 1 in days |
| ltfu, transplant, death_v1, date_ltfu, date_transplant, date_death, tto_ltfu, tto_transplant, tto_death | logical, date, numeric | Status indicators (TRUE/FALSE), corresponding event dates (yyyy-mm-dd), and time-to-event values (days) |


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

## 1. Clusteranalysis— `cluster_generation.Rmd`
- *Not provided: Apply general data cleaning and time-to-event calculation to export `data_clean.csv`*
- The code starts with importing `data_clean.csv`
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
