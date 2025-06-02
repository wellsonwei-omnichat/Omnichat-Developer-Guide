---
title: Order Object
excerpt: Definition of the data structure used for each order.
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
      slug: sync-order-history-data
      title: Order History Import
---
# Order Fields

| Field                  | Description                                                                             |
| :--------------------- | :-------------------------------------------------------------------------------------- |
| orderId                | Internal unique identifier for the order                                                |
| orderName              | Order number displayed on the page (e.g., for customer reference)                       |
| orderDate              | Date and time when the order was placed, in ISO-8601 format (e.g., 2025-04-11T15:30:00) |
| orderAmount            | Total amount of the order including items, tax, and delivery fees                       |
| orderCurrency          | Currency code in string format combining ISO 4217 code and symbol (e.g., USD$, SGD$)    |
| orderStatus            | Current status of the order (e.g., Processing, Shipped, Completed, Canceled)            |
| paymentMethod          | Payment method used for the order (e.g., Credit Card, PayPal, Cash on Delivery)         |
| paymentStatus          | Status of the payment (e.g., Paid, Pending, Failed)                                     |
| paymentFee             | Any additional fee charged for the selected payment method (if applicable)              |
| deliveryMethod         | Delivery method selected for the order (e.g., Home Delivery, Store Pickup)              |
| deliveryInfo           | Delivery details including recipient, address, and contact information                  |
| deliveryStatus         | Current delivery status (e.g., Pending, In Transit, Delivered)                          |
| deliveryFee            | Cost of delivery for the order                                                          |
| deliveryTrackingNumber | Tracking number provided by the delivery service (if available)                         |
| items                  | List of items included in the order                                                     |
| totalItemsAmount       | Subtotal amount for all items before discounts, tax, and delivery fees                  |
| orderDiscount          | Total discount applied to the order (e.g., coupons, promotions)                         |
| totalTaxFee            | Total tax applied to the order                                                          |

## Item Fields

| Field     | Description                                                  |
| :-------- | :----------------------------------------------------------- |
| productId | Unique identifier of the product                             |
| name      | Name or title of the item being ordered                      |
| brand     | Brand of the product                                         |
| category  | Category or classification the product belongs to            |
| variant   | Specific variation of the product (e.g., size, color, model) |
| quantity  | Number of units of the item in the order                     |
| price     | Price per unit of the item (before tax and discounts)        |
