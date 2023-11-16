# Performance and Tuning Overview #

## Query Optimizer Workflow ##
Typical workflow of the Snowflake query optimizer:
1. Row Operations: Inspect `FROM`, `JOIN` and `WHERE` clauses for partition pruning
   * Static pruning based on the columns in the `WHERE` clause based on the `MIN/MAX` micro-partition metadata
   * Dynamic pruning based on the `JOIN` columns
2. Inspect `GROUP BY` and `HAVING`
3. Inspect `SELECT`, `DISTINCT`, `ORDER BY` and `LIMIT`

## Query Optimization Tips ##
* Take advantage of partition pruning by limiting the initial data set as much as possible.
  * Use appropriate filters as early as possible
  * Filter on columns which would be naturally ordered (or have been clustered to be ordered) in micro-partitions
    * Natural clustering occurs on columns which have high correlation to ingestion order, e.g. date columns
  * When filtering by string value, avoid wildcards at the beginning of the string as the optimizer cannot take advantage of the `MIN/MAX` micro-partition metadata
  * Prefer uncorrelated over correlated subqueries. A correlated subquery is one which would have to execute multiple times since its query clause (or, worse, clauses!) depends on multiple values from the parent query.  
* Join on unique keys
  * Ensure keys are distinct to avoid join explosions
  * Understand relationships between tables before joining
  * Avoid many-to-main joins
  * Avoid unintentional cross joins
* Prefer low cardinality columns for `GROUP BY` clauses
* Add `LIMIT` to `ORDER BY` clauses where possible
* Limit `ORDER BY` usage to a single instance in the top level `SELECT` wherever possible
* Review the query `Profile Overview` for
  * spilling to disk
  * high network usage

## Altering Query Behaviour ##
These can be set for at the Account/Session/Role or Virtual Warehouse level:
* `STATEMENT_TIMEOUT_IN_SECONDS`: How long can a query run before being cancelled by the system, Default: 2 days
* `STATEMENT_QUEUED_TIMEOUT_IN_SECONDS`:  How long can a queued query wait before being cancelled by the system, Default: 0 (forever)
