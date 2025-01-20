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

