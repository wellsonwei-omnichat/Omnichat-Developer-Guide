---
title: Subscription Preparations
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
# Creating an Endpoint

You must first develop an API endpoint that supports two types of requests, one for endpoint validation and the other for event notifications. The endpoint should use the HTTPS protocol, so your server must be properly configured and have a valid SSL certificate installed (self-signed certificates are not supported).

## Endpoint Validation

Whenever you add a new webhook subscription in the Omnichat Admin Panel, Omnichat will send a **GET** request to your endpoint URL to validate the endpoint's validity. This request includes the following parameters appended to the endpoint URL:

| Parameter    | Example Value | Description                                 |
| :----------- | :------------ | :------------------------------------------ |
| verify_token | KRuk32ccaF    | The Verification Token you set up.          |
| challenge    | 3vU6S2ThsY    | A random string that you must return to us. |

### Request Example

Here is an example of the request to validate the endpoint:

```http HTTP
GET https://www.example.com/webhook?verify_token=KRuk32ccaF&challenge=3vU6S2ThsY
```

### Handling the Request

Each time your endpoint receives a validation request, you must perform the following logic:

* Confirm that the value of **verify_token** matches the one you've set.
* Return the value of **challenge** in the response body with **200 OK** status to us.

When Omnichat receives the **challenge** value and confirm that it matches the value at the time of the request, the subscription is considered successful; otherwise, it's a failure.

## Event Notifications

Whenever an event related to the topic you subscribed to occurs in the Omnichat system, it will send a data change object to your endpoint via a **POST** request. Different topics will have different data change objects; please refer to [Introduction to Topics](doc:introduction-to-topics).

### Request Header

When Omnichat sends each event notification, in addition to sending the data change object via the request body, it also includes some additional information in the request header.

| Parameter             | Example Value                                                    | Description                               |
| :-------------------- | :--------------------------------------------------------------- | :---------------------------------------- |
| User-Agent            | OmnichatWebhook/1.0                                              | A fixed value                             |
| X-Omnichat-Event-Id   | 6548e27f6dccad43685e3c93                                         | An unique identifier for the event        |
| X-Omnichat-Trace-Name | chat-api                                                         | Omnichat internal trace name              |
| X-Omnichat-Trace-Id   | 46e545ae-69a4-4a64-ad9d-076a64dd5962                             | Omnichat internal trace id                |
| X-Omnichat-Topic      | customer/update                                                  | Topic name                                |
| X-Omnichat-Timestamp  | 1699275390964                                                    | Event occurrence time                     |
| X-Omnichat-Team       | Omnichat                                                         | Your team name                            |
| X-Omnichat-Signature  | b82a35387b8d3de3c17cd4c68741dc437f76a4e26c9594726b2fb9852bcdf8e6 | Hmac-SHA256 signature of the request body |

### Request Example

For example, if you subscribed to the **customer/update** topic and there are any changes for a customer, you will receive a request like this:

```Text HTTP
POST / HTTPS/1.1
Host: www.example.com/webhook
Content-Type: application/json
Content-Length: 346
User-Agent: OmnichatWebhook/1.0
X-Omnichat-Trace-Name: chat-api
X-Omnichat-Trace-Id: 46e545ae-69a4-4a64-ad9d-076a64dd5962
X-Omnichat-Topic: customer/update
X-Omnichat-Timestamp: 1699275390964
X-Omnichat-Team: Easychat-2
X-Omnichat-Signature: b82a35387b8d3de3c17cd4c68741dc437f76a4e26c9594726b2fb9852bcdf8e6
X-Omnichat-Event-Id: 6548e27f6dccad43685e3c93

{"memberId":null,"email":"limitsea0103+100@gmail.com\n","phone":null,"name":"ChunChi 測試","tags":["web remarketing","jn"],"customAttributes":null,"socialContacts":[{"platform":"line","channelId":"1574311979","userId":"U6eb935d9805ccd03d5a0a4bbc8cf80e5"}],"createdAt":"2023-08-01T14:14:27.225+08:00","updatedAt":"2023-11-06T20:56:30.934+08:00"}
```

### Verifying Request Body

Omnichat will use the signature secret to sign a Hmac-SHA256 signature on all event notification request bodies and put it in the **X-Omnichat-Signature** header. You will obtain the signature secret after adding the webhook subscription in the Omnichat Admin Panel. Strongly recommend verifying the request body to prevent forged requests.

The verification steps are as follows:

1. Generate a Hex-encoded Hmac-SHA256 signature using the request body and webhook secret.

```javascript
const crypto = require('crypto');
const requestBody = '{{request-body}}';
const signatureSecret = '{{signature-secret}}';
const hmac = crypto.createHmac('sha256', signatureSecret);
hmac.update(requestBody);
const hash = hmac.digest('hex');
```

2. Compare your signature with the signature in the **X-Omnichat-Signature** header. If they match, the request is considered trustworthy.

### Responding to Requests

Your webhook endpoint should respond with **200 OK** to all event notification requests within **15 seconds** of receiving the request. If there is a timeout or a response other than **200 OK**, it will be considered a delivery failure.  Recommend responding immediately upon receiving the request.

### Automatic Disablement

When Omnichat detects that event notifications have consecutively failed more than 20 times or that over 10% of them have failed within an hour, it will automatically disable the webhook subscription for that endpoint.
