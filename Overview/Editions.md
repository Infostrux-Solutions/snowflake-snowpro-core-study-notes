# Snowflake Editions #

## Standard ##
Introductory level offering, providing full, unlimited access to all of Snowflake’s standard features
* Complete SQL Data Warehouse
* Secure data sharing across regions/clouds
* Business hours support, M-F
* Always-on enterprise grade encryption in transit and at rest
* Customer dedicated virtual warehouses
* Federated authentication
* Database replication
* Fail-safe

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
* Multi-Cluster warehouses
* Up to 90 days of time travel
* Materialized Views
* Column-level security
* Annual rekey of all encrypted data

### SPECIFICS ###
* No query statement encryption
* No Failover/Fallback
* No Tri-Secret Secure encryption
* No AWS PrivateLink support

## Business Critical ##
Offers even higher levels of data protection to support the needs of organizations with extremely sensitive data
* All features of `Enterprise` plus:
* HIPPA (Health Insurance Portability and Accountability Act) support
* PCI compliance
* Data encryption everywhere
* Query statement encryption
* Enhanced security policy
* Database Failover and Fallback for business continuity (e.g. replication with failover and fallback accross regions)
* AWS PrivateLink support
* Tri-Secret Secure encryption using customer-managed keys (AWS)

## Virtual Private Snowflake (VPS) ##
Business Critical Edition but in a completely different Snowflake environment, isolated from all other Snowflake accounts
* All features of `Business Critical` plus:
* Customer dedicated virtual servers wherever the encryption key is in memory
* Customer dedicated metadata store
* Additional operational visibility

## Government Regions ##
For government agencies that require compliance with US federal privacy and security standards, such as FIPS 140–2 and FedRAMP, Snowflake provides support for those only on Amazon Web Services and Azure. These government regions are only supported on Business-Critical Edition or higher.