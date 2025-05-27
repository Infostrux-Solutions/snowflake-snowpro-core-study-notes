[Back to README](../README.md) | Previous: [BulkLoading.md](BulkLoading.md) | Next: [ContinuousDataProcessing.md](ContinuousDataProcessing.md)

# Continuous Loading #

There are different ways to ingest data continuously into Snowflake:
* Snowpipe: the easiest and most popular way
* Snowflake Connector for Kafka: Reads data from Apache Kafka topics and loads the data into a Snowflake table
* Third-Party Data Integration Tools: You can do it with other [supported integration tools](https://docs.snowflake.com/en/user-guide/ecosystem-etl.html)

## Snowpipe ##
Enables streaming/pipeline/micro-batch/near-real-time loading of frequent, small volumes of data into Snowflake.
* Specifies the `COPY INTO` command that is used to load the data
* It can be used with internal or external stages
* Can be used with structured and semi-structured data
* No scheduling is required
* Snowpipe is serverless; it doesn't use Virtual Warehouses
* It is used for small volumes of frequent data which it loads continuously (micro-batches)
* Snowpipe does not guarantee that files will be loaded in the same order that they were staged
* Snowpipe retains 14 days of metadata vs. bulk loading which retains metadata for 64 days. You cannot copy the same files with Snowpipe again during these 14 days
  * Renaming a previously ingested file in the stage does not modify the metadata so the file won't be re-ingested at the next SnowPipe run
* The default behaviour when there is an error loading files is `SKIP_FILE` rather than bulk copy's `ABORT_STATEMENT`
* A Snowpipe can be paused, resumed and its return status can be retrieved.

Snowpipe can be notified of new files in the stage in one of two ways:
* A call can be made to the [Snowflake REST API](https://docs.snowflake.com/en/user-guide/data-load-snowpipe-rest-apis.html) to trigger the `ALTER PIPE <pipe_name> REFRESH` command to check the stage for new files to be loaded.
  * It requires key pair authentication with a JSON Web Token (JWT)
  * APIs endpoints available:
    * Data File Ingestion: `insertFiles`
    * Load History Reports: `insertReport` and `loadHistoryScan`
* You can setup a task which would run the `ALTER PIPE <pipe_name> REFRESH` command on a schedule

Alternatively, you can use the Snowpipe `AUTO_INGEST` method, together with notifications setup on your cloud provider so the pipe is automatically notified when a file lands in the stage
  * `AUTO_INGEST` is only available on AWS external stages by using S3 event messages dispatched by Amazon's SQS (Simple Queue Service)
  * For more information, see [Automating Snowpipe for Amazon S3](https://docs.snowflake.com/en/user-guide/data-load-snowpipe-auto-s3.html)

Once Snowpipe receives a trigger for the ingestion, whether via the REST API or a notification from the cloud provider, files are moved from the stage into an Ingestion Queue and then into the Pipe which contains the `COPY INTO` command with the source stage and the target table.

## Billing ##
Customers are billed for the cloud compute used by Snowpipe per-second, per-core on actual compute usage.

In addition to the cloud compute costs, there is an utilization cost charge of 0.06 credits per 1000 files notified by using the REST API or `AUTO_INGEST`


[Back to README](../README.md) | Previous: [BulkLoading.md](BulkLoading.md) | Next: [ContinuousDataProcessing.md](ContinuousDataProcessing.md)
