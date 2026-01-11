---
title: Rooms APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
# Rooms APIs

APIs for managing chat rooms.

## Subscription Required

| Feature Toggle | Description |
|----------------|-------------|
| `open_api_crm` | CRM Open API Module - Required for Assign Agent API |
| `open_api_omo` | OMO Open API Module - Required for Assign Agent API |
| `open_api_3rd_party_ai_agent` | 3rd-party AI Agent Open API Module - Required for To Human Agent API |

---

# Assign Agent

Assign a follow-up agent to a chat room.

## Endpoint

**POST** `https://open-api.omnichat.ai/v1/rooms/assign-agent`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |
| Content-Type | application/json | - |

## Request Body

| Field | Type | Required | Description |
| :---- | :--- | :------- | :---------- |
| platform | String | Yes | Messaging platform: `line`, `facebook`, `whatsapp`, `instagram`, `wechat`, `webchat` |
| channelId | String | Yes | Channel ID |
| recipientId | String | Yes | Contact's user ID |
| agentId | String | No | Agent's username (UUID). If not provided, room will be unassigned |

## Request Example

```json
{
    "platform": "line",
    "channelId": "1657703186",
    "recipientId": "U2bd582c37356d37cb6d46a823de3a908",
    "agentId": "1d9e3925-f08c-4236-92ef-b4c5394c9a14"
}
```

## Response Body

### Success - 204

HTTP Status 204 with empty response body

### Failed - HTTP Status 4xx / 5xx

```json
{
    "errorCode": "INVALID_REQUEST_BODY",
    "message": "Invalid request body"
}
```

---

# To Human Agent API

Transfer a conversation from AI agent to human agent.

## Endpoint

**POST** `https://open-api.omnichat.ai/v1/rooms/to-human-agent`

## Request Body

| Field  | Type   | Required | Description                      |
| :----- | :----- | :------- | :------------------------------- |
| roomId | String | Y        | ID of the chat room to hand-over |
| team   | String | Y        | Team account ID                  |

## Request Example

```json
{
    "roomId": "67ffde199a2d2ebc4714d41c", 
    "team": "TEAM-ID"
}
```

## Response Body

### Success - 204

Successfully set room to live chat.

### Failed - 400 Bad Request

Room is not allowed to assign to human

```
{
    "errorCode": "NOT_ALLOWED_ASSIGN_TO_HUMAN",
    "message": ""
}
```

### Failed - 404 Not Found

Specific room does not exist

```
{
    "errorCode": "ROOM_NOT_FOUND",
    "message": ""
}
```
