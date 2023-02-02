# TT3 Intent Integration Guide

## 1. Android Intents Mechanism

Steps in this section:

1. Retrieve a `Transaction ID` and payment `JWT`from the Halo Backend.
2. Send an Intent Request to the Halo Dot Go application.

**1. Retrieve Transaction ID and JWT from Halo Backend**

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
    "accountNumber": "1234567890",
    "id": "0987654321",
    "maxCollectionAmount": "100", 
    "contractReference": "TT3 Transaction",
    "timestamp": "Mon Jan 02 00:00:00 SAST 2023"
}
```

The request should be sent to the following endpoint:

https://kernelserver.prod.haloplus.io/1.0.8/consumer/tt3IntentTransaction

_**Full cURL example**_

```
curl 
-X POST
-H "Content-Type: application/json"
-H "x-api-key: dm9sb2R5bXlyQHN5bnRoZXNpcy5jby56YS4yNDU3MTE0OC01NjUxLTQ5YTEtOTIzMi0zMTk0OTk4MGFhMDI="
-d '{
        "merchantId" : 9, 
        "accountNumber": "1234567890",
        "id": "0987654321",
        "maxCollectionAmount": "100", 
        "contractReference": "TT3 Transaction",
        "timestamp": "Mon Jan 02 00:00:00 SAST 2023"
    }'
https://kernelserver.prod.haloplus.io/1.0.8/consumer/intentTransaction
```

**2. Send an Intent Request to the Halo Dot Go**

We provide sample code to help you with the intent request function call. The code is available on your Halo Dot Go Merchant Portal. The code is made available in this repo ovehere.

## 2. Deeplinking Mechanism

Steps in this section:
   1. Retrieve the Transaction URL from the Halo Backend
   2. Use the Generated URL to call the Halo Dot Go application.

**1. Retrieve the Transaction URL from the Halo Backend**

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
    "accountNumber": "1234567890",
    "id": "0987654321",
    "maxCollectionAmount": "100", 
    "contractReference": "Test from Postman",
    "timestamp": "Mon Jan 02 00:00:00 SAST 2023",
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
        "accountNumber": "1234567890",
        "id": "0987654321",
        "maxCollectionAmount": "100", 
        "contractReference": "Test from Postman",
        "timestamp": "Mon Jan 02 00:00:00 SAST 2023",
        "isConsumerApp": false,
        "image": {
            "required": false
        }
    }'
https://kernelserver.prod.haloplus.io/1.0.12/consumer/tt3QRCode
```

**2. Use the Generated URL to call the Halo Dot Go application**

The generated link returned by the API call can then be used to invoke the Halo Dot Go application and start process transactions.

## 3. Conclusion

That concludes the guide to integrating the Halo Dot Go into your application. For any questions, please do not hesitate to reach out to the Halo Dot Team.

Not what you were looking for? If you are looking for the TT3 Intent Integration guide, it is over [here](transaction-intent-integration-guide.md)
