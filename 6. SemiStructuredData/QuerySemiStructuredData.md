[Back to README](../README.md) | Previous: [Overview.md](Overview.md) | Next: [DDL_DML.md](../7. SQLAndQuerying/DDL_DML.md)

# Query Semi-Structured Data #

```
-- Sample "weather" VARIANT column data
{ "humidity": 45.6, "cloud_cover": { "density": 25.0, "description": "scattered clouds" }}
```
* To access a value in a `VARIANT` column under a given key, you can use:
  * colon (`:`) notation:
  `SELECT weather:humidity`
  * square brackets (`[]`) notation: `SELECT weather['humidity']`
* To access values of nested objects, you can chain the keys names of each nested object with dot (`.`) to reach the value: `SELECT weather:cloud_cover.density`
* `VARIANT` data can be cast to SQL data types using the double colon `::` syntax:
```
SELECT
    weather:humidity::NUMBER(10, 2) AS humidity_percent,
    weather:cloud_cover.description::VARCHAR as cloud_description
```

## Semi-structured Data Functions ##
> [Semi-structured Data Functions](https://docs.snowflake.com/en/sql-reference/functions-semistructured.html)

* `ARRAY_AGG`: array creation and manipulation
* `OBJECT_AGG`: object creation and manipulation
* `PARSE_JSON`: JSON and XML parsing
* `TO_ARRAY`: conversion to array
* [FLATTEN](https://docs.snowflake.com/en/sql-reference/functions/flatten.html): a table function that takes a VARIANT, OBJECT, or ARRAY column and explodes compound values into multiple rows. Often used in [Lateral Joins](https://docs.snowflake.com/en/sql-reference/constructs/join-lateral.html#example-of-using-lateral-with-flatten). Returns a table with a defined set of columns:
  * `SEQ`: unique sequence number associated with the input record. Not guaranteed to be continuous or ordered
  * `KEY`: for maps or objects, the key of the exploded value; `NULL` for arrays
  * `PATH`: path to the data structure element that is being flattened
  * `INDEX`: with arrays, index of the element; `NULL` otherwise
  * `VALUE`: value of the flattened element
  * `THIS`: the element being flattened; useful for recursive flattening with `RECURSIVE => TRUE`
* `IS_<object_type>`: type checking
* `AS_<object_type>`: type casting
