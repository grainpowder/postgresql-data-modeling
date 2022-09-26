# Sparkify Data Modeling

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app. They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, whose role is to create a database schema and ETL pipeline for this analysis.

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