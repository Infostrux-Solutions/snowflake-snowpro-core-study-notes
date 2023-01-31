# Continuous Processing #

## Tasks ##
A Task is a way to run a SQL statement without having to depend on external tools but rather Snowflake's own scheduling
* Tasks can be queued based on the outcome of other Tasks
* Tasks can also be used with Streams
* Tasks can call Stored Procedures
* Tasks can be run at a set `SCHEDULE` interval (in minutes) or with a cron expression
* Creating a task requires the `CREATE TASK` privilege
* Tasks are initially created in the suspended state, they can be started/resumed with `ALTER TASK <task_name> RESUME;`
* Tasks execute with the privileges of the owning Role
* Tasks cannot be triggered manually
* A Task needs to have a defined Warehouse which it can use
  * the Warehouse must have been created in advance - it cannot be created within the task

## Streams ##
A Stream can be created on a table and used for CDC (Change Data Capture) to identify and act on changed records.
* Streams hold no data. They can be thought of as timestamped bookmarks for a particular state of a table
* Streams can be of two types:
  * Standard Stream
    * Captures all changes in the table records
    * The Streams metadata columns capture:
      * what the action was - `INSERT`, `UPDATE`, `DELETE`, etc.
      * whether it was an update
      * `row_id` impacted by the change
  * Append-Only Stream