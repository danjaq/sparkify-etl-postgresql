# Data Modeling with PostgreSQL
An ETL pipeline to analyze the listening behavior of Sparkify's users, built for Udactiy's Data Engineering Nanodegree. 

## Overview
This ETL pipeline combines two data sets: 1) a subset of the [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/) and 2) simulated user logs from a music streaming service. Once read in, the data is processed and added to a PostgreSQL database. Input is stored in a series of JSON files. The intent of this project is to produce a database useful for analyzing user behavior, specifically what songs users are listening to. Database tables use a star schema for the benefit of simplifying the queries needed. The fact table is `songplays` and the following are the dimension tables: `time`, `users`, `songs`, and `artists`.

## Files
- data/ : Folder containing 71 song and 30 user log JSON files.
- create_tables.py : Python script to drop and create the tables anew.
- etl.ipynb : Jupyter notebook outlining the procedures, with code, for creation of the pipeline.
- etl.py : Python script to create the full pipeline.
- LICENSE : Standard MIT license.
- README.md: This file/
- sql_queries.py: Python script containing a list of queries to create, drop, and query the database.
- test.ipynb : Jupyter Notebook to run tests on database.

## Run Instructions
1. Run `create_tables.py` to create the needed tables for import. 
2. Run `etl.py` to import the data from the JSON files stored in `data/`.
3. `test.ipynb` contains convenient commands to confirm the data was executed successfully. Additional queries can also be run from this notebook.

### Sample Queries 
Please find some sample queries below along with their output. These queries are also contained in `test.ipynb` for convenience.
#### Top 5 Songs
`SELECT COUNT(DISTINCT sp.songplay_id) AS "Total Plays",\
            s.title\
            FROM songplays AS sp\
            JOIN songs AS s\
            ON sp.song_id = s.song_id\
            GROUP BY s.title\
            ORDER BY "Total Plays" DESC\
            LIMIT 5;`
#### Gender Breakdown of Users
`SELECT COUNT(user_id) AS "Total",\
            gender\
            FROM users\
            GROUP BY gender\
            ORDER BY "Total" DESC;`
