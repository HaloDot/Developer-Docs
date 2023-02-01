# Transaction Intent Integration Guide

* [Transaction Intent Integration Guide](transaction-intent-integration-guide.md#transaction-intent-integration-guide)
  * [1. Intent Integration Methods](transaction-intent-integration-guide.md#1-intent-integration-methods)
  * [2. Android Intents Mechanism](transaction-intent-integration-guide.md#2-android-intents-mechanism)
  * [3. Deeplinking Mechanism](transaction-intent-integration-guide.md#3-deeplinking-mechanism)
  * [4. Conclusion](transaction-intent-integration-guide.md#4-conclusion)

## 1. Intent Integration Methods

The Halo Dot Link application currently provides different mechanisms to integrate our payments solution depending on your use-case. The different methods are:

1. Android Intents Mechanism
2. Deeplinking Mechanism
3. Android Intents with Callback

Have a look at the image below as a guideline:

![Integration Mechanisms](<../../assets/Android vs deeplinking.png>)

This guide will walk you through integration for each mechanism. If you are trying to do a TT3 intent integration, refer to the [TT3 Integration Guide](tt3-intent-integration-guide.md).

## 2. Android Intents Mechanism

This section provides guidance on how to integrate your calling application with the Halo Dot Go app through the Android Intent Mechanism. This is an easy three-step process:

1. Retrieve your `Merchant ID` and `API Key` from the Merchant Portal.
2. Retrieve a `Transaction ID` and payment `JWT`from the Halo Backend.
3. Send an Intent Request to the Halo Dot Go application.

**1. Retrieve details from the Merchant Portal**

_**Get Merchant ID**_

The `Merchant ID` can easy be found from the Halo Dot Go Merchant Portal. From the Merchant Portal, navigate to the Help Center Tab. There, under Try Deep Linking you will see your unique `Merchant ID`. See screenshot below:

![Merchant Portal](<../../assets/Merchant Portal.png>))

_**Get x-api-key**_

Right next to your `Merchant ID` on the Try Deep Linking page is the option to generate your `API Key`. Selecting this option will transfer you to the User Management Page:

![User Management Page](../../Intents/assets/User%20Page.png)

Now you can generate a unique `API Key` for your user. Note the warning pop-up when generating an `API Key`.

![API Key Warning](<../../assets/API Key Warning.png>)

Since an `API Key`is a sensitive value, it is stored as an encrypted value in our database and only presented in clear text once during the initial retrieval. It is the responsibility of the user to keep their `API Key` safe.

![API Key](<../../assets/Generated API Key.png>)

**2. Retrieve Transaction ID and JWT from Halo Backend**

Step two of Android Intents Mechanism integration is to initialize the transaction on the Halo Dot backend through an API request. You will need the `API Key` and `Merchant ID` from the previous step for this API call. The response will contain a `Transaction ID` and `JWT Token` that will be used in the third and final step.

_**Let’s take a closer look at the API request.**_ To illustrate the API Request, we will be looking at a basic cURL request. Here’s a list of the parameters for the cURL request:

| Parameter | Value                            | Description                     |
| --------- | -------------------------------- | ------------------------------- |
| -X        | POST                             | Request Type                    |
| -H        | “Content-Type: application/json” | Content Type of the Request     |
| -H        | “x-api-key: ”                    | The API Key retrieved in Step 1 |
| -d        | JSON Body show below             | The JSON body of the Request    |

Request JSON body:

```json
{
    "merchantId" : 9, 
    "paymentReference": "Intent Transaction",
    "amount": 10, 
    "timestamp": "Mon Jan 02 00:00:00 SAST 2023", 
    "currencyCode": "ZAR" 
}
```

The request should be sent to the following endpoint:

https://kernelserver.prod.haloplus.io/1.0.8/consumer/intentTransaction

_**Full cURL example**_

```
curl 
-X POST \
-H "Content-Type: application/json" \
-H "x-api-key: dm9sb2R5bXlyQHN5bnRoZXNpcy5jby56YS4yNDU3MTE0OC01NjUxLTQ5YTEtOTIzMi0zMTk0OTk4MGFhMDI=" \
-d '{
        "amount":1.0,
        "merchantId": 9,
        "paymentReference": "Intent Transaction",
        "currencyCode": "ZAR",
        "timestamp": "Mon Jan 02 00:00:00 SAST 2023"
}'
https://kernelserver.prod.haloplus.io/1.0.8/consumer/intentTransaction
```

**3. Send an Intent Request to the Halo Dot Go**

We provide sample code to help you with the intent request function call. The code is available on your Halo Dot Go Merchant Portal. The code is made available in this repo ovehere.

## 3. Deeplinking Mechanism

This section provides guidance on how to integrate your calling application with the Halo Dot Go app through a URL. Invoking the Halo Dot Go application is an easy three-step process:

1. Retrieve your Merchant ID from the Merchant Portal
2. Retrieve JWT from the Halo Backend
3. Retrieve the Transaction URL from the Halo Backend

**1. Retrieve details from the Merchant Portal**

Exact same proccess as described under the _**Get Merchant ID**_ subheading [here](transaction-intent-integration-guide.md#2-android-intents-mechanism)

**2. Retrieve JWT from the Halo Backend**

Step two is where we deviate from the proccess of the Android Intent Mechanism. The API call for a endpoint to use with Deeplinking requires a `JWT token`.

One option to get a fresh `JWT token` is an API call. This is a very basic call.

The endpoint for this call is: https://authserver.prod.haloplus.io/login

The request is a POST with a JSON body with two variables:

* username
* password

The username and password are the same as you use on the Halo Dot Go application.

**3. Retrieve the Transaction URL from the Halo Backend**

The last step of Deeplinking integration is to retrieve the URL from the Halo Dot backend through an API request. You will need the `Merchant ID` and `JWT` from the previous two steps for this API call.

_**Let’s take a closer look at the API request.**_

To illustrate the API Request, we will be looking at a basic cURL request. Here’s a list of the parameters for the cURL request:

| Parameter | Value                            | Description                  |
| --------- | -------------------------------- | ---------------------------- |
| -X        | POST                             | Request Type                 |
| -H        | “Content-Type: application/json” | Content Type of the Request  |
| -H        | “Authorisation: Bearer ”         | The JWT retrieved in Step 2  |
| -d        | JSON Body show below             | The JSON body of the Request |

Request JSON body:

```json
{
    "merchantId" : 9, 
    "paymentReference": "URL Intent Transaction",
    "amount": 10, 
    "timestamp": "Mon Jan 02 00:00:00 SAST 2023", 
    "currencyCode": "ZAR",
    "isConsumerApp": false,
    "image": {
        "required": false
    }
}
```

The request should be sent to the following endpoint: https://kernelserver.prod.haloplus.io/1.0.12/consumer/qrCode

_**Full cURL example**_

```
curl 
-X POST
-H "Content-Type: application/json"
-H "Authorisation: Bearer dm9sb2R5bXlyQHN5bnRoZXNpcy5jby56YS4yNDU3MTE0OC01NjUxLTQ5YTEtOTIzMi0zMTk0OTk4MGFhMDI=" 
-d '{
      "merchantId" : 9, 
      "paymentReference": "URL Intent Transaction",
      "amount": 10, 
      "timestamp": "Mon Jan 02 00:00:00 SAST 2023", 
      "currencyCode": "ZAR",
      "isConsumerApp": false,
      "image": {
          "required": false
      }
    }'
https://kernelserver.prod.haloplus.io/1.0.12/consumer/qrCode
```

The generated link returned by the API call can then be used to invoke the Halo Dot Go application and start process transactions.

## 4. Conclusion

That concludes the guide to integrate the Halo Dot Go into your application. For any questions, please do not hesitate to reach out to the Halo Dot Team.

Not what you were looking for? If you are looking for the the TT3 Intent Integration guide, it is over [here](tt3-intent-integration-guide.md)
