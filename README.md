# Yelp Business Data Pipeline

## Overview

This repository contains a data engineering pipeline that ingests Yelp business and review datasets, cleans and transforms the raw data, and loads it into a warehouse for downstream analytics. The goal of the pipeline is to demonstrate an end‑to‑end ETL workflow using modern tools that scales to large datasets and produces clean, queryable tables.

## Features

- **Data acquisition** – download raw JSON or CSV dumps of Yelp businesses, reviews and users (e.g. from Yelp’s open dataset).
- **Schema inference and normalization** – parse nested JSON structures, extract relevant fields, and produce normalized tables (businesses, categories, reviews, users) with primary keys.
- **Data quality checks** – validate field types, handle missing values, and enforce referential integrity between tables.
- **Incremental processing** – support incremental loads by processing new files or updated records without reprocessing the entire dataset.
- **Load to warehouse** – write cleaned tables to a data warehouse (e.g. PostgreSQL, BigQuery or Snowflake) with optimal data types and clustering.
- **Orchestration** – optionally orchestrate the pipeline with Airflow or Prefect for scheduling, monitoring and retry logic.

## Directory structure

```
Yelp-Business-Data-Pipeline/
├── src/
│   ├── extract.py        # download or read raw Yelp data files
│   ├── transform.py      # clean, normalize and validate records
│   ├── load.py           # load cleaned tables into the warehouse
│   ├── utils.py          # helper functions for logging, config, etc.
│   └── config.yml        # configuration for file paths and connections
├── data/
│   └── raw/              # store raw input files (not committed)
├── tests/
│   └── test_transform.py # tests for transformation logic
├── docs/
│   └── architecture.md   # pipeline diagrams and notes
├── readme.md             # project description (this file)
├── requirements.txt      # Python dependencies
└── .gitignore
```

## Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/Suma4681/Yelp-Business-Data-Pipeline.git
   cd Yelp-Business-Data-Pipeline
   ```

2. **Create a virtual environment and install dependencies:**

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

3. **Configure the pipeline:**

   Edit `src/config.yml` to specify paths to your raw data files and warehouse connection details. Do not commit secrets; use environment variables for credentials where possible.

4. **Run the pipeline:**

   ```bash
   python src/extract.py
   python src/transform.py
   python src/load.py
   ```

   Or orchestrate with a tool like Airflow by writing a DAG that calls these scripts.

## Testing

Run the test suite with:

```bash
pytest
```

## Future improvements

- Add streaming ingestion with Kafka for near‑real‑time updates.
- Implement data quality dashboards to visualize missing values and outliers.
- Containerize the pipeline with Docker and provide a `docker-compose.yml` for local development.
- Integrate with a reporting layer (e.g. Looker or Superset) to build dashboards on top of the warehouse.

## License

This project is licensed under the MIT License.
