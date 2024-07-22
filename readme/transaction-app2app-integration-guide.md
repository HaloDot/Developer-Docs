---
description: >-
  Integration with Halo.Go application for Transactions using Android Intent
  Mechanisms or Deeplinking.
---

# Transaction App to App Integration Guide

## Architecture&#x20;

To initiate the transaction, the Customer Application must initiate the call between itself and  the Customer Backend first that the it wants to create intent transaction, this information is then passed  though, packaged, sealed and stored in Halo Backend. The process is as follows:&#x20;

1. Consumer Application creates a request  to the Customer Backend to create an Intent transaction.
2. The Consumer Backend will pass through the consumer transaction details:&#x20;

* the reference Number&#x20;
* currency,
* transaction amounts, &#x20;
* merchandising information out to the Halo backend.&#x20;

3. The Halo Backend packages it up, stores it as a "blob".&#x20;
4. With that it creates a transaction ID along with a signed JWT which is  sent back to the Customer Backend then passed to the Customer App to start the Transaction. The Consumer app will do a look up which returns all the transaction information.
5. So, at time of  transacting, the Consumer Application would have received a transaction ID and since the app itself cannot do a transaction, the Halo Backend signs a JWT specifically for this transaction to Identify it.
6. &#x20;These are passed through to the SDK which uses the information to start the actually payment cycle process.&#x20;
7. The SDK then request transaction details from the Halo Backend.&#x20;
8. The Halo Backend will return the packaged transaction information. . These are then passed into the SDK for further processing.

For authorization of the transaction, that is where the PIN Entry and Attestation process begins, so to authenticate the transaction.

The Architecture is drawn below:&#x20;

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Intent Processing</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Transaction/Payment Processing</p></figcaption></figure>



## 1. Android Intents Mechanism

Steps in this section: 1. Retrieve a `Transaction ID` and payment `JWT`from the Halo Backend. 2. Send an Intent Request to the Halo Dot Go application.

**1. Retrieve Transaction ID and JWT from Halo Backend**

Step two of Android Intents Mechanism integration is to initialize the transaction on the Halo Dot backend through an API request. You will need the `API Key` and `Merchant ID` from the previous step for this API call. The response will contain a `Transaction ID` and `JWT Token` that will be used in the third and final step.

_**Let’s take a closer look at the API request.**_

## Intent Transaction

<mark style="color:green;">`POST`</mark> `https://kernelserver.{env}.haloplus.io/{version}/consumer/intentTransaction`

The call to the Halo Dot Backend to initiate an Intent Transaction.

#### Path Parameters

| Name                                      | Type   | Description                              |
| ----------------------------------------- | ------ | ---------------------------------------- |
| version<mark style="color:red;">\*</mark> | String | The backend version                      |
| env<mark style="color:red;">\*</mark>     | String | The backend environment \[dev, qa, prod] |

#### Headers

| Name                                           | Type   | Description                                    |
| ---------------------------------------------- | ------ | ---------------------------------------------- |
| Content-Type<mark style="color:red;">\*</mark> | String | Content Type of the Request: application/json  |
| x-api-key<mark style="color:red;">\*</mark>    | String | The API Key retrieved from the Merchant Portal |

#### Request Body

| Name                                               | Type    | Description                        |
| -------------------------------------------------- | ------- | ---------------------------------- |
| merchantId<mark style="color:red;">\*</mark>       | Integer | Merchant ID from Merchant Portal   |
| paymentReference<mark style="color:red;">\*</mark> | String  | Reference of the transaction       |
| amount<mark style="color:red;">\*</mark>           | String  | Amount of the transaction (100.01) |
| timestamp<mark style="color:red;">\*</mark>        | String  | ISO Standard Timestamp             |
| currencyCode<mark style="color:red;">\*</mark>     | String  | ISO Standard Currency Codes        |

{% tabs %}
{% tab title="200: OK Intent Transaction JWT" %}
```json
{
    "id": "ffe12ca8-61e6-48f9-b09c-537818652988",
    "token": "eyJhbGciOiJSUzUxMiIsInR5cCI6IkpXVCJ9.eyJ1c3IiOiJoYWxvIiwiYXVkX2ZpbmdlcnByaW50cyI6InNoYTI1Ni96YzZjOTdKaEtQWlVhK3JJclZxamtuREUxbERjREs3N0c0MXNEbysxYXkwPSIsImtza19waW4iOiJzaGEyNTYvMVpuYTRUNlBLY0ozS3EvZGJWeWxiOG42MmovQWRRWVV6V3JqLzRzazVROD0iLCJtZXJjaGFudElkIjozMTcsImlhdCI6MTY3NTMzMzQyMCwiZXhwIjoxNjc1MzM0MzIwLCJhdWQiOiJrZXJuZWxzZXJ2ZXIucWEuaGFsb3BsdXMuaW8iLCJpc3MiOiJhdXRoc2VydmVyLnFhLmhhbG9wbHVzLmlvIiwic3ViIjoiYzQwMWIxYTYtNDI5Ny00NDM1LTg3OWItMDAyNTZhY2E4N2NjIn0.fCsDOSlkOz2nqjAohFYZNIO6f5cp4xbLer6s4o9BVJckoPRwxShdQLBxOySoYhioZ2WaYWFO-qhxDQjQG8RsPYByGsgIgQtVRaudS_IGI4Xv0KG8p0A9isX8jlw8KEeZwEuaj-zHUg4DAO4n3ydVAd3NjM1oysMKUbdn5MmW-wH7keutNCKtq9qF_hF0A8s3rUCO8UsB5QuXzz18VfPFe6fs3LoOGMHiKvgRWlhpKhrfXWQAw8vpwCLeY58vfa8LFGixMS526322s_dGTxkKC5f366GBWgoqHDyporidblCy64T5MbgifL41kiXahNQs6B4eLmuWeUTosHQ6jUajiEsa61QnUY1K9Pv3kT7bFDYy4Hvu2mdktzpV2p6MpM9gH3E4LLZGKhOJLjkf8LP7NsE-h4aN1XlKHJmMex8yMaAgV-_wxLCDPrK0Q7KgKGTNRByi8HkluhYYuMlslXXjN13ff8alMxCEBeyrkubi_X-tlTeilSmEF1tbWZ4WYiUfbNNqsfFDBKfErQc8dpJz22ou2DxyBd8_esBG1aEv4c5dIPciu_i2vG6FQADW_CNHmc01UnfymyReatc1c0WzFQS_OmoS3yaxymnvlCY_pD_bcZUr-5s60IQnu1D1wCeRfM1QE6-xSJvWx7sbXpbdNGbv1_PFM4xQTsuE6fBxzis"
}
```
{% endtab %}
{% endtabs %}

**2. Send an Intent Request to the Halo Dot Go**

We provide a sample code to help you with the intent request function call. The code is available in the App to app menu item in your Halo.Go Portal.

## 2. Deeplinking Mechanism

**1. Retrieve the Transaction URL from the Halo Backend**

Step two of the Deeplinking integration is to initialize the transaction on the Halo Dot backend through an API request. You will need the `API Key` and `Merchant ID` from the previous step for this API call. The response will contain the URL that can be used to invoke the Halo Dot application.

_**Let’s take a closer look at the API request.**_

## Deeplink Transaction

<mark style="color:green;">`POST`</mark> `https://kernelserver.prod.haloplus.io/1.0.12/consumer/qrCode`

The call to the Halo Dot Backend to initiate an Intent Transaction and retrieve a Transaction URL that can be used to invoke the Halo Dot Link application

#### Path Parameters

<table><thead><tr><th width="174">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>version<mark style="color:red;">*</mark></td><td>Stirng</td><td>The backend version</td></tr><tr><td>env<mark style="color:red;">*</mark></td><td>String</td><td>The backend environment [dev, qa, prod]</td></tr></tbody></table>

#### Headers

| Name                                           | Type   | Description                                    |
| ---------------------------------------------- | ------ | ---------------------------------------------- |
| Content-Type<mark style="color:red;">\*</mark> | String | Content Type of the Request: application/json  |
| x-api-key<mark style="color:red;">\*</mark>    | String | The API Key retrieved from the Merchant Portal |

#### Request Body

<table><thead><tr><th width="214">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>merchantId<mark style="color:red;">*</mark></td><td>Integer</td><td>Merchant ID from Merchant Portal</td></tr><tr><td>paymentReference<mark style="color:red;">*</mark></td><td>String</td><td>Reference of the transaction</td></tr><tr><td>amount<mark style="color:red;">*</mark></td><td>String</td><td>Amount of the  transaction (e.g. 100.01)</td></tr><tr><td>timestamp<mark style="color:red;">*</mark></td><td>String</td><td>ISO Standard Timestamp</td></tr><tr><td>currencyCode<mark style="color:red;">*</mark></td><td>String</td><td>ISO Standard Currency Codes</td></tr><tr><td>isConsumerApp<mark style="color:red;">*</mark></td><td>Boolean</td><td>Indicate if the call is for a Consumer App</td></tr><tr><td>image<mark style="color:red;">*</mark></td><td>JSON</td><td>Set to true to generate a QR code - {"required": false} </td></tr></tbody></table>

{% tabs %}
{% tab title="200: OK URL to invoke the Halo Dot Application for a payment" %}
```json
{
    "url": "https://halompos.page.link/DYfL4EZEzvAzBfBAS",
    "reference": "c9e1were-8156-444c-894d-e065d71366a6"
}
```
{% endtab %}
{% endtabs %}

**2. Use the Generated URL to call the Halo Dot Go application**

The generated link returned by the API call can then be used to invoke the Halo.Go application and start process transactions.

## 3. Conclusion

That concludes the guide on integrating the Halo.Go into your application. For any questions, please do not hesitate to reach out to the Halo Dot Team.
