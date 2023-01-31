# Authorization #

* Snowflake's authorization model is a combination of:
  * Role-Based
    * Privileges are granted to Roles
    * Roles are granted to users
  * Discretionary Access Control
    * all Snowflake objects are individually securable
    * each object has an owner who can grant others access to the object
* Privileges that can be set depend on the securable object. They can be very broad or very granular.
* Secure Views and UDFs (User Defined Functions)
  * Prevent data from being indirectly exposed via programmatic methods
  * Only authorized users can see the view or UDF definition
  * bypass some of the optimizations to achieve better security so they are not as efficient
* Row-level access - uses `CURRENT_ROLE()` or `CURRENT_USER()` to provide row-level security, e.g.
  ```iso92-sql
  SELECT ...
  FROM data_table
  JOIN auth_table
    ON auth_table.auth = data_table.auth
    AND auth_table.role = CURRENT_ROLE()
  ;
  ```

