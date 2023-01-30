# Bulk Loading #

Bulk loading is used for migrating data from traditional data sources. Bulk loading uses a transactional boundary control which wraps each `COPY INTO` command into an individual transaction that can be rolled back if errors are encountered. Bulk loading uses user-managed compute resources (Virtual Warehouses) which affect the processing time and cost of data loading.

With bulk loading you can ingest files from your local filesystem or from the cloud. Both require either the creation of a named stage or using a table or user stage.

The `PUT` command is used to copy files from a local filesystem into a stage.
> Compression during a `PUT` operation uses the **local** machine's memory and `/tmp` directory disk space.

The `LIST` command can be used to list the files in the stage.

When loading data from cloud storage it is generally recommended to create an external stage. If no stage is created, you will need to provide the location, credentials and decryption keys for each `COPY INTO` command.

## COPY INTO Command ##
The `COPY INTO` command is used to load the data from the stage into the table. Snowflake will automatically load all files in the stage which have not been previously loaded. Metadata on which files have been loaded is kept around for about 64 days.
> BEST PRACTICE: Files should not be kept in a stage for longer than 64 days

If you want to load files regardless whether they were loaded before, you can use:
* `FILES = ('<file_name>'[, '<file_name>'][, ...])` - comma-separated list of files to load
* `PATTERN = '<regex_pattern>'` - match the files to be loaded

Other options:
* `FILE_FORMAT` - must be specified unless a file format has already been attached to the stage or the table
* `VALIDATION_MODE` - "dry run" to validate the data without loading it
* `SIZE_LIMIT` - limit the amount of data being ingested
* `PURGE` - delete any files from the stage which were successfully loaded. Default is `FALSE`
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
  * `ABORT_STATEMENT` - abort the `COPY INTO` execution on any error encountered. Rows loaded prior to the error is reverted.

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