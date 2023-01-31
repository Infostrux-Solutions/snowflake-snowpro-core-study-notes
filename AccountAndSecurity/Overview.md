# Account and Security Overview #

Snowflake's Security model is a combination of:
* Discretionary access control - object based; all Snowflake objects are individually securable
* Role-based access control
  * Privileges are granted to Roles
  * Roles are granted to users

## Security Aspects ##
* Access: network policies
* Authentication: Password, MFA or SSO
* Authorization: Discretionary access control - Role-based access control
  * Privileges are granted to Roles
  * Roles are granted to users
* Data Protection
  * AES 256 bit encryption and periodic re-keying
  * TLS 1.2 encryption for all client communications
* Infrastructure: handled by cloud providers

## Snowflake Operational Controls ##
* NIST 800-53
* SOC2 Type 2
* SOC1 Type II
* ISO/IEC 27001:2013
* HIPAA (Snowflake Business Critical Edition)
* PCI (Snowflake Business Critical Edition)
* FedRAMP (Snowflake Business Critical Edition)
