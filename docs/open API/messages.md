---
title: Messages
deprecated: false
hidden: false
metadata:
  robots: index
---
# Messages

APIs for retrieving chat history and sending direct messages to contacts.

---

# Get Chat History

Get chat history messages by date range.

## Subscription Required

| Feature Toggle | Description |
|----------------|-------------|
| `open_api_crm` | CRM Open API Module - Required for retrieving chat history |

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/messages`

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
      <td>page</td>
      <td>Integer</td>
      <td>No</td>
      <td>Page number. Default: 1</td>
    </tr>
    <tr>
      <td>pageSize</td>
      <td>Integer</td>
      <td>No</td>
      <td>Number of messages per page. Default: 20, Max: 100</td>
    </tr>
    <tr>
      <td>after</td>
      <td>Long</td>
      <td>Yes</td>
      <td>Start of date range in unix timestamp (milliseconds), inclusive. Max date range: 7 days</td>
    </tr>
    <tr>
      <td>before</td>
      <td>Long</td>
      <td>Yes</td>
      <td>End of date range in unix timestamp (milliseconds), exclusive. Max date range: 7 days</td>
    </tr>
    <tr>
      <td>platform</td>
      <td>String</td>
      <td>Yes</td>
      <td>Messaging Platform. Values: `line`, `facebook`, `instagram`, `wechat`, `whatsapp`, `webchat`</td>
    </tr>
    <tr>
      <td>channelId</td>
      <td>String</td>
      <td>No</td>
      <td>Specific Messaging Platform Channel ID</td>
    </tr>
  </tbody>
</Table>

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | Array of `Message` Objects | Messages sent/received in the specific period |
| totalElements | Integer | Total number of messages |

### `Message` Object

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
      <td>channel</td>
      <td>`Channel` Object</td>
      <td>Messaging Channel of the message</td>
    </tr>
    <tr>
      <td>roomId</td>
      <td>String</td>
      <td>Chat Room ID</td>
    </tr>
    <tr>
      <td>customerUserId</td>
      <td>String</td>
      <td>Customer User ID</td>
    </tr>
    <tr>
      <td>id</td>
      <td>String</td>
      <td>Message ID</td>
    </tr>
    <tr>
      <td>senderType</td>
      <td>String</td>
      <td>Sender type. Values: `customer`, `agent`, `bot`</td>
    </tr>
    <tr>
      <td>senderName</td>
      <td>String</td>
      <td>Sender name</td>
    </tr>
    <tr>
      <td>senderUserId</td>
      <td>String</td>
      <td>Sender's User ID</td>
    </tr>
    <tr>
      <td>senderPhone</td>
      <td>String</td>
      <td>Sender's phone (for agent)</td>
    </tr>
    <tr>
      <td>senderEmail</td>
      <td>String</td>
      <td>Sender's email (for agent)</td>
    </tr>
    <tr>
      <td>time</td>
      <td>Long</td>
      <td>Message sent/received timestamp</td>
    </tr>
    <tr>
      <td>messageType</td>
      <td>String</td>
      <td>Message type. Values: `text`, `photo`, `audio`, `video`, `document`, `chatbot`</td>
    </tr>
    <tr>
      <td>messageStatus</td>
      <td>String</td>
      <td>Message status. Values: `sent`, `delivered`, `read`, `error`</td>
    </tr>
    <tr>
      <td>message</td>
      <td>String</td>
      <td>Message text content (Nullable)</td>
    </tr>
    <tr>
      <td>mediaUrl</td>
      <td>String</td>
      <td>Media file URL (Nullable)</td>
    </tr>
  </tbody>
</Table>

### `Channel` Object

| Field | Type | Description |
| :---- | :--- | :---------- |
| platform | String | Messaging Platform: `line`, `facebook`, `whatsapp`, `instagram`, `wechat`, `website` |
| channelId | String | Platform-specific Channel ID |

### Success Response - HTTP Status 200

```json
{
  "content": [
    {
      "channel": {
        "platform": "whatsapp",
        "channelId": "85290000001"
      },
      "id": "mid-1",
      "time": 1604647464032,
      "senderName": "Peter",
      "senderUserId": "85290000002",
      "senderPhone": "85290000002",
      "senderEmail": null,
      "senderType": "customer",
      "messageType": "text",
      "messageStatus": "delivered",
      "message": "hello",
      "mediaUrl": null,
      "roomId": "wh18695d48-5788-4d0a-a02c-9522a996258c-85290000002",
      "customerUserId": "85290000002"
    }
  ],
  "totalElements": 2301
}
```

---

# Get Message Details

Get message details by message ID.

## Subscription Required

| Feature Toggle | Description |
|----------------|-------------|
| `open_api_crm` | CRM Open API Module - Required for retrieving message details |

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/messages/{messageId}`

## Path Parameters

| Parameter | Type | Required | Description |
| :-------- | :--- | :------- | :---------- |
| messageId | String | Yes | Message ID |

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | `Message` Object | Message details |

### Success Response - HTTP Status 200

```json
{
  "content": {
    "channel": {
      "platform": "whatsapp",
      "channelId": "85290000001"
    },
    "id": "mid-1",
    "time": 1604647464032,
    "senderName": "Peter",
    "senderUserId": "85290000002",
    "senderPhone": "85290000002",
    "senderEmail": null,
    "senderType": "customer",
    "messageType": "text",
    "messageStatus": "delivered",
    "message": "hello",
    "mediaUrl": null,
    "roomId": "wh18695d48-5788-4d0a-a02c-9522a996258c-85290000002",
    "customerUserId": "85290000002"
  }
}
```

---

# Send Direct Message

Send a direct message to a single contact.

## Subscription Required

| Feature Toggle | Description |
|----------------|-------------|
| `open_api_marketing` | Marketing Open API Module - Required for sending direct messages |

## Endpoint

**POST** `https://open-api.omnichat.ai/v1/direct-messages`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |
| Content-Type | application/json | - |

## Request Body

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>Field</th>
      <th>Type</th>
      <th>Required</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>trackId</td>
      <td>String</td>
      <td>Yes</td>
      <td>Track ID for performance tracking</td>
    </tr>
    <tr>
      <td>platform</td>
      <td>String</td>
      <td>Yes</td>
      <td>Messaging Platform: `line`, `whatsapp` (facebook not yet supported)</td>
    </tr>
    <tr>
      <td>channelId</td>
      <td>String</td>
      <td>Yes</td>
      <td>Messaging Platform Channel ID</td>
    </tr>
    <tr>
      <td>to</td>
      <td>String</td>
      <td>Yes</td>
      <td>Contact's User ID</td>
    </tr>
    <tr>
      <td>tags</td>
      <td>Array of String</td>
      <td>No</td>
      <td>Tags to add after message sent successfully</td>
    </tr>
    <tr>
      <td>messages</td>
      <td>Array of `Message` Object</td>
      <td>Yes</td>
      <td>Messages to send. Max: 5 for text/image/products, 1 for block</td>
    </tr>
    <tr>
      <td>customAttributes</td>
      <td>Array of `Custom Attribute` Object</td>
      <td>No</td>
      <td>Custom attributes to set before sending</td>
    </tr>
  </tbody>
</Table>

### `Message` Object

| Field | Type | Description |
| :---- | :--- | :---------- |
| type | String | Message type (see platform-specific types below) |
| text | String | Required for type=text |
| image | String | Required for type=image (Image URL) |
| blockId | String | Required for type=block (Chatbot Message Block ID) |
| products | Array of `Product` Object | Required for type=products (Max 10 products) |
| whatsappTemplate | Object | Required for type=whatsappTemplate |
| lineFlexMessageTemplates | Array | Required for type=lineFlexMessageTemplates |

**Platform-specific message types:**

| Platform | Supported Types |
| :------- | :-------------- |
| LINE | `text`, `image`, `block`, `products`, `lineFlexMessageTemplates` |
| WhatsApp | `whatsappTemplate` |

### `Product` Object

| Field | Type | Required | Description |
| :---- | :--- | :------- | :---------- |
| name | String | Yes | Product Name |
| image | String | Yes | Product Image URL |
| url | String | Yes | Product Link URL |
| price | String | No | Product Price with currency |
| buttonLabel | String | Yes | CTA button text |

### Success Response - HTTP Status 200

```json
{
  "content": {
    "trackId": "remarketing-001",
    "messageId": [
      "wamid.HBgLODUyOTAzNTQ1MzMVAgARGBI3NEM2MUUwQkU4MTAxRkQxN0QA"
    ]
  }
}
```

### Error Codes

| Error Code | Description |
| :--------- | :---------- |
| INVALID_REQUEST_BODY | Invalid request body |
| CONTACT_UNSUBSCRIBED | Contact is unsubscribed |
| CONTACT_NOT_REACHABLE | Contact exceeded subscription plan limit |
| INTERNAL_SERVER_ERROR | Internal server error |
| UNEXPECTED_ERROR | Unexpected error |

## Examples

### Send Text + Image Message (LINE)

```json
{
  "trackId": "remarketing-001",
  "platform": "line",
  "channelId": "12345678",
  "to": "U1111111111111",
  "tags": ["remarking-001"],
  "messages": [
    { "type": "text", "text": "Final Sale Message 1" },
    { "type": "text", "text": "Final Sale Message 2" },
    { "type": "image", "image": "https://example.com/image.png" }
  ]
}
```

### Send Chatbot Block Message

```json
{
  "trackId": "remarketing-001",
  "platform": "line",
  "channelId": "12345678",
  "to": "U1111111111111",
  "messages": [
    { "type": "block", "blockId": "07269d7a-68d6-4f36-9c0b-c837d9b296ef" }
  ]
}
```

### Send WhatsApp Template Message

```json
{
  "trackId": "cny2023",
  "platform": "whatsapp",
  "channelId": "85290000001",
  "to": "85260000001",
  "messages": [
    {
      "type": "whatsappTemplate",
      "whatsappTemplate": {
        "name": "cny_campaign_2023",
        "components": [
          {
            "type": "header",
            "parameters": [
              { "type": "image", "image": { "link": "https://example.com/red-pocket.png" } }
            ]
          },
          {
            "type": "body",
            "parameters": [
              { "type": "text", "text": "Mr. Chan" },
              { "type": "text", "text": "$100 Red pocket" }
            ]
          }
        ]
      }
    }
  ]
}
```
