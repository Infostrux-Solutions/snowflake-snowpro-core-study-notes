[Back to README](../README.md) | Previous: [ZeroCopyCloning.md](../2. Storage/ZeroCopyCloning.md) | Next: [ContinuousDataLoading.md](ContinuousDataLoading.md)

# Bulk Loading #

Bulk load is the process of loading batches of data from files available in a stage into Snowflake tables.

* You need to specify the table name where you want to copy the data, the stage where the files are, the file/patterns you want to copy, and the file format
* Bulk loading uses a transactional boundary control which wraps each `COPY INTO` command into an individual transaction that can be rolled back if errors are encountered
* The information about the loaded files is stored in Snowflake's metadata. You cannot COPY the same file again in the next 64 days unless you force it with the `FORCE = True` option
  * Renaming a previously ingested file in the stage does not modify the metadata so the file won't be re-ingested with the next `COPY INTO` command
* Bulk loading uses user-managed compute resources (Virtual Warehouses) which affect the processing time and cost of data loading.
* Some data transformations can be performed during data load, e.g. column reordering, column omission, type casting, etc.
  * some transformations like Flatten, Join, Group by, Filters or Aggregations are not supported.
* You cannot Load/Unload files from your Local Drive, they need to be staged (`PUT`) or downloaded (`GET`) first
* Using the Snowflake UI, you can only load files up to 50MB. You can copy bigger files using SnowSQL.
* Organizing input data by granular path can improve load performance

## Staging ##

### Staging from a Local Storage on a Client Machine ###
We can use the `PUT` command to UPLOAD files from a local directory/folder to an INTERNAL STAGE (named internal stage, user stage, or table stage):
```
PUT file:///tmp/data/mydata.csv @my_int_stage;
```
* `PUT` does NOT work with external stages.
* You cannot use the `PUT` command from the Snowflake Web UI, you will need to use SnowSQL
* Compression during a `PUT` operation uses the **local** machine's memory and `/tmp` directory disk space. 
* Uploaded files are automatically encrypted with 128-bit or 256-bit keys
* The `LIST` command can be used to list the files in the stage. 

### Staging from Cloud Storage ###
* When loading data from cloud storage it is generally recommended to create an external stage
* If no stage was created, you will need to provide the location, credentials and decryption keys for each `COPY INTO` command.

## COPY INTO Command ##
The `COPY INTO` command is used to load the data from staged files to an existing table. Snowflake will automatically load all files in the stage matching the query parameters which have not been previously loaded
* Metadata on which files have been loaded is kept around for about 64 days.
> BEST PRACTICE: Files should not be kept in a stage for longer than 64 days

When loading files, you can:
* name the files explicitly, e.g `FILES = ('<file_name>'[, '<file_name>'][, ...])`
* provide a pattern to match the files to be loaded: `PATTERN = '<regex_pattern>'`

Other options:
* `FILE_FORMAT` - must be specified unless a file format has already been attached to the stage or the table
* `VALIDATION_MODE` - "dry run" to validate the data without loading it
* `SIZE_LIMIT` - limit the amount of data being ingested
* `PURGE` - delete any files from the stage which were successfully loaded. Default is `FALSE`
  * If the purge operation fails for any reason, no error is returned
* `RETURN_FAILED_ONLY` - returns only the failed rows. Default is `FALSE`
* `ENFORCE_LENGTH` - will cause data that exceeds the column size defined in the table to be treated as errors. Default is `TRUE`
* `TRUNCATECOLUMNS` - will cause data that exceeds the column size defined in the table to be truncated to the column size and not treated as an error. Default is `FALSE`
* `FORCE` - reload previously loaded files. Default is `FALSE`. `TRUNCATE`-ing a table resets the metadata for previously loaded files so `FORCE` is not needed for a `TRUNCATE`-d table.
* `LOAD_UNCERTAIN_FILES` - load files older than 64 days where Snowflake metadata on whether they were loaded or not no longer exists. Default is `FALSE`
* `ON_ERROR` - specify how to handle errors. Default is `ABORT_STATEMENT`:
  * `CONTINUE` - skip error rows and continue processing file to the end
  * `SKIP_FILE` - files with errors are skipped
  * `SKIP_FILE_<n>` - files with a `<n>` number of errors are skipped
  * `SKIP_FILE_<n>%` - files with a `<n>%` percentage of errors are skipped
  * `ABORT_STATEMENT` - abort the `COPY INTO` execution on any error encountered. Rows loaded prior to the error are reverted

## Validating a Data Load ##
Data can be validated before loading with the `COPY INTO` option `VALIDATION_MODE` which can be set to:
* `RETURN_<n>_ROWS`
* `RETURN_ERRORS`
* `RETURN_ALL_ERRORS`

Validating data after a load can be done with the `VALIDATE` command which returns all errors encountered during a specific load job into a given table:
```sql
VALIDATE([namespace.]<table_name>,
  JOB_ID => { '<query_id>' | _last }
);
```


[Back to README](../README.md) | Previous: [ZeroCopyCloning.md](../2. Storage/ZeroCopyCloning.md) | Next: [ContinuousDataLoading.md](ContinuousDataLoading.md)
