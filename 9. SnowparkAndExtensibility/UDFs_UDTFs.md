[Back to README](../README.md) | Previous: [StoredProcedures.md](StoredProcedures.md) | Next: [BillingAndCost.md](../10. MonitoringAndUsage/BillingAndCost.md)

# UDFs and UDTFs

*Notes related to Snowpark and Extensibility: User-Defined Functions (UDFs) and User-Defined Table Functions (UDTFs).*

## Key Topics
*   **User-Defined Functions (UDFs):**
    *   **Purpose:** Extend SQL by encapsulating custom logic that can be called within queries.
    *   **Types:**
        *   **Scalar UDFs:** Return a single value per input row.
        *   **Supported Languages:** SQL, JavaScript, Java (via Snowpark), Python (via Snowpark).
    *   **Creation:** `CREATE FUNCTION ... RETURNS <datatype> LANGUAGE <language> AS ...`
    *   **Volatility:** `VOLATILE`, `IMMUTABLE`, `STABLE`.
    *   **Secure UDFs:** Restrict access to underlying data for UDFs shared via Secure Data Sharing.
*   **User-Defined Table Functions (UDTFs):**
    *   **Purpose:** Return a set of rows (a table) for each input row or for each partition.
    *   **Supported Languages:** JavaScript, Java (via Snowpark), Python (via Snowpark).
    *   **Creation:** `CREATE FUNCTION ... RETURNS TABLE(...) LANGUAGE <language> AS ...`
    *   **Usage:** Typically used with the `TABLE()` keyword or in a `LATERAL JOIN`.
*   **Stored Procedures:**
    *   While not strictly UDFs/UDTFs, they are related extensibility features.
    *   Support procedural logic, SQL execution, variable handling.
    *   Languages: SQL (Scripting), JavaScript, Java (Snowpark), Python (Snowpark), Scala (Snowpark).
*   **Performance Considerations:** Language choice, complexity of logic.


[Back to README](../README.md) | Previous: [StoredProcedures.md](StoredProcedures.md) | Next: [BillingAndCost.md](../10. MonitoringAndUsage/BillingAndCost.md)
