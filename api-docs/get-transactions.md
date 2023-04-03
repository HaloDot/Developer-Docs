---
description: Asynchronously retrieve information about transactions
---

# Get Transaction Status and Details

## Get Status of Transactions

{% swagger method="get" path="/:reference" baseUrl="https://kernelserver.{env}.haloplus.io/{version}/consumer/QRCode" summary="" %}
{% swagger-description %}
Asynchronously get Status of a transactions invoked through a link.
{% endswagger-description %}

{% swagger-parameter in="path" name="version" type="String" required="true" %}
The backend version.
{% endswagger-parameter %}

{% swagger-parameter in="path" required="true" name="env" type="String" %}
The backend environment [dev, qa, prod]
{% endswagger-parameter %}

{% swagger-parameter in="query" name=":reference" type="String" required="true" %}
The id received when creating the intent transaction
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-key" type="String" required="true" %}
The API Key retrieved from the Merchant Portal
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Status of the transaction" %}
```javascript
{
    "qrCodeState": "ResponseReceivedByPhone",
    "transactionId": "693b47d8-e325-4808-8f86-67e388fd35ec",
    "merchantTransactionReference": "TT3 Test",
    "userId": "ebfbd120-76db-4a47-b040-f14ff7ee291f",
    "status": "AcknowledgedByPhone",
    "disposition": "Approved",
    "amount": "0.01",
    "currency": "ZAR",
    "type": "DebiCheck",
    "responseCode": "0",
    "authorisationCode": "3CA40B2A",
    "createdAt": "2023-03-01T10:35:02.585Z",
    "updatedAt": "2023-03-01T10:35:05.499Z",
    "collectionDay": "25",
    "creditorABSN": "InsuranceABC",
    "accountNumber": "123456789",
    "idNumber": "",
    "maxCollectionAmount: "1000",
    "contractReference": "Example Ref",
    "paymentReference": "Example Ref";
}
```
{% endswagger-response %}
{% endswagger %}

## Get Status of TT3 Transactions

{% swagger method="get" path="/:reference" baseUrl="https://kernelserver.{env}.haloplus.io/{version}/consumer/tt3QRCode" summary="" %}
{% swagger-description %}
Asynchronously get Status about TT3 transactions invoked through a link.
{% endswagger-description %}

{% swagger-parameter in="path" name="version" type="String" required="true" %}
The backend version.
{% endswagger-parameter %}

{% swagger-parameter in="path" required="true" name="env" type="String" %}
The backend environment [dev, qa, prod]
{% endswagger-parameter %}

{% swagger-parameter in="query" name=":reference" type="String" required="true" %}
The reference received in the response when the link is created
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-key" type="String" required="true" %}
The API Key retrieved from the Merchant Portal
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Status of the transaction" %}
```javascript
{
    "qrCodeState": "ResponseReceivedByPhone",
    "transactionId": "693b47d8-e325-4808-8f86-67e388fd35ec",
    "merchantTransactionReference": "TT3 Test",
    "userId": "ebfbd120-76db-4a47-b040-f14ff7ee291f",
    "status": "AcknowledgedByPhone",
    "disposition": "Approved",
    "amount": "0.01",
    "currency": "ZAR",
    "type": "DebiCheck",
    "responseCode": "0",
    "authorisationCode": "3CA40B2A",
    "createdAt": "2023-03-01T10:35:02.585Z",
    "updatedAt": "2023-03-01T10:35:05.499Z",
    "collectionDay": "25",
    "creditorABSN": "InsuranceABC",
    "accountNumber": "123456789",
    "idNumber": "",
    "maxCollectionAmount: "1000",
    "contractReference": "Example Ref",
    "paymentReference": "Example Ref";
}
```
{% endswagger-response %}
{% endswagger %}



### Status of transaction descriptions:

| QRCodeState                                | Description                                                                                    |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| QRCodeGenerated                            | Initial call made to create the QR code/URL                                                    |
| QRCodeScanned                              | Device retrieves the transaction details that were provided when the QR code/URL was generated |
| TransactionStarted                         | Performed before reading the card, the device is ready to read card.                           |
| TransactionCreated                         | Card reading completed. Transaction has been sent to gateway.                                  |
| ResponseReceivedByPhone (Definite Success) | The response from gateway is acknowledged by device.                                           |

### Status Codes:

| BadRequestReceived                   |   |
| ------------------------------------ | - |
| RequestReceived                      |   |
| ErrorFindingConfig                   |   |
| ReadyToSubmitToPaymentProcessor      |   |
| SubmittedToPaymentProcessor          |   |
| NoResponseFromPaymentProcessor       |   |
| BadResponseFromPaymentProcessor      |   |
| ResponseReceivedFromPaymentProcessor |   |
| RespondedToPhone                     |   |
| FailedToRespondToPhone               |   |
| AcknowledgedByPhone                  |   |

### Response Codes:

The responseCode fields maps to the ISO 8583 response codes

{% embed url="https://en.wikipedia.org/wiki/ISO_8583#Ver_1987" %}
ISO 8589 Codes
{% endembed %}

## Get Transactions Details

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
