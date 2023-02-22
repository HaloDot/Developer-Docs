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

{% swagger-parameter in="path" name="env" type="String" required="true" %}
The backend environment [dev, qa, prod]
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-header" type="String" required="true" %}
The API Key retrieved from the Merchant Portal
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Status of the transaction" %}
```javascript
{
    "status": [Approved, Declined, UnableToGoOnline, Indeterminate, Voided]
}
```
{% endswagger-response %}
{% endswagger %}

## 2. Get TT3 Transactions via API Call

{% swagger method="get" path="/:reference" baseUrl="https://kernelserver.{env}.haloplus.io/{version}/consumer/tt3QRCode" summary="" %}
{% swagger-description %}
Asynchronously get details about TT3 transactions
{% endswagger-description %}

{% swagger-parameter in="path" name="version" type="String" required="true" %}
The backend version.
{% endswagger-parameter %}

{% swagger-parameter in="path" required="true" name="envv" type="String" %}
The backend environment [dev, qa, prod]
{% endswagger-parameter %}

{% swagger-parameter in="query" name=":reference" type="String" %}
The TT3 Transaction Reference
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-key" type="String" %}
The API Key retrieved from the Merchant Portal
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Status of the transaction" %}
```javascript
{
    "qrCodeState": [QRCodeGenerated, QRCodeScanned, TransactionStarted, TransactionCreated, ResponseReceivedByPhone]
}
```
{% endswagger-response %}
{% endswagger %}
