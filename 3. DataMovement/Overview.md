[Back to README](../README.md) | Previous: [DataUnloading.md](DataUnloading.md) | Next: [AccessControl.md](../4. AccountAndSecurity/AccessControl.md)

# Data Movement #

Loading and unloading data into Snowflake can be:
* [Bulk Loading](./BulkLoading.md)
* [Continuous Data Loading](./ContinuousDataLoading.md)
* using a Connector

Factors which affect loading times are
* the physical location of the stage,
* GZIP compression efficiency, or
* the number and types of columns

You can both load and unload data into tables with the `COPY` command
* LOAD: copy data from a stage into a Snowflake table 
* UNLOAD: copy data from a table to a stage

## File Formats ##
A schema-level named object which defines the format information required for Snowflake to interpret a file. You can specify different parameters, for example, the file’s delimiter, if you want to skip the header or not, etc.

| Format  | Type            | Load | Unload | Binary Format |
|---------|-----------------|------|--------|---------------|
| CSV     | Structured      | Yes  | Yes    | No            |
| JSON    | Semi-structured | Yes  | Yes    | No            |
| Parquet | Semi-structured | Yes  | Yes    | Yes           |
| XML     | Semi-structured | Yes  | No     | No            |
| AVRO    | Semi-structured | Yes  | No     | Yes           |
| ORC     | Semi-structured | Yes  | No     | Yes           |

* Structured data: CSV
  * It’s the fastest file format to load data
  * May need to specify `FIELD_DELIMITER`, `RECORD_DELIMITER` and whether the file header should be skipped with `SKIP_HEADER`
* Semi-structured data: JSON, Parquet, Avro, ORC, XML
  * Semi-structured data can be loaded as a `VARIANT` type in a Snowflake table
  * The maximum size for the `VARIANT` data type is 16MB
  * it can be queried using JSON notation, see [Query Semi-Structured Data](../SemiStructuredData/QuerySemiStructuredData.md)
* File Format has to be specified for every `COPY INTO` command
  * A File Format can be attached to a stage - automatically associates the File Format for all files stored in the stage
  * A File Format can be attached to a table - automatically associates the File Format for all `COPY INTO` commands targeting the table
  * A File Format can be specified for each `COPY INTO` command which will override the stage or table ones, if specified


[Back to README](../README.md) | Previous: [DataUnloading.md](DataUnloading.md) | Next: [AccessControl.md](../4. AccountAndSecurity/AccessControl.md)
