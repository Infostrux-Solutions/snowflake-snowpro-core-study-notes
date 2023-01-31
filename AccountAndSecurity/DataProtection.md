# Data Protection #

* AES 256 bit encryption at rest and in motion
* Hierarchical encryption key model
  * Root key
  * Account master Key - each account has its own key
  * Object Master Keys - each object has its own key
  * File Keys - each micro-partition file has its own key
* Encryption keys are
  * active: used for encryption and decryption
  * retired: used for decryption of data previously encrypted with that key
  * destroyed: no longer used
* Encryption key rotation and expiration with no customer impact
  * keys are automatically rotated every 30 days
  * Optional annual re-keying of data for Snowflake Enterprise edition or higher
* TLS 1.2 encryption for all client communications
* Data is replicated across 3 availability zones in the cloud provider region
* Data Protection/Recovery features:
  * Time Travel
  * Failsafe
  * Database Replication
