[Back to README](../README.md) | Previous: [Overview.md](../8. MarketplaceAndDataExchange/Overview.md) | Next: [Overview.md](Overview.md)

# External Functions

*Notes related to Snowpark and Extensibility: Using External Functions.*

## Key Topics
*   **Purpose:** To call code that resides and executes outside of Snowflake (e.g., custom machine learning models, proprietary algorithms, microservices).
*   **Architecture:**
    *   Snowflake sends data to a proxy service (e.g., AWS API Gateway, Azure API Management, Google Cloud API Gateway).
    *   The proxy service forwards the request to the remote service (e.g., AWS Lambda, Azure Function, Google Cloud Function).
    *   The remote service processes the data and returns a response.
*   **Creating External Functions:** `CREATE EXTERNAL FUNCTION ... API_INTEGRATION = ... AS ...`
*   **API Integration Object:** Securely stores information about the proxy service.
*   **Request/Response Format:** Typically JSON.
*   **Security Considerations:** Authentication and authorization between Snowflake, proxy service, and remote service.
*   **Use Cases:** Geocoding, sentiment analysis, custom model inference, accessing external APIs.
