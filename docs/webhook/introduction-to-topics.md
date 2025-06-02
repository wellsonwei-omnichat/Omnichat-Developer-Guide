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
This document will introduce various events related to the topics we provide, as well as the fields in the data change object that will be sent during event notifications.

# customer/create and customer/update

Events related to this topic occur when a new customer is created in your team or when the data of an existing customer is updated.

In addition to directly adding a new customer, the following scenarios also create a new customer:

- When a new contact is generated within your integrated social platform channels.
- When a visitor logs into your website for the first time (requires chat plugin installation).
- When a customer service agent manually enters a phone or email for a contact in a website conversation in the Omnichat Admin Panel.

The following actions are considered as updating customer data:

- Updating the values in the email, phone, and name fields.
- Adding or removing tags.
- Changes in the values of custom attributes.
- Adding or removing contact channels.
- Adding a new website session (occurs when a customer logs in with a new browser).
- Logging into your website.

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

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Description",
    "0-0": "platform",
    "0-1": "Platform name  \nPossible values: **line**, **facebook**, **instagram**, or **whatsapp**",
    "1-0": "channelId",
    "1-1": "Channel ID / WhatsApp Business Phone Number",
    "2-0": "userId",
    "2-1": "Social Messenger Channel User ID  \n  \n- LINE: LINE User ID\n- Facebook: Facebook PSID\n- Instagram: Instagram IGSID\n- WhatsApp: User Phone Number"
  },
  "cols": 2,
  "rows": 3,
  "align": [
    "left",
    "left"
  ]
}
[/block]


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
         "platform": "facebook",
         "channelId": "101892172823806",
         "userId": "6037142306382747"
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

- Customers click the **subscribe** or **unsubscribe** buttons on chatbot messages.
- Customers send a message for the first time on Facebook, Instagram, or Whatsapp channels, which is considered as **subscribe**.
- Customers leave a comment for the first time on Facebook Post, Instagram Post, or Instagram Story, which is considered as **subscribe**.
- Customers **add** or **unblock** on Line channels, which is considered as **subscribe**.
- Customers **block** on Line channels, which is considered as **unsubscribe**.
- Other non-customer-initiated actions, e.g., manually adding Whatsapp contacts in the Omnichat Admin Panel.

Note: Bulk operations (e.g., importing customers) temporarily do not support sending event notifications.

## Data Change Object Structure

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Description",
    "0-0": "memberId",
    "0-1": "Customer's unique ID",
    "1-0": "email",
    "1-1": "Customer's email",
    "2-0": "phone",
    "2-1": "Customer's phone",
    "3-0": "name",
    "3-1": "Customer's name",
    "4-0": "platform",
    "4-1": "Contact platform name  \n(The value could be one of **line**, **facebook**, **instagram**, or **whatsapp**)",
    "5-0": "channelId",
    "5-1": "Contact channel ID / WABA Phone Number (Whatsapp)",
    "6-0": "userId",
    "6-1": "Contact user ID / User Phone Number (Whatsapp)"
  },
  "cols": 2,
  "rows": 7,
  "align": [
    "left",
    "left"
  ]
}
[/block]


## Data Change Object Example

```json
{
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "name": "Bruce Ni",
  "platform": "line",
  "channelId": "1656935362",
  "userId": "U36bd7222a92b5cb04e4716f0c9c0dea6"
}
```

# customer/channel_phone_binding

Events related to this topic occur when customers within the social platform channels you have integrated have successfully completed phone binding.

## Data Change Object Structure

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Description",
    "0-0": "platform",
    "0-1": "Platform identifier  \n(Currently only support **line**)",
    "1-0": "channelId",
    "1-1": "Contact channel ID",
    "2-0": "userId",
    "2-1": "Contact user ID",
    "3-0": "phone",
    "3-1": "Customer's phone"
  },
  "cols": 2,
  "rows": 4,
  "align": [
    "left",
    "left"
  ]
}
[/block]


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

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Description",
    "h-2": "Type",
    "h-3": "Nullable",
    "0-0": "platform",
    "0-1": "Messaging Platform.  \n  \nSupported values:  \n  \n- `line`\n- `whatsapp`",
    "0-2": "String",
    "0-3": "",
    "1-0": "channelId",
    "1-1": "Messaging Platform Channel ID.  \n  \n- For `line` → LINE Messaging Channel ID\n- For `whatsapp` → WhatsApp Business Phone Number",
    "1-2": "String",
    "1-3": "",
    "2-0": "userId",
    "2-1": "Customer's User ID.  \n  \n- For `line` → LINE User ID\n- For `whatsapp` → WhatsApp Phone Number",
    "2-2": "String",
    "2-3": "",
    "3-0": "memberId",
    "3-1": "Customer's unique ID",
    "3-2": "String",
    "3-3": "Nullable",
    "4-0": "email",
    "4-1": "Customer's email",
    "4-2": "String",
    "4-3": "Nullable",
    "5-0": "phone",
    "5-1": "Customer's phone",
    "5-2": "String",
    "5-3": "Nullable",
    "6-0": "agentName",
    "6-1": "The agent name of the agent bound to the customer",
    "6-2": "String",
    "6-3": "Nullable",
    "7-0": "agentEmail",
    "7-1": "The Omnichat login email of the agent bound to the customer",
    "7-2": "String",
    "7-3": "Nullable",
    "8-0": "agentPhone",
    "8-1": "The Omnichat login phone of the agent bound to the customer",
    "8-2": "String",
    "8-3": "Nullable",
    "9-0": "agentEmployeeCode",
    "9-1": "The employee code of the agent bound to the customer",
    "9-2": "String",
    "9-3": "Nullable",
    "10-0": "agentLocationName",
    "10-1": "The shop location name of the agent bound to the customer",
    "10-2": "String",
    "10-3": "Nullable",
    "11-0": "agentLocationCode",
    "11-1": "The shop location code of the agent bound to the customer",
    "11-2": "String",
    "11-3": "Nullable"
  },
  "cols": 4,
  "rows": 12,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


## Data Change Object Example

```json JSON
{
  "platform": "whatsapp",
  "channelId": "85298765432",
  "userId": "8526543210",
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "agentName": "John Doe",
  "agentEmail": "john.doe@example.com",
  "agentPhone": "85256785678",
  "agentEmployeeCode": "S0001",
  "agentLocationName": "Shop A",
  "agentLocationCode": "SHOP-A",
}
```

<br />

# direct_msg/status

Events related to this topic occur when there is a status change after sending a Direct Message.

The various **statuses** are explained below:

- **delivered**: The message has been delivered to the recipient's device (applicable to Whatsapp only).
- **failed**: The message delivery to the recipient's device has failed (applicable to Whatsapp only).
- **read**: The message has been read (not applicable to text or image messages in Line).
- **clicked**: A button within the message has been clicked.
- **responded**: The message has been responded to.

## Data Change Object Structure

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Description",
    "0-0": "trackId",
    "0-1": "Message track ID",
    "1-0": "messageIds",
    "1-1": "Message IDs",
    "2-0": "platform",
    "2-1": "Contact platform name  \n(The value could be one of **line**, **facebook**, **instagram**, or **whatsapp**)",
    "3-0": "channelId",
    "3-1": "Contact channel ID / WABA Phone Number (Whatsapp)",
    "4-0": "userId",
    "4-1": "Contact user ID / User Phone Number (Whatsapp)",
    "5-0": "memberId",
    "5-1": "Customer's unique ID",
    "6-0": "email",
    "6-1": "Customer's email",
    "7-0": "phone",
    "7-1": "Customer's phone",
    "8-0": "status",
    "8-1": "Message status"
  },
  "cols": 2,
  "rows": 9,
  "align": [
    "left",
    "left"
  ]
}
[/block]


## Data Change Object Example

```json
{
  "trackId": "testing-event",
  "messageIds": [
    "testing-message-id"
  ],
  "platform": "line",
  "channelId": "1656935362",
  "userId": "U36bd7222a92b5cb04e4716f0c9c0dea6",
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "status": "read"
}
```

# whatsapp_flow/flow_create

Events related to this topic occur when customers complete the WhatsApp Flow form.

## Data Change Object Structure

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Description",
    "0-0": "name",
    "0-1": "Customer's name",
    "1-0": "phone",
    "1-1": "Customer's phone",
    "2-0": "flowId",
    "2-1": "WhatsApp flow's ID",
    "3-0": "flowName",
    "3-1": "WhatsApp flow's Name",
    "4-0": "responseTime",
    "4-1": "Customer response time",
    "5-0": "flowResponse",
    "5-1": "The original response from WhatsApp  \nSee **interactive.nfm_reply.response_json** in [Meta Offical Doc](https://developers.facebook.com/docs/whatsapp/flows/reference/flowswebhooks)"
  },
  "cols": 2,
  "rows": 6,
  "align": [
    "left",
    "left"
  ]
}
[/block]


## Data Change Object Example

```json
{
  "name": "Omnichat",
  "phone": "85261234567",
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

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Description",
    "0-0": "triggerId",
    "0-1": "The ID of `Notification Message`, each call has 1 triggerId  \nSee <https://developers.omnichat.ai/docs/send-notification-messages-to-contacts>",
    "1-0": "settingId",
    "1-1": "Please `Copy 'Setting ID'` in [LINE NotiPress](https://console.omnichat.ai/line-notipress)",
    "2-0": "settingName",
    "2-1": "The `Name` of setting",
    "3-0": "phone",
    "3-1": "Customer's phone",
    "4-0": "text",
    "4-1": "The `SMS content` of setting"
  },
  "cols": 2,
  "rows": 5,
  "align": [
    "left",
    "left"
  ]
}
[/block]


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

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Description",
    "0-0": "ticketId",
    "0-1": "A sequence number",
    "1-0": "subject",
    "1-1": "The subject of this ticket",
    "2-0": "customerName",
    "2-1": "Customer's name",
    "3-0": "isGroupChat",
    "3-1": "Flag used to determine if the ticket is related to a group chat",
    "4-0": "isCollaborationChat",
    "4-1": "Flag used to determine if the ticket is related to a collaboration chat  \n`This flag is editable`",
    "5-0": "platform",
    "5-1": "Supported values:  \n-`webchat`  \n-`line`  \n-`whatsapp`  \n-`wechat`  \n-`instagram`  \n-`facebook`",
    "6-0": "channelId",
    "6-1": "Contact channel ID / WABA Phone Number (Whatsapp)",
    "7-0": "userId",
    "7-1": "Contact user ID / User Phone Number (Whatsapp)",
    "8-0": "status",
    "8-1": "Supported values:  \n-`Open`  \n-`InProgress`  \n-`Closed`",
    "9-0": "createdAt",
    "9-1": "Creation time",
    "10-0": "closedAt",
    "10-1": "Closed time when the ticket status is set to `Closed`.  \nAlways be `null` for `ticket/create` webhook",
    "11-0": "firstFollowUpAt",
    "11-1": "Refer to these `actionType`  \n-`FOLLOW_UP_FROM_OPEN`  \n-`FOLLOW_UP_FROM_CHATBOT`  \n-`REOPEN`  \n-`NINEONEAPP_SYNC`  \n-`WHATSAPP_ADD_CONVERSATION`",
    "12-0": "firstResponseAt",
    "12-1": "The first response time of this ticket",
    "13-0": "agentLogs",
    "13-1": "List of `Agent Logs`  \nDefault is an empty array"
  },
  "cols": 2,
  "rows": 14,
  "align": [
    "left",
    "left"
  ]
}
[/block]


### Agent Logs

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Description",
    "0-0": "agentId",
    "0-1": "Agent's ID",
    "1-0": "agentName",
    "1-1": "Agent's name",
    "2-0": "actionType",
    "2-1": "`NEW_ROOM` : New conversation created  \n`FOLLOW_UP_FROM_OPEN` : Agent follows up the conversation from open case  \n`FOLLOW_UP_FROM_CHATBOT` : Agent follows up the conversation from open chatbot case  \n`TAKE_OVER` : Agent takes over the conversation from another agent  \n`PASS` : The conversation is passed to another agent  \n`REOPEN` : The conversation is reopened  \n`NINEONEAPP_SYNC` : Agent follows up via 91App data sync  \n`OMO_OVERWRITE` : Agent is changed due to users scan the OMO QRCode  \n`WHATSAPP_ADD_CONVERSATION` : A new WhatsApp conversation is created by the agent  \n`OMO_CLOSE_ASSIGN` : The bound sales agent becomes the follow-up agent when the conversation is closed",
    "3-0": "occurredAt",
    "3-1": "The time when action occurs"
  },
  "cols": 2,
  "rows": 4,
  "align": [
    "left",
    "left"
  ]
}
[/block]


<br />

## Data Change Object Example - create

```json JSON
{
    "ticketId": 123,
    "subject": "2025-02-10 13:54:56",
    "customerName": "Omnichat",
    "isGroupChat": false,
    "isCollaborationChat": false,
    "platform": "line",
    "channelId": "e0c32549-e9b0-11ef-be98-029459aa0a08",
    "userId": "Ued81902b3a32475898b6b16f970686af",
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

<br />

## Data Change Object Example - update

```json
{
    "ticketId": 123,
    "subject": "2025-02-10 13:54:56",
    "customerName": "Omnichat",
    "isGroupChat": false,
    "isCollaborationChat": false,
    "platform": "line",
    "channelId": "e0c32549-e9b0-11ef-be98-029459aa0a08",
    "userId": "Ued81902b3a32475898b6b16f970686af",
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