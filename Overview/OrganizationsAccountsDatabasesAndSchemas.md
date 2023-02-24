# Organizations, Accounts, Databases And Schemas #

## Organization ##
Top level securable object which serves as a logical grouping of Accounts.
* The Organization object is not available by default. It can be enabled on request by Snowflake Support.
* Once enabled, it makes available features which make use of multiple accounts such as database replication and failover.
* It can be used for monitoring usage and billing across accounts.
* The `ORGADMIN` role is added to the primary account in the Organization to allow management of the contained Account objects
* By default there is a limit of 25 Accounts in an Organization, can be increased by Snowflake Support

## Account ##
Logical grouping of Databases.
* Each account is hosted on a single cloud provider and in a single geographic region
* By default, Snowflake does not move data between regions unless requested
* The region where the account is provisioned affects:
  * the account and storage price
  * which regulatory certifications you can achieve
  * some Snowflake features which may be region-specific
* The account's name must be unique within an organization, regardless of which Snowflake region the account is in.
* The URL of an account (e.g. `xy12345.us-est-2.aws.snowflakecomputing.com`) consists of
  * the account identifier (sometimes referred to as the account name) `xy12345.us-est-2.aws` which can consists any mixture of the following:
    * the account locator `xy12345`
    * the cloud services region ID `us-est-2` and
    * the cloud provider `aws`
  * and the snowflake domain, `snowflakecomputing.com`
* It is possible to request a vanity address to convert the identifier into your company's name.
* An account is created with the system-defined role `ACCOUNTADMIN`
* When an account is created by an `ORGADMIN`, the account name (`acme-marketing-account`) will contain a unique organization name `acme` and the account name `marketing-account`

## Database ##
Logical container of your data, organized in Schemas.
* A Database can be created as a clone from another Database
* A Database can be created as a replica of another Database
* A Database can be created from a Share object provided by another Account
* Databases can be created as `Transient`
  * Time Travel: 0 or 1 days
  * No Fail-Safe support

## Schema ##
Logical grouping of Tables, Views, Stored Procedures, UDFs, Stages, File Formats, Pipes, Sequences, Shares, etc. Every schema belongs to a single Database. When a database is created, there are two default schemas created in it
* A Schema can be created as a clone from another Schema
* The Database name and Schema name together form the Namespace for all Schema objects
* `public`: default schema for any object created without specifying a schema
* `information_schema`: stores metadata information
* Schemas can be created as `Transient`.
  * Time Travel: 0 or 1 days
  * No Fail-Safe support

