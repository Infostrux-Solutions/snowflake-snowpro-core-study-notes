# Objects #
* All objects in Snowflake are securable.
* Other than the Organization object, objects can be at the Account level or the Schema level
  * Account level objects:
    * User
    * Role
    * Grants
    * Warehouse
    * Database
    * Resource Monitor
    * Integration
  * Schema level objects:
    * Table
    * External Table
    * View
    * Stream
    * Task
    * Stored Procedure
    * UDF (User Defined Function)
    * Sequence
    * Stage
    * File Format
    * Pipe
* The definitions of most objects can be retrieved using the [GET_DDL()](https://docs.snowflake.com/en/sql-reference/functions/get_ddl.html) function.

## Organization ##
Top level securable object which serves as a logical grouping of Accounts.

## Account ##
Logical grouping of Databases. The account's name must be unique within an organization, regardless of which Snowflake region the account is in. The URL of the account consists of the account identifier, the cloud provider region and the snowflake domain, `snowflakecomputing.com`, e.g. `tn10000.eu-west-1.snowflakecomputing.com`. It is possible to request a vanity address to convert the identifier into your company's name.

## Warehouse ##
Warehouses are the compute part of the Snowflake engine. They are a set of virtual machines provided at runtime to help execute a given query.

## Database ##
Logical collection of Schemas.
* Databases can be created as `Transient`
  * Time Travel: 0 or 1 days
  * No Fail-Safe support

## Schema ##
Logical grouping of Tables, Views, Stored Procedures, UDFs, Stages, File Formats, Pipes, Sequences, Shares, etc. Every schema belongs to a single Database. When a database is created, there are two default schemas created in it
* `public`: default schema for any object created without specifying a schema
* `information_schema`: stores metadata information
* Schemas can be created as `Transient`.
  * Time Travel: 0 or 1 days
  * No Fail-Safe support

## Table ##
Contains all the data in a database.

### Permanent ###
* Default table type, used for the highest level of data protection and recovery
* Persists until dropped
* Up to 90 days or Time Travel (on Snowflake Enterprise edition and higher)
* Fail-Safe support

### Transient ###
* Persists until dropped
* Available across sessions
* Time Travel: 0 or 1 days
* No Fail-Safe support

### Temporary ###
* Used for transitory data
* Tied to and available only within the context a single user session
* Time Travel: 0 or 1 days
* No Fail-Safe support

### External ###
* Snowflake table "over" data stored in an external data lake
* Data is accessed via an external stage
* Persists until removed
* Read-only
* No Time Travel
* No Fail-Safe support

## View ##
Named definition of a SQL query which can be queried as if it were a table.

### Standard ###
* Default view type
* Executes as the role which owns it
* DDL available to any role with access to the view

### Secure ###
* Executes as the role which owns it
* DDL available only to authorized users
* Snowflake query optimizer bypasses optimizations used for regular views so secure views are less performant

### Materialized ###
* Results of underlying query are stored
  * Incurs storage costs
* Behaves more like a table
* Results are autorefreshed in the background
* Consumes background compute for the auto-refresh
  * The background compute does not require a customer-provided warehouse; Snowflake manages the compute
* Secure materialized views are supported

## Stage ##
Object pointing to the location of data files in cloud storage

## File Format ##
Pre-defined format structure that describes a set of staged data to access or load into Snowflake tables for CSV, JSON, AVRO, ORC, PARQUET, and XML input types

## Sequence ##
You can generate unique numbers with sequences. They are like counters.

## Pipe ##
A special type of object which enables the automatic loading of data from Stage files as soon as they are available.

## Stored Procedure ##
> [Stored Procedure](https://docs.snowflake.com/en/sql-reference/stored-procedures.html)

Extend the system to perform operations.
* A stored procedure can return a single value or (if you are using Snowflake Scripting) tabular data
* Stored procedures can be written in:
  * Java (using Snowpark)
  * JavaScript
  * Python (using Snowpark)
  * Scala (using Snowpark)
  * [Snowflake Scripting](https://docs.snowflake.com/en/developer-guide/snowflake-scripting/index.html), an extension to Snowflake SQL that adds support for procedural logic
* Stored Procedures can be secure or unsecure
* Stored Procedures support schema definition (DDL) and data modification (DML) SQL statements
* Stored Procedures can run multiple SQL statements.
* Stored Procedures are allowed, but not required, to explicitly return a value (such as an error indicator)
* Store Procedures CANNOT return a set of rows
* Stored Procedures can be defined to run as their owner (by default) or as the procedure caller (`EXECUTE AS CALLER`)
* Stored Procedures can be defined to run as their owner (by default) or as the procedure caller (`EXECUTE AS CALLER`)
* Stored Procedures interact with Snowflake using an API in the respective language, e.g. JavaScript API
  * API Objects:
    * `Snowflake` - contains the methods of the Stored Procedure API; this object is accessible by default (there is no need to create it)
    * `Statement` - provides method to execute a query statement and access its metadata
    * `ResultSet` - iterable object which contains the query results;
    * `SfDate` - wrapper around the Snowflake SQL `TIMESTAMP` data types
  * Snowflake Stored Procedures allow migrating of other databases' stored procedures by embedding their SQL in the Snowflake Stored Procedure's API code
* Argument names in the SQL portions of a Stored Procedure are case-insensitive

## UDF: User-Defined Function ##
> [User Defined Function](https://docs.snowflake.com/en/sql-reference/user-defined-functions.html)

Extend Snowflake to perform operations that are not available through built-in, system-defined functions.
* UDFs accept 0 or more parameters.
* For each row passed to a UDF, the UDF returns either:
  * a scalar (i.e. single) value, or
  * if defined as a `RETURNS TABLE` function, a set of rows. When the UDF returns a table, it can be called a User Defined Table Function (UDTF)
* A UDF can be written in:
  * Java
  * JavaScript
  * Python
  * SQL (default support language)
* UDFs can be secure or unsecure
* UDFs do not support schema definitions (DDL) or data modifications (DML)
* While system functions can be listed with `SHOW FUNCTIONS;`, to list UDFs, use `SHOW USER FUNCTIONS;`
* When calling a UDF which returns a table, you must wrap it in the `TABLE()` function
  ```postgres-psql
  SELECT * FROM TABLE(MY_UDTF_FUNCTION(param1, param2));
  ```

## Data Shares ##
See [Data Sharing](DataSharing.md)
