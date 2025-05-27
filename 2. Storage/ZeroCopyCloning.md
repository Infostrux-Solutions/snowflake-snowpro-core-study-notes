[Back to README](../README.md) | Previous: [DataStorageLayer.md](DataStorageLayer.md) | Next: [BulkLoading.md](../3. DataMovement/BulkLoading.md)

# Zero-Copy Cloning

*Notes related to Storage and Data Protection: Understanding and using Zero-Copy Cloning.*

## Key Topics
*   **Concept:** Creating copies of databases, schemas, or tables without duplicating the underlying storage.
*   **Mechanism:** Clones reference the same micro-partitions as the source object at the time of cloning. Changes to the source or clone create new micro-partitions (copy-on-write).
*   **Speed and Efficiency:** Cloning is nearly instantaneous and incurs no additional storage costs initially.
*   **Use Cases:**
    *   Development and testing environments.
    *   Data backup and recovery (in conjunction with Time Travel).
    *   Creating sandboxes for data analysis or experimentation.
*   **Syntax:** `CREATE <object_type> <clone_name> CLONE <source_object_name> [AT | BEFORE (TIMESTAMP | OFFSET | STATEMENT => '<statement_id>')]`
*   **Impact on Time Travel:** Clones inherit the Time Travel history of the source object up to the point of cloning.


[Back to README](../README.md) | Previous: [DataStorageLayer.md](DataStorageLayer.md) | Next: [BulkLoading.md](../3. DataMovement/BulkLoading.md)
