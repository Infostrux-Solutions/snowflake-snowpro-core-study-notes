# User Defined Functions #

Official Documentation: [User Defined Functions](https://docs.snowflake.com/en/sql-reference/user-defined-functions.html)

User Defined Functions (UDFs) perform custom operations that are not available through the built-in functions.

* Snowflake supports UDFs written in SQL, JavaScript, Java and Python
  * The body of a SQL UDF is enclosed in double dollar signs: `$$`; SQL is the default supported language.
  * The body of a JavaScript UDF is enclosed in single quotes `'`; the language (`javascript`) of the UDF must be specified
* UDFs can be secure or unsecure
* UDFs do not support schema definitions (DDL) or data modifications (DML)
* A UDF must return a value
  * The return value can be a single scalar value, or
  * a set of rows, if a UDF is defined as a table function (often referred as a User Defined Table Function, or UDTF)
    * A UDTF must return a table: `RETURNS TABLE`
    * When calling a UDTF, you must wrap it in the `TABLE()` function, e.g.
    ```postgres-psql
    SELECT * FROM TABLE(MY_UDTF_FUNCTION(param1, param2));
    ```
* While system functions can be listed with `SHOW FUNCTIONS;`, to list UDFs, use `SHOW USER FUNCTIONS;`
