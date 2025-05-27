[Back to README](../README.md) | Previous: [DDL_DML.md](DDL_DML.md) | Next: [Overview.md](Overview.md)

# Functions

*Notes related to SQL and Querying: Built-in and user-defined functions.*

## Key Topics
*   **Built-in Functions:**
    *   **Scalar Functions:** Operate on single values (e.g., string functions like `UPPER()`, `SUBSTRING()`; numeric functions like `ABS()`, `ROUND()`; date/time functions like `CURRENT_DATE()`, `DATEADD()`; conversion functions like `TO_VARCHAR()`, `TRY_CAST()`).
    *   **Aggregate Functions:** Operate on a set of values and return a single summary value (e.g., `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`, `LISTAGG()`).
    *   **Window Functions:** Operate on a set of rows (a "window") and return a single value for each row based on the group of rows (e.g., `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()`, `LAG()`, `LEAD()`, `SUM() OVER (PARTITION BY ...)`).
    *   **Table Functions:** Return a set of rows (e.g., `FLATTEN()` for semi-structured data, `SPLIT_TO_TABLE()`).
    *   **System Functions:** Provide information about the system or perform system-level operations (e.g., `CURRENT_USER()`, `CURRENT_ROLE()`, `GET_DDL()`).
*   **User-Defined Functions (UDFs):**
    *   **SQL UDFs:** Written in SQL, can be scalar or tabular.
    *   **JavaScript UDFs:** Scalar or tabular, allow more complex logic.
    *   **Java UDFs (via Snowpark):** Scalar or tabular, leverage Java ecosystem.
    *   **Python UDFs (via Snowpark):** Scalar or tabular, leverage Python ecosystem.
*   **User-Defined Table Functions (UDTFs):** Functions that return a set of rows, often used with JavaScript, Java, or Python.


[Back to README](../README.md) | Previous: [DDL_DML.md](DDL_DML.md) | Next: [Overview.md](Overview.md)
