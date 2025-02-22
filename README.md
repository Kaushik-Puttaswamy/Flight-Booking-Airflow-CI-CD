
# ✈️ Flight-Booking-Airflow-CICD

Welcome to **Flight-Booking-Airflow-CICD**! This project automates the orchestration and processing of flight booking data using [Apache Airflow](https://airflow.apache.org/), [Google Cloud Platform (GCP)](https://cloud.google.com/), and [PySpark](https://spark.apache.org/). Our CI/CD pipeline ensures efficient deployment and data processing across both development and production environments.

---

## 📚 Table of Contents
- [🚀 Features](#-features)
- [📁 Project Structure](#-project-structure)
- [🔧 Setup](#-setup)
- [🔄 CI/CD Workflow](#-cicd-workflow)
- [🛫 Airflow DAG](#-airflow-dag)
- [🔥 PySpark Job](#-pyspark-job)
- [▶️ How to Run](#-how-to-run)
- [📊 Sample Data](#-sample-data)
- [💡 Conclusion](#-conclusion)
- [🔮 Future Work](#-future-work)

---

## 🚀 Features

- **CI/CD Integration**  
  Automates deployment of Airflow DAGs, PySpark jobs, and environment variables using GitHub Actions.

- **Apache Airflow**  
  Orchestrates the pipeline, including file sensing and data processing tasks.

- **PySpark Data Processing**  
  Transforms flight booking data and generates insights for storage in BigQuery.

- **GCP Integration**  
  Leverages GCP services like Composer (Airflow), BigQuery, and Cloud Storage.

---

## 📁 Project Structure

```plaintext
.
├── .github/workflows/
│   └── Flight-Booking-CICD.yml    # GitHub Actions workflow file for CI/CD
├── airflow_job/
│   └── airflow_job.py             # Airflow DAG for data orchestration
├── spark_job/
│   └── spark_transformation_job.py # PySpark job for data processing
├── variables/
│   ├── dev/
│   └── variables.json             # Development environment variables
│   └── prod/
│       └── variables.json         # Production environment variables
└── flight_booking.csv             # Sample flight booking data
```

---

## 🔧 Setup

### Prerequisites

1. **GCP Project** with:
   - A Composer (Airflow) environment.
   - BigQuery datasets for both **dev** and **prod**.
   - A Cloud Storage bucket for data and DAG storage.

2. **GitHub Secrets**:
   - `GCP_SA_KEY`: Service account key in JSON format.
   - `GCP_PROJECT_ID`: Your GCP project ID.

---

## 🔄 CI/CD Workflow

The pipeline is triggered on changes to the following branches:

- **dev**: Deploys resources to the development environment.
- **main**: Deploys resources to the production environment.

### Workflow Tasks

1. **Upload Airflow Variables**: Uploads `variables.json` to GCS.
2. **Import Variables**: Imports variables into the corresponding Composer environment.
3. **Sync DAGs & Jobs**: Synchronizes Airflow DAGs and PySpark jobs to GCS.

---

## 🛫 Airflow DAG

### DAG: `flight_booking_dataproc_bq_dag`

- **File Sensor**: Monitors for the presence of the input CSV file in the GCS bucket.
- **PySpark Job**: Processes flight booking data and writes transformed data and insights to BigQuery.

#### Key Variables

- `env`: Deployment environment (`dev` or `prod`).
- `gcs_bucket`: Cloud Storage bucket name.
- `bq_project`: BigQuery project ID.
- `bq_dataset`: BigQuery dataset name.

---

## 🔥 PySpark Job

### File: `spark_transformation_job.py`

1. **Data Ingestion**: Reads flight booking data from GCS.
2. **Data Transformation**: Calculates:
   - Weekend Bookings.
   - Lead Time Categories.
   - Booking Success Rate.
3. **Insight Generation**: Derives insights on:
   - Route performance.
   - Booking origins.
4. **Data Output**: Writes the results to BigQuery.

---

## ▶️ How to Run

1. **Push Changes**: Commit and push changes to the `dev` or `main` branch.
2. **Automatic Deployment**: GitHub Actions deploys resources to the respective environment.
3. **Trigger the DAG**: Manually trigger the DAG via the Airflow UI to process the data.

---

## 📊 Sample Data

- **Input**: `flight_booking.csv`

- **Output**: BigQuery tables for:
  - `transformed_flight_data_{env}`
  - `route_insights_{env}`
  - `origin_insights_{env}`

---

## 💡 Conclusion

This project demonstrates a robust and scalable approach to managing flight booking data using Airflow and GCP services. By automating the deployment process with CI/CD pipelines and leveraging PySpark for data transformation, the workflow achieves efficiency and accuracy in both development and production environments.

---

## 🔮 Future Work

- **Real-Time Processing**: Enhance the pipeline to support streaming data for near real-time insights.
- **Data Quality Checks**: Integrate automated validations to ensure data integrity before processing.
- **Advanced Analytics**: Incorporate machine learning models for predictive insights (e.g., demand forecasting, pricing trends).
- **Monitoring and Alerts**: Implement detailed monitoring and alerting for task failures and performance issues.
- **Multi-Region Deployment**: Scale the pipeline to support multi-region data processing for global availability.

---

Happy Coding! 🚀

