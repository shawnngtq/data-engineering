# Apache Airflow

- [Apache Airflow](#apache-airflow)
  - [Operators](#operators)
  - [Installation](#installation)
  - [Configuration](#configuration)
  - [Removal](#removal)
  - [Reference](#reference)

Open-source workflow management: https://github.com/apache/airflow

## Operators

| Operator                        | Description                                                |
| ------------------------------- | ---------------------------------------------------------- |
| BashOperator                    | executes a bash command                                    |
| PythonOperator                  | calls an arbitrary Python function                         |
| EmailOperator                   | sends an email                                             |
| SimpleHttpOperator              | sends an HTTP request                                      |
| MySqlOperator, PostgresOperator | executes a SQL command                                     |
| Sensor                          | waits for a certain time, file, database row, S3 key, etc… |

## Installation

```bash
# Create dev environment
conda create -n myenv python=3.7 anaconda

# Start env
conda activate myenv

# Install airflow (conda)
conda install -c conda-forge airflow

# Install airflow (pip)
# https://airflow.apache.org/installation.html
pip install apache-airflow
```

## Configuration

```bash
# Create PostgreSQL DB
sudo -u postgres psql

postgres=# CREATE DATABASE airflow;
postgres=# CREATE USER myuser WITH ENCRYPTED PASSWORD 'mypass';
postgres=# GRANT ALL PRIVILEGES ON DATABASE airflow to myuser;
postgres=# ALTER DATABASE airflow OWNER TO myuser;

# Use PostgreSQL instead of SQLite3
vim ~/airflow/airflow.cfg

    # The executor class that airflow should use. Choices include
    # SequentialExecutor, LocalExecutor, CeleryExecutor
    executor = LocalExecutor

    # The SqlAlchemy connection string to the metadata database.
    # SqlAlchemy supports many different database engine, more information
    # their website
    sql_alchemy_conn = postgresql+psycopg2://user:password@localhost:5432/airflow

# Initialize DB
airflow initdb
```

## Removal

```bash
# Remove physical folder
rm -r ~/airflow

# Export env to yml
conda env export > environment.yml

# Remove dev env
conda info --envs
conda remove --name myenv --all
```

## Reference

- https://airflow.apache.org/index.html
- https://andana.me/2019/01/20/python-DAG.html
- https://gist.github.com/rosiehoyem/9e111067fe4373eb701daf9e7abcc423
