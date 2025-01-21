# Flight-Booking-Airflow-CICD

This project automates the orchestration and processing of flight booking data using Apache Airflow, Google Cloud Platform (GCP), and PySpark. The CI/CD pipeline ensures efficient deployment and data processing in development and production environments.

## Features

•	CI/CD Integration: Automates deployment of Airflow DAGs, PySpark jobs, and environment variables using GitHub Actions.
 
•	Apache Airflow: Orchestrates the pipeline, including file sensing and data processing tasks.
 
•	PySpark Data Processing: Transforms flight booking data and generates insights for storage in BigQuery.
 
•	GCP Integration: Utilizes GCP services like Composer (Airflow), BigQuery, and Cloud Storage.
 
## Project Structure

.
├── .github/workflows/

│   └── Flight-Booking-CICD.yml    # GitHub Actions workflow file for CI/CD

├── airflow_job/

│   └── airflow_job.py             # Airflow DAG for data orchestration

├── spark_job/

│   └── spark_transformation_job.py # PySpark job for data processing

├── variables/

│   ├── dev/
│
│   └── variables.json         # Development environment variables

│   └── prod/

│       └── variables.json         # Production environment variables

└── flight_booking.csv             # Sample flight booking data


## Setup

### Prerequisites
	
 1.	GCP Project with:

   	• Composer (Airflow) environment.
	  
   	• BigQuery datasets for dev and prod.
	  
   	• Cloud Storage bucket for data and DAG storage.
   
2.	GitHub Secrets:
 
  	• GCP_SA_KEY: Service account key in JSON format.
	
  	• GCP_PROJECT_ID: GCP project ID.

## CI/CD Workflow

The pipeline is triggered on changes to the following branches:

	
 •	dev: Deploys resources to the development environment.
 
	
 •	main: Deploys resources to the production environment.

Workflow tasks include:
	
 1.	Uploading Airflow variables (variables.json) to GCS.
	
 2.	Importing variables into the corresponding Composer environment.
	
 3.	Syncing Airflow DAGs and PySpark jobs to GCS.

## Airflow DAG

### DAG: flight_booking_dataproc_bq_dag

1.	File Sensor: Checks for the availability of the input CSV file in the GCS bucket.

2.	PySpark Job: Processes flight booking data and writes transformed data and insights to BigQuery.

### Key Variables

•	env: Deployment environment (dev or prod).

•	gcs_bucket: Cloud Storage bucket name.
	
•	bq_project: BigQuery project ID.

•	bq_dataset: BigQuery dataset name.

## PySpark Job

### spark_transformation_job.py

•	Reads flight booking data from GCS.

•	Applies transformations to calculate:
	
 	• Weekend Bookings.
 
	
 	• Lead Time Categories.
 
	
 	• Booking Success Rate.

•	Generates insights for:
	
 	• Route performance.
	
 	• Booking origins.

•	Writes results to BigQuery.

## How to Run
	
 1.	Push changes to the dev or main branch.
	
 2.	GitHub Actions automatically deploy resources to the respective environment.
	
 3.	Trigger the DAG manually via the Airflow UI to process the data.
