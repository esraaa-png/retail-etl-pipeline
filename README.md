Retail Data Warehouse ETL Pipeline
📌 Overview

This project demonstrates a complete end-to-end ETL pipeline built using Apache Airflow and PostgreSQL.

The pipeline extracts retail sales data from CSV files, transforms and validates the data, then loads it into a PostgreSQL Data Warehouse using a modular and production-style architecture.

The workflow is orchestrated with Airflow DAGs and containerized using Docker for easy local deployment and scalability.

✨ Features
Automated ETL orchestration with Airflow
CSV-based retail sales ingestion
Data cleaning and transformation
Data validation before loading
PostgreSQL Data Warehouse integration
Modular ETL architecture
Structured logging and monitoring
Dockerized environment
Astro CLI compatible
Scalable DAG design
Retry handling for failed tasks
Production-style folder structure
🏗️ Pipeline Architecture
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
🛠️ Tech Stack
Layer	Technology
Orchestration	Apache Airflow 2.x
Runtime	Astro CLI
Database	PostgreSQL
Language	Python
Containerization	Docker
Data Processing	Pandas
Logging	Python Logging
📂 Project Structure
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
├── screenshots/
│
├── tests/
│
├── requirements.txt
├── Dockerfile
├── README.md
└── .env
⚡ Getting Started
1️⃣ Clone the Repository
git clone <your-repository-link>

cd retail-data-warehouse
2️⃣ Configure Environment Variables

Create a .env file:

POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_DB=retail_dw
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
3️⃣ Start Airflow
astro dev start

Airflow UI:

http://localhost:8080

Default credentials:

admin / admin
4️⃣ Configure PostgreSQL

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
5️⃣ Add Airflow Connection

Inside the Airflow UI:

Admin → Connections

Create a PostgreSQL connection:

Field	Value
Conn ID	postgres_default
Conn Type	Postgres
Host	localhost
Port	5432
Schema	retail_dw
Login	postgres
Password	postgres
6️⃣ Trigger the DAG
astro dev run dags trigger retail_etl_dag
🗄️ Database Schema
dim_products

Stores product metadata.

Column	Type
product_id	INT
product_name	VARCHAR
category	VARCHAR
price	NUMERIC
Example
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
Example
1 | 101 | 1001 | 2 | 3000 | 2025-01-01
2 | 102 | 1002 | 1 | 1200 | 2025-01-02
3 | 103 | 1003 | 5 | 4250 | 2025-01-03
🔄 ETL Workflow

The pipeline follows these stages:

Extract
Read raw retail sales CSV files
Load data into Pandas DataFrames
Transform
Clean missing values
Convert data types
Standardize columns
Calculate metrics
Validate
Check null values
Detect duplicates
Validate schema consistency
Load
Insert transformed data into PostgreSQL
Maintain warehouse integrity
📊 Monitoring & Logging

Each Airflow task logs:

Extracted records count
Transformation steps
Validation failures
Loaded row counts
Error tracebacks
DAG execution status

Logs can be monitored from:

Airflow Task Logs
Docker Container Logs
🚀 Future Improvements
Incremental loading support
REST API ingestion
Kafka streaming integration
Data quality alerts
CI/CD pipeline integration
Email notifications
Dashboard visualization with Tableau or Microsoft Power BI
📈 Learning Outcomes

Through this project, the following concepts were applied:

ETL Pipeline Design
Data Warehousing
Workflow Orchestration
Airflow DAG Development
PostgreSQL Integration
Docker Containerization
Data Validation Techniques
Production-style Data Engineering Practices
👩‍💻 Author

Esraa Abdelazeem
Data Engineer | Data Analyst | AI Enthusiast

Passionate about building scalable data pipelines, automating workflows, and transforming raw data into actionable insights.
