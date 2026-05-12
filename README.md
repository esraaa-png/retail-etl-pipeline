Retail Data Warehouse ETL Pipeline

A production-ready ETL pipeline built using Apache Airflow, PostgreSQL, and Docker to extract, transform, validate, and load retail sales data into a data warehouse environment.

Overview

This project demonstrates a complete ETL workflow orchestrated with Apache Airflow.

The pipeline extracts retail sales data from CSV files, processes and validates the data, then loads it into PostgreSQL using a modular and scalable architecture.

The project is designed to simulate real-world Data Engineering practices including workflow orchestration, structured logging, modular ETL development, and containerized deployment.

Features
ETL orchestration using Apache Airflow
CSV data ingestion
Data transformation and validation
PostgreSQL data warehouse integration
Modular ETL architecture
Structured logging and monitoring
Dockerized development environment
Astro CLI support
Retry handling for failed tasks
Scalable DAG design
Pipeline Architecture
CSV Dataset
     │
     ▼
Extract Data
     │
     ▼
Transform Data
     │
     ▼
Validate Data
     │
     ▼
Load into PostgreSQL
     │
     ▼
Retail Data Warehouse
Tech Stack
Layer	Technology
Orchestration	Apache Airflow 2.x
Runtime	Astro CLI
Database	PostgreSQL
Programming Language	Python
Data Processing	Pandas
Containerization	Docker
Monitoring	Python Logging
Project Structure
retail-data-warehouse/
│
├── dags/
│   └── retail_etl_dag.py
│
├── include/
│   ├── data/
│   │   └── retail_sales.csv
│   │
│   ├── extract.py
│   ├── transform.py
│   ├── validate.py
│   └── load_postgres.py
│
├── tests/
├── screenshots/
│
├── requirements.txt
├── Dockerfile
├── README.md
└── .env
Getting Started
1. Clone the Repository
git clone <your-repository-link>

cd retail-data-warehouse
2. Configure Environment Variables

Create a .env file:

POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_DB=retail_dw
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
3. Start Airflow
astro dev start

Airflow UI:

http://localhost:8080

Default credentials:

admin / admin
4. Configure PostgreSQL

Enter the PostgreSQL container:

docker exec -it airflow_postgres bash

Connect to PostgreSQL:

psql -U postgres

Create database and user:

CREATE USER airflow WITH PASSWORD 'airflow';

ALTER USER airflow CREATEDB;

CREATE DATABASE retail_dw OWNER airflow;

GRANT ALL PRIVILEGES ON DATABASE retail_dw TO airflow;

Reconnect using:

psql -U airflow -d retail_dw
5. Add Airflow Connection

Inside the Airflow UI:

Admin → Connections

Create a PostgreSQL connection using the following values:

Field	Value
Conn ID	postgres_default
Conn Type	Postgres
Host	localhost
Port	5432
Schema	retail_dw
Login	postgres
Password	postgres
6. Trigger the DAG
astro dev run dags trigger retail_etl_dag
Database Schema
dim_products

Stores product metadata.

Column	Type
product_id	INT
product_name	VARCHAR
category	VARCHAR
price	NUMERIC

Example:

1 | Laptop     | Electronics | 15000
2 | Headphones | Electronics | 1200
3 | Chair      | Furniture   | 850
fact_sales

Stores transactional sales data.

Column	Type
sale_id	INT
product_id	INT
customer_id	INT
quantity	INT
total_amount	NUMERIC
sale_date	DATE

Example:

1 | 101 | 1001 | 2 | 3000 | 2025-01-01
2 | 102 | 1002 | 1 | 1200 | 2025-01-02
3 | 103 | 1003 | 5 | 4250 | 2025-01-03
ETL Workflow
Extract
Read raw retail sales CSV files
Load data into Pandas DataFrames
Transform
Handle missing values
Convert data types
Standardize column formats
Calculate required metrics
Validate
Check for null values
Detect duplicate records
Validate schema consistency
Load
Insert transformed data into PostgreSQL
Maintain data warehouse integrity
Monitoring and Logging

Each Airflow task logs:

Extracted record counts
Transformation steps
Validation results
Loaded row counts
Error tracebacks
DAG execution status

Logs can be monitored through:

Airflow Task Logs
Docker Container Logs
Future Improvements
Incremental loading support
REST API ingestion
Kafka streaming integration
Automated alerts and notifications
CI/CD pipeline integration
Dashboard visualization using Tableau or Microsoft Power BI
Learning Outcomes

This project demonstrates practical experience with:

ETL Pipeline Development
Data Warehousing
Workflow Orchestration
Airflow DAG Design
PostgreSQL Integration
Docker Containerization
Data Validation Techniques
Production-style Data Engineering Practices
Author

Esraa Abdelazeem
Data Engineer | Data Analyst | AI Enthusiast

Passionate about building scalable data pipelines, automating workflows, and transforming raw data into actionable insights.
