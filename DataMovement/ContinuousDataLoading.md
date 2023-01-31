# Continuous Loading #

Continuous data loading is used for modern data sources. It uses a Snowpipe object to ingest files as they appear in the stage rather than one file (or group of files) per `COPY INTO` statement. No scheduling is required and the user does not need to manage (start, suspend, manage size, etc.) any Virtual Warehouses. Continuous Loading uses cloud (serverless) compute.

Typically, there would be a source application which would load files into the stage. Ingestion then can happen in one of two ways:
* A call can be made to the Snowflake REST API to trigger the `ALTER PIPE <pipe_name> REFRESH` command to check the stage for new files to be loaded.
  * It can be used with internal or external stages
  * Alternatively, you can setup a task which would run the `ALTER PIPE <pipe_name> REFRESH` command on a schedule.
* You can use the Snowpipe `AUTO_INGEST` method, together with notifications setup on your cloud provider so the pipe is automatically notified when a file lands in the stage
  * The `AUTO_INGEST` method only works with external stages
  * Auto-Ingest is only available on AWS external stages by using S3 event messages

Once Snowpipe receives a trigger for the ingestion, whether via the REST API or a notification from the cloud provider, files are moved from the stage into an Ingestion Queue and then into the Pipe which contains the `COPY INTO` command with the source stage and the target table.
* the Snowpipe can be paused, resumed and its return status can be retrieved.

## Billing ##
Customers are billed for the cloud compute used by Snowpipe per-second, per-core on actual compute usage.

In addition to the cloud compute costs, there is an utilization cost charge of 0.06 credits per 1000 files notified by using the REST API or `AUTO_INGEST`
