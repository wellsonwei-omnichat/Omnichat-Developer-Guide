---
title: Broadcast APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
# Broadcast APIs

APIs for sending and managing broadcast messages.

## Subscription Required

| Feature Toggle | Description |
|----------------|-------------|
| `open_api_marketing` | Marketing Open API Module - Required for all Broadcast endpoints |

---

# Send Broadcast

Send broadcast messages to multiple recipients.

## Endpoint

**POST** `https://open-api.omnichat.ai/v1/broadcast`

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
      <td>platform</td>
      <td>String</td>
      <td>Yes</td>
      <td>Messaging platform. Supported values: `line`, `whatsapp`</td>
    </tr>
    <tr>
      <td>channelId</td>
      <td>String</td>
      <td>Yes</td>
      <td>Channel identifier</td>
    </tr>
    <tr>
      <td>subject</td>
      <td>String</td>
      <td>Yes</td>
      <td>Broadcast subject</td>
    </tr>
    <tr>
      <td>to</td>
      <td>Array of String</td>
      <td>Yes</td>
      <td>Recipient identifiers (Max: 150)</td>
    </tr>
    <tr>
      <td>messages</td>
      <td>Array of Message</td>
      <td>Yes</td>
      <td>Broadcast message objects</td>
    </tr>
    <tr>
      <td>tags</td>
      <td>Array of String</td>
      <td>No</td>
      <td>Tags to add when broadcasting</td>
    </tr>
    <tr>
      <td>scheduledAt</td>
      <td>String</td>
      <td>No</td>
      <td>ISO-8601 datetime. If null, send immediately</td>
    </tr>
  </tbody>
</Table>

### Message Object

| Field | Type | Required | Description |
| :---- | :--- | :------- | :---------- |
| type | String | Yes | Message type: `text`, `image`, `block`, `whatsappTemplate` |
| text | String | Conditional | Text content (required for `text` type). Max 5 text messages |
| blockId | String | Conditional | Chatbot block ID (required for `block` type). Max 1 block message |
| whatsappTemplate | Object | Conditional | WhatsApp template (required for `whatsappTemplate` type). Max 1 template message |

### WhatsApp Template Object

| Field | Type | Required | Description |
| :---- | :--- | :------- | :---------- |
| namespace | String | Yes | Template namespace |
| name | String | Yes | Template name |
| components | Object | Yes | Template components |

## Request Example

```json
{
  "platform": "line",
  "channelId": "1657703186",
  "subject": "Promotion Campaign",
  "to": ["U2bd582c37356d37cb6d46a823de3a908", "U2bd582c37356d37cb6d46a823de3a909"],
  "messages": [
    {
      "type": "text",
      "text": "Hello! Check out our new promotion!"
    }
  ],
  "tags": ["promotion", "campaign"]
}
```

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| broadcastId | String | Broadcast identifier |

### Success Response - HTTP Status 200

```json
{
  "broadcastId": "67890abcdef12345"
}
```

### Failed Response - HTTP Status 4xx / 5xx

```json
{
  "errorCode": "INVALID_BROADCAST_MESSAGE",
  "message": "There is more than one type in the list of messages."
}
```

---

# Get Broadcast List

Query broadcast jobs with aggregate statistics.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/broadcast`

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
      <td>type</td>
      <td>String</td>
      <td>Yes</td>
      <td>Broadcast job type. Values: `1` (Broadcast), `3` (Open API)</td>
    </tr>
    <tr>
      <td>platform</td>
      <td>String</td>
      <td>No</td>
      <td>Messaging platform. Values: `facebook`, `line`, `whatsapp`</td>
    </tr>
    <tr>
      <td>channelId</td>
      <td>String</td>
      <td>No</td>
      <td>Channel ID</td>
    </tr>
    <tr>
      <td>status</td>
      <td>String</td>
      <td>No</td>
      <td>Status filter. Values: `pending`, `scheduled`, `processing`, `completed`, `canceled`, `failed`</td>
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
      <td>Page size (1-100). Default: 10</td>
    </tr>
  </tbody>
</Table>

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | Array of Broadcast | List of broadcast jobs |
| totalElements | Integer | Total number of records |

### Broadcast Object

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
      <td>id</td>
      <td>String</td>
      <td>Broadcast ID</td>
    </tr>
    <tr>
      <td>platform</td>
      <td>String</td>
      <td>Messaging platform: `facebook`, `line`, `whatsapp`</td>
    </tr>
    <tr>
      <td>channelId</td>
      <td>String</td>
      <td>Channel ID</td>
    </tr>
    <tr>
      <td>channelName</td>
      <td>String</td>
      <td>Channel name</td>
    </tr>
    <tr>
      <td>subject</td>
      <td>String</td>
      <td>Broadcast subject</td>
    </tr>
    <tr>
      <td>recipientType</td>
      <td>Integer</td>
      <td>1: Custom filter, 2: CSV list, 3: Open API, 4: Segment</td>
    </tr>
    <tr>
      <td>type</td>
      <td>Integer</td>
      <td>1: Broadcast, 2: Mass message, 3: Open API Broadcast</td>
    </tr>
    <tr>
      <td>mode</td>
      <td>String</td>
      <td>Recipient filter mode: `filter`, `manual`, `csv`</td>
    </tr>
    <tr>
      <td>sentAt</td>
      <td>String</td>
      <td>Sent time (ISO8601 format)</td>
    </tr>
    <tr>
      <td>status</td>
      <td>Integer</td>
      <td>0: pending, 1: completed, 2: processing, 3: canceled, 4: scheduled, 9: failed</td>
    </tr>
    <tr>
      <td>recipientCount</td>
      <td>Integer</td>
      <td>Total recipients</td>
    </tr>
    <tr>
      <td>success</td>
      <td>Integer</td>
      <td>Successful sent count</td>
    </tr>
    <tr>
      <td>successRate</td>
      <td>String</td>
      <td>Success rate percentage</td>
    </tr>
    <tr>
      <td>sent</td>
      <td>Integer</td>
      <td>Sent count</td>
    </tr>
    <tr>
      <td>failed</td>
      <td>Integer</td>
      <td>Failed count</td>
    </tr>
    <tr>
      <td>read</td>
      <td>Integer</td>
      <td>Read count</td>
    </tr>
    <tr>
      <td>readRate</td>
      <td>String</td>
      <td>Read rate percentage</td>
    </tr>
    <tr>
      <td>clicked</td>
      <td>Integer</td>
      <td>Clicked count</td>
    </tr>
    <tr>
      <td>clickRate</td>
      <td>String</td>
      <td>Click-through rate percentage</td>
    </tr>
    <tr>
      <td>revenue</td>
      <td>String</td>
      <td>Revenue generated</td>
    </tr>
    <tr>
      <td>purchase</td>
      <td>Integer</td>
      <td>Purchase count</td>
    </tr>
    <tr>
      <td>tags</td>
      <td>Array of String</td>
      <td>Tags added to contacts</td>
    </tr>
  </tbody>
</Table>

### Success Response - HTTP Status 200

```json
{
  "content": [
    {
      "id": "67890abcdef12345",
      "platform": "line",
      "channelId": "1657703186",
      "channelName": "My LINE Channel",
      "subject": "Promotion Campaign",
      "recipientType": 3,
      "type": 3,
      "mode": "manual",
      "sentAt": "2024-01-15T10:30:00",
      "status": 1,
      "recipientCount": 100,
      "success": 95,
      "successRate": "95.00%",
      "sent": 100,
      "failed": 5,
      "read": 50,
      "readRate": "52.63%",
      "clicked": 20,
      "clickRate": "21.05%",
      "revenue": "10000.00",
      "purchase": 5,
      "tags": ["promotion"]
    }
  ],
  "totalElements": 1
}
```

---

# Get Broadcast Detail

Get detailed information about a specific broadcast job.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/broadcast/{id}`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |

## Path Parameters

| Parameter | Type | Required | Description |
| :-------- | :--- | :------- | :---------- |
| id | String | Yes | Broadcast job ID |

## Response Body

Extends the Broadcast Object with additional fields:

| Field | Type | Description |
| :---- | :--- | :---------- |
| responded | Integer | Responded count |
| respondRate | String | Respond rate percentage |
| unsubscribed | Integer | Unsubscribed count |
| unsubscribeRate | String | Unsubscribe rate percentage |
| cost | String | Cost generated |
| roas | String | Return on Ad Spend |
| messageCount | Integer | Total messages to send |
| messageSuccess | Integer | Messages successfully sent |
| messageSuccessRate | String | Message success rate |
| respondedWithin12Hour | Integer | Responded within 12 hours |
| respondedWithin24Hour | Integer | Responded within 24 hours |
| respondedWithin48Hour | Integer | Responded within 48 hours |
| responseRateWithin12Hour | String | Response rate within 12 hours |
| responseRateWithin24Hour | String | Response rate within 24 hours |
| responseRateWithin48Hour | String | Response rate within 48 hours |

### Success Response - HTTP Status 200

```json
{
  "id": "67890abcdef12345",
  "platform": "line",
  "channelId": "1657703186",
  "channelName": "My LINE Channel",
  "subject": "Promotion Campaign",
  "status": 1,
  "recipientCount": 100,
  "success": 95,
  "successRate": "95.00%",
  "responded": 30,
  "respondRate": "31.58%",
  "unsubscribed": 2,
  "unsubscribeRate": "2.11%",
  "cost": "500.00",
  "roas": "20.00",
  "messageCount": 100,
  "messageSuccess": 95,
  "messageSuccessRate": "95.00%",
  "respondedWithin12Hour": 20,
  "respondedWithin24Hour": 25,
  "respondedWithin48Hour": 30
}
```

### Failed Response - HTTP Status 404

```json
{
  "errorCode": "BROADCAST_NOT_FOUND",
  "message": "Broadcast not found"
}
```

---

# Get Broadcast Recipients

Get the recipient list for a specific broadcast job.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/broadcast/{id}/recipients`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |

## Path Parameters

| Parameter | Type | Required | Description |
| :-------- | :--- | :------- | :---------- |
| id | String | Yes | Broadcast job ID |

## Query Parameters

| Parameter | Type | Required | Description |
| :-------- | :--- | :------- | :---------- |
| status | String | No | Status filter: `failed`, `read`, `clicked`, `responded`, `success`, `notDelivered`, `unsubscribed` |
| page | Integer | No | Page number. Default: 1 |
| pageSize | Integer | No | Page size (1-100). Default: 10 |

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | Array of Recipient | List of recipients |
| totalElements | Integer | Total number of records |

### Recipient Object

| Field | Type | Description |
| :---- | :--- | :---------- |
| name | String | Recipient name |
| phone | String | Recipient phone |
| success | Boolean | Whether message was sent successfully |
| sentAt | String | Sent time |
| read | Boolean | Whether message was read |
| readAt | String | Read time |
| clicked | Boolean | Whether message was clicked |
| clickedAt | String | Clicked time |
| responded | Boolean | Whether recipient responded |
| respondedAt | String | Responded time |
| messageId | String | Message ID |
| error | String | Error message (if failed) |

### Success Response - HTTP Status 200

```json
{
  "content": [
    {
      "name": "John Doe",
      "phone": "85298765432",
      "success": true,
      "sentAt": "2024-01-15T10:30:00",
      "read": true,
      "readAt": "2024-01-15T10:35:00",
      "clicked": true,
      "clickedAt": "2024-01-15T10:36:00",
      "responded": false,
      "respondedAt": null,
      "messageId": "msg123456",
      "error": null
    }
  ],
  "totalElements": 1
}
```

---

# Get Click Statistics of Buttons

Get click statistics for buttons in a broadcast message.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/broadcast/{broadcast_id}/buttons`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |

## Path Parameters

| Parameter | Type | Required | Description |
| :-------- | :--- | :------- | :---------- |
| broadcast_id | String | Yes | Broadcast job ID |

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | Array | List of button click statistics |

### Click Statistics Object

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
      <td>messageIndex</td>
      <td>Integer</td>
      <td>Index of the message this button belongs to (starting from 0)</td>
    </tr>
    <tr>
      <td>cardIndex</td>
      <td>Integer</td>
      <td>Index of the card for card-type messages; otherwise 0</td>
    </tr>
    <tr>
      <td>buttonIndex</td>
      <td>Integer</td>
      <td>Index of the button (starting from 1). 0 refers to card's default action (image tap)</td>
    </tr>
    <tr>
      <td>clickedCount</td>
      <td>Integer</td>
      <td>Total number of clicks</td>
    </tr>
    <tr>
      <td>clickedPercentage</td>
      <td>String</td>
      <td>Percentage of total clicks (e.g., "23.45%")</td>
    </tr>
  </tbody>
</Table>

### Success Response - HTTP Status 200

```json
{
  "content": [
    {
      "messageIndex": 0,
      "cardIndex": 0,
      "buttonIndex": 1,
      "clickedCount": 50,
      "clickedPercentage": "62.50%"
    },
    {
      "messageIndex": 0,
      "cardIndex": 0,
      "buttonIndex": 2,
      "clickedCount": 30,
      "clickedPercentage": "37.50%"
    }
  ]
}
```

### Failed Response - HTTP Status 404

```json
{
  "errorCode": "BROADCAST_NOT_FOUND",
  "message": "Broadcast not found"
}
```
