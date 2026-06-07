# NYC Taxi Data Engineering Pipeline

## Overview

This project demonstrates the design and implementation of an end-to-end Data Engineering pipeline using Databricks, Apache Spark (PySpark), Delta Lake, AWS S3, and Medallion Architecture principles. The pipeline processes NYC Yellow Taxi trip data sourced from Kaggle and transforms raw data into business-ready analytical datasets.

The solution follows a modern data lake architecture consisting of Bronze, Silver, and Gold layers, enabling scalable data processing, reliable storage, and analytical reporting.

---

## Architecture

```text
Kaggle Dataset
       │
       ▼
     AWS S3
       │
       ▼
 Databricks + Spark
       │
       ▼
 Bronze Layer (Raw Data)
       │
       ▼
 Silver Layer (Cleaned Data)
       │
       ▼
 Gold Layer (Business Metrics)
       │
       ├── Gold Monthly Revenue
       ├── Gold Payment Revenue
       └── Gold Hourly Trips
       │
       ▼
 Databricks Dashboard
       │
       ▼
 Databricks Genie
```

---

## Technology Stack

* Databricks
* Apache Spark (PySpark)
* Delta Lake
* AWS S3
* Kaggle Datasets
* Databricks Dashboards
* Databricks Genie
* Unity Catalog

---

## Dataset

Dataset: NYC Yellow Taxi Trip Data

The dataset contains trip-level information including:

* Pickup and drop-off timestamps
* Passenger count
* Trip distance
* Fare amount
* Payment type
* Tips and surcharges
* Total trip revenue

---

## Medallion Architecture

### Bronze Layer

Purpose:

* Store raw taxi trip data exactly as received from the source.

Table:

* `yellow_tripdata_2015_01`

Activities:

* Data ingestion from AWS S3
* Schema inference
* Raw data preservation

---

### Silver Layer

Purpose:

* Clean and standardize raw records.

Table:

* `yellow_tripdata_silver`

Transformations:

* Removed records with invalid trip distances
* Removed records with invalid fare amounts
* Removed records with invalid passenger counts
* Applied data quality filtering
* Prepared data for analytics

Example:

```python
clean_df = (
    df.filter(df.trip_distance > 0)
      .filter(df.fare_amount > 0)
      .filter(df.passenger_count > 0)
)
```

---

### Gold Layer

Purpose:

* Create business-ready analytical datasets.

Tables:

#### gold_monthly_revenue

Monthly revenue aggregation generated from taxi transactions.

Metrics:

* Monthly revenue trends
* Revenue reporting

---

#### gold_payment_revenue

Revenue analysis grouped by payment method.

Metrics:

* Revenue by payment type
* Payment behavior analysis

---

#### gold_hourly_trips

Trip volume aggregated by pickup hour.

Metrics:

* Peak travel hours
* Demand analysis

---

## Delta Lake Implementation

The project leverages Delta Lake for:

* ACID transactions
* Reliable writes
* Schema enforcement
* Time travel capabilities
* Improved data quality management

All Bronze, Silver, and Gold tables are stored as Delta tables within Databricks.

---

## Data Processing Workflow

### Notebook 1: Bronze to Silver

File:

* `nyc-trip-Bron-Sil`

Responsibilities:

* Load raw taxi data
* Apply data quality checks
* Create Silver layer table

Output:

* `yellow_tripdata_silver`

---

### Notebook 2: Silver to Gold

File:

* `nyc-trip-sil-gold`

Responsibilities:

* Generate analytical datasets
* Create business metrics
* Populate Gold layer tables

Outputs:

* `gold_monthly_revenue`
* `gold_payment_revenue`
* `gold_hourly_trips`

---

## Dashboard

The Gold layer datasets are visualized using Databricks Dashboards to provide business insights into:

* Revenue trends
* Payment method distribution
* Peak trip demand periods

Dashboard screenshots can be found in the `screenshots/` directory.

---

## Databricks Genie

Databricks Genie was used to perform natural language exploration of the Gold layer datasets, enabling business users to query data using conversational prompts.

---

## Skills Demonstrated

### Data Engineering

* ETL Pipeline Development
* Data Lake Architecture
* Medallion Architecture
* Data Quality Validation
* Data Modeling

### Big Data Technologies

* Apache Spark
* PySpark DataFrames
* Spark SQL
* Delta Lake

### Cloud Technologies

* AWS S3
* Databricks
* Unity Catalog

### Analytics & Reporting

* Dashboard Development
* Business Metric Generation
* Self-Service Analytics with Genie

---

## Future Enhancements

* Databricks Workflows for orchestration
* Incremental data ingestion
* Delta Lake MERGE operations
* Apache Airflow integration
* Real-time ingestion using Kafka
* Advanced monitoring and data quality checks

---

## Project Outcome

This project demonstrates the implementation of a scalable cloud-based data engineering pipeline capable of processing large datasets using Spark and Delta Lake while following industry-standard Medallion Architecture practices. The resulting Gold layer provides business-ready datasets that support reporting, analytics, and self-service data exploration.
