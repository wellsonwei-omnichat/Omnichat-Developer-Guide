---
title: API Specification
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
# Endpoint

[https://api.omnichat.ai/restapi/v1/pixel/events](https://api.omnichat.ai/restapi/v1/pixel/events)

---

## Authorization

Put your API access token in the Authorization header using the Bearer schema.

```
Authorization: Bearer {YOUR-API-TOKEN}
```

---

## Request Method

**POST**

---

## Content Type

**application/json**

---

## Request Body

### Common Properties

The following properties are shared among all events, and you should include these fields in all events:

| Field Name  | Data Type | Required | Description                                                                                                                                       | Example                                      |
|-------------|-----------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|
| `action`    | String    | Y        | Event type. Available values: `pageview`, `view_product`, `add_to_cart`, `remove_from_cart`, `checkout`, `purchase`                                | `pageview`                                   |
| `device`    | String    | Y        | Device type. Available values: `web`, `ios`, `android`                                                                                           | `ios`                                        |
| `memberId`  | String    | N        | Shop Member ID of the current user. For guests, leave it empty.                                                                                   | `12345`                                      |
| `salesId`   | String    | N        | The sales tracking ID. This tracking ID is obtained from the `ocsaid` query parameter from the product referral tracking link / deeplink.         | `49e27321-45c6-44d8-9ab7-9ae574c1307b:SHOP-A` |
| `utmSource` | String    | N        | UTM Campaign Source                                                                                                                               | `google`                                     |
| `utmMedium` | String    | N        | UTM Campaign Medium                                                                                                                               | `cpc`                                        |
| `utmCampaign` | String  | N        | UTM Campaign Name                                                                                                                                 | `acquisition`                                |
| `utmTerm`   | String    | N        | UTM Term                                                                                                                                           | `running`                                    |
| `utmContent` | String   | N        | UTM Content                                                                                                                                       | `textlink`                                   |

---

### Common Object Types

#### Product Object

| Field Name  | Data Type | Required | Description                                                                                     | Example       |
|-------------|-----------|----------|-------------------------------------------------------------------------------------------------|---------------|
| `id`        | String    | Y        | Unique product ID / SKU                                                                         | `PD001`       |
| `name`      | String    | Y        | Product Name                                                                                    | `iPhone 12`   |
| `brand`     | String    | N        | Product Brand                                                                                   | `Apple`       |
| `category`  | String    | N        | Product Category                                                                                | `Smart Phone` |
| `variant`   | String    | N        | Product Variant                                                                                 | `Black`       |
| `quantity`  | Integer   | Y for actions: `add_to_cart`, `remove_from_cart`, `checkout`, `purchase`                                  | `1`           |
| `price`     | Number    | N        | Product Price                                                                                   | `699.99`      |

For request samples, please refer to this Postman collection: [https://documenter.getpostman.com/view/6268933/TVzXCF5Y](https://documenter.getpostman.com/view/6268933/TVzXCF5Y)

---

## Event 1: Pageview

> 📘 Only supports `device=web`.

Send this event when a customer visits any page of your website.

| Field Name  | Data Type | Required | Description                     | Example                    |
|-------------|-----------|----------|---------------------------------|----------------------------|
| `action`    | String    | Y        | Set **pageview** for this event | `pageview`                 |
| `url`       | String    | Y        | Current website URL             | [https://your.website.com](https://your.website.com) |
| `referrerUrl` | String  | N        | Referrer URL                    | [https://your.website.com](https://your.website.com) |

#### Example

```json
{
  "action": "pageview",
  "device": "web",
  "memberId": "12345",
  "salesId": "49e27321-45c6-44d8-9ab7-9ae574c1307b:SHOP-A",
  "url": "https://google.com",
  "referrerUrl": "https://google.com"
}
```

---

## Event 2: View Product

Send this event when a customer view a product.

| Field Name | Data Type               | Required | Description                         | Example      |
| :--------- | :---------------------- | :------- | :---------------------------------- | :----------- |
| `action`   | String                  | Y        | Set **view_product** for this event | view_product |
| `items`    | Array of Product Object | Y        | Products viewed by the customer     |              |

#### Example

```json
{
  "action": "view_product",
  "device": "ios",
  "memberId": "12345",
  "salesId": "49e27321-45c6-44d8-9ab7-9ae574c1307b:SHOP-A",
  "items": [
    {
      "id": "PD001",
      "price": 699.99,
      "name": "iPhone 12",
      "brand": "Apple",
      "category": "Smart Phone",
      "variant": "Black"
    }
  ]
}
```

---

## Event 3: Add to cart

Send this event when a customer adds products to the shopping cart.

| Field Name | Data Type               | Required | Description                                         | Example     |
| :--------- | :---------------------- | :------- | :-------------------------------------------------- | :---------- |
| `action`   | String                  | Y        | Set **add_to_cart** for this event                  | add_to_cart |
| `items`    | Array of Product Object | Y        | Products added to the shopping cart by the customer |             |

#### Example

```json
{
  "action": "add_to_cart",
  "device": "ios",
  "memberId": "12345",
  "salesId": "49e27321-45c6-44d8-9ab7-9ae574c1307b:SHOP-A",
  "items": [
    {
      "id": "PD001",
      "price": 699.99,
      "name": "iPhone 12",
      "brand": "Apple",
      "category": "Smart Phone",
      "variant": "Black 64",
      "quantity": 2
    },
    {
      "id": "PD002",
      "price": 599.99,
      "name": "iPhone 11",
      "brand": "Apple",
      "category": "Smart Phone",
      "variant": "Silver",
      "quantity": 1
    }
  ]
}
```

---

## Event 4: Remove from cart

Send this event when a customer removes products from the shopping cart.

| Field Name | Data Type               | Required | Description                                             | Example          |
| :--------- | :---------------------- | :------- | :------------------------------------------------------ | :--------------- |
| `action`   | String                  | Y        | Set **remove_from_cart** for this event                 | remove_from_cart |
| `items`    | Array of Product Object | Y        | Products removed from the shopping cart by the customer |                  |

#### Example

```json
{
  "action": "remove_from_cart",
  "device": "ios",
  "memberId": "12345",
  "salesId": "49e27321-45c6-44d8-9ab7-9ae574c1307b:SHOP-A",
  "items": [
    {
      "id": "PD001",
      "price": 699.99,
      "name": "iPhone 12",
      "brand": "Apple",
      "category": "Smart Phone",
      "variant": "Black 64",
      "quantity": 1
    }
  ]
}
```

---

## Event 5: Checkout

Send this event when a customer starts the checkout process.

| Field Name | Data Type               | Required | Description                       | Example  |
| :--------- | :---------------------- | :------- | :-------------------------------- | :------- |
| `action`   | String                  | Y        | Set **checkout** for this event   | checkout |
| `items`    | Array of Product Object | Y        | All products in the shopping cart |          |

#### Example

```json
{
  "action": "checkout",
  "device": "ios",
  "memberId": "12345",
  "salesId": "49e27321-45c6-44d8-9ab7-9ae574c1307b:SHOP-A",
  "items": [
    {
      "id": "PD001",
      "price": 699.99,
      "name": "iPhone 12",
      "brand": "Apple",
      "category": "Smart Phone",
      "variant": "Black 64",
      "quantity": 1
    },
    {
      "id": "PD002",
      "price": 599.99,
      "name": "iPhone 11",
      "brand": "Apple",
      "category": "Smart Phone",
      "variant": "Silver",
      "quantity": 1
    }
  ]
}
```

---

## Event 6: Purchase

Send this event when a customer completed a purchase.

| Field Name    | Data Type               | Required | Description                       | Example    |
| :------------ | :---------------------- | :------- | :-------------------------------- | :--------- |
| `action`      | String                  | Y        | Set **purchase** for this event   | purchase   |
| `transactionId` | String                | Y        | Transaction ID                    | TX20200001 |
| `amount`      | Number                  | Y        | Transaction total amount          | 1299.98    |
| `currency`    | String                  | Y        | Currency code (ISO 4217)          | HKD        |
| `items`       | Array of Product Object | N        | All products in the shopping cart |            |

#### Example

```json
{
  "action": "purchase",
  "device": "ios",
  "memberId": "12345",
  "salesId": "49e27321-45c6-44d8-9ab7-9ae574c1307b:SHOP-A",
  "transactionId": "TX20200001",
  "amount": 1299.98,
  "currency": "USD",
  "items": [
    {
      "id": "PD001",
      "price": 699.99,
      "name": "iPhone 12",
      "brand": "Apple",
      "category": "Smart Phone",
      "variant": "Black 64",
      "quantity": 1
    },
    {
      "id": "PD002",
      "price": 599.99,
      "name": "iPhone 11",
      "brand": "Apple",
      "category": "Smart Phone",
      "variant": "Silver",
      "quantity": 1
    }
  ]
}
```

---

## Event 7: Traffic Source

> 📘 Only supports `device=ios/android`.

| Field Name | Data Type | Required | Description                           | Example        |
| :--------- | :-------- | :------- | :------------------------------------ | :------------- |
| `action`   | String    | Y        | Set **traffic_source** for this event | traffic_source |

#### Example

```json
{
  "action": "traffic_source",
  "device": "web",
  "memberId": "12345",
  "salesId": "49e27321-45c6-44d8-9ab7-9ae574c1307b:SHOP-A",
  "utmSource": "omnichat",
  "utmMedium": "product_referral_whatsapp",
  "utmCampaign": "product_referral_abc"
}
```

---

## Event 8: Member Mapping

> 📘 You must submit at least one of the following fields:
> 
> “memberId”, “memberEmail” or “memberPhone”

| Field Name      | Data Type | Required | Description                                     | Example                    |
|-----------------|-----------|----------|-------------------------------------------------|----------------------------|
| `member_mapping`| String    | Y        | Set **member_mapping** for this event           | `member_mapping`           |
| `memberEmail`   | String    | N        | Member Email                                    | `example@example.com`      |
| `memberPhone`   | String    | N        | Member mobile phone number. Country code is mandatory. | `85291234567`             |
| `memberName`    | String    | N        | Member Name                                    | `Peter Chan`               |
| `memberProfilePic` | String | N        | Member profile picture URL                      | [https://example.com/profile.jpg](https://example.com/profile.jpg) |

#### Example

```json
{
  "action": "member_mapping",
  "device": "web",
  "memberId": "12345",
  "memberEmail": "example@example.com",
  "memberPhone": "85291234567",
  "memberName": "Peter Chan",
  "memberProfilePic": "https://example.com/profile.jpg"
}
```