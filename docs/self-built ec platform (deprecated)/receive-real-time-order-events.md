---
title: Real-Time Orders
excerpt: How to send real-time order updates to Omnichat.
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Implementing Order Event Dispatch Logic

You will need to implement logic in your system to send order events to Omnichat whenever an order is created or updated.

## Order Event Types

There are two types of order events:  

### `order/create`

Use this event to send newly created orders. Omnichat will insert the order into our system.  
If the order number already exists, the event will be ignored and no updates will be made.

### `order/update`

Use this event to send updated order data. Omnichat will update the corresponding record in our system.  
If the order number does not exist, the event will be ignored and no record will be created.

> ⚠️ **Note:** If you are using Omnichat for the first time, please make sure to complete the **Order History Import** before sending update events.

## Webhook Specifications

To send an order event to Omnichat, make a **POST** request to the Omnichat **Webhook Endpoint**. The URL of this endpoint can be obtained from the Omnichat Admin Panel.

### Request Header

In addition to placing a single [**Order Object**](doc:order-object) as a JSON string in the request body, you must also include the **Webhook Token** and the **Order Event Type** in the request headers.

| Parameter     | Example Value     | Description                                                          |
| :------------ | :---------------- | :------------------------------------------------------------------- |
| Content-Type  | application/json  | Indicates that the request body is in JSON format                    |
| Authorization | Bearer Ajz3JArTKe | Place the Webhook Token obtained from the Omnichat Admin Panel       |
| X-EC-Event    | order/update      | Specifies the type of order event (`order/create` or `order/update`) |

### Request Example

Below is an example for sending an `order/update` event to the Omnichat `Webhook Endpoint`.