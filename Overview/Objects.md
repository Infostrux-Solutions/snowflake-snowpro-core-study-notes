# Objects #
All objecst in Snowflake are securable.

The definitions of most objects can be retrieved using the `GET_DDL()` function, see [GET_DDL()](https://docs.snowflake.com/en/sql-reference/functions/get_ddl.html).

## Organization ##
Top level securable object which serves as a logical grouping of Accounts.

## Account ##
Logical grouping of Databases.

## Databases ##
Logical grouping of Schemas.

## Schemas ##
Logical grouping of Tables, Views, Stored Procedures, UDFs, Stages, File Formats, Pipes, Sequences, Shares, etc.

## Tables ##

### Permanent ###
* Default table type, used for the highest level of data protection and recovery
* Persists until dropped
* Up to 90 days or Time Travel (on Snowflake Enterprise edition and higher)
* Fail-Safe support

### Transient ###
* Persists until dropped
* Available across sessions
* Time Travel: 0 or 1 days
* No Fail-Safe support

### Temporary ###
* Used for transitory data
* Tied to and available only within the context a single user session
* Time Travel: 0 or 1 days
* No Fail-Safe support

### External ###
* Snowflake table "over" data stored in an external data lake
* Data is accessed via an external stage
* Persists until removed
* Read-only
* No Time Travel
* No Fail-Safe support

### Notes ###
* Databases and schemas can be created as `Transient` as well.

## Views ##
Named definition of a SQL query which can be queried as if it were a table.

### Standard ###
* Default view type
* Executes as the role which owns it
* DDL available to any role with access to the view

### Secure ###
* Executes as the role which owns it
* DDL available only to authorized users
* Snowflake query optimizer bypasses optimizations used for regular views so secure views are less performant

### Materialized ###
* Results of underlying query are stored
  * Incurs storage costs
* Behaves more like a table
* Results are autorefreshed in the background
* Consumes background compute for the auto-refresh
  * The background compute does not require a customer-provided warehouse; Snowflake manages the compute
* Secure materialized views are supported

## Data Shares ##
See [Data Sharing](DataSharing.md)