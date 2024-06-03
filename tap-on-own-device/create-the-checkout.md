---
description: >-
  Simply integrate with our Tap on Own Device API library and your customers can
  pay by tapping their own card or digital wallet on their own device!
---

# Create the Checkout

{% hint style="info" %}
**CAUTION**

The Tap on Own Device APIs should only be called from your server. This flow ensures the security of your payments and provides a trusted result to your server.
{% endhint %}

## Steps

1. [Create the Checkout](create-the-checkout.md#id-1.-create-the-checkout)
   * Display QR code
2. [Verify the payment is successful](create-the-checkout.md#id-2.-verify-that-the-payment-is-successful)

### 1. Create the Checkout

The Checkout API requires authenticated access, see [here](../api-docs/authentication.md) for more details.

A Checkout represents what your customer sees on the payment page, including the amount to collect, currency, and any other additional details. This interface displays the available checkout methods. For example, one of the checkout methods could be "Pay Contactless." To enable this, you would add an endpoint behind an action (such as a button) that creates the Tap on Own transaction request.

### Deeplink Transaction <a href="#deeplink-transaction" id="deeplink-transaction"></a>

<pre><code><a data-footnote-ref href="#user-content-fn-1">POST https://kernelserver.prod.haloplus.io/consumer/qrCode</a>
</code></pre>

The call to the Halo Dot Backend to retrieve a Transaction URL .

**Path Parameters**

| Name  | Type   | Description                              |
| ----- | ------ | ---------------------------------------- |
| env\* | String | The backend environment \[dev, qa, prod] |

**Headers**

| Name           | Type   | Description                                    |
| -------------- | ------ | ---------------------------------------------- |
| Content-Type\* | String | Content Type of the Request: application/json  |
| x-api-key\*    | String | The API Key retrieved from the Merchant Portal |

**Request Body**

| Name               | Type    | Description                                             |
| ------------------ | ------- | ------------------------------------------------------- |
| merchantId\*       | String  | Merchant ID from Merchant Portal                        |
| paymentReference\* | String  | Reference of the transaction                            |
| amount\*           | String  | Amount of the transaction (e.g. 100.01)                 |
| timestamp\*        | String  | ISO Standard Timestamp                                  |
| currencyCode\*     | String  | ISO Standard Currency Codes                             |
| isConsumerApp\*    | Boolean | Indicate if the call is for a Consumer App              |
| image\*            | JSON    | Set to true to generate a QR code - {"required": false} |

```json
{
    "merchantId" : "{Your MID}", 
    "paymentReference": "",
    "amount": 5, 
    "timestamp": "Thu Aug 25 09:43:59 SAST 2022", 
    "currencyCode": "ZAR",
    "isConsumerApp": false,
    "image": {
        "required": false
    }
}
```

**Sample response**

The deeplink transaction response contains a URL used to either redirect the customer to the tap screen if the transaction is occurring on the same device, or to display a QR code if the transaction is made on a different device. The URL is embedded in the QR code, and when scanned, it invokes the application to prompt the card tap.

200: OK URL to invoke the Halo Dot Application for a payment

```
{
    "url": "https://halompos.page.link/DYfL4EZEzvAzBfBAS",
    "reference": "c9e1were-8156-444c-894d-e065d71366a6"
}
```

### 2. Verify that the payment is Successful

When a payment is successful, we will send a webhook event to the url provided. It is highly recommended to use webhooks to check the payment status before fulfilling the order.

For more information on receiving webhook events, see here.

The status of the payment can be verified by referring to the `disposition` field of the webhook event. A payment is considered successful if its `disposition` is marked as `approved.`



[^1]: 
