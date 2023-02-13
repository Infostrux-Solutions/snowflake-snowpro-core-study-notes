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
* LOAD: copy data from the stages into a Snowflake table 
* UNLOAD: co;y data from a table to a stage, or external location

## File Formats ##
A named object that lives inside a `SCHEMA` which defines how Snowflake would read a file. Supported file types
* Structured data: CSV
  * May need to specify `FIELD_DELIMITER`, `RECORD_DELIMITER` and whether the file header should be skipped with `SKIP_HEADER`
* Semi-structured data: JSON, Parquet, Avro, ORC, XML
* File Format has to be specified for every `COPY INTO` command
  * A File Format can be attached to a stage - automatically associates the File Format for all files stored in the stage
  * A File Format can be attached to a table - automatically associates the File Format for all `COPY INTO` commands targeting the table
  * A File Format can be specified for each `COPY INTO` command which will override the stage or table ones, if specified 

## Pipe (Snowpipe) ##
Enables streaming/pipeline/micro-batch data loading into Snowflake.
* Specify the `COPY INTO` command that is used to load the data
* Can be used with structured and semi-structured data
