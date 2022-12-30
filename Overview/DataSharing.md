# Data Sharing #
* Shares are named Snowflake objects that encapsulate all of the information required to share a database
* For each shared database, Snowflake supports using grants to provide granular access control to selected objects in the database:
  * Tables
  * External tables
  * Secure views
    * Preferred way to share data
    * allows sharing only select rows and columns rather than entire tables
    * allows providing different sets to different Consumers by filtering the data based on the values of the context functions `CURRENT_ACCOUNT()` and `CURRENT_ROLE()` which would return the Consumer account name and role, respectively.
  * Secure materialized views
  * Secure UDFs
* Objects shared between accounts are `READ-ONLY`
* Shares are secure, configurable, and controlled 100% by the provider account
* Data is shared live:
  * No data movement or copying
  * Consumers immediately see all updates
  * Data can be shared with an unlimited number of Consumers
  * Consumers can create new tables from a share
* Sharing accounts:
  * Providers - share data with others, no cost to share other than the storage of the shared data
  * Consumers
    * shared data does not take up any storage in the Consumer account
    * The only charges to consumers are for the compute resources (i.e. Virtual Warehouses) used to query the shared data
  * Reader Accounts
    * Consumers who are not Snowflake customers and do not have a Snowflake account
    * Providers setup and administer the Reader accounts within their own environment
      * A reader account can only consume data from the provider account that created it
      * Providers manage all aspects of the Reader Account - users, roles, permissions, warehouses, etc.
    * Readers use the compute from the data provider's account; the provider incurs that cost
    * Providers can track and manage the queries Readers can run and can monetize them by charging for the data share or the queries run
* Things to know
  * Shares can only be created by users
    * with the `ACCOUNTADMIN` role
    * or with a role that has been explicitly given the permission to create Shares 
  * Shares can be created between accounts but not within the same account
  * Consumers cannot re-share a Share
  * Shared data cannot be cloned in the typical Snowflake zero-copy clone fashion - consumers must copy the data if they want it to exist in their own account.
  * Snowflake does not charge for creating shares although Providers can charge Consumers or Reader Accounts to monetize their data
  * Sharing is available across all [Snowflake Editions](Editions.md)
  * (Is that still the case?) Currently you can only share with accounts in the same cloud and region.

## Types ##
* Public Data Marketplace
* Private Data Exchange

## References ##
* [Introduction to Secure Data Sharing](https://docs.snowflake.com/en/user-guide/data-sharing-intro.html)