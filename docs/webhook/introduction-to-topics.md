---
title: Introduction to Topics
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
<br />

This document will introduce various events related to the topics we provide, as well as the fields in the data change object that will be sent during event notifications.

# customer/create and customer/update

Events related to this topic occur when a new customer is created in your team or when the data of an existing customer is updated.

In addition to directly adding a new customer, the following scenarios also create a new customer:

* When a new contact is generated within your integrated social platform channels.
* When a visitor logs into your website for the first time (requires chat plugin installation).
* When a customer service agent manually enters a phone or email for a contact in a website conversation in the Omnichat Admin Panel.

The following actions are considered as updating customer data:

* Updating the values in the email, phone, and name fields.
* Adding or removing tags.
* Changes in the values of custom attributes.
* Adding or removing contact channels.
* Adding a new website session (occurs when a customer logs in with a new browser).
* Logging into your website.

Note: Bulk operations (e.g., importing customers) temporarily do not support sending event notifications.

## Data Change Object Structure

| Field            | Description                                   |
| :--------------- | :-------------------------------------------- |
| memberId         | Customer's unique ID                          |
| omniCustomerId   | Omnichat customer ID                          |
| email            | Customer's email                              |
| phone            | Customer's phone                              |
| name             | Customer's name                               |
| tags             | Customer's tags                               |
| customAttributes | Customer's custom attributes                  |
| socialContacts   | Customer's social channel contact information |
| createdAt        | Creation time                                 |
| updatedAt        | Last modification time                        |

### Customer's custom attributes

| Field | Description     |
| :---- | :-------------- |
| key   | Attribute key   |
| value | Attribute value |

### Customer's social channel contact information

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        platform
      </td>

      <td>
        Platform name Possible values: **line**, **facebook**, **instagram**, or **whatsapp**
      </td>
    </tr>

    <tr>
      <td>
        channelId
      </td>

      <td>
        Channel ID / WhatsApp Business Phone Number
      </td>
    </tr>

    <tr>
      <td>
        userId
      </td>

      <td>
        Social Messenger Channel User ID

        * LINE: LINE User ID
        * Facebook: Facebook PSID
        * Instagram: Instagram IGSID
        * WhatsApp: User Phone Number. May be `null` when the WhatsApp user enables the Username feature
      </td>
    </tr>

    <tr>
      <td>
        bsuid
      </td>

      <td>
        WhatsApp Business-Scoped User ID. Only present for WhatsApp contacts. May be `null`
      </td>
    </tr>
  </tbody>
</Table>

## Data Change Object Example

```json
{
   "memberId": "bruce001",
   "omniCustomerId": "67c7f3a056c62166b9cdaab8",
   "email": "bruce.ni@omnichat.ai",
   "phone": "886987654321",
   "name": "Bruce Ni",
   "tags": [
      "FB keyword auto reply add tag",
      "FB chatroom add tag",
      "FB broadcast add tag"
   ],
   "customAttributes": [
      {
         "key": "membership_tier",
         "value": "Bronze"
      }
   ],
   "socialContacts": [
      {
         "platform": "whatsapp",
         "channelId": "85298765432",
         "userId": "8526543210",
         "bsuid": "US.13491208655302741918"
      }
   ],
   "createdAt": "2023-11-09T14:09:57.511+08:00",
   "updatedAt": "2023-11-09T17:53:08.734+08:00"
}
```

# customer/channel_subscribe

# customer/channel_unsubscribe

Events related to this topic occur when customers **subscribe** or **unsubscribe** within the social platform channels you have integrated.

The following actions are considered as **subscription** and **unsubscription**:

* Customers click the **subscribe** or **unsubscribe** buttons on chatbot messages.
* Customers send a message for the first time on Facebook, Instagram, or Whatsapp channels, which is considered as **subscribe**.
* Customers leave a comment for the first time on Facebook Post, Instagram Post, or Instagram Story, which is considered as **subscribe**.
* Customers **add** or **unblock** on Line channels, which is considered as **subscribe**.
* Customers **block** on Line channels, which is considered as **unsubscribe**.
* Other non-customer-initiated actions, e.g., manually adding Whatsapp contacts in the Omnichat Admin Panel.

Note: Bulk operations (e.g., importing customers) temporarily do not support sending event notifications.

## Data Change Object Structure

| Field     | Description                                                                                                       |
| :-------- | :---------------------------------------------------------------------------------------------------------------- |
| memberId  | Customer's unique ID                                                                                              |
| email     | Customer's email                                                                                                  |
| phone     | Customer's phone                                                                                                  |
| name      | Customer's name                                                                                                   |
| platform  | Contact platform name (The value could be one of **line**, **facebook**, **instagram**, or **whatsapp**)          |
| channelId | Contact channel ID / WABA Phone Number (Whatsapp)                                                                 |
| userId    | Contact user ID / User Phone Number (Whatsapp). May be `null` when the WhatsApp user enables the Username feature |
| bsuid     | WhatsApp Business-Scoped User ID. Only present for WhatsApp. May be `null`                                        |

## Data Change Object Example

```json
{
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "name": "Bruce Ni",
  "platform": "whatsapp",
  "channelId": "85298765432",
  "userId": "8526543210",
  "bsuid": "US.13491208655302741918"
}
```

# customer/channel_phone_binding

Events related to this topic occur when customers within the social platform channels you have integrated have successfully completed phone binding.

## Data Change Object Structure

| Field     | Description                                           |
| :-------- | :---------------------------------------------------- |
| platform  | Platform identifier (Currently only support **line**) |
| channelId | Contact channel ID                                    |
| userId    | Contact user ID                                       |
| phone     | Customer's phone                                      |

## Data Change Object Example

```json
{
  "platform": "line",
  "channelId": "1656935362",
  "userId": "U36bd7222a92b5cb04e4716f0c9c0dea6",
  "phone": "886987654321"
}
```

# customer/channel_omo_binding

Events related to this topic occur when

1. A customer completed or unbound OMO binding in the social messaging platform.
2. The binding agent is updated.

## Data Change Object Structure

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Description
      </th>

      <th>
        Type
      </th>

      <th>
        Nullable
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        platform
      </td>

      <td>
        Messaging Platform.

        Supported values:

        * `line`
        * `whatsapp`
      </td>

      <td>
        String
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        channelId
      </td>

      <td>
        Messaging Platform Channel ID.

        * For `line` → LINE Messaging Channel ID
        * For `whatsapp` → WhatsApp Business Phone Number
      </td>

      <td>
        String
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        userId
      </td>

      <td>
        Customer's User ID.

        * For `line` → LINE User ID
        * For `whatsapp` → WhatsApp Phone Number. May be `null` when the WhatsApp user enables the Username feature
      </td>

      <td>
        String
      </td>

      <td>
        Nullable (WhatsApp only)
      </td>
    </tr>

    <tr>
      <td>
        bsuid
      </td>

      <td>
        WhatsApp Business-Scoped User ID. Only present for WhatsApp
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>

    <tr>
      <td>
        memberId
      </td>

      <td>
        Customer's unique ID
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>

    <tr>
      <td>
        email
      </td>

      <td>
        Customer's email
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>

    <tr>
      <td>
        phone
      </td>

      <td>
        Customer's phone
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>

    <tr>
      <td>
        agentId
      </td>

      <td>
        The agent's system ID
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>

    <tr>
      <td>
        agentName
      </td>

      <td>
        The agent name of the agent bound to the customer
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>

    <tr>
      <td>
        agentEmail
      </td>

      <td>
        The Omnichat login email of the agent bound to the customer
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>

    <tr>
      <td>
        agentPhone
      </td>

      <td>
        The Omnichat login phone of the agent bound to the customer
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>

    <tr>
      <td>
        agentEmployeeCode
      </td>

      <td>
        The employee code of the agent bound to the customer
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>

    <tr>
      <td>
        agentLocationName
      </td>

      <td>
        The shop location name of the agent bound to the customer
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>

    <tr>
      <td>
        agentLocationCode
      </td>

      <td>
        The shop location code of the agent bound to the customer
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>

    <tr>
      <td>
        agentPhotoUrl
      </td>

      <td>
        The agent's photo
      </td>

      <td>
        String
      </td>

      <td>
        Nullable
      </td>
    </tr>
  </tbody>
</Table>

## Data Change Object Example

```json JSON
{
  "platform": "whatsapp",
  "channelId": "85298765432",
  "userId": "8526543210",
  "bsuid": "US.13491208655302741918",
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "agentName": "John Doe",
  "agentEmail": "john.doe@example.com",
  "agentPhone": "85256785678",
  "agentEmployeeCode": "S0001",
  "agentLocationName": "Shop A",
  "agentLocationCode": "SHOP-A",
  "agentPhotoUrl": "https://media-cdn.omnichat.ai/your_image.png"
}
```

# direct_msg/status

Events related to this topic occur when there is a status change after sending a Direct Message.

The various **statuses** are explained below:

* **delivered**: The message has been delivered to the recipient's device (applicable to Whatsapp only).
* **failed**: The message delivery to the recipient's device has failed (applicable to Whatsapp only).
* **read**: The message has been read (not applicable to text or image messages in Line).
* **clicked**: A button within the message has been clicked.
* **responded**: The message has been responded to.

## Data Change Object Structure

| Field      | Description                                                                                                       |
| :--------- | :---------------------------------------------------------------------------------------------------------------- |
| trackId    | Message track ID                                                                                                  |
| messageIds | Message IDs                                                                                                       |
| platform   | Contact platform name (The value could be one of **line**, **facebook**, **instagram**, or **whatsapp**)          |
| channelId  | Contact channel ID / WABA Phone Number (Whatsapp)                                                                 |
| userId     | Contact user ID / User Phone Number (Whatsapp). May be `null` when the WhatsApp user enables the Username feature |
| memberId   | Customer's unique ID                                                                                              |
| email      | Customer's email                                                                                                  |
| phone      | Customer's phone                                                                                                  |
| status     | Message status                                                                                                    |
| bsuid      | WhatsApp Business-Scoped User ID. Only present for WhatsApp. May be `null`                                        |

## Data Change Object Example

```json
{
  "trackId": "testing-event",
  "messageIds": [
    "testing-message-id"
  ],
  "platform": "whatsapp",
  "channelId": "85298765432",
  "userId": "8526543210",
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "status": "delivered",
  "bsuid": "US.13491208655302741918"
}
```

# whatsapp_flow/flow_create

Events related to this topic occur when customers complete the WhatsApp Flow form.

## Data Change Object Structure

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        name
      </td>

      <td>
        Customer's name
      </td>
    </tr>

    <tr>
      <td>
        phone
      </td>

      <td>
        Customer's phone. May be `null` when the WhatsApp user enables the Username feature
      </td>
    </tr>

    <tr>
      <td>
        bsuid
      </td>

      <td>
        WhatsApp Business-Scoped User ID. May be `null`
      </td>
    </tr>

    <tr>
      <td>
        flowId
      </td>

      <td>
        WhatsApp flow's ID
      </td>
    </tr>

    <tr>
      <td>
        flowName
      </td>

      <td>
        WhatsApp flow's Name
      </td>
    </tr>

    <tr>
      <td>
        responseTime
      </td>

      <td>
        Customer response time
      </td>
    </tr>

    <tr>
      <td>
        flowResponse
      </td>

      <td>
        The original response from WhatsApp See **interactive.nfm_reply.response_json** in

        [Meta Offical Doc](https://developers.facebook.com/docs/whatsapp/flows/reference/flowswebhooks)
      </td>
    </tr>
  </tbody>
</Table>

## Data Change Object Example

```json
{
  "name": "Omnichat",
  "phone": "85261234567",
  "bsuid": "US.13491208655302741918",
  "flowId": "1234567890",
  "flowName": "Example Flow",
  "responseTime": "2024-07-01T17:42:24.333+08:00",
  "flowResponse": {
    "Example Column 1":["0","1","2"],
    "Example Column 2":["0"]
  }
}
```

# lon/send_sms

Events related to this topic occur when Omnichat fails to receive the LON webhook within a specified date range.

## Data Change Object Structure

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        triggerId
      </td>

      <td>
        The ID of `Notification Message`, each call has 1 triggerId See

        [https://developers.omnichat.ai/docs/send-notification-messages-to-contacts](https://developers.omnichat.ai/docs/send-notification-messages-to-contacts)
      </td>
    </tr>

    <tr>
      <td>
        settingId
      </td>

      <td>
        Please `Copy 'Setting ID'` in

        [LINE NotiPress](https://console.omnichat.ai/line-notipress)
      </td>
    </tr>

    <tr>
      <td>
        settingName
      </td>

      <td>
        The `Name` of setting
      </td>
    </tr>

    <tr>
      <td>
        phone
      </td>

      <td>
        Customer's phone
      </td>
    </tr>

    <tr>
      <td>
        text
      </td>

      <td>
        The `SMS content` of setting
      </td>
    </tr>
  </tbody>
</Table>

## Data Change Object Example

```json
{
  "triggerId": "65eeb7e89282985332c3a3df",
  "settingId": "66f4f35520bad960157a5de4",
  "settingName": "Shipping Notification",
  "phone": "85261234567",
  "text": "Your order has been delivered."
}
```

# ticket/create

Events related to this topic occur when a chat-related ticket is created.

# ticket/update

Events related to this topic occur when a chat-related ticket is updated.

## Data Change Object Structure

| Field               | Description                                                                                                                            |
| :------------------ | :------------------------------------------------------------------------------------------------------------------------------------- |
| ticketId            | A sequence number                                                                                                                      |
| subject             | The subject of this ticket                                                                                                             |
| customerName        | Customer's name                                                                                                                        |
| isGroupChat         | Flag used to determine if the ticket is related to a group chat                                                                        |
| isCollaborationChat | Flag used to determine if the ticket is related to a collaboration chat `This flag is editable`                                        |
| platform            | Supported values: -`webchat` -`line` -`whatsapp` -`wechat` -`instagram` -`facebook`                                                    |
| channelId           | Contact channel ID / WABA Phone Number (Whatsapp)                                                                                      |
| userId              | Contact user ID / User Phone Number (Whatsapp). May be `null` when the WhatsApp user enables the Username feature                      |
| bsuid               | WhatsApp Business-Scoped User ID. Only present for WhatsApp. May be `null`                                                             |
| status              | Supported values: -`Open` -`InProgress` -`Closed`                                                                                      |
| createdAt           | Creation time                                                                                                                          |
| closedAt            | Closed time when the ticket status is set to `Closed`. Always be `null` for `ticket/create` webhook                                    |
| firstFollowUpAt     | Refer to these `actionType` -`FOLLOW_UP_FROM_OPEN` -`FOLLOW_UP_FROM_CHATBOT` -`REOPEN` -`NINEONEAPP_SYNC` -`WHATSAPP_ADD_CONVERSATION` |
| firstResponseAt     | The first response time of this ticket                                                                                                 |
| agentLogs           | List of `Agent Logs` Default is an empty array                                                                                         |

### Agent Logs

| Field      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| :--------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| agentId    | Agent's ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| agentName  | Agent's name                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| actionType | `NEW_ROOM` : New conversation created `FOLLOW_UP_FROM_OPEN` : Agent follows up the conversation from open case `FOLLOW_UP_FROM_CHATBOT` : Agent follows up the conversation from open chatbot case `TAKE_OVER` : Agent takes over the conversation from another agent `PASS` : The conversation is passed to another agent `REOPEN` : The conversation is reopened `NINEONEAPP_SYNC` : Agent follows up via 91App data sync `OMO_OVERWRITE` : Agent is changed due to users scan the OMO QRCode `WHATSAPP_ADD_CONVERSATION` : A new WhatsApp conversation is created by the agent `OMO_CLOSE_ASSIGN` : The bound sales agent becomes the follow-up agent when the conversation is closed |
| occurredAt | The time when action occurs                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

## Data Change Object Example - create

```json JSON
{
    "ticketId": 123,
    "subject": "2025-02-10 13:54:56",
    "customerName": "Omnichat",
    "isGroupChat": false,
    "isCollaborationChat": false,
    "platform": "whatsapp",
    "channelId": "85298765432",
    "userId": "8526543210",
    "bsuid": "US.13491208655302741918",
    "status": "Open",
    "createdAt": "2025-02-13T13:54:56.848+08:00",
    "closedAt": null,
    "firstFollowUpAt": "2025-02-10T13:54:56.848+08:00",
    "firstResponseAt": "2025-02-10T13:55:23.184+08:00",
    "agentLogs": [
        {
            "agentId": "8fc7e9e3-f742-4772-b918-02180f4a4403",
            "agentName": "Chris Sales",
            "actionType": "FOLLOW_UP_FROM_OPEN",
            "occurredAt": "2025-02-10T13:54:56.869+08:00"
        }
    ]
}
```

## Data Change Object Example - update

```json
{
    "ticketId": 123,
    "subject": "2025-02-10 13:54:56",
    "customerName": "Omnichat",
    "isGroupChat": false,
    "isCollaborationChat": false,
    "platform": "whatsapp",
    "channelId": "85298765432",
    "userId": "8526543210",
    "bsuid": "US.13491208655302741918",
    "status": "Closed",
    "createdAt": "2025-02-13T13:54:56.848+08:00",
    "closedAt": "2025-02-13T13:55:06.829+08:00",
    "firstFollowUpAt": "2025-02-10T13:54:56.848+08:00",
    "firstResponseAt": "2025-02-10T13:55:23.184+08:00",
    "agentLogs": [
        {
            "agentId": "8fc7e9e3-f742-4772-b918-02180f4a4403",
            "agentName": "Chris Sales",
            "actionType": "FOLLOW_UP_FROM_OPEN",
            "occurredAt": "2025-02-10T13:54:56.869+08:00"
        }
    ]
}
```

# ticket/delete

Events related to this topic occur when a chat-related ticket is deleted.

## Data Change Object Structure

| Field    | Description              |
| :------- | :----------------------- |
| ticketId | The ID of deleted ticket |

## Data Change Object Example

```json
{
    "ticketId": 123
}
```

# broadcast_msg/status

Events related to this topic occur when there is a status change after sending a Broadcast Message.

The various **statuses** are explained below:

* **read**: The message has been read (not applicable to text or image messages in Line).
* **clicked**: A button within the message has been clicked.
* **responded**: The message has been responded to.
* **unsubscribed**: The recipient unsubscribed after receiving the message.

## Data Change Object Structure

| Field       | Description                                               |
| :---------- | :-------------------------------------------------------- |
| broadcastId | Broadcast ID                                              |
| platform    | Contact platform name (Currently applicable to Line only) |
| channelId   | Contact channel ID                                        |
| userId      | Contact user ID                                           |
| memberId    | Customer's unique ID                                      |
| email       | Customer's email                                          |
| phone       | Customer's phone                                          |
| status      | Message status                                            |

## Data Change Object Example

```json
{
  "broadcastId": "b59b93d4-a179-4b32-ab75-dc573fae6004",
  "platform": "line",
  "channelId": "1656935362",
  "userId": "U36bd7222a92b5cb04e4716f0c9c0dea6",
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "status": "read"
}
```

```json
{
  "broadcastId": "b59b93d4-a179-4b32-ab75-dc573fae6004",
  "platform": "line",
  "channelId": "1656935362",
  "userId": "U36bd7222a92b5cb04e4716f0c9c0dea6",
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "status": "read"
}
```

<br />
