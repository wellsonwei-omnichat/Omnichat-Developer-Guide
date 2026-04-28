---
title: Copy of Business-Scoped User IDs API & Webhook Updates
excerpt: >-
  Review the WhatsApp BSUID webhook updates, including affected payloads, field
  definitions, and JSON examples for each webhook topic.
deprecated: false
hidden: true
metadata:
  robots: noindex
---
# Business-Scoped User ID (BSUID) — Webhook Updates

WhatsApp will launch a [Usernames feature](https://developers.facebook.com/documentation/business-messaging/whatsapp/business-scoped-user-ids?) later this year. When enabled by users, phone numbers might not be included in Message Webhooks. In response, Omnichat will add a new `bsuid` field to the affected webhook payloads.

**BSUIDs will begin appearing in webhooks in early May 2026.**

## Overview

| Property            | Detail                                             |
| :------------------ | :------------------------------------------------- |
| Field name          | `bsuid`                                            |
| Type                | String                                             |
| Nullable            | Yes — omitted from the payload when not applicable |
| Applicable platform | WhatsApp only                                      |

> **Note:** `bsuid` appears only for WhatsApp contacts. For all other platforms the field is absent. When a WhatsApp user enables the Username feature, `userId` (phone number) **may become `null`** while `bsuid` is populated. Both fields can also be present simultaneously. Please ensure your integration handles `null` values for `userId` on WhatsApp events.

***

## customer/create and customer/update

`bsuid` is added inside each entry of the `socialContacts` array for WhatsApp contacts.

### Updated: Customer's social channel contact information

| Field     | Description                                                                                                              | Type       | Nullable |
| :-------- | :----------------------------------------------------------------------------------------------------------------------- | :--------- | :------- |
| platform  | Platform name. Possible values: **line**, **facebook**, **instagram**, or **whatsapp**                                   | String     |          |
| channelId | Channel ID / WhatsApp Business Phone Number                                                                              | String     |          |
| userId    | Social Messenger Channel User ID (LINE User ID / Facebook PSID / Instagram IGSID / WhatsApp Phone Number)                | String     | Yes      |
| **bsuid** | **WhatsApp Business-Scoped User ID. Only present for WhatsApp contacts when the user has enabled the Username feature.** | **String** | **Yes**  |

### Updated JSON example

```json
{
  "memberId": "bruce001",
  "omniCustomerId": "67c7f3a056c62166b9cdaab8",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "name": "Bruce Ni",
  "tags": [
    "FB keyword auto reply add tag"
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
      "userId": "8526543210",    // CHANGED: may be null when WhatsApp Username feature is enabled
      "bsuid": "US.13491208655302741918"    // ADDED
    }
  ],
  "createdAt": "2023-11-09T14:09:57.511+08:00",
  "updatedAt": "2023-11-09T17:53:08.734+08:00"
}
```

***

## customer/channel_subscribe and customer/channel_unsubscribe

`bsuid` is added as a top-level field for WhatsApp subscribe / unsubscribe events.

### Updated Data Change Object Structure

| Field     | Description                                                                                                     | Type       | Nullable |
| :-------- | :-------------------------------------------------------------------------------------------------------------- | :--------- | :------- |
| memberId  | Customer's unique ID                                                                                            | String     |          |
| email     | Customer's email                                                                                                | String     |          |
| phone     | Customer's phone                                                                                                | String     |          |
| name      | Customer's name                                                                                                 | String     |          |
| platform  | Contact platform name. Possible values: **line**, **facebook**, **instagram**, or **whatsapp**                  | String     |          |
| channelId | Contact channel ID / WABA Phone Number (WhatsApp)                                                               | String     |          |
| userId    | Contact user ID / User Phone Number (WhatsApp)                                                                  | String     | Yes      |
| **bsuid** | **WhatsApp Business-Scoped User ID. Only present for WhatsApp when the user has enabled the Username feature.** | **String** | **Yes**  |

### Updated JSON example

```json
{
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "name": "Bruce Ni",
  "platform": "whatsapp",
  "channelId": "85298765432",
  "userId": "8526543210",    // CHANGED: may be null when WhatsApp Username feature is enabled
  "bsuid": "US.13491208655302741918"    // ADDED
}
```

***

## customer/channel_omo_binding

`bsuid` is added as a top-level field for WhatsApp OMO binding events.

### Updated Data Change Object Structure

| Field             | Description                                                                                                     | Type       | Nullable |
| :---------------- | :-------------------------------------------------------------------------------------------------------------- | :--------- | :------- |
| platform          | Messaging Platform. Supported values: `line`, `whatsapp`                                                        | String     |          |
| channelId         | Messaging Platform Channel ID                                                                                   | String     |          |
| userId            | Customer's User ID (LINE User ID / WhatsApp Phone Number)                                                       | String     | Yes      |
| **bsuid**         | **WhatsApp Business-Scoped User ID. Only present for WhatsApp when the user has enabled the Username feature.** | **String** | **Yes**  |
| memberId          | Customer's unique ID                                                                                            | String     | Yes      |
| email             | Customer's email                                                                                                | String     | Yes      |
| phone             | Customer's phone                                                                                                | String     | Yes      |
| agentId           | The agent's system ID                                                                                           | String     | Yes      |
| agentName         | The agent name of the agent bound to the customer                                                               | String     | Yes      |
| agentEmail        | The Omnichat login email of the agent bound to the customer                                                     | String     | Yes      |
| agentPhone        | The Omnichat login phone of the agent bound to the customer                                                     | String     | Yes      |
| agentEmployeeCode | The employee code of the agent bound to the customer                                                            | String     | Yes      |
| agentLocationName | The shop location name of the agent bound to the customer                                                       | String     | Yes      |
| agentLocationCode | The shop location code of the agent bound to the customer                                                       | String     | Yes      |
| agentPhotoUrl     | The agent's photo                                                                                               | String     | Yes      |

### Updated JSON example

```json
{
  "platform": "whatsapp",
  "channelId": "85298765432",
  "userId": "8526543210",    // CHANGED: may be null when WhatsApp Username feature is enabled
  "bsuid": "US.13491208655302741918",    // ADDED
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

***

## direct_msg/status

`bsuid` is added as a top-level field for WhatsApp Direct Message status events.

### Updated Data Change Object Structure

| Field      | Description                                                                                                     | Type       | Nullable |
| :--------- | :-------------------------------------------------------------------------------------------------------------- | :--------- | :------- |
| trackId    | Message track ID                                                                                                | String     |          |
| messageIds | Message IDs                                                                                                     | Array      |          |
| platform   | Contact platform name. Possible values: **line**, **facebook**, **instagram**, or **whatsapp**                  | String     |          |
| channelId  | Contact channel ID / WABA Phone Number (WhatsApp)                                                               | String     |          |
| userId     | Contact user ID / User Phone Number (WhatsApp)                                                                  | String     |          |
| memberId   | Customer's unique ID                                                                                            | String     |          |
| email      | Customer's email                                                                                                | String     |          |
| phone      | Customer's phone                                                                                                | String     |          |
| status     | Message status                                                                                                  | String     |          |
| **bsuid**  | **WhatsApp Business-Scoped User ID. Only present for WhatsApp when the user has enabled the Username feature.** | **String** | **Yes**  |

### Updated JSON example

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
  "bsuid": "US.13491208655302741918"    // ADDED
}
```

***

## whatsapp_flow/flow_create

`bsuid` is added as a top-level field when customers complete a WhatsApp Flow form.

### Updated Data Change Object Structure

| Field        | Description                                                                                                                                                                            | Type       | Nullable |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------- | :------- |
| name         | Customer's name                                                                                                                                                                        | String     | Yes      |
| phone        | Customer's phone                                                                                                                                                                       | String     |          |
| **bsuid**    | **WhatsApp Business-Scoped User ID. Only present when the user has enabled the Username feature.**                                                                                     | **String** | **Yes**  |
| flowId       | WhatsApp flow's ID                                                                                                                                                                     | String     |          |
| flowName     | WhatsApp flow's Name                                                                                                                                                                   | String     |          |
| responseTime | Customer response time                                                                                                                                                                 | String     |          |
| flowResponse | The original response from WhatsApp. See `interactive.nfm_reply.response_json` in the [Meta Official Doc](https://developers.facebook.com/docs/whatsapp/flows/reference/flowswebhooks) | Object     |          |

### Updated JSON example

```json
{
  "name": "Omnichat",
  "phone": "85261234567",
  "bsuid": "US.13491208655302741918",    // ADDED
  "flowId": "1234567890",
  "flowName": "Example Flow",
  "responseTime": "2024-07-01T17:42:24.333+08:00",
  "flowResponse": {
    "Example Column 1": ["0", "1", "2"],
    "Example Column 2": ["0"]
  }
}
```

***

## ticket/create and ticket/update

`bsuid` is added as a top-level field for WhatsApp ticket events.

### Updated Data Change Object Structure

| Field               | Description                                                                                                     | Type       | Nullable |
| :------------------ | :-------------------------------------------------------------------------------------------------------------- | :--------- | :------- |
| ticketId            | A sequence number                                                                                               | Integer    |          |
| subject             | The subject of this ticket                                                                                      | String     |          |
| customerName        | Customer's name                                                                                                 | String     |          |
| isGroupChat         | Flag used to determine if the ticket is related to a group chat                                                 | Boolean    |          |
| isCollaborationChat | Flag used to determine if the ticket is related to a collaboration chat                                         | Boolean    |          |
| platform            | Supported values: `webchat`, `line`, `whatsapp`, `wechat`, `instagram`, `facebook`                              | String     |          |
| channelId           | Contact channel ID / WABA Phone Number (WhatsApp)                                                               | String     |          |
| userId              | Contact user ID / User Phone Number (WhatsApp)                                                                  | String     |          |
| **bsuid**           | **WhatsApp Business-Scoped User ID. Only present for WhatsApp when the user has enabled the Username feature.** | **String** | **Yes**  |
| status              | Supported values: `Open`, `InProgress`, `Closed`                                                                | String     |          |
| createdAt           | Creation time                                                                                                   | String     |          |
| closedAt            | Closed time when the ticket status is `Closed`. Always `null` for `ticket/create`                               | String     | Yes      |
| firstFollowUpAt     | First follow-up time                                                                                            | String     |          |
| firstResponseAt     | The first response time of this ticket                                                                          | String     |          |
| agentLogs           | List of Agent Logs. Default is an empty array                                                                   | Array      |          |

### Updated JSON example — create

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
  "bsuid": "US.13491208655302741918",    // ADDED
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

***

## Webhooks Not Affected

The following webhook topics are **not** affected by BSUID changes:

* `broadcast_msg/status`
* `customer/channel_phone_binding`
* `lon/send_sms`
* `ticket/delete`

***

## Change Log

| Date       | Change                                                                                                                                                                                                                                                         |
| :--------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2026/05/06 | Added `bsuid` field to `customer/create`, `customer/update`, `customer/channel_subscribe`, `customer/channel_unsubscribe`, `customer/channel_omo_binding`, `direct_msg/status`, `whatsapp_flow/flow_create`, `ticket/create`, `ticket/update` webhook payloads |
