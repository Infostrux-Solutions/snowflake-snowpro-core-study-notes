[Back to README](../README.md) | Previous: [QuerySemiStructuredData.md](../6. SemiStructuredData/QuerySemiStructuredData.md) | Next: [Functions.md](Functions.md)

# DDL and DML

*Notes related to SQL and Querying: Data Definition Language (DDL) and Data Manipulation Language (DML) commands.*

## Key Topics
*   **Data Definition Language (DDL):**
    *   `CREATE`: `DATABASE`, `SCHEMA`, `TABLE` (including `TRANSIENT`, `TEMPORARY`), `VIEW` (including `SECURE`, `MATERIALIZED`), `SEQUENCE`, `FILE FORMAT`, `STAGE`, `PIPE`, `STREAM`, `TASK`, `FUNCTION`, `PROCEDURE`, `ROLE`, `USER`, `WAREHOUSE`, `RESOURCE MONITOR`.
    *   `ALTER`: Modifying existing objects (e.g., `ALTER TABLE ADD COLUMN`, `ALTER WAREHOUSE SET WAREHOUSE_SIZE = 'MEDIUM'`).
    *   `DROP`: Removing objects (e.g., `DROP TABLE`).
    *   `UNDROP`: Restoring dropped objects (leveraging Time Travel).
    *   `SHOW`: Listing objects (e.g., `SHOW TABLES`, `SHOW WAREHOUSES`).
    *   `DESCRIBE`: Displaying object metadata (e.g., `DESCRIBE TABLE`).
*   **Data Manipulation Language (DML):**
    *   `INSERT`: Adding new rows to a table.
    *   `UPDATE`: Modifying existing rows.
    *   `DELETE`: Removing rows.
    *   `MERGE`: Performing `INSERT`, `UPDATE`, and `DELETE` operations in a single statement (UPSERT).
    *   `TRUNCATE TABLE`: Removing all rows from a table (faster than `DELETE` for full table clear).
*   **Transactions:**
    *   `BEGIN`, `COMMIT`, `ROLLBACK`.
    *   Understanding auto-commit behavior in Snowflake.
    *   Multi-statement transactions.
