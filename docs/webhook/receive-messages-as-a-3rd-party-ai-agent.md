---
title: Receive Messages as a 3rd-party AI Agent
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

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

        * `ai-session:open`: Start to chat with AI agent, message webhook will be sent upon received this event
        * `message:new`: Customer / User send a message
        * `ai-session:close`:
          End up chat with AI agent, no message webhooks will be sent until next ai-session is open |
          | payload | Payload | N | Event payload |  |
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

| Field               | Type   | Nullable | Description                               | Remark                         |
| ------------------- | ------ | -------- | ----------------------------------------- | ------------------------------ |
| id                  | String | N        | Channel ID                                |                                |
| externalId          | String | N        | Actual Channel ID to platform             |                                |
| currentUrl          | String | N        | URL to current page which user is viewing | Valid if platform is `webchat` |
| platform            | String | N        | Platform name                             | Possible values:               |
| `webchat`: Web chat |        |          |                                           |                                |
| metadata            | Object | N        | Metadata                                  | Currently not available        |

### `Room` Object

<Table>
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
        Room ID
      </td>

      <td>

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
        Room type
      </td>

      <td>
        Possible values:  
        `individual`: 1-on-1 conversation
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
        (Currently not available)
      </td>
    </tr>
  </tbody>
</Table>

### `Message` Object

| Field      | Type    | Nullable | Description                 | Remark                      |
| ---------- | ------- | -------- | --------------------------- | --------------------------- |
| id         | String  | N        | Message ID                  |                             |
| replyToken | String  | Y        | Reply token for line        | required for LINE messaging |
| createdAt  | String  | N        | Message timestamp           | ISO 8601                    |
| sender     | Sender  | N        | Sender information          |                             |
| content    | Content | N        | Message content information |                             |

### `Sender` Object

<Table>
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
        Sender ID
      </td>

      <td>
        Customer or teammate username in Omnichat
      </td>
    </tr>

    <tr>
      <td>
        externalId
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Sender actual user ID
      </td>

      <td>
        User ID in Omnichat
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
        Sender type
      </td>

      <td>
        Possible values:  
        `customer`  
        `agent`  
        `bot`
      </td>
    </tr>

    <tr>
      <td>
        senderName
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Sender name
      </td>

      <td>

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

<br />

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

        * `text`
        * `image`
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
        Message content url for media
      </td>

      <td>
        not null if type = `image`
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

<br />

<br />
