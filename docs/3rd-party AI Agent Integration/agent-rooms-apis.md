---
title: Agent Rooms APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
# To Human Agent

Hand over the chat from `AI Chat` to `Open - Human Agent`

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/rooms/to-human-agent](https://open-api.omnichat.ai/v1/rooms/to-human-agent)

## Request Body

| Field  | Type   | Required | Description                      |
| :----- | :----- | :------- | :------------------------------- |
| roomId | String | Y        | ID of the chat room to hand over |
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

Successfully set up a room from `AI chat` to `Open-human agent`.

### Failed - 400 Bad Request

The room is not allowed to be assigned to `Open-human agent`.

```json
{
    "errorCode": "NOT_ALLOWED_ASSIGN_TO_HUMAN",
    "message": ""
}
```

### Failed - 404 Not Found

A specific room does not exist

```json
{
    "errorCode": "ROOM_NOT_FOUND",
    "message": "Room does not exist, roomId: xxx"
}
```

<br />

# Close Case

Change the chat status from `AI Chat` to `Closed`

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/rooms/close](https://open-api.omnichat.ai/v1/rooms/close)

## Request Body

| Field  | Type   | Required | Description                      |
| :----- | :----- | :------- | :------------------------------- |
| roomId | String | Y        | ID of the chat room to be closed |
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

Successfully closed an `AI Chat` room.

### Failed - 400 Bad Request

The room cannot be closed.

(e.g., a chat room not in `AI Chat`, or it's a chat room with collaborating human agents.)

```json
{
    "errorCode": "INVALID_REQUEST_BODY",
    "message": "The room status is not supported, RoomStatus={statusCode}"
}
```

<br />

### Failed - 404 Not Found

A specific room does not exist

```json
{
    "errorCode": "NOT_FOUND",
    "message": "Can't find the Room={roomId} in team={teamId}"
}
```
