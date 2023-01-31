# Data Clustering #

## Natural Clustering ##
* As data is loaded into a table, micro-partitions are created based on ingestion order. That is natural clustering.
  * Natural clustering occurs when data is read as a single data load
* The ingestion order may be highly correlated with the values in one or more columns, e.g. autoincrement IDs, dates, sequential numbers, etc.
* The source data organization determines what range of values (`MIN/MAX`) is represented in each micro-partition

## Clustering Keys ##
When the ingestion-order natural clustering is not advantageous, it can be overriden by designating clustering keys. This will result in like data (by key) being co-loaded in the same micro-partitions.
```iso92-sql
CREATE|ALTER TABLE ...
CLUSTER BY (<column_or_expression>, ...)
```
* Use one to three clustering keys at maximum
* Prefer and order clustering keys from low to high cardinality which will result in fewer, larger sets of micro-partitions being co-located together
* Snowflake maintains and updates the clustering order in the background which incurs compute and storage costs as micropartitions need to be rewritten
* Typically, clusering keys are added after ingestion, and/or when natural clustering is no longer helpfull.

### Clustering Keys Considerations ###
* Clustering keys are most useful with very large tables (multi-terabyte range) or tables where query performance degrades as the table gets larger.
* Frequently-changing tables will consume more credits for reclustering
* Automatic clustering can be suspended and resumed
* The `SYSTEM$CLUSTERING_INFORMATION()` function can be used to get clustering information on a table's column. Good clustering will result in:
  * low `average_depth` values which indicates low similarity between micro-partition `MIN/MAX` values
  * `partition_depth_histogram` with a high number of low value depths

