# dbt-GCP-BigQuery-Healthcare-data-pipeline 🚀  
**A fully automated, production-grade data pipeline on** **GCP** **using** **DBT**, **BigQuery**, **and GitHub Actions (CI/CD)** — **built to simulate a real-world healthcare analytics use case.**


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

## 📌 1. Project Overview

This project demonstrates my ability to build a **scalable, production-grade data pipeline** using industry-standard tools. From raw data ingestion and transformation to CI/CD and visualization, this project simulates the daily responsibilities of a Data Engineer.

> ⚙️ Tech stack: GCP + BigQuery + DBT Core + GitHub Actions + Python 

---

## 🛠️ 2. Tools & Technologies Used

| Tool                | Purpose                                      |
|---------------------|----------------------------------------------|
| **Google Cloud Platform (GCP)** | Infrastructure & storage             |
| **BigQuery**         | Data warehouse / SQL engine                  |
| **Google Cloud Storage** | Raw data file storage                   |
| **DBT Core**         | Transformations, testing, documentation     |
| **GitHub Actions**   | CI/CD automation pipeline                   |
| **Python**           | Data generation script                      |

---

## 🧱 3. Architecture Diagram

This project follows a modular and automated data engineering architecture on Google Cloud.  
Raw synthetic healthcare data is generated and stored in GCS, externalized into BigQuery, transformed via DBT models, and deployed through CI/CD using GitHub Actions.

<p align="center">
  <img src="./images/architecture-diagram.png" alt="Architecture Diagram" width="750"/>
</p>

---

## 🔁 4. Step-by-Step Workflow

### 4.1 GCP Setup
- Created a new Google Cloud project (`root-matrix-457217-p5`)
- Enabled **BigQuery**, **Cloud Storage**, and **IAM** APIs
- Created service accounts with proper IAM roles (`BigQuery Admin`, `Storage Admin`, etc.)

<p align="center">
  <img src="./images/gcp-project-setup.png" alt="GCP Project Setup" width="700"/>
</p>

### 4.2 BigQuery Datasets & GCS Buckets
- Created datasets:
  - `dev_healthcare_data`
  - `prod_healthcare_data`
- **Cloud Storage bucket (`healthcare-data-bucket-amarkhatri`) was created automatically by the Python script**

<p align="center">
  <img src="./images/gcs-bucket-files.png" alt="GCS Bucket with Raw Files" width="700"/>
</p>

### 4.3 Data Generation Script (Python)

To simulate a real-world healthcare data pipeline, I wrote a Python script that:

- Generates synthetic data using the **Faker** library for:
  - Patient demographics (`CSV`)
  - Electronic health records (`JSON`)
  - Insurance claims (`Parquet`)
- Creates a **Cloud Storage bucket** if it doesn't already exist
- **Cleans the target folders** before uploading new files
- Uploads raw data directly to GCS (`dev/` and `prod/` folders)
- Writes all files in appropriate formats using:
  - `pandas` for CSV
  - `json` for newline-delimited JSON
  - `pyarrow` for Parquet

✅ The script performs **all ingestion + staging steps programmatically**, without manual uploads.

> 📁 Script location: [`data_generator/synthetic_data_generator.py`](./data_generator/synthetic_data_generator.py)

#### 🔑 Key Logic Overview

```python
# Create the bucket if it doesn't exist
def create_bucket():
    bucket = storage_client.bucket(BUCKET_NAME)
    if not bucket.exists():
        storage_client.create_bucket(BUCKET_NAME)

# Generate synthetic patients
def generate_patients(num_records):
    ...
    return pd.DataFrame(patients)

# Upload CSV, JSON, or Parquet to GCS
def upload_to_gcs(data, path, filename, file_format):
    ...
```


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

## 🧬 5. Data Lineage & Model Flow

> _Include a screenshot of your DBT Cloud lineage graph here_

Shows how raw data from GCS flows into staging, transformations, and final analytical tables.

---

## 📸 6. Screenshots & Walkthrough

Add screenshots of:

- BigQuery datasets (`dev` and `prod`)
- GCS bucket with raw files
- DBT models + directory structure
- GitHub Actions CI passing

