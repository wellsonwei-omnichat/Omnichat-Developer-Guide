---
title: Order History Import
excerpt: Guide to providing historical order data to Omnichat.
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: receive-real-time-order-events
      title: Real-Time Orders
---
# Implementing the Order History API

A **GET /orders** endpoint should be provided to allow Omnichat to retrieve your order history. Omnichat supports importing up to **1 million** orders. The import process will automatically stop once this limit is reached.

You may choose to implement offset-based or cursor-based pagination, depending on your system architecture and performance considerations. In addition, please ensure that the access token configured in the Omnichat Admin Panel is properly validated in your API.

The following are implementation guidelines and examples for reference.

## Request Query Parameters

### Offset-based pagination

| Parameter  | Description                                              |
| :--------- | :------------------------------------------------------- |
| pageSize   | Number of orders per page (Maximum allowed value: 1,000) |
| pageNumber | Index of the page to retrieve (Starting from 1)          |

### Cursor-based pagination

| Parameter | Description                                                                     |
| :-------- | :------------------------------------------------------------------------------ |
| pageSize  | Number of orders per page (Maximum allowed value: 1,000)                        |
| pageToken | Token that identifies the page of results to retrieve (null for the first page) |

## Request Example

```http
GET /orders?pageNumber=1&pageSize=1000 HTTPS/1.1
Host: www.your-domain-name.com
User-Agent: OmnichatOrderSync/1.0
X-Omnichat-Team: 69629324-b39c-4ca9-8d9d-e92485c185be
X-Omnichat-Job-Id: 33e2e142-8fb1-49d2-991f-96fb1721afed
Authorization: Bearer {{your_access_token}}
```

## Response Body Fields

### Offset-based pagination

| Field         | Description                                              |
| :------------ | :------------------------------------------------------- |
| content       | Array of [**Order Objects**](doc:order-object)           |
| pageSize      | Number of orders per page (Maximum allowed value: 1,000) |
| pageNumber    | Current page number                                      |
| totalPages    | Total Number of pages (Maximum allowed value: 1,000)     |
| totalElements | Total Number of orders                                   |

### Cursor-based pagination

| Field         | Description                                                 |
| :------------ | :---------------------------------------------------------- |
| content       | Array of [**Order Objects**](doc:order-object)              |
| pageSize      | Number of orders per page (Maximum allowed value: 1,000)    |
| nextPageToken | Token to be used to fetch the next page (null if last page) |

## Response Body Example

```json
{
  "content": [
    {
      "orderId": "ORD12345678",
      "orderDate": "2025-04-11T14:30:00Z",
      "orderAmount": "$142.48",
      "orderStatus": "Shipped",
      "paymentMethod": "Credit Card",
      "paymentStatus": "Paid",
      "deliveryMethod": "Home Delivery",
      "deliveryInfo": "Jane Doe, 123 Main St, Springfield, IL, 62704, USA, +1-555-1234",
      "deliveryStatus": "In Transit",
      "deliveryFee": "$5.00",
      "deliveryTrackingNumber": "TRACK123456789",
      "items": [
        {
          "title": "Wireless Mouse",
          "quantity": 2,
          "price": "$15.99"
        },
        {
          "title": "Mechanical Keyboard",
          "quantity": 1,
          "price": "$89.50"
        }
      ],
      "totalItemsAmount": "$121.48",
      "orderDiscount": "$10.00",
      "totalTaxFee": "$6.00"
    }
  ],
  "pageNumber": 1,
  "pageSize": 1000,
  "totalPages": 1,
  "totalElements": 1
}
```
