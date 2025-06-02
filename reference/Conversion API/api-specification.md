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

<https://api.omnichat.ai/restapi/v1/pixel/events>



# Authorization

Put your API access token in Authorization header using the Bearer schema.

`Authorization: Bearer {YOUR-API-TOKEN}`



# Request Method

POST



# Content Type

application/json



# Request Body

## Common Properties

The following properties are shared among all events and you should include these fields in all events

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Data Type",
    "h-2": "Required",
    "h-3": "Description",
    "h-4": "Example",
    "0-0": "action",
    "0-1": "String",
    "0-2": "Y",
    "0-3": "Event type. Available values:  \n-`pageview`  \n-`view_product`  \n-`add_to_cart`  \n-`remove_from_cart`  \n-`checkout`  \n-`purchase`",
    "0-4": "pageview",
    "1-0": "device",
    "1-1": "String",
    "1-2": "Y",
    "1-3": "Device type. Available values:  \n- `web`  \n- `ios`  \n- `android`",
    "1-4": "ios",
    "2-0": "memberId",
    "2-1": "String",
    "2-2": "N",
    "2-3": "Shop Member ID of the current user.  \nFor guests, please leave if empty.",
    "2-4": "12345",
    "3-0": "salesId",
    "3-1": "String",
    "3-2": "N",
    "3-3": "The sales tracking ID.  \nThis tracking ID is obtained from the “ocsaid” query parameter from the product referral tracking link / deeplink",
    "3-4": "49e27321-45c6-44d8-9ab7-9ae574c1307b:SHOP-A",
    "4-0": "utmSource",
    "4-1": "String",
    "4-2": "N",
    "4-3": "UTM Campaign Source",
    "4-4": "google",
    "5-0": "utmMedium",
    "5-1": "String",
    "5-2": "N",
    "5-3": "UTM Campaign Medium",
    "5-4": "cpc",
    "6-0": "utmCampaign",
    "6-1": "String",
    "6-2": "N",
    "6-3": "UTM Campaign Name",
    "6-4": "acquistion",
    "7-0": "utmTerm",
    "7-1": "String",
    "7-2": "N",
    "7-3": "UTM Term",
    "7-4": "running",
    "8-0": "utmContent",
    "8-1": "String",
    "8-2": "N",
    "8-3": "UTM content",
    "8-4": "textlink"
  },
  "cols": 5,
  "rows": 9,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]




## Common Object Types

### Product Object

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Data Type",
    "h-2": "Required",
    "h-3": "Description",
    "h-4": "Example",
    "0-0": "id",
    "0-1": "String",
    "0-2": "Y",
    "0-3": "Unique product ID / SKU",
    "0-4": "PD001",
    "1-0": "name",
    "1-1": "String",
    "1-2": "Y",
    "1-3": "Product Name",
    "1-4": "iPhone 12",
    "2-0": "brand",
    "2-1": "String",
    "2-2": "N",
    "2-3": "Product Brand",
    "2-4": "Apple",
    "3-0": "category",
    "3-1": "String",
    "3-2": "N",
    "3-3": "Product Category",
    "3-4": "Smart Phone",
    "4-0": "variant",
    "4-1": "String",
    "4-2": "N",
    "4-3": "Product Variant",
    "4-4": "Black",
    "5-0": "quantity",
    "5-1": "Integer",
    "5-2": "Y for action:  \n- `add_to_cart`  \n- `remove_from_cart`  \n- `checkout`  \n- `purchase`",
    "5-3": "Item Quantity",
    "5-4": "1",
    "6-0": "price",
    "6-1": "Number",
    "6-2": "N",
    "6-3": "Product Price",
    "6-4": "699.99"
  },
  "cols": 5,
  "rows": 7,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


For request sample, please refer to this Postman collection: <https://documenter.getpostman.com/view/6268933/TVzXCF5Y>



## Event 1: Pageview

> 📘 Only support device=web

Send this event when a customer visits any page of your website.

| Field Name  | Data Type | Required | Description                     | Example                    |
| :---------- | :-------- | :------- | :------------------------------ | :------------------------- |
| action      | String    | Y        | Set **pageview** for this event | pageview                   |
| url         | String    | Y        | Current website URL             | <https://your.website.com> |
| referrerUrl | String    | N        | Referrer URL                    | <https://your.website.com> |

### Example

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



## Event 2: View Product

Send this event when a customer view a product.

| Field Name | Data Type               | Required | Description                         | Example      |
| :--------- | :---------------------- | :------- | :---------------------------------- | :----------- |
| action     | String                  | Y        | Set **view_product** for this event | view_product |
| items      | Array of Product Object | Y        | Products viewed by the customer     |              |

### Example

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



## Event 3: Add to cart

Send this event when a customer adds products to the shopping cart.

| Field Name | Data Type               | Required | Description                                         | Example     |
| :--------- | :---------------------- | :------- | :-------------------------------------------------- | :---------- |
| action     | String                  | Y        | Set **add_to_cart** for this event                  | add_to_cart |
| items      | Array of Product Object | Y        | Products added to the shopping cart by the customer |             |

### Example

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



## Event 4: Remove from cart

Send this event when a customer removes products from the shopping cart.

| Field Name | Data Type               | Required | Description                                             | Example          |
| :--------- | :---------------------- | :------- | :------------------------------------------------------ | :--------------- |
| action     | String                  | Y        | Set **remove_from_cart** for this event                 | remove_from_cart |
| items      | Array of Product Object | Y        | Products removed from the shopping cart by the customer |                  |

### Example

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



## Event 5: Checkout

Send this event when a customer starts the checkout process.

| Field Name | Data Type               | Required | Description                       | Example  |
| :--------- | :---------------------- | :------- | :-------------------------------- | :------- |
| action     | String                  | Y        | Set **checkout** for this event   | checkout |
| items      | Array of Product Object | Y        | All products in the shopping cart |          |

### Example

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



## Event 6: Purchase

Send this event when a customer completed a purchase.

| Field Name    | Data Type               | Required | Description                       | Example    |
| :------------ | :---------------------- | :------- | :-------------------------------- | :--------- |
| action        | String                  | Y        | Set **purchase** for this event   | purchase   |
| transactionId | String                  | Y        | Transaction ID                    | TX20200001 |
| amount        | Number                  | Y        | Transaction total amount          | 1299.98    |
| currency      | String                  | Y        | Currency code (ISO 4217)          | HKD        |
| items         | Array of Product Object | N        | All products in the shopping cart |            |

### Example

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



## Event 7: Traffic Source

> 📘 Only support device=ios/android

| Field Name | Data Type | Required | Description                           | Example        |
| :--------- | :-------- | :------- | :------------------------------------ | :------------- |
| action     | String    | Y        | Set **traffic_source** for this event | traffic_source |

### Example

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



## Event 8: Member Mapping

> 📘 You must submit at least one of the following fields:
> 
> “memberId”, “memberEmail” or “memberPhone”

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Data Type",
    "h-2": "Required",
    "h-3": "Description",
    "h-4": "Example",
    "0-0": "member_mapping",
    "0-1": "String",
    "0-2": "Y",
    "0-3": "Set **member_mapping** for this event",
    "0-4": "member_mapping",
    "1-0": "memberEmail",
    "1-1": "String",
    "1-2": "N",
    "1-3": "Member Email",
    "1-4": "[example@example.com](mailto:example@example.com)",
    "2-0": "memberPhone",
    "2-1": "String",
    "2-2": "N",
    "2-3": "Member mobile phone number.  \nCountry code is mandatory.",
    "2-4": "85291234567",
    "3-0": "memberName",
    "3-1": "String",
    "3-2": "N",
    "3-3": "Member Name",
    "3-4": "Peter Chan",
    "4-0": "memberProfilePic",
    "4-1": "String",
    "4-2": "N",
    "4-3": "Member profile picture URL",
    "4-4": "<https://example.com/profile.jpg>"
  },
  "cols": 5,
  "rows": 5,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


### Example

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