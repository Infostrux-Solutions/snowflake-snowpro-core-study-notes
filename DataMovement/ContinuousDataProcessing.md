# Continuous Processing #

## Tasks ##
> [Tasks](https://docs.snowflake.com/en/user-guide/tasks-intro)

A Task is a way to run a **single SQL statement** on schedule without having to depend on external tools. A task can execute any one of the following types of SQL code:
* Single SQL statement
* Call to a stored procedure
* Procedural logic using [Snowflake Scripting](https://docs.snowflake.com/en/developer-guide/snowflake-scripting/index)

### Task Features ###
* Tasks can be queued based on the outcome of other Tasks to for DAGs
  * the Root task will be the only one to which the scheduler is set
  * The root task can have a queuing time in case something else is already in the warehouse
  * Child tasks will always have a queuing time.
  * the children’s tasks only run after the parent's task finishes
  * Each task can have a maximum of 100 children tasks
  * A tree of tasks can have a maximum of 1000 tasks, including the root one
  * each non-root task can have dependencies on multiple predecessor tasks, up to 100 predecessors
  * if we eliminated the predecessor task, there are two options:
    * Child task becomes a standalone task
    * Child task becomes a root task
  ```postgres-psql
  -- Create a child task
  CREATE TASK <newTask> AFTER <rootTask>;
  ALTER TASK <newTask> ADD AFTER <rootTask>;
  ```
  ![](../images/DataPipelineTasksDagExampleDimension.png)
* Tasks can also be used with Streams
* Tasks can call Stored Procedures
* Tasks can be run at a set `SCHEDULE` interval (in minutes) or with a cron expression
* Creating a task requires the `CREATE TASK` privilege
* Tasks are initially created in the suspended state
  * they can be started/resumed with `ALTER TASK <task_name> RESUME;`
* Tasks execute with the privileges of the owning Role
  * if the owner role of a task is deleted, task ownership is reassigned to the role that dropped the role
* Tasks cannot be triggered manually
* Snowflake ensures only one instance of a task with a schedule is executed at a given time
  * if a task is still running when the next scheduled execution time occurs, that scheduled time is **skipped**.
* Tasks also have a maximum duration of 60 minutes by default

### Task Compute Resources ###
Tasks require compute resources to execute SQL code. When a task is being created, the user has the choice to opt for using their own Virtual Warehouse or let Snowflake use serverless compute:
* User-managed Virtual Warehouse. To enable that, the Virtual Warehouse where the task would execute must be specified with the `WAREHOUSE` option, see [Optional Parameters](https://docs.snowflake.com/en/sql-reference/sql/create-task#optional-parameters)
* Snowflake-managed (i.e. serverless compute model). This is useful for frequently running tasks which would make suspending the warehouse where they run impossible. While Snowflake will automatically scale the serverless compute depending on the workload, the initial size of the serverless compute resource can be specified using `USER_TASK_MANAGED_INITIAL_WAREHOUSE_SIZE`

### Task History ###
You can use the `information_schema.task_history()` Snowflake function to query the history of task usage within a specified date range. You need one of these privileges to see the task history:
* You have the `ACCOUNTADMIN` role
* You are the owner of a task
* You have the global `MONITOR_EXECUTION` privilege
```postgres-psql
SELECT *
FROM table(information_schema.task_history())
ORDER BY scheduled_time;
```

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