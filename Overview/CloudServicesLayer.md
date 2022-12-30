# Cloud Services Layer #

* Manages all activity across Snowflake
  * Centralized storage
    * Micropartitions
    * Micropartition versioning for Time Travel
  * Compute
  * Metadata and Statistics collected and kept up-to-date
  * Handles queries that depend on Metadata only (no Warehouse required), e.g.:
    * Retrieve or modify the session context
    * Retrieve metadata about objects (users, warehouses, databases)
    * Get statistics, e.g.: `MIN` and `MAX` of a column, `COUNT`, number of `NULL`s
    * DDL retrieval
  * Time Travel and Cloning
  * Security
    * Authentication
    * Access Control
      * Roles and Users
      * Shares
    * Encryption Key Management
  * Transactions
  * SQL Optimization
    * Cost-based
    * Automatic `JOIN` order optimization (no hints required)
    * Automatic statistics gathering
    * Data Pruning based on the metadata and statistics  
  * Availability
  * Transparent online updates and patches
* Runs on Snowflake-managed compute
