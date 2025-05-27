[Back to README](../README.md) | Previous: [UDFs_UDTFs.md](../9. SnowparkAndExtensibility/UDFs_UDTFs.md) | Next: [Overview.md](Overview.md)

# Billing and Cost

*Notes related to Monitoring and Usage: Understanding Snowflake billing and managing costs.*

## Key Topics
*   **Snowflake Billing Model:**
    *   **Compute:** Billed per second (minimum 60 seconds) based on warehouse size and uptime (credits).
    *   **Storage:** Billed per terabyte per month (compressed data) for data in tables, Time Travel, Fail-safe, internal stages.
    *   **Serverless Features:** Billed based on their specific consumption metrics (e.g., Snowpipe per file/data volume, Automatic Clustering per reclustered data).
    *   **Cloud Services Layer:** Generally free, but usage exceeding 10% of daily compute credits may incur charges.
*   **Interpreting Billing Statements:** Understanding credit usage, storage costs, and other charges.
*   **Cost Management Strategies:**
    *   Right-sizing virtual warehouses.
    *   Using auto-suspend and auto-resume for warehouses.
    *   Leveraging multi-cluster warehouses effectively for concurrency.
    *   Implementing Resource Monitors.
    *   Optimizing queries to reduce compute time.
    *   Managing data retention (Time Travel settings).
    *   Choosing appropriate Snowflake editions for required features.
*   **Using `ACCOUNT_USAGE` views for cost analysis.**
