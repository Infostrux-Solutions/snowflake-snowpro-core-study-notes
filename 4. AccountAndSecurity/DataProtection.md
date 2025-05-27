[Back to README](../README.md) | Previous: [Authorization.md](Authorization.md) | Next: [Overview.md](Overview.md)

# Data Protection #

> [Continuous Data Protection](https://docs.snowflake.com/en/user-guide/data-cdp.html)

## Encryption at Rest and in Transit ##
* Encryption in transit for all client communication using TLS 1.2 SSL
* AES 256 bit encryption at rest and in motion
* Encryption at every level, see [Hierarchical encryption key model](https://docs.snowflake.com/en/user-guide/security-encryption-manage.html#hierarchical-key-model)
  * Root Key
  * Account master Key - each account has its own key
  * Object Master Keys - each object has its own key
  * File Keys - each micro-partition file has its own key
* Automatic key expiration and rotation with no customer impact every 30 days. Key states:
  * active: used for encryption and decryption
  * retired: used for decryption of data previously encrypted with that key
  * destroyed: no longer used
* Enterprise Edition and above can enable automatic annual re-keying
* Tri-Secret Secure or Bring Your Own Key
  * uses a composite master key which is a composite of a customer-maintained key with a Snowflake-managed key
  * the customer-maintained key must be available at all times for continuous access
* Staging Encryption
  * In Snowflake-managed internal stages, Snowflake manages encryption
  * Customers can also choose to manage their own cloud storage stages where they would need to secure and encrypt the data prior to loading into Snowflake

## Continuous Availability ##
* Cloud providers replicate Snowflake storage across at least three availability zones within each cloud region where Snowflake is deployed
  * Each availability zone consists of multiple data centers which are:
    * geographically separated
    * have their own security
    * are on separate power grids
    * have their own individual power backups
* Snowflake performs fully transparent online updates and patches with no maintenance downtime windows

## Snowflake-specific Data Security Features ##

### Time Travel ###

> [Understanding & Using Time Travel](https://docs.snowflake.com/en/user-guide/data-time-travel.html)

Access historical data at any point of time within a defined retention time period. Allows querying/rollback to a previous state of a table/schema/DB within the retention period.

* Maximum retention period can be configured per account, DB, schema and/or table by setting `DATA_RETENTION_TIME_IN_DAYS`:
  * Standard Edition - up to 1 day
  * Enterprise Edition and higher - up to 90 days
  * The default retention time is 1 day in all editions unless explicitly changed
  * Can be disabled by setting `DATA_RETENTION_TIME_IN_DAYS = 0`
  * To view current settings, use [SHOW PARAMETERS](https://docs.snowflake.com/en/sql-reference/sql/show-parameters.html)
* Allows fixing common mistakes
  * `UNDROP` a DB/Schema/Table
    * Attempting to restore an object with a name that already exists will result in an error
  * Access the previous state of a table with [AT or BEFORE](https://docs.snowflake.com/en/sql-reference/constructs/at-before.html)
    * Query the data in its previous state
    * Clone a DB/Schema/Table from its preivous state
    ```
    -- by Timestamp
    SELECT *
    FROM my_table
    AT(timestamp => 'Mon, 01 May 2021 08:00:00 -0700'::timestamp_tz);

    -- by Offset
    SELECT *
    FROM my_table
    AT(offset => -60*15);

    -- before query statement ID
    SELECT *
    FROM my_table
    BEFORE(STATEMENT => '8e5d0ca9-005e-44e6-b858-a8f5b37c5726');
    ```
* Adds to storage costs for maintaining the additional historical data

### Zero-Copy Cloning ###
Enables taking a quick snapshot of a DB/schema/table.

* Zero-copy cloning is a metadata-only operation
  * Zero-Copy cloning is a FREE operation
* Originally, both the original and the clone's objects are pointing to the same micro-partitions
* No data is copied, so no additional storage costs are incurred until data is changed in the original or in the clone
* Usage
  * often used to quickly spin up a Dev or Test environment as a zero-copy clone of Production
  * can be used to create backups or data snapshots at given points of time
  * can be used to create read-only snapshots for reporting as of a given point of time, e.g.: month-, year-end, etc.
* Some considerations:
  * Privileges are not cloned
  * Data History is not cloned
  * Stages cloning
    * Named Internal Stages are not cloned
    * External Stages are cloned
    * Table Stages are cloned
  * Pipes cloning: pipes that reference
    * internal stages are not cloned
    * external stages are cloned
* Privileges required for cloning objects:
  * Table: `SELECT`
  * Pipe, Stream, Task: `OWNERSHIP`
  * all other objects: `USAGE`

### Fail-Safe ###
Non-configurable, 7-day retention for historical data after the Time Travel expiration
* Only accessible by Snowflake support personnel
* Fail-safe cannot be disabled
* Admins can view Fail Safe storage use in the Web UI under `Account > Billing & Usage`
* Only permanent tables have a Fail-Safe period. Not supported for Temporary, Transient or External tables
* Adds to storage costs for maintaining the additional historical data

### Snowflake replication features ###
Snowflake provides customers with additional replication features, over and above the cloud providers' replication across availability zones.


[Back to README](../README.md) | Previous: [Authorization.md](Authorization.md) | Next: [Overview.md](Overview.md)
