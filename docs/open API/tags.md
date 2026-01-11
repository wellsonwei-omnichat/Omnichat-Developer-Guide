---
title: Tags
deprecated: false
hidden: false
metadata:
  robots: index
---
# Tags

APIs for retrieving tagging log records.

## Subscription Required

| Feature Toggle | Description |
|----------------|-------------|
| `open_api` | Open API Module - Required for retrieving tagging logs |

---

# Get Tagging Log Records

Get tagging log records by specific date range.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/tagging-logs/records`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |

## Query Parameters

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Type</th>
      <th>Required</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>taggedAfter</td>
      <td>Long</td>
      <td>Yes</td>
      <td>Start of date range in unix timestamp (milliseconds), inclusive</td>
    </tr>
    <tr>
      <td>taggedBefore</td>
      <td>Long</td>
      <td>Yes</td>
      <td>End of date range in unix timestamp (milliseconds), exclusive</td>
    </tr>
    <tr>
      <td>page</td>
      <td>Integer</td>
      <td>No</td>
      <td>Page number. Default: 1</td>
    </tr>
    <tr>
      <td>pageSize</td>
      <td>Integer</td>
      <td>No</td>
      <td>Page size. Default: 20</td>
    </tr>
  </tbody>
</Table>

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | Array of `TaggingLog` Object | Tagging log records |
| totalElements | Integer | Total number of records |

### `TaggingLog` Object

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>Field</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>time</td>
      <td>String</td>
      <td>Time when tagging happened (ISO format)</td>
    </tr>
    <tr>
      <td>platform</td>
      <td>String</td>
      <td>Messaging platform: `line`, `facebook`, `whatsapp`, `instagram`, `wechat`, `webchat`</td>
    </tr>
    <tr>
      <td>channelId</td>
      <td>String</td>
      <td>Channel ID</td>
    </tr>
    <tr>
      <td>userId</td>
      <td>String</td>
      <td>Contact's User ID</td>
    </tr>
    <tr>
      <td>tag</td>
      <td>String</td>
      <td>Tag added to contact</td>
    </tr>
    <tr>
      <td>source</td>
      <td>String</td>
      <td>Source of tagging (see below)</td>
    </tr>
    <tr>
      <td>messageId</td>
      <td>String</td>
      <td>Related message ID</td>
    </tr>
  </tbody>
</Table>

### Tagging Sources

| Source | Description |
| :----- | :---------- |
| bot | Chatbot |
| broadcast | Broadcast message |
| manual | Manual tagging |
| import | Data import |
| keyword_auto_reply | Keyword auto-reply |
| open_api | Open API |
| game | Game |
| abandoned_cart | Abandoned cart |
| remarketing | Remarketing |
| product_referral | Product referral |
| journey | Customer journey |
| line_rich_menu | LINE Rich Menu |
| third_party_system | Third-party system |
| coupon | Coupon |
| cross_channel_connector | Cross-channel connector |
| phone_binding | Phone binding |
| survey_cake | SurveyCake |
| social_channel_mapping | Social channel mapping |
| chatbot_button | Chatbot button |
| add_cart | Add to cart |

### Success Response - HTTP Status 200

```json
{
  "content": [
    {
      "time": "2023-01-03T12:32:12",
      "platform": "whatsapp",
      "channelId": "85211111111",
      "userId": "85222222222",
      "tag": "subscribed",
      "source": "bot",
      "messageId": "wamid.123213123123"
    }
  ],
  "totalElements": 1
}
```

### Error Response - HTTP Status 4xx / 5xx

```json
{
  "errorCode": "INVALID_REQUEST_BODY",
  "message": "Invalid request body"
}
```
