[Back to README](../README.md) | Previous: [Overview.md](Overview.md) | Next: [UsageMonitoring.md](UsageMonitoring.md)

# Query History

*Notes related to Monitoring and Usage: Understanding and using Query History.*

## Key Topics
*   **Accessing Query History:**
    *   **Snowsight UI:**
        *   "Activity" -> "Query History" page.
        *   Filtering, sorting, and viewing query details.
        *   Accessing the Query Profile for detailed execution plan analysis.
    *   **SQL:**
        *   `ACCOUNT_USAGE.QUERY_HISTORY` view (data latency up to 45 mins - 3 hours).
        *   `TABLE(INFORMATION_SCHEMA.QUERY_HISTORY(...))` table function (real-time for recent queries, limited history).
*   **Information Available:**
    *   Query ID, query text, user, role, warehouse used, status (running, success, failed), start time, end time, duration.
    *   Bytes scanned, partitions scanned, rows produced.
    *   Error messages for failed queries.
*   **Use Cases:** Troubleshooting failed queries, identifying long-running queries, performance analysis, auditing query activity.
*   **Query Profile:** Detailed graphical representation of query execution plan, operator statistics, and potential bottlenecks.
