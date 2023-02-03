---
description: >-
  Integration with Halo.Go application for TT3 Transactions using Android Intent
  Mechanisms or Deeplinking.
---

# TT3 Intent Integration Guide

## 1. Android Intents Mechanism

Steps in this section:

1. Retrieve a `Transaction ID` and payment `JWT`from the Halo Backend.
2. Send an Intent Request to the Halo Dot Go application.

**1. Retrieve Transaction ID and JWT from Halo Backend**

Step two of Android Intents Mechanism integration is to initialize the transaction on the Halo Dot backend through an API request. You will need the `API Key` and `Merchant ID` from the previous step for this API call. The response will contain a `Transaction ID` and `JWT Token` that will be used in the third and final step.

_**Let’s take a closer look at the API request.**_&#x20;

{% swagger method="post" path="" baseUrl="https://kernelserver.{env}.haloplus.io/{version}/consumer/tt3IntentTransaction" summary="Intent Transaction" expanded="false" %}
{% swagger-description %}
The call to the Halo Dot Backend to initiate a TT3 Intent Transaction.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" required="true" type="String" %}
Content Type of the Request: application/json
{% endswagger-parameter %}

{% swagger-parameter in="header" type="String" name="x-api-key" required="true" %}
The API Key retrieved from the Merchant Portal
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchantId" type="Integer" required="true" %}
Merchant ID from Merchant Portal
{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="String" %}
ID number of the account holder
{% endswagger-parameter %}

{% swagger-parameter in="body" name="accountNumber" required="true" type="String" %}
Account Number of the Debit Order
{% endswagger-parameter %}

{% swagger-parameter in="body" name="maxCollectionAmount" type="Integer" required="true" %}
Max amount of the Debit Order
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" type="String" required="true" %}
ISO Standard Timestamp
{% endswagger-parameter %}

{% swagger-parameter in="body" name="contractReference" type="String" required="true" %}
Reference of the Debit Order
{% endswagger-parameter %}

{% swagger-parameter in="path" name="version" type="String" required="true" %}
The backend version.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="env" type="String" required="true" %}
The backend environment [dev, qa, prod]
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="TT3 Intent Transaction JWT" %}
```json
{
    "id": "ffe12ca8-61e6-48f9-b09c-537818652988",
    "token": "eyJhbGciOiJSUzUxMiIsInR5cCI6IkpXVCJ9.eyJ1c3IiOiJoYWxvIiwiYXVkX2ZpbmdlcnByaW50cyI6InNoYTI1Ni96YzZjOTdKaEtQWlVhK3JJclZxamtuREUxbERjREs3N0c0MXNEbysxYXkwPSIsImtza19waW4iOiJzaGEyNTYvMVpuYTRUNlBLY0ozS3EvZGJWeWxiOG42MmovQWRRWVV6V3JqLzRzazVROD0iLCJtZXJjaGFudElkIjozMTcsImlhdCI6MTY3NTMzMzQyMCwiZXhwIjoxNjc1MzM0MzIwLCJhdWQiOiJrZXJuZWxzZXJ2ZXIucWEuaGFsb3BsdXMuaW8iLCJpc3MiOiJhdXRoc2VydmVyLnFhLmhhbG9wbHVzLmlvIiwic3ViIjoiYzQwMWIxYTYtNDI5Ny00NDM1LTg3OWItMDAyNTZhY2E4N2NjIn0.fCsDOSlkOz2nqjAohFYZNIO6f5cp4xbLer6s4o9BVJckoPRwxShdQLBxOySoYhioZ2WaYWFO-qhxDQjQG8RsPYByGsgIgQtVRaudS_IGI4Xv0KG8p0A9isX8jlw8KEeZwEuaj-zHUg4DAO4n3ydVAd3NjM1oysMKUbdn5MmW-wH7keutNCKtq9qF_hF0A8s3rUCO8UsB5QuXzz18VfPFe6fs3LoOGMHiKvgRWlhpKhrfXWQAw8vpwCLeY58vfa8LFGixMS526322s_dGTxkKC5f366GBWgoqHDyporidblCy64T5MbgifL41kiXahNQs6B4eLmuWeUTosHQ6jUajiEsa61QnUY1K9Pv3kT7bFDYy4Hvu2mdktzpV2p6MpM9gH3E4LLZGKhOJLjkf8LP7NsE-h4aN1XlKHJmMex8yMaAgV-_wxLCDPrK0Q7KgKGTNRByi8HkluhYYuMlslXXjN13ff8alMxCEBeyrkubi_X-tlTeilSmEF1tbWZ4WYiUfbNNqsfFDBKfErQc8dpJz22ou2DxyBd8_esBG1aEv4c5dIPciu_i2vG6FQADW_CNHmc01UnfymyReatc1c0WzFQS_OmoS3yaxymnvlCY_pD_bcZUr-5s60IQnu1D1wCeRfM1QE6-xSJvWx7sbXpbdNGbv1_PFM4xQTsuE6fBxzis"
}
```
{% endswagger-response %}
{% endswagger %}

**2. Send an Intent Request to the Halo Dot Go**

We provide a sample code to help you with the intent request function call. The code is available on your Halo Dot Go Merchant Portal. The code is made available in this repo over here.

## 2. Deeplinking Mechanism

Steps in this section:

1. Retrieve the `Transaction URL` from the Halo Backend
2. Use the Generated URL to call the Halo Dot Go application.

**1. Retrieve the Transaction URL from the Halo Backend**

The last step of Deeplinking integration is to retrieve the URL from the Halo Dot backend through an API request. You will need the `API Key` and `Merchant ID` from Getting Started for this API call.

_**Let’s take a closer look at the API request.**_

_****_

{% swagger method="post" path="" baseUrl="https://kernelserver.{env}.haloplus.io/{version}/consumer/tt3QRCode" summary="Transaction URL" %}
{% swagger-description %}
The call to the Halo Dot Backend to initiate an Intent Transaction and retrieve a Transaction URL that can be used to invoke the Halo Dot Link application
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" required="true" type="String" %}
Content Type of the Request: application/json
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-key" required="true" type="String" %}
The API Key retrieved from the Merchant Portal
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchantId" type="Integer" required="true" %}
Merchant ID from Merchant Portal
{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="String" required="true" %}
ID number of the account holder
{% endswagger-parameter %}

{% swagger-parameter in="body" name="accountNumber" type="String" required="true" %}
Account Number of the Debit Order
{% endswagger-parameter %}

{% swagger-parameter in="body" name="maxCollectionAmount" type="Integer" required="true" %}
Max amount of the Debit Order
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" type="String" required="true" %}
ISO Standard Timestamp
{% endswagger-parameter %}

{% swagger-parameter in="body" required="true" name="contractReference" type="Boolean" %}
contractReference
{% endswagger-parameter %}

{% swagger-parameter in="body" type="Boolean" name="isConsumerApp" %}
Indicate if the call is for a Consumer App
{% endswagger-parameter %}

{% swagger-parameter in="body" required="true" name="image" type="JSON" %}
Set to true to generate a QR code - {"required": false} 
{% endswagger-parameter %}

{% swagger-parameter in="path" name="version" type="String" required="true" %}
The backend version.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="env" type="String" required="true" %}
The backend environment [dev, qa, prod]
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="URL to invoke the Halo Dot Application for a payment" %}
```json
{
    "url": "https://halompos.page.link/DYfL4EZEzvAzBfVNA"
}
```
{% endswagger-response %}
{% endswagger %}

**2. Use the Generated URL to call the Halo Dot Go application**

The generated link returned by the API call can then be used to invoke the Halo Dot Go application and start processing the transaction.

## 3. Conclusion

That concludes the guide to integrating the Halo Dot Go into your application. For any questions, please do not hesitate to reach out to the Halo Dot Team.

Not what you were looking for? If you are looking for the TT3 Intent Integration guide, it is over [here](transaction-intent-integration-guide.md)
