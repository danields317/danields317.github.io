# API Management
API Management is an Azure service that creates a layer between API's and their callers. Callers go through the Azure API Management tool before reaching the actual endpoint, which can provide monitoring, security and other features.
## Core Components
The API Management system is made up of three core components.
- **API Gateway** - System that handles API calls and enforces configured networking rules.
- **Management Plane** - Interface used to configure the API management instance.
- **Developer Portal** - Automatically generated portal with API information.
## Products
API endpoints are grouped into a Product. This product can then be shared with developers to use.
There are **Open** and **Protected** products. A protected product requires a subscription to the product, which can be configured to require approval by an administrator. An Open product can be used without subscribing.
## Groups
API Management has three groups of users.
- **Administrators** - Manages the API Management instance and creates API's and products.
- **Developers** - Consume products and build applications that use the API's.
- **Guests** - Configured Read-only users. Can view API's but not call them.
## Policies
Statements sequentially executed on a request or response. Can perform different tasks like converting data structure or check rate limiting. Policies can be configured on an API through XML. The policy system contains multiple different Policy Expressions that can be used to create policies.
```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies>
```
## Securing APIs
API Management offers a Subscription system to secure APIs. A subscription generates a key that the client needs to add to their request to API Management to get authenticated.

A Subscription can be created on three scopes:
- **All APIs** - Access to all APIs in the API Management instance.
- **API** - Access to a single API.
- **Product** - Access to all APIs in a product.
A subscription contains two keys. Primary and Secondary key. Only one has to be added to the request. The point of the secondary key is to prevent downtime when the primary key is unusable (e.g. when it needs to be regenerated).

The key can be passed in a request in two ways. Either as a header or query parameter.
```bash
curl --header "Ocp-Apim-Subscription-Key: <key string>" https://<apim gateway>.azure-api.net/api/path
curl https://<apim gateway>.azure-api.net/api/path?subscription-key=<key string>
```
## Certificate security
There are policies specific to certificate validation. These can be useful when very granular access is desired. The table underneath shows the four important ways a certificate can be validated.

| Property                       | Description                                          |
| ------------------------------ | ---------------------------------------------------- |
| **Certificate Authority (CA)** | Only allow certificates signed by a particular CA    |
| **Thumbprint**                 | Allow certificates containing a specified thumbprint |
| **Subject**                    | Only allow certificates with a specified subject     |
| **Expiration Date**            | Don't allow expired certificates                     |

---

*References*
- [*Explore API Management*](https://learn.microsoft.com/en-us/training/modules/explore-api-management/)