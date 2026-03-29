Postgres_DB_to_DF

A PostgreSQL to Pandas DataFrame pipeline demonstrating data ingestion, database connectivity, and modern Python data workflows using SQLAlchemy, psycopg2, and psycopg3. This project is designed for data scientists and developers who want to build production-ready data ingestion workflows.

Table of Contents
Overview
Features
Technology Stack
Setup
Environment Variables
Usage
Example Output
License
Overview

Data collection is a critical step in any data science workflow. Often, the most valuable data resides in relational databases rather than local CSVs.

This project demonstrates:

Setting up a PostgreSQL database and tables.
Ingesting data into Pandas DataFrames.
Using legacy (psycopg2) and modern (psycopg3) approaches with SQLAlchemy.
Managing credentials securely with a .env file.
Optional: using high-performance drivers like ADBC (future-ready).


Features
Connects to PostgreSQL database with Python.
Supports legacy (psycopg2) and modern (psycopg3) connections.
Reads SQL tables directly into Pandas DataFrames.
Secure credential management via .env.
Fully compatible with Windows, Linux, and uv projects.


Technology Stack
Component	Version / Tool
Database	PostgreSQL (latest)
GUI Tool	pgAdmin 4
Python Libraries	Pandas, SQLAlchemy, psycopg2, psycopg3, python-dotenv
Environment	uv environment / virtualenv
Notebook	Jupyter Notebook


Setup
Clone the repository
git clone https://github.com/yourusername/Postgres_DB_to_DF.git
cd Postgres_DB_to_DF
Create and activate uv environment
uv new Postgres_DB_to_DF
uv activate Postgres_DB_to_DF


Install dependencies
uv add ipykernel pandas sqlalchemy psycopg psycopg2 psycopg[binary] python-dotenv

Create .env file at project root:
DB_USER=postgres
DB_PASSWORD=yourpassword
DB_HOST=localhost
DB_PORT=5432
DB_NAME=ds_pipeline

Replace with your PostgreSQL username, password, host, and database name.

Environment Variables
Variable	Description
DB_USER	PostgreSQL username
DB_PASSWORD	PostgreSQL password
DB_HOST	Database host (default: localhost)
DB_PORT	Database port (default: 5432)
DB_NAME	Database name

Usage
Legacy psycopg2 approach
from sqlalchemy import create_engine
from sqlalchemy.engine import URL
import pandas as pd
from dotenv import load_dotenv
import os

load_dotenv()

url_legacy = URL.create(
    drivername="postgresql+psycopg2",
    username=os.getenv("DB_USER"),
    password=os.getenv("DB_PASSWORD"),
    host=os.getenv("DB_HOST"),
    port=os.getenv("DB_PORT"),
    database=os.getenv("DB_NAME")
)

engine_legacy = create_engine(url_legacy)
df_legacy = pd.read_sql("SELECT * FROM employees", engine_legacy)
print(df_legacy)
Modern psycopg3 approach
url_modern = URL.create(
    drivername="postgresql+psycopg",
    username=os.getenv("DB_USER"),
    password=os.getenv("DB_PASSWORD"),
    host=os.getenv("DB_HOST"),
    port=os.getenv("DB_PORT"),
    database=os.getenv("DB_NAME")
)

engine_modern = create_engine(url_modern)
df_modern = pd.read_sql("SELECT * FROM employees", engine_modern)
print(df_modern)
Example Output
employee_id	first_name	last_name	department	salary	hire_date
1	Alice	Smith	IT	80000.0	2022-01-15
2	Bob	Johnson	HR	65000.0	2021-06-01
3	Charlie	Williams	Finance	90000.0	2020-09-23
License

MIT License – free to use, modify, and distribute.