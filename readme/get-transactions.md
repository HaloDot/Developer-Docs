---
description: Asynchronously retrieve information about transactions
---

# Get Transactions

## 1. Get Transactions via API Call

It is possible to get more information about a transaction asynchronously with an API Call to the Halo Backend.

_**Let’s take a closer look at the API request.**_&#x20;

{% swagger method="get" path="/:id" baseUrl="https://kernelserver.{env}.haloplus.io/{version}/transactions" summary="" %}
{% swagger-description %}
Asynchronously get details about transactions
{% endswagger-description %}

{% swagger-parameter in="query" name=":id" type="String" required="true" %}
The Transaction ID
{% endswagger-parameter %}

{% swagger-parameter in="path" name="version" type="String" required="true" %}
The backend version.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="env" type="String" %}
The backend environment [dev, qa, prod]
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-header" type="String" %}
The API Key retrieved from the Merchant Portal
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
