---
description: >-
  Asynchronously retrieve information about payment transactions and TT3
  Transactions
---

# Get Transaction Status and Details

## Get Status of Transaction Request

<mark style="color:blue;">`GET`</mark> `https://kernelserver.{env}.haloplus.io/consumer/QRCode/:reference`

Asynchronously get Status of a transactions invoked through a link.

#### Path Parameters

| Name                                      | Type   | Description                              |
| ----------------------------------------- | ------ | ---------------------------------------- |
| env<mark style="color:red;">\*</mark>     | String | The backend environment \[dev, qa, prod] |

#### Query Parameters

| Name                                         | Type   | Description                                          |
| -------------------------------------------- | ------ | ---------------------------------------------------- |
| :reference<mark style="color:red;">\*</mark> | String | The id received when creating the intent transaction |

#### Headers

| Name                                        | Type   | Description                                    |
| ------------------------------------------- | ------ | ---------------------------------------------- |
| x-api-key<mark style="color:red;">\*</mark> | String | The API Key retrieved from the Merchant Portal |

{% tabs %}
{% tab title="200: OK Status of the transaction" %}
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
{% endtab %}
{% endtabs %}

### Transaction Response Descriptions:

| Field                        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Type             |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| qrCodeState                  | Status of the deeplink created                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | String (64)      |
| transactionId                | ID of the transaction when created                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | String (UUID v4) |
| merchantTransactionReference | Reference entered by the merchant                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | String (255)     |
| status                       | At what point the transaction is in the transaction flow (ResponseReceivedFromPaymentProvider)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | String (64)      |
| disposition                  | <p>The outcome of the transaction (e.g. Approved)<br><br></p><p>There are 5 possible values for <code>disposition</code>​:</p><ul><li><code>Approved</code>​ - this means we got an approved message back from the processor </li><li><code>Declined</code>​ - this means we received a decline from the processor</li><li><code>UnableToGoOnline</code>​ - this means we couldn't connect to the processor. Essentially a decline, but it tells us the decline is due to a network error, and not a card issue</li><li><code>Indeterminate</code>​ - this means we either received an error from the processor or no response. This means we are unable to determine the status of the transaction. Typically, we treat these as declines and then we attempt to void the transaction in the background, in the event that the processor got the message but we just didn't get the response</li><li><code>Voided</code>​ - the transaction was reversed.</li></ul> | String (32)      |
| amount                       | Value of transaction (e.g 100.01)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | String           |
| currency                     | Currency of the amount (e.g. ZAR, GBP)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | String (3)       |
| type                         | The type of transaction (e.g. Tap, TT3, Secure card reader)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | String (32)      |
| responseCode                 | The ISO response code of the transaction                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Number           |
| createdAt                    | ISO date when the transaction was created                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |                  |
| updatedAt                    | ISO date when the transaction was last updated                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |                  |
| paymentReference             | Reference of the transaction provided by customer                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | String (255)     |

## Get Status of TT3 Transaction

<mark style="color:blue;">`GET`</mark> `https://kernelserver.{env}.haloplus.io/consumer/tt3QRCode/:reference`

Asynchronously get Status about TT3 transactions invoked through a link.

#### Path Parameters

| Name                                      | Type   | Description                              |
| ----------------------------------------- | ------ | ---------------------------------------- |
| env<mark style="color:red;">\*</mark>     | String | The backend environment \[dev, qa, prod] |

#### Query Parameters

| Name                                         | Type   | Description                                                     |
| -------------------------------------------- | ------ | --------------------------------------------------------------- |
| :reference<mark style="color:red;">\*</mark> | String | The reference received in the response when the link is created |

#### Headers

| Name                                        | Type   | Description                                    |
| ------------------------------------------- | ------ | ---------------------------------------------- |
| x-api-key<mark style="color:red;">\*</mark> | String | The API Key retrieved from the Merchant Portal |

{% tabs %}
{% tab title="200: OK Status of the transaction" %}
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
    "instalmentAmount": "750",
    "instalmentVisibility": "both",
    "contractReference": "Example Ref",
    "paymentReference": "Example Ref";
}
```
{% endtab %}
{% endtabs %}

### TT3 Transaction Response Descriptions:

| Field                | Description                                                                                    | Type                |
| -------------------- | ---------------------------------------------------------------------------------------------- | ------------------- |
| qrCodeState          | Status of the deeplink created                                                                 | String (64)         |
| transactionId        | ID of the transaction when created                                                             | String (UUID v4)    |
| status               | At what point the transaction is in the transaction flow (ResponseReceivedFromPaymentProvider) | String (64)         |
| disposition          | The outcome of the transaction (e.g. Approved)                                                 | String (32)         |
| currency             | Currency of the amount (e.g. ZAR, GBP)                                                         | String (3)          |
| type                 | The type of transaction (e.g. Tap, TT3, Secure card reader)                                    | String (32)         |
| responseCode         | The ISO response code of the transaction                                                       | Number              |
| authorisationCode    | Message Authorization Code (MAC)                                                               | String (MAC Length) |
| createdAt            | ISO date when the transaction was created                                                      |                     |
| updatedAt            | ISO date when the transaction was last updated                                                 |                     |
| collectionDay        | The day in which the debit order should be collected                                           | Number              |
| creditorABSN         | Name of Insurance Company                                                                      | String              |
| accountNumber        | Account number of the customer                                                                 | String              |
| idNumber             | ID number of the customer                                                                      | String (13)         |
| instalmentAmount     | Instalment amount of the Debit Order (e.g. 100.01)                                             | String              |
| instalmentVisibility | both, maximumOnly, instalmentOnly                                                              | Enum                |
| maxCollectionAmount  | The value of the debit order (100.01)                                                          | String              |
| contractReference    | Reference of the debicheck transaction provided by customer                                    | String (255)        |

<table><thead><tr><th width="374">QRCodeState</th><th>Description</th></tr></thead><tbody><tr><td>QRCodeGenerated</td><td>Initial call made to create the QR code/URL</td></tr><tr><td>QRCodeScanned</td><td>Device retrieves the transaction details that were provided when the QR code/URL was generated</td></tr><tr><td>TransactionStarted</td><td>Performed before reading the card, the device is ready to read card.</td></tr><tr><td>TransactionCreated</td><td>Card reading completed. Transaction has been sent to gateway.</td></tr><tr><td>ResponseReceivedByPhone (Definite Success)</td><td>The response from gateway is acknowledged by device.</td></tr></tbody></table>

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

#### Mapped ISO Response Codes

```kotlin
            "0" to "Approved or completed successfully",
            "1" to "Refer to card issuer",
            "2" to "Refer to card issuer's special conditions",
            "3" to "Invalid merchant",
            "4" to "Pick-Up",
            "5" to "Do not honor",
            "6" to "Error",
            "7" to "Pick-up card, special condition",
            "8" to "Honour with identification",
            "9" to "Request in progress",
            "10" to "Approved for partial amount",
            "11" to "Approved (VIP)",
            "12" to "Invalid transaction",
            "13" to "Invalid amount",
            "14" to "Invalid card number (no such number)",
            "15" to "No such issuer",
            "16" to "Approved, update track 3",
            "17" to "Customer cancellation",
            "18" to "Customer dispute",
            "19" to "Re-enter transaction",
            "20" to "Invalid response",
            "21" to "No action taken",
            "22" to "Suspected malfunction",
            "23" to "Unacceptable transaction fee",
            "24" to "File update not supported by receiver",
            "25" to "Unable to locate record on file",
            "26" to "Duplicate file update record, old record replaced",
            "27" to "File update field edit error",
            "28" to "File update file locked out",
            "29" to "File update not successful, contact acquirer",
            "30" to "Format error",
            "31" to "Bank not supported by switch",
            "32" to "Completed partially",
            "33" to "Expired card",
            "34" to "Suspected fraud",
            "35" to "Card acceptor contact acquirer",
            "36" to "Restricted card",
            "37" to "Card acceptor call acquirer security",
            "38" to "Allowable PIN tries exceeded",
            "39" to "No credit account",
            "40" to "Requested function not supported",
            "41" to "Lost card",
            "42" to "No universal account",
            "43" to "Stolen card, pick-up",
            "44" to "No investment account",
            "51" to "Not sufficient funds",
            "52" to "No checking account",
            "53" to "No savings account",
            "54" to "Expired Card",
            "55" to "Incorrect PIN",
            "56" to "No card record",
            "57" to "Transaction not permitted to cardholder",
            "58" to "Transaction not permitted to terminal",
            "59" to "Suspected fraud",
            "60" to "Card acceptor contact acquirer",
            "61" to "Exceeds withdrawal amount limit",
            "62" to "Restricted card",
            "63" to "Security violation",
            "64" to "Original amount incorrect",
            "65" to "Exceeds withdrawal frequency limit",
            "66" to "Card acceptor call acquirer's security department",
            "67" to "Hard capture (requires that card be picked up at ATM)",
            "68" to "Response received too late",
            "75" to "Allowable PIN tries exceeded",
            "90" to "Cutoff is in process (switch ending a day's business and starting the next. Transaction can be sent again in a few minutes)",
            "91" to "Issuer or switch is inoperative",
            "92" to "Financial institution or intermediate network facility cannot be found for routing",
            "93" to "Transaction cannot be completed. Violation of law",
            "94" to "Duplicate transmission",
            "95" to "Reconcile error",
            "96" to "System malfunction"

```

## Get Tap on Own Transaction Status

Get the status information of a tap on own transaction using the transaction's merchant reference.

<mark style="color:blue;">`GET`</mark> `https://kernelserver.{env}.haloplus.io/consumer/taponown/:merchantReference`

_**Let’s take a closer look at the API request.**_&#x20;

#### Path Parameters

| Name                                      | Type   | Description                              |
| ----------------------------------------- | ------ | ---------------------------------------- |
| env<mark style="color:red;">\*</mark>     | String | The backend environment \[dev, qa, prod] |

#### Query Parameters

| Name                                  | Type   | Description        |
| ------------------------------------- | ------ | ------------------ |
| :merchantReference<mark style="color:red;">\*</mark> | String | The merchant reference provided to the Halo.SDK when starting a transaction. |

#### Headers

| Name                                           | Type   | Description                                    |
| ---------------------------------------------- | ------ | ---------------------------------------------- |
| Authorization Bearer<mark style="color:red;">\*</mark> | String | The JWT received using the developer portal credentials (username and password) |

> Note: To obtain this token you may need to make a POST call to https://authserver.{env}.haloplus.io/login and use {username:your-username,password:your-password} as your json body.

{% tabs %}
{% tab title="200: OK Status" %}
```javascript
{
    "id": "693b47d8-e325-4808-8f86-67e388fd35ec",
    "merchantReference": "My-Unique-Transaction-Reference",
    "disposition": "Approved",
    "errorCode": 0
}
```
{% endtab %}
{% tab title="400: Bad Request"%}
```javascript
{
    "errorCode": 122,
    "message": "E122: Transaction not found. It may have not gone online yet.",
    "httpStatusCode": 400
}
```
{% endtab %}
{% tab title="500: Internal Error"%}
```javascript
{
    "errorCode": 201,
    "message": "Error finding requested transaction",
    "httpStatusCode": 500
}
```
{% endtab %}
{% endtabs %}

### Status Response Descriptions:
| Field | Description | Type |
| ---------------------------- | --------------------- | ---------------- |
| id | Halo backend transaction id | String (UUID) |
| merchantReference | Unique transaction reference provided by Halo.SDK integrating app. | String |
| disposition | <p>The outcome of the transaction (e.g. Approved)<br><br></p><p>There are 5 possible values for <code>disposition</code>​:</p><ul><li><code>Approved</code>​ - this means we got an approved message back from the processor </li><li><code>Declined</code>​ - this means we received a decline from the processor</li><li><code>UnableToGoOnline</code>​ - this means we couldn't connect to the processor. Essentially a decline, but it tells us the decline is due to a network error, and not a card issue</li><li><code>Indeterminate</code>​ - this means we either received an error from the processor or no response. This means we are unable to determine the status of the transaction. Typically, we treat these as declines and then we attempt to void the transaction in the background, in the event that the processor got the message but we just didn't get the response</li><li><code>Voided</code>​ - the transaction was reversed.</li></ul> | String (32) |
| errorCode | Halo backend error code| Number |
| message | Halo backend error message in the event of an error| String |

## Get Transaction Details

It is possible to get more information about a transaction asynchronously with an API Call to the Halo Backend.

_**Let’s take a closer look at the API request.**_&#x20;

<mark style="color:blue;">`GET`</mark> `https://kernelserver.{env}.haloplus.io/transactions/:id`

Asynchronously get details about transactions&#x20;

#### Path Parameters

| Name                                      | Type   | Description                              |
| ----------------------------------------- | ------ | ---------------------------------------- |
| env<mark style="color:red;">\*</mark>     | String | The backend environment \[dev, qa, prod] |

#### Query Parameters

| Name                                  | Type   | Description        |
| ------------------------------------- | ------ | ------------------ |
| :id<mark style="color:red;">\*</mark> | String | The Transaction ID |

#### Headers

| Name                                           | Type   | Description                                    |
| ---------------------------------------------- | ------ | ---------------------------------------------- |
| x-api-header<mark style="color:red;">\*</mark> | String | The API Key retrieved from the Merchant Portal |

{% tabs %}
{% tab title="200: OK Details of the transaction" %}
```json
{
    "id": "1d87e52a-ed08-4b5a-96c6-3f6942a1dc17",
    "passthroughUserId": null,
    "merchantTransactionReference": "17a42d8a-2717-45b6-95f7-7f4957e36c16",
    "dataRecord": "nwIGAAAAAQAAnwMGAAAAAAAAnyYIvmPeBfQYE4mCAhmAUApDT00wMiB2MSAwXzQBAZ82AgACnwcC/8CfCQIAAp8nAYCfNAMfAwKEB6AAAAAEMGCfHggwMkE0NjQ4M58QEgEQoAAPBAAAAAAAAAAAAAAA/58zAwAICJ8aAgcQnzUBIZUFAAAAgAFfKgIHEJoDIwYGnAEAnzcEAczRLA==",
    "details": [
        {
            "tags": [
                {
                    "tag": "9F1A",
                    "value": "0710"
                },
                {
                    "tag": "8C",
                    "value": "9F02069F03069F1A0295055F2A029A039C019F37049F35019F45029F4C089F34039F21039F7C14"
                },
                {
                    "tag": "8E",
                    "value": "000000000000000042031F03"
                },
                {
                    "tag": "8F",
                    "value": "F1"
                },
                {
                    "tag": "9F10",
                    "value": "0110A0000F040000000000000000000000FF"
                },
                {
                    "tag": "90",
                    "value": "39C18446D3EA015A4624C1C9E173D71FF2A515A50CD74E1D0DB840FE1679EF29911F9B47A273F74D711A0E5832B1D0663006F31274B056C2EC93BB5E1A7BCD4F79D947475D8644D37CFD475565BC58EDD19B6454682F6B8E70A80FF752F8C7F664747149B9A13CCF82BCBD74A3CAA176FE3F4BC1D5E08E7FEEDF2DEA063FD43FABEE5269722B24A5EAD869F46A9C3F8C92DE40EFCCC53BCCF0C03CDF7A2BDB98B5E348D7743944E9A894273DAD31FA4A"
                },
                {
                    "tag": "9F0E",
                    "value": "0000000000"
                },
                {
                    "tag": "FF8106",
                    "value": "9F42020840DF8115060000000000FFDF810E0100DF810F01009F6E200056010239390102030405060708090A0B0C0D0E0F101112131415161718191A"
                },
                {
                    "tag": "9F0F",
                    "value": "0000000000"
                },
                {
                    "tag": "94",
                    "value": "08010100100101011801010020010200"
                },
                {
                    "tag": "9F0D",
                    "value": "0000000000"
                },
                {
                    "tag": "95",
                    "value": "0000008001"
                },
                {
                    "tag": "9A",
                    "value": "230606"
                },
                {
                    "tag": "9F27",
                    "value": "80"
                },
                {
                    "tag": "9C",
                    "value": "00"
                },
                {
                    "tag": "9F26",
                    "value": "BE63DE05F4181389"
                },
                {
                    "tag": "9F21",
                    "value": "140406"
                },
                {
                    "tag": "9F1D",
                    "value": "4C00800000000000"
                },
                {
                    "tag": "DF8307",
                    "value": "00"
                },
                {
                    "tag": "9F1E",
                    "value": "3032413436343833"
                },
                {
                    "tag": "DF9E08",
                    "value": "80"
                },
                {
                    "tag": "9F39",
                    "value": "07"
                },
                {
                    "tag": "DF9E09",
                    "value": "57126799998900000074324D49122010123456785A0A6799998900000074324F5F24034912315F25031601015F280208405F3401018C279F02069F03069F1A0295055F2A029A039C019F37049F35019F45029F4C089F34039F21039F7C148D0C910A8A0295059F37049F4C088E0C000000000000000042031F039F0702FFC09F080200029F0D0500000000009F0E0500000000009F0F0500000000009F420208409F4A01821980"
                },
                {
                    "tag": "9F36",
                    "value": "0002"
                },
                {
                    "tag": "9F37",
                    "value": "01CCD12C"
                },
                {
                    "tag": "DF9E07",
                    "value": "999999999999"
                },
                {
                    "tag": "DF9E00",
                    "value": "80"
                },
                {
                    "tag": "DF9E01",
                    "value": "80"
                },
                {
                    "tag": "9F34",
                    "value": "1F0302"
                },
                {
                    "tag": "9F35",
                    "value": "21"
                },
                {
                    "tag": "9F32",
                    "value": "03"
                },
                {
                    "tag": "9F33",
                    "value": "000808"
                },
                {
                    "tag": "DF8136",
                    "value": "012C"
                },
                {
                    "tag": "9F4A",
                    "value": "82"
                },
                {
                    "tag": "DF8137",
                    "value": "32"
                },
                {
                    "tag": "9F4B",
                    "value": "3F47C7E108DE3DFB6A2D06B7267D562545333B3180C556E234AE3BC41365BF9BC3468C2E2812D364537FC9CBCFB65835EBEC8C66DD9105789CF5BF914C16CE821BF887032721AB35C223FBCA562DF3A72987E0E42F11F2B1565563A25F14D0AF"
                },
                {
                    "tag": "DF8134",
                    "value": "0012"
                },
                {
                    "tag": "DF8135",
                    "value": "0018"
                },
                {
                    "tag": "DF8132",
                    "value": "0014"
                },
                {
                    "tag": "DF8133",
                    "value": "0032"
                },
                {
                    "tag": "DF8130",
                    "value": "0D"
                },
                {
                    "tag": "9F4C",
                    "value": "BC0413ECA936A8F4"
                },
                {
                    "tag": "DF8131",
                    "value": "000001000001200000080000080020000004000004002000000100000100200000020000020020000000000000000700"
                },
                {
                    "tag": "9F47",
                    "value": "03"
                },
                {
                    "tag": "9F48",
                    "value": "0000000000000006600000000000000000000000000000000055"
                },
                {
                    "tag": "EF8105",
                    "value": "01"
                },
                {
                    "tag": "EF8104",
                    "value": "00"
                },
                {
                    "tag": "EF8103",
                    "value": "01"
                },
                {
                    "tag": "EF8102",
                    "value": "01"
                },
                {
                    "tag": "9F42",
                    "value": "0840"
                },
                {
                    "tag": "9F40",
                    "value": "6000C03001"
                },
                {
                    "tag": "DF812D",
                    "value": "000013"
                },
                {
                    "tag": "9F46",
                    "value": "39C3FC17136E58987D046155C4A50A6E6DD5ACEFDF19D2B3CA84F063043A960C36B8F5609303AADE7D973BD7D5C057087F74B65C18DDE826362FC20C754EE3D2274D11CB94E245AB5C7A259F57C3D63FDAA381670F591FB1A7F3B22195CFB4421633A30DF6E7901AC6309B3F64A6EA97"
                },
                {
                    "tag": "DF8129",
                    "value": "30F0F000B0F0FF00"
                },
                {
                    "tag": "DF8127",
                    "value": "01F4"
                },
                {
                    "tag": "DF8125",
                    "value": "999999999999"
                },
                {
                    "tag": "DF8126",
                    "value": "000000050000"
                },
                {
                    "tag": "DF8123",
                    "value": "000000000000"
                },
                {
                    "tag": "DF8124",
                    "value": "999999999999"
                },
                {
                    "tag": "DF8121",
                    "value": "0000800000"
                },
                {
                    "tag": "DF8122",
                    "value": "840000000C"
                },
                {
                    "tag": "DF8120",
                    "value": "840000000C"
                },
                {
                    "tag": "DF811F",
                    "value": "08"
                },
                {
                    "tag": "DF811B",
                    "value": "B0"
                },
                {
                    "tag": "4F",
                    "value": "A0000000043060"
                },
                {
                    "tag": "DF811A",
                    "value": "9F6A04"
                },
                {
                    "tag": "50",
                    "value": "434F4D30322076312030"
                },
                {
                    "tag": "DF8118",
                    "value": "40"
                },
                {
                    "tag": "DF8119",
                    "value": "08"
                },
                {
                    "tag": "DF8116",
                    "value": "1B000000000000000000000000000000000000000000"
                },
                {
                    "tag": "DF8117",
                    "value": "00"
                },
                {
                    "tag": "DF8114",
                    "value": "90"
                },
                {
                    "tag": "DF8115",
                    "value": "0000000000FF"
                },
                {
                    "tag": "9F6E",
                    "value": "0056010239390102030405060708090A0B0C0D0E0F101112131415161718191A"
                },
                {
                    "tag": "5F25",
                    "value": "160101"
                },
                {
                    "tag": "DF810E",
                    "value": "00"
                },
                {
                    "tag": "5F28",
                    "value": "0840"
                },
                {
                    "tag": "DF810F",
                    "value": "00"
                },
                {
                    "tag": "DF810C",
                    "value": "02"
                },
                {
                    "tag": "DF8107",
                    "value": "0000000100000000000000000710000000800107102306060001CCD12C21000000000000000000001F03021404060000000000000000000000000000000000000000"
                },
                {
                    "tag": "9F7E",
                    "value": "01"
                },
                {
                    "tag": "5F34",
                    "value": "01"
                },
                {
                    "tag": "5F2A",
                    "value": "0710"
                },
                {
                    "tag": "9F06",
                    "value": "A0000000043060"
                },
                {
                    "tag": "9F03",
                    "value": "000000000000"
                },
                {
                    "tag": "9F09",
                    "value": "0002"
                },
                {
                    "tag": "9F07",
                    "value": "FFC0"
                },
                {
                    "tag": "9F08",
                    "value": "0002"
                },
                {
                    "tag": "9F02",
                    "value": "000000010000"
                },
                {
                    "tag": "82",
                    "value": "1980"
                },
                {
                    "tag": "84",
                    "value": "A0000000043060"
                },
                {
                    "tag": "87",
                    "value": "03"
                }
            ],
            "maskedPAN": "679999*********4324",
            "encryptedV2": {
                "keyVersion": "ERqqMJM4mCAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
                "fingerprint": "",
                "encryptedCardData": "OVq8nqoXs4MQ+A+dSTzlnyxwDMc7t7mEs8tMJwspHZqCORQAOB3Gx9+RfM33tZqKiJQezpFC4+CvyC7TWF0UvQtEdN9IpPAFXfuETCQUyJcC/L8nY2oeCN/015Yqw6su2mpgW1JWfklcFiqx1vbYoF1R39BG2CrAV9XFozmm4fKzQ1M+FD7xsuwXgRO/4qaSFTkWg8Dg8DsqeRawfyaGRnR5mUOa4JWjbeBhZ9Bid5BNptLlwfXEilsnM0Qn1VYy/LwbvewJ4bZuQeJSbmaB52C8INnrswK65anS7fIZqkNQoCZ7CIjJ1FsF4ob30p8XippufuvI6ZmyvnsNsS5suA=="
            },
            "paymentProviderId": 100
        }
    ],
    "latitude": "-25.6921586",
    "longitude": "28.0414386",
    "deviceinstallationId": "F38BD0EA331F9CAAEEDF2C88BC41EED6",
    "transactionstatusId": 10,
    "transactionDispositionId": 0,
    "amount": "100",
    "currency": "ZAR",
    "responseCode": 0,
    "transactionTypeId": 1,
    "originalTransactionId": null,
    "acquirerId": 36,
    "userId": "216c55a5-0ae4-46ec-a217-3c865f58c401",
    "transactionFeesConfigId": null,
    "transactionFee": null,
    "authorisationCode": "00",
    "createdAt": "2023-06-06T12:04:14.247Z",
    "updatedAt": "2023-06-06T12:04:17.141Z",
    "receiptData": {
        "effectiveDate": "160101",
        "expiryDate": null,
        "authorizationCode": "00",
        "tid": "F38BD0EA331F9CAAEEDF2C88BC41EED6",
        "transactionReference": "1d87e52a-ed08-4b5a-96c6-3f6942a1dc17",
        "merchantName": "Fletcherville",
        "formattedMerchantAddress": "",
        "transactionType": "Tap",
        "approvalText": "Approved",
        "aid": "A0000000043060",
        "amount": "ZAR 100.00",
        "currency": "ZAR",
        "applicationLabel": "COM02 v1 0",
        "applicationPreferredName": null,
        "association": "Maestro Debit",
        "isoResponseCode": "0",
        "cryptogram": "BE63DE05F4181389",
        "cryptogramType": "ARQC",
        "tvr": "0000008001",
        "date": "2023/06/06",
        "time": "12:04",
        "maskedPan": "679999*********4324"
    }
}
```
{% endtab %}
{% endtabs %}

{% swagger src="../.gitbook/assets/swaggerDoc (2).yaml" path="/transactions/{transactionId}:" method="get" %}
[swaggerDoc (2).yaml](<../.gitbook/assets/swaggerDoc (2).yaml>)
{% endswagger %}

### Transaction Details Receipt Data:

