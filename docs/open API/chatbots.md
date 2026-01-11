---
title: Chatbot APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
# Chatbot APIs

Manage chatbots and their message blocks.

## Subscription Required

| Feature Toggle | Description |
|----------------|-------------|
| `open_api_marketing` | Marketing Open API Module - Required for all Chatbot endpoints |

---

# Get Chatbot List

Get the list of chatbots owned by your team.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/chatbots`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |

## Response Body

Array of `Chatbot` Objects wrapped in a `content` field.

### `Chatbot` Object

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>Field</th>
      <th>Type</th>
      <th>Nullable</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>id</td>
      <td>String</td>
      <td>N</td>
      <td>Chatbot ID (UUID format)</td>
    </tr>
    <tr>
      <td>name</td>
      <td>String</td>
      <td>N</td>
      <td>Chatbot name</td>
    </tr>
    <tr>
      <td>type</td>
      <td>Integer</td>
      <td>N</td>
      <td>
        Chatbot Type. Different messaging platforms have different message formats, so special message formats are only allowed in specific type chatbots.

        Possible values:
        - `1`: All Platform
        - `2`: Facebook / IG Only
        - `3`: LINE Only
        - `4`: Web Chat Only
        - `5`: For Abandoned Cart
        - `6`: For WhatsApp Only
      </td>
    </tr>
  </tbody>
</Table>

### Success Response - HTTP Status 200

```json
{
  "content": [
    {
      "id": "0031ab01-93b1-480a-9270-83b4f48c4229",
      "name": "LINE chatbot",
      "type": 3
    },
    {
      "id": "007898be-c595-4668-a6ba-1ab9c593cace",
      "name": "FB chatbot",
      "type": 2
    }
  ]
}
```

### Error Response - HTTP Status 4xx / 5xx

```json
{
  "errorCode": "INVALID_REQUEST_BODY",
  "message": "Invalid request body"
}
```

---

# Get Chatbot's Message Blocks

Get the list of message blocks for a specific chatbot.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/chatbots/{chatbotId}/message-blocks`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |

## Path Parameters

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
      <td>chatbotId</td>
      <td>String</td>
      <td>Yes</td>
      <td>Chatbot ID (UUID format)</td>
    </tr>
  </tbody>
</Table>

## Response Body

Array of `Message Block` Objects wrapped in a `content` field.

### `Message Block` Object

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>Field</th>
      <th>Type</th>
      <th>Nullable</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>id</td>
      <td>String</td>
      <td>N</td>
      <td>Message Block ID (UUID format)</td>
    </tr>
    <tr>
      <td>name</td>
      <td>String</td>
      <td>N</td>
      <td>Message Block name</td>
    </tr>
  </tbody>
</Table>

### Success Response - HTTP Status 200

```json
{
  "content": [
    {
      "id": "07269d7a-68d6-4f36-9c0b-c837d9b296ef",
      "name": "Promo 1 Block"
    },
    {
      "id": "0833e711-f607-42da-aff7-b566b2d760e9",
      "name": "Promo 2 Block"
    }
  ]
}
```

### Error Response - HTTP Status 4xx / 5xx

```json
{
  "errorCode": "CHATBOT_NOT_FOUND",
  "message": "Chatbot not found"
}
```

> 📘 Note
> If the chatbot exists but has no message blocks, the response will be an empty array in the `content` field.
