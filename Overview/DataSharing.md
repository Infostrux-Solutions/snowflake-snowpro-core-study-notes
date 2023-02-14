# Data Sharing #

> [Introduction to Secure Data Sharing](https://docs.snowflake.com/en/user-guide/data-sharing-intro.html)

Secure Data Sharing lets you share selected objects in a database in your (Provider) account with other (Consumer) Snowflake accounts. You can share the following Snowflake database objects:
* Tables 
* External tables 
* Secure views 
* Secure materialized views 
* Secure UDFs

## Shares ##

Shares are named Snowflake objects that encapsulate all of the information required to share a database
* The privileges that grant access to the database, schemas and specific objects we want to share
* The consumer accounts with which the database and its objects are shared.

Some sample SQL:
```postgres-psql
-- Create a Share and give SELECT privileges to table
CREATE SHARE myShare;
GRANT USAGE ON DATABASE myDb TO SHARE myShare;
GRANT USAGE ON SCHEMA myDb.public TO SHARE myShare;
GRANT SELECT ON TABLE myDb.public.myTable TO SHARE myShare;

-- Show all Shares in the account
SHOW SHARES;

-- See all the privileges a Share has
SHOW GRANTS TO SHARE myShare;

-- See the accounts (consumers) that have access to the Share
SHOW GRANTS OF SHARE myShare;
```

### Provider ###
* Shares data with others
* No cost to share other than the storage of the shared data
* Has full control over the data shared and the privileges they give to the share
* Can revoke privileges granted to the share at any time 
* Pays for the storage of the data they share

### Consumer ###
Accounts that receive the share/data.
* Shared data does not take up any storage in the Consumer account so Consumers don’t pay for its storage
* Time Travel is not available to Consumers on shared data
* Zero-Copy Cloning is not available to Consumers on shared data

#### Full Account Consumer ####
* The only charges to consumers are for the compute resources (i.e. Virtual Warehouses) used to query the shared data

#### Reader Account Consumer ####
* Consumers who are not Snowflake customers and do not have a Snowflake account
* The Reader account is set up within the Provider's environment
  * Providers manage all aspects of the Reader Account - users, roles, permissions, warehouses, etc.
  * A reader account can only consume data from the provider account that created it
* Readers must use Warehouses from the Provider's account; the Provider incurs the compute cost
* Providers can track and manage the queries Readers can run and can monetize them by charging for the data share or the queries run

### Sharing Features ###
* All database objects shared between accounts are `READ-ONLY`,(i.e. the objects cannot be modified or deleted, including adding or modifying table data
* Data is shared live:
  * No data movement or copying
  * Consumers immediately see all updates
  * Data can be shared with an unlimited number of Consumers
  * Consumers can create new tables from a share
* Shares can only be created by users
  * with the `ACCOUNTADMIN` role
  * or with a role that has been explicitly given the permission to create Shares
* Shares can be created between accounts but not within the same account
* Consumers cannot re-share a Share
* Shared data cannot be cloned in the typical Snowflake zero-copy clone fashion - consumers must copy the data if they want it to exist in their own account.
* Snowflake does not charge for creating shares although Providers can charge Consumers or Reader Accounts to monetize their data
* Sharing is available across all [Snowflake Editions](Editions.md)
* The Consumer and Provider accounts must be in the same cloud and region to share data
  * A Provider can replicate their data to an account in another cloud and region if they want to share it with a Consumer in the other cloud/region.

### Sharing with Secure Views ###
The preferred way to share data is by using Secure Views:
* allows sharing only select rows and columns rather than entire tables
* allows providing different sets to different Consumers by filtering the data based on the values of the context functions `CURRENT_ACCOUNT()` and `CURRENT_ROLE()` which would return the Consumer account name and role, respectively.

## Types ##
* Public Data Marketplace
* Private Data Exchange
