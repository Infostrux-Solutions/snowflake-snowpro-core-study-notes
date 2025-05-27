[Back to README](../README.md) | Previous: [QueryHistory.md](QueryHistory.md) | Next: [ConnectorsAndDrivers.md](../11. ClientToolsAndConnectivity/ConnectorsAndDrivers.md)

# Usage Monitoring

*Notes related to Monitoring and Usage: Monitoring resource and credit usage.*

## Key Topics
*   **`ACCOUNT_USAGE` Schema:**
    *   Primary source for historical usage data (data latency applies).
    *   **Key Views:**
        *   `WAREHOUSE_METERING_HISTORY`: Credit consumption by virtual warehouses.
        *   `STORAGE_USAGE`: Average daily storage consumption (bytes) for databases, stages, Time Travel, Fail-safe.
        *   `PIPE_USAGE_HISTORY`: Credits consumed by Snowpipe.
        *   `AUTOMATIC_CLUSTERING_HISTORY`: Credits consumed by automatic clustering.
        *   `TASK_HISTORY`: Execution status and credit usage for tasks.
        *   `REPLICATION_USAGE_HISTORY`: Credits and data transferred for replication.
        *   `MATERIALIZED_VIEW_REFRESH_HISTORY`: Credits for materialized view maintenance.
        *   `SEARCH_OPTIMIZATION_HISTORY`: Credits for search optimization service.
*   **`INFORMATION_SCHEMA`:** Provides real-time metadata and some usage information (e.g., `LOAD_HISTORY` for recent loads).
*   **Resource Monitors:** Proactive control over credit usage (covered in Virtual Warehouses section).
*   **Snowsight UI:** Dashboards and views for visualizing usage (e.g., "Admin" -> "Usage").
