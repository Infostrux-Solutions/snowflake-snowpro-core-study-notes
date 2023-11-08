# Snowflake Editions #
[Feature / Edition Matrix](https://docs.snowflake.com/en/user-guide/intro-editions#feature-edition-matrix)

The Snowflake Editions determine what features are available to the customer and what level of service they require. The Snowflake Edition affects the amount charged for compute and data storage. 

## Standard ##
Introductory level offering, providing full, unlimited access to all of Snowflake’s core features
* Complete SQL Data Warehouse
  * Includes standard DDL and DML features
  * Includes advanced DML statement such as multi-table inserts, merge and windowing functions  
* Secure data sharing across regions/clouds
* Premier Support 24 x 365
* Always-on enterprise grade encryption in transit and at rest
* Customer dedicated virtual warehouses
* Federated authentication
* Database replication
* External Functions 
* Snowsight analytics UI 
* Create your own Data Exchange 
* Data Marketplace access
* Fail-safe
* Continuous Data Protection
  * Time Travel
  * Network Policies

### SPECIFICS ###
* 1 day of time travel
* No Multi-Cluster warehouses
* No Materialized Views
* No column-level security
* No query statement encryption
* No Failover/Fallback
* No AWS PrivateLink support
* No Tri-Secret Secure encryption

## Enterprise ##
Designed specifically for the needs of large-scale enterprises and organizations
* All features of `Standard` plus:
* Multi-Cluster Warehouses
* Up to 90 days of time travel
* Materialized Views
* Column-level security
  * Dynamic Data Masking - uses masking policies to mask some columns for users with a lower role at query time
  * External Data Tokenization
    * tokenize sensitive data before loading it into Snowflake
    * you can also detokenize it using masking policies
    * useful for sensitive data like passwords, etc.
* Search Optimization Service 
* Annual rekey of all encrypted data

### SPECIFICS ###
* No query statement encryption
* No Failover/Fallback
* No Tri-Secret Secure encryption
* No AWS PrivateLink support

## Business Critical ##
Offers even higher levels of data protection to support the needs of organizations with extremely sensitive data
* All features of `Enterprise` plus:
* Higher level of data protection
  * Data encryption everywhere
  * Query statement encryption
  * Enhanced security policy
  * Database Failover and Fallback for business continuity (e.g. replication with failover and fallback accross regions)
  * AWS PrivateLink support
  * Tri-Secret Secure encryption using customer-managed keys (AWS)
* Enhanced security, see: [Snowflake’s Security & Compliance Reports](https://www.snowflake.com/snowflakes-security-compliance-reports/)

  * HIPPA (Health Insurance Portability and Accountability Act) support / HITRUST
  * PCI (PCI-DSS)
  * ISO/IEC 27001
  * FedRAMP Moderate
  * SOC 1 Type II
  * SOC 2 Type II
  * GxP
* External Functions - AWS API Gateway Private Endpoints support

## Virtual Private Snowflake (VPS) ##
Business Critical Edition but in a completely separate Snowflake environment, isolated from all other Snowflake accounts, to provide the highest level of security for governments and financial institutions
* All features of `Business Critical` plus:
* Dedicated Services Layer, not shared with other accounts
* Customer dedicated virtual servers wherever the encryption key is in memory
* Customer dedicated metadata store
* Additional operational visibility

## Government Regions ##
For government agencies that require compliance with US federal privacy and security standards, such as FIPS 140–2 and FedRAMP, Snowflake provides support for those only on Amazon Web Services and Azure. These government regions are only supported on Business-Critical Edition or higher.
