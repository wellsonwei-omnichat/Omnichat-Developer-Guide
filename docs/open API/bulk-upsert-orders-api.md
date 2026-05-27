---
title: Bulk Upsert Orders API
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Request

## Endpoint

**PUT** [https://open-api.omnichat.ai/v1/third-party-orders](https://open-api.omnichat.ai/v1/third-party-orders)

## Request body

| Field  | Type                   | Required | Description                |
| :----- | :--------------------- | :------- | :------------------------- |
| orders | Array of Order Objects | Y        | Orders to insert or update |

### Order Object

| Field                  | Type                  | Required | Description                                                                              |
| :--------------------- | :-------------------- | :------- | :--------------------------------------------------------------------------------------- |
| memberId               | String                | Y        | Unique identifier of the customer                                                        |
| orderId                | String                | Y        | Internal primary key (PK) of the order used by the system                                |
| orderName              | String                | Y        | Order number displayed on the page (e.g., for customer reference)                        |
| orderDate              | String                | Y        | Date and time when the order was placed, in ISO-8601 format (e.g., 2025-04-11T15:30:00)  |
| orderAmount            | Float                 | Y        | Total amount of the order including items, tax, and delivery fees                        |
| orderCurrency          | String                | Y        | Currency code in string format combining ISO 4217 code and symbol (e.g., `USD$`, `SGD$`) |
| orderStatus            | String                | Y        | Current status of the order (e.g., Processing, Shipped, Completed, Canceled)             |
| paymentMethod          | String                | N        | Payment method used for the order (e.g., Credit Card, PayPal, Cash on Delivery)          |
| paymentStatus          | String                | Y        | Status of the payment (e.g., Paid, Pending, Failed)                                      |
| paymentFee             | Float                 | N        | Any additional fee charged for the selected payment method (if applicable)               |
| deliveryMethod         | String                | N        | Delivery method selected for the order (e.g., Home Delivery, Store Pickup)               |
| deliveryInfo           | String                | N        | Delivery details including recipient, address, and contact information                   |
| deliveryStatus         | String                | N        | Current delivery status (e.g., Pending, In Transit, Delivered)                           |
| deliveryFee            | Float                 | N        | Cost of delivery for the order                                                           |
| deliveryTrackingNumber | String                | N        | Tracking number provided by the delivery service (if available)                          |
| items                  | Array of Item Objects | Y        | List of items included in the order                                                      |
| totalItemsAmount       | Float                 | N        | Subtotal amount for all items before discounts, tax, and delivery fees                   |
| orderDiscount          | Float                 | N        | Total discount applied to the order (e.g., coupons, promotions)                          |
| totalTaxFee            | Float                 | N        | Total tax applied to the order                                                           |

### Item Object

| Field     | Type    | Required | Description                                                  |
| :-------- | :------ | :------- | :----------------------------------------------------------- |
| productId | String  | Y        | Unique identifier of the product                             |
| name      | String  | Y        | Name or title of the item being ordered                      |
| brand     | String  | N        | Brand of the product                                         |
| category  | String  | N        | Category or classification the product belongs to            |
| variant   | String  | N        | Specific variation of the product (e.g., size, color, model) |
| quantity  | Integer | Y        | Number of units of the item in the order                     |
| price     | Float   | Y        | Price per unit of the item (before tax and discounts)        |

## Request body example

```json
{
  "orders": [
    {
      "memberId": "member-123",
      "orderId": "order-001",
      "orderName": "#10001",
      "orderDate": "2025-04-11T15:30:00",
      "orderAmount": 299.99,
      "orderCurrency": "USD$",
      "orderStatus": "Completed",
      "paymentMethod": "Credit Card",
      "paymentStatus": "Paid",
      "paymentFee": 5.00,
      "deliveryMethod": "Home Delivery",
      "deliveryInfo": "Recipient: John Smith, Address: 123 Main St, New York, NY 10001",
      "deliveryStatus": "Delivered",
      "deliveryFee": 15.00,
      "deliveryTrackingNumber": "TRACK123456",
      "items": [
        {
          "productId": "prod-001",
          "name": "Sports T-Shirt",
          "brand": "Nike",
          "category": "Apparel",
          "variant": "Blue-L",
          "quantity": 2,
          "price": 49.99
        },
        {
          "productId": "prod-002",
          "name": "Running Shorts",
          "brand": "Nike",
          "category": "Apparel",
          "variant": "Black-M",
          "quantity": 1,
          "price": 39.99
        }
      ],
      "totalItemsAmount": 139.97,
      "orderDiscount": 10.00,
      "totalTaxFee": 12.60
    }
  ]
}
```

# Response

## Response body

| Field   | Type   | Description              |
| :------ | :----- | :----------------------- |
| content | Object | Response content wrapper |

### Content Object

| Field         | Type    | Description                                                                      |
| :------------ | :------ | :------------------------------------------------------------------------------- |
| matchedCount  | Integer | Number of orders found using `orderId` that match the query criteria             |
| modifiedCount | Integer | Number of orders found using `orderId` that were modified (content updated)      |
| insertedCount | Integer | Number of new orders inserted because no existing order was found with `orderId` |

## Response body example

```json
{
  "content": {
    "matchedCount": 0,
    "modifiedCount": 0,
    "insertedCount": 1
  }
}
```

<br />
