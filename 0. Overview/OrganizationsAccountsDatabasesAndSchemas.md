[Back to README](../README.md) | Previous: [ObjectModel.md](ObjectModel.md) | Next: [Pricing.md](Pricing.md)

# Organizations, Accounts, Databases And Schemas #

## Organization ##
* The top-level entity in the Snowflake hierarchy.
* Represents a customer's entire Snowflake presence.
* Can contain multiple Snowflake accounts.
* Managed by the `ORGADMIN` role.

## Account ##
* A distinct Snowflake instance within an organization.
* Contains databases, schemas, warehouses, users, roles, etc.
* Each account has its own independent storage and compute resources.
* Managed by the `ACCOUNTADMIN` role.

## Database ##
* A container for schemas and other database objects.
* Can be standard or shared (from a data share).

## Schema ##
* A container for database objects such as tables, views, stages, etc.
* Belongs to a database.
* Provides a logical grouping for objects.


[Back to README](../README.md) | Previous: [ObjectModel.md](ObjectModel.md) | Next: [Pricing.md](Pricing.md)
