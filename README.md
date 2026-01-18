Weather Data Pipeline with Apache Airflow
Overview

This project implements a daily ETL pipeline using Apache Airflow to fetch current weather data from the OpenWeatherMap API, transform the raw API response, and store the processed data as CSV files in Amazon S3.

The pipeline is designed to be reliable, modular, and production-ready, demonstrating real-world data engineering concepts such as API ingestion, orchestration, transformation, and cloud storage.

DAG Details

DAG Name: weather_dag

Schedule: Daily (@daily)

Catchup: Disabled

Retries: 2 retries with a 2-minute delay between attempts

Workflow

The DAG follows a simple and clear task sequence:

1. API Availability Check

Uses HttpSensor to verify that the OpenWeatherMap API is reachable.

2. Data Extraction

Uses SimpleHttpOperator to fetch current weather data for Portland from the OpenWeatherMap API.

3. Transformation & Load

Uses PythonOperator to:

Parse and transform the raw JSON response

Convert temperatures to Fahrenheit

Convert timestamps to local time

Store the transformed data as a CSV file in Amazon S3

Task Order

is_weather_api_ready
↓

extract_weather_data
↓

transform_load_weather_data

Data Collected

Each record contains the following fields:

City name

Weather description

Temperature (Fahrenheit)

Feels-like temperature (Fahrenheit)

Minimum temperature (Fahrenheit)

Maximum temperature (Fahrenheit)

Atmospheric pressure

Humidity

Wind speed

Record timestamp (local time)

Sunrise time (local time)

Sunset time (local time)

Output

The transformed weather data is stored as timestamped CSV files in the following Amazon S3 bucket:

s3://weatherapiairflowyoutubebucket-yml/

Each file represents one daily snapshot of weather data.

Requirements

Apache Airflow 2.x

Python 3.8+

OpenWeatherMap API key

AWS credentials with access to Amazon S3
