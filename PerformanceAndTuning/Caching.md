# Caching #

One of the most important ways to improve the speed of queries in Snowflake and optimize costs is the cache. There are several different caches in Snowflake: Metadata, Query Result, and Warehouse cache.

## Metadata Cache ##
The Metadata cache is maintained in the Cloud Services Layer and contains objects information & statistics (see [Architecture](../Overview/Architecture.md)). Snowflake automatically stores different types of metadata to improve the compilation time and query optimization. This helps in operations like `MIN`, `MAX`, `COUNT`, etc., where Snowflake does not need to use the warehouses (and no computing credits are charged), as it has the information already available in the metadata cache.
* The metadata cache information is stored for 64 days
* The metadata cache contains information about staged files and their ingestion status

## Query Result Cache ##
The Cloud Services Layer accepts SQL requests from users, coordinates queries, managing transactions and results and also holds the Query Results Cache
* Holds the results of every query executed in the past 24 hours up to 31 days (depending on how  many times it's reused).
* The query results are available across virtual warehouses, so cached query results returned are available to all users of the system, provided the underlying data has not changed
  * If the data in the Storage Layer changes, the caches are automatically invalidated.
* No data is scanned from the Storage Layer and no compute is required so no computing credits are charged for cached results
* Cached query results do NOT incur Storage costs
* Can't have context functions (e.g. current_time())
* Same role is used as the previous query
* You can disable the Query Result cache with this command:
  ```
  ALTER SESSION SET USE_CACHED_RESULT = FALSE
  ```

## Warehouse Cache ##
The actual SQL is executed across the nodes of a Virtual Data Warehouse. This layer holds a cache of the micro-partition data queried, and is often referred to as Local Disk I/O although in reality this is implemented using SSD storage.
* All data in the compute layer is temporary, and only held as long as the virtual warehouse is active.
* Suspending or resizing a warehouse will clear the data cache
  * A low Auto-Suspend setting (e.g. auto-suspend after 1 minute) minimizes the use of the Warehouse data cache
  * A resized Warehouse (up or down) starts with a cold (clear) cache 
* You can get information on how much data is read from Local (Warehouse) storage vs. Remote (Storage layer) by inspecting the query profile's "Scanned Bytes" metric.
* It is recommended to use dedicated Virtual Warehouses for similar workloads. For example, a Virtual Warehouse for BI tasks, another for Data Science, etc. There is a chance that data cached by the warehouse for similar queries can can be re-used
* The larger a warehouse is, the larger the warehouse cache size is