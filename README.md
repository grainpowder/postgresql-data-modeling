# Sparkify Data Modeling

An imaginary startup company Sparkify provides music streaming service, and has been stored data on songs and user activity in JSON file format for a long time. This disabled their data analyst and data science team to utilize this data, since information in individual file cannot be easily queried. Therefore, primary role of data engineer facing such situation can be listed as follows:

1. Define relational database schemas to store raw data appropriately
1. Extract related data field from data stored in each file
1. Transform extracted data into required format if needed
1. Load extracted, transformed data into intialized database

## Repository

This repository contains two jupyter notebooks and three Python modules. Role of each file can be explained as follows.

* `sql_queries.py`: contains all sql queries for CRUD operation for created database
* `create_tables.py`: actual module that initializes database and table if they do not exist
* `etl.py`: actual module that reads and processes files from song_data and log_data and loads them into tables in database
* `etl.ipynb`: shows execution result of each of atomic operation that consists of methods defined in `etl.py`
* `test.ipynb`: directly make connection to created database and apply some sanity checks on each of table

## Execute

```shell
python create_tables.py
python etl.py
```

## Schema

`create_tables.py` creates four dimension tables `songs`, `users`, `artists`, `time` which contains atomic information on songs, users, artists and certain timestamp respectively. Information in those tables are then combined to construct fact table `songplays`, which stores event generated at certain time by certain user which listened to certain song created by certain artist. Since each of primary key defined in one of four dimension table is used to define event in fact table, this setup can be characterized as star schema.