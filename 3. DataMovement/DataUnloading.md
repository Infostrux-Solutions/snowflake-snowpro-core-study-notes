[Back to README](../README.md) | Previous: [ContinuousDataProcessing.md](ContinuousDataProcessing.md) | Next: [Overview.md](Overview.md)

# Data Unloading #

Similar to [Bulk Loading](BulkLoading.md), unloading uses the `COPY INTO` command to unload data to an internal or external stage. The difference is that, when unloading, we would
```sql
COPY INTO <stage> FROM <table>;
```

## Unloading to Local Storage on a Client Machine ##
If data has been unloaded to a Snowflake INTERNAL STAGE (named internal stage, user stage, or table stage), you can use the `GET` command to DOWNLOAD the files to a local directory/folder on a client machine:
```
GET @my_int_stage file:///tmp/data/;
```
* You cannot use the `GET` command from the Snowflake Web UI, you will need to use SnowSQL

### Staging from Cloud Storage ###
* It is recommended to use an external named stage for data unloading
* Files can also be unloaded directly to cloud storage by specifying the URL and any necessary credentials

## Considerations ##
* Supported file formats
  * Flat (CSV, TSV, etc.) for structured data
  * JSON - semi-structured data
  * Parquet - semi-structured data
* When unloading unnested semi-structured data, you will need to use the `OBJECT_CONSTRUCT` function to recreate the JSON/Parquet data.
* When unloading, files are split
  * Each server in the Data Warehouse cluster can process 8 files in parallel, so the larger the Data Warehouse, the more (smaller) files will be generated. Choosing a smaller Warehouse will result in fewer, larger files.
  * You can specifiy the `SINGLE` option for the `COPY INTO` command to prevent files from being split but that results in a significant performance degradation as you'd be using one Data Warehouse thread instead of 8.
  * Default average file size is around 16MB, compressed. `MAX_FILE_SIZE` can be specified to change that but there are some cloud-specific limitations
    * Azure max filesize is 256MB
    * The max filesize for GCP and Amazon is 5GB
* You can use the `LIST` and `REMOVE` commands to manage files in stages.
* `SELECT` queries in the `COPY INTO` statement support the full SQL syntax which allows complex transformations on data egress, e.g. `JOIN`-ing data from multiple tables, perform aggregations, ordering and filtering, etc.

## Empty Strings vs. Null Values Options ##
* `FIELD_OPTIONALLY_ENCLOSED_BY` - specify the character to use to enclose your fields
* `EMPTY_FIELD_AS_NULL` - convert empty fields into `NULL`, the default is `FALSE`
* `NULL_IF` - convert `NULL` values to something else


[Back to README](../README.md) | Previous: [ContinuousDataProcessing.md](ContinuousDataProcessing.md) | Next: [Overview.md](Overview.md)
