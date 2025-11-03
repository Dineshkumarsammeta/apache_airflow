# Apache Airflow Projects  
This repository contains a set of workflows/DAGs built using **Apache Airflow** to support automation, scheduling, monitoring and orchestration of data pipelines.

## 📋 Table of Contents  
- [About](#about)  
- [Features](#features)  
- [Repository Structure](#repository‐structure)  
- [Getting Started](#getting‐started)  
  - [Prerequisites](#prerequisites)  
  - [Installation](#installation)  
  - [Running the Web Server & Scheduler](#running‐the‐web‐server‐scheduler)  
- [Usage](#usage)  
  - [How to Add a DAG](#how‐to‐add­a‐dag)  
  - [How to Trigger & Monitor](#how‐to‐trigger‐monitor)  
- [Configuration](#configuration)  
- [Best Practices](#best‐practices)  
- [License](#license)  
- [Contributing](#contributing)  
- [Contact](#contact)  

## About  
This project is designed to manage, schedule and monitor data workflows using Apache Airflow. It includes a set of sample and production-ready DAGs (Directed Acyclic Graphs) that demonstrate good practices for orchestration, logging, dependency management, and error handling.

## Features  
- 🚀 Scalable task scheduling and orchestration using Airflow’s core concepts (DAGs, Operators, Tasks)  
- Modular DAGs stored in a `dags/` folder for clarity  
- Logs persisted in `logs/` folder for auditing and troubleshooting  
- Example configuration files (e.g., `airflow.cfg`, `webserver_config.py`) to customise behaviour  
- Extensible — add your own DAGs, operators, hooks easily  

## Repository Structure  
├── dags/ # Airflow DAG definitions
├── logs/ # Airflow task logs
├── airflow.cfg # Airflow configuration file
├── webserver_config.py # Webserver custom configuration
├── airflow.db # SQLite DB for local dev (not recommended for production)
└── README.md # This file

bash
Copy code

## Getting Started  

### Prerequisites  
- Python 3.7+  
- pip  
- A virtual environment tool (recommended: `venv` or `conda`)  
- (For production) A more robust metadata database (PostgreSQL/MySQL) and message broker (RabbitMQ/Redis)  

### Installation  
```bash
# Clone the repository  
git clone https://github.com/Dineshkumarsammeta/apache_airflow.git  
cd apache_airflow  

# Create and activate virtual environment  
python3 -m venv .venv  
source .venv/bin/activate    # On Windows: .venv\Scripts\activate  

# Install dependencies  
pip install apache-airflow  # or pin a version: apache-airflow==2.x.x  
Running the Web Server & Scheduler
bash
Copy code
# Initialise the metadata database (for first time)  
airflow db init  

# Create a user for the web UI (one-time)  
airflow users create \
    --username admin \
    --firstname Admin \
    --lastname User \
    --role Admin \
    --email admin@example.com  

# Start the web server  
airflow webserver --port 8080  

# In another shell, start the scheduler  
airflow scheduler  
Then open your browser pointing to http://localhost:8080 to view the Airflow UI.

Usage
How to Add a DAG
Copy your DAG file to the dags/ directory.

Follow naming conventions (e.g., example_my_dag.py) and ensure dag_id, schedule, default_args are set.

The DAG will appear in the UI shortly after the scheduler detects it.

How to Trigger & Monitor
Use the UI to trigger DAG runs manually or rely on schedule_interval.

Monitor task status, logs and retries via the UI.

Logs for each task run are available under the logs/ folder.

Configuration
You can customise behaviour via airflow.cfg and webserver_config.py.
Some key settings you may want to adjust:

executor (e.g., LocalExecutor, CeleryExecutor)

sql_alchemy_conn to point to a production-grade database

dags_folder to change where DAGs are picked up

base_log_folder to change log storage

Best Practices
Version control your DAGs and dependencies.

Do not use SQLite for production metadata; switch to PostgreSQL or MySQL.

Use LocalExecutor only for small deployments; use CeleryExecutor / Kubernetes for scale.

Isolate tasks (idempotent, retryable).

Use connection IDs and variables instead of hard‐coding credentials.

Use branching, task groups, sub-DAGs for complex workflows.

Monitor and alert on failures, retries, SLA misses.

License
This project is released under the MIT License — see LICENSE for details.

Contributing
Contributions are welcome! Whether it’s a bug fix, new feature or improved documentation:

Fork the repository

Create your feature branch (git checkout -b feature-xyz)

Commit your changes (git commit -m 'Add new DAG for xyz')

Push to the branch (git push origin feature-xyz)

Open a Pull Request and describe your changes

Contact
Maintainer: Dinesh Kumar Sammeta
GitHub profile: https://github.com/Dineshkumarsammeta
Feel free to open issues or pull requests for feedback or suggestions.
