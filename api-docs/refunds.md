---
description: Refund a transaction
---

# Refunds

{% swagger method="post" path="/refund" baseUrl="https://kernelserver.{env}.haloplus.io/{version}/transactions/transactionId" summary="" %}
{% swagger-description %}
Asynchronously get details about transactions
{% endswagger-description %}

{% swagger-parameter in="path" name="version" type="String" required="true" %}
The backend version.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="env" type="String" required="true" %}
The backend environment [dev, qa, prod]
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-header" type="String" required="true" %}
The API Key retrieved from the Portal
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="Number" required="true" %}
Monetary value of the transaction
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refundReference" type="String" required="true" %}
Reference of the refund
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Status of the transaction" %}
```javascript
{
    type: "Approved",
    authorizationCode: "asdflk",
    tags: [{ "tag": "9F1E", "33333333"}],
    haloReference: "5cb6a780-f3bc-45b6-b1ef-bf7fe5e41fbf",  
    errorMessage: "Ok",
    errorCode: 0,
    isoResponseCode: 0,
    association: "Visa",
    expiryDate: "07/24",
    paymentProviderReference: "5cb6a780-f3bc-45b6-b1ef-bf7fe5e41fbf"
}
```
{% endswagger-response %}
{% endswagger %}
