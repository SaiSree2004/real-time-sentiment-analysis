# 🚀 Real-Time Social Media Sentiment Analysis Pipeline

## 📌 Project Overview

This project implements a **real-time data pipeline** that streams social media data, processes it for sentiment analysis, and stores the results in structured layers for analytics.

The pipeline helps analyze **public sentiment from social media posts** and generate insights useful for **brand monitoring and trend analysis**.

The system is built using **AWS streaming services and Databricks** to process large volumes of streaming data efficiently. It follows the **Medallion Architecture (Bronze, Silver, Gold)** to organize raw, processed, and aggregated data.

The dataset used in this project is based on the **Twitter Sentiment Analysis Dataset from Kaggle**, which contains tweet text, user details, timestamps, and sentiment labels.

---

## 🏗 Architecture Overview

The pipeline processes streaming data through the following steps:

- Social media data is streamed through **Amazon Kinesis Data Streams**
- Streaming data is delivered to **Amazon S3 using Kinesis Firehose**
- **Databricks Structured Streaming** reads data from the data lake
- Data is processed and stored in **Delta Lake tables**
- Data is organized into **Bronze, Silver, and Gold layers**
- Processed data is used for **real-time sentiment analytics**

---

## 🗂 Data Layers

### 🥉 Bronze Layer

**Table:** `social_catalog.raw.tweet_data`

The Bronze layer stores **raw incoming data exactly as it arrives from the streaming source**.This layer is used mainly for auditing and replaying the original data if required.

**Key Characteristics**

- Raw JSON data
- Minimal transformations
- Used for auditing and replaying original data

---

### 🥈 Silver Layer

**Table:** `social_catalog.processed.valid_tweets`

The Silver layer contains **cleaned and validated data**.Invalid records and corrupted data are filtered out at this stage.

**Key Transformations**

- JSON parsing using predefined schema
- Data validation and filtering
- Handling missing or invalid fields
- Standardizing data formats

---

### 🥇 Gold Layer

**Table:** `social_catalog.analytics.sentiment_stats`

The Gold layer stores **aggregated analytical data** that can be used for reporting and dashboards.

**Example Metrics**

- Sentiment distribution (Positive / Negative / Neutral)
- Hourly sentiment trends
- Tweet activity statistics

This layer is optimized for **analytics and business insights**.

---

## ⚙️ Pipeline Features

### 🔄 Real-Time Streaming

- Uses **Databricks Structured Streaming**
- Processes micro-batches every **10 seconds**

### ✅ Data Quality Checks

- Validation rules ensure only **valid tweets are processed and stored in the Silver layer**

### ⚠️ Error Handling

- Checkpointing and logging are used to **recover from failures and maintain pipeline stability **

### 🔐 Data Governance

-This project uses **Unity Catalog** to manages tables and access control across the data platform.

### 📊 Monitoring and Alerts

- Detects unusual sentiment patterns
- Logs anomalies for investigation

---

## 🛠 Technologies Used

| Technology | Purpose |
|-----------|--------|
| Databricks | Data processing platform |
| PySpark | Streaming data processing |
| Delta Lake | Reliable data storage |
| Amazon Kinesis | Real-time data streaming |
| Amazon S3 | Data lake storage |
| AWS Kinesis Firehose | Data delivery |
| Python | Processing logic |
| Pytest | Testing |
| Git / GitHub | Version control |
| Unity Catalog | Data governance |

---

## 👩‍💻 Roles and Responsibilities

- Designed and implemented a **real-time sentiment analysis pipeline** using  Databricks and AWS services.
- Streamed social media data using **Amazon Kinesis** and delivered it to Amazon S3 through Firehose.
- Delivered streaming data to **Amazon S3 through Firehose**
- Developed **PySpark Structured Streaming jobs**
- Implemented **Medallion Architecture (Bronze, Silver, Gold)**
- Parsed JSON records and performed **data validation**
- Implemented **sentiment classification logic**
- Configured **checkpointing and error handling**
- Used **Git for version control**
- Performed testing using **Pytest**

---

## 🎯 Project Objective

The objective of this project is to build a **scalable real-time data pipeline** that analyzes social media sentiment and provides insights for **business decision-making and brand monitoring**.

---

## 📈 Outcomes

- Built a **scalable streaming data pipeline** using AWS and Databricks.
- Implemented structured data processing using **Delta Lake based data architecture**
- Ensured **data quality and reliability** through validation and logging.
- Enabled **real-time sentiment analytics** for social media sentiment monitoring.
