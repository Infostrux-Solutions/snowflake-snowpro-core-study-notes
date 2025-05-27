[Back to README](../README.md) | Previous: [LoadAndUnloadSemiStructuredData.md](LoadAndUnloadSemiStructuredData.md) | Next: [QuerySemiStructuredData.md](QuerySemiStructuredData.md)

# Semi-Structured Data Overview #

Snowflake supports the following semi-structured data file formats:
* JSON
* Avro - originally developed for Apache Hadoop
* ORC (Optimized Row Columnar) - used for Hive data
* Parquet - binary format used in the Hadoop ecosystem
* XML (Extensible Markup Language)

Semi-structured data is a first-class citizen in Snowflake:
* ingested in the same way as structured data, with micropartitions, metadata, compression and encryption, to enable quicker query access and partition pruning
* all SQL operations are supported with native syntax for accessing data even in semi-structured fields

Semi-structured data is supported using the `VARIANT` data type:
* holds standard SQL data types as well as arrays and objects
* Objects - collection of key-value pairs where the values are of `VARIANT` type
* Arrays - collection of values where each value is a `VARIANT`
* non-native values (e.g. dates, timestamps) are stored as strings in `VARIANT` columns
* operations can be slower than when stored as the corresponding data type


[Back to README](../README.md) | Previous: [LoadAndUnloadSemiStructuredData.md](LoadAndUnloadSemiStructuredData.md) | Next: [QuerySemiStructuredData.md](QuerySemiStructuredData.md)
