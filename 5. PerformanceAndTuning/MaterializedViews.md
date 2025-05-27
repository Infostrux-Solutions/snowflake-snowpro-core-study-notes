[Back to README](../README.md) | Previous: [DataClustering.md](DataClustering.md) | Next: [Overview.md](Overview.md)

# Materialized Views

*Notes related to Performance and Tuning: Understanding and using Materialized Views.*

## Key Topics
*   **Concept:** Pre-computed datasets based on a query definition, stored like a table. Results are kept up-to-date automatically by Snowflake.
*   **Purpose:** Improve performance for complex, frequently executed queries, especially those involving aggregations or joins on large datasets.
*   **Creation:** `CREATE MATERIALIZED VIEW <view_name> AS <query_definition>`
*   **Maintenance:** Snowflake automatically and transparently maintains materialized views as base table data changes. This incurs compute costs.
*   **Query Rewrite:** The Snowflake optimizer can automatically rewrite queries against base tables to use a relevant materialized view if it improves performance.
*   **Use Cases:** Accelerating dashboards, BI reports, and common analytical queries.
*   **Limitations and Considerations:** Restrictions on query definitions (e.g., no non-deterministic functions, no UDFs, specific join types), impact of base table changes on refresh costs.
*   **Monitoring:** `MATERIALIZED_VIEW_REFRESH_HISTORY` in `ACCOUNT_USAGE`.


[Back to README](../README.md) | Previous: [DataClustering.md](DataClustering.md) | Next: [Overview.md](Overview.md)
