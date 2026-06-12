---
title: Receive Messages from Webhook
excerpt: >-
  When a chat room is in `AI Chat`, the webhook will send message events when a
  customer interact with the channel.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Data Object

| Field | Type           | Nullable | Description      | Remark |
| ----- | -------------- | -------- | ---------------- | ------ |
| team  | Team           | N        | Team information |        |
| event | Array of Event | N        | Message events   |        |

### `Team` Object

| Field  | Type   | Nullable | Description | Remark             |
| ------ | ------ | -------- | ----------- | ------------------ |
| id     | String | N        | Team ID     | Identifier to team |
| locale | String | N        | Locale      |                    |

### `Event` Object

<Table align={["left","left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Nullable
      </th>

      <th>
        Description
      </th>

      <th>
        Remark
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        id
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Team ID
      </td>

      <td>
        Identifier to team
      </td>
    </tr>

    <tr>
      <td>
        createdAt
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Event timestamp
      </td>

      <td>
        ISO 8601
      </td>
    </tr>

    <tr>
      <td>
        type
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Event type
      </td>

      <td>
        Possible values:

        - `ai-session:open`: Start to chat with AI agent, message webhook will be sent upon receiving this event
        - `message:new`: Customer / User sends a message
        - `ai-session:close`:
          End up chat with AI agent, no message webhooks will be sent until the next ai-session is open
      </td>
    </tr>

    <tr>
      <td>
        payload
      </td>

      <td>
        Payload
      </td>

      <td>
        N
      </td>

      <td>
        Event payload
      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

### `Payload` Object

| Field   | Type    | Nullable | Description         | Remark |
| ------- | ------- | -------- | ------------------- | ------ |
| channel | Channel | N        | Channel information |        |
| room    | Room    | N        | room information    |        |
| message | Message | N        | Message information |        |

### `Channel` Object

| Field      | Type   | Nullable | Description                                      | Remark                                                                       |
| :--------- | :----- | :------- | :----------------------------------------------- | :--------------------------------------------------------------------------- |
| id         | String | N        | Channel ID                                       |                                                                              |
| externalId | String | N        | Actual Channel ID to the platform                |                                                                              |
| currentUrl | String | N        | URL to the current page that the user is viewing | Valid if the platform is `webchat`                                           |
| platform   | String | N        | Platform name                                    | Possible values:<br />`webchat`<br />`line`<br />`facebook`<br />`instagram` |
| metadata   | Object | N        | Metadata                                         | Currently not available                                                      |

### `Room` Object

| Field    | Type   | Nullable | Description | Remark                                                  |
| :------- | :----- | :------- | :---------- | :------------------------------------------------------ |
| id       | String | N        | Room ID     |                                                         |
| type     | String | N        | Room type   | Possible values:<br />`individual`: 1-on-1 conversation |
| metadata | Object | N        | Metadata    | (Currently not available)                               |

### `Message` Object

| Field      | Type    | Nullable | Description                 | Remark                      |
| ---------- | ------- | -------- | --------------------------- | --------------------------- |
| id         | String  | N        | Message ID                  |                             |
| replyToken | String  | Y        | Reply token for LINE        | required for LINE messaging |
| createdAt  | String  | N        | Message timestamp           | ISO 8601                    |
| sender     | Sender  | N        | Sender information          |                             |
| content    | Content | N        | Message content information |                             |

### `Sender` Object

| Field      | Type   | Nullable | Description                          | Remark                                                   |
| :--------- | :----- | :------- | :----------------------------------- | :------------------------------------------------------- |
| id         | String | N        | Sender ID                            |                                                          |
| externalId | String | N        | Sender's actual user ID in Omnichat. | Can be used for contact info query/update.               |
| type       | String | N        | Sender type                          | Possible values:<br />`customer`<br />`agent`<br />`bot` |
| senderName | String | N        | Sender name                          |                                                          |
| metadata   | Object | N        | Metadata                             |                                                          |

### `Content` Object

<Table align={["left","left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Nullable
      </th>

      <th>
        Description
      </th>

      <th>
        Remark
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        type
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Message type
      </td>

      <td>
        Possible values:

        - `text`
        - `image`
        - `file`
      </td>
    </tr>

    <tr>
      <td>
        text
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Message content
      </td>

      <td>
        not null if type = `text`
      </td>
    </tr>

    <tr>
      <td>
        url
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Message content URL for media
      </td>

      <td>
        not null if type = `image` or `file`
      </td>
    </tr>

    <tr>
      <td>
        metadata
      </td>

      <td>
        Object
      </td>

      <td>
        N
      </td>

      <td>
        Metadata
      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

## Data Object Example

### `text`

```json
{
    "team": {
      "id": "635753b278bf6600ffa4f37a",
      "locale": "zh-Hant",
    },
    "events": [
        {
      	    "id": "6800c938f5db472b153e2d9c",
            "createdAt": "2025-04-17T09:26:16.167Z",
            "type": "message:new",
            "payload": {
                "channel": {
                    "id": "fagagfafasfasfasfasf",
                    "externalId": "661e1adb55751a86cd162034",
                    "currentUrl": "https://www.example.com/item1",
                    "platform": "webchat",
                    "metadata": {}
                },
                "room": {
                    "id": "67ffde199a2d2ebc4714d41c",
                    "type": "individual",
                    "metadata": {}
                },
                "message": {
                    "id": "6800c93853ee2083547ca736",
                    "createdAt": "2025-04-17T09:26:16.167Z",
                    "sender": {
                        "id": "67ffdc02080b8449e1888888",
                        "externalId": "67ffdc02080b8449e14428d7",
                        "type": "customer",
                        "senderName": "強森學長",
                        "metadata": {}
                    },
                    "content": {
                        "type": "text",
                        "text": "hello",
                        "metadata": {}
                    }
				        }
            }
        }
    ]
}
```

### `image`

```json
{
    "team": {
        "id": "635753b278bf6600ffa4f37a",
        "locale": "zh-Hant",
    },
    "events": [
        {
            "id": "6800c938f5db472b153e2d9c",
            "createdAt": "2025-04-17T09:26:16.167Z",
            "type": "message:new",
            "payload": {
                "channel": {
                    "id": "fagagfafasfasfasfasf",
                    "externalId": "661e1adb55751a86cd162034",
                    "currentUrl": "https://www.example.com/item1",
                    "platform": "webchat",
                    "metadata": {}
                },
                "room": {
                    "id": "67ffde199a2d2ebc4714d41c",
                    "type": "individual",
                    "metadata": {}
                },
                "message": {
                    "id": "6800c93853ee2083547ca736",
                    "createdAt": "2025-04-17T09:26:16.167Z",
                    "sender": {
                        "id": "67ffdc02080b8449e1888888",
                        "externalId": "67ffdc02080b8449e14428d7",
                        "type": "customer",
                        "senderName": "強森學長",
                        "metadata": {}
                    },
                    "content": {
                        "type": "image",
                        "url": "hello",
                        "metadata": {}
                    }
                }
            }
        }
    ]
}
```

<br />
