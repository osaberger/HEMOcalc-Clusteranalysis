# Workflow

## Overview
General data cleaning and time-to-event calculation are applied to export a cleaned dataset:  
`data_clean.csv`

This file serves as the input for all downstream analyses.

### Structure
| **Name** | **id** | **center** | **baseline** | **visit 1** | **FU time** | **ltfu** | **transplant** | **death** | **date ltfu** | **date transplant** | **date death** | **timeto ltfu** | **timeto transplant** | **timeto death** | **age** | **gender** | **bmi** |**dialysis vintage** | **dialysis access** | **dialysis dose** | **blood flow** | rkf | ktv| iPTH | noxPTH | beta crosslaps | opg | imanox | perox | srankl | hscrp |
|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|-----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|
| **Class** | string | string | date | date | numeric | logical | logical | logical | date | date | date | numeric | numeric | numeric | numeric | string | numeric | numeric | string | numeric | numeric | numeric | numeric | numeric | numeric | numeric | numeric | numeric | numeric | numeric | numeric |
| **Information** | Patient identifier | ID number | (yyyy-mm-dd) | (yyyy-mm-dd) | (days) | (TRUE/FALSE) | (TRUE/FALSE) | (TRUE/FALSE) | (yyyy-mm-dd) | (yyyy-mm-dd) | (yyyy-mm-dd) | (days) | (days) | (days) | (years) | (MALE/FEMALE) | VALUE | (months) | (CATH/AVF) | (h per week) | (mL/min) | (mL/day) | VALUE | (pg/mL) | (pg/mL) | (ng/mL) | (pmoL/mL) | (µmoL/mL) | (µmoL/mL) | (ng/mL) | (mg/L) |


                     
---

## 1. Cluster Analysis — `cluster_generation.Rmd`

- Imports `data_clean.csv`
- Performs preprocessing and computes Gower distance
- Determines the optimal number of clusters (Silhouette width)
- Assesses cluster stability via bootstrap resampling
- Runs the **PAM algorithm** on the dataset
- Saves the dataset with assigned cluster labels as `clusterresults.csv`

---

## 2. Description & Outcome Analysis — `cluster_outcomes.Rmd`

- Imports relabelled cluster data from `clusterresults.csv`
- Generates descriptive statistics for each cluster  
- Performs **Kaplan–Meier** and **competing-risk (CIF)** analyses of outcomes
- Fits an **incremental Fine–Gray model** to test the added predictive value of cluster membership

---

## 3. Validation — `leaveonecenterout_analysis.Rmd`
Validation is performed both within earlier steps and explicitly here:

- **`leaveonecenterout_analysis.Rmd`** – Runs clustering while excluding one center at a time  
