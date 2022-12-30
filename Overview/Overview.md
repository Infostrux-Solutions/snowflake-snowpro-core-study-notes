# Overview #

## The Snowflake Platform ##
Snowflake is a data platform built for the cloud and delivered as a service.

## Architecture ##
* [Cloud Services Layer](CloudServicesLayer.md)
* Multi-Cluster Compute (Virtual Warehouses)
* Centralized Storage - single copy and source of truth for the data
* Cloud Agnosting Layer - allows Snowflake to run on the major cloud providers: AWS, Azure, GCP

## Features ##
* ANSI SQL compliant OLAP data warehouse
* Multi-cluser, shared data architecture
* Self-tuning and self-healing
* Pay only for what you use: storage and compute
* Compute (Virtual Warehouses) can be
  * `Scaled Up/Down` by resizing the warehouse on the fly to accommodate complex, heavy workloads
  * `Scaled Out` by using multi-cluster Warehouses allowing Snowflake to automatically spin up additional compute clusters to handle large concurrent query workloads
  * Automatically suspended and resumed to accomodate periods of inactivity
* Time Travel (see below for more info)
* Fail-Safe (see below for more info)
* Live data sharing
  * Private 1:1 and 1:many data sharing
  * Public data marketplaces
  * Secure private data exchanges
* Multi-cloud: AWS, Azure, GCP
* Zero-Copy Cloning
  * Only metadata is copied
  * Once an object is cloned, the individual copies evolve separately and their storage increases only by the amount of data that was modified in each copy.

### Time Travel ###
* Allows access previous versions of the data - the data in its state at a point of time in the past
* A minimum of Enterprise edition required for time travel longer than 1 day, up to 90 days
* The period of time travel can be set by database, schema or table

### Fail-Safe ###
* A data backup feature
* Snowflake admins can recover and restore data up to 7 days after the Time Travel period expires
* Accessible only by contacting Snowflake support administrators
* Only available for permanent tables
* Fail-Safe incurs additional storage costs for the extra 7 days of data retention
