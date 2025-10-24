# Workflow

This is the structure of the main file:

### Structure
| **Name** | **id** | **center** | **date v0** | **date v1** | **FU time** | **ltfu** | **transplant** | **death** | **date ltfu, transplant, death** | **time to ltfu, transplant, death** | **age** | **gender** |
|-----------|---------|-------------|--------------|--------------|-------------|------------|----------------|---------------|----------------|--------------------|----------------|----------------|--------------------|---------------|
| **Class** | string | string | date | date | numeric | logical | logical | logical | date | numeric | numeric | string |
| **Information** | Patient identifier | ID number | (yyyy-mm-dd) | (yyyy-mm-dd) | (days) | (TRUE/FALSE) | Date of LTFU | Date of transplant | (yyyy-mm-dd) | (days) | (years) | (M/F) |




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
