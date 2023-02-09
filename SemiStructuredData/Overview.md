# Semi-Structured Data Overview #

Snowflake supports the following semi-structured data formats:
* JSON
* Avro - originally developed for Apache Hadoop
* ORC (Optimized Row Columnar) - used for Hive data
* Parquet - binary format used in the Hadoop ecosystem
* XML (Extensible Markup Language)

These are first-level data types:
* ingested in the same way as structured data, with micropartitions, metadata, compression and encryption, to enable quicker query access and partition pruning
* Support for all SQL operations
* Native syntax for accessing data even in semi-structured fields

Semi-structured data types:
* `VARIANT` - holds standard SQL data types as well as arrays and objects
  * Objects - collection of key-value pairs where the values are of `VARIANT` type
  * Arrays - collection of values where each value is a `VARIANT`
  * non-native values (e.g. dates, timestamps) are stored as strings in `VARIANT` columns
  * operations can be slower than when stored as the corresponding data type
