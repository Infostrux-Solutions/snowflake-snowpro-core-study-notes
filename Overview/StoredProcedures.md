# Stored Procedures #

> [Stored Procedures](https://docs.snowflake.com/en/sql-reference/stored-procedures.html)

Stored Procedures allow procedural logic and error handling that SQL does not support

* Snowflake supports writing Stored Procedures in JavaScript, Java, Python and Scala
* Stored Procedures can be secure or unsecure
* Stored Procedures support schema definition (DDL) and data modification (DML) SQL statements
* Stored Procedures can run multiple SQL statements.
* Stored Procedures are allowed, but not required, to explicitly return a value (such as an error indicator)
* Store Procedures CANNOT return a set of rows
* Stored Procedures can be defined to run as their owner (by default) or as the procedure caller (`EXECUTE AS CALLER`)
* Stored Procedures interact with Snowflake using an API in the respective language, e.g. JavaScript API
  * API Objects:
    * `Snowflake` - contains the methods of the Stored Procedure API; this object is accessible by default (there is no need to create it)
    * `Statement` - provides method to execute a query statement and access its metadata
    * `ResultSet` - iterable object which contains the query results;
    * `SfDate` - wrapper around the Snowflake SQL `TIMESTAMP` data types
  * Snowflake Stored Procedures allow migrating of other databases' stored procedures by embedding their SQL in the Snowflake Stored Procedure's API code 
* Argument names in the SQL portions of a Stored Procedure are case-insensitive
* The body of a Stored Procedure is enclosed in double dollar signs: `$$`
