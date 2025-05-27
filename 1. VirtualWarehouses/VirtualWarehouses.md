[Back to README](../README.md) | Previous: [ResourceMonitors.md](ResourceMonitors.md) | Next: [DataStorageLayer.md](../2. Storage/DataStorageLayer.md)

# Virtual Warehouses #

Virtual Warehouses (VWs) are the compute layer in Snowflake's architecture. It is a logical wrapper around a cluster of servers with CPU, memory and disk. Data Warehouses are used to perform queries and DML operations (like loading data into tables).
* The actual compute underlying the VW is fully managed by Snowflake
* While running, even if idle, a VW consumes Snowflake credits - you are charged for compute
* VWs can be Standard or Multi-Cluster Warehouses (MCW). Standard Warehouses have only a single compute cluster and cannot scale out

## SCALE OUT/IN: Multi-Cluster Warehouses (MCW) ## 
MCWs can automatically `SCALE OUT/IN` by spawning (or shutting down) additional compute clusters
* used for handling spikes in concurrent compute requests
* MCWs are a feature of Snowflake Enterprise Edition and higher
* MCWs can set to scale out to a maximum of 10 clusters
* The number of credits billed is calculated based on the size and the number of warehouses that run within the time period
* MCWs scale out under two Scaling Policies - Standard and Economy
  * Standard policy: starts additional clusters if a query is queueing or expected to queue
  * Economy policy: will start an additional cluster only after at least 6 minutes of workload have been queued up for the future cluster
* Incoming queries are load-balanced across the available running clusters

## SCALE UP/DOWN: Resizing Warehouses ##
A Virtual Warehouse can `SCALE UP/DOWN` (be resized), manually, at any time, even while running
  * used for handling complex, long-running queries or ingesting large data sets
  * when resized while running, currently executing queries will complete at the current size; queued and new queries will execute at the new size
  * Efficient scale up/down should give approximately linearly proportionate results, e.g. running a query on a double-sized warehouse should cut the query run time in half.
  * It is recommended to keep queries and workloads of similar complexity and with similar compute demands on the same warehouse to simplify compute resource size management
  * Resizing can be included in SQL scripts so a warehouse can be scaled up/down depending on the demands of subsequent queries

## Creating Warehouses ##
* One can create an unlimited number of warehouses in their account.
* XS (Extra Small) is the smallest size of VW with one server per cluster.
  * each size up doubles the number of servers in the cluster as well as the number of Snowflake credits consumed
  * sizes range from XS, through S, M, L, XL, 2XL up to 6XL (currently)
    * the default size for warehouses created through the web interface is XL
    * the default size for warehouses created using SQL is XS
    * 5XL and 6XL warehouses are generally available in AWS regions, and in preview in US Government and Azure regions.
* A VW can be set to auto-suspend when idle for a configurable number of minutes.
  * By default, the auto-suspend option is enabled.
  * Through the web UI auto-suspend can be set as low as 5 minutes
  * Through SQL auto-suspend can be set to the minimum auto-suspend setting of 1 minute (60 seconds)
  * VWs can also be started or suspended manually
* A VW can also be set to auto-resume when a new query is submitted
  * Auto-resume is enabled by default 
  * A VW will automatically start when first created
  * In SQL a VW can be created in suspended mode by setting the `INITIALLY_SUSPENDED = TRUE` option
* When a VW is first created, it has, by default, the USAGE permission granted to the role that owns/creates it since ownership defaults to the object creator
 
## Compute Credits ##
> For more info, see [Understanding Compute Cost](https://docs.snowflake.com/en/user-guide/cost-understanding-compute)
* Customer-managed compute is charged per second with a 60-second minimum each time the warehouse starts
* Snowflake-created serverless (background) compute is charged per second with no minimum.
* Credit cost varies depending on cloud provider and region
* One server in the VW cluster uses one credit per hour, so, for example, an XS (1 server) will use one credit per hour while a large (8 servers) will use 8 credist per hour

### Cloud Services Compute Billing ###
* Customers are charged for cloud computing (e.g. in the Cloud Services Layer) that exceeds 10% of the total compute costs for the account.
* Use the `WAREHOUSE_METERING_HISTORY` view to see how much cloud compute your account is using

## Transactions ##
A transaction is a sequence of SQL statements that are committed or rolled back as a unit. All statements in the transaction are either applied (i.e., committed) or undone (i.e., rolled back) together. For this reason, transactions are ACID (Atomicity, Consistency, Isolation & Durability) compliant.

* If a session is disconnected for whatever reason and a transaction remains in a detached state which cannot be committed or rolled back, Snowflake takes 4 hours to abort a transaction and roll it back.
* You can abort a running transaction with the system function `SYSTEM$ABORT_TRANSACTION `
* Each transaction has independent scope
* Snowflake does not support nested Transactions, although it supports nested Stored Procedure calls


[Back to README](../README.md) | Previous: [ResourceMonitors.md](ResourceMonitors.md) | Next: [DataStorageLayer.md](../2. Storage/DataStorageLayer.md)
