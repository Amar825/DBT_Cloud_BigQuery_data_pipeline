# DBT_Cloud_BigQuery_data_pipeline 🚀  
An end-to-end data engineering pipeline using **Google Cloud Platform**, **DBT**, and **BigQuery**, with full automation through **GitHub Actions (CI/CD)**.

---

## 📚 Table of Contents
1. [Project Overview](#project-overview)
2. [Tools & Technologies Used](#tools--technologies-used)
3. [Architecture Diagram](#architecture-diagram)
4. [Step-by-Step Workflow](#step-by-step-workflow)
   - [4.1 GCP Setup](#41-gcp-setup)
   - [4.2 BigQuery Datasets & GCS Buckets](#42-bigquery-datasets--gcs-buckets)
   - [4.3 Data Generation & Upload](#43-data-generation--upload)
   - [4.4 External Table Creation](#44-external-table-creation)
   - [4.5 DBT Modeling](#45-dbt-modeling)
   - [4.6 Testing & Documentation](#46-testing--documentation)
   - [4.7 CI/CD with GitHub Actions](#47-cicd-with-github-actions)
   - [4.8 Deployment to Production](#48-deployment-to-production)
   - [4.9 Scheduled Jobs & Looker Dashboard](#49-scheduled-jobs--looker-dashboard)
5. [Data Lineage & Model Flow](#data-lineage--model-flow)
6. [Screenshots & Walkthrough](#screenshots--walkthrough)
7. [Key Learnings](#key-learnings)
8. [Why This Project Matters](#why-this-project-matters)
9. [Conclusion](#conclusion)
10. [Contact Me](#contact-me)

---

## 📌 Project Overview

This project demonstrates my ability to build a **scalable, production-grade data pipeline** using industry-standard tools. From raw data ingestion and transformation to CI/CD and visualization, this project simulates the daily responsibilities of a Data Engineer.

> ⚙️ Tech stack: GCP + BigQuery + DBT Core + GitHub Actions + Python + Looker Studio

---

## 🛠️ Tools & Technologies Used

| Tool                | Purpose                                      |
|---------------------|----------------------------------------------|
| **Google Cloud Platform (GCP)** | Infrastructure & storage             |
| **BigQuery**         | Data warehouse / SQL engine                  |
| **Google Cloud Storage** | Raw data file storage                   |
| **DBT Core**         | Transformations, testing, documentation     |
| **GitHub Actions**   | CI/CD automation pipeline                   |
| **Python**           | Data generation script                      |
| **Looker Studio**    | Visualization / dashboarding                |

---

## 🧱 Architecture Diagram

> _Add a PNG/diagram showing: GCS → BigQuery External Tables → DBT Models → CI/CD → Looker_

---

## 🔁 Step-by-Step Workflow

### 4.1 GCP Setup
- Created GCP project
- Configured IAM roles and Service Accounts
- Enabled BigQuery & GCS

### 4.2 BigQuery Datasets & GCS Buckets
- Created `dev_healthcare_data` and `prod_healthcare_data`
- Created GCS bucket `healthcare-data-bucket-*`

### 4.3 Data Generation & Upload
- Wrote Python script using `Faker` and `Pandas`
- Generated realistic healthcare data (patients, EHR, claims)
- Uploaded CSV, JSON, Parquet to GCS

### 4.4 External Table Creation
- Used BigQuery to create external tables from GCS
- Formats: CSV (patients), JSON (EHR), Parquet (claims)

### 4.5 DBT Modeling
- Built staging (`stg_`) and core (`fct_`, `dim_`) models
- Used `source()` and `ref()` for lineage and modularity

### 4.6 Testing & Documentation
- Added `schema.yml` for column-level tests (`not_null`, `unique`)
- Used `dbt test`, `dbt docs generate`, `dbt docs serve`

### 4.7 CI/CD with GitHub Actions
- `ci.yml`: runs `dbt test` on pull requests
- `cd.yml`: deploys models to prod on merge to `main`
- Injected GCP credentials via GitHub Secrets

### 4.8 Deployment to Production
- All models deployed to `prod_healthcare_data` via GitHub Actions
- Fully automated and version-controlled

### 4.9 Scheduled Jobs & Looker Dashboard
- Scheduled DBT builds (daily)
- Created interactive dashboards in Looker Studio

---

## 🧬 Data Lineage & Model Flow

> _Include a screenshot of your DBT Cloud lineage graph here_

Shows how raw data from GCS flows into staging, transformations, and final analytical tables.

---

## 📸 Screenshots & Walkthrough

Add screenshots of:

- BigQuery datasets (`dev` and `prod`)
- GCS bucket with raw files
- DBT models + directory structure
- GitHub Actions CI passing
- Looker Studio dashboard
