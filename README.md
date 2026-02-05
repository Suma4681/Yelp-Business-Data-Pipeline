# Yelp Business Data Pipeline (AWS + Databricks + Neo4j)

End-to-end data pipeline that ingests Yelp JSON datasets, transforms them into analytics-ready Parquet tables, and enables BI + graph analytics through AWS Athena/QuickSight and Neo4j.

## Why this matters
Most real-world data work is messy JSON + schema drift + scale. This project demonstrates production-style ETL: ingestion → validation → transformation → curated tables → analytics & visualization.

## What it does
- Ingests Yelp JSON datasets from AWS S3.
- Performs PySpark ETL in Databricks:
  - Flattens nested JSON/struct columns.
  - Normalizes schemas and enforces consistent types.
  - Removes duplicates and handles missing/null fields.
  - Generates curated, query-friendly tables in Parquet.
- Enables SQL analytics with Athena, dashboards via QuickSight, and graph analytics via Neo4j (user-business relationships).

## Tech Stack
AWS (S3, Lambda [optional trigger], Athena, QuickSight)  
Processing: Databricks (PySpark)  
Graph DB: Neo4j AuraDB (optional)  
Storage: Parquet on S3

## Outputs (Proof)
- Curated tables: `dim_business`, `fact_reviews`, `dim_users` (and others).
- Queryable datasets in Athena and QuickSight dashboards.
- Graph model for network analysis (users, businesses, categories).

> **Screenshots (please add):**
> - Athena query results (`docs/athena_query.png`)
> - QuickSight dashboard (`docs/quicksight_dashboard.png`)
> - Neo4j graph view (`docs/neo4j_graph.png`)
> - Databricks job run (`docs/databricks_run.png`)

## Architecture overview
1. **Ingest raw JSON** from Yelp dataset to S3.
2. **Process with Databricks** using PySpark to clean, flatten, and prepare Parquet tables.
3. **Store curated tables** back to S3.
4. **Query** curated data using AWS Athena and visualize with QuickSight.
5. **Optional**: Load selected entities into Neo4j for graph analysis.

## Getting started
### Running in Databricks
1. Fork this repo and upload the PySpark scripts from the `ETL-script` directory to your Databricks workspace.
2. Configure S3 paths and AWS credentials in a notebook or cluster environment variables (`RAW_BUCKET`, `CURATED_BUCKET`, etc.).
3. Execute the scripts in order to ingest businesses, reviews, and users, then transform them into curated tables.
4. Query the curated tables with Athena, or create dashboards in QuickSight.

### Local sample run
If you want to experiment locally, run a simplified sample:
```
python scripts/sample_run.py --input data/sample_business.json --output data/out.parquet
```
(Assumes you have Python, PySpark, and `data/sample_business.json` downloaded.)

## Data model
- `dim_business`: Business attributes (id, name, location, categories, attributes…)
- `dim_users`: User attributes (id, review_count, yelping_since…)
- `fact_reviews`: Review facts (business_id, user_id, stars, date, text…)

## Examples of insights
- Top-rated categories by city.
- Trends in star ratings over time.
- Power users and most-reviewed businesses.
- Relationship networks (via Neo4j) to detect communities.

## Repository structure
```
ETL-script/       # PySpark scripts for ingestion and transformation
lambda/           # AWS Lambda function to trigger pipeline (optional)
neo4j_load/       # Scripts to load data into Neo4j
test_cases/       # Sample test scripts
README.md         # Project documentation
```

## Improvements
- Implement automated data quality checks (e.g., Great Expectations).
- Add CI for linting/testing.
- Add orchestrator (Airflow or Databricks Jobs).
- Provide sample dashboards and graph queries.

## Author
Sumanth Reddy Koppula
