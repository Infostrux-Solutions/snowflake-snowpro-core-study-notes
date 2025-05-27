[Back to README](../README.md) | Previous: [Snowpark.md](Snowpark.md) | Next: [UDFs_UDTFs.md](UDFs_UDTFs.md)

# Stored Procedures

*Notes related to Snowpark and Extensibility: Creating and using Stored Procedures.*

## Key Topics
*   **Purpose:** Encapsulate complex logic, procedural control flow, and multiple SQL statements into a single callable unit.
*   **Supported Languages:**
    *   SQL (Snowflake Scripting)
    *   JavaScript
    *   Java (via Snowpark)
    *   Python (via Snowpark)
    *   Scala (via Snowpark)
*   **Creation:** `CREATE PROCEDURE <proc_name> (...) RETURNS <datatype> LANGUAGE <language> AS ...`
*   **Execution:** `CALL <proc_name>(...)`
*   **Features:** Variables, control structures (IF/ELSE, loops), error handling, dynamic SQL execution.
*   **Caller's Rights vs. Owner's Rights:** Understanding execution context and privileges.
*   **Use Cases:** Automating administrative tasks, complex data transformations, implementing business logic.
