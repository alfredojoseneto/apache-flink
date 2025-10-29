# Apache Flink Project 🚀

[![Apache Flink](https://img.shields.io/badge/Apache%20Flink-1.17.1-blue)](https://flink.apache.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Java](https://img.shields.io/badge/Java-11-red?logo=java&logoColor=white)](https://www.java.com/)
[![Scala](https://img.shields.io/badge/Scala-2.12-DC322F?logo=scala&logoColor=white)](https://www.scala-lang.org/)

This project provides a containerized Apache Flink environment with SQL client support for data processing and analytics.

## 📋 Project Structure

```
.
├── apache_flink/
│   ├── data/              # Data directory for input files
│   │   └── test.csv
│   ├── settings/         # Configuration settings
│   └── sql-client/       # SQL Client configuration
│       ├── bin/
│       │   └── sql-client.sh
│       ├── conf/
│       │   └── flink-conf.yaml
│       ├── Dockerfile
│       └── docker-entrypoint.sh
├── docker-compose.yml    # Docker services configuration
└── pyproject.toml       # Python project configuration
```

## 🚀 Components

The project consists of three main services:

### 1. SQL Client 💻

- Custom-built SQL client for Apache Flink
- Interactive SQL query execution
- Mounted settings volume for configuration
- Connects to JobManager for query execution

### 2. JobManager 🎮

- Flink version: 1.17.1
- Exposed on port 8081
- Handles job scheduling and coordination
- Accessible via web interface at http://localhost:8081

### 3. TaskManager 🔧

- Flink version: 1.17.1
- Configured with 10 task slots
- Executes the actual data processing tasks
- Scales horizontally based on needs

## 📦 Prerequisites

- Docker
- Docker Compose

## 🚀 Getting Started

1. Clone the repository:

```bash
$ git clone <repository-url>
$ cd apache-flink
```

2. Start the Flink cluster:

```bash
$ docker-compose up -d
```

3. Access the services:

- Flink Dashboard: http://localhost:8081
- SQL Client: `docker exec -it sql-client /bin/bash`

## 📂 Volume Mounts

The following volumes are mounted in the containers:

- `/settings`: Configuration settings
- `/data`: Data files for processing

## 🛠️ Configuration

The environment can be customized through:

- `flink-conf.yaml` in the sql-client/conf directory
- Environment variables in docker-compose.yml
- Settings directory for additional configurations

## 🔧 Task Manager Configuration

Current settings:

- Number of task slots: 10
- Auto-scaling enabled
- Direct connection to JobManager

## 📝 Scripts

```bash
# access container
$ docker exec -it sql-client /bin/bash

# start cli client
$ ./sql-client.sh

# create flink table
$ create table
  people_job (
    id INT,
    name STRING,
    job STRING,
    salary BIGINT
  )
  WITH (
    'connector' = 'filesystem',
    'path' = 'file:///data/test.csv',
    'format' = 'csv',
    'csv.ignore-parse-errors' = 'true'
  );

# run retrieve query
$ select * from people_job;
```
