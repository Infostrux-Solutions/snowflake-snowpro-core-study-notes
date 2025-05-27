[Back to README](../README.md) | Previous: [Overview.md](Overview.md) | Next: [StoredProcedures.md](StoredProcedures.md)

# Snowpark

*Notes related to Snowpark and Extensibility: Using Snowpark for data engineering and data science.*

## Key Topics
*   **Supported Languages:** Python, Java, Scala.
*   **Core Concepts:**
    *   **Session:** Establishing a connection to Snowflake.
    *   **DataFrames:** Lazy-evaluated, immutable, distributed collections of data organized into named columns.
    *   **Transformations:** Operations on DataFrames (e.g., `select`, `filter`, `join`, `groupBy`).
    *   **Actions:** Operations that trigger computation and return results (e.g., `collect`, `show`, `count`).
*   **Execution Model:** Snowpark code is translated into SQL and executed on Snowflake's compute engine (Virtual Warehouses).
*   **Use Cases:**
    *   ETL/ELT pipelines.
    *   Data preparation and feature engineering for machine learning.
    *   Building applications that interact with Snowflake data.
*   **Snowpark ML (Python):** Tools for end-to-end machine learning model development and deployment within Snowflake.
*   **Deployment:** Running Snowpark code as Stored Procedures or UDFs.
