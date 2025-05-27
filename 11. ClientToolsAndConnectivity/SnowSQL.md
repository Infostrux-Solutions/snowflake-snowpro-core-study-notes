[Back to README](../README.md) | Previous: [Overview.md](Overview.md) | Next: [Snowsight.md](Snowsight.md)

# SnowSQL

*Notes related to Client Tools and Connectivity: Using the SnowSQL command-line client.*

## Key Topics
*   **Installation:** Downloading and installing SnowSQL for various operating systems.
*   **Configuration:**
    *   Connection parameters via command-line options.
    *   Using the `~/.snowsql/config` file for named connections and default settings.
*   **Basic Usage:**
    *   Connecting to Snowflake.
    *   Executing SQL queries, DDL, and DML statements.
    *   Exiting SnowSQL (`!quit` or `!exit`).
*   **Key Commands:**
    *   `!source <filepath>`: Executing SQL scripts from a file.
    *   `!define <var>=<value>`: Setting variables.
    *   `!variables`: Listing defined variables.
    *   `!set output_format=<format>`: Changing output format (e.g., `psql`, `csv`, `tsv`, `json`).
    *   `PUT`: Uploading local files to internal stages.
    *   `GET`: Downloading files from internal stages to local.
*   **Scripting:** Using SnowSQL for automated tasks.
