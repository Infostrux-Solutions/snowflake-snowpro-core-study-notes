# Data Movement #

Loading and unloading data into Snowflake can be:
* Bulk Loading
* Snowpipe Pipelines
* using a Connector

When data is loaded into Snowflake, it is stored in micropartitions
* each micropartition contains a subset of the ingested table rows
* data in the micropartition is compressed and encrypted
* for each micropartition, Snowflake stores metadata such as
  * `MIN` and `MAX` of values stored in each column in the micropartition
  * Counts
  * `NULL` values, etc.


## Stages ##
A Stage is a cloud storage/repository location used for storing files before they are loaded into or unloaded from Snowflake. Stages can be three types
* Table stage
  * internal stage - managed by Snowflake
  * created automatically every time a table is created
  * named `@%[TABLE_NAME]`
  * does not support setting file formats
* User stage
  * internal stage - managed by Snowflake
  * created automatically every time a user is created
  * named `@~`
  * does not support setting file formats
* Named stage
  * Can be
    * once `[STAGE_NAME]` is created, it is referred to with the `@` symbol, e.g. `@[STAGE_NAME]`
    * internal stage - managed by Snowflake, or
    * external - managed by the customer, can be even in a different cloud provider or region
  * created manually
    * Creating an external stage requires providing
      * URL where the files are located
      * credentials to access the files
      * decryption keys to enable decryption of the data
  * can specify file format

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
