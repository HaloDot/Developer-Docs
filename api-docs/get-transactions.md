---
description: >-
  Asynchronously retrieve information about payment transactions and TT3
  Transactions
---

# Get Transaction Status and Details

## Get Status of Transaction Request

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
    "merchantTransactionReference": "Transaction Test",
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
    "paymentReference": "Example Ref";
}
```
{% endswagger-response %}
{% endswagger %}

### Transaction Response Descriptions:

| Field                        | Description                                                                                    | Type             |
| ---------------------------- | ---------------------------------------------------------------------------------------------- | ---------------- |
| qrCodeState                  | Status of the deeplink created                                                                 | String (64)      |
| transactionId                | ID of the transaction when created                                                             | String (UUID v4) |
| merchantTransactionReference | Reference entered by the merchant                                                              | String (255)     |
| status                       | At what point the transaction is in the transaction flow (ResponseReceivedFromPaymentProvider) | String (64)      |
| disposition                  | The outcome of the transaction (e.g. Approved)                                                 | String (32)      |
| amount                       | Value of transaction (e.g R100)                                                                | String           |
| currency                     | Currency of the amount (e.g. ZAR, GBP)                                                         | String (3)       |
| type                         | The type of transaction (e.g. Tap, TT3, Secure card reader)                                    | String (32)      |
| responseCode                 | The ISO response code of the transaction                                                       | Number           |
| createdAt                    | ISO date when the transaction was created                                                      |                  |
| updatedAt                    | ISO date when the transaction was last updated                                                 |                  |
| paymentReference             | Reference of the transaction provided by customer                                              | String (255)     |

## Get Status of TT3 Transaction

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
    "amount": 10000,
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

### TT3 Transaction Response Descriptions:

| Field               | Description                                                                                    | Type                |
| ------------------- | ---------------------------------------------------------------------------------------------- | ------------------- |
| qrCodeState         | Status of the deeplink created                                                                 | String (64)         |
| transactionId       | ID of the transaction when created                                                             | String (UUID v4)    |
| status              | At what point the transaction is in the transaction flow (ResponseReceivedFromPaymentProvider) | String (64)         |
| disposition         | The outcome of the transaction (e.g. Approved)                                                 | String (32)         |
| currency            | Currency of the amount (e.g. ZAR, GBP)                                                         | String (3)          |
| type                | The type of transaction (e.g. Tap, TT3, Secure card reader)                                    | String (32)         |
| responseCode        | The ISO response code of the transaction                                                       | Number              |
| authorisationCode   | Message Authorization Code (MAC)                                                               | String (MAC Length) |
| createdAt           | ISO date when the transaction was created                                                      |                     |
| updatedAt           | ISO date when the transaction was last updated                                                 |                     |
| collectionDay       | The day in which the debit order should be collected                                           | Number              |
| creditorABSN        | Name of Insurance Company                                                                      | String              |
| accountNumber       | Account number of the customer                                                                 | String              |
| idNumber            | ID number of the customer                                                                      | String (13)         |
| maxCollectionAmount | The value of the debit order ( R100)                                                           | String              |
| contractReference   | Reference of the debicheck transaction provided by customer                                    | String (255)        |

| QRCodeState                                | Description                                                                                    |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| QRCodeGenerated                            | Initial call made to create the QR code/URL                                                    |
| QRCodeScanned                              | Device retrieves the transaction details that were provided when the QR code/URL was generated |
| TransactionStarted                         | Performed before reading the card, the device is ready to read card.                           |
| TransactionCreated                         | Card reading completed. Transaction has been sent to gateway.                                  |
| ResponseReceivedByPhone (Definite Success) | The response from gateway is acknowledged by device.                                           |

### Status Options:

| BadRequestReceived                   | The request received from the device was badly formatted                  |
| ------------------------------------ | ------------------------------------------------------------------------- |
| RequestReceived                      | The backend received the transaction request from the device              |
| ErrorFindingConfig                   | The backend was unable to find config for this transaction                |
| ReadyToSubmitToPaymentProcessor      | The transaction is about to be submitted to the payment processor         |
| SubmittedToPaymentProcessor          | The transaction has been submitted to the payment processor               |
| NoResponseFromPaymentProcessor       | The payment processor did not respond to the payment request              |
| BadResponseFromPaymentProcessor      | The payment processor returned an invalid response to the payment request |
| ResponseReceivedFromPaymentProcessor | The payment processor responded to the request                            |
| RespondedToPhone                     | The transaction outcome was returned to the device                        |
| FailedToRespondToPhone               | The transaction outcome could not be returned to the device               |
| AcknowledgedByPhone                  | The device acknowledged the outcome                                       |

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

### Transaction Details Status Options:

| Status           |   |
| ---------------- | - |
| Approved         |   |
| Declined         |   |
| UnableToGoOnline |   |
| Indeterminate    |   |
| Voided           |   |

