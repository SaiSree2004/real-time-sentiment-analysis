# Real-Time Social Media Analytics Pipeline (AWS + Databricks + DBT + PySpark + Airflow)

---

## Project Objective

This project implements an end-to-end data pipeline for social media analytics using:

AWS • Databricks • PySpark • Delta Lake • Apache Airflow • DBT

The pipeline follows the Medallion Architecture (Bronze → Silver → Gold) to transform raw data into analytics-ready datasets.

### Key Business Outputs

* Sentiment trend analysis (Positive / Negative / Neutral)
* User influence rankings based on engagement score
* Topic performance insights (AI, Sports, Finance, Cloud)
* Geographic trend analysis by country
* Valid vs invalid tweet distribution
* Daily & hourly tweet activity patterns

---

## Datasets

### Source

* AWS S3 Bucket — realtime-parquetfiles (eu-north-1)
* Registered via AWS Glue Catalog → realtime_tweets

### Tables Used

* tweets_tb → Raw tweet content
* sentiment_tb → Sentiment scores
* trends_tb → Trending topics
* user_metadata_tb → User data
* valid_tb → Validated tweets

Each dataset contains ~50,500 records

---

## Lakehouse Architecture

The pipeline integrates:

* AWS (S3, Glue)
* Databricks (Processing)
* Delta Lake
* Airflow (Orchestration)
* DBT (Transformations)

### End-to-End Architecture

![Architecture Diagram](Dashboard/images/architecture.png)

---

## Medallion Architecture Layers

### Bronze Layer (Raw Data)

**Purpose**

* Store raw data from S3
* Maintain data lineage
* Enable traceability

**Operations**

* Parquet ingestion from AWS S3
* Schema validation
* Metadata via AWS Glue
* Add ingested_at timestamp

---

### Silver Layer (Cleaned Data)

**Purpose**

* Clean and standardize datasets
* Handle missing values
* Ensure analytics-ready quality

**Transformations**

* Timestamp parsing
* Null handling using averages
* Column cleaning
* Duplicate removal
* Data enrichment (topic & country filling)

Output size: ~47K rows per table

---

### Gold Layer (Analytics Data)

**Purpose**
Generate business-ready datasets for dashboards.

**Includes**

* Dimension Tables (topic, country, user)
* Fact Tables (tweets, trends)
* Aggregations (sentiment, influence)
* Metrics Tables (KPIs, trends, distributions)

### DBT Transformations (Gold Layer)

DBT is used in the Gold layer to manage transformations and build analytics models.

* Modular SQL-based transformations
* Creation of fact and dimension tables
* Data lineage tracking
* Version-controlled transformations
* Automated testing for data quality

Example models:

* fact_tweet_sentiment
* fact_tweet_engagement
* dim_user
* dim_topic

### Data Model — Star Schema (Gold Layer)

![Star Schema Gold Layer](Dashboard/images/data_model.svg)

---

## Pipeline Orchestration (Airflow)

Orchestrated using Apache Airflow DAGs

### Tasks

* Bronze ingestion
* Silver transformation
* Gold aggregation (DBT models)

Runs daily at midnight

### Airflow DAG

![Airflow DAG](Dashboard/images/airflow.jpeg)

---

## Data Quality Checks

* Null handling using averages
* Duplicate removal
* Schema validation
* S3 file existence checks
* Row count validation

Monitoring via:

* Airflow logs
* Databricks logs
* AWS S3 logs

---

## Alerts and Monitoring

The pipeline includes alerting mechanisms to ensure reliability and quick issue detection.

* Airflow task failure alerts
* Job retry notifications
* Data quality failure alerts
* Missing data or delayed pipeline alerts
* Threshold-based alerts (sudden drop/spike in tweet volume)

Alerts can be configured using:

* Airflow email alerts
* Databricks job notifications
* CloudWatch (for AWS services)

---

## Project Folder Structure

```
Real-Time-Social-Media-Sentiment-Analysis-Pipeline
│
├── Datasets
│   └── raw_data
│
├── Development
│   ├── Bronze
│   │   └── bronze_code.py
│   ├── Silver
│   │   └── silver_code.py
│   ├── Gold
│   │   └── gold_code.py
│   └── DAG
│       └── dag_code.py
│
├── Testing
│   ├── test_bronze.py
│   ├── test_silver.py
│   └── test_gold.py
│
├── Dashboard
│   ├── images
│   │   ├── final-arch.png
│   │   ├── airflow.jpeg
│   │   ├── star_schema_gold_layer.svg
│   │   ├── tweet_dashboard.png
│   │   ├── sentiment_dashboard.png
│   │   ├── trend_dashboard.png
│   │   ├── users_influence_dashboard.png
│   │   └── overview_dashboard.png
│   └── dashboard_queries.ipynb
│
└── README.md
```

---

## Analytics Dashboards

### Overview

![Overview Dashboard](Dashboard/images/overview_dashboard.png)

### Tweet Activity

![Tweet Dashboard](Dashboard/images/tweet_dashboard.png)

### Sentiment Analysis

![Sentiment Dashboard](Dashboard/images/sentiment_dashboard.png)

### Trend Analysis

![Trend Dashboard](Dashboard/images/trend_dashboard.png)

### Users & Influence

![Users Dashboard](Dashboard/images/users_influence_dashboard.png)

---

## Business Insights

* Sentiment Analysis → Track sentiment trends per topic
* User Influence → Identify top influencers
* Topic Performance → Measure engagement per topic
* Geographic Trends → Country-level insights
* Data Quality Monitoring → Valid vs invalid tweets
* Peak Activity Analysis → Identify active hours

---

## Technologies Used

* Python
* PySpark
* Databricks
* Delta Lake
* AWS S3
* AWS Glue
* Apache Airflow
* DBT
* Unity Catalog
* Databricks SQL
* Git and GitHub

---

## Installation

```bash
git clone https://github.com/Sahanap1708/real-time-sentiment-pipeline.git
cd real-time-sentiment-pipeline
pip install -r requirements.txt
```

---

## Running the Pipeline

### Databricks

1. Upload notebooks
2. Create Job (Bronze → Silver → Gold)
3. Use cluster: realtime-cluster
4. Schedule daily

### Airflow

```bash
airflow dags trigger socialmedia_pipeline_dag
```

---

## Future Enhancements

* Real-time streaming (Kafka / Kinesis)
* Machine learning sentiment models
* Advanced BI dashboards (Power BI / Tableau)
* Automated data quality monitoring
* Multi-platform integration

---

## License

This project is for educational and research purposes.

---

## Author

Project Lead

Sahana P

Team Members

* Sahana P
* Gullanki Vara Naga Sai Sree
* Subhadip Sasmal
* Peruri Sireesha
