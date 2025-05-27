[Back to README](../README.md) | Previous: [VirtualWarehouseScaling.md](../5. PerformanceAndTuning/VirtualWarehouseScaling.md) | Next: [Overview.md](Overview.md)

# Load and Unload Semi-Structured Data #

## Create File Format ##
> [CREATE FILE FORMAT](https://docs.snowflake.com/en/sql-reference/sql/create-file-format)
```
CREATE FILE FORMAT <file_format_name>
TYPE = { JSON | AVRO | ORC | PARQUET | XML }
[<format_options>];
```

## JSON Data ##

### Some JSON Format Options ###
* `COMPRESSION`: Specifies compression algorithm
  * Supported: `GZIP`, `BZ2`, `BROTLI`, `ZSTD`, `DEFLATE`, `RAW_DEFLATE`, `NONE`
    * the `BROTLI` algorithm is not supported in `AUTO` mode
  * Default for loading: `AUTO`
  * Default for unloading: `GZIP`
* `FILE_EXTENSION`: Specifies file extension to use
  * Default: `.JSON` 
  * Only used for unloading
* `ALLOW_DUPLICATE`: Allows duplicate object field names
  * Default: `FALSE`
  * Only the last field value will be preserved
  * Only used for loading
* `STRIP_OUTER_ARRAY`: If `TRUE`, JSON parser will strip outer array brackets `[]` so the file is not treated as a single JSON entry
  * Default: `FALSE`
  * Only used for loading
* `STRIP_NULL_VALUES`: If `TRUE`, JSON parser will remove object fields or array elements with `NULL` values
  * Default: `FALSE`
  * Only used for loading
* `DATE_FORMAT`: Defines the date format in strings
  * Default: `AUTO`
  * Used only for loading JSON data into separate columns
* `TIME_FORMAT`: Defines the time format in strings
  * Default: `AUTO`
  * Used only for loading JSON data into separate columns

### Load Options for JSON Data ###
Load the file with no parsing or transformations into a `VARIANT` column:
```
COPY INTO table_name
FROM <file(s) in stage>
FILE_FORMAT = (FORMAT_NAME = <JSON format with options>);
```
Transform the file into columns and load into a table with pre-defined columns:
```
COPY INTO table_name
FROM (
    SELECT <keys>
    FROM <file(s) in stage>
)
FILE_FORMAT = (FORMAT_NAME = <JSON format with options>);
```

## Parquet Data ##

### Some Parquet Format Options ###
* `COMPRESSION`: Specifies compression algorithm
  * Supported: `LZO`, `SNAPPY`, `NONE`
  * Default for loading: `AUTO`
  * Default for unloading: `GZIP`
* `SNAPPY_COMPRESSION`:
  * Default: `TRUE`
  * Only used for unloading
* `BINARY_AS_TEXT`: Whether to interpret columns with no defined logical data type as `UTF-8` text. When set to `FALSE`, Snowflake interprets these columns as binary data.
  * Default: `TRUE`
  * Only used for loading
* `TRIM_SPACE`: Whether to remove leading and trailing white space from strings
  * Default: `FALSE`
  * Only used for loading Parquet data into separate columns
* `NULL_IF`: Replace matching strings with a SQL `NULL` value
  * Default: `\\N`
  * Only used for loading Parquet data into separate columns

### Load Options for Parquet Data ###
Load the file with no parsing or transformations into a `VARIANT` column:
```
COPY INTO table_name
FROM <file(s) in stage>
FILE_FORMAT = (FORMAT_NAME = <parquet format with options>);
```
Transform the file into columns and load into a table with pre-defined columns:
```
COPY INTO table_name
FROM (
    SELECT
      $1:<column_name>::<data_type>,
      $1:<column_name>::<data_type>,
      ...
    FROM <file(s) in stage>
)
FILE_FORMAT = (FORMAT_NAME = <parquet format with options>);
```

## Loading MATCH_BY_COLUMN_NAME Option ##
* Load semi-structured data directly into columns of a table the names of which match the names of the high-level keys present in the data
* Supported for JSON, AVRO, ORC and Parquet file formats
```
COPY INTO table_name
FROM <file(s) in stage>
FILE_FORMAT = (FORMAT_NAME = <file format>)
MATCH_BY_COLUMN_NAME = CASE_INSENSITIVE;
```

## Unloading Data ##
* Supported formats
  * JSON: Unload from a `VARIANT` column or reconstruct a JSON format
  * Parquet: Use a `SELECT` to unload the table columns into a Parquet file


[Back to README](../README.md) | Previous: [VirtualWarehouseScaling.md](../5. PerformanceAndTuning/VirtualWarehouseScaling.md) | Next: [Overview.md](Overview.md)
