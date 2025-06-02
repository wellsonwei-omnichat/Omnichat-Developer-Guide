---
title: Usecases Sample
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
# API 1: Check Order Pickup

## Endpoint

POST https\://\{your-api-domain}/order-pickup-info

## Request Body

```json
{
  "orderId": "A0000001"
}
```

## Response Body

***

### Success Case

Return HTTP status 200 with the following body if orderId is valid.

```json
{
  "messages": [
    {
      "type": "text",
      "text": "訂單號碼: A0000001\nSMS發送日子: 2022-04-12 14:01\n取貨分店資料: Wong Tai Sin"
    }
  ]
}
```

***

### Failed Case

Return HTTP status 400 with empty body if orderId is invalid.

***

# API 2: Check Order Confirmation

## Endpoint

POST https\://\{your-api-domain}/order-confirmation-info

## Request body

```json
{
  "orderId": "A0000001"
}
```

## Response Body

***

### Success Case

Return HTTP status 200 with the following body if orderId is valid.

```json
{
  "messages": [
    {
      "type": "text",
      "text": "訂單號碼: A0000001\nSMS發送日子: 2022-04-12 14:01\n取貨分店資料: Wong Tai Sin"
    }
  ]
}
```

***

### Failed Case

Return HTTP status 400 with empty body if orderId is invalid.

***

# API 3: Request Change Pickup

## Endpoint

POST https\://\{your-api-domain}/change-pickup

## Request Body

```json
{
  "orderId": "A0000001"
}
```

## Response Body

***

### Success Case

Return HTTP status 200 with the following body if orderId is valid.

```json
{
  "messages": [
    {
      "type": "text",
      "text": "你好，抱歉，網購訂單不能更改提貨點。疫情關係，延遲提取網購商品，不會額外收取行政費。閣下盡快提貨或由他人憑網購單號代領即可。謝謝。"
    }
  ]
}
```

***

### Failed Case

Return HTTP status 400 with empty body if orderId is invalid.

***

# API 4: Check Order using Phone & Email

## Endpoint

POST https\://\{your-api-domain}/check-orders

## Request Body

```json
{
  "phone": "98765432",
  "email": "[example@example.com](mailto:example@example.com)"
}
```

## Response Body

***

### Success Case

Return HTTP status 200 with the following body if phone and email are valid.

```json
{
  "messages": [
    {
      "type": "text",
      "text": "訂單號碼: A0000001\nSMS發送日子: 2022-04-12 14:01\n取貨分店資料: Wong Tai Sin"
    }
  ]
}
```

***

### Failed Case

Return HTTP status 400 with empty body if phone or email is invalid.

***

# API 5: Check Inventory

## Endpoint

POST https\://\{your-api-domain}/check-inventory

## Request Body

```json
{
  "productCode": "111111111",
  "area": "香港區",
  "district": "北角區"
}
```

## Response Body

***

### Success Case

Return HTTP status 200 with the following body if product code, area and district are valid.

```json
{
  "messages": [
    {
      "type": "text",
      "text": "直至今日XX時，查詢之貨品庫存如下:\n中環堅道分店庫存為XX件；中源廣場分店 庫存為XX件；中環威靈頓街分店 庫存為XX件；\n由於商品庫存並非實時反映，店舖存貨因時不同，歡迎親臨分店選購及確認，敬請留意。 \n**如該分店的庫存為0件不需顯示**"
    }
  ]
}
```

***

### Failed Case

Return HTTP status 400 with empty body if product code or area or district is invalid.

***
