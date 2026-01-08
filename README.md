# Weather ETL Pipeline

## Project Overview
The Weather ETL Pipeline is an automated data engineering project that extracts real-time weather data for Abuja, Nigeria, from a public weather API, transforms it for analysis, and loads it into a PostgreSQL database for storage and querying. The pipeline is fully orchestrated using Apache Airflow, making it easy to schedule and monitor hourly data ingestion.

This project demonstrates core data engineering skills, including API extraction, data transformation, relational database management, and workflow orchestration. The Projectis also structured following production ETL best practices with separated extract, transform, load layers.

## Architecture Diagram

            ┌───────────────┐
            │  Weather API   │
            └───────┬───────┘
                    │
             Extract (Python)
                    │
                    ▼
            Transform (Pandas)
                    │
                    ▼
        Load to PostgreSQL Table
                    │
                    ▼
      Scheduled Run (Airflow DAG - Hourly)

## Tools Used

* Python – Data extraction, transformation, and scripting

* Pandas – Data cleaning and processing

* PostgreSQL – Relational database for storing weather data

* SQL – Table creation and data queries

* Apache Airflow – Orchestration and scheduling of ETL tasks

* Git/GitHub – Version control

* Shell / Bash – Automation of scripts


## Setup Instructions

### Clone the repository

git clone https://github.com/neduifeanyi/weather-etl-pipeline.git
cd weather-etl-pipeline


### Create a Python virtual environment

python -m venv venv
source venv/bin/activate  # Linux / Mac
venv\Scripts\activate     # Windows


### Install required packages

pip install -r requirements.txt


### Set up PostgreSQL

CREATE DATABASE weather_db;

CREATE TABLE weather_hourly (
    id SERIAL PRIMARY KEY,
    timestamp TIMESTAMP,
    temperature NUMERIC,
    humidity NUMERIC,
    wind NUMERIC
);


Update your database credentials in load.py.

### Configure Airflow

export AIRFLOW_HOME=~/airflow
airflow db init
airflow users create --username admin --firstname Chinedu --lastname Igweneme --role Admin --email admin@example.com


### Add DAG

Place weather_etl_dag.py in airflow/dags/

Start Airflow:

airflow scheduler
airflow webserver


### Run the DAG

Open the Airflow UI at http://localhost:8080

Turn on the DAG: weather_etl_pipeline

It will run automatically every hour.

## Sample Queries

### Average temperature per day:
SELECT DATE(timestamp) AS day,
       AVG(temperature) AS avg_temp
FROM weather_hourly
GROUP BY day
ORDER BY day;

### Highest wind speed recorded:
SELECT timestamp, wind
FROM weather_hourly
ORDER BY wind DESC
LIMIT 1;

### Last 24 hours data:
SELECT *
FROM weather_hourly
WHERE timestamp >= NOW() - INTERVAL '24 HOURS'
ORDER BY timestamp;

## What I Learned

* How to extract data from an API using Python

* Data cleaning and transformation with Pandas

* Designing and loading data into PostgreSQL

* Automating ETL pipelines using Apache Airflow DAGs

* Using Git/GitHub for version control

* Structuring a data engineering project for reproducibility and scalability

This project demonstrates my ability to build end-to-end ETL pipelines, a fundamental skill for a Data Engineer role.
