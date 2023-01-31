# Authentication #

Identifies the user and confirms whether they are allowed to login.

## Authentication Methods ##
* Username and password policy (Snowflake-controlled, cannot be changed)
  * Password can be 8-256 characters long and must contain
    * at least one uppercase letter
    * at least one lowercase letter
    * at least one number 
* MFA: Multi-Factor Authentication with the Duo app
* SSO/Federated Authentication (SAML 2.0), e.g. Okta
* Other
  * Oauth: authentication from a 3rd party service or application
  * Key Pair: JSON Web Token (JWT) signed with a private/public RSA key pair
  * SCIM (System Cross-domain Identity Management): often used in Azure or Okta