---
title: Rooms APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

# To Human Agent API

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/rooms/to-human-agent](https://open-api.omnichat.ai/v1/rooms/to-human-agent)

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
