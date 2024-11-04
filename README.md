# DBT ELT Data Pipeline

## Overview
This project is an ELT (Extract, Load, Transform) Data Pipeline that integrates **dbt (data build tool)**, **Snowflake**, and **Docker**, and **Apache Airflow** to automate tasks for data processing and transformation. The pipeline extracts data, loads it into Snowflake, transforms it using dbt models, and orchestrates the entire workflow using Airflow. The project utilizes **Astronomer** for Airflow deployment and management, leveraging **Astronomer Cosmos** for smooth integration of dbt within Airflow DAGs.

## Features
- **dbt Data Transformation**: Modular SQL transformations using dbt models, macros, and tests.
- **Airflow Orchestration**: Automated scheduling and execution of the data pipeline using Airflow DAGs.
- **Dockerized Environment**: Containerization of the entire application using Docker for consistency across environments.
- **Snowflake Integration**: Secure connection and data management within the Snowflake cloud data warehouse.
- **Astronomer Cosmos Integration**: Simplifies the integration of dbt within Airflow.
- **Data Quality Assurance**: Implemented tests and validations to ensure data integrity.
- **Scalable**: Easy to scale and maintain due to modular design and use of industry-standard tools.

## Usage
### Starting the Airflow Environment
1. **Build and Start the Docker Containers**:
    ```
    astro dev start
    ```

2. **Access the Airflow Web Interface**:
    Open your browser and navigate to `http://localhost:8080`.
    - **Default Credentials**:
        - Username: `admin`
        - Password: `admin`

3. **Trigger the DAG**:
    - Locate the `dbt_dag` in the Airflow UI.
    - Toggle the DAG to the "on" position if it's paused.
    - Manually trigger the DAG or let it run according to its schedule.

4. **Monitor the Pipeline**:
    - Use the Airflow UI to monitor task execution, view logs, and troubleshoot if necessary.

### Stopping the Airflow Environment
To stop the Airflow services and Docker containers:
    ```bash
    astro dev stop
    ```

## Prerequisites
- **Docker**: Ensure Docker is installed and running on your machine.
- **dbt**: Installed within the Docker container via the `Dockerfile`.
- **Astronomer CLI**: Install the Astronomer CLI to manage Airflow projects.
    - Install via Homebrew:
        ```
        brew install astro
        ```
- **Snowflake Account**: Access to a Snowflake data warehouse with appropriate permissions.
- **Python Virtual Environment**: (Optional) For local development and testing.

## Input
- **Raw Data Sources**: The pipeline is designed to work with TPCH datasets.
- **dbt Models**: SQL files located in the `models/` directory defining the transformations.
- **Macros and Tests**: Custom dbt macros and tests to ensure data quality.
- **Airflow DAGs**: Python files defining the workflows, located in the `dags/` directory.

## Output
- **Transformed Data**: Cleaned and transformed data loaded into Snowflake, ready for analysis.
- **Fact and Dimension Tables**: Created in Snowflake based on the dbt models.
- **Logs and Reports**: Execution logs available in Airflow for monitoring and troubleshooting.

## Notes
- **Configuration Files**:
    - **Dockerfile**: Defines the Docker image.
    - **requirements.txt**: Lists the Python dependencies.
    - **airflow_settings.yaml**: Used to set up Airflow connections and variables.

- **Airflow Connections**:
    - A Snowflake connection (`snowflake_conn`) must be configured in Airflow with the correct account name, username, password, and other optional parameters like warehouse, database, schema, and role.

- **dbt Integration**:
    - The `dbt_dag.py` file defines the Airflow DAG that orchestrates the dbt project.
    - Ensure that the paths in `dbt_dag.py` are correctly set to point to the dbt project and the `dbt` executable within the Docker container.

- **Extensibility**:
    - The pipeline can be extended to include additional data sources, transformations, and outputs.
    - Additional DAGs and tasks can be added to the Airflow project as needed.