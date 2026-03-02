# Project 6: EHR Cohort Extraction & Time-to-Event Analysis (OMOP CDM) 🏥

**Status:** Completed  
**Goal:** Build a local relational database engine to ingest synthetic Electronic Health Records (EHR) formatted to the OMOP Common Data Model, and write optimized SQL to extract a chronological patient cohort.

## 📌 Overview
Navigating real-world clinical data requires a deep understanding of relational databases and temporal clinical logic. This project demonstrates the ability to ingest raw OMOP CDM tables (`person`, `condition_occurrence`, `procedure_occurrence`), establish a local SQLite database, and execute complex SQL joins to reconstruct a patient's clinical journey from diagnosis to intervention.

## 🛠️ Tech Stack
* **Language:** Python 3.13, SQL (SQLite dialect)
* **Data Engineering:** `sqlite3`, `pandas` (ETL pipeline)
* **Data Visualization:** `seaborn`, `matplotlib`
* **Data Standard:** OMOP Common Data Model v5.3 (Maternal Health Synthea Dataset)

## 🧠 Methodology
1. **Database Engine Initialization:** Engineered a Python script to programmatically spin up a local SQLite database and ingest multiple CSV files into relational SQL tables, handling memory constraints.
2. **Optimized SQL Cohort Extraction:** Wrote a highly optimized `INNER JOIN` query linking the Person, Condition, and Procedure tables. Implemented strict temporal logic (`procedure_date >= condition_start_date`) directly within the database engine to prevent Cartesian memory explosions, successfully extracting 50,000+ valid chronological pathways in seconds.
3. **Time-to-Event Analysis:** Utilized Pandas datetime broadcasting to calculate the exact number of days between diagnosis and intervention, filtering for the first 365 days of care.

## 📈 Key Clinical Insights
* **Acute Intervention Workflow:** The Time-to-Event histogram revealed a heavily right-skewed distribution, with the vast majority of interventions occurring within 0-10 days of the initial diagnosis. This strongly indicates an acute care environment where diagnostic findings immediately trigger clinical procedures.

## 🚀 How to Run
1. Clone the repository.
2. Ensure the OMOP CSV tables (`person.csv`, `condition_occurrence.csv`, `procedure_occurrence.csv`) are located in the `data/` directory.
3. Open `notebooks/01_omop_cohort_extraction.ipynb` and execute the cells to build the database, run the SQL queries, and generate the Time-to-Event histogram.